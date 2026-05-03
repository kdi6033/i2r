# LCD35 — RP2040 + CrowPanel 3.5" IPS LCD HMI 템플릿

> **AI 프로그래밍 방법**  
> 아래 프롬프트를 Claude(또는 다른 AI)에 붙여넣고 원하는 동작을 한국어로 설명하면  
> AI가 소스를 직접 수정해 줍니다.
>
> ```
> https://raw.githubusercontent.com/kdi6033/i2r/main/LCD35.md 읽고 [원하는 동작을 한국어로 설명]
> ```
>
> **예시**
> - `LCD35.md 읽고 입력 채널을 8개로 늘려줘`
> - `LCD35.md 읽고 제어판 탭에 온도 게이지를 추가해줘`
> - `LCD35.md 읽고 출력 버튼 색상을 빨간색 계열로 바꿔줘`
> - `LCD35.md 읽고 탭3 메뉴얼에 내 유튜브 링크를 추가해줘`

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|------|------|
| MCU | Raspberry Pi RP2040 |
| 디스플레이 | CrowPanel 3.5" IPS ILI9488 (480×320) |
| 터치 | XPT2046 저항막 방식 |
| UI 라이브러리 | LVGL v9 |
| 통신 | Serial1 (UART, 9600 bps) — ESP32 PLC 연동 |
| 파일시스템 | LittleFS (설정 저장) |
| 한글 폰트 | NotoSansKR 20px |

**화면 구성 (탭 3개)**

```
┌────────────────────────────────┐
│  제어판  │  설정  │  메뉴얼    │  ← 탭바 (48px)
├────────────────────────────────┤
│  INPUT  LED ×4                 │
│  OUTPUT 버튼 ×4                │
│  [하단 상태바: WiFi MQTT 시각] │
└────────────────────────────────┘
```

---

## 2. 하드웨어 핀 배선 (User_Setup.h)

| 신호 | GPIO | 설명 |
|------|------|------|
| TFT_CS | 2 | LCD Chip Select |
| TFT_RST | 3 | LCD Reset |
| TFT_DC | 4 | Data/Command |
| TFT_MOSI | 11 | SPI1 TX (LCD + Touch 공유) |
| TFT_SCLK | 10 | SPI1 SCK (LCD + Touch 공유) |
| TFT_BL | 5 | 백라이트 (HIGH=ON) |
| TFT_MISO | 12 | SPI1 RX (Touch TDO) |
| TOUCH_CS | 6 | 터치 Chip Select |
| TOUCH_IRQ | 8 | 터치 인터럽트 |
| Serial1 TX | 0 | ESP32 RX 연결 |
| Serial1 RX | 1 | ESP32 TX 연결 |

---

## 3. 필요 라이브러리

Arduino IDE 라이브러리 매니저에서 설치:

- **TFT_eSPI** — Bodmer (User_Setup.h 파일을 라이브러리 폴더에 복사)
- **lvgl** v9.x — LVGL
- **ArduinoJson** v7.x — Benoit Blanchon
- **LittleFS** — RP2040 보드 패키지에 포함

보드 패키지: **Raspberry Pi Pico/RP2040** (Earle F. Philhower)

---

## 4. 터치 캘리브레이션

`calibration.ino`를 먼저 실행해 원시 값을 측정한 뒤 아래 상수를 교체합니다.

```cpp
#define CAL_RY_MIN  204
#define CAL_RY_MAX  3781
#define CAL_RX_MIN  311
#define CAL_RX_MAX  3808
```

---

## 5. JSON 통신 프로토콜 (Serial1 ↔ ESP32)

### HMI → ESP32 (전송)

| 커맨드 | JSON 예시 | 동작 |
|--------|-----------|------|
| 출력 토글 | `{"c":"so","n":0,"v":1}` | n번 출력을 v(0/1)로 설정 |
| 설정 저장 | `{"c":"si","e":"이메일","ssid":"AP","password":"PW","mqttBroker":"주소"}` | Wi-Fi/MQTT 설정 전송 |
| 설정 요청 | `{"c":"ti","req":"config"}` | ESP32에 현재 설정 요청 |
| 블루투스 | `{"c":"ti","bleboot":1}` | BLE 모드 부팅 |
| 펌웨어 | `{"c":"df","f":"파일명.bin"}` | OTA 다운로드 요청 |

### ESP32 → HMI (수신)

| 커맨드 | JSON 예시 | 동작 |
|--------|-----------|------|
| 상태 갱신 | `{"c":"ti","in":[0,1,0,0],"out":[1,0,0,0],"wifi":true,"mqtt":true,"time":"14:30","mac":"AA:BB:..."}` | UI 전체 갱신 |
| 설정 수신 | `{"c":"cfg","ssid":"...","password":"...","e":"...","mqttBroker":"..."}` | 설정 화면 자동 입력 |
| OTA 시작 | `{"c":"df_start"}` | 다운로드 시작 알림 |
| OTA 결과 | `{"c":"df_result","ok":1}` | 완료/실패 알림 |

---

## 6. 코드 구조 요약

```
setup()
 ├─ Serial / Serial1 초기화
 ├─ LittleFS 마운트
 ├─ TFT 초기화 (ILI9488, rotation=1, invertDisplay=true)
 ├─ LVGL 초기화 (버퍼 1/10, flush_cb, tick_cb, indev)
 └─ UI 생성
     ├─ tab1 제어판: INPUT LED ×4 + OUTPUT 버튼 ×4 + 상태바
     ├─ tab2 설정: SSID/PW/Email/MQTT 입력 + 가상키보드
     └─ tab3 메뉴얼: QR코드 팝업 버튼 목록

loop()
 ├─ Serial1 수신 → parseJSONPayload()
 ├─ Watchdog (10초 무응답 시 리셋, i2r-03-hmi 한정)
 └─ lv_timer_handler()
```

---

## 7. 커스터마이징 포인트

소스에서 자주 수정하는 부분:

| 위치 | 변수/상수 | 설명 |
|------|-----------|------|
| 상단 | `String type` | 보드 타입 식별자 |
| 상단 | `COL_*` 매크로 | 전체 색상 팔레트 |
| 상단 | `CH_IN_ON_HEX[]` / `CH_OUT_ON_HEX[]` | 채널별 ON 색상 |
| `setup()` | `titles[]` / `urls[]` | 메뉴얼 탭 링크 목록 |
| `setup()` | `show_qr_panel(url)` 호출부 | 사용법 QR URL |
| `parseJSONPayload()` | `doc["c"] == "ti"` 블록 | 수신 데이터 처리 확장 |

---

## 8. 전체 소스 코드

### hmi-i2r09.ino

