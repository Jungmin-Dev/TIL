<h1> WITH(RECURSIVE) 구문 </h1>

 - WITH 문은 임시테이블을 만들 때 사용하며 RECURSIVE를 함께 사용하면 재귀쿼리로 활용할 수 있다.
 - WITH 임시테이블 명 AS ()
 ```sql 
 WITH RECURSIVE 재귀함수 명 AS (
  SELECT 
  FROM 시작할 테이블 
  UNION ALL
  SELECT 
  FROM 반복할 테이블
  )
```

<h2>1. WITH문을 사용하는 이유? </h2>

 - 반복되는 (서브)쿼리를 사용할 경우 성능이 저하될 수 있으므로 TEMP라는 임시테이블에 저장하여 필요할 때 마다 불러서 사용하면 같은 쿼리를 여러번 실행하지 않으므로 성능에 문제가 되지않는다.
 - TEMP 테이블에는 한계가 있기 때문에 적절히 사용하는 것이 좋다.

<h2>2. WITH문 사용 예시</h2>

- 사원 테이블에서 직업별 월급 합산분을 출력하는데 직업별 월급 합산분의 평균보다 높은 것만 출력하라

2-1. 일반 쿼리

```sql
	SELECT SUM(SAL)
	FROM EMP 
	GROUP BY JOB
	HAVING SUM(SAL) > (SELECT AVG(SUM(SAL)) FROM EMP GROUP BY SAL)
```

2-2. WITH절 사용 쿼리

```sql
	WITH TMP AS (
	    SELECT SUM(SAL) AS SSUM
	    FROM EMP
	    GROUP BY JOB
	)
	SELECT * 
	FROM TMP 
	WHERE TOTAL > (SELECT AVG(TOTAL) FROM TMP)
```
  
<h2>3. WITH RECURSIVE문을 사용하는 이유?</h2>

- 데이터 간의 계층 관계를 직관적으로 표현하기 위해 사용한다.
- ex) 최상위 부모부터 최하위 자식까지 레벨을 부여하여 보기 쉽게 표현  

<h2>4. WITH RECURSIVE문 사용 예시</h2>

 - 1부터 10 까지 수를 출력하라

```sql
    WITH RECURSIVE TMP AS (
	SELECT 1 AS START 
	UNION ALL 
	SELECT START + 1 
	FROM TMP 
	WHERE START > 10
    )
```
 - 프로그래머스 문제 예시 
https://programmers.co.kr/learn/courses/30/lessons/59413
