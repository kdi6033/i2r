# ✅ i2r IoT PLC (Physical · On-Device AI · Edge Controller Lineup)

📌 i2r 플랫폼은  
- **코드 작성 없이 UI 입력만으로 동작하는 PLC**
- **센서 중심의 Physical AI 제어**
- **On-Device AI 기반 현장 판단**
- **Edge Controller 기반 즉시 실행**

을 핵심 개념으로 설계된 **클라우드 연동 IoT PLC 플랫폼**입니다.

📌 MQTT · MongoDB · React UI · Python을 연동하여  
- 센서 데이터 수집
- 제어 조건 및 규칙 UI 설정
- 실시간 상태 모니터링
- PLC 출력 및 액추에이터 제어

를 하나의 통합 환경에서 제공합니다.

📌 ESP32 기반 IoT PLC는  
- Wi-Fi / Bluetooth / RS-485 / MQTT 통신을 지원하며
- 센서 입력을 Edge 단에서 즉시 해석하고
- On-Device AI 판단 결과에 따라
- PLC 출력과 외부 제어 시스템을 자동으로 동작시킵니다.

📌 이를 통해 **입력(Sensor) → 판단(AI) → 출력(Control)** 이  
- 프로그램 없이
- UI 설정만으로
- 산업 현장에서 안정적으로 실행되는  
**Physical AI 기반 Edge PLC 제어 구조**를 구현합니다.

---

## 📺 i2r 공식 채널 및 자료 링크
- 🛒 i2r 제품구매: href="https://i2r.link/products
- 💻 GitHub: https://github.com/kdi6033  
- 📺 YouTube: https://www.youtube.com/@i2r-link  
- 🌐 공식 사이트: https://i2r.link  
- 📧 문의: kdi6033@doowon.ac.kr
  
---

## 🔷i2r IoT PLC

| i2r-02<br>IoT PLC (4ch) | i2r-03<br>IoT PLC (4ch 센서) | i2r-04<br>IoT PLC (8ch) | i2r-04-motor<br>모터제어  |
| :---: | :---: | :---: | :---: |
| <img src="https://github.com/kdi6033/i2r-02/raw/main/images/i2r-02-kc.png?raw=true" height="150"> | <img src="https://github.com/kdi6033/i2r-03/raw/main/images/i2r-03-kc.png?raw=true" height="140"> | <img src="https://github.com/kdi6033/i2r-04/raw/main/images/i2r-04-kc.jpg?raw=true" height="140"> | <img src="https://github.com/kdi6033/i2r-04/raw/main/images/case-i2r-04-motor.png?raw=true?raw=true" height="150"> |
| <img src="https://github.com/kdi6033/i2r-02/raw/main/images/case-i2r02-iso.png?raw=true" height="130"> | <img src="https://github.com/kdi6033/i2r-03/raw/main/images/case-i2r03-iso1.png?raw=true" height="160"> | <img src="https://github.com/kdi6033/i2r-04/raw/main/images/case-i2r04-3.png?raw=true" height="150"> | <img src="https://github.com/user-attachments/assets/7e89cdee-cd46-428f-a51d-386c9fe9e315?raw=true" height="150"> |
| <img src="https://github.com/kdi6033/i2r-02/raw/main/images/case-i2r02-kc.png?raw=true" height="140"> | <img src="https://github.com/kdi6033/i2r-03/raw/main/images/case-i2r03-kc.png?raw=true" height="140"> | <img src="https://github.com/kdi6033/i2r-04/raw/main/images/case-i2r04-kc.png?raw=true" height="135"> |  |

## 🔷i2r IoT PLC 회로도
| i2r-02 | i2r-03| i2r-04 | i2r-04-motor |
| :---: | :---: | :---: | :---: |
| <img src="https://github.com/kdi6033/i2r-02/raw/main/images/i2r-02-pin-con.png?raw=true" height="150"> | <img src="https://github.com/kdi6033/i2r-03/raw/main/images/i2r-03-pin-con.png?raw=true" height="140"> | <img src="https://github.com/kdi6033/i2r-04/raw/main/images/i2r-04-circuit.png?raw=true?raw=true" height="140"> | <img src="https://github.com/kdi6033/i2r-04/raw/main/images/i2r-04-motor-circiut.jpg?raw=true?raw=true?raw=true" height="150"> |
| <img src="https://github.com/kdi6033/i2r-02/raw/main/images/i2r-02-1.png?raw=true" height="130"> | <img src="https://github.com/kdi6033/i2r-03/raw/main/images/i2r-03-port.jpg?raw=true?raw=true" height="150">| <img src="https://github.com/kdi6033/i2r-04/raw/main/images/i2r-04-pin.jpg?raw=true?raw=true" height="150"> | |


## 🔷i2r IoT PLC 사양
| i2r-02 | i2r-03| i2r-04 | i2r-04-motor |
| :---: | :---: | :---: | :---: |
| - 정격전압 : 5V DC, 보드내에서는 5V로 설계했습니다.
- 입력전압 : 7V에서 26V DC Free Volt, 7V에서 26V 사이 전압을 공급하면         레귤레이터에서 5V 로 전원을 공급합니다.
- 작동온도 : -40 ℃ - 85 ℃
- 입력 : 4개, 접점만 연결되면 동작합니다. 별도의 전압을 인가하면 고장의 원인이 됩니다.
- 출력 : 1개는 30A 250VAC/30VDC
3개는 10A VAC, 10A VDC, 10A 125VAC, 10A 28VDC
- 통신: WIFI 802.11 b / g / n (802.11n에서 최대 150Mbps) 및 Bluetooth 4.2 BR / EDR + BLE
와이파이는 2.4G에 연결하세요. 5G는 동작하지 않습니다.
- RS232 통신 : 보드내에 TTL Level의 rx, tx 단자가 있습니다.
 | i2r-03| i2r-04 | i2r-04-motor |


---

**사용 방법**   
- React 웹앱 기반 모니터링 및 제어: 다양한 환경에서 실시간으로 모니터링하고 제어할 수 있습니다.    
- 로컬 컴퓨터: 로컬 네트워크를 통해 기기를 모니터링하고 제어할 수 있습니다.
- AWS 클라우드: 클라우드 기반으로 원격지에서도 기기의 상태를 모니터링하고 제어가 가능합니다.     
- 스마트폰 애플리케이션: 모바일 앱을 통해 언제 어디서나 기기의 상태를 확인하고 제어할 수 있습니다.

**스마트폰,탭,PC로 제어**    
""https://i2r.link**  접속하면 페이지마다 유튜브 링크를 따라 해보시면 쉽게 사용할 수 있습니다.

## ✅ 프로토콜
**2025년7월15일 chatgpt에 적합한 프로토콜을 새로 작성하고 있습니다. 이전에 구매한 보드는 7월30일 이후 새로운 펌웨어를 다운 받아 주세요**

- i2r 보드의 mqtt 통신에서는 아래와 같이 구성되어 email을 저장하면 다음 토픽으로 자신에 해당되는 데이터를 통신 할 수 있습니다.     
- 이 문서는 i2r IoT 보드와 클라이언트 간 MQTT 통신 시 사용하는 JSON 기반 명령어 프로토콜을 설명합니다.  
- 모든 메시지는 경량화를 위해 **축약된 필드명**과 **축약된 명령어 코드(`c`)**를 사용합니다.

#### 기본 MQTT 토픽 구조
---
- **intopic**  : `i2r/{email}/in`  
- **outtopic** : `i2r/{email}/out`

> `email`은 각 사용자의 고유 ID 역할을 합니다.
---

### JSON 메시지 필드명 요약

