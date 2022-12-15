<h1> JPA, Hibernate, Spring Data JPA </h1>

- JPA공부를 시작함에 있어서 가장헷갈렸던 부분이 JPA와 Hibernate와의 관계였다.
- 동영상강의에서는 처음에 EntityManager를 활용하여 Data를 삭제 저장 업데이트를 하지만, 실제 실무에서는 EntityManager를 사용하지 않고 Repository 인터페이스 만을 이용해서 JPA를 사용한다.

<h2> 🎈 JPA </h2>

<h4> 기술 명세 </h4>

- JPA(Java Persistence API)는 자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스이다.
- javax.persistance 단순히 인터페이스이며 구현체는 없다. EntityManager도 인터페이스이다.

<h2> 🎈 Hibernate </h2>

<h4> JPA의 구현체 </h4>

- Hibernate는 JPA 명세의 구현체이다. javax.persistence.EntityManager와 같은 JPA의 인터페이스를 직접 구현한 라이브러리이다.
- Hibernate는 아래의 JPA의 인터페이스를 상속받고 각각 Impl로 구현하고 있다.
  - JPA
  - EntityManagerFactory, EntityManager, EntityTransaction
  - Hibernate
  - SessionFactory, Session, Transcation

<h2> 🎈 Spring Data JPA </h2>

<h4> JPA를 쓰기 편하게 만들어놓은 모듈 </h4>

- 우리가 사용하는 Repository가 Spring Data JPA의 핵심이다.
- Spring Data JPA는 JPA를 한단계 더 추상화시킨 Repository라는 인터페이스를 제공한다.

아래블로그에 자세히 나와있어서 참고하면 좋을듯 하다.(조금 더 많이 살펴봐야겠다.) <br>
https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/

출처 : https://cornswrold.tistory.com/317 - JPA, Hibernate, Spring Data JPA 구분하기 (차이점)
