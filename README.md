# MSA_STUDY
[![HitCount](http://hits.dwyl.com/ldk-hub/SpringCloudConfigTEST.svg)](http://hits.dwyl.com/ldk-hub/SpringCloudConfigTEST)

## EUREKA, Ribbon API

Saas 구조 - 12 팩터 앱 자세한 내용 : https://12factor.net/ko/

## MSA - 마이크로서비스 아키텍처란? 
대용량 트래픽을 커버리지하기 위한 서버 중앙화 다중클라이언트 대상으로 실시간 배포를 할 수 있는 강점이 있음. 서비스 로스타임이 없다.(즉시반영)
대규모 서비스 경우 각 서비스별로 모듈화하여 개발할 수 있는 구조 만약 서비스 모듈에서 오류가 발생하게되면 해당서비스만 로스되며 다른서비스에는 영향이 가지 않는 구조 

## 기존 모노리틱 아키텍처와 마이크로 서비스 아키텍처의 차이점
![1](https://user-images.githubusercontent.com/12209348/71953552-f099a000-3225-11ea-98c8-0536deea6d72.PNG)

 - 모노리틱 : 하나의 서버에 모든 시스템 구성을 사용.
 - 마이크로서비스아키텍처 : 서비스는 중앙관리 서버에서 그외 서비스별로 vm 구성을 쪼개어 사용하여 관리하는 구조 
 
 * eureka   
     바야흐로 클라우드 시대, 서버는 실제 서버 컴퓨터에서 돌아가지않고 아마존과 같은 호스팅 업체가 관리하는 클라우드 서버에서 실행된다.   
     서버 IP는 유동적으로 변경되고 서버 관리자는 이에 대한 조치를 일일이 하기 힘듬으로 동적으로 이동하는 서버(eureka client)를 관리하는 서버(eureka server)를 구성하여 조치한다.   
     이렇게 실제 클라이언트의 요청을 처리하는 서버(eureka client)들 사이에서 Middle-tier(중간다리) 역할을 하는것이 eureka server이다.   
     eureka client 관리뿐 아니라 로드 밸런싱이나 장애 복구 기능까지 제공한다.   

     eureka_discovery   
   -  Service Registry: 서비스(eureka client)가 자기 자신의 정보를 Eureka Server에 등록하는 행동   
   -  Service Discovery: 클라이언트가 요청을 보내면 Service Registry 되어있는 서비스 들을 Eureka Server에서 발견하는 과정  
   -  Eureka 구성 요소 관련  
   -  Eureka Server: Eureka Client들을 관리(등록, 제어, 삭제, 제공) 하는 서버  
   -  Eureka Client: Service Registry 하여 서비스에 대한 비지니스 로직을 처리하는 클라이언트, 다른 Eureka Client 들과 연동하여 비지니스 로직을 처리한다.  
   -  Eureka Service: Eureka Server에 등록된 서비스를 가리킴, Eureka Client가 제공하는 서비스로 하나의 서비스의 원활한 수행을 위해 동시에 같은 서비스를 지원하는 여러개의 Eureka Client 가 동작할 수 있다.  
   -  Eureka Instance: Eureka에 등록되어 목록에서 조회 가능한 Eureka Service를 의미  

  * 리본 (부하분산 처리) 
   - 클라이언트 로드밸런서
   - 기본 라운드로빈(RR) 방식의 부하분산 처리가능 
   - 스프링클라우드로 부터 서버목록을 전달받아 사용가능
   - 클라이언트에서 서버에 접근하는 방식으로 3번이상 연결실패 시 다른 서버로 연결시도함.
  
  * 로드밸런서에서 로드밸런싱이 이뤄지지않고 
    - api-gateway에서 로드밸런스 됨. ribbon은 eureka 서비스 사용시 내부에서 같이 작동한다.
    - HTTP,TCP,UDP 모두지원 함
    - 대상의 지속적인 ping을 체크하여 서비스 UP/DOWN을 판단할 수 있음.
 
 * 기존 서버사이드 방식과 리본의 방식 
  ![1](https://user-images.githubusercontent.com/12209348/67823500-b6fe3780-fb06-11e9-98c6-ddaef4ff87fb.PNG)
 
 * 서킷 브레이커
  - 서킷 브레이커 경우 전류 차단기 처럼 
  - 서로의 접점이 문제가 발생 할 경우 해당 문제부분을 일시적으로 차단시켜주어 기존의 사용중인 서비스는 유지하고 문제되는부분만 격리시켜주는 기능

 * 넷플릭스OSS (키워드)
   - ZUUL: 클라이언트의 요청을 해당 경로로 전달하는 역할
   - HYSTRIX :서킷브레이커 라이브러리를 제공(시스템 장애생기면 연쇄작용으로 무너지지않게 차단기역할)
   - RIBBON : 로드밸런싱 기능
   - EUREKA : 유레카 서버에서 유레카 클라이언트 대상으로 중앙 관리를 할 수 있는 구조
 

## MSA 사용목적  
대규모 트래픽 몰리는 서비스 경우  
하나의 시스템에서 트래픽이몰리거나 유입이 많은 서비스를 분산시켜 장애 대응 및 세부 관리를 할수있음.  
 - 기존의 모놀리틱 -> MSA 전환   

## 변경 키워드  
  - 톰캣에서 < - > hikariCP   
  - 유레카  
  - 리본 
  - 히스트릭스  
  - 줄  
  - 서킷브레이커  

## 계획  
- chapter - 서비스별 분산구조 구성 테스트   
       * 유레카 서버에 로그인, 회원가입, 메인화면 구성  
       * 유레카 클라이언트에서는 통계대시보드, 차트 통계,캘린더 페이지 구성  
chapter 2. - 서비스 부하분산 테스트  
         
chapter 3. - 서킷브레이커 테스트  

## 개발 환경  
 - java, jsp , springboot  
 - hikariCP  
 - Jquery, ajax, jpa, Mybatis  
 - postgresqlDB, OracleDB ->H2(DB중 가벼움)  
 
 ## 진행이슈  
  - 노트북의 메모리와 CPU가 2개의 db구동과 여러개의 서비스 실행과정에서 OOM이 발생 해당 테스트 환경 대응방안 모색   
  - 메모리 점유율 이슈 (간헐적으로 블루스크린발생)sts 최적화 작업, oracle xe, postgresqldb, 노트북 프로세스 모두 종료 후 세팅 등    
  - 노트북 메모리 이슈는 기존 오라클, 포스트그레스큐엘을 >H2, 포스트그레스큐엘을 사용하여 테스트예정  
  - 포스트그레스큐엘은 jpa로만 구성, H2는 마이바티스로 구성  
  - 기존 대시보드 프로젝트를 MSA시스템 구성으로 채택  
 
  * 예제개발 진행예정 항목리스트
   - 기존의 adminDashBoard프로젝트를 2분할하여 MSA로 구성계획 및 설계안 작성
   - 두개의 DBMS로 분할 postgresql, oracle DB 
   - 유입이 많을 것같은 서비스를 별도의 서비스로 분할하여 
   - 모노리틱으로 구성된 프로젝트를 MSA로 구성하는 방향으로 컨셉을 잡아 설계
