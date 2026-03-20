# i2r IoT PLC — CLAUDE.md
# i2r-02 / i2r-03 / i2r-04 공통 AI 개발 도우미
# PLC 기본 동작 전용 (v1.0) — MQTT 없이 로컬 동작
#
# ✅ 사용법 (claude.ai 채팅창에 입력):
# "https://raw.githubusercontent.com/kdi6033/i2r/main/CLAUDE.md
#  읽고 [보드 모델] [원하는 동작] 만들어줘"
#
# 예시:
#   "i2r-03 출력1번 1초 간격으로 ON OFF 해줘"
#   "i2r-04 입력1 들어오면 출력1 나가게 해줘"
#   "i2r-03 온도 30도 넘으면 출력1 켜줘"

---

## 1. 보드 공통 정보

- MCU: ESP32
- 통신: Wi-Fi 802.11 b/g/n (2.4GHz)
- 개발환경: Arduino IDE
- 공식사이트: https://i2r.link
- 구매: https://i2r.link/products
- GitHub: https://github.com/kdi6033/i2r
- YouTube: https://www.youtube.com/@i2r-link

---

## 2. Arduino IDE 보드 설정 (필수)

```
툴 → 보드 → ESP32 Dev Module
Flash Size: 8MB
Partition Scheme: Custom (partitions.csv 사용)
Upload Speed: 921600
```

### 파티션 테이블 (partitions.csv)
프로젝트 폴더에 아래 내용으로 partitions.csv 파일 생성:
```csv
# Name,   Type, SubType, Offset,   Size
nvs,      data, nvs,     0x9000,   0x5000
otadata,  data, ota,     0xe000,   0x2000
app0,     app,  ota_0,   0x10000,  0x280000
app1,     app,  ota_1,   0x290000, 0x280000
coredump, data, coredump,0x510000, 0x10000
spiffs,   data, spiffs,  0x520000, 0x1E0000
```

---

## 3. 보드별 핀맵

### i2r-02 (4채널 입출력)
| 기능 | GPIO | 비고 |
|------|------|------|
| OUT1 | 26 | 릴레이1 (HIGH=ON) |
| OUT2 | 27 | 릴레이2 (HIGH=ON) |
| OUT3 | 32 | 릴레이3 (HIGH=ON) |
| OUT4 | 33 | 릴레이4 (HIGH=ON) |
| IN1 | 16 | 디지털 입력1 |
| IN2 | 17 | 디지털 입력2 |
| IN3 | 18 | 디지털 입력3 |
| IN4 | 19 | 디지털 입력4 |
| LED | 2 | 내장 LED |
| TRIGGER | 34 | 공장 초기화 |

### i2r-03 (4채널 입출력 + 온습도 센서)
| 기능 | GPIO | 비고 |
|------|------|------|
| OUT1 | 26 | 릴레이1 (HIGH=ON) |
| OUT2 | 27 | 릴레이2 (HIGH=ON) |
| OUT3 | 32 | 릴레이3 (HIGH=ON) |
| OUT4 | 33 | 릴레이4 (HIGH=ON) |
| IN1 | 16 | 디지털 입력1 |
| IN2 | 17 | 디지털 입력2 |
| IN3 | 18 | 디지털 입력3 |
| IN4 | 19 | 디지털 입력4 |
| SDA (I2C) | 21 | AHT21 온습도 센서 |
| SCL (I2C) | 22 | AHT21 온습도 센서 |
| LED | 2 | 내장 LED |
| TRIGGER | 34 | 공장 초기화 |

### i2r-04 (8채널 입출력)
| 기능 | GPIO | 비고 |
|------|------|------|
| OUT1 | 26 | 릴레이1 (HIGH=ON) |
| OUT2 | 27 | 릴레이2 (HIGH=ON) |
| OUT3 | 32 | 릴레이3 (HIGH=ON) |
| OUT4 | 33 | 릴레이4 (HIGH=ON) |
| OUT5 | 21 | 릴레이5 (HIGH=ON) |
| OUT6 | 22 | 릴레이6 (HIGH=ON) |
| OUT7 | 23 | 릴레이7 (HIGH=ON) |
| OUT8 | 25 | 릴레이8 (HIGH=ON) |
| IN1 | 18 | 디지털 입력1 |
| IN2 | 19 | 디지털 입력2 |
| IN3 | 4 | 디지털 입력3 |
| IN4 | 5 | 디지털 입력4 |
| IN5 | 12 | 디지털 입력5 |
| IN6 | 13 | 디지털 입력6 |
| IN7 | 14 | 디지털 입력7 |
| IN8 | 15 | 디지털 입력8 |
| LED | 2 | 내장 LED |
| TRIGGER | 36 | 공장 초기화 |