| 전체 명칭         | 축약 코드 | 설명                                                                           |
| ----------------- | -------- | ------------------------------------------------------------------------------- |
| adc               | `adc`    | analog to digital, 센서 ad converter (예: `3.4`)                                 |
| bat               | `bat`    | battaery output, 센서 보드에 들어오는 밭데리 전압 (예: `3.4`)                      |
| command           | `c`      | 명령 종류 (예: `df`, `so`, `gs`, `sch`, `bs` 등 축약어 사용)                      |
| calibration       | `cali`   | 	센서값 보정 (예: 28.1)                                                         |
| delay             | `d`      | 입력신호가 들어오고 출력이 나가기 까지 지연시간 단위:초                              |
| duration          | `du`     | 센서에 의해서 동작할 때 동작시간 0이면 무한대로 지속함                               |
| dayOfWeek         | `dw`     | 반복 요일: 숫자(0=일 \~ 6=토), 또는 배열 `[1,3,5]` (월, 수, 금)                     |
| email             | `e`      | email                                                                            |
| endMinutes (분)   | `end`    | 종료 시간 (예: 오전 10시 = `600`)                                                 |
| fileName          | `f`      | file Name                                                                       |
| from              | `fr`     | 메세지를 보내는 기기의 mac 주소                                                   |
| getStatus         | `gs`     | 보드 상태 요청 (온도, 습도, in/out 등)                                            |
| humidity          | `humi`   | 센서 현재 습도 값 (예: `55`)                                                       |
| in                | `in`     | 입력 상태 배열 (예: `[0,1,0,0]`)                                                  |
| light             | `light`  | 센서 조도 값 (예: `120`)                                                          |
| mac               | `m`      | 대상 장치의 MAC 주소 (예: `"A0:B7:65:CD:4D:34"`)                                  |
| portNo            | `n`      | 출력 핀 번호 (0부터 시작)                                                         |
| value             | `v`      | 출력 값: `true` 또는 `false`, 혹은 수치 값                                        |
| operation         | `o`      | 작업 종류: `"save"`, `"list"`, `"delete"`, `"deleteAll"`, `"cali"`, `"insert"` 등 |
| out               | `out`    | 출력 상태 배열 (예: `[1,0,0,0]`)                                                  |
| pinIndex          | `pi`     | 출력 핀 인덱스 (0\~3)                                                             |
| pageNo            | `pn`     | 	list 에서 데이터의 번호                                                        |
| portState         | `ps`     | 제어할 출력 포트 정보 배열 (예: `[{"m": "...", "n": 0, "v": true}]`)               |
| repeatMode        | `rm`     | 반복 주기: `0` = 매일, `1` = 매주                                                  |
| slotIndex         | `sI`     | 스케줄 작업시 슬롯 (번호)인덱스 지정                                               |
| startMinutes (분) | `start`  | 시작 시간 (예: 오전 9시 30분 = `570`)                                             |
| temperature       | `temp`   | 센서 현재 온도 값 (예: `27.8`)                                                    |
| trigger           | `tr`     | `bio`: ON(1) OFF(0) 가 될 때 트리거 설정 후 delay를 설정하면 그 시간에 동작한다.   |
| triggerValue      | `tv`     | 트리거가 동작하는 센서 값                                                        |
| type              | `t`      | 보드 종류 (예: `3` = i2r-03)                                                    |
| typeSensor        | `ts`     | 센서 타입 (`temp`, `humi`, `light`)                                             |

---

### 명령어 (command : c) 축약 코드 목록

| 전체 명칭           | 축약 코드 (`c`)   | 설명 |
|---------------------|------------------|------|
| `bindIO`           | `bio`            | 입력 상태에 따라 출력 연동 설정  |
| `bindSensor`       | `bs`             | 센서 조건에 따라 출력 제어 (온도, 습도, 조도 등) |
| `downloadFirmware` | `df`             | 보드에 펌웨어를 다운로드 |
| `schedule`         | `sch`            | 시간 기반 출력 동작 스케줄 설정  | 
| `setInfo`          | `si`             | Wi-Fi, MQTT 브로커 등 설정 정보 전송 |
| `setOutput`        | `so`             | 핀출력을 표시 (1 = ON, 0 = OFF) |
| `touchInput`       | `ti`            | Touch Panel(RP2040 등) 전달 |

---
### 예제 및 상세 설명 

| `command` (`c`) | 예제 및 상세 설명 |
|----------------|-------------------|
| **`downloadFirmware`**<br> (`df`) |인터넷에서 통신으로 펌웨어를 보드로 내려 받는다<br> {"c":"df","m":"D8:13:2A:C3:E7:68","fileName":"i2r-03.ino.bin"} |
| **`setInfo`** <br>(`si`) |와이파이 및 통신에 필요한 정보를 보내 보드에 기록하여 기기는 여기 정보로 통신을 연결한다.<br> {"c":"si",'ssid':'***','password'='***', 'e':'***', 'mqttBroker':'ai.doowon.ac.kr'}} |
| **`bindIO`**<br> (`bio`) | **`bind_input_output`**<br>아래 상세설명 참조|
| **`bindSensor`**<br> (`bs`) | 아래 상세설명 참조 |:
| **`downloadFirmware`**<br> (`df`) | ```{ "c": "df", "m": "D8:13:2A:C3:E7:68", "fileName": "i2r-03.ino.bin" }``` <br>지정한 MAC 주소를 가진 보드에 인터넷을 통해 펌웨어를 다운로드합니다. `.ino.bin` 또는 `.bin` 파일이 대상이며, OTA 업데이트를 통해 자동 적용됩니다. |
| **`getStatus`**<br> (`gs`) | ```{ "c": "gs", "m": "EC:64:C9:43:E8:B8" }```<br>지정 보드의 상태를 요청합니다. 응답으로 온도, 습도, 입력포트(`in`), 출력포트(`out`) 정보가 포함됩니다.<br>응답 예시:<br>`{"t":3,"email":"kdi6033@gmail.com","m":"EC:64:C9:43:E8:B8","temp":28.4,"humi":38,"in":[0,0,0,0],"out":[0,0,0,0]}` |
| **`scheduleOutput`**<br> (`sch`) | 아래 상세설명 참조 |
| **`setInfo`**<br> (`si`) | ```{ "c": "si", "ssid": "i2r_wifi", "password": "00000000", "email": "user@example.com", "mqttBroker": "mqtt.i2r.link" }``` <br> 보드가 Wi-Fi 및 MQTT 브로커에 연결할 수 있도록 설정 정보를 저장합니다. 이후 재시작 시 자동 연결됩니다. |
| **`setOutput`**<br> (`so`) | ```{ "c": "so", "m": "A0:B7:65:CD:4D:34", "n": 1, "v": 1 }``` <br> 지정 보드의 `n`번 출력 핀을 제어합니다. `v: 1`은 ON, `v: 0`은 OFF입니다. 릴레이, 모터, LED 등에 사용됩니다. |
| **`touchInput`**<br> (`ti`) | ```{ "c": "ti", "light": 120 }```<br>RP2040 등의 외부 터치패널에서 측정한 조도 값을 IoT 보드에 전달하여 조건 제어에 활용할 수 있습니다. |

#### ✅ 스케줄 제어 프로토콜 (Schedule / c: "sch")

- 스케줄 기능은 특정 시간대에 PLC 출력을 자동으로 ON/OFF 제어하는 기능입니다.
- 즉, “매일 또는 특정 요일에 정해진 시간에 자동으로 스위치를 켜거나 끄는 기능”을 수행합니다.
- 모든 설정은 MQTT 메시지(JSON 형식)으로 전송됩니다.

1️⃣ 매일 스케줄 등록 (Insert) <br>

- 매일 10:44부터 10:45까지 MAC 주소 "D4:8C:49:50:46:F4" 장치의 0번 포트 출력을 켜는 스케줄을 등록합니다. <br>
- "rm":"daily"는 매일 반복, "dw":0은 요일(일요일)을 의미하며 "dw"가 생략되면 daily 모드로 동작합니다. <br>
- start와 end는 자정(00:00) 기준 분 단위입니다. 예: 10:44 → 10×60 + 44 = 644, 10:45 → 645

- Full JSON (개발용 / 디버그용) <br>
{"command": "schedule","operation": "insert","mac": "D4:8C:49:50:46:F4","pinIndex": 0,"startMinutes": 644,"endMinutes": 645,"repeatMode": "daily","dayOfWeek": 0} <br>
- Compressed JSON (MQTT 실제 전송) <br>
```
{"c": "sch","m": "D4:8C:49:50:46:F4","o": "insert","pi": 0,"start": 644,"end": 645,"rm": "daily","dw": 0}
```

2️⃣ 매주 스케줄 등록 (Insert) <br>

- 매주 월요일(1), 수요일(3) 오전 10:50부터 10:51까지 <br>
- MAC 주소 "D4:8C:49:50:46:F4" 장치의 0번 포트 출력을 켜는 스케줄을 등록합니다. <br>
- "rm":"weekly"는 주간 반복을 의미하며, "dw":[1,3]은 월요일(1)과 수요일(3)에만 동작함을 뜻합니다. <br>
- "dw" 배열 값은 0=일, 1=월, 2=화, 3=수, 4=목, 5=금, 6=토입니다. <br>
- start와 end는 자정(00:00) 기준 분 단위입니다.  예: 10:50 → 10×60 + 50 = 650, 10:51 → 651 <br>
- "pi":0은 제어할 포트 번호입니다. <br>

