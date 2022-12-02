준비해야될 내용

## 스프링

스프링 : 자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로서 엔터프라이즈급 애플리케이션을 개발하기 위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션

IOC : Depengency Lookup 즉 의존성 탐색 알맞은 의존성을 탐색하는것 , Depengency Ingection 의존성 주입으로 구성되며 Inversion of Control 즉 제어의 역전이라는 의미다,객체의 생성부터 생명주기 관리까지 제어의 주도권이 개발자가 아닌 프레임워크가 쥐게 되면서 개발자는 비즈니스 로직에만 집중할수 있게 된다
스프링빈은 런타임시 생성되며 프록시로 생성되며 실제 객체 참조시 인스턴스화된다.

PSA : 잘 만들어진 인터페이스를 말하는것으로 스프링의 잘만들어진 인터페이스들을 지칭하는 말이다.
예시로 플랫폼트랜잭션매니저가 존재한다. 플랫폼트랜잭션매니저 인터페이스를 상속받아서 jdbc, hibernate, jpa등등 많은 트랜잭션 매니저를 구현할수있다.
그과정에서 플랫폼트랜잭션매니저의 코드는 변경이없으며 , 또한 외부 api를 테스트하는 코드를 만들기 위해서는 해당 api객체를 생성하는 인터페이스를 정의한후 해당 인터페이스를 상속받은 서비스객체를 생성한후 실제 외부 static API를 사용하는곳에서 구현한 서비스를 주입받게 하면 된다.

AOP : 관점 지향 프로그래밍 , 공통적으로 사용되는 코드 즉 흩어진 관심사를 통일해서 모듈화해 비즈니스로직에서 분리해서 사용하는것. 즉 중복코드를 줄이고 비즈니스 로직에만 집중할수 있도록 하는것에 있다.

gc :

Strong 참조방식의 객체의경우 unreachable해지면 gc의 대상이된다, 아니라면 대상이 되지 않음

jdk 9 이후로는 g1 gc가 기본 mark-sweep and compact방식

old영역으로 넘어가는 객체의 수를 최대한 줄이는것이 관건

@transactional의 분해 

readonly시 성능향상의 이유? 변경감지를 위한 스냅샷 세션을 저장할필요가 없어서 성능이 향상된다

@transactional 이 명시되면spring aop에서는 transactional 프록시 객체를 호출하게 되고 해당 객체내에서 jdbc transaction을 실행하게 된다.

jdbc transaction 처리의 경우 트랜잭션이 실행되면 해당 트랜잭션이 시행되는동안 db에 대한 쿼리 결과를 임시로 저장하고 트랜잭션이 끝난이후 db에 반영하게 된다.

이과정에서 오류가 발생할시 트랜잭션동안 일어난 모든결과 롤백, 그리고 두개이상의 db에대한 트랜잭션 처리시에는 jta를 사용해야 한다.

## jwt 

header,payload,signature로 구성된다 header는 토큰의 종류와 해시알고리즘 종류를 나타냄 payload는 claims 증 사용자의 정보 및 권한, key-value형태이다 signature는 header, payload를 b64로 암호화하고 이를 대상으로 비밀키로 암호화한것이다.

access token , refresh token은 서버단에 저장되는 암호화 데이터로 front단에서 구글 ouath api를 사용해 유저의 구글아이디가 유효할시 code를 발급받게 되고 해당 code를 server로 

회원가입 요청을 하게 되면 email과 nickname값을 user객체로 포장해서 저장한뒤 accessT, refreshT를 발급하고 해당 토큰을 front로 반환해준다.

로그인 요청시 api요청 code를 보내고 해당 code를 파싱해서 email값을 얻고 레포지토리에서 조회후 토큰들 반환

서비스 요청시마다 token유효를 체크하고(인터셉터로 가로챔) accessT ,refreshT 유효성 검증

accessT 유효하지않고 refreshT 유효하지 않을시 Exception

인터셉터에서 예외발생하지 않을시 Controller로 request들 도착

- 장/단점

규격이 정해져있어서 다양한 웹서비스 클라이언트에 적용하기 쉽다.

payload가 많아지면 토큰이 커져 서버에 부하가 생길수있다.

토큰이 재발급되기 전까지는 사용자 정보가 갱신되어도 변경되지않는다