---

## 4. 필수 라이브러리

| 라이브러리 | 검색어 | 용도 | 보드 |
|-----------|--------|------|------|
| Adafruit AHTX0 | Adafruit AHTX0 | AHT21 온습도 | i2r-03 |

> 설치: Arduino IDE → 스케치 → 라이브러리 포함하기 → 라이브러리 관리

---

## 5. 보드별 베이스 코드

### [i2r-02 베이스 코드]

```cpp
// ============================================================
// i2r-02 IoT PLC 베이스 코드
// 입력: 4채널 (IN1~IN4)
// 출력: 4채널 릴레이 (OUT1~OUT4)
// ============================================================

// 출력 핀 (릴레이, HIGH=ON)
#define OUT1 26
#define OUT2 27
#define OUT3 32
#define OUT4 33

// 입력 핀
#define IN1 16
#define IN2 17
#define IN3 18
#define IN4 19

// 내장 LED
#define LED_PIN 2

void setup() {
  Serial.begin(115200);

  // 출력 핀 초기화
  pinMode(OUT1, OUTPUT); digitalWrite(OUT1, LOW);
  pinMode(OUT2, OUTPUT); digitalWrite(OUT2, LOW);
  pinMode(OUT3, OUTPUT); digitalWrite(OUT3, LOW);
  pinMode(OUT4, OUTPUT); digitalWrite(OUT4, LOW);

  // 입력 핀 초기화
  pinMode(IN1, INPUT);
  pinMode(IN2, INPUT);
  pinMode(IN3, INPUT);
  pinMode(IN4, INPUT);

  // LED 초기화
  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, HIGH);

  Serial.println("i2r-02 PLC 시작");
}

void loop() {
  // ★ 사용자 로직 추가 구역


}
```

---

### [i2r-03 베이스 코드]

```cpp
// ============================================================
// i2r-03 IoT PLC 베이스 코드
// 입력: 4채널 (IN1~IN4)
// 출력: 4채널 릴레이 (OUT1~OUT4)
// 센서: AHT21 온습도 (I2C: SDA=21, SCL=22)
// ============================================================
#include <Adafruit_AHTX0.h>

// 출력 핀 (릴레이, HIGH=ON)
#define OUT1 26
#define OUT2 27
#define OUT3 32
#define OUT4 33

// 입력 핀
#define IN1 16
#define IN2 17
#define IN3 18
#define IN4 19

// 내장 LED
#define LED_PIN 2

Adafruit_AHTX0 aht;
unsigned long lastSensorRead = 0;
float currentTemp = 0;
float currentHumi = 0;

void setup() {
  Serial.begin(115200);

  // 출력 핀 초기화
  pinMode(OUT1, OUTPUT); digitalWrite(OUT1, LOW);
  pinMode(OUT2, OUTPUT); digitalWrite(OUT2, LOW);
  pinMode(OUT3, OUTPUT); digitalWrite(OUT3, LOW);
  pinMode(OUT4, OUTPUT); digitalWrite(OUT4, LOW);

  // 입력 핀 초기화
  pinMode(IN1, INPUT);
  pinMode(IN2, INPUT);
  pinMode(IN3, INPUT);
  pinMode(IN4, INPUT);

  // LED 초기화
  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, HIGH);

  // AHT21 센서 초기화
  Wire.begin(21, 22); // SDA=21, SCL=22
  if (!aht.begin()) {
    Serial.println("❌ AHT21 센서 초기화 실패");
  } else {
    Serial.println("✅ AHT21 센서 초기화 성공");
  }

  Serial.println("i2r-03 PLC 시작");
}

void readSensor() {
  if (millis() - lastSensorRead < 2000) return;
  lastSensorRead = millis();
  sensors_event_t humidity, temp;
  aht.getEvent(&humidity, &temp);
  currentTemp = temp.temperature;
  currentHumi = humidity.relative_humidity;
  Serial.print("온도: "); Serial.print(currentTemp, 1); Serial.println("°C");
  Serial.print("습도: "); Serial.print(currentHumi, 1); Serial.println("%");
}

void loop() {
  readSensor(); // 2초마다 센서 읽기

  // ★ 사용자 로직 추가 구역
  // currentTemp, currentHumi 변수 사용 가능
  // digitalRead(IN1~IN4) 입력 읽기
  // digitalWrite(OUT1~OUT4, HIGH/LOW) 출력 제어


}
```

