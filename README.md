<SQLD 개발자 자격증 용어 정리 및 내용 정리>

# 도메인
- 값의 허용 범위
- 언터티 내에서 속성에 대한 데이터 타입과 크기 지정
- 엔터티 내에서 속성에 대한 NOT NULL /NULL 지정
- 엔터티 내에서 속성에 대한 CHECK 조건을 지정

# 식별자 / 비식별자
- 식별자 :부모의 주식별자 -> 자식의 주식별자로 상속
- 비식별자 : 부모로 부터 상속을 받지만 일반 속성으로 사용

# 속성
- 업무에서 필요로 하는 인스턴스로 관리하고자 하는 의미상 분리되지 않는 최소의 데이터 단위
- 엔터티를 설명하고 인스턴스의 구성요소

# 인스턴스
- 테이블의 각 행을 의미

# 주식별자 / 본질식별자 / 보조식별자 / 복합식별자
- 주식별자 : 유일성 최소성 불변성 존재성을 만족하는 식별자
- 보조식별자 : 유일성과 최소성만 만좃하는 식별자 참조 관계 연결에 사용 할 수 없음
- 본질식별자 : 유일성을 만족하는 식별자 
- 복합식별자 : 여러 속성을 지닌 식별자

# 참조무결성
- 외래키는 부모키(기본키)값과 같거나 NULL 이여야 한다.

# 주식별자 도출 기준
- 해당 업무에서 자주 이용되는 속성
- 명칭, 내역 등과 같이 이름으로 기술되는 것들은 주식별 선정하지 않는다.
- 너무 많은 속성을 포함하지 않는다.
- 변경 될 수 없다.

# 엔터티
- 업무에서 관리해야 하는 데이터의 집합 (명사) 인스턴스의 집합

# 반정규화
- 중복컬럼 추가 - 조인감소를 위해
- 파생컬럼 추가 - 조회 성능을 우수하게 하기위해 미리 계산된 컬럼을 추가
- 이력테이블에 기능 칼럼 추가 - 최신값을 처리하는 이력의 특성을 고려하여 기능성 컬럼 추가
- 반정규화는 데이터 무결성을 해침 
- 반정규화 대상 :  빈도수 / 대량범위 / 통계 처리 (Sorting, Order by는 반정규화 대상이 아니다.)

# 데이터 모델링 순서
- 개념적 모델링 -> 논리적 모델링 -> 물리적 모델링

# 분산 데이터베이스
- 분산 데이터베이스 : 논리적으로 같은 시스템, 물리적 분산, 데이터 무결성을 해침

# 분산 데이터베이스 특징
- 사용하려는 데이터의 저장 장소 명시가 불필요 : 위치 투명성
- 분할되서 여러군데 저장 : 분할 투명성
- 지역사상 투명성 : 지역 DBMS와 물리적 DB 사이 Mapping을 보장
- 장애 투명성 : 장애가 발생하여도 무관
- 병행 투명성 : 다수 트랜잭션이 동시에 해도 결과가 일치

# Row Chaining / Row migration
- Row Chaining : row가 너무 길어서 여러 블록에 걸쳐서 저장
- Row migration : 수정후 다른 블록 빈공간에 저장
- 디스크 I/O 많이 발생 -> 성능 저하
- 해결책 : 파티셔닝	(리스트 파티셔닝, 레인지 파티셔닝, 해시 파티셔닝)

# RANGE 파티셔닝 / LIST 파티셔닝 / HASH 파티셔닝
- RANGE 파티셔닝 : 관계가 쉽다 / 많이 사용된다 / 숫자값으로 분리된다
- LIST 파티셔닝 : 대량 데이터 / 특정컬럼(생성일자)이 이 없음 / PK
- HASH 파티셔닝 : 관리가 어렵다 / 데이터 위치를 모른다.

# VARCHAR
- 가변 문자열 (비교연산자 불가능)

# CHARACTER
- 고정 길이 문자열 정보로 S만큼 최대 길이를 갖고 고정 길이를 가지고 있으모로 할당된 변수 값의 길이가 S보다 작을 경우에는 그 차이 길이 만큼 공간으로 채워진다.

# 최소 조인 조건
- N개의 테이블 -> N-1개 조건

# TRUNCATE TABLE
- 테이블 자체가 삭제되는 것이 아니라 해당 테이블의 모든 행들이 제거되고 저장 공간을
- 재사용 가능(특정 행을 삭제 할 수는 없다.)
- 구조 자체 삭제는 DROP TABLE을 이용
- DDL로 분류
- DELETE 명령어와 처리 방식 자체가 다름.
- 전체 데이터 삭제시 부하가 더 적어서 권장
- 오토커밋이기 때문에 정상적인 복구가 불가능

