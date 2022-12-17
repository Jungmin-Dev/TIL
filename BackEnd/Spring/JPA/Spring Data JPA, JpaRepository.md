<h1> Spring Data JPA </h1>

- 스프링 프레임워크 + JPA에 특화된 기능 제공
- 데이터 접근 계층을 개발할 때 구현 클래스 없이 인터페이스만으로도 작동
- 동적으로 구현 객체를 생성해서 주입
<h2> JpaRepository </h2>

<h3> 설정 </h3>

- SomeRepository extends JpaRepository<{엔티티 타입}, {식별자 타입}>

```java
public interface MemberRepository extends JpaRepository<Member, Long> {
    List<Member> findByName(String name);
}
```

<h3> 주요 메소드 </h3>

- `save(S)` : 새로운 엔티티는 저장하고 이미 있는 엔티티는 수정한다.
- `delete(T)` : 엔티티 하나를 삭제한다. (em.remove())
- `findOne(ID)` : 엔티티 하나를 조회한다. (em.find())
- `getOne(ID)` : 엔티티 하나를 프록시로 조회한다. (em.getReference())
- `findAll()` : 모든 엔티티를 조회한다. Sort나 Pageable을 파라미터로 제공할 수 있다.

<h3> 쿼리 메소드 </h3>

- 메소드 이름으로 쿼리 생성
- 메소드 이름으로 JPA NamedQuery 호출
- @Query 사용해서 Repository interface에 쿼리 직접 정의

<h3> Parameter Binding </h3>

- 위치 기반 파라미터 바인딩 (디폴트)
- 이름 기반 파라미터 바인딩

``` java
Member findByUserName(@Param("name") String username);
```

<h3> 벌크성 수정 쿼리 </h3>

``` java
@Modifying
@Query("update Product p set p.price = p.price * 1.1 where p.stockAmount < :stockAmount")
int bulkPriceUp(@Param("stockAmount") String stockAmount);
@Modifying(clearAutomatically = true) : 벌크성 쿼리 실행 후 Persistence Context 초기화
```

<h3> Return Type </h3>

<h4> 단건 </h4>

- 리턴 타입 지정
- 0건 조회 시 null 반환
- 여러 건 조회 시 예외 발생

<h4> 여러 건 </h4>

- 컬렉션 인터페이스 사용
- 0건 조회 시 빈 컬렉션 반환

<h3> Paging & Sort </h3>

``` java
PageRequest pageRequest = new PageRequest(0, 10, new Sort(Direction.DESC, "name"));
Page<Member> result = memberRepository.findByNameStartingWith("김", pageRequest);
PageRequest Parameter : 현재 페이지, 조회할 데이터 수, Sort 조건
```

<h3> Specification </h3>

``` java
PageRequest pageRequest = new PageRequest(0, 10, new Sort(Direction.DESC, "name"));
Page<Member> result = memberRepository.findByNameStartingWith("김", pageRequest);
PageRequest Parameter : 현재 페이지, 조회할 데이터 수, Sort 조건
```

출처 : https://velog.io/@jwkim/JPA-Spring-Data-JPA-JpaRepository - [JPA] Spring Data JPA, JpaRepository