```cpp
// RP2040 터치패널 - LVGL v9 
// Version: 0.1.0 - 2025-03-05
// LV_USE_TFT_ESPI 0 (수동 드라이버 사용)-

#include "NotoSansKR_20.h"
#include "hardware/watchdog.h" // 워치독 라이브러리 추가
#include "lv_qrcode.hpp"
#include "qrcodegen.hpp"
#include <ArduinoJson.h>
#include <LittleFS.h>
#include <TFT_eSPI.h>
#include <lvgl.h>

#define SCREEN_WIDTH 480
#define SCREEN_HEIGHT 320
#define TFT_BL_PIN 18


/* ══════════════════════════════════════════
   현대적 HMI 컬러 팔레트 — Light Theme
   ※ invertDisplay(false) 기준
   ══════════════════════════════════════════ */
#define COL_BG        lv_color_hex(0xF0F4F8)   /* 연한 청회색 배경 */
#define COL_PANEL     lv_color_hex(0xFFFFFF)   /* 흰색 카드 패널 */
#define COL_PANEL2    lv_color_hex(0xE8ECF2)   /* 버튼 OFF 밝은 배경 */
#define COL_TAB_BG    lv_color_hex(0xF0F4F8)   /* 탭바 배경 */

/* 텍스트 */
#define COL_TXT_MAIN  lv_color_hex(0x1E2329)   /* 짙은 다크 텍스트 */
#define COL_TXT_SUB   lv_color_hex(0x64748B)   /* 회색 보조 텍스트 */
#define COL_BORDER    lv_color_hex(0xCBD5E1)   /* 패널 테두리 (연한 회색) */

/* 주 강조색 */
#define COL_PRIMARY   lv_color_hex(0x2563EB)   /* 선명한 블루 */
#define COL_PRIMARY2  lv_color_hex(0x1D4ED8)   /* 딥 블루 */

/* 신호 상태 색 */
#define COL_SUCCESS   lv_color_hex(0x16A34A)   /* 그린 - 활성 */
#define COL_OFF       lv_color_hex(0xE2E8F0)   /* OFF 밝은 배경 */
#define COL_OFF_BRD   lv_color_hex(0xCBD5E1)   /* OFF 테두리 */
#define COL_WARN      lv_color_hex(0xEA580C)   /* 경고 오렌지 */

/* ── 채널별 개성 있는 컬러 (INPUT / OUTPUT 각각) ── */
/* INPUT 채널 색 (OFF 상태) — 채널 색상의 연한 버전 */
#define COL_IN1_OFF   lv_color_hex(0xDBEAFE)   /* 채널1 OFF - 연한 블루 */
#define COL_IN2_OFF   lv_color_hex(0xD1FAE5)   /* 채널2 OFF - 연한 그린 */
#define COL_IN3_OFF   lv_color_hex(0xEDE9FE)   /* 채널3 OFF - 연한 바이올렛 */
#define COL_IN4_OFF   lv_color_hex(0xFEF3C7)   /* 채널4 OFF - 연한 앰버 */
/* INPUT 채널 색 (ON  상태) */
#define COL_IN1_ON    lv_color_hex(0x0078FF)   /* 채널1 ON - 블루 */
#define COL_IN2_ON    lv_color_hex(0x00C48C)   /* 채널2 ON - 에메랄드 */
#define COL_IN3_ON    lv_color_hex(0xBB55FF)   /* 채널3 ON - 바이올렛 */
#define COL_IN4_ON    lv_color_hex(0xFF8C00)   /* 채널4 ON - 앰버 */

/* OUTPUT 버튼 색 (OFF) — 연한 파스텔 */
#define COL_OUT1_OFF  lv_color_hex(0xDBEAFE)
#define COL_OUT2_OFF  lv_color_hex(0xEDE9FE)
#define COL_OUT3_OFF  lv_color_hex(0xFEE2E2)
#define COL_OUT4_OFF  lv_color_hex(0xD1FAE5)
/* OUTPUT 버튼 색 (ON) */
#define COL_OUT1_ON   lv_color_hex(0x0078FF)   /* 채널1 ON - 블루 */
#define COL_OUT2_ON   lv_color_hex(0x8B2BE2)   /* 채널2 ON - 퍼플 */
#define COL_OUT3_ON   lv_color_hex(0xFF3B3B)   /* 채널3 ON - 레드 */
#define COL_OUT4_ON   lv_color_hex(0x00B080)   /* 채널4 ON - 틸 */

/* LED↔버튼 색상: OFF=파스텔, ON=선명한 원색 */
static const uint32_t CH_IN_OFF_HEX[4]  = {0xD1FAE5, 0xD1FAE5, 0xD1FAE5, 0xD1FAE5};
static const uint32_t CH_IN_ON_HEX[4]   = {0x00B080, 0x00B080, 0x00B080, 0x00B080};
static const uint32_t CH_OUT_OFF_HEX[4] = {0xEDE9FE, 0xEDE9FE, 0xEDE9FE, 0xEDE9FE};
static const uint32_t CH_OUT_ON_HEX[4]  = {0xFF8C00, 0xFF8C00, 0xFF8C00, 0xFF8C00};

/* 0으로 바꾸면 탭뷰가 표시됩니다. */
#define HMI_DEBUG_SIMPLE_SCR 0

/* 1로 바꾸면 LVGL 없이 TFT만 사용 (디스플레이 동작 확인용) */
#define HMI_TFT_ONLY_TEST 0

TFT_eSPI tft = TFT_eSPI();

String type = "i2r-02-hmi";
static String serialBuffer = "";
static unsigned long lastSerialTime = 0;
unsigned long serialTimeoutMs = 10000;

/* 제어판 UI 변수 */
static lv_obj_t *in_led[4];
static lv_obj_t *btn[4];
static bool btnState[4] = {false};

static lv_obj_t *wifi_icon = NULL;
static lv_obj_t *mqtt_icon = NULL;
static lv_obj_t *time_label = NULL;

static lv_obj_t *ssid_ta = NULL;
static lv_obj_t *pw_ta = NULL;
static lv_obj_t *email_ta = NULL;
static lv_obj_t *mqtt_ta = NULL;
static lv_obj_t *connect_btn = NULL;
static lv_obj_t *manual_btn = NULL;
static lv_obj_t *bt_btn = NULL;
static lv_obj_t *fw_btn = NULL;
static lv_obj_t *mac_label = NULL;
static lv_obj_t *tab2_ref = NULL;
static lv_obj_t *qr_panel = NULL;
static lv_obj_t *qr_overlay = NULL;

/* 온도·습도 라벨 (제어판 탭) */
static lv_obj_t *temp_label = NULL;
static lv_obj_t *humi_label = NULL;

static lv_style_t style_ta;
static lv_style_t style_ta_focused;

/* 화면 1/10 버퍼 */
#define BUF_PIXELS (SCREEN_WIDTH * SCREEN_HEIGHT / 10)
#define BUF_BYTES (BUF_PIXELS * (uint32_t)sizeof(lv_color16_t))

alignas(8) static uint8_t buf[BUF_BYTES];


// calibration.ino 실행 결과값으로 교체하세요
#define CAL_RY_MIN  204
#define CAL_RY_MAX  3781
#define CAL_RX_MIN  311
#define CAL_RX_MAX  3808

/* in[] 상태에 따라 입력 LED 표시 — 채널별 고유 색상 */
static void updateInputLedUI(uint8_t index, bool state) {
  if (index >= 4 || !in_led[index])
    return;
  if (state) {
    lv_color_t onCol  = lv_color_hex(CH_IN_ON_HEX[index]);
    lv_obj_set_style_bg_color(in_led[index], onCol, LV_PART_MAIN);
    lv_obj_set_style_border_color(in_led[index], lv_color_white(), LV_PART_MAIN);
    lv_obj_set_style_border_width(in_led[index], 2, LV_PART_MAIN);
    lv_obj_set_style_shadow_width(in_led[index], 28, LV_PART_MAIN);
    lv_obj_set_style_shadow_color(in_led[index], onCol, LV_PART_MAIN);
    lv_obj_set_style_shadow_spread(in_led[index], 8, LV_PART_MAIN);
    lv_obj_set_style_shadow_opa(in_led[index], LV_OPA_50, LV_PART_MAIN);
    lv_obj_set_style_shadow_offset_x(in_led[index], 0, LV_PART_MAIN);
    lv_obj_set_style_shadow_offset_y(in_led[index], 0, LV_PART_MAIN);
  } else {
    lv_color_t offCol = lv_color_hex(CH_IN_OFF_HEX[index]);
    lv_obj_set_style_bg_color(in_led[index], offCol, LV_PART_MAIN);
    lv_obj_set_style_border_color(in_led[index], lv_color_hex(CH_IN_ON_HEX[index]), LV_PART_MAIN);
    lv_obj_set_style_border_width(in_led[index], 2, LV_PART_MAIN);
    lv_obj_set_style_shadow_width(in_led[index], 0, LV_PART_MAIN);
    lv_obj_set_style_shadow_opa(in_led[index], LV_OPA_TRANSP, LV_PART_MAIN);
  }
}

/* 출력 버튼 상태 갱신 — 채널별 고유 색상 */
static void updateButtonUI(uint8_t index, bool state) {
  if (index >= 4 || !btn[index])
    return;
  if (state) {
    lv_color_t onCol = lv_color_hex(CH_OUT_ON_HEX[index]);
    lv_obj_set_style_bg_color(btn[index], onCol, LV_PART_MAIN);
    lv_obj_set_style_border_color(btn[index], lv_color_white(), LV_PART_MAIN);
    lv_obj_set_style_shadow_width(btn[index], 25, LV_PART_MAIN);
    lv_obj_set_style_shadow_color(btn[index], onCol, LV_PART_MAIN);
    lv_obj_set_style_shadow_spread(btn[index], 7, LV_PART_MAIN);
    lv_obj_set_style_shadow_opa(btn[index], LV_OPA_40, LV_PART_MAIN);
    lv_obj_set_style_shadow_offset_x(btn[index], 0, LV_PART_MAIN);
    lv_obj_set_style_shadow_offset_y(btn[index], 0, LV_PART_MAIN);
  } else {
    lv_color_t offCol = lv_color_hex(CH_OUT_OFF_HEX[index]);
    lv_obj_set_style_bg_color(btn[index], offCol, LV_PART_MAIN);
    lv_obj_set_style_border_color(btn[index], lv_color_hex(CH_OUT_ON_HEX[index]), LV_PART_MAIN);
    lv_obj_set_style_shadow_width(btn[index], 0, LV_PART_MAIN);
    lv_obj_set_style_shadow_opa(btn[index], LV_OPA_TRANSP, LV_PART_MAIN);
  }
}

/* PLC로 출력 토글 전송 */
static void sendToggleCommand(uint8_t btnIndex, bool state) {
  JsonDocument doc;
  doc["c"] = "so";
  doc["n"] = btnIndex;
  doc["v"] = state ? 1 : 0;
  String json;
  serializeJson(doc, json);
  Serial1.println(json);
  Serial.println("[SEND] " + json);
}

static void btn_event_cb(lv_event_t *e) {
  uint8_t index = (uint32_t)(uintptr_t)lv_event_get_user_data(e);
  if (index >= 4)
    return;
  btnState[index] = !btnState[index];
  updateButtonUI(index, btnState[index]);
  sendToggleCommand(index, btnState[index]);
}

void loadHMIConfig() {
  Serial.println("\n[loadHMIConfig] 디스크에서 설정 파일 읽기 시도 중...");
  File f = LittleFS.open("/config.json", "r");
  if (f) {
    String jsonStr = f.readString();
    f.close();
    if (jsonStr.length() > 0) {
      JsonDocument doc;
      DeserializationError error = deserializeJson(doc, jsonStr);
      if (!error) {
        if (doc["ssid"].is<const char *>())
          lv_textarea_set_text(ssid_ta, doc["ssid"].as<const char *>());
        if (doc["pw"].is<const char *>())
          lv_textarea_set_text(pw_ta, doc["pw"].as<const char *>());
        if (doc["email"].is<const char *>())
          lv_textarea_set_text(email_ta, doc["email"].as<const char *>());
        if (doc["mqtt"].is<const char *>())
          lv_textarea_set_text(mqtt_ta, doc["mqtt"].as<const char *>());
      }
    }
  }
}

void saveHMIConfig(const char *ssid, const char *pw, const char *email,
                   const char *mqtt) {
  File f = LittleFS.open("/config.json", "w");
  if (f) {
    JsonDocument doc;
    doc["ssid"]  = ssid  ? ssid  : "";
    doc["pw"]    = pw    ? pw    : "";
    doc["email"] = email ? email : "";
    doc["mqtt"]  = mqtt  ? mqtt  : "";
    String output;
    serializeJson(doc, output);
    f.print(output);
    f.close();
    Serial.println("[saveHMIConfig] 저장: " + output);
  }
}

/* Serial1 JSON 파싱 */
static void parseJSONPayload(const char *payload, unsigned int length) {
  JsonDocument doc;
  DeserializationError error = deserializeJson(doc, payload, length);
  if (error) { Serial.println("JSON Error"); return; }

  if (doc["c"] == "ti") {
    JsonArray inArray = doc["in"];
    if (!inArray.isNull())
      for (size_t i = 0; i < 4 && i < inArray.size(); i++)
        updateInputLedUI((uint8_t)i, inArray[i].as<bool>());

    JsonArray outArray = doc["out"];
    if (!outArray.isNull())
      for (size_t i = 0; i < 4 && i < outArray.size(); i++) {
        bool v = outArray[i].as<bool>();
        if (btnState[i] != v) { btnState[i] = v; updateButtonUI((uint8_t)i, v); }
      }

    if (wifi_icon) {
      bool wifiOk = doc["wifi"] | false;
      lv_obj_set_style_text_color(wifi_icon, wifiOk ? COL_SUCCESS : COL_OFF, LV_PART_MAIN);
    }
    if (mqtt_icon) {
      bool mqttOk = doc["mqtt"] | false;
      lv_obj_set_style_text_color(mqtt_icon, mqttOk ? COL_SUCCESS : COL_OFF, LV_PART_MAIN);
    }
    if (time_label && !doc["time"].isNull())
      lv_label_set_text(time_label, doc["time"] | "00:00");
    if (mac_label && !doc["mac"].isNull())
      lv_label_set_text_fmt(mac_label, "MAC: %s", doc["mac"] | "----");

    if (type == "i2r-03-hmi") {
      if (temp_label && !doc["temp"].isNull()) {
        char tbuf[20];
        snprintf(tbuf, sizeof(tbuf), "온도: %.1f°C", doc["temp"].as<float>());
        lv_label_set_text(temp_label, tbuf);
      }
      if (humi_label && !doc["humi"].isNull()) {
        char tbuf[20];
        snprintf(tbuf, sizeof(tbuf), "습도: %.0f%%", doc["humi"].as<float>());
        lv_label_set_text(humi_label, tbuf);
      }
    }
  }

  if (doc["c"] == "df_start") {
    serialTimeoutMs = 300000;
    if (mac_label) {
      lv_label_set_text(mac_label, "펌웨어 다운로드 중...");
      lv_obj_set_style_text_color(mac_label, lv_color_hex(0xEA580C), LV_PART_MAIN);
    }
  }

  if (doc["c"] == "df_result") {
    serialTimeoutMs = 10000;
    bool ok = doc["ok"].as<int>() == 1;
    if (mac_label) {
      lv_label_set_text(mac_label, ok ? "업데이트 완료. 재부팅합니다." : "업데이트 실패. 다시 시도해 주세요.");
      lv_obj_set_style_text_color(mac_label,
        lv_color_hex(ok ? 0x10B981 : 0xEF4444), LV_PART_MAIN);
    }
  }

  if (doc["c"] == "cfg") {
    const char *ssid  = doc["ssid"] | "";
    const char *pw    = doc["password"].isNull() ? (doc["pw"] | "") : (doc["password"] | "");
    const char *email = doc["e"].isNull() ? (doc["email"] | "") : (doc["e"] | "");
    const char *mqtt  = doc["mqttBroker"].isNull() ? (doc["mqtt"] | "") : (doc["mqttBroker"] | "");
    if (strlen(mqtt) == 0) mqtt = "mqtt.i2r.link";
    saveHMIConfig(ssid, pw, email, mqtt);
    loadHMIConfig();
  }
}

/* 설정 탭 버튼들: 1초간 연두색 후 원래색 복원용 */
struct btn_flash_t { lv_obj_t *btn; lv_color_t restore_color; };
static btn_flash_t flash_conn, flash_bt, flash_fw, flash_manual;

static void btn_flash_restore_timer_cb(lv_timer_t *t) {
  btn_flash_t *d = (btn_flash_t *)lv_timer_get_user_data(t);
  if (d && d->btn) { lv_obj_set_style_bg_color(d->btn, d->restore_color, LV_PART_MAIN); d->btn = NULL; }
  lv_timer_delete(t);
}

/* QR 팝업 — 전체화면 다크 오버레이 위에 QR 표시 */
static void show_qr_panel(const char *url, lv_obj_t * /*parent*/) {
  if (qr_overlay) { lv_obj_delete(qr_overlay); qr_overlay = NULL; qr_panel = NULL; }

  qr_overlay = lv_obj_create(lv_scr_act());
  lv_obj_set_size(qr_overlay, SCREEN_WIDTH, SCREEN_HEIGHT);
  lv_obj_set_pos(qr_overlay, 0, 0);
  lv_obj_set_style_bg_color(qr_overlay, lv_color_black(), LV_PART_MAIN);
  lv_obj_set_style_bg_opa(qr_overlay, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_border_width(qr_overlay, 0, LV_PART_MAIN);
  lv_obj_set_style_pad_all(qr_overlay, 0, LV_PART_MAIN);
  lv_obj_set_style_radius(qr_overlay, 0, LV_PART_MAIN);
  lv_obj_remove_flag(qr_overlay, LV_OBJ_FLAG_SCROLLABLE);

  qr_panel = lv_obj_create(qr_overlay);
  lv_obj_set_size(qr_panel, 380, 210);
  lv_obj_center(qr_panel);
  lv_obj_set_style_bg_color(qr_panel, lv_color_hex(0x111111), LV_PART_MAIN);
  lv_obj_set_style_border_color(qr_panel, lv_color_hex(0x58A6FF), LV_PART_MAIN);
  lv_obj_set_style_border_width(qr_panel, 2, LV_PART_MAIN);
  lv_obj_set_style_radius(qr_panel, 12, LV_PART_MAIN);
  lv_obj_set_style_pad_all(qr_panel, 0, LV_PART_MAIN);

  lv_obj_t *qr = my_qrcode_create(qr_panel, 150, lv_color_white(), lv_color_black());
  if (qr && url) {
    char url_buf[256];
    strncpy(url_buf, url, 255); url_buf[255] = '\0';
    my_qrcode_update(qr, (void *)url_buf, (uint32_t)strlen(url_buf));
    lv_obj_align(qr, LV_ALIGN_LEFT_MID, 40, 0);
  }

  lv_obj_t *close_btn = lv_btn_create(qr_panel);
  lv_obj_set_size(close_btn, 100, 50);
  lv_obj_align(close_btn, LV_ALIGN_RIGHT_MID, -40, 0);
  lv_obj_set_style_bg_color(close_btn, lv_color_hex(0x1F2937), LV_PART_MAIN);
  lv_obj_set_style_border_color(close_btn, lv_color_hex(0x58A6FF), LV_PART_MAIN);
  lv_obj_set_style_border_width(close_btn, 1, LV_PART_MAIN);
  lv_obj_set_style_radius(close_btn, 8, LV_PART_MAIN);
  lv_obj_t *l_close = lv_label_create(close_btn);
  lv_label_set_text(l_close, "닫기");
  lv_obj_set_style_text_font(l_close, &NotoSansKR_20, LV_PART_MAIN);
  lv_obj_set_style_text_color(l_close, lv_color_white(), LV_PART_MAIN);
  lv_obj_center(l_close);

  lv_obj_add_event_cb(close_btn,
    [](lv_event_t *e) {
      if (qr_overlay) { lv_obj_delete(qr_overlay); qr_overlay = NULL; qr_panel = NULL; }
    }, LV_EVENT_CLICKED, NULL);
}

static int flush_count = 0;

void my_disp_flush(lv_display_t *display, const lv_area_t *area, uint8_t *px_map) {
  uint32_t w = (uint32_t)(area->x2 - area->x1 + 1);
  uint32_t h = (uint32_t)(area->y2 - area->y1 + 1);
  if (flush_count < 4) {
    Serial.printf("flush #%d x=%d y=%d w=%d h=%d\n", flush_count, area->x1, area->y1, w, h);
    flush_count++;
  }
  tft.startWrite();
  tft.setAddrWindow((uint32_t)area->x1, (uint32_t)area->y1, w, h);
  tft.pushColors((uint16_t *)px_map, w * h, true);
  tft.endWrite();
  lv_display_flush_ready(display);
}

static uint32_t my_tick_get(void) { return (uint32_t)millis(); }

void my_touchpad_read(lv_indev_t *indev, lv_indev_data_t *data) {
  uint16_t rx = 0, ry = 0;
  if (digitalRead(TOUCH_IRQ) == LOW && tft.getTouchRaw(&rx, &ry)) {
    int16_t px = constrain(map(ry, CAL_RY_MIN, CAL_RY_MAX, 0, 480), 0, 479);
    int16_t py = constrain(map(rx, CAL_RX_MAX, CAL_RX_MIN, 0, 320), 0, 319);
    data->state   = LV_INDEV_STATE_PRESSED;
    data->point.x = px;
    data->point.y = py;
  } else {
    data->state = LV_INDEV_STATE_RELEASED;
  }
}


void setup() {
  Serial.begin(115200);
  delay(500);

  Serial1.setTX(0); Serial1.setRX(1);
  Serial1.begin(9600);
  delay(100);
  Serial1.println("INIT");
  lastSerialTime = millis();
  serialBuffer.reserve(512);

  pinMode(TFT_BL_PIN, OUTPUT);
  digitalWrite(TFT_BL_PIN, LOW);

  if (!LittleFS.begin()) {
    LittleFS.format();
    LittleFS.begin();
  }

  tft.begin();
  tft.setRotation(1);
  tft.invertDisplay(true);
  tft.fillScreen(TFT_BLACK);

#if HMI_TFT_ONLY_TEST
  tft.fillScreen(TFT_RED);
  delay(2000);
  return;
#endif

  lv_init();
  lv_tick_set_cb(my_tick_get);

  lv_display_t *disp = lv_display_create(SCREEN_WIDTH, SCREEN_HEIGHT);
  lv_display_set_default(disp);
  lv_display_set_flush_cb(disp, my_disp_flush);
  lv_display_set_buffers(disp, buf, NULL, BUF_BYTES, LV_DISPLAY_RENDER_MODE_PARTIAL);

  lv_indev_t *indev = lv_indev_create();
  lv_indev_set_type(indev, LV_INDEV_TYPE_POINTER);
  lv_indev_set_read_cb(indev, my_touchpad_read);
  lv_indev_set_display(indev, disp);

  lv_obj_t *scr = lv_screen_active();
  lv_obj_set_style_bg_color(scr, COL_BG, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(scr, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_text_font(scr, &NotoSansKR_20, LV_PART_MAIN);

#if HMI_DEBUG_SIMPLE_SCR
  lv_obj_t *lbl = lv_label_create(scr);
  lv_label_set_text(lbl, "LVGL OK");
  lv_obj_set_style_text_color(lbl, lv_color_white(), LV_PART_MAIN);
  lv_obj_align(lbl, LV_ALIGN_CENTER, 0, 0);
#else
  lv_obj_t *tabview = lv_tabview_create(scr);
  lv_tabview_set_tab_bar_position(tabview, LV_DIR_TOP);
  lv_tabview_set_tab_bar_size(tabview, 48);

  lv_obj_t *tab_btns = lv_tabview_get_tab_bar(tabview);
  lv_obj_set_style_bg_color(tab_btns, COL_TAB_BG, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(tab_btns, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_border_side(tab_btns, LV_BORDER_SIDE_BOTTOM, LV_PART_MAIN);
  lv_obj_set_style_border_color(tab_btns, COL_BORDER, LV_PART_MAIN);
  lv_obj_set_style_border_width(tab_btns, 1, LV_PART_MAIN);
  lv_obj_set_style_text_font(tab_btns, &NotoSansKR_20, LV_PART_MAIN);
  lv_obj_set_style_text_font(tab_btns, &NotoSansKR_20, LV_PART_ITEMS);
  lv_obj_set_style_text_color(tab_btns, COL_TXT_SUB, LV_PART_MAIN);
  lv_obj_set_style_text_color(tab_btns, COL_PRIMARY, LV_PART_ITEMS | LV_STATE_CHECKED);
  lv_obj_set_style_border_side(tab_btns, LV_BORDER_SIDE_BOTTOM, LV_PART_ITEMS | LV_STATE_CHECKED);
  lv_obj_set_style_border_color(tab_btns, COL_PRIMARY, LV_PART_ITEMS | LV_STATE_CHECKED);
  lv_obj_set_style_border_width(tab_btns, 3, LV_PART_ITEMS | LV_STATE_CHECKED);
  lv_obj_set_style_bg_opa(tab_btns, LV_OPA_TRANSP, LV_PART_ITEMS);
  lv_obj_set_style_bg_opa(tab_btns, LV_OPA_TRANSP, LV_PART_ITEMS | LV_STATE_CHECKED);

  lv_obj_t *tab1 = lv_tabview_add_tab(tabview, "제어판");
  lv_obj_t *tab2 = lv_tabview_add_tab(tabview, "설정");
  lv_obj_t *tab3 = lv_tabview_add_tab(tabview, "메뉴얼");

  lv_obj_add_event_cb(tabview,
    [](lv_event_t *e) {
      lv_obj_t *tv = (lv_obj_t *)lv_event_get_target(e);
      uint16_t active_tab = lv_tabview_get_tab_act(tv);
      if (active_tab == 1) {
        Serial.println("=== 설정 창 데이터 확인 ===");
        Serial.print("WIFI: [");  Serial.print(lv_textarea_get_text(ssid_ta));  Serial.println("]");
        Serial.print("PW: [");    Serial.print(lv_textarea_get_text(pw_ta));    Serial.println("]");
        Serial.print("EMAIL: ["); Serial.print(lv_textarea_get_text(email_ta)); Serial.println("]");
        Serial.print("MQTT: [");  Serial.print(lv_textarea_get_text(mqtt_ta));  Serial.println("]");
        Serial.println("==========================");
      }
    }, LV_EVENT_VALUE_CHANGED, NULL);

  lv_obj_set_style_bg_color(tab1, COL_BG, LV_PART_MAIN);
  lv_obj_set_style_bg_color(tab2, COL_BG, LV_PART_MAIN);
  lv_obj_set_style_bg_color(tab3, COL_BG, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(tab1, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(tab2, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(tab3, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_remove_flag(tab1, LV_OBJ_FLAG_SCROLLABLE);
  lv_obj_remove_flag(tab2, LV_OBJ_FLAG_SCROLLABLE);
  lv_obj_remove_flag(tab3, LV_OBJ_FLAG_SCROLLABLE);
  lv_obj_set_style_pad_all(tab1, 0, LV_PART_MAIN);
  lv_obj_set_style_pad_all(tab2, 0, LV_PART_MAIN);
  lv_obj_set_style_pad_all(tab3, 0, LV_PART_MAIN);

  /* ─ INPUT 헤더 ─ */
  lv_obj_t *lbl_in_hdr = lv_label_create(tab1);
  lv_label_set_text(lbl_in_hdr, "INPUT");
  lv_obj_set_style_text_font(lbl_in_hdr, &lv_font_montserrat_14, LV_PART_MAIN);
  lv_obj_set_style_text_color(lbl_in_hdr, COL_TXT_SUB, LV_PART_MAIN);
  lv_obj_align(lbl_in_hdr, LV_ALIGN_TOP_LEFT, 6, 2);

  lv_obj_t *panel_in = lv_obj_create(tab1);
  lv_obj_set_size(panel_in, 476, 86);
  lv_obj_align(panel_in, LV_ALIGN_TOP_MID, 0, 18);
  lv_obj_set_style_bg_color(panel_in, COL_PANEL, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(panel_in, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_radius(panel_in, 14, LV_PART_MAIN);
  lv_obj_set_style_border_color(panel_in, COL_BORDER, LV_PART_MAIN);
  lv_obj_set_style_border_width(panel_in, 1, LV_PART_MAIN);
  lv_obj_set_style_pad_all(panel_in, 0, LV_PART_MAIN);
  lv_obj_remove_flag(panel_in, LV_OBJ_FLAG_SCROLLABLE);

  for (int i = 0; i < 4; i++) {
    in_led[i] = lv_obj_create(panel_in);
    lv_obj_set_size(in_led[i], 60, 60);
    lv_obj_set_style_radius(in_led[i], LV_RADIUS_CIRCLE, LV_PART_MAIN);
    lv_obj_set_style_bg_color(in_led[i], lv_color_hex(CH_IN_OFF_HEX[i]), LV_PART_MAIN);
    lv_obj_set_style_border_color(in_led[i], lv_color_hex(CH_IN_ON_HEX[i]), LV_PART_MAIN);
    lv_obj_set_style_border_width(in_led[i], 2, LV_PART_MAIN);
    lv_obj_set_style_shadow_width(in_led[i], 0, LV_PART_MAIN);
    lv_obj_align(in_led[i], LV_ALIGN_LEFT_MID, 38 + (i * 112), 0);
    lv_obj_t *led_num = lv_label_create(in_led[i]);
    lv_label_set_text_fmt(led_num, "%d", i + 1);
    lv_obj_set_style_text_color(led_num, COL_TXT_MAIN, LV_PART_MAIN);
    lv_obj_set_style_text_font(led_num, &NotoSansKR_20, LV_PART_MAIN);
    lv_obj_align(led_num, LV_ALIGN_CENTER, 0, 0);
  }

  lv_obj_t *lbl_out_hdr = lv_label_create(tab1);
  lv_label_set_text(lbl_out_hdr, "OUTPUT");
  lv_obj_set_style_text_font(lbl_out_hdr, &lv_font_montserrat_14, LV_PART_MAIN);
  lv_obj_set_style_text_color(lbl_out_hdr, COL_TXT_SUB, LV_PART_MAIN);
  lv_obj_align(lbl_out_hdr, LV_ALIGN_TOP_LEFT, 6, 107);

  lv_obj_t *panel_out = lv_obj_create(tab1);
  lv_obj_set_size(panel_out, 476, 86);
  lv_obj_align(panel_out, LV_ALIGN_TOP_MID, 0, 125);
  lv_obj_set_style_bg_color(panel_out, COL_PANEL, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(panel_out, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_radius(panel_out, 14, LV_PART_MAIN);
  lv_obj_set_style_border_color(panel_out, COL_BORDER, LV_PART_MAIN);
  lv_obj_set_style_border_width(panel_out, 1, LV_PART_MAIN);
  lv_obj_set_style_pad_all(panel_out, 0, LV_PART_MAIN);
  lv_obj_remove_flag(panel_out, LV_OBJ_FLAG_SCROLLABLE);

  for (int i = 0; i < 4; i++) {
    btn[i] = lv_btn_create(panel_out);
    lv_obj_set_size(btn[i], 88, 68);
    lv_obj_set_style_bg_color(btn[i], lv_color_hex(CH_OUT_OFF_HEX[i]), LV_PART_MAIN);
    lv_obj_set_style_radius(btn[i], 12, LV_PART_MAIN);
    lv_obj_set_style_border_width(btn[i], 2, LV_PART_MAIN);
    lv_obj_set_style_border_color(btn[i], lv_color_hex(CH_OUT_ON_HEX[i]), LV_PART_MAIN);
    lv_obj_set_style_shadow_width(btn[i], 0, LV_PART_MAIN);
    lv_obj_align(btn[i], LV_ALIGN_LEFT_MID, 24 + (i * 112), 0);
    lv_obj_add_event_cb(btn[i], btn_event_cb, LV_EVENT_CLICKED, (void *)(uintptr_t)i);
    lv_obj_t *label = lv_label_create(btn[i]);
    lv_label_set_text_fmt(label, "%d", i + 1);
    lv_obj_set_style_text_font(label, &NotoSansKR_20, LV_PART_MAIN);
    lv_obj_set_style_text_color(label, COL_TXT_MAIN, LV_PART_MAIN);
    lv_obj_align(label, LV_ALIGN_CENTER, 0, 0);
  }

  lv_obj_t *status_bar = lv_obj_create(tab1);
  lv_obj_set_size(status_bar, 476, 26);
  lv_obj_align(status_bar, LV_ALIGN_BOTTOM_MID, 0, -2);
  lv_obj_set_style_bg_color(status_bar, COL_PANEL, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(status_bar, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_radius(status_bar, 8, LV_PART_MAIN);
  lv_obj_set_style_border_color(status_bar, COL_BORDER, LV_PART_MAIN);
  lv_obj_set_style_border_width(status_bar, 1, LV_PART_MAIN);
  lv_obj_set_style_pad_all(status_bar, 2, LV_PART_MAIN);
  lv_obj_remove_flag(status_bar, LV_OBJ_FLAG_SCROLLABLE);

  wifi_icon = lv_label_create(status_bar);
  lv_label_set_text(wifi_icon, LV_SYMBOL_WIFI);
  lv_obj_set_style_text_font(wifi_icon, &lv_font_montserrat_14, LV_PART_MAIN);
  lv_obj_set_style_text_color(wifi_icon, COL_TXT_SUB, LV_PART_MAIN);
  lv_obj_align(wifi_icon, LV_ALIGN_LEFT_MID, 6, 0);

  mqtt_icon = lv_label_create(status_bar);
  lv_label_set_text(mqtt_icon, LV_SYMBOL_REFRESH);
  lv_obj_set_style_text_font(mqtt_icon, &lv_font_montserrat_14, LV_PART_MAIN);
  lv_obj_set_style_text_color(mqtt_icon, COL_TXT_SUB, LV_PART_MAIN);
  lv_obj_align(mqtt_icon, LV_ALIGN_LEFT_MID, 32, 0);

  time_label = lv_label_create(status_bar);
  lv_label_set_text(time_label, "00:00");
  lv_obj_set_style_text_font(time_label, &NotoSansKR_20, LV_PART_MAIN);
  lv_obj_set_style_text_color(time_label, COL_PRIMARY, LV_PART_MAIN);
  lv_obj_align(time_label, LV_ALIGN_CENTER, 0, 0);

  if (type == "i2r-03-hmi") {
    humi_label = lv_label_create(status_bar);
    lv_label_set_text(humi_label, "---%");
    lv_obj_set_style_text_font(humi_label, &NotoSansKR_20, LV_PART_MAIN);
    lv_obj_set_style_text_color(humi_label, COL_TXT_SUB, LV_PART_MAIN);
    lv_obj_align(humi_label, LV_ALIGN_RIGHT_MID, -6, 0);

    temp_label = lv_label_create(status_bar);
    lv_label_set_text(temp_label, "--.-°C");
    lv_obj_set_style_text_font(temp_label, &NotoSansKR_20, LV_PART_MAIN);
    lv_obj_set_style_text_color(temp_label, COL_TXT_SUB, LV_PART_MAIN);
    lv_obj_align_to(temp_label, humi_label, LV_ALIGN_OUT_LEFT_MID, -8, 0);
  }

  /* ── 탭2 설정 ── */
  tab2_ref = tab2;
  lv_style_init(&style_ta);
  lv_style_set_bg_color(&style_ta, lv_color_darken(COL_PANEL, 10));
  lv_style_set_border_color(&style_ta, COL_OFF);
  lv_style_set_border_width(&style_ta, 1);
  lv_style_set_radius(&style_ta, 6);
  lv_style_set_text_color(&style_ta, COL_TXT_MAIN);
  lv_style_set_text_font(&style_ta, &NotoSansKR_20);

  lv_style_init(&style_ta_focused);
  lv_style_set_bg_color(&style_ta_focused, lv_color_hex(CH_OUT_OFF_HEX[0]));
  lv_style_set_border_color(&style_ta_focused, lv_color_hex(CH_OUT_ON_HEX[0]));
  lv_style_set_border_width(&style_ta_focused, 2);
  lv_style_set_text_color(&style_ta_focused, COL_TXT_MAIN);
  lv_style_set_text_font(&style_ta_focused, &NotoSansKR_20);

  lv_obj_t *panel_set = lv_obj_create(tab2);
  lv_obj_set_size(panel_set, 440, 260);
  lv_obj_align(panel_set, LV_ALIGN_CENTER, 0, 0);
  lv_obj_set_style_bg_opa(panel_set, LV_OPA_TRANSP, LV_PART_MAIN);
  lv_obj_set_style_border_width(panel_set, 0, LV_PART_MAIN);
  lv_obj_remove_flag(panel_set, LV_OBJ_FLAG_SCROLLABLE);

  lv_obj_t *form_cont = lv_obj_create(panel_set);
  lv_obj_set_size(form_cont, 420, 180);
  lv_obj_align(form_cont, LV_ALIGN_TOP_MID, 0, 0);
  lv_obj_set_style_bg_color(form_cont, COL_PANEL, LV_PART_MAIN);
  lv_obj_set_style_radius(form_cont, 12, LV_PART_MAIN);
  lv_obj_set_style_border_width(form_cont, 0, LV_PART_MAIN);
  lv_obj_remove_flag(form_cont, LV_OBJ_FLAG_SCROLLABLE);

  ssid_ta = lv_textarea_create(form_cont);
  lv_obj_set_width(ssid_ta, 190);
  lv_textarea_set_one_line(ssid_ta, true);
  lv_textarea_set_placeholder_text(ssid_ta, "와이파이 이름");
  lv_obj_add_style(ssid_ta, &style_ta, LV_PART_MAIN);
  lv_obj_add_style(ssid_ta, &style_ta_focused, LV_PART_MAIN | LV_STATE_FOCUSED);
  lv_obj_align(ssid_ta, LV_ALIGN_TOP_LEFT, 0, 0);

  pw_ta = lv_textarea_create(form_cont);
  lv_obj_set_width(pw_ta, 190);
  lv_textarea_set_one_line(pw_ta, true);
  lv_textarea_set_password_mode(pw_ta, true);
  lv_textarea_set_placeholder_text(pw_ta, "비밀번호");
  lv_obj_add_style(pw_ta, &style_ta, LV_PART_MAIN);
  lv_obj_add_style(pw_ta, &style_ta_focused, LV_PART_MAIN | LV_STATE_FOCUSED);
  lv_obj_align(pw_ta, LV_ALIGN_TOP_RIGHT, 0, 0);

  email_ta = lv_textarea_create(form_cont);
  lv_obj_set_size(email_ta, 190, 40);
  lv_textarea_set_one_line(email_ta, true);
  lv_textarea_set_placeholder_text(email_ta, "이메일");
  lv_obj_add_style(email_ta, &style_ta, LV_PART_MAIN);
  lv_obj_add_style(email_ta, &style_ta_focused, LV_PART_MAIN | LV_STATE_FOCUSED);
  lv_obj_align(email_ta, LV_ALIGN_TOP_LEFT, 0, 50);

  mqtt_ta = lv_textarea_create(form_cont);
  lv_obj_set_size(mqtt_ta, 190, 40);
  lv_textarea_set_one_line(mqtt_ta, true);
  lv_textarea_set_placeholder_text(mqtt_ta, "MQTT 주소");
  lv_textarea_set_text(mqtt_ta, "mqtt.i2r.link");
  lv_obj_add_style(mqtt_ta, &style_ta, LV_PART_MAIN);
  lv_obj_add_style(mqtt_ta, &style_ta_focused, LV_PART_MAIN | LV_STATE_FOCUSED);
  lv_obj_align(mqtt_ta, LV_ALIGN_TOP_RIGHT, 0, 50);

  mac_label = lv_label_create(form_cont);
  lv_label_set_text(mac_label, "MAC: ----");
  lv_obj_set_style_text_font(mac_label, &NotoSansKR_20, LV_PART_MAIN);
  lv_obj_set_style_text_color(mac_label, COL_TXT_SUB, LV_PART_MAIN);
  lv_obj_align(mac_label, LV_ALIGN_BOTTOM_LEFT, 0, -10);

  lv_obj_t *act_row = lv_obj_create(panel_set);
  lv_obj_set_size(act_row, 420, 60);
  lv_obj_align(act_row, LV_ALIGN_BOTTOM_MID, 0, 0);
  lv_obj_set_style_bg_opa(act_row, LV_OPA_TRANSP, LV_PART_MAIN);
  lv_obj_set_style_border_width(act_row, 0, LV_PART_MAIN);
  lv_obj_set_flex_flow(act_row, LV_FLEX_FLOW_ROW);
  lv_obj_set_flex_align(act_row, LV_FLEX_ALIGN_SPACE_BETWEEN, LV_FLEX_ALIGN_CENTER, LV_FLEX_ALIGN_CENTER);
  lv_obj_remove_flag(act_row, LV_OBJ_FLAG_SCROLLABLE);

  manual_btn = lv_btn_create(act_row);
  lv_obj_set_size(manual_btn, 100, 42);
  lv_obj_set_style_bg_color(manual_btn, COL_PANEL2, LV_PART_MAIN);
  lv_obj_set_style_border_color(manual_btn, COL_OFF_BRD, LV_PART_MAIN);
  lv_obj_set_style_border_width(manual_btn, 1, LV_PART_MAIN);
  lv_obj_set_style_radius(manual_btn, 8, LV_PART_MAIN);
  lv_obj_t *l_manual = lv_label_create(manual_btn);
  lv_label_set_text(l_manual, "사용법");
  lv_obj_set_style_text_font(l_manual, &NotoSansKR_20, LV_PART_MAIN);
  lv_obj_set_style_text_color(l_manual, COL_TXT_MAIN, LV_PART_MAIN);
  lv_obj_align(l_manual, LV_ALIGN_CENTER, 0, 0);

  connect_btn = lv_btn_create(act_row);
  lv_obj_set_size(connect_btn, 100, 42);
  lv_obj_set_style_bg_color(connect_btn, COL_PRIMARY2, LV_PART_MAIN);
  lv_obj_set_style_border_color(connect_btn, COL_PRIMARY, LV_PART_MAIN);
  lv_obj_set_style_border_width(connect_btn, 1, LV_PART_MAIN);
  lv_obj_set_style_shadow_width(connect_btn, 12, LV_PART_MAIN);
  lv_obj_set_style_shadow_color(connect_btn, COL_PRIMARY2, LV_PART_MAIN);
  lv_obj_set_style_radius(connect_btn, 8, LV_PART_MAIN);
  lv_obj_t *l_conn = lv_label_create(connect_btn);
  lv_label_set_text(l_conn, "연결");
  lv_obj_set_style_text_font(l_conn, &NotoSansKR_20, LV_PART_MAIN);
  lv_obj_set_style_text_color(l_conn, lv_color_white(), LV_PART_MAIN);
  lv_obj_align(l_conn, LV_ALIGN_CENTER, 0, 0);

  bt_btn = lv_btn_create(act_row);
  lv_obj_set_size(bt_btn, 100, 42);
  lv_obj_set_style_bg_color(bt_btn, COL_PANEL2, LV_PART_MAIN);
  lv_obj_set_style_border_color(bt_btn, COL_OFF_BRD, LV_PART_MAIN);
  lv_obj_set_style_border_width(bt_btn, 1, LV_PART_MAIN);
  lv_obj_set_style_radius(bt_btn, 8, LV_PART_MAIN);
  lv_obj_t *l_bt = lv_label_create(bt_btn);
  lv_label_set_text(l_bt, "블루투스");
  lv_obj_set_style_text_font(l_bt, &NotoSansKR_20, LV_PART_MAIN);
  lv_obj_set_style_text_color(l_bt, COL_TXT_MAIN, LV_PART_MAIN);
  lv_obj_align(l_bt, LV_ALIGN_CENTER, 0, 0);

  fw_btn = lv_btn_create(act_row);
  lv_obj_set_size(fw_btn, 82, 42);
  lv_obj_set_style_bg_color(fw_btn, COL_PANEL2, LV_PART_MAIN);
  lv_obj_set_style_border_color(fw_btn, COL_OFF_BRD, LV_PART_MAIN);
  lv_obj_set_style_border_width(fw_btn, 1, LV_PART_MAIN);
  lv_obj_set_style_radius(fw_btn, 8, LV_PART_MAIN);
  lv_obj_t *l_fw = lv_label_create(fw_btn);
  lv_label_set_text(l_fw, "펌웨어");
  lv_obj_set_style_text_font(l_fw, &NotoSansKR_20, LV_PART_MAIN);
  lv_obj_set_style_text_color(l_fw, COL_TXT_MAIN, LV_PART_MAIN);
  lv_obj_align(l_fw, LV_ALIGN_CENTER, 0, 0);

  lv_obj_t *kb = lv_keyboard_create(tab2);
  lv_obj_add_flag(kb, LV_OBJ_FLAG_HIDDEN);
  lv_obj_align(kb, LV_ALIGN_BOTTOM_MID, 0, 0);
  lv_obj_set_style_text_font(kb, &lv_font_montserrat_14, LV_PART_MAIN);
  lv_obj_set_style_text_font(kb, &lv_font_montserrat_14, LV_PART_ITEMS);

  auto ta_focus_cb = [](lv_event_t *e) {
    lv_event_code_t code = lv_event_get_code(e);
    lv_obj_t *ta = (lv_obj_t *)lv_event_get_target(e);
    lv_obj_t *kb = (lv_obj_t *)lv_event_get_user_data(e);
    if (code == LV_EVENT_FOCUSED || code == LV_EVENT_CLICKED) {
      lv_keyboard_set_textarea(kb, ta);
      lv_obj_remove_flag(kb, LV_OBJ_FLAG_HIDDEN);
      if (connect_btn) lv_obj_add_flag(connect_btn, LV_OBJ_FLAG_HIDDEN);
      if (manual_btn)  lv_obj_add_flag(manual_btn,  LV_OBJ_FLAG_HIDDEN);
      if (bt_btn)      lv_obj_add_flag(bt_btn,      LV_OBJ_FLAG_HIDDEN);
      if (fw_btn)      lv_obj_add_flag(fw_btn,      LV_OBJ_FLAG_HIDDEN);
      if (mac_label)   lv_obj_add_flag(mac_label,   LV_OBJ_FLAG_HIDDEN);
      if (qr_panel)    lv_obj_add_flag(qr_panel,    LV_OBJ_FLAG_HIDDEN);
    }
  };
  lv_obj_add_event_cb(ssid_ta,  ta_focus_cb, LV_EVENT_ALL, kb);
  lv_obj_add_event_cb(pw_ta,    ta_focus_cb, LV_EVENT_ALL, kb);
  lv_obj_add_event_cb(email_ta, ta_focus_cb, LV_EVENT_ALL, kb);
  lv_obj_add_event_cb(mqtt_ta,  ta_focus_cb, LV_EVENT_ALL, kb);

  lv_obj_add_event_cb(kb,
    [](lv_event_t *e) {
      lv_event_code_t code = lv_event_get_code(e);
      if (code == LV_EVENT_CANCEL || code == LV_EVENT_READY) {
        lv_obj_t *kb = (lv_obj_t *)lv_event_get_target(e);
        lv_obj_add_flag(kb, LV_OBJ_FLAG_HIDDEN);
        if (connect_btn) lv_obj_remove_flag(connect_btn, LV_OBJ_FLAG_HIDDEN);
        if (manual_btn)  lv_obj_remove_flag(manual_btn,  LV_OBJ_FLAG_HIDDEN);
        if (bt_btn)      lv_obj_remove_flag(bt_btn,      LV_OBJ_FLAG_HIDDEN);
        if (fw_btn)      lv_obj_remove_flag(fw_btn,      LV_OBJ_FLAG_HIDDEN);
        if (mac_label)   lv_obj_remove_flag(mac_label,   LV_OBJ_FLAG_HIDDEN);
        if (qr_panel)    lv_obj_remove_flag(qr_panel,    LV_OBJ_FLAG_HIDDEN);
      }
    }, LV_EVENT_ALL, NULL);

  lv_obj_add_event_cb(manual_btn,
    [](lv_event_t *e) {
      lv_obj_set_style_bg_color(manual_btn, COL_SUCCESS, LV_PART_MAIN);
      flash_manual.btn = manual_btn; flash_manual.restore_color = COL_OFF;
      lv_timer_t *t = lv_timer_create(btn_flash_restore_timer_cb, 1000, &flash_manual);
      lv_timer_set_repeat_count(t, 1);
      show_qr_panel("https://youtu.be/eMnKAh1EjlE", lv_scr_act());
    }, LV_EVENT_CLICKED, NULL);

  lv_obj_add_event_cb(connect_btn,
    [](lv_event_t *e) {
      lv_obj_set_style_bg_color(connect_btn, COL_SUCCESS, LV_PART_MAIN);
      flash_conn.btn = connect_btn; flash_conn.restore_color = COL_PRIMARY;
      lv_timer_t *t = lv_timer_create(btn_flash_restore_timer_cb, 1000, &flash_conn);
      lv_timer_set_repeat_count(t, 1);
      String email_str = lv_textarea_get_text(email_ta);
      String ssid_str  = lv_textarea_get_text(ssid_ta);
      String pw_str    = lv_textarea_get_text(pw_ta);
      String mqtt_str  = lv_textarea_get_text(mqtt_ta);
      email_str.trim(); ssid_str.trim(); pw_str.trim(); mqtt_str.trim();
      saveHMIConfig(ssid_str.c_str(), pw_str.c_str(), email_str.c_str(), mqtt_str.c_str());
      JsonDocument doc;
      doc["c"] = "si"; doc["e"] = email_str; doc["ssid"] = ssid_str;
      doc["password"] = pw_str; doc["mqttBroker"] = mqtt_str;
      String json; serializeJson(doc, json);
      Serial1.println(json); Serial.println("[SEND] " + json);
    }, LV_EVENT_CLICKED, NULL);

  lv_obj_add_event_cb(bt_btn,
    [](lv_event_t *e) {
      lv_obj_set_style_bg_color(bt_btn, COL_SUCCESS, LV_PART_MAIN);
      flash_bt.btn = bt_btn; flash_bt.restore_color = COL_OFF;
      lv_timer_t *t = lv_timer_create(btn_flash_restore_timer_cb, 1000, &flash_bt);
      lv_timer_set_repeat_count(t, 1);
      if (mac_label) {
        lv_label_set_text(mac_label, "블루투스 모드: 스마트폰 노트북 사용하세요");
        lv_obj_set_style_text_color(mac_label, lv_color_hex(0x1D4ED8), LV_PART_MAIN);
      }
      JsonDocument doc; doc["c"] = "ti"; doc["bleboot"] = 1;
      String json; serializeJson(doc, json);
      Serial1.println(json); Serial.println("[SEND] " + json);
    }, LV_EVENT_CLICKED, NULL);

  lv_obj_add_event_cb(fw_btn,
    [](lv_event_t *e) {
      lv_obj_set_style_bg_color(fw_btn, COL_SUCCESS, LV_PART_MAIN);
      flash_fw.btn = fw_btn; flash_fw.restore_color = COL_OFF;
      lv_timer_t *t = lv_timer_create(btn_flash_restore_timer_cb, 1000, &flash_fw);
      lv_timer_set_repeat_count(t, 1);
      if (mac_label) {
        lv_label_set_text(mac_label, "보드에 업데이트 명령 전송 중...");
        lv_obj_set_style_text_color(mac_label, lv_color_hex(0xEA580C), LV_PART_MAIN);
      }
      JsonDocument doc; doc["c"] = "df"; doc["f"] = (String)type + ".ino.bin";
      String json; serializeJson(doc, json);
      Serial1.println(json); Serial.println("[SEND] " + json);
    }, LV_EVENT_CLICKED, NULL);

  /* ── 탭3 메뉴얼 ── */
  lv_obj_t *list_cont = lv_obj_create(tab3);
  lv_obj_set_size(list_cont, 440, 260);
  lv_obj_center(list_cont);
  lv_obj_set_style_bg_color(list_cont, COL_PANEL, LV_PART_MAIN);
  lv_obj_set_style_bg_opa(list_cont, LV_OPA_COVER, LV_PART_MAIN);
  lv_obj_set_style_radius(list_cont, 12, LV_PART_MAIN);
  lv_obj_set_style_border_width(list_cont, 0, LV_PART_MAIN);
  lv_obj_set_style_pad_all(list_cont, 10, LV_PART_MAIN);
  lv_obj_set_flex_flow(list_cont, LV_FLEX_FLOW_ROW_WRAP);
  lv_obj_set_style_pad_gap(list_cont, 10, 0);
  lv_obj_remove_flag(list_cont, LV_OBJ_FLAG_SCROLLABLE);

  static const char *titles[] = {
    "기기연결/로그인", "타이머 설정", "입력 트리거",  "센서 트리거",
    "Github 메뉴얼",   "아이티알 홈", "HMI 한글폰트 설치"
  };
  static const char *urls[] = {
    "https://youtu.be/kyL2uF-BGZQ",  "https://youtu.be/UIoOG9Iwc24",
    "https://youtu.be/m2ZyhRWnZ0o",  "https://youtu.be/doaUzRg5nQU",
    "https://github.com/kdi6033/i2r","https://i2r.link",
    "https://github.com/kdi6033/i2r"
  };

  for (int i = 0; i < 7; i++) {
    lv_obj_t *btn_link = lv_btn_create(list_cont);
    lv_obj_set_width(btn_link, 190);
    lv_obj_set_style_bg_color(btn_link, COL_PANEL2, LV_PART_MAIN);
    lv_obj_set_style_radius(btn_link, 10, LV_PART_MAIN);
    lv_obj_set_style_border_color(btn_link, COL_OFF_BRD, LV_PART_MAIN);
    lv_obj_set_style_border_width(btn_link, 1, LV_PART_MAIN);
    lv_obj_t *l = lv_label_create(btn_link);
    lv_label_set_text(l, titles[i]);
    lv_obj_set_style_text_font(l, &NotoSansKR_20, LV_PART_MAIN);
    lv_obj_set_style_text_color(l, COL_TXT_MAIN, LV_PART_MAIN);
    lv_obj_center(l);
    lv_obj_add_event_cb(btn_link,
      [](lv_event_t *e) {
        const char *url = (const char *)lv_event_get_user_data(e);
        show_qr_panel(url, lv_scr_act());
      }, LV_EVENT_CLICKED, (void *)urls[i]);
  }
#endif

  lv_obj_invalidate(scr);
  lv_refr_now(disp);
  for (int i = 0; i < 15; i++) { lv_timer_handler(); delay(5); }

  digitalWrite(TFT_BL_PIN, HIGH);
  loadHMIConfig();

  JsonDocument doc;
  doc["c"] = "ti"; doc["req"] = "config";
  String reqJson; serializeJson(doc, reqJson);
  Serial1.println(reqJson);
  Serial.println("[SEND req] " + reqJson);
}

void loop() {
#if HMI_TFT_ONLY_TEST
  static int phase = 0;
  uint16_t col = (phase == 0) ? TFT_RED : (phase == 1) ? TFT_GREEN : TFT_BLUE;
  tft.fillScreen(col);
  tft.setTextColor(TFT_WHITE, col);
  tft.setTextDatum(MC_DATUM);
  tft.drawString("TFT OK", SCREEN_WIDTH / 2, SCREEN_HEIGHT / 2, 4);
  phase = (phase + 1) % 3;
  delay(1500);
  return;
#endif

  while (Serial1.available()) {
    char c = Serial1.read();
    lastSerialTime = millis();
    if (c == '\n') {
      serialBuffer.trim();
      if (serialBuffer.length() > 0) {
        Serial.println("[RX] " + serialBuffer);
        parseJSONPayload(serialBuffer.c_str(), serialBuffer.length());
      }
      serialBuffer = "";
    } else {
      if (serialBuffer.length() < 512) serialBuffer += c;
    }
  }

  if (type == "i2r-03-hmi") {
    if (millis() - lastSerialTime > serialTimeoutMs) {
      Serial.println("Timeout -> Reset");
      delay(50);
      watchdog_enable(1, 1);
      while (true) {}
    }
  }

  lv_timer_handler();
  delay(5);
}
```

