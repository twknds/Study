## OSI 7계층 Layer

- 특징

순서 : 송신은 7계층 -> 1계층, 수신은 1계층 -> 7계층 순으로 진행되고, 이 모델에 따라 각 단계별 프로토콜을 정의한다.

계층의 독립 : 어떤 계층의 변화가 다른 계층에 영향을 주지 않는다.

상위 > 하위 : 기본적으로 하위 계층은 상위 계층을 위해 기능하고, 상위 계층은 하위 계층에 관여하지 않는다.

- 물리 계층(physical Layer)

물리 계층에서는 주로 전기적, 기계적, 기능적인 특성을 이용하여 통신 케이블로 데이터를 전송한다.

사용되는 통신 단위는 비트이며 이것은 1과 0으로 나타내어진다.

단지 데이터를 전기적인 신호로만 변환해서 주고받는 기능만 한다.

장비로는 "통신 케이블", "리피터", "허브"가 있다.

데이터 전송만 하고 어떤 에러가 있는지 신경 쓰지 않는다.

정리 : "통신 케이블", "리피터", "허브"등을 통해 데이터 전송.

- 데이터 링크 계층(DataLink Layer)

물리계층을 통해 송수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행할 수 있도록 도와주는 역할을 한다.

통신에서의 오류도 찾아주고 재전송도 하는 기능을 가지고 있는 것이다.

MAC 주소를 가지고 통신하게 된다.

MAC 주소란? : 네트워크 세그먼트의 데이터 링크 계층에서 통신을 위한 네트워크 인터페이스에 할당된 고유 식별자이다.

물리 주소 ex)wifi 주소,라 생각하면 된다.

이 계층에서 데이터 전송되는 단위를 프레임(frame) 이라 한다.

장비로는 "브리지", "스위치"가 있다.

물리 계층에서 발생할 수 있는 오류를 찾아 내고, 수정하는데 필요한 기능적, 절차적 수단을 제공한다.

정리 : 프레임에 MAC주소를 부여 하고 에러검출,재전송,흐름제어를 한다.

- 네트워크 계층(Network Layer)

이 계층에서 가장 중요한 기능은 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능(라우팅)이다.

여기에 사용되는 프로토콜의 종류도 다양하고, 라우팅하는 기술도 다양하다.

이 계층은 경로를 선택하고 주소를 정하고 경로에 따라 패킷을 전달해주는 것이 이 계층의 역할이다.

장비로는 대표적으로 "라우터(router)" 이다.

네트워크 계층(Network layer)은 여러개의 노드를 거칠때마다 경로를 찾아주는 역할을 하는 계층이다.

그럼 네트워크 계층에서는 무슨일을 할까??

라우팅, 흐름 제어, 세그멘테이션, 오류 제어, Internetworking 등을 수행한다.

데이터를 연결하는 다른 네트워크를 통해 전달함으로써 인터넷이 가능하게 한다.

IP(논리적인 주소 구조)를 할당해 주는 역할

정리 : IP주소를 부여하고 경로(route)를 설정해 준다.

- 전송 계층(Transport Layer)

통신을 활성화하기 위한 계층이다. 보통 TCP프로토콜을 이용하며, 포트를 열어서 응용프로그램들이 전송을 할 수 있게 한다.

만약 데이터가 왔다면 4계층에서 해당 데이터를 하나로 합쳐서 5계층에 던져 준다.

단대단 오류제어 및 흐름제어 이 계층 까지는 물리적인 계층에 속한다.

TCP / UDP프로토콜을 사용한다.

전송 계층(Transport layer)은 양 끝단(End to end)의 사용자들이 신뢰성있는 데이터를 주고 받을 수 있도록 해 주어, 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해

준다.

시퀀스 넘버 기반의 오류 제어 방식을 사용한다.

시퀀스 넘버 기반?