- Full JSON (개발용 / 디버그용) <br>
{"c": "sch","m": "D4:8C:49:50:46:F4","o": "insert","pi": 0,"start": 650,"end": 651,"rm": "weekly","dw": [1, 3]}

- Compressed JSON (MQTT 실제 전송) <br>
```
{"c": "sch","m": "D4:8C:49:50:46:F4","o": "insert","pi": 0,"start": 650,"end": 651,"rm": "weekly","dw": [1, 3]
}
```

	
3️⃣ 매주 스케줄 목록 조회 (List) <br>
- 해 장치의 등록된 모든 스케줄을 조회합니다. <br>
- Full JSON (개발용 / 디버그용) <br>
{"command": "schedule","operation": "list","mac": "D4:8C:49:50:46:F4","pinIndex": 0} <br>

- Compressed JSON (MQTT 실제 전송) <br>
```
{"c": "sch","m": "D4:8C:49:50:46:F4","o": "list","pi": 0}
```
- 응답 예시 <br>
{"c": "sch","m": "D4:8C:49:50:46:F4","o": "list","pi": 0,"rm": "weekly","dw": [1,3],"start": 650,"end": 651,"slotIndex": 2} <br>


4️⃣ 매주 스케줄 삭제 (Delete)  <br>
특정 slotIndex를 지정하여 해당 스케줄 한 개만 삭제합니다.  <br>
"sI"는 slotIndex를 의미하며, 목록 조회(List) 결과에서 받은 값을 사용합니다.  <br>

- Full JSON (개발용 / 디버그용) <br>
{"command": "schedule","operation": "delete","mac": "D4:8C:49:50:46:F4","pinIndex": 0,"slotIndex": 2}  <br>

- Compressed JSON (MQTT 실제 전송) <br>
```
{"c": "sch","m": "D4:8C:49:50:46:F4","o": "delete","pi": 0,"sI": 2}
```

5️⃣ 매주 스케줄 전체 삭제 (DeleteAll)  <br>
- 해당 장치의 특정 포트(pi)에 등록된 모든 주간 스케줄을 삭제합니다.  <br>
- 여러 요일 또는 여러 시간대 스케줄을 한 번에 제거할 때 사용합니다.  <br>
- 
- Full JSON (개발용 / 디버그용) <br>
{"command": "schedule","operation": "deleteAll","mac": "D4:8C:49:50:46:F4","pinIndex": 0}  <br>

- Compressed JSON (MQTT 실제 전송) <br>
```
{"c": "sch","m": "D4:8C:49:50:46:F4","o": "deleteAll","pi": 0}
```
--------------------

#### ✅ 입출력 설정 프로토콜 예제 (bindIO / c:"bio")
1️⃣ 트리거 등록 <br>
입력 0번 포트가 ON 되면, → 출력 1번 포트를 ON 시킵니다. d:0 → 지연시간 없음 (즉시 실행) <br>
- Full JSON (개발용 / 디버그용) <br>
{"command": "bindIO", "operation": "insert", "trigger": true, "mac": "D4:D4:DA:73:87:3C", "portNo": 0, "delay": 0, "portState": [{ "mac": "D4:D4:DA:73:87:3C", "portNo": 1, "value": true }] } <br>
- Compressed JSON (MQTT 실제 전송) <br>
{ "c": "bio", "o": "i", "t": true, "m": "D4:D4:DA:73:87:3C", "n": 0, "d": 0, "ps": [ { "m": "D4:D4:DA:73:87:3C", "n": 1, "v": 1 }] } <br>

2️⃣ 트리거 목록 확인 (List) <br>
트리거 현황을 자동으로 요청하면 다음 메시지를 보냅니다. <br>
- Full JSON (개발용 / 디버그용) <br>
{ "command": "bindIO", "operation": "list", "mac": "D4:D4:DA:73:87:3C" } <br>
- Compressed JSON (MQTT 실제 전송) <br>
{ "c":"bio", "o":"l", "m":"D4:D4:DA:73:87:3C" } <br>
보드는 등록된 모든 트리거 목록을 응답합니다.  <br>
{ "c":"bio", "o":"l", "m":"D4:D4:DA:73:87:3C", "tr":[ {"n":0, "d":0, "ps":[{"n":1,"v":1}] }]}  <br>

3️⃣ 트리거 삭제 (Delete)  <br>
입력 0번 트리거를 삭제하려면 다음 메시지를 보냅니다. <br>
- Full JSON (개발용 / 디버그용) <br>
{ "command": "bindIO", "operation": "delete", "mac": "D4:D4:DA:73:87:3C", "portNo": 0 } <br>
- Compressed JSON (MQTT 실제 전송) <br>
{ "c": "bio", "o": "d", "m": "D4:D4:DA:73:87:3C", "n": 0 } <br>
----------------------------

#### ✅ 센서 트리거 프로토콜 예제 (bindSensor / c:"bs")    
- 센서의 측정값이 특정 상한(올라갈 때) 또는 하한(내려갈 때) 에 도달하면 지정한 기기의 출력을 자동으로 제어하는 기능입니다.  <br>
- 즉, “센서 값이 특정 조건을 만족하면 → **다른 장치(또는 본인)의 릴레이/스위치**를 제어”합니다. <br>
- 서로 다른 IoT PLC끼리도 연결이 가능하며 **중복 설정**도 가능 합니다. <br>

1️⃣ 트리거 등록 (Insert) <br>
습도센서의 온도가 55로 상승할 때 맥어드레스가 "D4:D4:DA:73:87:3C"인 기기의 0번 포트의 출력을 true로 한다. "du":0 가 0 이면 지속시간은 무한대 이다. <br>
- Full JSON (개발용 / 디버그용) <br>
{"command": "bindSensor","operation": "insert","mac": "D4:D4:DA:73:87:3C","type": "humidity","trigger": true,"triggerValue": 55,"duration": 0,
  "portState": [{"mac": "D4:D4:DA:73:87:3C","portNo": 0,"value": true}] }     <br> 
- Compressed JSON (MQTT 실제 전송) <br>
```
{"c":"bs","ts":"humi","m":"D4:D4:DA:73:87:3C","o":"insert","tr":1,"tv":55,"du":0,"ps":[{"m":"D4:D4:DA:73:87:3C","n":0,"v":1}]}
```

2️⃣ 트리거 목록 확인 (List) <br>
습도에 대한 리스트를 요청한다. <br>
- Full JSON (개발용 / 디버그용) <br>
{"command": "bindSensor","operation": "list","mac": "D4:D4:DA:73:87:3C","type": "humidity"} <br>
- Compressed JSON (MQTT 실제 전송) <br>
```
 {"c":"bs","ts":"humidity","m":"D4:D4:DA:73:87:3C","o":"list"}
```
- 응답예시 <br>
{"c":"bs","o":"list","ts":"humi","tr":1,"tv":55,"du":0,"sI":11,"ps":[{"m":"D4:D4:DA:73:87:3C","n":0,"v":1}],"e":"kdi6033@gmail.com","t":"3","fr":"D4:D4:DA:73:87:3C","m":"D4:D4:DA:73:87:3C"} <br>

3️⃣ 트리거 삭제 (Delete) <br>
습도센서에서 슬롯번호 1 의 설정을 제거한다. <br>
- Full JSON (개발용 / 디버그용) <br>
{"command": "bindSensor","operation": "delete","mac": "D4:D4:DA:73:87:3C","type": "humidity","slotIndex": 1} <br>
- Compressed JSON (MQTT 실제 전송) <br>
```
{"c":"bs","ts":"humidity","m":"D4:D4:DA:73:87:3C","o":"delete","sI":1}
```

4️⃣ 센서 타입 전체 삭제 (DeleteAll) <br>
습도센서의 설정된 모든 값을 제거한다. <br>
- Full JSON (개발용 / 디버그용) <br>
{"command": "bindSensor","operation": "calibration","mac": "D4:D4:DA:73:87:3C","type": "humidity","value": 44} <br>

- Compressed JSON (MQTT 실제 전송) <br>
```
 {"c":"bs","ts":"humidity","m":"D4:D4:DA:73:87:3C","o":"deleteAll"}
```

5️⃣ 센서 보정 (Calibration) <br>
습도센서의 현재 값을 44로 설정한다. <br>
- Full JSON (개발용 / 디버그용) <br>
{"command": "bindSensor","operation": "cali","mac": "D4:D4:DA:73:87:3C","type": "humidity","value": 44} <br>
- Compressed JSON (MQTT 실제 전송) <br>
```
{"c":"bs","ts":"humidity","m":"D4:D4:DA:73:87:3C","o":"cali","v":44}
```

----------------

