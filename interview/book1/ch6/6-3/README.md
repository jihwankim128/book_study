# SQL

## 데이터 정의 언어 (DDL, Data Definition Language)

* CREATE
  * DB, DB 객체를 생성
  * CREATE TABLE {NAME}
  * VIEW, INDEX, USER, ...
  
  ```sql
    CREATE TABLE USERS (
        user_id BIGINT PRIMARY KEY AUTO_INCREMENT,
        username VARCHAR(50) NOT NULL,
        email VARCHAR(100) UNIQUE,
        ...
        -- 혹은 
        PRIMARY KEY (user_id),
        CONSTRAINT UK_EMAIL UNIQUE (email)
    );
  ```
  
* ALTER
  * 생성된 DB TABLE을 수정 및 삭제 할 수 있다.
    * 필드, 제약 조건 추가 및 제거
  ```sql
  ALTER TABLE AUTH ADD COLUMN user_id BIGINT NOT NULL;
  ALTER TABLE AUTH ADD FOREIGN KEY (user_id) REFERENCES USER(user_id);
  ...
  ```
  
* DROP
  * DB 및 DB 객체를 제거한다.
  * `DROP DATABASE 데이터베이스_이름;`
  * `DROP TABLE 테이블_이름;`
  
* TRUNCATE
  * 테이블의 구조를 유지한 채로 모든 레코드를 제거
  * `TRUNCATE TABLE 테이블_이름;`
  * DESC로 구조는 유지되는 것을 확인 할 수 있다.

* ETC
  * SHOW, DESCRIBE (DESC) 등의 DDL도 존재

## 데이터 조작 언어 (DML, DATA MANIPULATION LANGUAGE)

* INSERT
  * `INSERT INTO 테이블_이름(필드1, 필드2, ...) VALUES (값1, 값2, ...);`
  * 제약 조건에 위배되는 경우 실행이 거부 된다.
* UPDATE & DELETE
  * `UPDATE 테이블_이름 SET 필드1=값1, 필드2=값2, ... WHERE 조건식;`
  * `DELETE FROM 테이블_이름 WHERE 조건식;`
  * WHERE 조건식은 생략이 가능
  * 참조에 대한 동작 4가지
    * UPDATE와 DELETE는 6-2에서 작성한 참조 동작을 적용할 수 있다.
    * 기본 동작(NO ACTION)은 RESTRICT
* SELECT
  ``` sql
  SELECT 필드1, 필드2, ... or *(모든 필드)
  FROM 테이블_이름
  WHERE 조건식
  GROUP BY 그룹화할_필드
  HAVING 그룹화_필터_조건
  ORDER BY 정렬할_필드 <OPTION>
  LIMIT 레코드_제한;
  ```
  * FROM 절 이후는 선택 사항이다.
* GROUP BY
  * 동일한 값끼리 묶어서 집계하는 기능 (MAP 자료구조처럼 키-값 쌍으로 그룹화하는 기능)
  * `SELECT name, COUNT(*) AS 동일_인원 FROM USERS GROUP BY name;`
* HAVING
  * GROUP BY에 적용하기 위한 조건
  * `SELECT name, COUNT(name) AS 동일_인원 FROM USERS GROUP BY name HAVING COUNT(*) >= 2;`

## 트랜잭션 제어 언어 (TCL, Transaction Control Language)

* **COMMIT**: 데이터 베이스에 작업 반영
* **ROLLBACK**: 작업 이전의 상태로 되돌림
* **SAVEPOINT**: 롤백의 기준점 설정, TRANSACTION 내부에서만 동작
* 여러 쿼리 실행 시
```sql
START TRANSACTION;
    SELECT USERS; -- 시점 A
    UPDATE USERS;
    SELECT USERS; -- 시점B, 시점 A와 다른 정보
    ROLLBACK
    SELECT USERS; -- 시점 A와 동일
    UPDATE USERS:
    SELECT USERS; -- 다시 시점 B로 변경
COMMIT; -- 최종 시점 B 저장
```
* SAVEPOINT 활용시
```sql
START TRANSACTION;
    SELECT USERS; -- 시점 A
    SAVEPOINT sp1;
    UPDATE USERS;
    SAVEPOINT sp2;
    SELECT USERS; -- 시점 B, 시점 A에서 변경된 정보
    ROLLBACK TO SAVEPOINT sp1;
    SELECT USERS; -- 시점 A와 동일
    --ROLLBACK TO SAVEPOINT sp2;
    --sp1로 이동하면서 sp2가 사라짐
COMMIT;
```

## 데이터 제어 언어 (DCL, Data Control Language)

* **GRANT**: 사용자에게 권한 부여
* **REVOKE**: 사용자로부터 권한 회수
* DBMS 사용자 계정 생성에 사용 됨.
```sql
GRANT SELECT, INSERT ON users TO 'username'@'localhost';
REVOKE DELETE ON users FROM 'username'@'localhost';
```