### User_Setup.h

```cpp
// TFT_eSPI User_Setup - CrowPanel 3.5" IPS ILI9488 (RP2040)

#define USER_SETUP_INFO "CrowPanel 3.5 ILI9488 RP2040"

#define ILI9488_DRIVER

#define TFT_WIDTH  320
#define TFT_HEIGHT 480

#define TFT_INVERSION_ON

#define TFT_CS    2
#define TFT_RST   3
#define TFT_DC    4
#define TFT_MOSI  11
#define TFT_SCLK  10
#define TFT_BL    5
#define TFT_MISO  12
#define TFT_BACKLIGHT_ON HIGH

#define TOUCH_CS  6
#define TOUCH_IRQ 8

#define TFT_SPI_PORT 1

#define SPI_FREQUENCY       40000000
#define SPI_READ_FREQUENCY  20000000
#define SPI_TOUCH_FREQUENCY  2500000

#define LOAD_GLCD
#define LOAD_FONT2
#define LOAD_FONT4
#define LOAD_FONT6
#define LOAD_FONT7
#define LOAD_FONT8
#define LOAD_GFXFF
#define SMOOTH_FONT
```

---

## 9. AI 활용 예시

아래는 이 파일을 AI에 전달해 코드를 수정한 실제 예시입니다.

