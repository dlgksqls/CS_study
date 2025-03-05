<h1>SQL</h1>

<h2 style="color: cornflowerblue"> 데이터 정의 언어 DDL <br>(Data Define Language)</h2>

<h3> CREATE</h3>
<p>데이터베이스 (CREATE DATABASE), 테이블 (CREATE TABLE), 뷰, 인덱스, 사용자 ,, 까지 데이터베이스에서 관리될 수 있는 다양한 대상을 정의함</p>
<p>필드 타입 우측 또는 CREATE TABLE문 하단에 특정 필드가 지켜야 할 제약 조건을 명시할 수 있음</p>

![제약조건.png](image%2F%EC%A0%9C%EC%95%BD%EC%A1%B0%EA%B1%B4.png)

![CREATE_TABLE.png](image%2FCREATE_TABLE.png)

<h3> ALTER</h3>
<p>CREATE TABLE문을 통해 생성된 테이블에 새로운 필드를 추가하거나 기존의 필드를 수정/삭제할 수 있고, 제약 조건 또한 새롭게 추가하거나 수정/삭제할 수 있음</p>

```sql
ALTER TABLE posts ADD COLUMN new_field VARCHAR(50) NOT NULL;
```

<h3> DROP</h3>

```sql
DROP DATABASE 데이터베이스_이름;
DROP TABLE 테이블_이름;
```

<h3> TRUNCATE</h3>
<p>테이블의 구조를 유지한 채로 테이블의 모든 레코드를 삭제</p>

```sql
TRUNCATE TABLE 테이블_이름;
```

<h2 style="color: cornflowerblue"> 데이터 조작 언어 DML <br>(Data Manipulation Language)</h2>

<h3> INSERT</h3>
<p>테이블에 레코드를 삽입하는 명령어</p>

```sql
INSERT INTO 테이블_이름(필드1, 필드2) VALUES (값1, 값2);
INSERT INTO 테이블_이름(필드1, 필드2) VALUES 
                                 (값1, 값2),
                                 (값1, 값2),
                                 (값1, 값2);
```

<h3> UPDATE, DELETE</h3>

```sql
UPDATE 테이블 이름
SET 필드1 = 값1, 필드2 = 값2
WHERE 조건식;
```

```sql
DELETE 테이블_이름
WHERE 조건식;
```

<h3> SELECT</h3>

```mysql
SELECT 필드1, 필드2
FROM 테이블_이름
WHERE 조건식
GROUP BY 그룹화할_필드
HAVING 필터_조건
ORDER BY 정렬할_필드
LIMIT 레코드_제한
```

<h3> GROUP BY</h3>
<p>특정 필드를 기준으로 필드를 그룹화하기 위해 사용</p>

<h3> HAVING</h3>
<p>GROUP BY절로 그룹화된 결과에 조건을 적용하기 위해 사용됨</p>

```mysql
SELECT major, AVG(gpa) AS 평균
FROM students
GROUP BY major
HAVING AVG(gpa) >= 3.6
```

<h3> ORDER BY</h3>
<p>특정 필드를 기준으로 데이터를 정렬하는 데 사용됨</p>
<ul>
    <li>DESC : 내림차순</li>
    <li>ASC : 오름차순 (default)</li>
</ul>

<h3> LIMIT</h3>
<p>레코드 수를 제한하기 위해 사용됨</p>
<p>아래의 예는 상위 3개의 레코드만 조회됨</p>

```mysql
SELECT *
FROM students
LIMIT 3;
```

<h2 style="color: cornflowerblue"> 트랜잭션 제어 언어 (TCL) <br>Transaction Control Language</h2>

<ul>
    <li>COMMIT : 데이터베이스에 작업 반영</li>
    <li>ROLLBACK : 작업 이전의 상태로 되돌림</li>
    <li>SAVEPOINT : 롤백의 기준점 설정</li>
</ul>

<h2 style="color: cornflowerblue"> 데이터 제어 언어 (DCL) <br>Data Control Language</h2>

<ul>
    <li>GRANT : 사용자에게 권한 부여</li>
    <li>REVOKE : 사용자로부터 권한 회수</li>
</ul>