시퀀스 넘버 : 통신과 제어에서 데이터를 관리하기 위해 번호를 부여한다.(대표적인 전송 계층인 TCP로 예를 들면, TCP 패킷 헤더에 Sequence & Ack number라는 걸 채운다)

사용 이유 : 해당 번호는 순서 역전 방지, 중복 패킷 방지 등을 이유로 사용한다.

즉, 데이터를 패킷 단위로 나눠서 전송하는데, 이것들이 섞이거나 중복되지 않게 잘 전송될 수 있도록 한다.

전송 계층은 특정 연결의 유효성을 제어하고, 일부 프로토콜은 상태 개념이 있고(stateful) 연결 기반(connection oriented)이다.

패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송한다는 것을 뜻한다.

종단간(end-to-end) 통신을 다루는 최하위 계층으로 종단간 신뢰성 있고 효율적인 데이터를 전송하며, 기능은 오류검출 및 복구와 흐름제어, 중복검사 등을 수행한다.

정리 : 패킷 생성(Assembly/Sequencing/Deassembly/Error detection/Request repeat/Flow control) 및 전송을 한다.

- 세션 계층(Session Layer)

데이터가 통신하기 위한 논리적인 연결을 의미한다.

양 끝단의 프로세스가 데이터 통신(송수신)을 관리하기 위한 방법을 제시하는 계층이다.

동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full duplex)의 통신과 함께, 체크 포인트의 유무, 종료, 다시 시작 과정 등을 수행한다.

TCP/IP 세션을 만들고 없애는 책임을 진다.

정리 : 통신하는 사용자들을 동기화하고 오류복구 명령들을 일괄적으로 다루고 통신을 하기 위한 세션을 확립/유지/중단 (운영체제가 해준다.)

- 표현 계층(Presentation Layer)

데이터 표현이 상이한 응용 프로세스의 독립성을 제공하고, 암호화 한다.

코드 간의 번역을 담당하여 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어 준다. MIME 인코딩이나 암호화 등의 동작이 이 계층에서 이루어진다.

ex) EBCDIC로 인코딩된 문서 파일을 ASCII로 인코딩된 파일로 바꿔 준다.

해당 데이터가 TEXT인지, 그림인지, GIF인지 JPG인지의 구분 해주기도 한다.

정리 : 사용자의 명령어를 완성및 결과 표현. 포장/압축/암호화

- 응용 계층(Application Layer)

사용자가 보는 소프트웨어의 UI, 네트워크 서비스, 사용자의 입출력 부분 등을 담당하는 계층이다.

HTTP, FTP, SMTP, POP3, IMAP, Telnet 등과 같은 프로토콜이 있다.

해당 통신 패킷들은 방금 나열한 프로토콜에 의해 모두 처리되며 우리가 사용하는 브라우저나, 메일 프로그램은 프로토콜을 보다 쉽게 사용하게 해주는 응용프로그램이다.

즉, 모든 통신의 양 끝단은 HTTP와 같은 프로토콜이지 응용프로그램이 아니다.

응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다.

일반적인 응용 서비스는 관련된 응용 프로세스들 사이의 전환을 제공한다.

응용 서비스의 경우 JVM, Terminal등이 있다.

정리 : 네트워크 소프트웨어 UI 부분, 사용자의 입출력(I/O)부분

## HTTP 프로토콜이란?

HTTP 프로토콜이란 인터넷 상에서 데이터를 주고 받기위한 상호간의 규칙을 정의하고 특정 기간내에 데이터를 송수신을 할 수 있는 규약이라고 보면 된다.

웹상에서는 서버와 클라이언트가 서로 데이터를 주고 받기위한 방식으로 Http프로토콜을 사용하고 있다.

Http는 어떤 종류의 데이터 이든지 전송 할 수 있다.

OSI 7계층중 응용계층 프로토콜이며 TCP/IP위에서 작동하도록 되어있다.

일반적으로 포트번호 80을 가진다.

## Http Request 구조

POST /user/create HTTP/1.1

