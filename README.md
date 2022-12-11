공부하다가 이건왜 ? 궁금한것을 기록하고 답변을 찾는 브랜치

## VM위에 VM을 띄울수는 없을까 ?? - 해결 : 가능!

https://osb330.tistory.com/5

가능하다 ! 하지만 이렇게 운영체제를 운영하게 되면 2중으로 싸인 운영체제는 하이퍼바이저를 2개 거쳐야 하기때문에 1개만 거쳐도 무거운 운영체제를 더무겁게 해서 매우 성능상 안좋다.

컨테이너는 운영체제 위에서 작동하며 호스트 OS와 커널을 공유하지만 VM은 자신만의 운영체제를 가지며(게스트 OS) 자체 커널을 가지고있다. 

## HTTPS 비대칭키?

비대칭키를 통해서 암호화 복호화를 할경우 서버측에서 정해놓은 공개키를 이용해서 클라이언트가 복호화를 진행하게 된다.

하지만 공개키는 만천하에 공개되어있고 , 서버의 데이터가 중간에 탈취당하거나 이상한 사람에게 간다면 이거 위험한거 아닌가 ?

그렇기 떄문에 존재하는것이 CA , CA에 서버는 공개키를 제공하고 CA로부터 공개키를 제공받은 클라이언트는 인증된 사용자이므로 결국 이상한사람은 공개키를 가질수 없다 !

하지만 매번 공개키로 암호화하고 개인키로 복호화 하고 반대로 수행하는것은 리소스 활용면에서 좋지않다 , 그렇기에 처음에 대칭키를 공개키로 복호화해서 서버로 전송하는 작업을 통해서 서버는 클라이언트와 대칭키를 공유하게 되고 이후 서버는 마음놓고 데이터를 전송해도 된다.

대칭키 방식으로 암복호화하며 데이터를 주고받는다면 안전하다.
다만 대칭키를 양쪽이 모두 안전하게 가지고 있는 상태에 도달하기 위해 비대칭키 방식이 필요하다.
서버의 공개키로 암호화해서 전송한다면 클라이언트의 전송은 안전하게 된다.
서버가 내 정보를 보내도 되는 신뢰할만한 사이트인지에 대해 확인하기 위해 CA 역할이 필요하다.
서버는 CA의 개인키로 암호화된 자신의 인증서를 응답해주고 브라우저는 이를 CA 공개키로 복호화한다.
복호화 결과로 나온 서버의 공개키로 대칭키를 암호화해서 전달한다.
이후로는 안전하게 대칭키로 데이터를 주고받는다.