restful(stateless)한 환경에서 쓰기좋다

데이터를 담고있어서 데이터를 얻기위해서 타 서비스에 요청하는 과정이 줄어든다.

토큰의 만료시간이 있는경우 만료시간까지 파기시킬수없으므로 중요정보를 넣거나 노출시키는 일은 없어야함

인증 : 사용자의 신원을 검사하는 행위

인가 : 리소스나 기능에 액세스할 수 있는 권한을 부여하는 프로세스

## 컨테이너

컨테이너는 어떤 환경에서나 실행하기 위해 필요한 모든 요소를 포함하는 소프트웨어 패키지

컨테이너는 애플리케이션을 실제 구동 환경으로부터 추상화할 수 있는 논리 패키징 메커니즘을 제공

- 컨테이너의 이점

책임 분리,워크로드 이동성,애플리케이션 격리

- 컨테이너 vs VM

컨테이너는 VM보다 훨씬 더 경량입니다.

컨테이너는 OS 수준에서 가상화되고 VM은 하드웨어 수준에서 가상화됩니다.

가상머신은 애플리케이션을 동작시키기 위해서 애플리케이션이 사용하는 리소스만 사용하는 것뿐만 아니라 운영체제가 동작하기 위한 리소스가 추가로 필요

(컨테이너는 OS 커널을 공유하며 VM에 필요한 것보다 훨씬 적은 메모리를 사용합니다)

컨테이너는 가상 머신과 마찬가지로 애플리케이션을 관련 라이브러리 및 종속 항목과 함께 패키지로 묶어 소프트웨어 서비스 구동을 위한 격리 환경을 마련

- 도커

이미지 : 실행할 애플리케이션과 라이브러리 및 환경을 하나의 패키지로 묶은 것

컨테이너 : 이미지를 실행한 컨테이너

레지스트리 : 이미지를 저장하고 공유할 수 있는 스토리지

도커 허브 등과 같은 공용 레지스트리와 개인 및 특정 시스템만 사용할 수 있는 사설 레지스트리를 직접 구축 가능

도커는 컨테이너를 주류 기술로 만든 최초의 컨테이너 플랫폼으로, 쿠버네티스에서 기본적으로 애플리케이션을 구동하기 위한 구성요소 중 하나

서버 운영 측면에서 배포와 운영에 도커를 꼭 써야만 하는 건 아닙니다.

하지만 수평적 확장의 자유로움, 서버의 견고함을 보장하면서 동적으로 바꿀 수 있는 유연함, 인수인계 시간 절약 등의 편리한 해결 방법을 제공하는 도커를 쓰지 않을 이유는 없습니다.

## jdbc

JDBC API는 관계형 데이터베이스에 연결하고 Java 프로그램에서 SQL 쿼리를 실행하는 데 사용

JDBC API는 Java 프로그램과 실제 JDBC 드라이버 간의 느슨한 연결을 허용하는 방식으로 작성되어 한 데이터베이스에서 다른 데이터베이스 서버로 쉽게 전환할 수 있습니다

JDBC-ODBC 브리지 드라이버: JDBC-ODBC 브리지 드라이버는 ODBC 드라이버를 사용하여 데이터베이스에 연결합니다. JDBC-ODBC 브리지 드라이버는 JDBC 메서드 호출을 ODBC 함수 호출로 변환합니다. 이것은 드라이버가 얇기 때문에 권장되지 않습니다. 사용하기 쉽고 모든 데이터베이스에 쉽게 연결할 수 있습니다.

네이티브 API 드라이버(일부 자바 드라이버): 네이티브 API 드라이버는 데이터베이스의 클라이언트 측 라이브러리를 사용합니다. 드라이버는 JDBC 메서드 호출을 데이터베이스 API의 기본 호출로 변환합니다. 완전히 Java로 작성되지 않았습니다. 성능은 JDBC-ODBC 브리지 드라이버보다 우수합니다. 그러나 기본 드라이버는 각 클라이언트 시스템에 설치해야 합니다.

네트워크 프로토콜 드라이버(전체 자바 드라이버): 네트워크 프로토콜 드라이버는 JDBC 호출을 벤더별 데이터베이스 프로토콜로 직간접적으로 변환하는 미들웨어(애플리케이션 서버)를 사용합니다. 전적으로 Java로 작성되었습니다. 감사, 로드 밸런싱, 로깅 등과 같은 많은 작업을 수행할 수 있는 애플리케이션 서버 때문에 클라이언트 측 라이브러리에 대한 요구 사항이 없습니다.