Host: localhost:8080
Connection: keep-alive
Content-Length: 57
Cache-Control: max-age=0
Origin: http://localhost:8080
Upgrade-Insecure-Requests: 1

userId=test&password=1234&name=testName&email=test%40test.com

- Request StartLine

Request가 올 때 요청의 시작줄 이다.

Method Path Version 형식으로 온다.

- Method 종류

GET: 요청받은 URI의 정보를 검색하여 응답

POST: 요청된 자원을 생성, 보통 Response에 Location 필드를 넣고 응답

PUT: 요청된 자원을 수정, Location을 포함시키지 않고 주로 클라이언트가 요청한 URI 주소를 포함하여 응답 * DELETE: 요청된 자원을 삭제할 것을 요청

HEAD: GET방식과 동일하지만, 응답에 BODY가 없고 응답코드와 HEAD만 응답

OPTIONS: 메소드의 종류를 확인할 경우 사용

TRACE: 원격지 서버에 루프백 메시지 호출하기 위해 테스트용으로 사용

Path : HTTP 요청 주소이다.

Version : HTTP Version이다.

보통 요청 Version을 통해 응답 Version을 맞춘다.)

버전은 0.9/1.0/1.1/2.0이 있다.

- Request Header

Request의 요청 정보를 담고있는 부분이다.

Key-Value 형식으로 되어 있다.

Connectionless, Stateless

Http는 클라이언트가 요청을 보내면 연결을 끊어 버리는 특징을 가지고 있다.(Connectionless)

따라서 Header에 keep-alive라는 속성을 줘서 재활용 한다.

stateless는 통신이 끝나면 상태를 유지하지 않는 특징이다.

연결을 끊는 순간 클라이언트와 서버의 통신이 끝나며 상태 정보는 유지하지 않는 특성을 가지고 있다.

이 두가지를 해결하기 위해서 쿠키와 세션을 사용한다.

- Request Body

Request의 요청할 데이터를 담고 있는 부분이다.

전송하는 데이터가 없으면 Body부분은 비어있다.

- Http Response

HTTP/1.1 200 OK

Content-Type: text/html; charset=UTF-8
Content-Length: 6097

<!DOCTYPE html...
Response Status

Http Response의 응답 상태를 나타내주는 부분이다.

Version StatusCode Status로 구성 되어 있다.

대표적인 상태 코드 및 텍스트

200 Ok : 요청이 성공적으로 수행

302 Found : 요청을 리다이렉션으로 수행 (Location을 사용)

403 Forbidden : 요청한 페이지가 접근 금지 및 차단

404 Not Found : 요청한 페이지가 없음

500 Internal Server Error : 내부 서버 오류

- Response Header

Http Request 헤더와 동일

Response 헤더가 따로 있음 (참고 사이트 확인)

- Response Body

Http Request Body와 동일

전송하는 데이터가 없으면 Body부분은 비어있음

용도에 따라 html코드나 Json등 데이터를 내보냄

## HTTP(HyperText Transfer Protocol)

웹 상에서 웹 서버 및 웹브라우저 상호 간의 데이터 전송을 위한 응용계층 프로토콜이다.

처음에는, WWW 상의 하이퍼텍스트 형태의 문서를 전달하는데 주로 이용 되었고

현재에는, 이미지,비디오,음성 등 거의 모든 형식의 데이터 전송이 가능하다.

- 특징

요청과 응답 구조

동작 형태는 클라이언트 / 서버 로 동작한다.

메세지 교환 형태의 프로토콜

클라이언트와 서버 간에 HTTP 메세지를 주고받으며 통신 [SMTP 전자메일 프로토콜과 유사하다.]

- 트랜잭션 중심의 비연결성 프로토콜

종단간 연결이 없음 (Connectionless)

이전의 상태를 유지하지 않음 (Stateless)

전송 계층 프로토콜 : TCP, 포트 번호 : 80

** HTTP 와 HTTPS의 차이❓

