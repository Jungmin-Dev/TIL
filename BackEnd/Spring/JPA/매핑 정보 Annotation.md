<h1> 매핑 정보 Annotation </h1>

> javax.persistence: JPA Annotation 패키지

<h3> 가장 기본이 되는 Annotation </h3>

<h4> @Entity </h4>

- 엔티티 클래스
- 클래스를 테이블과 매핑

<h4> @Table </h4>

- 매핑할 테이블 정보
- name 속성에 테이블 이름 명시 (ex. @Table(name="MEMBER"))
- 생략할 경우 엔티티 클래스 이름으로 매핑

<h4> @Id </h4>

- 클래스의 식별자 필드를 테이블의 PK에 매핑

<h4> @Column </h4>

- 클래스의 필드를 테이블의 컬럼에 매핑

출처 : https://velog.io/@jwkim/JPA-%EB%A7%A4%ED%95%91-%EC%A0%95%EB%B3%B4-Annotation - [JPA] 매핑 정보 Annotation
