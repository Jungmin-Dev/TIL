<h1> JPA </h1>

- JPA(Java Persistence API)는 자바 진영의 ORM 기술 표준

- JPA가 제공하는 API를 사용하면 객체를 DB에 저장하고 관리할 때, 개발자가 직접 SQL을 작성하지 않아도 된다.
- JPA가 개발자 대신 적절한 SQL을 생성해서 DB에 전달하고, 객체를 자동으로 Mapping 해준다.
- JPA는 내부적으로 JDBC API를 활용하는데, 개발자가 직접 JDBC API를 활용하면 패러다임 불일치, SQL 의존성 등으로 인해 효율성이 떨어진다.
- 이 때, JPA를 활용한다면 모든 SQL에 대해 개발자 대신 JPA가 자동으로 해결해 준다는 점에서 생산성을 크게 높인다.

<h3> ORM </h3>

- ORM(Object-Relational Mapping)은 객체와 관계형 DB를 매핑한다는 뜻
- ORM 프레임워크를 사용하면 객체를 마치 자바 컬렉션에 저장하듯 저장할 수 있고, 이에 대해 ORM 프레임워크가 적절한 SQL을 생성해서 DB에 객체를 저장해준다.

<h3> Hibernate </h3>

- 자바 진영의 다양한 ORM 프레임워크 중 가장 많이 사용되는 성숙한 프레임워크

- 이러한 Hibernate 기반으로 만들어진 ORM 기술 표준이 바로 JPA다.
- 즉, JPA라는 ORM 기술 표준을 구현한 것이 Hibernate이므로, JPA를 사용하려면 Hibernate를 사용하면 된다.

![image](https://user-images.githubusercontent.com/74536458/207317078-ebf9bb49-4a37-4876-bdda-d7031d128eeb.png)

> 👍🏼 이를 통해, 개발자는 관계형 DB를 사용해도 객체지향 어플리케이션 개발에 집중할 수 있게 된다.

<h3> 사용 이유 </h3>

<h3> 1) 생산성 </h3>

- 자바 컬렉션에 객체를 저장하듯이 JPA에게 저장할 객체만 전달하면 JPA가 대신 처리해준다.

```java
jpa.persist(member); // 저장
Member member = jpa.find(memberId); // 조회
```
- 반복적인 코드와 CRUD용 SQL을 개발자가 직접 작성하지 않아도 된다.
- CREATE TABLE과 같은 DDL 문을 자동으로 생성해줄 수 있다.
 
<h3> 2) 유지보수 </h3>

- SQL을 직접 다루면 엔티티에 필드를 하나만 추가해도 그에 해당하는 SQL과 결과를 매핑하기위한 JDBC API 코드를 모두 변경해야한다. JPA를 사용하면 이런 과정을 JPA가 대신 해준다. 
- JPA가 패러다임의 불일치 문제를 해결해주므로 객체지향 언어가 가진 장점들을 활용해서 유연하고 유지보수하기 좋은 도메인 모델을 편리하게 설계할 수 있다.
 
<h3> 3) 성능 </h3>

- JPA는 애플리케이션과 데이터베이스 사이에서 동작하므로 최적화 관점에서 시도해볼 수 있는 것들이 많다.

```java
String memberId = "test"

Member member1 = jpa.find(memberId); // 조회
Member member2 = jpa.find(memberId); // 조회
```
- 같은 회원을 두번 조회하는 코드다. 

- JPA를 사용하지 않았을땐 두번의 SELECT 쿼리가 수행되지만 JPA를 사용하면 한번만 SELECT 쿼리가 수행되고, 그 다음은 이미 조회한 회원 객체를 재사용한다.


<h3> 데이터 접근 추상화와 벤더 독립성 </h3>

- JPA는 애플리케이션과 데이터베이스 사이에 추상화된 데이터 접근 계층을 제공해서 애플리케이션이 특정 데이터베이스 기술에 종속되지 않도록 한다. 
- 데이터 베이스 변경도 유연하게 처리가 가능하다. JPA에게 다른 데이터베이스를 사용한다고 알려주기만 하면 된다.



출처 : https://velog.io/@jwkim/JPA-JPA%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80 - [JPA] JPA란 무엇인가? <br>
출처 : https://devfunny.tistory.com/813 - [JPA 프로그래밍] 1. JPA 란 무엇인가?