# ✅ 아두이노 프로그램 설정    
<a href="https://youtu.be/UrJd-RHRh6U">
    <img src="https://github.com/user-attachments/assets/67556286-b878-44ef-9175-553a6aa418ef" alt="Updating the screen" width="400">
</a>    

[24-7 보드 아두이노 프로그램](https://github.com/user-attachments/assets/67556286-b878-44ef-9175-553a6aa418ef)

File->Preferences->Additional Boards Manager URLs    
https://dl.espressif.com/dl/package_esp32_index.json    
<img src="https://github.com/user-attachments/assets/06ad8c17-ff02-44dc-be2c-938445e5f4b6" width="50%" />   

Tools->Boars Manager   

<img src="https://github.com/user-attachments/assets/51f0ed8c-96f8-4c98-aa2b-f361b2235f68" width="30%" />

### partitions.csv 파일 작성
Flash 메모리 할당을 합니다.
Skech->Export Compiled Binary 를 실행하면 build 디렉토리가 만들어 집니다.
다음은 생성된 파일 용량 입니다.
```
2024-09-29  오전 09:44         1,932,784 board-i2r-03.ino.bin
2024-09-29  오전 09:44            24,896 board-i2r-03.ino.bootloader.bin
2024-09-29  오전 09:44        20,233,488 board-i2r-03.ino.elf
2024-09-29  오전 09:44        24,280,721 board-i2r-03.ino.map
2024-09-29  오전 09:44         8,388,608 board-i2r-03.ino.merged.bin
2024-09-29  오전 09:44             3,072 board-i2r-03.ino.partitions.bin
               6개 파일          54,863,569 바이트
```
i2r-03.ino.bin (1,932,784 바이트): 이 파일은 컴파일된 애플리케이션 바이너리입니다. 애플리케이션 자체가 약 1.8MB 크기로, 이는 플래시 메모리 내 app0 또는 app1 파티션에 저장됩니다.    

i2r-03.ino.bootloader.bin (24,896 바이트): 부트로더 파일로, 매우 작은 크기입니다. 일반적으로 부트로더는 플래시 메모리의 별도 파티션에 저장되며, 약 24KB 정도로 충분히 작은 크기입니다.    

i2r-03.ino.elf (20,233,464 바이트): ELF 파일은 디버그 정보가 포함된 파일로, 플래시 메모리에는 업로드되지 않고 컴파일 과정 중에만 사용됩니다. 즉, 이 파일은 실제로 디바이스에 영향을 미치지 않습니다.    

i2r-03.ino.map (24,273,503 바이트): 이 파일은 메모리 매핑 정보를 포함하는 파일로, 디버깅을 위해 사용됩니다. 이 역시 플래시 메모리에는 업로드되지 않으므로 실제 메모리 용량과는 무관합니다.    

i2r-03.ino.merged.bin (8,388,608 바이트): 이 파일은 애플리케이션, 부트로더, 파티션 테이블이 합쳐진 통합 바이너리 파일입니다. 이 크기가 플래시 메모리의 전체 크기와 일치하므로, 이 파일을 플래시 메모리에 업로드할 경우 전체 용량을 꽉 채우게 됩니다.   

i2r-03.ino.partitions.bin (3,072 바이트): 파티션 테이블 파일로, 작은 크기이므로 문제없이 플래시 메모리에 저장될 수 있습니다.    

1,932,784 board-i2r-03.ino.bin 이 파일이 실행파일은 1.95M 정도의 용량 입니다.
실행 파일을 위해 여유있게  2.5M, OTA를 위해 같은 용량 2.5M, SPIFF 에는 1.8M를 할당 하겠습니다.    
[ChatGPT]
```
2024-09-29  오전 09:44         1,932,784 board-i2r-03.ino.bin
2024-09-29  오전 09:44            24,896 board-i2r-03.ino.bootloader.bin
2024-09-29  오전 09:44        20,233,488 board-i2r-03.ino.elf
2024-09-29  오전 09:44        24,280,721 board-i2r-03.ino.map
2024-09-29  오전 09:44         8,388,608 board-i2r-03.ino.merged.bin
2024-09-29  오전 09:44             3,072 board-i2r-03.ino.partitions.bin
               6개 파일          54,863,569 바이트
실행 파일을 위해 여유있게  2.5M, OTA를 위해 같은 용량 2.5M, SPIFF 에는 1.8M를 할당해서 partitions.csv 파일 작성해줘
```
다음은 생성된 partitions.csv 파일 입니다.
```
# Name,   Type, SubType, Offset,  Size,   Flags
nvs,      data, nvs,     0x9000,  0x5000,
otadata,  data, ota,     0xe000,  0x2000,
app0,     app,  ota_0,   0x10000, 0x280000,  
app1,     app,  ota_1,   0x290000, 0x280000, 
spiffs,   data, spiffs,  0x510000, 0x180000  
```
- 첫 번째로 NVS 파티션은 비휘발성 저장소(Non-Volatile Storage)입니다. 이 영역은 설정값이나 작은 데이터를 영구적으로 저장하는데 사용됩니다. 예를 들어, 와이파이 연결 정보나 디바이스 설정 값과 같은 데이터를 저장할 수 있으며, 이 데이터는 전원을 껐다 켜도 유지됩니다. NVS는 EEPROM과 비슷한 역할을 하며, 이 테이블에서는 0x9000 오프셋에서 시작하여 20KB 크기로 할당되어 있습니다. Offset: 0x9000 에서 시작해서 Size: 0x5000 (20KB) 할당

- 두 번째로 OTA 데이터 파티션은 OTA 업데이트를 관리하는데 사용됩니다. OTA(Over-The-Air) 업데이트는 디바이스의 펌웨어를 무선으로 업데이트할 수 있는 기능인데, 이 파티션은 현재 실행 중인 애플리케이션과 업데이트 상태를 저장하는 역할을 합니다. OTA 업데이트가 진행될 때, 시스템이 어떤 애플리케이션을 실행할지 결정하는 중요한 정보를 여기에 저장합니다. 이 파티션은 0xe000 오프셋에서 시작하며, 8KB의 크기를 가집니다. Offset: 0xe000 에서 시작해서 Size: 0x2000 (8KB) 할당

- 세 번째와 네 번째로 app0과 app1 파티션은 각각 OTA 업데이트를 위한 애플리케이션 저장 공간입니다. 일반적으로 ESP32는 두 개의 애플리케이션 파티션을 가집니다. 하나는 현재 실행 중인 애플리케이션이 저장된 공간이고, 다른 하나는 새로운 업데이트를 다운로드할 공간입니다. 예를 들어, 현재 실행 중인 애플리케이션은 app0에 저장되어 있고, OTA 업데이트를 통해 새로운 펌웨어가 app1에 다운로드됩니다. 업데이트가 완료되면 다음에 디바이스가 부팅될 때 app1에서 애플리케이션이 실행됩니다. app0과 app1 파티션은 각각 2.5MB 크기로 할당되어 있어 대규모 애플리케이션을 저장할 수 있습니다. app0 는 Offset: 0x10000 에서 시작해서 Size: 0x280000 (2.5MB) 할당, app1는 Offset: 0x290000 에서 시작해서 Size: 0x280000 (2.5MB) 할당

- 마지막으로 SPIFFS 파티션은 파일 시스템 저장 공간입니다. SPIFFS는 플래시 메모리를 기반으로 한 파일 시스템으로, 디바이스가 HTML 파일, 이미지, 스크립트 파일 등 다양한 파일 데이터를 저장하고 읽을 수 있도록 도와줍니다. 예를 들어, 웹서버를 구현하는 경우 웹 페이지의 정적 파일을 SPIFFS에 저장할 수 있습니다.  이 파티션은 1.5MB 크기로 할당되어 있으며, 시스템이 파일 기반 데이터를 관리할 수 있는 중요한 공간입니다. Offset: 0x510000 에서 시작해서 Size: 0x180000 (1.5MB) 할당.

# ✅ 아마존 크라우드 AWS IoT 서버  (React)     
react로 구축한 서버는 제 github "React"에 정리해 놓았습니다.

<table>
  <tr>
    <td>
      <a href="https://youtu.be/n1MRXSVtbBI">
        <img src="https://github.com/user-attachments/assets/8a2ccaba-8b4a-44a1-8ac9-556d96cbd0ad" alt="AWS Instal EC2 Ubuntu Server 22.04" width="400">
      </a>
    </td>
    <td>
      <a href="https://youtu.be/5ojpKiQ00qk">
        <img src="https://github.com/user-attachments/assets/10dfdc4e-d581-4cfe-92f1-8a700069e1f4" alt="AWS IOT Core Mqtt" width="400">
      </a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://youtu.be/mruzmon95BE">
        <img src="https://github.com/user-attachments/assets/bb05f92c-e8d3-4ca2-a0c4-7a97adb5c08f" alt="AWS IOT Core Mqtt" width="400">
      </a>
    </td>
    <td>
      <a href="https://youtu.be/WJrOxAN7ZH0">
        <img src="https://github.com/user-attachments/assets/69d1455b-cbb1-4f09-b0c2-356d4bbcc515" alt="AWS IOT Core Mqtt" width="400">
      </a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://youtu.be/vLT3sr_xAFE">
        <img src="https://github.com/user-attachments/assets/7c56667a-631c-4bc4-a681-a7a4a49cb729" alt="AWS IoT server" width="400">
      </a>
    </td>
    <td>
      <a href="https://youtu.be/Q7IL_ERRIwI">
        <img src="https://github.com/user-attachments/assets/5f8fae58-d80b-4d26-b863-c20c24a20021" alt="AWS IoT 보안 server" width="400">
      </a>
    </td>
  </tr>
</table>


<br>

[mongoDB 설치순서](https://github.com/kdi6033/i2r/blob/main/txt/aws%20mongoDB%20install)    

## ✅ PC IoT 서버 (React)    
** 앞으로 다른 바쁜 작업이 끝나고 나면 정리해서 올리겠습니다.
- PC에서 React 와 mongoDB를 설치하여 인터넷 상에서 제어한다.
- 어플에서 IoT-PLC를 와이파이에 접속만 시키면 데이터베이스에 자동 저장되고 제어판넬이 자동으로 생성되어서 모니터링/제어를 할 수 있다.

<table>
  <tr>
    <td>
        <a href="https://youtu.be/5spmnQX0IjM">
            <img src="https://github.com/user-attachments/assets/9da548f6-9872-48d7-846c-e790586c5511" alt="mongodb, compass 윈도우용 설치하기 " width="400">
        </a>  
    </td>
    <td>
        mongoDB에 데이터가 자동으로 저장 된 모습    
        <img src="https://github.com/user-attachments/assets/1c8ee718-8561-4eeb-bdd4-366b209b9fc6" width="400">    <br>
    </td>
  </tr>
</table>


## ✅ IoT PLC HMI 한글 터치스크린 ChatGPT

- ESP32 IoT PLC와 CrowPanel(RP2040)을 RS232 직렬 통신으로 연결하여,
- CrowPanel은 사용자 인터페이스(UI) 및 I2C 센서 계측을 담당하고,
- ESP32는 릴레이 제어 및 클라우드(MQTT) 연동을 담당하는 IoT 제어 시스템입니다.
- IoT PLC는  CrowPanel(RP2040) 터치 스크린을 사용합니다. 와이파이가 있는 제품을 전파인증을 받아 판매해야 함으로 인증이 필요없는 제품을 선택했습니다. 아래는 당사의 기술자료 입니다. 

**시스템 구성**
| 항목             | 설명                                         |
| -------------- | ------------------------------------------ |
| **RS232 마스터**  | CrowPanel (RP2040)                         |
| **RS232 슬레이브** | ESP32                                      |
| **센서 계측**      | CrowPanel에서 I2C로 직접 계측 (조도, 온습도 등)         |
| **UI 이벤트**     | 터치 버튼 입력 → RS232 메시지 전송 (`{"cmd":"on"}` 등) |
| **액츄에이터 제어**   | ESP32에서 명령 수신 후 릴레이/모터 제어                  |
| **클라우드 연동**    | ESP32 → MQTT 전송 (선택적 기능)                   |

**연결 방식**    
- CrowPanel (RP2040) ↔ ESP32 (IoT PLC)
    - RS232 직렬 통신 사용
    - 안정적인 양방향 데이터 전송 지원
- 센서 계측 (CrowPanel 내부)
    - RP2040이 I2C 버스로 조도, 온도, 습도 등 센서를 직접 읽음
    - I2C는 최대 32바이트 프레임 제한과 양방향 통신의 한계가 있어, PLC와 UI 간 통신에는 적합하지 않음
    - 따라서 UI ↔ PLC 통신은 RS232, 센서 ↔ RP2040 통신만 I2C로 유지

### CrowPanel Pico Display 3.5" HMI 모듈

이 보드는 RP2040 MCU + 3.5" 480×320 TFT LCD + 정전식 터치스크린이 결합된 HMI(Human Machine Interface) 모듈입니다. LVGL, C/C++, MicroPython을 지원하여 다양한 UI 및 IoT 응용에 활용할 수 있습니다.

<img src="https://github.com/user-attachments/assets/15416181-7861-4fea-976b-fcb33cc896f0" alt="회로도" width="700">

**📌 주요 기능**
- RP2040 듀얼코어 MCU 내장 → 외부 보드 없이 단독 동작 가능
- 3.5인치 480×320 해상도 TFT 디스플레이 → 선명한 그래픽 표현
- 정전식 터치스크린 → 직관적인 UI 제어 가능
- LVGL 지원 → 버튼, 슬라이더, 차트, 키보드 등 고급 GUI 구성
- USB-C 포트 → 전원 공급 및 펌웨어 업로드 지원
- C/C++ & MicroPython 개발 환경 → 초보자부터 전문가까지 사용 가능
- GPIO 확장 핀 제공 → 센서, 액추에이터 등 외부 장치 연결 가능
- HMI 전용 설계 → IoT, 스마트 제어, 교육용 UI 개발에 최적화

**⚙️ GPIO Pin Definition**

| Pin | Function       | Pin | Function               |
| --- | -------------- | --- | ---------------------- |
| P1  | GP0 / UART0 TX | P9  | GP19                   |
| P2  | GP1 / UART0 RX | P10 | GP20 / I2C0 SDA        |
| P3  | GP2 / I2C1 SDA | P11 | GP21 / I2C0 SCL        |
| P4  | GP3 / I2C1 SCL | P12 | GP26 / ADC1 / I2C1 SDA |
| P5  | GP4 / UART1 TX | P13 | GP27 / ADC0 / I2C1 SCL |
| P6  | GP5 / UART1 TX | P14 | GP28 / ADC2            |
| P7  | GP6 / I2C1 SDA | P15 | GND                    |
| P8  | GP7 / I2C1 SCL | P16 | VCC 3V3                |


**⚙️ 주요 사양 (Specifications)**
| 항목            | 내용                                |
| ------------- | --------------------------------- |
| **MCU**       | Raspberry Pi RP2040               |
| **디스플레이**     | 3.5인치 TFT LCD                     |
| **해상도**       | 480 × 320 pixels                  |
| **터치 방식**     | 정전식 터치스크린 (CTP)                   |
| **터치 컨트롤러**   | FT6236 (I2C 인터페이스)                |
| **플래시 메모리**   | 16MB (외부 Flash)                   |
| **USB**       | USB Type-C (프로그램 업로드 및 전원 공급)     |
| **I/O 인터페이스** | 20핀 확장헤더 (I2C, SPI, UART, GPIO 등) |
| **전원 입력**     | 5V (USB-C 또는 확장 커넥터)              |
| **크기**        | 85mm × 55mm                       |
| **사용가능 언어**   | C/C++, MicroPython                |
| **LVGL 지원**   | LVGL 8.x / 9.x 지원 (UI 개발용 라이브러리)  |


**터치스크린 프로토콜**
조도센서 값을 참조하는 예제
```
{ "c": "ti", "light": 120 }
```

## ✅ I2C 통신 프로그램
<details>
<summary>💻 C code 예제 - 마스터 프로그램 : 터치스크린 RP2040</summary>
    
```c
#include <Wire.h>

#define I2C_ADDR 0x08  // ESP32 슬레이브 주소
#define SDA_PIN 20     // I2C SDA 핀
#define SCL_PIN 21     // I2C SCL 핀

void setup() {
  Wire.setSDA(SDA_PIN);
  Wire.setSCL(SCL_PIN);
  Wire.begin();  // I2C 마스터 시작
  Serial.begin(115200);
  delay(1000);
  Serial.println("I2C Master 시작");
}

void sendCommand(const String& cmd) {
  Wire.beginTransmission(I2C_ADDR);
  Wire.write(cmd.c_str());
  Wire.endTransmission();
  Serial.println("전송: " + cmd);
}

void loop() {
  sendCommand("{\"cmd\":\"on\"}");
  delay(3000);

  sendCommand("{\"cmd\":\"off\"}");
  delay(3000);
}
```
</details>

<details>
<summary>💻 C code 예제 - 슬레이브 프로그램 : IoT PLC ESP32</summary>
    
```c
#include <Wire.h>

#define SLAVE_ADDR 0x08
#define SDA_PIN 16
#define SCL_PIN 17

String received = "";

void receiveEvent(int howMany) {
  char c;
  received = "";
  while (Wire.available()) {
    c = Wire.read();
    received += c;
  }
  Serial.println("수신된 데이터: " + received);
}

void setup() {
  Serial.begin(115200);
  delay(500);
  Serial.println("I2C Slave 시작");

  // 슬레이브 모드로 SDA/SCL 핀 지정
  Wire.begin(SLAVE_ADDR, SDA_PIN, SCL_PIN, 100000);
  Wire.onReceive(receiveEvent);
}

void loop() {
  // 슬레이브는 이벤트 기반이므로 loop는 비워둠
}
```
</details>

## ✅ LVGL, TFT_eSPI 설치
그래픽과 터치스크린을 구현하기 위한 구조를 설명하겠습니다.
- LVGL 에서는 그래픽에 필요한 설정을 해야 합니다.
- ILI9341 는 터치 스크린마다 사용하는 종류가 달라지므로 TFT_eSPI 에 정의를 해야 합니다.

📺 CrowPanel(RP2040) 기술 자료    
[참조기술문서 및 프로그램 다운로드](https://github.com/Elecrow-RD/CrowPanel-Pico-Display-Course-File)    
[회로도](https://github.com/user-attachments/files/20807927/CrowPanel_Pico_Display-3.5_V1.0-SCH.pdf)    
[유튜브 시청](https://www.youtube.com/watch?v=5lLdKOjR-Lo&list=PLwh4PlcPx2GdvAtPGuAf1ocWj1UyPWw3W)    
[Wiki](https://www.elecrow.com/wiki/CrowPanel_Pico_HMI_Display-3.5.html)    

아두이노에서 보드 설정할 때 사용하세요
```
Additional Boards Manager URLs
https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json
```

### 1. LVGL + TFT_eSPI + ILI9341 관계

**1) LVGL (Light and Versatile Graphics Library)**
- 오픈소스 GUI 라이브러리
- 버튼, 슬라이더, 차트, 탭, 텍스트 등 고급 UI 위젯 제공
- 하드웨어 독립적 → 직접 LCD 제어하지 않음
- 대신 “화면에 이 사각형을 그려라” 같은 **그리기 요청(draw call)**만 처리
- 실제 픽셀 출력은 **디스플레이 드라이버(TFT_eSPI)**에 맡김
- 👉 즉, UI 엔진 (사용자 인터페이스 제공)

**2) TFT_eSPI (디스플레이 드라이버)**
- ESP32 전용 고속 그래픽 라이브러리
- ILI9341, ST7735, ST7796 등 여러 디스플레이 칩 지원
- tft.drawPixel(x, y, color) 같은 저수준 API 제공
- SPI 통신을 최적화하여 빠른 화면 갱신 가능
- LVGL 같은 상위 라이브러리가 직접 ILI9341을 제어하지 않고 TFT_eSPI를 통해 제어
- 👉 즉, 소프트웨어 드라이버 (ESP32 ↔ ILI9341 연결)

**3) ILI9341 (디스플레이 컨트롤러)**
- 2.4~3.2인치 TFT LCD에서 많이 사용하는 디스플레이 드라이버 칩
- SPI 또는 병렬 인터페이스를 통해 픽셀 데이터를 수신
- 하드웨어적으로 LCD 패널의 픽셀 제어, 컬러 표현, 메모리 관리를 담당
- 예: 0,0 좌표에 빨간색 픽셀 그려라 → ILI9341이 LCD에 실제 반영
👉 즉, 하드웨어 칩 (디스플레이 컨트롤러)

**4) 관계 정리**
- LVGL → UI를 논리적으로 관리 (버튼, 차트, 텍스트 등)
- TFT_eSPI → LVGL이 요청한 그래픽을 픽셀 단위 명령으로 변환
- ILI9341 → 실제 TFT LCD 패널의 픽셀을 제어하여 화면에 출력

**5) 데이터 흐름**
```
LVGL (UI/위젯 관리)
   ↓
TFT_eSPI (ESP32용 디스플레이 드라이버)
   ↓
ILI9341 (하드웨어 컨트롤러)
   ↓
LCD 화면 출력
```

### 2. LVGL (Light and Versatile Graphics Library) 디스플레이 드라이버
적은 메모리에서도 부드럽고 직관적인 터치 UI를 구현할 수 있는 오픈소스 그래픽 라이브러리입니다    
다음 기술 사이트를 참조하세요   
[lvgl 기술사이트](https://github.com/lvgl/lvgl)    

### 📺 시연 영상 (IoT PLC HMI, LVGL 설치와 Hello 띄우기)
<a href="https://youtu.be/wRLgRPrYtvk">
  <img src="https://github.com/user-attachments/assets/6dea72b2-359e-486d-a27f-4110a77b258c" width="300" />
</a>

** 디스플레이 드라이버의 역할 **
LVGL 디스플레이 드라이버는 아래 두 가지를 담당합니다.
1) Flush callback (disp_drv.flush_cb)
- LVGL이 "이 영역을 빨간색으로 칠해라"라고 명령을 내리면,
- flush_cb 함수가 해당 픽셀 데이터를 실제 LCD 드라이버(ST7796, ILI9341 등) 로 전송합니다.
2) Buffer 관리 (lv_disp_draw_buf_t)
- LVGL은 화면 전체 크기만큼의 버퍼를 만들 필요가 없습니다.
- 보통 화면의 1/10~1/20 크기 버퍼만 두고, 해당 영역만 갱신합니다.
- 이 버퍼와 실제 하드웨어 전송을 연결하는 것이 디스플레이 드라이버의 역할입니다.