HTTPS의 S는 Secure약자 이다. 일반적으로 HTTP 프로토콜의 문제점은 서버로부터 브라우저로 전송되는 정보가 암호화 되지 않는다. 이 말은 쉽게 정보가 노출될 수 있다는 의미이다.

HTTPS 프로토콜은 SSL(보안 소켓 계층)을 사용함으로써 보안을 유지할 수 있게 되었다.

- SSL 이란?

SSL(Secure Sockets Layer)은 인터넷으로 전송된 데이터의 인증, 암호화, 암호 해독을 가능하게 하는 웹브라우저와 서버의 프로토콜.

SSL 인증서 서버를 사용자에게 인증하고 서버와 사용자 간 전송된 데이터를 암호화 할 수 있게 하는 서버 인증서를 의미한다.

## URL(Uniform Resource Locator)

URL은 네트워크 상에서 자원이 어디 있는지를 알려주기 위한 규약이다.

즉, 컴퓨터 네트워크와 검색 메커니즘에서의 위치를 지정하는, 웹 리소스에 대한 참조를 의미한다.

다시말하면, URL은 자원에 목적지를 알려준다.

- 통신방법

사용할 프로토콜을 말하며, 리소스를 어떻게 요청, 접근할 것인지를 명시한다.

웹에서 주로 HTTP프로토콜을 사용한다.

ftp, mailto(이메일), rtsp(스트리밍)과 같은 프로토콜을 사용할 수도 있다.

사용자 ID과 비밀번호

어떤 서버들은 자신이 가지고 있는 데이터에 접근하기 위해서 사용자의 이름과 비밀번호를 요구합니다.

ex) ftp://victolee:12345@호스트/asd.xls

만약 웹 서버에서 사용자이름과 비밀번호를 요구하는 URL 스킴을 사용함에도 클라이언트가 이를 명시하지 않고 URL에 접근한다면, 기본값으로 "사용자 이름 : anonumous , 비밀번호는 브라우저

에서 제공하는 기본 값"을 따르게 된다.

- 주소와 포트

서버에는 포트에 따라 소켓이 연결되어 있고, 포트 번호에 따라 다른 프로토콜이 사용될 수 있습니다.

HTTP 프로토콜에서 포트 번호를 명시하지 않으면, 80번 포트를 기본 값으로 가진다.

경로

호스트에서 제공하는 자원의 경로를 의미합니다.

질의(추가정보)

Query String( 쿼리 스트링 )이라고도 합니다.

클라이언트가 자원을 GET 방식으로 요청할 때, 필요한 데이터를 함께 넘겨 줄 목적으로 사용합니다.

ex) http://localhost:3000/index?id=3&page=1 와 같이 id값 & page값

프래그먼트

HTML에는 각각의 요소에 id 속성을 부여할 수 있는데요, URL에 프래그먼트를 전달하면 페이지가 해당 id가 있는 곳으로 스크롤이 이동한다.

#bottom 을 붙이는 경우 페이지의 가장 마지막으로 이동한다.

## TCP/IP

TCP/IP란

데이터가 의도된 목적지에 닿을 수 있도록 보장해주는 통신 규약이다.

TCP와 IP 두가지의 프로토콜로 이루어져 있다.

 TCP(Transmission Control Protocol)

두 호스트가 교환하는 데이터와 승인 메세지의 형식을 정의하여, 서버와 클라이언트간의 데이터를 신뢰성있게 전달하기 위해 만들어진 규약이다.

- TCP 특징

TCP는 데이터 패킷에 일련의 번호를 부여함으로써, 데이터 손실을 찾아내서 교정하고, 순서를 재조합하여 클라이언트에게 전달할 수 있게 해준다.

TCP는 복잡해서 신뢰성이 높다는 장점이 있다.

정리 : 신뢰성이 있고 연결 지향적이다.



- IP(Internet Protocol)

