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

# PC IoT 서버    
- PC에서 node red 와 mongoDB를 설치하여 인터넷 상에서 제어한다.
- 어플에서 IoT-PLC를 와이파이에 접속만 시키면 데이터베이스에 자동 저장되고 제어판넬이 자동으로 생성되어서 모니터링/제어를 할 수 있다.

<a href="https://youtu.be/nL3qdDtZC98">
    <img src="https://github.com/user-attachments/assets/1015639c-ed79-44fb-a690-3545664a31e7" alt="node red 설치 윈도우용 " width="400">
</a>
<a href="https://youtu.be/5spmnQX0IjM">
    <img src="https://github.com/user-attachments/assets/9da548f6-9872-48d7-846c-e790586c5511" alt="mongodb, compass 윈도우용 설치하기 " width="400">
</a>    

[윈도우 PC용 소스프로그램](https://github.com/kdi6033/i2r/blob/main/0%20Source-Program-IOT/nodered-local.json)    
![nodered-flow](https://github.com/user-attachments/assets/69855573-c93a-4180-be8a-5cd442f85d2c)   
 
mongoDB에 데이터가 자동으로 저장 된 모습    
<img src="https://github.com/user-attachments/assets/1c8ee718-8561-4eeb-bdd4-366b209b9fc6" width="400">    <br>
- node red 에서 자동 생성된 제어판넬    
<img src="https://github.com/user-attachments/assets/91897ea9-785e-488f-9f3e-241a049b78f3" width="30%"><br>
node red flow    
 


[아마존 크라우드 AWS 소스프로그램](https://github.com/kdi6033/i2r/blob/main/0%20Source-Program-IOT/nodered-aws.json)
