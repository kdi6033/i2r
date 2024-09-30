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
    <img src="https://github.com/kdi6033/i2r-03/assets/37902752/4f55641c-9a50-4eda-8ada-3e0f6beb34c6" alt="다운로드 QR코드" width="200">
</a>  
<a href="https://youtu.be/bLvpejVkJcQ">
    <img src="https://github.com/user-attachments/assets/9523bd58-8626-4707-af54-0d5fd12a8c82" alt="IoT PLC App 통신 설정" width="400">
</a>
<a href="https://youtu.be/-O2wFqJ9-Qw">
    <img src="https://github.com/user-attachments/assets/4b88edef-1c0a-4c19-bd82-464cf4cacede" alt="입출력, 온도, 습도 동작설정" width="400">
</a>    
    
구매하신 보드에는 다음 프로그램이 설치되어 있습습니다. 어플과 연동하는 아두이노 프로그램으로 응용해서 사용하실 분들은 이 프로그램을 활용하세요. <br>

[i2r-02 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-02/blob/main/0%20Source-Program-IoT/board-i2r-02-local.ino)    
[i2r-03 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-03/blob/main/0%20Source-Program-IoT/board-i2r-03-local.ino)    
[i2r-04 보드 아두이노 소스프로그램](https://github.com/kdi6033/i2r-04/blob/main/0%20Source-Program-IoT/board-i2r-04-local.ino)    

### 아두이노 프로그램 설정    
<a href="https://youtu.be/UrJd-RHRh6U">
    <img src="https://github.com/user-attachments/assets/67556286-b878-44ef-9175-553a6aa418ef" alt="Updating the screen" width="400">
</a>
![24-7 보드 아두이노 프로그램](https://github.com/user-attachments/assets/67556286-b878-44ef-9175-553a6aa418ef)


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

# PC IoT 서버    
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

# 아마존 크라우드 AWS IoT 서버
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


# 프로토콜
i2r 보드의 mqtt 통신에서는 아래와 같이 구성되어 email을 저장하면 다음 토픽으로 자신에 해당되는 데이터를 통신 할 수 있습니다.     
intopic : i2r/email주소/in    
outtopic=i2r/email주소/out    
|order|  기능  |설명 및 프로토콜|
|--|-------|---|
|0|펌웨어 다운로드|인터넷에서 통신으로 펌웨어를 보드로 내려 받는다<br> {'order':0,'fileName'='i2r-03.ino.bin'}|
|1|정보입력|와이파이 및 통신에 필요한 정보를 보내 보드에 기록하여 기기는 여기 정보로 통신을 연결한다.<br> {"order":1,'ssid':'***','password'='***', 'email':'***', 'mqttBroker':'ai.doowon.ac.kr'}|
|2|핀출력| IoT PLC의 핀번호(0,1,2,3 4개)와 true/false를 보내면 릴레이가 동작한다. <br>{"mac":"A0:B7:65:CD:4D:34","order":2,"no":1,"value":true}<blockquote>맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 1번핀 릴레이를 on 시킨다.</blockquote> |
|3|상태전송요청|보드의 현재 상태를 mqtt로 보낸다.<br>요청 : {"mac":"EC:64:C9:43:E8:B8",'order':3}<blockquote> 맥어드레스가 "EC:64:C9:43:E8:B8"인 기기의 현재 상태를 보내온다. </blockquote> 응답예시  <br>{"type":3,"email":"kdi6033@gmail.com","mac":"EC:64:C9:43:E8:B8","temp":28.4,"humi":38,"in":[0,0,0,0],"out":[0,0,0,0]}|
|4|동작시간설정 | 보드의 동작시간을 일일 일주일 단위로 설정한다. <br>{'order':4,"oper":operation,"pI":pinIndex,"sH":시작시간,"sM":시작분,"eH":종료시간,"eM":종료분, "rM":repeatMode,"dW":dayOfWeek}<br>pI:pinIndex 출력핀 번호 0번부터 시작한다.<br> operation : "insert":설정을 추가한다. "delete":한개의 설정을 삭제한다. "deleteAll":모두 삭제한다.<br>repeatMode : "daily"="d", "weekly"="w"<br>dayOfWeek : 일주일 중 요일설정 일=0,월=1,화=2,수=3,목=4,금=5,토=6<br>예제<br>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"insert","pI":0,"sH":9,"sM":55,"eH":9,"eM":57,"rM":"d","dW":0}<blockquote>오전9시55분부터 9시57분까지 매일 동작한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"insert","pI":0,"sH":9,"sM":55,"eH":9,"eM":57,"rM":"w","dW":1}<blockquote>오전9시55분부터 9시57분까지 매주 월요일에 동작한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"list","pI":0}<blockquote>0번 포트에 저장 리스트를 보여준다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"delete","pI":0,"slotIndex":0}<blockquote>0번핀의 0번째 리스트를 삭제한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"deleteAll","pI":0}<blockquote>0번 핀의 저장된 값을 모두 지운다.</blockquote>|
|5|입력핀에 출력설정|입력핀의 on off 동작에 따라 출력을 연결한다. 통신에 연결되어 있는 모드 기기의 출력포트를 연결 할 수 있다.<br>예제<br> operation : "save":출력설정을 저장한다. "list":설정된 값의 리스트를 요구한다. "delete":선택한 설정 값을 지운다. <br>{"order":5,"oper":"save","mac":"A0:B7:65:CD:4D:34","portNo":0,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":1,"value":false},{"mac":"B0:A7:32:1D:B3:B8","port":1,"value":true}]} <blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀의 동작 저장 on 될때 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀이 on(true) 된다. off 될때 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀이 off(false) 된다. </blockquote>{"order":5,"mac":"A0:B7:65:CD:4D:34","oper":"list","portNo":0} <blockquote>맥어드레스 "A0:B7:65:CD:4D:34" 기기 0번 핀의 설정 값을 요청한다.</blockquote>응답 메세지 예시 <br>{"order":6,"mac":"A0:B7:65:CD:4D:34","portNo":0,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":1,"value":false},{"mac":"B0:A7:32:1D:B3:B8","port":1,"value":true}]}<br>{"order":5,"mac":"A0:B7:65:CD:4D:34","oper":"delete","portNo":0}<blockquote>0번 핀의 저장된 값을 모두 지운다.</blockquote>|
|6|온도변화에 출력설정|예제<br>{"order":6,"oper":"save","mac":"A0:B7:65:CD:4D:34","tempHigh":28,"tempLow":27,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":0,"value":false},{"mac":"D4:8A:FC:B5:30:10","port":0,"value":true}]} <blockquote>온도가 28도를 넘어설 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 on 되고 온도가 27도에서 떨어질 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 off 된다</blockquote>{"order":6,"mac":"A0:B7:65:CD:4D:34","oper":"list"}<blockquote>맥어드레스 "A0:B7:65:CD:4D:34" 기기 온도설정 리스트를 요청한다.</blockquote>    {"order":6,"oper":"cali","mac":"A0:B7:65:CD:4D:34","calTemp":28.1}<blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 현재 온도를 28.1로 세팅한다.</blockquote>{"order":6,"mac":"A0:B7:65:CD:4D:34","oper":"delete"}<blockquote>맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 온도에 따른 동작 연결을 삭제한다.</blockquote>|
|7|습도변화에 출력설정|예제<br>{"order":7,"oper":"save","mac":"A0:B7:65:CD:4D:34","humiHigh":50,"humiLow":49,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":0,"value":false},{"mac":"D4:8A:FC:B5:30:10","port":0,"value":true}]}<blockquote> 습도가 50을 넘어설 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 on 되고 습도가 49로 떨어질 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 off 된다</blockquote>{"order":7,"mac":"A0:B7:65:CD:4D:34","oper":"list"}<blockquote>맥어드레스 "A0:B7:65:CD:4D:34" 기기 온도설정 리스트를 요청한다.</blockquote> {"order":7,"oper":"cali","mac":"A0:B7:65:CD:4D:34","calHumi":48}<br><blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 현재 습도를 48로 세팅한다.</blockquote>{"order":7,"mac":"A0:B7:65:CD:4D:34","oper":"delete"}<blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 습도에 따른 동작 연결을 삭제한다.</blockquote>|

위에 기술한 프로토콜을 node red 에서 실행 한 것입니다. 폰의 어플에서 구현한 것을 node red로 프로그램해서 사용하세요.
<a href="https://youtu.be/ufBprCdABSk">
    <img src="https://github.com/user-attachments/assets/01886cc0-2b59-4e1c-962b-f5b7cc751a45" alt="i2r 프로토콜" width="800">
</a>

[프로토콜 node red 소스프로그램](https://github.com/kdi6033/i2r/blob/main/txt/protocol%20node%20red%20example.json)

<a href="https://youtu.be/ufBprCdABSk">
    <img src="https://github.com/user-attachments/assets/fd75d17a-1c77-46e2-872d-b610dede45c3" alt="protocol" width="400">
</a>