### 3. lvgl 설치 후 lv_conf.h 파일 만들기
lv_conf_template.h 를 필요한 항목을 수정해서 lv_conf.h 로 저장합니다.

**📌 요약 (수정해야 하는 항목만)**
1.#if 0 → #if 1
2. LV_COLOR_DEPTH = 16 (ILI9341)
3. LV_MEM_CUSTOM = 1 (malloc/free 사용)
4. LV_TICK_CUSTOM = 1, millis() 기반 설정
5. LV_DPI_DEF = 130 (3.5" 기준)
6. 폰트 설정: 필요 시 한글 폰트 추가
7. 위젯: 필요한 것만 1로 유지
8. 데모: 학습 시 1, 실제 코드에선 0


**1) 파일 활성화**
```
#if 0 /*Set it to "1" to enable content*/
```
👉 0 → 1 로 변경해야 LVGL이 이 설정을 읽습니다.
```
#if 1 /*Set it to "1" to enable content*/
```
**2) 색상 설정**
```
#define LV_COLOR_DEPTH 16
#define LV_COLOR_16_SWAP 0
```
ILI9341은 RGB565(16bit) 사용 → LV_COLOR_DEPTH 16 유지
색상이 뒤집혀 나오면 LV_COLOR_16_SWAP을 1로 변경

