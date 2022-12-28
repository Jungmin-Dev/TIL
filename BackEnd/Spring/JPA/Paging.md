
<h2> 주요 객체 </h2>

- `Page<T>` : 페이지 정보를 담게 되는 인터페이스
- `Pageable` : 페이지 처리에 필요한 정보를 담게 되는 인터페이스

<h2> 관계 및 사용 </h2>

- PageRequest에 의해 Pageable에 페이징 정보가 담겨 객체화 된다.
- Pageable이 JpaRepository가 상속된 인터페이스의 메서드에 파라미터로 전달된다.
- 2번의 메서드의 return 으로 Page<T>가 전달 된다.
- 전달된 Page<T>에 담겨진 Page 정보를 바탕으로 로직을 처리하면 된다.

<h2> PageRequest의 메서드 </h2>
  
- `of(int page, int size)` : 0부터 시작하는 페이지 번호와 개수. 정렬이 지정되지 않음
- `of(int page, int size, Sort sort)` : 페이지 번호와 개수, 정렬 관련 정보
- `of(int page int size, Sort sort, Direction direction, String ... props) ` : 0부터 시작하는 페이지 번호와 개수, 정렬의 방향과 정렬 기준 필드들
  
<h2> Page<T>의 메서드 </h2>
    
- `getTotalPages()` : 총 페이지 수
- `getTotalElements()` : 전체 개수
- `getNumber()` : 현재 페이지 번호
- `getSize()` : 페이지 당 데이터 개수
- `hasnext()` : 다음 페이지 존재 여부
- `isFirst()` : 시작페이지 여부
- `getContent(), get()` : 실제 컨텐츠를 가지고 오는 메서드. getContext는 List<Entity> 반환, get()은 Stream<Entity> 반환

<h2> Sort 객체 사용 </h2>
    
  ```java
        Sort sort1 = Sort.by("mno").descending();
        Sort sort2 = Sort.by("memoText").ascending();
        Sort sortAll = sort1.and(sort2);
        Pageable pageable = PageRequest.of(0, 10, sortAll);
  ```
    
- Sort.by("필드명")으로 오름차순 또는 내림차순 정렬이 가능하고

- Sort1.and(sort2)와 같이 and()를 사용해서 실제 PageRequest 사용 시 필드별로 정렬 조건을 전달할 수 있다.
    
    
출처 : https://sharekim-dev.tistory.com/29 - JPA Paging(Page, Pageable, PageRequest, Sort)
