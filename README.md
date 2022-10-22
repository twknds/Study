## Spring 프레임 워크의 어원

'스프링'이라는 이름의 유래는 이전에 Java EE(엔터프라이즈 에디션)의 스펙을 구현한 EJB가 기술의 복잡도가 증가해서 성능이 느렸던 것을 탈피하여, EJB 시절을 “겨울”에 빗대어 겨울 후의 “봄”으로 새로운 시작한다는 것을 의미하는 스프링(봄)이 되었다.

즉 개발자들에게 개발에만 집중할수잇는 환경을 제공하기 위한 프레임워크라고 할수있다.

스프링의 메인 3가지 기능

- IOC(Inversion Of Control)
- PSA(Potable Service Abstraction)
- AOP(Aspect Oriented Programming)

3가지는 비슷한 의미를 내포하고 있기도 하다.

## IOC : 제어의 역전

제어의 권한이 내가(Programmer) 아닌 프레임워크가 가진다는 뜻이며, 제어의 역전을 통해서 프레임워크가 객체를 알맞는 위치에 할당하고 개발자는 API를 사용하기만 하게 되었다.

EX) DI, IOC컨테이너

## PSA : 추상화 서비스

외부 라이브러리를 자바객체로 만들어 사용할수 있게 해주는 기능.

EX) Transaction Manager, @Controller, @Transactional 등등..

## AOP : 관점 지향 프로그래밍

핵심 비즈니스 로직외에 공통으로 개발되는 기능의 코드를 모아 개발을 편리하게 해준다.

1. 컴파일 이용방법
2. 바이트 코드 조작
3. 프록시 패턴

3가지 방법을 통해서 AOP를 구현할수 있고, Spring은 프록시 패턴을 통해서 AOP를 제공해준다.

EX) Aspect, Pointcut, JointPoint, Advice 외 Interface클래스

## Spring vs SpringBoot

SpringBoot는 Spring에서 내장 Tomcat이 추가되고 Dependency 자동화, Jar를 통한 배포, Spring Actuator를 이용한 모니터링과 관리, XML을 통한 설정이 필요없는점이다.


## JPA(Java Persistance API)
JPA는 ORM(Object Relation Mapper)의 한종류로써 자바 영속성 컨텍스트 명세 라는 뜻으로 풀이가 가능하다
ORM은 객체를 SQL문으로 변환해서 매핑해주는 매퍼로써 간단한 릴레이션을 만들기에는 쉬우나 릴레이션이 복잡해지면 상당한 숙련도를 요해서 러닝커브가 높은 기술중 하나이다.
요즘 추세는 Mybatis등의 다른 ORM과 섞어서 사용하는 추세이다.

JPA를 정의한 javax.persistence 패키지의 대부분은 interface , enum , Exception, 그리고  Annotation 들로 이루어져 있습니다.
JPA의 핵심이 되는 EntityManager 는 아래와 같이 javax.persistence 패키지 안에 interface 로 정의되어 있습니다.

```java

package javax.persistence; 
import ... 
public interface EntityManager {
  public void persist(Object entity);     
  public <T> T merge(T entity);     
  public void remove(Object entity);     
  public <T> T find(Class<T> entityClass, Object primaryKey);     
  // More interface methods...
}


```

해당양식처럼 EM은 interface로 구현되어있으며 PSA를 통해서 다양한 구현체와 사용될수 있다.

JPA를 사용하기 위해서는 JPA를 구현한 Hibernate, EclipseLink, DataNucleus 같은 ORM 프레임워크를 사용해야 합니다.
우리가 Hibernate를 많이 사용하는 이유는 가장 범용적으로 다양한 기능을 제공하기 때문입니다.

## hibernate

Hibernate는 JPA의 구현체 중 하나입니다.

Hibernate는 SQL을 사용하지 않고 직관적인 코드(메소드)를 사용해 데이터를 조작할 수 있습니다.

Hibernate가 SQL을 직접 사용하지 않는다고 해서 JDBC API를 사용하지 않는 것은 아닙니다.

