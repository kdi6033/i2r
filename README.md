# i2r
아이티알에서 제작한 기기 관련 정보를 제공합니다.    
Data Scientist, AI Scientist 를 희망하시는 분들에게 도움을 드리려 합니다.    
<br>
Node-RED를 활용하여 로컬 컴퓨터, AWS 클라우드, 스마트폰 애플리케이션에서 i2r-02, i2r-03, i2r-04 기기의 모니터링 및 제어를 가능하게 합니다.

### 주요 기능   
- Node-RED 기반 모니터링 및 제어: 다양한 환경에서 i2r 기기를 실시간으로 모니터링하고 제어할 수 있습니다.    
- 로컬 컴퓨터: 로컬 네트워크를 통해 기기를 모니터링하고 제어할 수 있습니다.    
- AWS 클라우드: 클라우드 기반으로 원격지에서도 기기의 상태를 모니터링하고 제어가 가능합니다.     
- 스마트폰 애플리케이션: 모바일 앱을 통해 언제 어디서나 기기의 상태를 확인하고 제어할 수 있습니다.

### 기기 정보   
링크를 누르면 기기 설명 사이트로 이동 합니다.    
- [i2r-01](https://github.com/kdi6033/i2r-01/tree/main/0%20Android%20App%20Program/server-i2r-01): 블루투스, mqtt, RS485, RS232 인터넷통신을 서로 연결합니다.    
- [i2r-02](https://github.com/kdi6033/i2r-02/tree/main/0%20Source-Program-IoT/board-i2r-02): 입출력 각4채널의 입출력 제어하는 IoT PLC     
- [i2r-03](https://github.com/kdi6033/i2r-03/tree/main/0%20Source-Program-IoT/board-i2r-03) : 입출력 각4채널의 입출력 제어하는 IoT PLC, 온습도 센서     
- [i2r-04](https://github.com/kdi6033/i2r-04/tree/main/0%20Source-Program-IoT/board-i2r-04) : 입출력 각2채널의 입출력 제어하는 IoT PLC, 2개의 아나로그 입력    

### 사용 방법    
- 스마트폰 또는 탭으로 제어 : 어플설치    
- PC IoT 서버  
- 아마존 크라우드 AWS IoT 서버
- 자세한 사용법과 서버 구축의 세부내용은 아래를 참조하세요

### 스마트폰 또는 탭으로 제어
다음 QR 링크를 눌러 어플을 설치하고 유튜브의 사용법을 따라하세요.    
QR CODE 연결하거나 그림을 누르세요 <br>   

<a href="https://play.google.com/store/apps/details?id=io.ionic.i2rReactIoT">
    <img src="https://github.com/user-attachments/assets/6fcca369-0c4a-4d6f-ad9b-642c6d29bdac" alt="다운로드 QR코드" width="200">
</a>  
<a href="https://youtu.be/bLvpejVkJcQ">
    <img src="https://github.com/user-attachments/assets/9523bd58-8626-4707-af54-0d5fd12a8c82" alt="IoT PLC App 통신 설정" width="400">
</a>
<a href="https://youtu.be/-O2wFqJ9-Qw">
    <img src="https://github.com/user-attachments/assets/4b88edef-1c0a-4c19-bd82-464cf4cacede" alt="입출력, 온도, 습도 동작설정" width="400">
</a>    
    
구매하신 보드에는 다음 프로그램이 설치되어 있습습니다. 어플과 연동하는 아두이노 프로그램으로 응용해서 사용하실 분들은 이 프로그램을 활용하세요. <br>

[i2r-02 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-02/releases/tag/board-i2r-02-v1.0)    
[i2r-03 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-03/releases/tag/board-i2r-03-v1.0)    
[i2r-04 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-04/releases/tag/board-i2r-04-v1.0)    


# 프로토콜
## 2025년7월15일 chatgpt에 적합한 프로토콜을 새로 작성하고 있습니다. 이전에 구매한 보드는 7월30일 이후 새로운 펌웨어를 다운 받아 주세요
i2r 보드의 mqtt 통신에서는 아래와 같이 구성되어 email을 저장하면 다음 토픽으로 자신에 해당되는 데이터를 통신 할 수 있습니다.     
intopic : i2r/email주소/in    
outtopic=i2r/email주소/out  

# 📡 i2r MQTT 통신 명령어 사전 (축약형)

이 문서는 i2r IoT 보드와 클라이언트 간 MQTT 통신 시 사용하는 JSON 기반 명령어 프로토콜을 설명합니다.  
모든 메시지는 경량화를 위해 **축약된 필드명**과 **축약된 명령어 코드(`c`)**를 사용합니다.

---

## ✅ 기본 MQTT 토픽 구조

- **intopic**  : `i2r/{email}/in`  
- **outtopic** : `i2r/{email}/out`

> `email`은 각 사용자의 고유 ID 역할을 합니다.

---

## ✅ JSON 메시지 필드명 요약

| 전체 명칭        | 축약 코드            | 설명                                                                           |
| --------------- | ---------------------- | ---------------------------------------------------------------------------- |
| email           | `e`                    | email                                                                        |
| command         | `c`                    | 명령 종류 (예: `df`, `so`, `gs`, `sch`, `bs` 등 축약어 사용)                   |
| mac             | `m`                    | 대상 장치의 MAC 주소 (예: `"A0:B7:65:CD:4D:34"`)                              |
| portNo          | `n`                    | 출력 핀 번호 (0부터 시작)                                                     |
| value           | `v`                    | 출력 값: `true` 또는 `false`, 혹은 수치 값                                    |
| operation       | `o`                    | 작업 종류: `"save"`, `"list"`, `"delete"`, `"deleteAll"`, `"cali"`, `"insert"` 등 |
| portState       | `ps`                   | 제어할 출력 포트 정보 배열 (예: `[{"m": "...", "n": 0, "v": true}]`)               |
| type            | `t`                    | `gs`: 보드 종류 (예: `3` = i2r-03)<br>`bs`: 센서 타입 (`temp`, `humi`, `light`)    |
| in              | `in`                   | 입력 상태 배열 (예: `[0,1,0,0]`)                                                  |
| out             | `out`                  | 출력 상태 배열 (예: `[1,0,0,0]`)                                                  |
| pinIndex        | `pi`                   | 출력 핀 인덱스 (0\~3)                                                             |
| startMinutes (분) | `start`                | 시작 시간 (예: 오전 9시 30분 = `570`)                                             |
| endMinutes (분)   | `end`                  | 종료 시간 (예: 오전 10시 = `600`)                                                 |
| repeatMode      | `rm`                   | 반복 주기: `0` = 매일, `1` = 매주                                                  |
| dayOfWeek         | `dw`                   | 반복 요일: 숫자(0=일 \~ 6=토), 또는 배열 `[1,3,5]` (월, 수, 금)                     |
| sensorHighValue   | `h`                    | 센서 동작의 상한 값 (예: 온도 28도)                                                |
| sensorLowValue    | `l`                   | 센서 동작의 하한 값 (예: 온도 26도)                                                 |
| temperature      | `temp`                 | 센서 현재 온도 값 (예: `27.8`)                                                     |
| humidity         | `humi`                 | 센서 현재 습도 값 (예: `55`)                                                       |
| light            | `light`                | 센서 조도 값 (예: `120`)                                                          |
| adc              | `adc`                  | analog to digital, 센서 ad converter (예: `3.4`)                                 |
| bat              | `bat`                  | battaery output, 센서 보드에 들어오는 밭데리 전압 (예: `3.4`)                      |
| calibration      | `cali`                 | 	센서값 보정 (예: 28.1)                                                         |
| pageNo           | `pn`                   | 	list 에서 데이터의 번호                                                        |


---

## ✅ 명령어 축약 코드 목록

| 전체 명칭           | 축약 코드 (`c`)   | 설명 |
|---------------------|------------------|------|
| `bindIO`           | `bio`            | 입력 상태에 따라 출력 연동 설정  |
| `bindSensor`       | `bs`             | 센서 조건에 따라 출력 제어 (온도, 습도, 조도 등) |
| `downloadFirmware` | `df`             | 보드에 펌웨어를 다운로드 |
| `getStatus`        | `gs`             | 보드 상태 요청 (온도, 습도, in/out 등)   |
| `schedule`          | `sch`            | 시간 기반 출력 동작 스케줄 설정  | 
| `setInfo`          | `si`             | Wi-Fi, MQTT 브로커 등 설정 정보 전송 |
| `setOutput`        | `so`             | 핀출력을 표시 (1 = ON, 0 = OFF) |
| `slotIndex`        | `sI`             | 스케줄 작업시 슬롯 (번호)인덱스 지정 |
| `touchInput`       | `ti`            | Touch Panel(RP2040 등) 전달 |

---
## ✅ 예제 및 상세 설명 

| `command` (`c`) | 예제 및 상세 설명 |
|----------------|-------------------|
| **`download_firmware`** (`df`) | ```{ "c": "df", "m": "D8:13:2A:C3:E7:68", "fileName": "i2r-03.ino.bin" }``` <br>지정한 MAC 주소를 가진 보드에 인터넷을 통해 펌웨어를 다운로드합니다. `.ino.bin` 또는 `.bin` 파일이 대상이며, OTA 업데이트를 통해 자동 적용됩니다. |
| **`set_info`** (`si`) | ```{ "c": "si", "ssid": "i2r_wifi", "password": "00000000", "email": "user@example.com", "mqttBroker": "mqtt.i2r.link" }``` <br> 보드가 Wi-Fi 및 MQTT 브로커에 연결할 수 있도록 설정 정보를 저장합니다. 이후 재시작 시 자동 연결됩니다. |
| **`set_output`** (`so`) | ```{ "c": "so", "m": "A0:B7:65:CD:4D:34", "n": 1, "v": 1 }``` <br> 지정 보드의 `n`번 출력 핀을 제어합니다. `v: 1`은 ON, `v: 0`은 OFF입니다. 릴레이, 모터, LED 등에 사용됩니다. |
| **`get_status`** (`gs`) | ```{ "c": "gs", "m": "EC:64:C9:43:E8:B8" }```<br>지정 보드의 상태를 요청합니다. 응답으로 온도, 습도, 입력포트(`in`), 출력포트(`out`) 정보가 포함됩니다.<br>응답 예시:<br>`{"t":3,"email":"kdi6033@gmail.com","m":"EC:64:C9:43:E8:B8","temp":28.4,"humi":38,"in":[0,0,0,0],"out":[0,0,0,0]}` |
| **`schedule_output`** (`sch`) | ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "insert", "n": 0, "start": 540, "end": 620, "rm": 0, "dw": [1,2,3,4,5] }```<br>출력핀 0번을 월~금 오전 9:00~10:20까지 자동으로 ON 되도록 예약합니다. `rm=0`은 매일 반복, `dw=[1~5]`는 월~금을 의미합니다. <br> ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "insert", "n": 0, "start": 595, "end": 597, "rm": 1, "dw": [1] }``` <br> 오전 9시 55분(9*60+55=595)부터 9시 57분(597)까지 매주 월요일(dw: [1])에 0번 출력 포트를 ON 하도록 예약합니다. rm: 1은 반복 모드로 "매주"를 의미합니다.<br> ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "list", "n": 0 }``` <br> 0번 포트에 저장된 스케줄 예약 리스트를 보여줍니다.<br> ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "delete", "n": 0, "slot": 0 }``` <br> 0번 출력 포트에 등록된 예약 중 첫 번째(slotIndex: 0) 항목을 삭제합니다.<br> ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "deleteAll", "n": 0 }``` <br> 0번 포트에 저장된 모든 예약 스케줄을 삭제합니다. |
| **`bind_input_output`** (`bio`) | ```{ "c": "bio", "o": "save", "m": "A0:B7:65:CD:4D:34", "n": 0, "ps": [ { "m": "D4:8A:FC:B5:30:10", "n": 1, "v": 1 }, { "m": "B0:A7:32:1D:B3:B8", "n": 1, "v": 0 } ] }```<br>입력 포트(n)가 ON이 되면 지정된 출력 포트를 ON, OFF가 되면 다른 출력 포트를 OFF합니다. 입력-출력 간 연동 제어를 구성할 수 있습니다.<br> ```{"c": "bio","o": "save","m": "A0:B7:65:CD:4D:34","n": 0,"ps": [{ "m": "D4:8A:FC:B5:30:10", "n": 1, "v": false },{ "m": "B0:A7:32:1D:B3:B8", "n": 1, "v": true }]}```<br> "A0:B7:65:CD:4D:34" 보드의 0번 입력 핀이 ON 되면 "B0:A7:32:1D:B3:B8"의 1번 포트가 ON, OFF가 되면 "D4:8A:FC:B5:30:10"의 1번 포트가 OFF 됩니다. <br> ```{"c": "bio","o": "list","m": "A0:B7:65:CD:4D:34","n": 0}``` <br> "A0:B7:65:CD:4D:34" 보드의 0번 입력 핀에 설정된 출력 연동 목록을 요청합니다. <br> 응답메세지 예시 ```{"c": "bio","m": "A0:B7:65:CD:4D:34","n": 0,"ps": [{ "m": "D4:8A:FC:B5:30:10", "n": 1, "v": 0 },{ "m": "B0:A7:32:1D:B3:B8", "n": 1, "v": 1 }]}``` <br>해당 입력 핀에 연결된 출력 포트 정보가 응답으로 전송됩니다. <br> ```{"c": "bio","o": "delete","m": "A0:B7:65:CD:4D:34","n": 0}``` <br> 입력 핀 0번에 저장된 모든 출력 연동 설정을 삭제합니다.|
| **`bind_sensor`** (`bs`) | ```{ "c": "bs", "m": "A0:B7:65:CD:4D:34", "o": "save", "t": "temp", "h": 28, "l": 27, "ps": [ { "m": "D4:8A:FC:B5:30:10", "n": 0, "v": 1 }, { "m": "D4:8A:FC:B5:30:10", "n": 0, "v": 0 } ] }```<br>온도 "A0:B7:65:CD:4D:34" 보드의 온도센서 값이 28도 초과 시 "D4:8A:FC:B5:30:10" 보드의 0번 포트 ON, 27도 이하 시 "D4:8A:FC:B5:30:10" 보드의 0번 포트가 OFF하는 자동 제어. `t`는 센서 종류(`temp`, `humi`, `light`)를 의미합니다. |
| **`touch_panel_input`** (`ti`) | ```{ "c": "ti", "light": 120 }```<br>RP2040 등의 외부 터치패널에서 측정한 조도 값을 IoT 보드에 전달하여 조건 제어에 활용할 수 있습니다. |

----------------

 # 이전 프로토콜 
 ## 앞에 정의된 프로토콜로 프로그램 수정 중 입니다.
|order|  기능  |설명 및 프로토콜|
|--|-------|---|
|0|펌웨어 다운로드|인터넷에서 통신으로 펌웨어를 보드로 내려 받는다<br> {"mac":"D8:13:2A:C3:E7:68","order":0,"fileName":"i2r-03.ino.bin"}|
|1|정보입력|와이파이 및 통신에 필요한 정보를 보내 보드에 기록하여 기기는 여기 정보로 통신을 연결한다.<br> {"order":1,'ssid':'***','password'='***', 'email':'***', 'mqttBroker':'ai.doowon.ac.kr'}|
|2|핀출력 `so` |IoT PLC의 핀번호(0,1,2,3 4개)와 true/false를 보내면 릴레이가 동작한다. <br>{"mac":"A0:B7:65:CD:4D:34","order":2,"no":1,"value":true}<blockquote>맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 1번핀 릴레이를 on 시킨다.</blockquote> |
|3|상태전송요청|보드의 현재 상태를 mqtt로 보낸다.<br>요청 : {"mac":"EC:64:C9:43:E8:B8",'order':3}<blockquote> 맥어드레스가 "EC:64:C9:43:E8:B8"인 기기의 현재 상태를 보내온다. </blockquote> 응답예시  <br>{"type":3,"email":"kdi6033@gmail.com","mac":"EC:64:C9:43:E8:B8","temp":28.4,"humi":38,"in":[0,0,0,0],"out":[0,0,0,0]}|
|4|동작시간설정 | 보드의 동작시간을 일일 일주일 단위로 설정한다. <br>{'order':4,"oper":operation,"pI":pinIndex,"sH":시작시간,"sM":시작분,"eH":종료시간,"eM":종료분, "rM":repeatMode,"dW":dayOfWeek}<br>pI:pinIndex 출력핀 번호 0번부터 시작한다.<br> operation : "insert":설정을 추가한다. "delete":한개의 설정을 삭제한다. "deleteAll":모두 삭제한다.<br>repeatMode : "daily"="d", "weekly"="w"<br>dayOfWeek : 일주일 중 요일설정 일=0,월=1,화=2,수=3,목=4,금=5,토=6<br>예제<br>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"insert","pI":0,"sH":9,"sM":55,"eH":9,"eM":57,"rM":"d","dW":0}<blockquote>오전9시55분부터 9시57분까지 매일 동작한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"insert","pI":0,"sH":9,"sM":55,"eH":9,"eM":57,"rM":"w","dW":1}<blockquote>오전9시55분부터 9시57분까지 매주 월요일에 동작한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"list","pI":0}<blockquote>0번 포트에 저장 리스트를 보여준다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"delete","pI":0,"slotIndex":0}<blockquote>0번핀의 0번째 리스트를 삭제한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"deleteAll","pI":0}<blockquote>0번 핀의 저장된 값을 모두 지운다.</blockquote>|
|5|입력핀에 출력설정 `bio`|입력핀의 on off 동작에 따라 출력을 연결한다. 통신에 연결되어 있는 모드 기기의 출력포트를 연결 할 수 있다.<br>예제<br> operation : "save":출력설정을 저장한다. "list":설정된 값의 리스트를 요구한다. "delete":선택한 설정 값을 지운다. <br>{"order":5,"oper":"save","mac":"A0:B7:65:CD:4D:34","portNo":0,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":1,"value":false},{"mac":"B0:A7:32:1D:B3:B8","port":1,"value":true}]} <blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀의 동작 저장 on 될때 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀이 on(true) 된다. off 될때 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀이 off(false) 된다. </blockquote>{"order":5,"mac":"A0:B7:65:CD:4D:34","oper":"list","portNo":0} <blockquote>맥어드레스 "A0:B7:65:CD:4D:34" 기기 0번 핀의 설정 값을 요청한다.</blockquote>응답 메세지 예시 <br>{"order":6,"mac":"A0:B7:65:CD:4D:34","portNo":0,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":1,"value":false},{"mac":"B0:A7:32:1D:B3:B8","port":1,"value":true}]}<br>{"order":5,"mac":"A0:B7:65:CD:4D:34","oper":"delete","portNo":0}<blockquote>0번 핀의 저장된 값을 모두 지운다.</blockquote>|
|6|온도변화에 출력설정|예제<br>{"order":6,"oper":"save","mac":"A0:B7:65:CD:4D:34","tempHigh":28,"tempLow":27,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":0,"value":false},{"mac":"D4:8A:FC:B5:30:10","port":0,"value":true}]} <blockquote>온도가 28도를 넘어설 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 on 되고 온도가 27도에서 떨어질 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 off 된다</blockquote>{"order":6,"mac":"A0:B7:65:CD:4D:34","oper":"list"}<blockquote>맥어드레스 "A0:B7:65:CD:4D:34" 기기 온도설정 리스트를 요청한다.</blockquote>    {"order":6,"oper":"cali","mac":"A0:B7:65:CD:4D:34","calTemp":28.1}<blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 현재 온도를 28.1로 세팅한다.</blockquote>{"order":6,"mac":"A0:B7:65:CD:4D:34","oper":"delete"}<blockquote>맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 온도에 따른 동작 연결을 삭제한다.</blockquote>|
|7|습도변화에 출력설정|예제<br>{"order":7,"oper":"save","mac":"A0:B7:65:CD:4D:34","humiHigh":50,"humiLow":49,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":0,"value":false},{"mac":"D4:8A:FC:B5:30:10","port":0,"value":true}]}<blockquote> 습도가 50을 넘어설 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 on 되고 습도가 49로 떨어질 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 off 된다</blockquote>{"order":7,"mac":"A0:B7:65:CD:4D:34","oper":"list"}<blockquote>맥어드레스 "A0:B7:65:CD:4D:34" 기기 온도설정 리스트를 요청한다.</blockquote> {"order":7,"oper":"cali","mac":"A0:B7:65:CD:4D:34","calHumi":48}<br><blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 현재 습도를 48로 세팅한다.</blockquote>{"order":7,"mac":"A0:B7:65:CD:4D:34","oper":"delete"}<blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 습도에 따른 동작 연결을 삭제한다.</blockquote>|
|8| 센서변화의 출력설정 | order 6,7 을 포함한 모든 센서의 동작을 설정 합니다. 프로토콜은 온도 습도와 동일 합니다. |
|9|센서 액튜에이터 참조값| 터치패널이 설치되어 별도의 cpu에서 센서 계측값을 메인보드로 보내면 이 값을 기록하고 크라우드 서버로 보낸자.     <br> 예제 터치스크린 rp2040에서 IoT PLC로 조도센서 값을 보낸다.     <br>{"order":8, "light":120} |

      

위에 기술한 프로토콜을 node red 에서 실행 한 것입니다. 폰의 어플에서 구현한 것을 node red로 프로그램해서 사용할수 있습니다.
<a href="https://youtu.be/ufBprCdABSk">
    <img src="https://github.com/user-attachments/assets/01886cc0-2b59-4e1c-962b-f5b7cc751a45" alt="i2r 프로토콜" width="800">
</a>

[프로토콜 node red 소스프로그램](https://github.com/kdi6033/i2r/blob/main/txt/protocol%20node%20red%20example.json)

<a href="https://youtu.be/ufBprCdABSk">
    <img src="https://github.com/user-attachments/assets/fd75d17a-1c77-46e2-872d-b610dede45c3" alt="protocol" width="400">
</a>

### 아두이노 프로그램 설정    
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

# Node-RED 서버 구축
## PC IoT 서버 (Node-RED)    
- PC에서 node red 와 mongoDB를 설치하여 인터넷 상에서 제어한다.
- 어플에서 IoT-PLC를 와이파이에 접속만 시키면 데이터베이스에 자동 저장되고 제어판넬이 자동으로 생성되어서 모니터링/제어를 할 수 있다.

<a href="https://youtu.be/nL3qdDtZC98">
    <img src="https://github.com/user-attachments/assets/1015639c-ed79-44fb-a690-3545664a31e7" alt="node red 설치 윈도우용 " width="400">
</a>
<a href="https://youtu.be/5spmnQX0IjM">
    <img src="https://github.com/user-attachments/assets/9da548f6-9872-48d7-846c-e790586c5511" alt="mongodb, compass 윈도우용 설치하기 " width="400">
</a>    


어플 아두이노 소스 프로그램과 동일 합니다.<br>

[i2r-02 보드 아두이노 프로그램](https://github.com/kdi6033/i2r-02/blob/main/0%20Source-Program-IoT/board-i2r-02-local.ino)  
[i2r-03 보드 아두이노 프로그램](https://github.com/kdi6033/i2r-03/blob/main/0%20Source-Program-IoT/board-i2r-03-local.ino)  
[i2r-04 보드 아두이노 프로그램](https://github.com/kdi6033/i2r-04/blob/main/0%20Source-Program-IoT/board-i2r-04-local.ino)  

[윈도우 PC용 NodeRED 소스프로그램](https://github.com/kdi6033/i2r/blob/main/0%20Source-Program-IOT/nodered-local.json)    
![nodered-flow](https://github.com/user-attachments/assets/69855573-c93a-4180-be8a-5cd442f85d2c)   
 
mongoDB에 데이터가 자동으로 저장 된 모습    
<img src="https://github.com/user-attachments/assets/1c8ee718-8561-4eeb-bdd4-366b209b9fc6" width="400">    <br>
- node red 에서 자동 생성된 제어판넬    
<img src="https://github.com/user-attachments/assets/91897ea9-785e-488f-9f3e-241a049b78f3" width="30%"><br>
node red flow    

## 아마존 크라우드 AWS IoT 서버  (Node-RED)     
<a href="https://youtu.be/n1MRXSVtbBI">
    <img src="https://github.com/user-attachments/assets/8a2ccaba-8b4a-44a1-8ac9-556d96cbd0ad" alt="AWS Instal EC2 Ubuntu Server 22.04" width="400">
</a>
<a href="https://youtu.be/5ojpKiQ00qk">
    <img src="https://github.com/user-attachments/assets/10dfdc4e-d581-4cfe-92f1-8a700069e1f4" alt="AWS IOT Core Mqtt" width="400">
</a>

<a href="https://youtu.be/mruzmon95BE">
    <img src="https://github.com/user-attachments/assets/bb05f92c-e8d3-4ca2-a0c4-7a97adb5c08f" alt="AWS IOT Core Mqtt" width="400">
</a>
<a href="https://youtu.be/WJrOxAN7ZH0">
    <img src="https://github.com/user-attachments/assets/69d1455b-cbb1-4f09-b0c2-356d4bbcc515" alt="AWS IOT Core Mqtt" width="400">
</a>

<a href="https://youtu.be/vLT3sr_xAFE">
    <img src="https://github.com/user-attachments/assets/7c56667a-631c-4bc4-a681-a7a4a49cb729" alt="AWS IoT server" width="400">
</a>
<a href="https://youtu.be/Q7IL_ERRIwI">
    <img src="https://github.com/user-attachments/assets/5f8fae58-d80b-4d26-b863-c20c24a20021" alt="AWS IoT 보안 server" width="400">
</a>

<br>

[i2r-02 보드 AWS 아두이노 프로그램](https://github.com/kdi6033/i2r-02/tree/main/0%20Source-Program-IoT/board-i2r-02-aws)  
[i2r-03 보드 AWS 아두이노 프로그램](https://github.com/kdi6033/i2r-03/tree/main/0%20Source-Program-IoT/board-i2r-03-aws)  
[i2r-04 보드 AWS 아두이노 프로그램](https://github.com/kdi6033/i2r-04/tree/main/0%20Source-Program-IoT/board-i2r-04-aws)  

[Node-RED 설치순서](https://github.com/kdi6033/i2r/blob/main/txt/aws%20node%20red%20install.txt)    

[mongoDB 설치순서](https://github.com/kdi6033/i2r/blob/main/txt/aws%20mongoDB%20install)    


[아마존 크라우드 AWS NodeRED 소스프로그램](https://github.com/kdi6033/i2r/blob/main/0%20Source-Program-IOT/nodered-aws.json)

# IoT PLC 터치스크린
ESP32 IoT PLC와 CrowPanel(RP2040)을 I2C로 연결하여,
CrowPanel은 사용자 인터페이스와 I2C 센서 계측을 담당하고,
ESP32는 릴레이 제어 및 클라우드(MQTT) 연동을 담당하는 IoT 제어 시스템입니다.    
![ChatGPT Image 2025년 6월 19일 오전 10_09_21](https://github.com/user-attachments/assets/06412467-1643-4176-95d3-0994f6a94572)

        
시스템 구성
| 항목           | 설명                                      |
| ------------ | --------------------------------------- |
| **I2C 마스터**  | CrowPanel (RP2040)                      |
| **I2C 슬레이브** | ESP32                                   |
| **센서 계측**    | CrowPanel에서 직접 I2C로 계측 (조도, 온습도 등)      |
| **UI 이벤트**   | 터치 버튼 → ESP32에 명령 전송 (`{"cmd":"on"}` 등) |
| **액츄에이터 제어** | ESP32에서 명령 수신 후 릴레이/모터 제어               |
| **클라우드 연동**  | ESP32 → MQTT 전송 (선택적 기능)                |

연결 핀 구성 (예시)
| 장치                 | 기능  | 핀       |
| ------------------ | --- | ------- |
| CrowPanel (RP2040) | SDA | GPIO 20 |
|                    | SCL | GPIO 21 |
| ESP32 (i2r-04)     | SDA | GPIO 16 |
|                    | SCL | GPIO 17 |


## CrowPanel(RP2040) 3.5" 터치스크린

주요 사양 (Specifications)
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


GPIO Pin Definition

| 핀 번호    | 기능                     |
| ------- | ---------------------- |
| **P1**  | GP0 / UART0 TX         |
| **P2**  | GP1 / UART0 RX         |
| **P3**  | GP2 / I2C1 SDA         |
| **P4**  | GP3 / I2C1 SCL         |
| **P5**  | GP4 / UART1 TX         |
| **P6**  | GP5 / UART1 RX         |
| **P7**  | GP6 / I2C1 SDA         |
| **P8**  | GP7 / I2C1 SCL         |
| **P9**  | GP19                   |
| **P10** | GP20 / I2C0 SDA        |
| **P11** | GP21 / I2C0 SCL        |
| **P12** | GP26 / ADC1 / I2C1 SDA |
| **P13** | GP27 / ADC0 / I2C1 SCL |
| **P14** | GP28 / ADC2            |
| **P15** | GND (Ground)           |
| **P16** | VCC (3.3V 출력)          |

📺 기술 자료    
[참조기술문서 및 프로그램 다운로드](https://github.com/Elecrow-RD/CrowPanel-Pico-Display-Course-File)    
[회로도](https://github.com/user-attachments/files/20807927/CrowPanel_Pico_Display-3.5_V1.0-SCH.pdf)    
[유튜브 시](https://www.youtube.com/watch?v=5lLdKOjR-Lo&list=PLwh4PlcPx2GdvAtPGuAf1ocWj1UyPWw3W)    
[Wiki](https://www.elecrow.com/wiki/CrowPanel_Pico_HMI_Display-3.5.html)    

### ✅ 터치스크린 프로토콜
첫번째 입력포트의 값이 on 일때
```
{ "c":1,"n":0,"v":1)
```

| 항목     | 바이트 수   | 설명                           |
| ------ | ------- | ---------------------------- |
| c | 1 byte  | commmand  (1:입력, 2:출력 )                |
| n  | 1 byte  | 입출력 포트번호 |
| v  | 1 byte  | int bool 등의 값  |


```
[0xA5][len][cmd][data...][chk]
```

| 항목     | 바이트 수   | 설명                           |
| ------ | ------- | ---------------------------- |
| `0xA5` | 1 byte  | 헤더 (시작 구분자)                  |
| `len`  | 1 byte  | 데이터 길이 (`cmd + data`의 바이트 수) |
| `cmd`  | 1 byte  | 명령 코드 (1=입력, 2=출력, 3=온도...)  |
| `data` | N bytes | 명령에 따른 실제 데이터                |
| `chk`  | 1 byte  | CRC-8 체크섬 (헤더 제외 전체에 대해 계산)  |

✅ 명령 코드 정의 (cmd)
| 값      | 의미    | 설명                 |
| ------ | ----- | ------------------ |
| `0x01` | 입력    | 버튼 번호 및 on/off 상태  |
| `0x02` | 출력    | 모터 상태 등            |
| `0x03` | 온도 센서 | 온도 전송 (`uint16_t`) |

✅ 예시 ①: 입력 명령 (버튼 2번이 ON)
| 필드  | 값                             |
| --- | ----------------------------- |
| 헤더  | `0xA5`                        |
| 길이  | `0x02` (명령 1 + 데이터 1 + 1 = 2) |
| 명령  | `0x01` (입력)                   |
| 데이터 | `0b00100001` = 버튼번호 2, 상태 ON  |
| CRC | 계산된 CRC8 값                    |

✅ CRC8 계산 방법 (예: x^8 + x^2 + x + 1)
```
uint8_t crc8(const uint8_t *data, size_t len) {
  uint8_t crc = 0x00;
  for (size_t i = 0; i < len; ++i) {
    crc ^= data[i];
    for (uint8_t j = 0; j < 8; ++j) {
      if (crc & 0x80)
        crc = (crc << 1) ^ 0x07;  // 다항식: x^8 + x^2 + x + 1 (0x07)
      else
        crc <<= 1;
    }
  }
  return crc;
}
```

# LVGL (Light and Versatile Graphics Library)
임베디드 시스템용 고성능 그래픽 UI 프레임워크
적은 메모리에서도 부드럽고 직관적인 터치 UI를 구현할 수 있는 오픈소스 그래픽 라이브러리입니다
[lvgl 기술사이트](https://github.com/lvgl/lvgl)    

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

기본적인 문자를 출력해 봅니다.
Text 출력 Hello 
```
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
버튼 출력 프로그램
```
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

# I2C 통신 프로그램
마스터 프로그램 : 터치스크린 RP2040
```
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

슬레이브 프로그램 : IoT PLC ESP32
```
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