씬 드라이버(전체 자바 드라이버): 씬 드라이버는 JDBC 호출을 공급업체별 데이터베이스 프로토콜로 직접 변환합니다. 그래서 얇은 드라이버로 알려져 있습니다. 전적으로 Java 언어로 작성되었습니다. 성능은 다른 모든 드라이버보다 우수하지만 이러한 드라이버는 데이터베이스에 따라 다릅니다.

## apache tomcat

웹 서버(apache) : 아파치서버란 클라이언트에서 요청하는 HTTP요청을 처리하는 웹서버를 의미한다,

이는 정적타입(HTML, CSS, 이미지 등)의 데이터만을 처리하기 때문에 톰캣이란 것이 등장한 것 같다

톰캣 : 톰캣 또한 아파치 소프트웨어 재단에서 후원을 하고 있으며, 오픈소스로 개발이 되고 있다.

JAVA EE 기반으로 만들어졌으며, JSP와 Servlet을 구동하기 위한 서블릿 컨테이너 역할을 수행한다.

아파치서버와는 다르게 DB연결, 다른 응용프로그램과 상호 작용 등 동적인 기능들을 사용할 수 있다.

서블릿 : 클라이언트의 요청을 받고 요청을 처리하여 결과를 클라이언트에게 제공하는 자바 인터페이스.

java.servlet.package에 정의된 인터페이스로서 서블릿의 라이프 사이클을 위한 세 가지 필수적인 메소드들을 정의한다. init(), service(), destory()

서블릿 컨테이너(servlet container) : 서블릿들을 모아 관리 , 새로운 요청이 들어올 때마다 새로운 스레드를 생성 , 작업이 끝난 서블릿 스레드 자동 제거

WAS(wab application server) : DB 처리, 로직 처리를 요구하는 동적타입을 제공하는 소프트웨어 프레임워크를 의미한다.

기본적으로 사용되는 기능 3가지는 아래와 같다.

- 프로그램 실행 환경과 데이터베이스 접속 기능을 제공한다.
- 여러 개의 트랜잭션을 관리한다.
- 업무를 처리하는 비즈니스 로직을 수행한다.

아파치 톰캣으로 부르는 이유? 기본적으로 위처럼 아파치와 톰캣의 기능은 나뉘어져 있지만, 톰캣 안에 있는 컨테이너를 통해 일부 아파치의 기능을 발휘하기 때문에 보통 아파치 톰캣으로 합쳐서 부르곤 한다.


## nginx 

L4 로드밸런싱 : 네트워크 계층 layer4(전송)에서 실행
TCP/UDP 포트 정보를 바탕으로 진행
데이터 안을 보지 않고 패킷 레벨에서만 진행
속도 빠르고 효율 높다
데이터 내용을 부호화하지 않아 안전하다
L7보다 저렴하다
사용자의 IP가 수시로 바뀌는 경우 연속적인 서비스 제공이 어렵다.

L7 로드밸런싱 : 네트워크 계층 layer7(응용)에서 실행
TCP/UDP + HTTP의 URI, FTP 파일명, 쿠키 정보 등을 바탕으로 진행
캐싱 기능을 제공
상세한 라우팅이 가능
비정상적인 트래픽은 사전에 필터링 > 안전성 높아짐
비용은 L4보다 높다.

소프트웨어에서의 로드밸런싱 : 
기본적으로 Reverse Proxy를 기반으로 동작한다.
로드밸런싱만을 위해 개발된 프로그램이 아니기 때문에 기본적인 로드밸런싱의 기능만이 있지만 그만큼 비용적으로 저렴하고 구축이 쉽다는 장점이 있다.

Nginx : 
오픈소스 소프트웨어
특정 알고리즘은 Nginx Plus에서만 사용이 가능하다.

HAProxy : 
오픈소스 소프트웨어
여러 로드밸런싱 기능을 지원한다.

Nginx 로드 밸런싱 메서드

라운드로빈 

서버의 가중치를 고려해, 실제 서버들을 처음부터 차례로 선택해 가며 모든 서버로 균등하게 분산 됨 (default)
장점 : 거의 균등하게 분산 가능
단점 : 경로가 보장 되지 않음