# PROCEDURE(프로시저) / TRIGGER(트리거) 
- PROCEDURE : EXECUTE 명령어로 실행 / COMMIT,ROLLBACK 가능 / 반드시 리턴값이 필요 / CREATE Procedure 문법 사용
- TRIGGER : 이벤트 발생 시 자동 실행 / COMMIT,ROLLBACK 불가능 / DML / CREATE Trigger 문법 사용

# CONNECT_BY_ROOT
계층형 쿼리에서 최상위 로우를 반환하는 연산자

# CONNECT_BY_ISLEAF
- 전개 과정에서 해당 데이터가 리프 데티어(최하단 데이터)이면 1 아니면 0

# SYS_CONNECT_BY_PATH
- 루트(시작)데이터부터 현재 전개할 데이터까지의 경로 표시

# START WITH
- 시작점을 지정

# CONNECT BY PRIOR
PRIOR 가 붙은 방향으로 
EX) PRIOR 부모컬럼 = 자식컬럼 자식->부모 역방향
EX) PRIOR 자식컬럼 = 부모컬럼 부모->자식 순방향

# 조인조건이 Non_Equal 이면 Merge Join이 효율적이다

# Sort Merge Join / Hash Join
- 등가, 비등가 조인 가능 / 조인키 기준 정렬
- 등가 조인만 가능 / 함수 처리함 / 선행 테이블 작다 / 별도의 저장 공간필요 / 인덱스가 없으면 유리 

#  COALESCE(NULL,'2') 
- 괄호안에 순서대로 확인하여 NULL 이 아닌 최초값 반환
ex) COALESCE(NULL,NULL,'1,'2') => 1를 반환 

# NULLIF('값1','값2')
- '값1','값2' 같다면  NULL 반환하는

# NVL(값1,값2) / ISNULL(값1,값2)
-  값1이 NULL 이면 값2 반환

# CASE
- CASE 'ab' WHEN 'bc' THEN 'cd' END  => ab = bc 이면 cd 아니면 NULL

# DECODE
- DECODE ('ab','bc','cd') => ab = bc 이면 cd 아니면 NULL

# GROUP BY ROLLUP (인수1,인수2)
- ROLLUP은 인수의 순서에 의해 결과값이 변경 
- EX) GROUP BY ROLLUP(ID,DEPT_NAME) =>  ID 총합과 전체총합을 출력
- 계층간 정렬 가능

# CUBE
- 결합 가능한 모든 값에 대하여 다차원 집계를 생성
- 계층간 정렬 가능
- 시스템 과부화 : CUBE > ROLLUP

#  UNION / UNION ALL / INTERSECT / MINUS / EXCEPT
- UNION : 중보허용x 합집합 
- UNION ALL : 중복허용 합집합 (정렬 작업을 하지 않음)
- INTERSECT : 교집합
- MINUS : 차집합(오라클)
- EXCEPT : 차집합(SQL SERVER)

# (+)
- (+) 가 붙은 테이블 말고 OUTER JOIN

# Unique Index Scan
- 1개의 값만 추출 (조건에 의해 1개 이상의 데이터가 추출 가능 할 경우 할 수 없음)

# 주문 REFERENCES 고객
- 고객이 부모 주문이 자식 관계

# 순번 구하는 함수
- RANK() : 중복값은 중복등수, 등수는 건넘뜀 EX) 1등,1등,3등
- ROW_NUMBER() : 중복값이 있어도 고유등수 부여 EX) 1등,2등,3등 
- DENSE_RANK() : 중복값은 중복등수, 등수는 건너뛰지 않음 EX) 1등,1등,2등

# 함수
- ROWNUMBER : 상위 첫행을 가져옴
- RATIO_TO_REPORT : 비율 0~1 값
- LAST_VALUE () OVER : 제일 마지막 값
- FIRST_VALUE () OVER : 제일 첫번째 값
- MAX() OVER : 제일 큰 값

# AUTO COMMIT
- SQL SERVER : AUTO COMMIT 꺼두면 UPDATE,CREATE 모두 취소되고 다시 테이블이 생성 되지않음
- ORACLE : DDL의 AUTO COMMIT이 기본이기 때문에 CREATE,UPDATE가 ROLLBACK를 하더라도 취소 되지않음

# LIKE'A%'
- A 로 시작하는 모든 ROW

# ROUND() / CEIL() / TRUNC() / FLOOR()
- ROUND() : 반올림
- CEIL() : 올림
- TRUNC() : 소수점 버림 
- FLOOR() : 내림