**3) 메모리 설정**
현재:
```
#define LV_MEM_CUSTOM 0
```
👉 ESP32는 malloc/free를 쓰는 게 일반적이므로 1로 변경
```
#define LV_MEM_CUSTOM 1
#define LV_MEM_CUSTOM_INCLUDE <stdlib.h>
#define LV_MEM_CUSTOM_ALLOC malloc
#define LV_MEM_CUSTOM_FREE free
```

**4) Tick 설정**
현재:
```
#define LV_TICK_CUSTOM 0
```
👉 Arduino 환경에서는 millis() 사용하도록 1로 변경
```
#define LV_TICK_CUSTOM 1
#define LV_TICK_CUSTOM_INCLUDE "Arduino.h"
#define LV_TICK_CUSTOM_SYS_TIME_EXPR (millis())
```

**5) DPI 설정**
```
#define LV_DPI_DEF 130
```
3.5" 320x480 해상도면 130 정도가 적당 (필요하면 100~140 사이 조정 가능)

**6) 폰트 설정 (한글 UI 필요 시)**
기본값:
```
#define LV_FONT_MONTSERRAT_14 1
#define LV_FONT_DEFAULT &lv_font_montserrat_14
```
👉 한글 표시하려면 커스텀 폰트 선언 추가
```
#define LV_FONT_CUSTOM_DECLARE LV_FONT_DECLARE(NotoSansKR_20)
```
(NotoSansKR_20.c 파일을 프로젝트에 포함해야 함)