Least-connected

서버의 가중치를 고려해, 활성 연결 수가 가장 적은 서버로 요청을 전송 함
장점 : 거의 균등하게 분산 가능
단점 : 경로 보장 되지 않음

ip-hash

Hasing key 를 사용하여 IP 별로 Index 를 생성하여 경로를 지정
요청이 전송되는 서버는 클라이언트 IP 주소에서 결정됨
IPv4 주소의 처음 세개의 octets 또는 전체 IPv6 주소가 해시 값을 계산하는 데 사용됨
장점 : 경로 보장 가능
단점 : 균등한 분산이 어려움

무중단 배포

무중단 배포는 서비스 장애와 배포의 부담을 최소화하기 위해 운영 중인 서비스를 중단하지 않고 신규 소프트웨어를 배포하는 기술입니다. 무중단 배포의 핵심은 로드밸런서(Load Balancer)를 통해 연결된 두 개 이상의 (서로 다른 IP, 포트를 가진) 인스턴스에 트래픽을 제어해 배포하는 것입니다. 배포 작업이 서비스에 영향을 주지 않도록 하기 위해 고객의 이용량에 따라 인스턴스는 물론 로드밸런서도 다중화를 고려해야 합니다. 즉, 무중단 배포를 하기 위해서는 고가용성의 시스템 인프라가 구성되어 있어야 합니다

- 롤링 배포(Rolling Deployment)

롤링 배포는 사용 중인 인스턴스 내에서 새 버전을 점진적으로 교체하는 것으로 무중단 배포의 가장 기본적인 방식입니다. 서비스 중인 인스턴스 하나를 로드밸런서에서 라우팅하지 않도록 한 뒤, 새 버전을 적용하여 다시 라우팅하도록 합니다. 이를 반복하여 모든 인스턴스에 새 버전의 애플리케이션을 배포합니다. 인스턴스마다 차례로 배포를 진행하기 때문에 상황에 따라 손쉽게 롤백(Roll Back)이 가능한 장점이 있습니다. 롤링 배포 방식은 가용 자원(인스턴스)이 제한적일 경우에 사용되며 새 버전을 배포할 때 인스턴스 수가 감소하기 때문에 서비스 처리 용량을 고려해야 합니다. 또한 배포가 진행되는 동안 구버전과 신버전이 공존하기 때문에 호환성 문제가 발생할 수 있습니다

- 블루-그린 배포(Blue-Green Deployment)

블루를 구버전, 그린을 신버전으로 지칭하여 붙여진 이름으로 운영 환경에 구버전과 동일하게 신버전의 인스턴스를 구성한 후, 로드밸런서를 통해 신버전으로 모든 트래픽을 전환하는 배포 방식입니다. 구버전과 동일한 운영 환경으로 신버전의 인스턴스를 구성하기 때문에 실제 서비스 환경에서 신버전을 미리 테스트 할 수 있는 장점이 있고 롤링 배포와 마찬가지로 빠른 롤백이 가능합니다. 배포가 완료된 후 남아 있는 기존 버전의 환경을 다음 배포에 재사용할 수 있습니다. 하지만 블루-그린 배포를 위해서는 시스템 자원이 두 배로 필요하며 새로운 환경에 대한 테스트가 전제되어야 합니다.

- 카나리 배포(Canary Deployment)

옛날 광부들이 유독 가스에 민감한 카나리아 새를 이용해 가스 누출 위험을 감지했던 것에서 유래한 것으로 잠재적 문제 상황을 미리 발견하기 위한 방식입니다. 신버전의 제공 범위를 늘려가면서 모니터링 및 피드백 과정을 거칠 수 있습니다. 로드밸런서를 통해 신버전의 제품을 경험하는 사용자를 조절할 수 있는 것이 특징으로 신버전을 특정 사용자(예: 모바일 이용자) 혹은 단순 비율에 따라 구분해 제공할 수 있습니다. 이 방식은 신버전의 배포 전에 실제 운영 환경에서 미리 테스트한다는 점이 블루-그린 배포와 비슷합니다. 하지만 카나리 배포는 단계적인 전환 방식을 통해 부정적 영향을 최소화하고 상황에 따라 트래픽 양을 늘리거나 롤백할 수 있습니다. 단, 롤링 배포와 마찬가지로 신·구 두 버전이 운영되기 때문에 버전 관리가 필요합니다.