Hibernate가 지원하는 메소드 내부에서는 JDBC API가 동작하고 있으며, 단지 개발자가 직접 SQL을 작성하지 않을 뿐 입니다.

JPA와 Hibernate는 마치 자바의 interface와 해당 interface를 구현한 class와 같은 관계입니다.

JPA의 핵심인 EntityManagerFactory , EntityManager , EntityTransaction 을 

Hibernate에서는 각각 SessionFactory , Session , Transaction 으로 상속받고 각각 Impl로 구현하고 있음을 확인할 수 있습니다.

## Hibernate의 장단점 

- 장점

생산성 : Hibernate는 SQL을 직접 사용하지 않고, 메소드 호출만으로 query가 수행된다.

즉, 반복적인 SQL 작업과 CRUD 작업을 직접 하지 않으므로 생산성이 매우 높아진다.

유지보수 : 테이블 컬럼이 변경되었을 경우, Mybatis에서는 관련 DAO의 파라미터, 결과, SQL 등을 모두 확인하여 수정해야 하지만

JPA는 JPA가 이런 일들을 대신 해주기 때문에 유지보수 측면에서 좋다.

객체지향적 개발 : 객체지향적으로 데이터를 관리할 수 있기 때문에 비즈니스 로직에 집중할 수 있다.

로직을 쿼리에 집중하기 보다 객체 자체에 집중할 수 있다.

특정 벤더에 종속적이지 않다.

여러 DB 벤더 (MySQL, ORACLE 등 . .)마다 SQL 사용이 조금씩 다르기 때문에 어플리케이션 개발 시 처음 선택한 DB를 나중에 바꾸는 것은 매우 어렵다.

하지만 JPA는 추상화된 데이터 접근 계층을 제공하기 때문에 특정 벤더에 종속적이지 않다.

설정 파일에서 JPA에게 어떤 DB를 사용하고 있는지 알려주기만 하면 얼마든지 DB를 변경할 수 있다.

- 단점

어렵다 : 많은 내용이 감싸져 있기 때문에 JPA를 잘 사용하기 위해서는 알아야 할 것이 많다.

잘 이해하고 사용하지 않으면 데이터 손실이 있을 수 있다.

성능 : 메소드 호출로 쿼리를 실행하는 것은 내부적으로 많은 동작이 있다는 것을 의미하므로, 직접 SQL을 호출하는것보다 성능이 떨어질 수 있다.

실제로 초기의 ORM은 쿼리가 제대로 수행되지 않았고, 성능도 좋지 못했다고 한다.

그러나 지금은 많이 발전하고 있고, 좋은 성능을 보여주고 있다.

세밀함이 떨어진다 : 메소드 호출로 SQL을 실행하기 때문에 세밀함이 떨어진다. 

또한 객체간의 매핑 (Entity Mapping)이 잘못되거나 JPA를 잘못 사용하여 의도하지 않은 동작을 할 수도 있다.

복잡한 통계 분석 쿼리를 메소드 호출로 처리하는 것은 힘들다.

이것을 보완하기 위해 JPA에서는 SQL과 유사한 기술인 JPQL을 지원한다.

SQL 자체 쿼리를 작성할 수 있도록 지원도 하고 있다.

## Spring Data JPA

Spring Data JPA는 Spring에서 제공하는 모듈 중 하나로 JPA를 쉽고 편하게 사용할 수 있도록 도와줍니다. 

기존에 JPA를 사용하려면 EntityManager를 주입받아 사용해야 하지만, 

Spring Data JPA는 JPA를 한단계 더 추상화 시킨 Repository 인터페이스를 제공합니다. 

Spring Data JPA가 JPA를 추상화 했다는 말은, Spring Data JPA의 Repository의 구현에서 JPA를 사용하고 있다는 것입니다. 

사용자가 Repository 인터페이스에 정해진 규칙대로 메소드를 입력하면,

Spring이 알아서 해당 메소드 이름에 적합한 쿼리를 날리는 구현체를 만들어서 Bean으로 등록해줍니다.