**7) 위젯 사용 여부**
기본값은 대부분 1 → 그대로 둬도 무방
👉 메모리 절약하려면 안 쓰는 위젯을 0으로 꺼두기
예: 버튼, 레이블, 슬라이더만 쓸 경우
```
#define LV_USE_BTN     1
#define LV_USE_LABEL   1
#define LV_USE_SLIDER  1
```

**8) 데모/예제**
```
#define LV_BUILD_EXAMPLES 1
#define LV_USE_DEMO_WIDGETS 1
```
처음 테스트할 때는 1로 켜두면 좋음
실제 제품 코드에서는 불필요하면 0으로 꺼서 용량/속도 최적화

### 3. TFT_eSPI 디스플레이 드라이버 설치
CrowPanel 터치스크린은 RP2040 + ILI9488 (480x320) 디스플레이에 맞게 수정해야 합니다.

TFT_eSPI 라이브러리 설치     
![TFT_eSPI](https://github.com/user-attachments/assets/1423d2ef-853d-418b-8de9-22546349be82)    

[참조기술문서 및 프로그램 다운로드](https://github.com/Elecrow-RD/CrowPanel-Pico-Display-Course-File)    
여기서 다운로드 받은 파일중에 User_Setup.h 를 아두이노 라이브러리 디렉토리에 복사 한다.   
![TFT_eSPI-1](https://github.com/user-attachments/assets/0839872d-5459-4bf3-996e-cec4612d6493)
World
lvgl 라이브러리 설치     
그림과 같이 꼭 8.3.11 버젼을 설치해야 프로그램이 실행 됩니다.
위에서 다운로드 받은 파일중에 lv_conf.h 를 아두이노 라이브러리 디렉토리에 복사 한다.  
![lvgl](https://github.com/user-attachments/assets/070e58a6-ff88-46ab-a752-f6446f9c30a9)

1) 드라이버 선택
기본값:
```
#define ILI9341_DRIVER
```
수정 후 (CrowPanel 제공):
```
#define ILI9488_DRIVER
```
👉 CrowPanel 3.5"는 ILI9488 드라이버 기반이므로, 드라이버를 ILI9341 → ILI9488로 변경.

2) 디스플레이 해상도
기본값: 정의 없음 (ILI9341는 기본적으로 240x320)
수정 후:
```
#define TFT_WIDTH  320
#define TFT_HEIGHT 480
```
👉 CrowPanel 디스플레이 해상도(320×480)에 맞게 설정.

3) 백라이트 제어
기본값:
```
// #define TFT_BL   32
// #define TFT_BACKLIGHT_ON HIGH
```
수정 후:
```
#define TFT_BL 18
#define TFT_BACKLIGHT_ON HIGH
```
👉 CrowPanel 보드에서 TFT 백라이트 제어 핀이 GPIO18이므로 핀 지정 추가.

4) 핀 매핑 (SPI + 제어 핀)

기본값 (ESP8266/ESP32용 예시 핀):
```
#define TFT_MISO  PIN_D6
#define TFT_MOSI  PIN_D7
#define TFT_SCLK  PIN_D5
#define TFT_CS    PIN_D8
#define TFT_DC    PIN_D3
#define TFT_RST   PIN_D4
```

수정 후 (RP2040 CrowPanel 전용 핀맵):
```
#define TFT_MISO  12
#define TFT_MOSI  11
#define TFT_SCLK  10
#define TFT_CS     9
#define TFT_DC     8
#define TFT_RST   15
#define TOUCH_CS  16
```
👉 RP2040 Pico HMI 보드에 맞게 핀 번호를 10~16번 핀으로 새롭게 매핑.

5) SPI 포트 선택
기본값: 없음

수정 후:
```
#define TFT_SPI_PORT 1
```
👉 RP2040은 SPI0/SPI1을 선택할 수 있는데, CrowPanel 보드는 SPI1을 사용.

6) SPI 클럭 주파수
기본값:
```
#define SPI_FREQUENCY  27000000
```

수정 후:
```
#define SPI_FREQUENCY  80000000
```
👉 ILI9488 드라이버와 RP2040 성능에 맞춰 최대 80MHz로 변경.

7) 추가된 항목
터치스크린 CS 핀 정의:
```
#define TOUCH_CS 16
```
👉 XPT2046 터치 컨트롤러용 CS 핀을 별도로 지정.


기본적인 문자를 출력해 봅니다.
<details>
<summary>💻 아두이노 예제 - 문자 출력</summary>
    
```c
#include <lvgl.h>
#include <TFT_eSPI.h>

/* 디스플레이 해상도 */
static const uint16_t screenWidth  = 480;
static const uint16_t screenHeight = 320;

static lv_disp_draw_buf_t draw_buf;
static lv_color_t buf[screenWidth * screenHeight / 10];

TFT_eSPI tft = TFT_eSPI();  // TFT 객체

/* 화면 갱신 함수 */
void my_disp_flush(lv_disp_drv_t *disp, const lv_area_t *area, lv_color_t *color_p) {
  uint32_t w = area->x2 - area->x1 + 1;
  uint32_t h = area->y2 - area->y1 + 1;

  tft.startWrite();
  tft.setAddrWindow(area->x1, area->y1, w, h);
  tft.pushColors((uint16_t *)&color_p->full, w * h, true);
  tft.endWrite();

  lv_disp_flush_ready(disp);
}

void setup() {
  Serial.begin(115200);
  lv_init();        // LVGL 초기화
  tft.begin();      // TFT 초기화
  tft.setRotation(3);  // 필요에 따라 회전값 변경

  // 버퍼 초기화
  lv_disp_draw_buf_init(&draw_buf, buf, NULL, screenWidth * screenHeight / 10);

  // 디스플레이 드라이버 설정
  static lv_disp_drv_t disp_drv;
  lv_disp_drv_init(&disp_drv);
  disp_drv.hor_res = screenWidth;
  disp_drv.ver_res = screenHeight;
  disp_drv.flush_cb = my_disp_flush;
  disp_drv.draw_buf = &draw_buf;
  lv_disp_drv_register(&disp_drv);

  // 간단한 Hello World 라벨
  lv_obj_t *label = lv_label_create(lv_scr_act());
  lv_label_set_text(label, "Hello World");
  lv_obj_align(label, LV_ALIGN_CENTER, 0, 0);  // 가운데 정렬
}

void loop() {
  lv_timer_handler();  // LVGL 내부 작업 처리
  delay(5);
}
 ```
</details>

<details>
<summary>💻 아두이노 예제 - 버튼 출력 프로그램</summary>
    
```c
#include <lvgl.h>
#include <TFT_eSPI.h>

static const uint16_t screenWidth  = 480;
static const uint16_t screenHeight = 320;

static lv_disp_draw_buf_t draw_buf;
static lv_color_t buf[screenWidth * screenHeight / 10];

TFT_eSPI tft = TFT_eSPI();  // TFT 인스턴스

/* 화면 갱신 콜백 */
void my_disp_flush(lv_disp_drv_t *disp, const lv_area_t *area, lv_color_t *color_p) {
  uint32_t w = area->x2 - area->x1 + 1;
  uint32_t h = area->y2 - area->y1 + 1;

  tft.startWrite();
  tft.setAddrWindow(area->x1, area->y1, w, h);
  tft.pushColors((uint16_t *)&color_p->full, w * h, true);
  tft.endWrite();

  lv_disp_flush_ready(disp);
}

/* 버튼 클릭 이벤트 핸들러 */
void btn_event_cb(lv_event_t *e) {
  lv_obj_t *btn = lv_event_get_target(e);
  const char *txt = lv_label_get_text(lv_obj_get_child(btn, 0));
  Serial.print("Button pressed: ");
  Serial.println(txt);
}

void setup() {
  Serial.begin(115200);
  lv_init();
  tft.begin();
  tft.setRotation(3);  // 필요 시 회전 변경

  lv_disp_draw_buf_init(&draw_buf, buf, NULL, screenWidth * screenHeight / 10);

  static lv_disp_drv_t disp_drv;
  lv_disp_drv_init(&disp_drv);
  disp_drv.hor_res = screenWidth;
  disp_drv.ver_res = screenHeight;
  disp_drv.flush_cb = my_disp_flush;
  disp_drv.draw_buf = &draw_buf;
  lv_disp_drv_register(&disp_drv);

  // 버튼 생성 (세로 정렬)
  lv_obj_t *btn_up = lv_btn_create(lv_scr_act());
  lv_obj_align(btn_up, LV_ALIGN_CENTER, 0, -60);
  lv_obj_add_event_cb(btn_up, btn_event_cb, LV_EVENT_CLICKED, NULL);
  lv_obj_t *label_up = lv_label_create(btn_up);
  lv_label_set_text(label_up, "up");

  lv_obj_t *btn_stop = lv_btn_create(lv_scr_act());
  lv_obj_align(btn_stop, LV_ALIGN_CENTER, 0, 0);
  lv_obj_add_event_cb(btn_stop, btn_event_cb, LV_EVENT_CLICKED, NULL);
  lv_obj_t *label_stop = lv_label_create(btn_stop);
  lv_label_set_text(label_stop, "stop");

  lv_obj_t *btn_down = lv_btn_create(lv_scr_act());
  lv_obj_align(btn_down, LV_ALIGN_CENTER, 0, 60);
  lv_obj_add_event_cb(btn_down, btn_event_cb, LV_EVENT_CLICKED, NULL);
  lv_obj_t *label_down = lv_label_create(btn_down);
  lv_label_set_text(label_down, "down");
}

void loop() {
  lv_timer_handler();
  delay(5);
}
```
</details>