## jenkins 

웹훅을 통해서 특정 branch에서 push가 발생시 자동으로 변경된 코드로 배포를 진행해주는 툴

젠킨스 컨테이너를 두개두고 nginx로 평소에는 develop브랜치를 가르치는 젠킨스컨테이너를 지정해놓고 코드변경시에는 update브랜치를 

## n+1문제

jpa를 사용하면서 연관관계가 있는 쿼리를 조회할시 발생하는 문제로 

JPA가 JPQL을 분석해서 SQL을 생성할 때는 글로벌 Fetch 전략을 참고하지 않고 오직 JPQL 자체만을 사용하기 때문에 발생한다.

## jsp

jsp의 httpservletrequest객체의 세션에다가 특정 servlet_id를 통해서 조회하는것이 아닌  해당 객체에서 계속 값을 넣었다 뺏다 하는방식으로 진행했음(트랜잭션처리가 없는 로컬 애플리케이션으로 설계했기때문)

## junit 

Exception관리 - checked, unchecked 두개의 차이는 컴파일과정에서 컴파일러가 체크하냐 안하냐의 차이이며, unchecked는 runtimeException을 상속받는다.

스프링 공식문서에는 checked는 트랜잭션 rollback이없고 unchecked는 롤백이있다고 되어있는데, 사실 이거는 개발자가 조정할수있는 부분이고 , 애플리케이션마다 다른부분이라 한마디로 속단할수없음.


## reflection

Reflection이란?

구체적인 클래스 타입을 알지 못해도 그 클래스의 메소드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API

런타임에 지금 실행되고 있는 클래스를 가져와서 실행해야하는 경우

동적으로 객체를 생성하고 메서드를 호출하는 방법

자바의 리플렉션은 클래스, 인터페이스, 메소드들을 찾을 수 있고, 객체를 생성하거나 변수를 변경하거나 메소드를 호출할 수 있다.


어떤 경우에 사용되나?

코드를 작성할 시점에는 어떤 타입의 클래스를 사용할지 모르지만, 런타임 시점에 지금 실행되고 있는 클래스를 가져와서 실행해야 하는 경우

프레임워크나 IDE에서 이런 동적인 바인딩을 이용한 기능을 제공한다. intelliJ의 자동완성 기능, 스프링의 어노테이션이 리플렉션을 이용한 기능이다.

## java8 

Lambda

stream

interface default method

Optional

new Date and Time API(LocalDateTime, …)

## java9

컬렉션 컬렉션에는 list, set, map을 쉽게 구성할 수 있는 몇 가지 추가 기능(list.of,map.of ... )

stream메서드 추가

try-with-resources 문 또는 다이아몬드 연산자(<>) 확장, HTTP클라이언트와 같은 몇 가지 다른 개선 사항 존재

## java10

가비지 컬렉션 등과 같은 Java 10에 몇 가지 변경 사항이 존재

개발자로서 보게 될 유일한 실제 변경 사항은 로컬 변수 유형 추론이라고도 하는 "var" 키워드의 도입

var 키워드
병렬 처리 가비지 컬렉션 도입으로 인한 성능 향상
JVM 힙 영역을 시스템 메모리가 아닌 다른 종류의 메모리에도 할당 가능


## java11

Oracle JDK와 OpenJDK 통합
Oracle JDK가 구독형 유료 모델로 전환
서드파티 JDK 로의 이전 필요
lambda 지역변수 사용법 변경
기타 추가

## java17

Pattern Matching for switch (Preview)
Sealed Classes (Finalized)
Foreign Function & Memory API (Incubator)
Deprecating the Security Manager

## DB

- 정규화

제1 정규형은 다음과 같은 규칙들을 만족해야 한다.

1. 각 컬럼이 하나의 속성만을 가져야 한다.
2. 하나의 컬럼은 같은 종류나 타입(type)의 값을 가져야 한다.
3. 각 컬럼이 유일한(unique) 이름을 가져야 한다.
4. 칼럼의 순서가 상관없어야 한다.

제2 정규형은 다음과 같은 규칙을 만족해야 한다.

