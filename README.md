# ✅ i2r IoT 기기
아이티알에서 제작한 기기 관련 정보를 제공합니다.    
Data Scientist, AI Scientist 를 희망하시는 분들에게 도움을 드리려 합니다.    
<br>
Node-RED를 활용하여 로컬 컴퓨터, AWS 클라우드, 스마트폰 애플리케이션에서 i2r-02, i2r-03, i2r-04 기기의 모니터링 및 제어를 가능하게 합니다.
**주요 기능 **   
- React 웹앱 기반 모니터링 및 제어: 다양한 환경에서 i2r 기기를 실시간으로 모니터링하고 제어할 수 있습니다.    
- 로컬 컴퓨터: 로컬 네트워크를 통해 기기를 모니터링하고 제어할 수 있습니다.
- AWS 클라우드: 클라우드 기반으로 원격지에서도 기기의 상태를 모니터링하고 제어가 가능합니다.     
- 스마트폰 애플리케이션: 모바일 앱을 통해 언제 어디서나 기기의 상태를 확인하고 제어할 수 있습니다.

**기기 정보**   
링크를 누르면 기기 설명 사이트로 이동 합니다.    
- [i2r-01](https://github.com/kdi6033/i2r-01/tree/main/0%20Android%20App%20Program/server-i2r-01): 블루투스, mqtt, RS485, RS232 인터넷통신을 서로 연결합니다.    
- [i2r-02](https://github.com/kdi6033/i2r-02/tree/main/0%20Source-Program-IoT/board-i2r-02): 입출력 각4채널의 입출력 제어하는 IoT PLC     
- [i2r-03](https://github.com/kdi6033/i2r-03/tree/main/0%20Source-Program-IoT/board-i2r-03) : 입출력 각4채널의 입출력 제어하는 IoT PLC, 온습도 센서     
- [i2r-04](https://github.com/kdi6033/i2r-04/tree/main/0%20Source-Program-IoT/board-i2r-04) : 입출력 각2채널의 입출력 제어하는 IoT PLC, 2개의 아나로그 입력    

**사용 방법**      
- 스마트폰 또는 탭으로 제어 : AWS 클라우드 웹앱 프로그램    
- PC IoT 서버  
- 아마존 크라우드 AWS IoT 서버
- 자세한 사용법과 서버 구축의 세부내용은 아래를 참조하세요

**스마트폰,탭,PC로 제어**    
https:// i2r.link  접속하면 페이지마다 유튜브 링크를 따라 해보시면 쉽게 사용할 수 있습니다.

[i2r-02 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-02/releases/tag/board-i2r-02-v1.0)    
[i2r-03 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-03/releases/tag/board-i2r-03-v1.0)    
[i2r-04 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-04/releases/tag/board-i2r-04-v1.0)    


# ✅ 프로토콜
**2025년7월15일 chatgpt에 적합한 프로토콜을 새로 작성하고 있습니다. 이전에 구매한 보드는 7월30일 이후 새로운 펌웨어를 다운 받아 주세요**

- i2r 보드의 mqtt 통신에서는 아래와 같이 구성되어 email을 저장하면 다음 토픽으로 자신에 해당되는 데이터를 통신 할 수 있습니다.     
- 이 문서는 i2r IoT 보드와 클라이언트 간 MQTT 통신 시 사용하는 JSON 기반 명령어 프로토콜을 설명합니다.  
- 모든 메시지는 경량화를 위해 **축약된 필드명**과 **축약된 명령어 코드(`c`)**를 사용합니다.

## 기본 MQTT 토픽 구조
---
- **intopic**  : `i2r/{email}/in`  
- **outtopic** : `i2r/{email}/out`

> `email`은 각 사용자의 고유 ID 역할을 합니다.
---

## JSON 메시지 필드명 요약

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
| sensorHighValue   | `h`      | 센서 동작의 상한 값 (예: 온도 28도)                                                |
| humidity          | `humi`   | 센서 현재 습도 값 (예: `55`)                                                       |
| in                | `in`     | 입력 상태 배열 (예: `[0,1,0,0]`)                                                  |
| sensorLowValue    | `l`      | 센서 동작의 하한 값 (예: 온도 26도)                                                 |
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
| temperature       | `temp`   | 센서 현재 온도 값 (예: `27.8`)                                                     |
| trigger           | `tr`     | `bio`: ON(true) OFF(false) 가 될 때 트리거 설정 후 delay를 설정하면 그 시간에 동작한다.   |
| type              | `t`      | `gs`: 보드 종류 (예: `3` = i2r-03)<br>`bs`: 센서 타입 (`temp`, `humi`, `light`)    |

---

## 명령어 축약 코드 목록

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
## 예제 및 상세 설명 

| `command` (`c`) | 예제 및 상세 설명 |
|----------------|-------------------|
| **`downloadFirmware`**<br> (`df`) |인터넷에서 통신으로 펌웨어를 보드로 내려 받는다<br> {"c":"df","m":"D8:13:2A:C3:E7:68","fileName":"i2r-03.ino.bin"} |
| **`setInfo`** <br>(`si`) |와이파이 및 통신에 필요한 정보를 보내 보드에 기록하여 기기는 여기 정보로 통신을 연결한다.<br> {"c":"si",'ssid':'***','password'='***', 'e':'***', 'mqttBroker':'ai.doowon.ac.kr'}} |
| **`bindIO`**<br> (`bio`) | **`bind_input_output`**<br>- operation: insert <br>```{"c":"bio","o":"insert","n":0,"v": 1,"d":20,"ps": [{ "m": "XX:XX", "n": 3, "v": 1, "d": 3 }]}``` <br>입력 2번포트(n:2)가 트리거 ON(v:1)이 되면 지정한 기기(mac:"m":"XX:XX") 출력 포트(n:3)를 3초(d:3) 후에 ON(v:1) 합니다.<br>- operation: list <br> ```{"c": "bio","o": "list","m": "A0:B7:65:CD:4D:34","n": 0}``` <br> "A0:B7:65:CD:4D:34" 보드의 0번 입력 핀에 설정된 출력 연동 목록을 요청합니다. <br> 응답메세지 예시 ```{"c": "bio","m": "A0:B7:65:CD:4D:34","n": 0,"ps": [{ "m": "D4:8A:FC:B5:30:10", "n": 1, "v": 0 },{ "m": "B0:A7:32:1D:B3:B8", "n": 1, "v": 1 }]}``` <br>해당 입력 핀에 연결된 출력 포트 정보가 응답으로 전송됩니다. <br> - operation: delete <br> ```{"c": "bio","o": "delete","m": "A0:B7:65:CD:4D:34","n": 0,"sI":1}``` <br> 입력 핀 0번(n:0)의 1번 슬롯(sI:1) 저장된 출력 연동 설정을 삭제합니다.<br> - operation: deleteAll <br> ```{"c": "bio","o": "deleteAll","m": "A0:B7:65:CD:4D:34","n": 0}``` <br> 입력 핀 0번에 저장된 모든 출력 연동 설정을 삭제합니다.|
| **`bindSensor`**<br> (`bs`) | ```{ "c": "bs", "m": "A0:B7:65:CD:4D:34", "o": "save", "t": "temp", "h": 28, "l": 27, "ps": [ { "m": "D4:8A:FC:B5:30:10", "n": 0, "v": 1 }, { "m": "D4:8A:FC:B5:30:10", "n": 0, "v": 0 } ] }```<br>온도 "A0:B7:65:CD:4D:34" 보드의 온도센서 값이 28도 초과 시 "D4:8A:FC:B5:30:10" 보드의 0번 포트 ON, 27도 이하 시 "D4:8A:FC:B5:30:10" 보드의 0번 포트가 OFF하는 자동 제어. `t`는 센서 종류(`temp`, `humi`, `light`)를 의미합니다. |ㅇ:
| **`downloadFirmware`**<br> (`df`) | ```{ "c": "df", "m": "D8:13:2A:C3:E7:68", "fileName": "i2r-03.ino.bin" }``` <br>지정한 MAC 주소를 가진 보드에 인터넷을 통해 펌웨어를 다운로드합니다. `.ino.bin` 또는 `.bin` 파일이 대상이며, OTA 업데이트를 통해 자동 적용됩니다. |
| **`getStatus`**<br> (`gs`) | ```{ "c": "gs", "m": "EC:64:C9:43:E8:B8" }```<br>지정 보드의 상태를 요청합니다. 응답으로 온도, 습도, 입력포트(`in`), 출력포트(`out`) 정보가 포함됩니다.<br>응답 예시:<br>`{"t":3,"email":"kdi6033@gmail.com","m":"EC:64:C9:43:E8:B8","temp":28.4,"humi":38,"in":[0,0,0,0],"out":[0,0,0,0]}` |
| **`scheduleOutput`**<br> (`sch`) | ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "insert", "n": 0, "start": 540, "end": 620, "rm": 0, "dw": [1,2,3,4,5] }```<br>출력핀 0번을 월~금 오전 9:00~10:20까지 자동으로 ON 되도록 예약합니다. `rm=0`은 매일 반복, `dw=[1~5]`는 월~금을 의미합니다. <br> ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "insert", "n": 0, "start": 595, "end": 597, "rm": 1, "dw": [1] }``` <br> 오전 9시 55분(9*60+55=595)부터 9시 57분(597)까지 매주 월요일(dw: [1])에 0번 출력 포트를 ON 하도록 예약합니다. rm: 1은 반복 모드로 "매주"를 의미합니다.<br> ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "list", "n": 0 }``` <br> 0번 포트에 저장된 스케줄 예약 리스트를 보여줍니다.<br> ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "delete", "n": 0, "slot": 0 }``` <br> 0번 출력 포트에 등록된 예약 중 첫 번째(slotIndex: 0) 항목을 삭제합니다.<br> ```{ "c": "sch", "m": "A0:B7:65:CD:4D:34", "o": "deleteAll", "n": 0 }``` <br> 0번 포트에 저장된 모든 예약 스케줄을 삭제합니다. |
| **`setInfo`**<br> (`si`) | ```{ "c": "si", "ssid": "i2r_wifi", "password": "00000000", "email": "user@example.com", "mqttBroker": "mqtt.i2r.link" }``` <br> 보드가 Wi-Fi 및 MQTT 브로커에 연결할 수 있도록 설정 정보를 저장합니다. 이후 재시작 시 자동 연결됩니다. |
| **`setOutput`**<br> (`so`) | ```{ "c": "so", "m": "A0:B7:65:CD:4D:34", "n": 1, "v": 1 }``` <br> 지정 보드의 `n`번 출력 핀을 제어합니다. `v: 1`은 ON, `v: 0`은 OFF입니다. 릴레이, 모터, LED 등에 사용됩니다. |
| **`touchInput`**<br> (`ti`) | ```{ "c": "ti", "light": 120 }```<br>RP2040 등의 외부 터치패널에서 측정한 조도 값을 IoT 보드에 전달하여 조건 제어에 활용할 수 있습니다. |

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

# ✅ PC IoT 서버 (React)    
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


# ✅ IoT PLC HMI 한글 터치스크린

ESP32 IoT PLC와 CrowPanel(RP2040)을 RS232 직렬 통신으로 연결하여,
CrowPanel은 사용자 인터페이스(UI) 및 I2C 센서 계측을 담당하고,
ESP32는 릴레이 제어 및 클라우드(MQTT) 연동을 담당하는 IoT 제어 시스템입니다.

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

## 1. CrowPanel Pico Display 3.5" HMI 모듈

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

## CrowPanel(RP2040) 3.5" 터치스크린

⚙️ 주요 사양 (Specifications)
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


📺 CrowPanel(RP2040) 기술 자료    
[참조기술문서 및 프로그램 다운로드](https://github.com/Elecrow-RD/CrowPanel-Pico-Display-Course-File)    
[회로도](https://github.com/user-attachments/files/20807927/CrowPanel_Pico_Display-3.5_V1.0-SCH.pdf)    
[유튜브 시청](https://www.youtube.com/watch?v=5lLdKOjR-Lo&list=PLwh4PlcPx2GdvAtPGuAf1ocWj1UyPWw3W)    
[Wiki](https://www.elecrow.com/wiki/CrowPanel_Pico_HMI_Display-3.5.html)    

###  터치스크린 프로토콜
조도센서 값을 참조하는 예제
```
{ "c": "ti", "light": 120 }
```

# ✅ I2C 통신 프로그램
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

# ✅ LVGL 한글 터치스크린 프로그램 HMI
그래픽과 터치스크린을 구현하기 위한 구조를 설명하겠습니다.
- LVGL 에서는 그래픽에 필요한 설정을 해야 합니다.
- ILI9341 는 터치 스크린마다 사용하는 종류가 달라지므로 TFT_eSPI 에 정의를 해야 합니다.
     
## 1. LVGL + TFT_eSPI + ILI9341 관계

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

## 2. LVGL (Light and Versatile Graphics Library) 디스플레이 드라이버
적은 메모리에서도 부드럽고 직관적인 터치 UI를 구현할 수 있는 오픈소스 그래픽 라이브러리입니다    
다음 기술 사이트를 참조하세요   
[lvgl 기술사이트](https://github.com/lvgl/lvgl)    

** 디스플레이 드라이버의 역할 **
LVGL 디스플레이 드라이버는 아래 두 가지를 담당합니다.
1) Flush callback (disp_drv.flush_cb)
- LVGL이 "이 영역을 빨간색으로 칠해라"라고 명령을 내리면,
- flush_cb 함수가 해당 픽셀 데이터를 실제 LCD 드라이버(ST7796, ILI9341 등) 로 전송합니다.
2) Buffer 관리 (lv_disp_draw_buf_t)
- LVGL은 화면 전체 크기만큼의 버퍼를 만들 필요가 없습니다.
- 보통 화면의 1/10~1/20 크기 버퍼만 두고, 해당 영역만 갱신합니다.
- 이 버퍼와 실제 하드웨어 전송을 연결하는 것이 디스플레이 드라이버의 역할입니다.

## lvgl 설치 후 lv_conf.h 파일 만들기
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

## 3. 디스플레이 드라이버 TFT_eSPI 설치
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


## 📘 LVGL 한글 폰트 적용 가이드
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
Name : 사용할 이름 입력
Font size: 20 입력 → NotoSansKR_20 생성
Bpp: 4 (일반적으로 4bpp 권장)
Output format: C array 선택
Browse: NotoSansKR-Regular.ttf 선택
Range: 빈칸
Symbols: 사용할 글짜들 입력
Submit 버튼을 누르면 NotoSansKR_20.c 파일이 생성됩니다.
```
<p align="left">
    <img src="https://github.com/user-attachments/assets/ebed64a9-ecf0-4fb0-93fb-a0599bd62cf4" alt="Google Fonts" width="600">
</p>


<details>
<summary>💻 C code 예제</summary>

```c
// ✅ 여기에 C 코드 작성
#include <stdio.h>

int main() {
    printf("Hello, GitHub!\n");
    return 0;
}
```
</details>

rrrrrrrr