### 4.📘 LVGL 한글 폰트 적용 가이드

### 📺 시연 영상 (IoT PLC HMI, 한글 띄우기)
<a href="https://youtu.be/4TOUC_N_nwQ">
  <img src="https://github.com/user-attachments/assets/07f24466-0a23-4921-a16c-edf3d1b6fb63" width="300" />
</a>

한글 출력 예제 프로그램 
<details>
<summary>💻 아두이노 예제 - 한글문자 출력</summary>
    
```c
#include <lvgl.h>
#include <TFT_eSPI.h>
#include "NotoSansKR_20.h"  // 생성한 한글 포함 폰트

static const uint16_t screenWidth  = 480;
static const uint16_t screenHeight = 320;
static lv_disp_draw_buf_t draw_buf;
static lv_color_t buf[screenWidth * screenHeight / 10];

TFT_eSPI tft = TFT_eSPI();

void my_disp_flush(lv_disp_drv_t *disp, const lv_area_t *area, lv_color_t *color_p) {
  uint32_t w = area->x2 - area->x1 + 1;
  uint32_t h = area->y2 - area->y1 + 1;

  tft.startWrite();
  tft.setAddrWindow(area->x1, area->y1, w, h);
  tft.pushColors((uint16_t *)&color_p->full, w * h, true);
  tft.endWrite();

  lv_disp_flush_ready(disp);
}

void setup() {
  Serial.begin(115200);
  lv_init();
  tft.begin();
  tft.setRotation(3);

  lv_disp_draw_buf_init(&draw_buf, buf, NULL, screenWidth * screenHeight / 10);

  static lv_disp_drv_t disp_drv;
  lv_disp_drv_init(&disp_drv);
  disp_drv.hor_res = screenWidth;
  disp_drv.ver_res = screenHeight;
  disp_drv.flush_cb = my_disp_flush;
  disp_drv.draw_buf = &draw_buf;
  lv_disp_drv_register(&disp_drv);

  lv_obj_t* label = lv_label_create(lv_scr_act());
  lv_obj_set_style_text_font(label, &NotoSansKR_20, LV_PART_MAIN);  // 폰트 직접 지정
  lv_label_set_text(label, "Hello 안녕");  // 테스트
  lv_obj_align(label, LV_ALIGN_CENTER, 0, 0);

}

void loop() {
  lv_timer_handler();
  delay(5);
}
 ```
</details>


**1. Noto Sans KR 폰트 다운로드**

LVGL에서 한글 UI를 만들기 위해서는 한글을 지원하는 폰트를 준비해야 합니다.
- VGL에서 사용할 한글 폰트는 [Google Fonts – Noto Sans KR](https://fonts.google.com/noto/specimen/Noto+Sans+KR) 에서 다운로드할 수 있습니다.
- **"Get font"** 버튼을 눌러 전체 폰트 패밀리를 다운로드합니다.
- 압축을 해제하면 여러 굵기(Thin, Light, Regular, Medium, Bold 등)의 .ttf 파일이 들어있습니다.    
예) NotoSansKR-Regular.ttf

<img src="https://github.com/user-attachments/assets/c0ace5c3-56ef-4a96-b16c-aef7819f74fe" alt="Google Fonts" width="400">

**2. LVGL 폰트 컨버터 사용하기**

- LVGL은 .ttf 폰트를 그대로 사용할 수 없으므로, LVGL 전용 C 소스 파일로 변환해야 합니다.
- [LVGL Font Converter](https://lvgl.io/tools/fontconverter)   웹사이트에 접속합니다.

- 다음과 같이 설정합니다:
```
Name : 사용할 이름 입력 → NotoSansKR_20 생성
Font size: 20 입력
Bpp: 4 (일반적으로 4bpp 권장)
Output format: C array 선택
Browse: NotoSansKR-Regular.ttf 선택
Range: 빈칸
Symbols: 사용할 글짜들 입력
Submit 버튼을 누르면 NotoSansKR_20.c 파일이 생성됩니다.
```

폰트다운로드 사이트 : https://fonts.google.com/noto/specimen/Noto+Sans+KR    

<p align="left">
    <img src="https://github.com/user-attachments/assets/ebed64a9-ecf0-4fb0-93fb-a0599bd62cf4" alt="Google Fonts" width="600">
</p>

Symbols
```
아이티알 제어판 설정 사용자메뉴얼 온도 습도 와이파이 이름 비밀번호 이메일 사용법 연결과 블루투스 펌웨어설치 다음 이전 조도 주소  기기  로그인 타이머 입력 트리거 센서 트리거 홈 한글폰트 설치 모터제어 크라우드 입력 동영상시청 다음 정보를 입력하세요 안드로이드 어플 제품사용설명서 보기 닫기 ° 0123456789 ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefgh기ijklmnopqrstuvwxyz ~!@#$%^&*()_+-=[]{}|;':",./<>? 
```

- 생성된 "NotoSansKR_20.c" 는 소스코드와 같은 디렉토리에 위치 합니다.
- chatgpt 에 의뢰하면 NotoSansKR_20.h 파일을 작성해 줍니다.
  
<details>
<summary>💻 C code - NotoSansKR_20.h </summary>

```c
#ifndef NOTOSANSKR_20_H
#define NOTOSANSKR_20_H

#include "lvgl.h"

#ifdef __cplusplus
extern "C" {
#endif

extern const lv_font_t NotoSansKR_20;

#ifdef __cplusplus
} /* extern "C" */
#endif

#endif
```
</details>

- NotoSansKR_20.c 파일 중 다음 두곳을 수정 합니다. 두 곳을 찿아서 아래와 같이 수정 하세요
```
/*
#ifdef __has_include
    #if __has_include("lvgl.h")
        #ifndef LV_LVGL_H_INCLUDE_SIMPLE
            #define LV_LVGL_H_INCLUDE_SIMPLE
        #endif
    #endif
#endif

#ifdef LV_LVGL_H_INCLUDE_SIMPLE
    #include "lvgl.h"
#else
    #include "lvgl/lvgl.h"
#endif
*/
#include "lvgl.h"
```

```
    //.static_bitmap = 0,
    .dsc = &font_dsc,          /*The custom font data. Will be accessed by `get_glyph_bitmap/dsc` */
```

디렉토리에 생성한 파일입니다.     

<img src="https://github.com/user-attachments/assets/c5f29d31-2507-4ac5-ac1b-34944f8d295f" width="600" >       
<br>    

```
버튼을 두개 만들어줘 라벨 "1번켜" 버튼을 누르면 
{ "c": "so", "m": "D4:8C:49:50:46:F4", "n": 1, "v": 1 }
을 시리얼 통신으로 보내고 "1번꺼" 버튼을 누르면
{ "c": "so", "m": "D4:8C:49:50:46:F4", "n": 1, "v": 0 } 을 보내줘
```
---

<br>     
<details>
    <summary>💻 C code 예제</summary>

```c
// ✅ 여기에 C 코드 작성

```
</details>


✅ 과목 문단명
▶️[유튜브] 유튜브
📌🔰 개요 및 준비
🎯 학습 목표 및 기대 효과
📋 요약 / 정리 / 확장 학습
⚙️ 개발 환경 및 준비물
🚀 실행, 런칭
🟢	시작 신호 (녹색: 실행 의미)
📦  필요 라이브러리 설치 방법 
💻 소프트웨어 
🔍	결과 확인, 테스트
🔗 링크
🌐 확장 기능 (통신)
📚 참고 자료 및 링크
💡	팁 / 확장 아이디어
🧠 학생 과제 또는 연습 문제
🤖	로봇 프로젝트 / 자율 동작 시스템