1. 1정규형을 만족해야 한다.
2. 모든 컬럼이칼럼이 부분적 종속(Partial Dependency)이 없어야 한다. == 모든 칼럼이 완전 함수 종속을 만족해야 한다.

제3 정규형은 다음과 같은 규칙을 만족해야 한다.

1. 2 정규형을 만족해야 한다.
2. 기본키를 제외한 속성들 간의 이행 종속성 (Transitive Dependency)이 없어야 한다.

BCNF는 제 3정규형을 좀 더 강화한 버전으로 다음과 같은 규칙을 만족해야 한다.

1. 3정규형을 만족해야 한다.
2. 모든 결정자가 후보키 집합에 속해야 한다.


반정규화

정규화 단계를 떨어뜨림으로써 성능상 이점을 얻을수있는경우 시행한다.

테이블과 칼럼의 반정규화는 데이터 무결성에 영향을 미치게 되나 관계의 반정규화는 데이터 무결성을 깨뜨릴 위험을 갖지 않고서도 데이터처리의 성능을 향상시킬 수 있는 반정규화의 기법이 된다. 데이터 모델 전체가 관계로 연결되어 있고 관계가 서로 먼 친척간에 조인관계가 빈번하게 되어 성능저하가 예상이 된다면 관계의 반정규화를 통해 성능향상을 도모할 필요가 있다.


- 인덱스

b-tree : 이진탐색을 트리로 구현해서 탐색의 효율성을 높힌 자료구조이다. 클러스터링 인덱스가 보통 b-tree로 구현된다.

b+tree : btree구조에서 자료를 맨밑의 리프노드에만 저장하는 형태, 연결리스트로 선형으로 연결된다. 탐색속도가 빠르지만 최악의경우 btree보다 느리다

pk, unique설정시 자동으로 인덱스 생성된다.

index 조정시간으로 인해서 select제외 dml작업 속도 

- 격리레벨

- READ UNCOMMITTED

READ UNCOMMITTED 격리수준에서는 어떤 트랜잭션의 변경내용이 COMMIT이나 ROLLBACK과 상관없이 다른 트랜잭션에서 보여진다

데이터 정합성에 문제가 많으므로, RDBMS 표준에서는 격리수준으로 인정하지도 않는다.

- READ COMMITTED

어떤 트랜잭션의 변경 내용이 COMMIT 되어야만 다른 트랜잭션에서 조회할 수 있다.

오라클 DBMS에서 기본으로 사용하고 있고, 온라인 서비스에서 가장 많이 선택되는 격리수준이다.

NON-REPETABLE READ 부정합 문제가 발생할 수 있다.

- REPEATABLE READ

트랜잭션이 시작되기 전에 커밋된 내용에 대해서만 조회할 수 있는 격리수준

자신의 트랜잭션 번호보다 낮은 트랜잭션 번호에서 변경된(+커밋된) 것만 보게 되는 것이다

UPDATE 부정합 : 이전에 트랜잭션에서 커밋되지 않은 언두영역의 데이터의 경우는 쓰기잠금이 걸리지않고 따라서 언두영역의 데이터에 변경이 일어나면 문제가 발생한다.

팬텀 쿼리 : 한 트랜잭션 내에서 같은 쿼리를 두 번 실행했는데, 첫 번째 쿼리에서 없던 유령(Phantom) 레코드가 두 번째 쿼리에서 나타나는 현상

트랜잭션 내부에 트랜잭션으로 언두영역의 값에 접근할경우 발생하는 문제들이다.


- SERIALIZABLE

완전분리 즉 트랜잭션이 시작되면 다른 트랜잭션의 시작을 방지한다.

기존의 경우는 select문은 공유잠금이 없는대 읽기작업에도 공유잠금이 걸린다.

## Redis

redis vs memcached vs dynamoDB

Redis 싱글스레드이며 다양한 자료구조 지원 및 스냅샷(RDB)방식으로 인해서 서버 장애시 데이터보존, 확장에 매우 용이하다 , master-slave구조 지원 및 샤딩 지원

memcached 멀티스레드이며 메모리에만 데이터저장 서버 장애시 데이터 날라감

dynamoDB 관리가 매우 편리하고 매우빠르지만 마이너한 데이터베이스라 관련 라이브러리 지원이 없다 아직.

캐시만을 위한 자료구조를 원하는 것이라면 redis가 적합할것