컴퓨터와 컴퓨터간에 데이터를 전송하기 위해서, 각 컴퓨터의 주소가 필요하다. Internet Protocol은 4바이트로 이루어진 컴퓨터의 주소이며, 192.168.9.255와 같이 3개의 마침표로 나뉘어진 

숫자로 표시된다.



IP 주소는 32비트로 구성되어 있는데 이걸 4등분 하여서 8비트 씩 4개로 쪼개었다.

8비트는 2^8승으로 0~255까지 수를 갖게 되고 , 우리가 흔히 아는 192.168.0.0와 같이 최대 255.255.255.255을 넘지 않는다.

IP는 TCP와는 달리 데이터의 재조합이나 손실여부 확인이 불가능하며, 단지 데이터를 전달하는 역할만을 담당한다.

IP주소는 하드웨어 고유의 식별번호인 MAC주소와 다르게 임시적으로 다른 주체(통신사)에게 받는 주소이므로, 바뀔수 있다.

- TCP/IP 특징

IP기반에 TCP가 사용되어 TCP/IP라 한다.

TCP가 데이터의 추적을, IP가 배달을 처리한다.

사용되는 곳

EMAIL(SMTP), HTTP, HTTPS, FTP, TELNET 등 우리에게 친숙한 인터넷 서비스의 대부분이 TCP/IP기반으로 동작한다.

- UDP 와 TCP 차이

TCP,UDP란 전송 계층에서 사용하는 프로토콜로 목적지 장비까지 전송한 패킷을 상위의 특정 응용 프로토콜에게 전달하는 것에 목적을 가진 전송 방식을 의미한다.



## UDP(User Datagram Protocol)

비연결형 서비스를 지원하는 전송계층 프로토콜로써, 인터넷상에서 서로 정보를 주고받을 때 정보를 보낸다는 신호나 받는다는 신호 절차를 거치지 않고,보내는 쪽에서 일방적으로 데이터를 전달

하는 통신 프로토콜이다.

- UDP 특징

데이터를 데이터그램 단위로 처리하는 프로토콜입니다.

데이터그램 : 독립적인 관계를 지니는 패킷이라는 뜻

신뢰성이 낮은 프로토콜로써 완전성을 보증하지 않는다

가상회선을 굳이 확립할 필요가 없고 유연하며 효율적 응용의 데이터 전송에 사용

일방적인 데이터 전달(중간에 신호절차를 거치지 않는다.)

순서제어,흐름제어,오류제어등 없다고 생각하면 된다.

비연결접속상태 하에서 통신한다.

실시간 응용 및 멀티캐스팅 가능

빠른 요청과 응답이 필요한 실시간 응용에 적합, 1:多에 적합하다.

헤더가 단순하다.

헤더의 고정크기가 8바이트만 사용하여 헤더처리에 많은 시간을 쓰지 않는다.

[TCP는 헤더에 20바이트 사용]

신뢰성보다는 연속성이 중요한 서비스의 예를 들면 실시간 서비스(streaming)에 자주 사용됩니다.

- TCP 와 UDP 차이점

정리 : TCP는 연속성보다 신뢰성있는 전송이 중요할 때에 사용하는 프로토콜이며,

UDP는 TCP보다 속도가 빠르며 네트워크 부하가 적다는 장점이 있지만, 신뢰성있는 데이터 전송을 보장하지는 않는다.

## SSH(Secure Shell)

SSH, Secure Shell은 인터넷 또는 네트워크 내에서 두 원격 호스트간에 보안 연결을 설정하는 데 사용되는 네트워크 프로토콜이다.

SSH는 암호화 된 형식을 사용하여 컴퓨터간에 데이터를 전송하므로 이 암호화 된 메커니즘은 교환되는 데이터의 기밀성과 무결성을 제공한다.

사용자 이름, 비밀번호등 기밀 데이터를 모두 암호화 된 형식으로 되어 있다.

원격 로그인 시스템 및 원격 명령 실행이 가능하다. (보안에 강함)

