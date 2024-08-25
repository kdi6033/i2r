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
- [i2r-01](https://github.com/kdi6033/i2r-01): 블루투스, mqtt, RS485, RS232 인터넷통신을 서로 연결합니다.    
- [i2r-02](https://github.com/kdi6033/i2r-02): 입출력 각4채널의 입출력 제어하는 IoT PLC     
- [i2r-03](https://github.com/kdi6033/i2r-03) : 입출력 각4채널의 입출력 제어하는 IoT PLC, 온습도 센서     
- [i2r-04](https://github.com/kdi6033/i2r-04) : 입출력 각2채널의 입출력 제어하는 IoT PLC, 2개의 아나로그 입력    

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
|order|  기능  |설명 및 프로토콜|
|--|-------|---|
|0|펌웨어 다운로드|인터넷에서 통신으로 펌웨어를 보드로 내려 받는다<br> {'order':0,'fileName'='i2r-03.ino.bin'}|
|1|정보입력|와이파이 및 통신에 필요한 정보를 보내 보드에 기록하여 기기는 여기 정보로 통신을 연결한다.<br> {"order":1,'ssid':'***','password'='***', 'email':'***', 'mqttBroker':'ai.doowon.ac.kr'}|
|2|핀출력| IoT PLC의 핀번호(0,1,2,3 4개)와 true/false를 보내면 릴레이가 동작한다. <br>{"mac":"A0:B7:65:CD:4D:34","order":2,"no":1,"value":true}}<blockquote>맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 1번핀 릴레이를 on 시킨다.</blockquote> |
|3|상태전송요청|보드의 현재 상태를 mqtt로 보낸다.<br>요청 : {"mac":"EC:64:C9:43:E8:B8",'order':3}<blockquote> 맥어드레스가 "EC:64:C9:43:E8:B8"인 기기의 현재 상태를 보내온다. </blockquote> 응답예시  <br>{"type":3,"email":"kdi6033@gmail.com","mac":"EC:64:C9:43:E8:B8","temp":28.4,"humi":38,"in":[0,0,0,0],"out":[0,0,0,0]}|
|4|동작시간설정 | 보드의 동작시간을 일일 일주일 단위로 설정한다. <br>{'order':4,"oper":operation,"pI":pinIndex,"sH":시작시간,"sM":시작분,"eH":종료시간,"eM":종료분, "rM":repeatMode,"dW":dayOfWeek}<br>pI:pinIndex 출력핀 번호 0번부터 시작한다.<br> operation : "insert":설정을 추가한다. "delete":한개의 설정을 삭제한다. "deleteAll":모두 삭제한다.<br>repeatMode : "daily"="d", "weekly"="w"<br>dayOfWeek : 일주일 중 요일설정 일=0,월=1,화=2,수=3,목=4,금=5,토=6<br>예제<br>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"insert","pI":0,"sH":14,"sM":10,"eH":14,"eM":20,"rM":1,"dW":0}<blockquote>일요일마다 일주일단위로 14시10분부터 14시20분까지 반복해서 동작한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"insert","pI":0,"sH":9,"sM":55,"eH":9,"eM":57,"rM":"d","dW":0}<blockquote>오전9시55분부터 9시57분까지 매일 동작한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"insert","pI":0,"sH":9,"sM":55,"eH":9,"eM":57,"rM":"w","dW":1}<blockquote>오전9시55분부터 9시57분까지 매주 월요일에 동작한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"delete","pI":0,"slotIndex":0}<blockquote>0번 리스트를 삭제한다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"list","pI":0}<blockquote>0번 포트에 저장 리스트를 보여준다.</blockquote>{"order":4,"mac":"A0:B7:65:CD:4D:34","oper":"deleteAll","pI":0}<blockquote>0번 핀의 저장된 값을 모두 지운다.</blockquote>|
|5|입력핀에 출력설정|입력핀의 on off 동작에 따라 출력을 연결한다. 통신에 연결되어 있는 모드 기기의 출력포트를 연결 할 수 있다.<br>예제<br> operation : "save":출력설정을 저장한다. "list":설정된 값의 리스트를 요구한다. "delete":선택한 설정 값을 지운다. <br>{"order":5,"oper":"save","mac":"A0:B7:65:CD:4D:34","portNo":0,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":1,"value":false},{"mac":"B0:A7:32:1D:B3:B8","port":1,"value":true}]} <blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀의 동작 저장 on 될때 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀이 on(true) 된다. off 될때 맥어드레스가 "A0:B7:65:CD:4D:34" 0번 핀이 off(false) 된다. </blockquote>{"order":5,"mac":"A0:B7:65:CD:4D:34","oper":"list","portNo":0} <blockquote>맥어드레스 "A0:B7:65:CD:4D:34" 기기 0번 핀의 설정 값을 요청한다.</blockquote>응답 메세지 예시 <br>{"order":6,"mac":"A0:B7:65:CD:4D:34","portNo":0,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":1,"value":false},{"mac":"B0:A7:32:1D:B3:B8","port":1,"value":true}]}|
|6|온도변화에 출력설정|예제<br>{"order":6,"oper":"save","mac":"A0:B7:65:CD:4D:34","tempHigh":28,"tempLow":27,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":0,"value":false},{"mac":"D4:8A:FC:B5:30:10","port":0,"value":true}]} <blockquote>온도가 28도를 넘어설 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 on 되고 온도가 27도에서 떨어질 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 off 된다</blockquote>{"order":6,"oper":"cali","mac":"A0:B7:65:CD:4D:34","calTemp":28.1}<blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 현재 온도를 28.1로 세팅한다.</blockquote>{"order":6,"mac":"A0:B7:65:CD:4D:34","oper":"delete"}<blockquote>맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 온도에 따른 동작 연결을 삭제한다.</blockquote>|
|7|습도변화에 출력설정|예제<br>{"order":7,"oper":"save","mac":"A0:B7:65:CD:4D:34","humiHigh":50,"humiLow":49,"portState":[{"mac":"D4:8A:FC:B5:30:10","port":0,"value":false},{"mac":"D4:8A:FC:B5:30:10","port":0,"value":true}]}<blockquote> 습도가 50을 넘어설 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 on 되고 습도가 49로 떨어질 때 맥어드레스 "D4:8A:FC:B5:30:10" 0번핀이 off 된다</blockquote>{"order":7,"oper":"cali","mac":"A0:B7:65:CD:4D:34","calHumi":48}<br><blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 현재 습도를 48로 세팅한다.</blockquote>{"order":7,"mac":"A0:B7:65:CD:4D:34","oper":"delete"}<blockquote> 맥어드레스가 "A0:B7:65:CD:4D:34"인 기기의 습도에 따른 동작 연결을 삭제한다.</blockquote>|