# ORDER BY
- 기본 정렬은 오름차순 ASC 생략가능
- ORACLE : NULL -> 무한대 가장 큰값
- SQL SERVER : NULL -> -무한대 가장 작은 값

# NL JOIN(NESTED LOOP JOIN) / SORT MARGE JOIN / HASH JOIN
- NL JOIN(NESTED LOOP JOIN): 랜덤 엑세스 , 대용량 SORT 작업에 유리(SORT!!!) 
- SORT MARGE JOIN : 등가("="),비등가("!=") JOIN 가능, 조인키 기준 정렬
- HASH JOIN : 등가("=") JOIN만 가능, 대량 작업에 유리(대량!!!), 함수처리, 선행테이블이 작아야 성능에 유리, 별도에 저장 공간이 필요, 인덱스가 없을 경우 더 유리

# CROSS JOIN / NATURAL JOIN
- CROSS JOIN : WHERE 절에 사용 가능 / JOIN KEY가 없을때 발생
- NATURAL JOIN : WHERE 절에 사용 불가능 / JOIN 컬럼 명시 불가 / JOIN KEY는 컬럼명


# WINDOW FUNCTION
- PARTITION 과 GROUP BY는 의미적으로 비슷
- 레코드 범위 지정 가능
- WINDOW FUNCTION 처리로 인한 건수가 줄어들 수 없음
- GROUP BY와 WINDOW FUNCTION은 병행하여 사용 불가

# WHERE 절
- NOY -> AND -> OR 순으로 연산

# NTILE(N)
- 전체 데이터를 N등분으로 나눔

# LAG() / LEAD()
- LAG() : 이전 N번째 행을 가져옴
- LEAD() : `이후 N번째 행을 가져옴

# DDL / DML / DCL / TCL
- DDL : CREATE, DROP, MODIFY, ALTER, RENAME
- DML : SELECT, DELETE, INSERT, UPDATE
- DCL : GRANT, REVOKE
- TCL : COMMIT, ROLLBACK

# VIEW 
- 복잡한 질의를 단순하게 작성 할 수 있다.
- 해당 형태의 SQL문을 자주 사용할 때 이용하면 편리하게 사용 할 수 있다.
- 실제 데이터를 가지고 있지 않다.
- 독립성 (테이블 구조가 변경되어도 응용프로그램은 변경 될 필요 X), 편리성, 보안성

# ALTER
- SQL SERVER에서 컬럼의 데이터 타입을 변형하는 구문 : ALTER COLNUMN
- SQL SERVER에서 테이블을 변형하는 구문 : ALTER TABLE

# GRANT
- SQL SERVER에서 테이블 생성권한을 주는 구문 

# PL/SQL
- BLOCK  구조로 되어있어 각 기능별로 모둘화가 가능
- 변수,상수 등을 선언하여 SQL 문장 간의 값을 교환
- IF,LOOP 등의 절차형 언어를 사용하여 절차적인 프로그램이 가능
- DBMS 정의 에러나 사용자 정의 에러를 정의하여 사용 
- PL/SQL은 오라클에 내장 오라클과 PL/SQL을 지원하는 어떤 서버로도 프로그램을 옮길 수 있음
- PL/SQL은 프로그램의 성능을 향상시킴
- PL/SQL은 BLOCK으로 묶어 BLOCK 전제를 서버를 보내기 떄문에 통신량을 줄임
- PL/SQL은 동적 SQL 또는 DDL 문장을 실행 할 때 EXECUTE IMMEDIATE를 사용 (소문자 가능)

# DROP / TRUNCATE / DELETE
DROP : DDL, 롤백 불가능, 오토커밋 테이블의 정의 자체를 삭제(완전 삭제)
TRUNCATE : DDL, 롤백 불가능, 오토커밋 테이블의 초기상태로 만듬(재사용 가능), 부하가 적음(빠름), 특정행 삭제 못함
DELETE : DML,  롤백 가능, 사용자 커밋 데이터만 삭제, 특정행 삭제 가능

# 데이터베이스 트랜잭션
- 원자성 : ALL OR NOTHING  모두 성공 OR 모두 실패 
- 일관성 : 잘못 되어있지 않으면 잘못 되어있지 않아야 한다 
- 지속성 : 트랜잭션이 갱신한 데이터는 영구적으로 저장 
- 고립성 : 다른 트랜잭션에 영향을 받아 잘못된 결과가 만들어서는 안된다

# SELF JOIN
- 한 테이블 내에서 두 칼럼이 연관 관계가 있다.
- 동일 테이블 사이의 조인
- FROM 절에 동일 테이블이 두번 이상 나타남
- 식별을 위해 반드시 ALIAS(별칭)을 사용해야 한다.
