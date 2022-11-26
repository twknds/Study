준비해야될 내용

## 스프링

스프링 : 자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로서 엔터프라이즈급 애플리케이션을 개발하기 위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션

IOC : Depengency Lookup 즉 의존성 탐색 알맞은 의존성을 탐색하는것 , Depengency Ingection 의존성 주입으로 구성되며 Inversion of Control 즉 제어의 역전이라는 의미다,객체의 생성부터 생명주기 관리까지 제어의 주도권이 개발자가 아닌 프레임워크가 쥐게 되면서 개발자는 비즈니스 로직에만 집중할수 있게 된다

PSA : 잘 만들어진 인터페이스를 말하는것으로 스프링의 잘만들어진 인터페이스들을 지칭하는 말이다.
예시로 플랫폼트랜잭션매니저가 존재한다. 플랫폼트랜잭션매니저 인터페이스를 상속받아서 jdbc, hibernate, jpa등등 많은 트랜잭션 매니저를 구현할수있다.
그과정에서 플랫폼트랜잭션매니저의 코드는 변경이없으며 , 또한 외부 api를 테스트하는 코드를 만들기 위해서는 해당 api객체를 생성하는 인터페이스를 정의한후 해당 인터페이스를 상속받은 서비스객체를 생성한후 실제 외부 static API를 사용하는곳에서 구현한 서비스를 주입받게 하면 된다.

AOP : 관점 지향 프로그래밍 , 공통적으로 사용되는 코드 즉 흩어진 관심사를 통일해서 모듈화해 비즈니스로직에서 분리해서 사용하는것. 즉 중복코드를 줄이고 비즈니스 로직에만 집중할수 있도록 하는것에 있다.

gc :

Strong 참조방식의 객체의경우 unreachable해지면 gc의 대상이된다, 아니라면 대상이 되지 않음

jdk 9 이후로는 g1 gc가 기본 mark-sweep and compact방식

old영역으로 넘어가는 객체의 수를 최대한 줄이는것이 관건

## jwt 

header,payload,tail로 구성된다 header는 토큰의 종류를 나타냄 payload는 정보 tail은 암호화

access token , refresh token은 서버단에 저장되는 암호화 데이터로 front단에서 구글 ouath api를 사용해 유저의 구글아이디가 유효할시 code를 발급받게 되고 해당 code를 server로 

회원가입 요청을 하게 되면 email과 nickname값을 user객체로 포장해서 저장한뒤 accessT, refreshT를 발급하고 해당 토큰을 front로 반환해준다.

로그인 요청시 api요청 code를 보내고 해당 code를 파싱해서 email값을 얻고 레포지토리에서 조회후 토큰들 반환

서비스 요청시마다 token유효를 체크하고(인터셉터로 가로챔) accessT ,refreshT 유효성 검증

accessT 유효하지않고 refreshT 유효하지 않을시 Exception

인터셉터에서 예외발생하지 않을시 Controller로 request들 도착

## 컨테이너

## hal-il준비 

## 코드리뷰

## erd

## jsp

## oracle SQL

## jdbc

## apache tomcat

## 서블릿

## nginx 

## 무중단배포 

## jenkins 

## aws 

## n+1문제

## aop 

## psa 

## di 

## junit 

Exception관리 - checked, unchecked 두개의 차이는 컴파일과정에서 컴파일러가 체크하냐 안하냐의 차이이며, unchecked는 runtimeException을 상속받는다.

스프링 공식문서에는 checked는 트랜잭션 rollback이없고 unchecked는 롤백이있다고 되어있는데, 사실 이거는 개발자가 조정할수있는 부분이고 , 애플리ㅏ케이션마다 다른부분이라 한마디로 속단할수없음.


## reflection

## java8 

## java11

## DB

- 정규화

- 인덱스

- 격리레벨
