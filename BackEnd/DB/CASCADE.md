<h1> CASCADE </h1>

<h3> 두 테이블을 연결해서 PK를 가지고 있는 쪽의 값을 삭제하면 FK로 연결된 값이 동시에 삭제되게 하는 옵션이다 </h3>

<h4> 테이블 생성 </h4>

```SQL
-- 부모 역할 테이블
CREATE TABLE MOTHER_TABLE(
PK_VAL1 VARCHAR2(20),
CONSTRAINT MOTHER_PK PRIMARY KEY (PK_VAL1)
);

-- 자식 역할 테이블
CREATE TABLE CHILD_TABLE(
PK_VAL1 VARCHAR2(20),
VAL2 VARCHAR2(20),
CONSTRAINT CHILD_PK
FOREIGN KEY (PK_VAL1) -- 해당 테이블의 FK 설정
REFERENCES MOTHER_TABLE(PK_VAL1) -- MOTHER 테이블의 PK와 연결
ON DELETE CASCADE -- MOTHER TABLE의 값 삭제시 연결된 값 삭제
);
```

<h4> 만약 생성과정이 아닌 ALTER로 테이블에 CASCADE를 설정해주기 위해선 아래와 같이 하면 된다. </h4>

```SQL
-- ALTER를 이용한 CASCADE 추가
ALTER TABLE 테이블명
ADD CONSTRAINT 제약조건명
FOREIGN KEY (CHILD_테이블의_FK값) -- 해당 테이블의 FK 설정
REFERENCES MOTHER_테이블명(MOTHER_테이블의_PK) -- MOTHER PK와 연결
ON DELETE CASCADE;
```

<h4> Table 값 생성 </h4>

```SQL
INSERT INTO MOTHER_TABLE VALUES('A');
INSERT INTO MOTHER_TABLE VALUES('B'); -- MOTHER 테이블에 값 추가

INSERT INTO CHILD_TABLE VALUES('A', 'A값1');
INSERT INTO CHILD_TABLE VALUES('A', 'A값2');
INSERT INTO CHILD_TABLE VALUES('B', 'B값1');
INSERT INTO CHILD_TABLE VALUES('B', 'B값2'); -- CHILD 테이블에 값 추가
```

<h4> PK - FK로 연결된 테이블 연쇄삭제 </h4>

```SQL
-- MOTHER 테이블의 값 삭제시 PK - FK로 연결된 CHILD 테이블의 값도 삭제
DELETE FROM MOTHER_TABLE WHERE PK_VAL1 = 'A'
```

<h4> CASCADE 제약조건 삭제방법 </h4>

```SQL
ALTER TABLE CHILD_테이블명 DROP CONSTRAINT 제약조건명
```

출처 : https://wakestand.tistory.com/205 [Wakestand Island]