mongoDB와 같은 영구저장형 nosql저장소를 원하는것이라면 dynamoDB를 선택할것



### 주소창에 www.google.co.kr을 검색하면 일어나는 일


1. 사용자가 웹브라우저 검색창에 www.google.com 입력
2. 웹브라우저는 캐싱된 DNS 기록들을 통해 해당 도메인주소와 대응하는 IP주소를 확인
이 단계에서 캐싱된 기록에 없을 경우, 다음단계로 넘어간다.

3. 웹브라우저가 HTTP를 사용하여 DNS에게 입력된 도메인 주소를 요청
4. DNS가 웹브라우저에게 찾는 사이트의 IP주소를 응답
ISP(Internet Service Provider)의 DNS서버가 호스팅하고 있는 서버의 IP주소를 찾기 위해 DNS query를 날린다.

DNS query의 목적
DNS 서버들을 검색해서 해당 사이트의 IP주소를 찾는데에 있다.
IP주소를 찾을 때 까지 DNS서버에서 다른 DNS서버를 오가며 에러가 날때까지 반복적으로 검색한다. = recursive search
DNS recursor(ISP의 DNS서버)는 name server들에게 물어물어 올바른 IP주소를 찾는데에 책임이 있다. name server는 도메인 이름 구조에 기반해서 주소를 검색하게 되는데, 예를 들어 설명해보자면,


'www.google.com' 주소에 대해 검색할 때,
1. DNS recursor가 root name server에 연락
2. .com 도메인 name server로 리다이렉트
3. google.com name server로 리다이렉트
4. 최종적으로 DNS기록에서 'www.google.com' 에 매칭되는 IP주소 찾기
5. 찾은 주소를 DNS recursor로 보내기
이 모든 요청들과 DNS recursor, IP주소는 작은 데이터 패킷을 통해 보내진다.
원하는 DNS기록을 가진 DNS서버에 도달할 때까지
클라이언트 ↔️ 서버를 여러번 오가는 과정을 거친다.

5. 웹브라우저가 웹서버에게 IP주소를 이용하여 html문서를 요청
TCP로 연결이 되면, 브라우저는 GET요청을 통해 서버에게 www.google.com의 웹페이지를 요구한다.

6. 웹어플리케이션서버(WAS)와 데이터베이스에서 우선 웹페이지 작업을 처리

7. 위의 작업처리 결과를 웹서버로 전송
8. 웹서버는 웹브라우저에게 html 문서결과를 응답
response는 status code로 서버 요청에 따른 상태를 보낸다.

9. 웹브라우저는 화면에 웹페이지 내용물 출력

## MSA

- 모놀리틱 아키텍쳐

Monolithic Architecture는 소프트웨어의 모든 구성요소가 한 프로젝트에 통합되어 있는 형태이다. 웹 개발을 예로 들면 웹 프로그램을 개발하기 위해 모듈별로 개발을 하고, 개발이 완료된 웹 어플리케이션을 하나의 결과물로 패키징하여 배포되는 형태를 말한다. 이런 어플리케이션을 모놀리식 어플리케이션이라 하며, 웹의 경우 WAR파일로 빌드되어 WAS에 배포하는 형태를 말한다. 주로 소규모 프로젝트에서 사용된다.

- 단점 

부분 장애가 전체 서비스의 장애로 확대될 수 있다. 

개발자의 잘못된 코드 배포 또는 갑작스런 트래픽 증가로 인해 성능에 문제가 생겼을 때, 서비스 전체의 장애로 확대될 수 있다.

부분적인 *Scale-out(여러 server로 나누어 일을 처리하는 방식)이 어렵다.

Monolithic Architecture에서는 사용되지 않는 다른 모든 서비스가 Scale-out되어야 하기 때문에 부분 Scale-out이 어렵다.

서비스의 변경이 어렵고, 수정 시 장애의 영향도 파악이 힘들다. 

여러 컴포넌트가 하나의 서비스에 강하게 결합되어 있기 때문에 수정에 대한 영향도 파악이 힘들다.

배포 시간이 오래 걸린다. 

최근 어플리케이션 개발 방법은 CI/CD를 통한 개발부터 배포까지 빠르게 반영하는 추세이다. 그러나 규모가 커짐에 따라 작은 변경에도 높은 수준의 테스트 비용이 발생하기도 하며, 많은 사람이 하나의 시스템을 개발하여 배포하기 때문에 영향을 줄 수 밖에 없다.