- 공통점과 차이점

**공통점

사용자가 원격 시스템에 로그인하여 명령을 실행할 수 있도록하는 네트워크 프로토콜.

둘 다 터미널 에뮬레이터로 분류된다.

**차이점

각 프로토콜의 보안 조치에 차이점이 있다.

Telnet은 보안 수준이 낮아 디버깅이나 테스트 용도에만 사용된다.

SSH는 높은 보안 성을 제공하기 때문에 원격 로그인 시스템 및 원격 명령 실행에 사용된다.

## DNS(Domain Name System)

호스트의 도메인 이름을 호스트의 네트워크 주소로 바꾸거나 그 반대의 변환을 수행하는 시스템이다.

- DNS 동작 원리

예시로 컴퓨터에서 크롬을 켜고 www.google.com 을 입력한다.

컴퓨터는 컴퓨터 내부에 등록 되어 있는 DNS 서버로 www.google.com에 해당되는 IP 주소를 물어보고

DNS 서버는 해당 도메인(구글 주소)의 IP를 알려준다.

컴퓨터는 이를 받아서 IP 주소에 해당하는 컴퓨터에 접속하게 되는 것이다.

## CORS (Cross Origin Resource Sharing)

CORS 정책은 우리가 가져오는 리소스들이 안전한지 검사하는 관문이다.

웹개발을 하는 사람들은 이 CORS 정책위반으로 인해 에러가 나는 상황을 많이들 겪어봤을것이라고 생각 된다.

- HTML → 기본적으로 Cross-Origin 정책을 따름

link 태그의 href에서 다른 origin의 css 등의 리소스에 접근하는 것이 가능

img 태그의 src에서 다른 리소스에 접근하는 것이 가능


- XMLHttpRequest, Fetch API 등 script 태그 내 → 기본적으로 Same-Origin 정책을 따름

자바스크립트는 서로 다른 도메인에 대한 요청을 보안상 제한한다. (브라우저 기본 설정은 하나의 서버 연결만 허용)

이 정책을 Same-Origin-Policy라고 한다.

## 출처 (Origin) 이란?

다른 출처간의 리소스 공유에 대해서 알아보기 전에 출처가 무엇을 의미하는지 이해할 필요가 있다. 

서버의 위치를 의미하는 https://google.comVisit Website 과 같은 URL은 하나의 문자열 같지만 다음과 같이 구성되어 있다.

-> 출처(Origin)는 Protolcol 과 Host 그리고 Port까지 모두 합친 것을 의미한다. 자바스크립트로 Location 객체가 가지고 있는 origin 프로퍼티에 접근하여 현재 출처를 알아낼 수도 있다.

이때 출처는 Protocol과 Host, 그리고 위 그림에는 나와있지 않지만 :80, :443과 같은 포트 번호까지 모두 합친 것을 의미한다. 즉, 서버의 위치를 찾아가기 위해 필요한 가장 기본적인 것들을 합쳐놓은 것이다.

또한 출처 내의 포트 번호는 생략이 가능한데, 이는 각 웹에서 사용하는 HTTP, HTTPS 프로토콜의 기본 포트 번호가 정해져있기 때문이다. HTTP가 정의된 RFC 2616 문서를 보면 다음과 같이 기본 포트 번호가 함께 정의되어있는 것을 볼 수 있다.

## Same Origin / Cross Origin 차이

웹에는 크게 SOP(Same Origin Policy)와 CORS(Cross Origin Resurce Sharing) 두가지 정책이 있다.
 
SOP - 동일 출처 정책

SOP는 "같은 출처에서만 리소스를 공유할 수 있다"라는 규칙을 가진 정책이다.
 
- Same Origin 기준 (출처 비교)

두개의 출처를 비교하는 방법은 URL의 구성요소 중 Protocol, Host, Port 이 세가지가 동일한지 확인하면 된다.

