***Spring 프레임 워크의 어원***

'스프링'이라는 이름의 유래는 이전에 Java EE(엔터프라이즈 에디션)의 스펙을 구현한 EJB가 기술의 복잡도가 증가해서 성능이 느렸던 것을 탈피하여, EJB 시절을 “겨울”에 빗대어 겨울 후의 “봄”으로 새로운 시작한다는 것을 의미하는 스프링(봄)이 되었다.

즉 개발자들에게 개발에만 집중할수잇는 환경을 제공하기 위한 프레임워크라고 할수있다.

스프링의 메인 3가지 기능

- IOC(Inversion Of Control)
- PSA(Potable Service Abstraction)
- AOP(Aspect Oriented Programming)

3가지는 비슷한 의미를 내포하고 있기도 하다.

**IOC : 제어의 역전

제어의 권한이 내가(Programmer) 아닌 프레임워크가 가진다는 뜻이며, 제어의 역전을 통해서 프레임워크가 객체를 알맞는 위치에 할당하고 개발자는 API를 사용하기만 하게 되었다.

EX) DI, IOC컨테이너

##PSA : 추상화 서비스

외부 라이브러리를 자바객체로 만들어 사용할수 있게 해주는 기능.

EX) Transaction Manager, @Controller, @Transactional 등등..

**AOP : 관점 지향 프로그래밍

핵심 비즈니스 로직외에 공통으로 개발되는 기능의 코드를 모아 개발을 편리하게 해준다.

1. 컴파일 이용방법
2. 바이트 코드 조작
3. 프록시 패턴

3가지 방법을 통해서 AOP를 구현할수 있고, Spring은 프록시 패턴을 통해서 AOP를 제공해준다.
EX) Aspect, Pointcut, JointPoint, Advice 외 Interface클래스