### 예시 1 — 채널 수 확장
```
https://raw.githubusercontent.com/kdi6033/i2r/main/LCD35.md 읽고
입력 채널을 8개로 늘려줘. LED 크기는 40px로 줄이고 두 줄로 배치해줘.
```

### 예시 2 — 새 데이터 표시
```
https://raw.githubusercontent.com/kdi6033/i2r/main/LCD35.md 읽고
JSON {"c":"ti","rpm":1234,"amp":5.6} 수신 시 제어판 탭에
RPM과 전류 값을 숫자로 표시하는 라벨을 추가해줘.
```

### 예시 3 — 색상 테마 변경
```
https://raw.githubusercontent.com/kdi6033/i2r/main/LCD35.md 읽고
전체 배경을 다크 테마(검정 계열)로 바꿔줘.
COL_BG, COL_PANEL, COL_TXT_MAIN 색상을 다크 모드에 맞게 조정해줘.
```

### 예시 4 — 탭 추가
```
https://raw.githubusercontent.com/kdi6033/i2r/main/LCD35.md 읽고
탭을 하나 더 추가해서 "그래프" 탭을 만들어줘.
Serial1에서 {"c":"ti","val":123} 을 받으면 LVGL lv_chart로 실시간 그래프를 그려줘.
```

---

## 10. 관련 링크

| 링크 | 내용 |
|------|------|
| [i2r GitHub](https://github.com/kdi6033/i2r) | 전체 프로젝트 소스 |
| [i2r.link](https://i2r.link) | 아이티알 홈페이지 |
| [기기연결/로그인](https://youtu.be/kyL2uF-BGZQ) | 초기 설정 유튜브 |
| [HMI 한글폰트 설치](https://github.com/kdi6033/i2r) | 한글 폰트 적용법 |