---

### [i2r-04 베이스 코드]

```cpp
// ============================================================
// i2r-04 IoT PLC 베이스 코드
// 입력: 8채널 (IN1~IN8)
// 출력: 8채널 릴레이 (OUT1~OUT8)
// ============================================================

// 출력 핀 (릴레이, HIGH=ON)
#define OUT1 26
#define OUT2 27
#define OUT3 32
#define OUT4 33
#define OUT5 21
#define OUT6 22
#define OUT7 23
#define OUT8 25

// 입력 핀
#define IN1 18
#define IN2 19
#define IN3 4
#define IN4 5
#define IN5 12
#define IN6 13
#define IN7 14
#define IN8 15

// 내장 LED
#define LED_PIN 2

// 출력 핀 배열 (반복 처리용)
int outputPins[] = {OUT1, OUT2, OUT3, OUT4, OUT5, OUT6, OUT7, OUT8};
int inputPins[]  = {IN1,  IN2,  IN3,  IN4,  IN5,  IN6,  IN7,  IN8};

void setup() {
  Serial.begin(115200);

  // 출력 핀 초기화
  for (int i = 0; i < 8; i++) {
    pinMode(outputPins[i], OUTPUT);
    digitalWrite(outputPins[i], LOW);
  }

  // 입력 핀 초기화
  for (int i = 0; i < 8; i++) {
    pinMode(inputPins[i], INPUT);
  }

  // LED 초기화
  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, HIGH);

  Serial.println("i2r-04 PLC 시작");
}

void loop() {
  // ★ 사용자 로직 추가 구역
  // digitalRead(IN1~IN8) 입력 읽기
  // digitalWrite(OUT1~OUT8, HIGH/LOW) 출력 제어


}
```

---

## 6. Claude 응답 규칙

사용자가 보드 모델과 원하는 동작을 말하면
반드시 아래 형식으로 완성 코드를 출력한다.

### ✅ 완성 코드
(해당 보드 베이스 코드 기반, ★ 구역에만 로직 추가, 바로 업로드 가능)

### 📌 수정된 부분
| 위치 | 수정 내용 |
|------|----------|
| (위치) | (내용) |

### 🔧 Arduino IDE 업로드 순서
1. Arduino IDE 열기
2. 완성 코드 전체 복사 → 붙여넣기
3. 툴 → 보드 → **ESP32 Dev Module** 선택
4. 툴 → 포트 → COM 포트 선택
5. ➡️ 업로드 클릭
6. 시리얼 모니터 115200으로 동작 확인

### ❓ 오류 해결표
| 오류 | 해결 |
|------|------|
| Adafruit_AHTX0.h not found | 라이브러리 매니저 → Adafruit AHTX0 설치 |
| 업로드 실패 | BOOT 버튼 누른 채 업로드 클릭 |
| 포트 인식 안됨 | 데이터 전송 가능 USB 케이블로 교체 |
| 릴레이 안됨 | HIGH=ON 확인, 전원 공급 확인 |
| 센서 오류 | I2C 배선 확인 (SDA=21, SCL=22) |

---

## 7. 사용 예시 모음

```
출력 제어:
"i2r-02 출력1번 1초 간격으로 ON OFF 해줘"
"i2r-04 출력1~4번 순서대로 0.5초 간격으로 켜줘"
"i2r-03 출력 전체 동시에 켜줬다가 꺼줘"

입력 연동:
"i2r-02 입력1 들어오면 출력1 나가게 해줘"
"i2r-04 입력1 ON이면 출력1 ON, 입력2 ON이면 출력2 ON"
"i2r-03 입력1 누르면 출력1 토글해줘"

센서 제어 (i2r-03):
"i2r-03 온도 30도 넘으면 출력1 켜줘"
"i2r-03 습도 60% 이하면 출력2 켜줘"
"i2r-03 온도 25~30도 유지되게 출력1 자동 제어해줘"

복합 동작:
"i2r-03 입력1 들어오면 출력1 켜고 3초 후 자동으로 꺼줘"
"i2r-04 입력1~4 중 하나라도 들어오면 출력1 켜줘"
"i2r-03 온도 30도 넘으면 출력1 켜고 시리얼로 경고 출력해줘"
"i2r-02 입력1 ON이면 출력1 ON, 입력2 ON이면 출력1 OFF 해줘"
```
