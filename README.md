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
- 어플설치    
- Node-RED 설치 및 설정    
- 로컬, AWS, 스마트폰 애플리케이션 환경에서의 Node-RED 플로우 설정    
- 각 기기의 모니터링 및 제어 테스트

### 안드로이드 어플
QR CODE 연결하거나 그림을 누르세요
<a href="https://play.google.com/store/apps/details?id=io.ionic.i2rReactIoT">
    <img src="https://github.com/kdi6033/i2r-03/assets/37902752/4f55641c-9a50-4eda-8ada-3e0f6beb34c6" alt="다운로드 QR코드" width="200">

### node red 프로그램    
- 어플에서 IoT-PLC를 와이파이에 접속만 시키면 데이터베이스에 자동 저당되고 제어판넬이 자동으로 생성되어서 모니터링/제어를 할 수 있다.    
mongoDB에 데이터가 자동으로 저장 된 모습    
<img src="https://github.com/user-attachments/assets/1c8ee718-8561-4eeb-bdd4-366b209b9fc6" width="50%">    
node red 에서 자동 생성죈 제어판넬    
![i2r-판넬](https://github.com/user-attachments/assets/795ec810-7478-4fc8-a41f-b7e726ee1cb1)    
node red flow    
![nodered-flow](https://github.com/user-attachments/assets/69855573-c93a-4180-be8a-5cd442f85d2c)    

[윈도우 PC용 소스프로그램](https://github.com/kdi6033/i2r/blob/main/0%20Source-Program-IOT/nodered-local.json)    
[아마존 크라우드 AWS 소스프로그램](https://github.com/kdi6033/i2r/blob/main/0%20Source-Program-IOT/nodered-aws.json)