한 Framework와 언어에 종속적이다.

Spring framework를 사용할 경우, blockchain 연동 모듈을 추가할 때 node.js를 사용하는 것이 일반적이며 강세이다. 그러나 java를 이용하여 해당 모듈을 작성할 수 밖에 없다. 선정했던 framework가 Spring이기 때문이다.

이러한 Monolithic Architecture의 문제점들을 보완하기 위해 MSA가 등장하게 되었다. 기존의 특정한 물리적인 서버에 서비스를 올리던 on-promise 서버 기반의 Monolithic Architecture에서 이제는 클라우드 환경을 이용하여 서버를 구성하는 MicroService Architecture로 많은 서비스들이 전환되고 있다. 

- MSA

MSA는 API를 통해서만 상호작용할 수 있다. 즉, 마이크로 서비스는 서비스의 end-point(접근점)을 API 형태로 외부에 노출하고, 실질적인 세부 사항은 모두 추상화한다. 내부의 구현 로직, 아키텍처와 프로그래밍 언어, 데이터베이스, 품질 유지 체계와 같은 기술적인 사항들은 서비스 API에 의해 철저하게 가려진다. 

제대로 설계 된 마이크로서비스는 하나의 비즈니스 범위에 맞춰 만들어지므로 하나의 기능만 수행한다. 즉, 어플리케이션 출시처럼 하나의 목표를 향해 일하지만 자기가 개발하는 서비스만 책임진다. 그리고 여러 어플리케이션에서 재사용할 수 있어야 한다.

어플리케이션은 항상 기술 중립적 프로토콜을 사용해 통신하므로 서비스 구현 기술과는 무관하다. 따라서 마이크로서비스 기반의 어플리케이션을 다양한 언어와 기술로 구축할 수 있다는 것을 의미한다. 

마이크로서비스는 SOA에서 사용되는 집중화된 관리 체계를 사용하지 않는다. 마이크로서비스 구현체의 공통적인 특징 중 하나는 ESB(Enterprise Service Bus)와 같은 무거운 제품에 의존하지 않는다는 점이다. REST 등 가벼운 통신 아키텍처, 또는 Kafka 등을 이용한 message stream을 주로 사용한다. 

- MSA의 장점

각각의 서비스는 모듈화가 되어있으며 이러한 모듈까리는 RPC 또는 message-driven API등을 이용하여 통신한다. 

이러한 MSA는 각각 개별의 서비스 개발을 빠르게 하며, 유지보수도 쉽게할 수 있도록 한다. 

팀 단위로 적절한 수준에서 기술 스택을 다르게 가져갈 수 있다. 회사가 java의 spring 기반이라도 MSA를 적용하면 node.js로 블록체인 개발 모듈을 연동함에 무리가 없다. 

마이크로서비스는 서비스별로 독립적 배포가 가능하다. 따라서 지속적인 배포 CD도 모놀로식에 비해서 가볍게 할 수 있다.

마이크로서비스는 각각 서비스의 부하에 따라 개별적으로 scale-out이 가능하다. 메모리, CPU적으로 상당부분 이득이 된다.


- MSA의 단점

MSA는 모놀리식에 비해 상대적으로 많이 복잡하다. 서비스가 모두 분산되어 있기 때문에 개발자는 내부 시스템의 통신을 어떻게 가져가야 할지 정해야한다. 또한, 통신의 장애와 서버의 부하 등이 있을 경우 어떻게 transaction을 유지할지 결정하고 구현해야한다. 

모놀리식에서는 단일 트랜잭션을 유지하면 됐지만 MSA에서는 비즈니스에 대한 DB를 가지고 있는 서비스도 각기 다르고, 서비스의 연결을 위해서는 통신이 포함되기 때문에 트랜잭션을 유지하는게 어렵다. 

통합 테스트가 어렵다. 개발 환경과 실제 운영환경을 동일하게 가져가는 것이 쉽지 않다. 

실제 운영환경에 대해서 배포하는 것이 쉽지 않다. 마이크로서비스의 경우 서비스 1개를 재배포 한다고 하면 다른 서비스들과의 연계가 정상적으로 이루어지고 있는지도 확인해야한다. 