즉 같은 프로토콜, 호스트, 포트를 사용한다면 다른 요소는 다르더라도 같은 출처로 인정된다. 반대로 리소스가 자신의 출처와 다를경우 브라우저는 교차출처 요청을 실행한다.
 
출처를 비교하는 로직은 서버에 구현된 스펙이 아닌 브라우저에 구현된 스펙이다.

만약 CORS정책을 위반하는 요청에 서버가 정상적으로 응답을 하더라도 브라우저가 이 응답을 분석해서 CORS정책에 위반되면 그 응답은 처리하지 않게 된다.
 
정리하자하면 프로토콜, 포트, 호스트 모두 일치해야 Same Origin이며, 이들중 하나라도 일치하지 않으면 Cross Origin 이 된다.

**internet Explorer는 Origin비교시 포트를 무시한다. -> 보안 취약

**보통 프론트엔드 개발자가 React와 같은 라이브러리를 사용해서 개발하는 경우 백엔드 서버와 별도의 프론트 서버가 존재한다. 
프론트 개발을 할때, 로컬의 백엔드 서버에 연동하거나 개발 서버에 연결해서 API 연동을 하는데 만일 다음과 같이,프론트 서버의 URL이 http://localhost:3000이고, 백엔드 서버가 http://localhost:8080에 띄워져 있다고 하면이때 프론트 서버와 백엔드 서버는 다른 출처 (Origin)으로써 Same-Origin Policy 정책을 어긋나기 때문에, 서버로부터 응답이 넘어올 때 브라우저에서 CORS Policy 오류를 발생시키게 된다.

## CORS - 교차 출처 리소스 공유

교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)는, 추가 HTTP 헤더를 사용하여 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 

부여하도록 브라우저에 알려주는 체제다.
 
즉, 위에서 시뻘겋게 CORS 어쩌구 에러는 CORS를 허용해서 아무런 탈 없이 다른 출처 리소스 공유를 해달라는 권고 사항 같은 것이라 볼 수 있다.
 
웹 애플리케이션은 리소스가 자신의 출처(도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행하게 된다.

**"교차 출처"는 "다른 출처"라고 표현하는게 좀 더 쉽게 이해할 수 있다.

CORS 기본 동작과정
 
1. 클라이언트에서 HTTP요청의 헤더에 Origin을 담아 전달한다.

다른 Origin의 리소스 요청시 클라이언트는 HTTP요청을 보낸다. 이때 요청헤더의 Origin필드에는 요청을 보내는 Origin을 담아보낸다. 

2. 서버는 응답헤더에 Access-Control-Allow-Origin을 담아 클라이언트로 전달한다.

서버가 응답을 보낼때, 허락하는 Origin을 클라이언트에게 전달한다.

3. 클라이언트에서, 자신이 보냈던 요청의 Origin과 서버가 보내준 Access-Control-Allow-Origin을 비교한다.

자신이 보낸 Origin과 서버가 보내준 Access-Control-Allow-Origin을 비교하여 차단할지 말지를 결정한다.

만약 유효하지 않다면 그 응답을 사용하지 않고 버린다. (위의 경우에는 둘다 http://localhost:3000이기 때문에 유효한 경우이다.)

**서버 응답은 CORS정책 위반 여부에 관여하지 않는다.CORS 정책에 의해 Origin을 비교하는 로직은 브라우저에 구현되어 있다.
그래서 서버에서 정상적인 응답을 하여 상태코드가 200이 나오더라도, 브라우저가 응답을 CORS정책 위반이라고 분석하면 그 응답은 사용하지 않는다. 
브라우저가 CORS정책 위반을 분석하는 시간은 서버의 응답이 도착한 이후이다.
즉, CORS정책을 위반하는 리소스 요청때문에 에러가 발생하더라도 서버 쪽 로그에서는 정상응답을 했다는 로그만 남기때문에, CORS를 정확히 이해해야만 CORS에러를 해결할 수 있는것이다.


