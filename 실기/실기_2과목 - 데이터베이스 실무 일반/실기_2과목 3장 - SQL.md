실기 2과목 페이지
[데이터베이스 실무 일반](https://github.com/JuNijen/Industrial-Engineer-Information-Processing/wiki/%EC%8B%A4%EA%B8%B0_2%EA%B3%BC%EB%AA%A9---%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%8B%A4%EB%AC%B4-%EC%9D%BC%EB%B0%98)


# #069. SQL - DDL
DDL은 스키마(Schema), 도메인(Domain), 테이블(Table), 뷰(View), 인덱스(Index)를 정의하거나 변경 또는 제거할 때 사용하는 언어이다.
DDL로 정의된 내용은 메타데이터(Metadata)가 되며, 시스템  카탈로그(Ststem Catalog)에 저장한다.
### DDL의 유형
- CREATE : 스키마, 도메인, 테이블, 뷰, 인덱스를 정의한다.
- ALTER : 테이블에 대한 정의를 변경한다.
- DROP : 스키마, 도메인, 테이블, 뷰, 트리거, 인덱스를 제거한다.
## 1. CREATE SCHEMA
스키마를 정의하는 명령문이다.
스키마는 하나의 응용(사용자)에 속하는 테이블과 기타 구성 요소 등을 그룹짓기 위한 것이다.
스키마의 식별을 위한 스키마 이름과 해당 스키마의 소유권자나 허가권자를 정의한다.
- 표기 형식 :
```
CREATE SCHEMA 스키마명 AUTHORIZATION 사용자_ID;
```
## 2. CREATE DOMAIN
도메인을 정의하는 명령문이다.
도메인이란 하나의 속성이 취할 수 있는 동일한 타입의 원자값들의 집합이다.
임의의 속성에서 취할 수 있는 값의 범위가 SQL에서 지원하는 전체 데이터 타입의 값이 아니고 일부분일 때, 사용자는 그 값의 범위를 도메인으로 정의할 수 있다.
정의된 도메인명은 일반적인 데이터 타입처럼 사용한다.
- 표기 형식 :
```
CREATE DOMAIN 도메인명 데이터_타입
```
[DEFAULT 기본값]
[CONSTRAInT 제약조건명 CHECK (범위 값)]
- 데이터_타입 : SQL에서 지원하는 데이터 타입
- 기본값 : 데이터를 입력하지 않았을 때 자동으로 입력되는 값
## 3. CREATE TABLE
테이블을 정의하는 명령문이다.
- 표기 형식 :
```
CREATE TABLE 테이블명 
    (속성명 데이터타입 [NOT NULL], … 
    [, PRIMARY KEY (기본키_속성명, …)]
    [, UNIQUE (대체키_속성명, …)]
    [, FOREIGN KEY (외래키_속성명, …)
        REFERENCES 참조테이블(기본키_속성명, …)]
        [ON DELETE 옵션]
        [ON UPDATE 옵션]
    [, CONSTRAINT 제약조건명][CHECK (조건식)];
```
- 기본 테이블에 포함될 모든 속성에 대하여 속성명, 속성의 데이터 타입, NOT NULL을 지정한다.
- PRIMARY KEY : 기본키로 사용할 속성 또는 속성의 집합을 지정한다.
- UNIQUE : 대체키로 사용할 속성 또는 속성의 집합을 지정하는 것으로 UNIQUE로 지정한 속성은 중복된 값을 가질 수 없다.
- FOREGN KEY ~ REFERENCES ~ : 외래키 속성과 참조 테이블에 관한 정보를 지정한다. 외래키가 지정되면 참조 무결성으 CASCADE 법칙이 적용된다.
- ON DELETE 옵션 : 참조 테이블의 튜플이 삭제되었을 때 기본 테이블에 취해야 할 사항을 지정한다. 옵션에는 NO ACTION, CASCADE, SET NULL, SET DEFAULT가 있다.
    ▶ NO ACTION : 참조 테이블의 튜플이 삭제되면 기본 테이블의 관련 튜플도 모두 삭제되고, 속성이 변경되면 관련 튜플의 속성 값도 모두 변경된다.
    ▶ SET NULL : 참조 테이블에 변화가 있으면 기본 테이블의 관련 튜플의 속성 값을 기본값으로 변경한다.
- CONSTRAINT : 제약 조건의 이름을 지정한다. 이름을 지정할 필요가 없으면 CHECK 절만 사용하여 속성 값에 대한 제약 조건을 명시한다.
- CHECK : 속성 값에 대한 제약 조건을 지정한다.
## 4. CREATE VIEW
뷰는 하나 이상의 기본 테이블로부터 유도되는 이름을 갖는 가상 테이블(Virtual Table)로, CREATE VIEW는 뷰를 정의하는 명령문이다.
- 표기 형식 :
```
CREATAE VIEW 뷰명 [(속성명[, 속성명, …])]
AS SELECT문;
```
- SELECT문을 서브 쿼리로 사용하여 seLECT문의 결과로서 뷰를 생성한다.
- 서브 쿼리인 SELECT문에는 UNION이나 ORDER BY절을 사용할 수 없다.
- 속성명을 기술하지 않으면 SELECT문의 속성명이 자동으로 사용된다.
## 5. CREATE INDEX
인덱스는 검색을 빠르게 하기 위해 만든 보조적인 데이터 구조이며, CREATE INDEX는 인덱스를 정의하는 명령문이다.
- 표기 형식 :
```
CREATE [UNIQUE] INDEX <인덱스명>
    ON 테이블명({속성명 [ASC | DESC][, 속성명 [ASC | DESC]]})
    [CLUSTER];
```
- UNIQUE
    ▶ 사용된 경우 : 중복 값이 없는 속성으로 인덱스를 생성한다.
    ▶ 생략된 경우 : 중복 값을 허용하는 속성으로 인덱스를 생성한다.
- 정렬 여부 지정
    ▶ ASC : 오름차순 정렬
    ▶ DESC : 내림차순 정렬
    ▶ 생략된 경우 : 오름차순으로 정렬됨
- CLUSTER : 지정된 키에 따라 튜플들을 그룹으로 지정하기 위해 사용한다.
## 6. CREATE TRIGGER
트리거(Trigger)는 데이터베이스 시스템에서 데이터의 입력, 갱신, 삭제 등의 이벤트(event)가 발생할 때 마다 자동적으로 수행되는 사용자 정의 프로시저다.
- 트리거는 SQL의 제약조건 방법을 통해 명시할 수 없는 무결성 제약조건을 구현하고, 관련 테이블의 데이터를 일치시킬 때 주로 사용한다.
- 표기 형식 : 
```
CREATE TRIGGER  xmflrjaud [동작시기 옵션][동작 옵션] ON 테이블명
REFERENCING [NEW | OLD] TABLE AS 테이블명
FOR EACH ROW
WHEN 조건식
트리거 BODY
```
- 동작시기 옵션 : 트리거가 실행될 때를 지정한다. 옵션에는 AFTER와 BEFORE가 있다.
    ▶ AFTER : 테이블이 변경된 후에 트리거가 실행된다.
    ▶ BEFORE : 테이블이 변경되기 전에 트리거가 실행된다.
- 동작 옵션 : 트리거가 실행되게 할 작업의 종류를 지정한다. 옵션에는 INSERT, DELETE, UPDATE가 있다.
    ▶ INSERT : 테이블에 새로운 레코드를 삽입될 때 트리거가 실행된다.
    ▶ DELETE : 테이블의 레코드를 삭제할 때 트리거가 실행된다.
    ▶ UPDATE : 테이블의 레코드를 수정할 때 트리거가 실행된다.
- 테이블 선택 옵션 : 트리거가 적용될 테이블의 종류를 지정한다. 옵션에는 NEW와 OLD가 있다.
    ▶ NEW : 새로 추가되거나 변경에 참여할 튜플들의 집합(테이블)에 트리거가 적용된다.
    ▶ OLD : 변경된 튜플들의 집합(테이블)에 트리거가 적용된다.
- WHEN : 트리거가 실행되면서 지켜야 할 조건을 지정한다.
- 트리거 BODY : 트리거의 본문 코드를 입력하는 부분이다.
    ▶ BEGIN으로 시작해서 END로 끝나는데, 적어도 하나 이상의 SQL문이 있어야 한다. 그렇지 않으면 오류가 발생한다.
    ▶ 변수에 값을 치환할 때는 예약어 SET를 사용한다.
## 7. ALTER TABLE
테이블에 대한 정의를 변경하는 명령문이다.
- 표기 형식 : 
```
ALTER TABLE 테이블명 ADD 속성명 데이터_타입 [DEFAULT '기본값'];
ALTER TABLE 테이블명 ALTER 속성명 [SET DEFAULT '기본값'];
ALTER TABLE 테이블명 DROP COlUMN 속성명 [CASCADE];
```
- ADD : 새로운 속성을 추가한다.
- ALTER : 속성의 기본값(Default)을 변경한다.
- DROP COLUMN : 속성을 제거한다.
## 8. DROP
스키마, 도메인, 테이블, 뷰, 인덱스, 트리거를 제거하는 명령문이다.
- 표기 형식 :
```
DROP SCHEMA 스키마명 [CASCADE | RESTRICT]
DROP DOMAIN 도메인명 [CASCADE | RESTRICT]
DROP TABLE 테이블명 [CASCADE | RESTRICT]
DROP VIEW 뷰명 [CASCADE | RESTRICT]
DROP INDEX 인덱스명 [CASCADE | RESTRICT]
DROP TRIGGER 트리거명 [CASCADE | RESTRICT]
DROP CONSTRAINT 제약조건명 [CASCADE | RESTRICT]
```
- CASCADE : 제거할 개체를 참조하는 다른 모든 개체를 함께 제거한다. 즉, 주 테이블의 데이터 제거 시, 각각의 외래키와 관계를 맺고 있는 모든 데이터를 함께 제거하는 참조 무결성 제약 조건을 설정하기 위해 사용된다.

# #070. SQL - SELECT
SELECT문은 테이블을 구성하는 튜플들 중에서 전체 또는 조건을 만족하는 튜플을 검색하여 주기억장치에 임시 테이블로 구성하는 명령문이다.
## 1. SELECT문의 일반 형식
```
SELECT [PREDICATE][테이블명.]속성명[AS 별칭][, 테이블명.]속성명, …]
FROM 테이블명[, 테이블명, …]
[WHERE 조건]
[GROUP BY 속성명[, 속성명, …]]
[HAVING 조건]
[ORDER BY 속성명 [ASC|DESC][, 속성명 [ASC|DESC], …]];
```
- SELECT절
    - PREDICATE : 검색할 튜플을 제한할 목적으로 사용되는 조건으로서, ALL, DISTINCT, DISTINCTROW 등이 올 수 있다.
        ▶ ALL : 모든 튜플들을 검색할 때 사용되며, 기본값이다.
        ▶ DISTINCT : 중복된 튜플을 제거할 때 사용된다.
        ▶ DISTINCTROW : 중복된 튜플을 제거하지만, 선택된 속성의 값이 아닌 튜플의 전체 값을 대상으로 할 때 사용된다.
    - 속성명 : 검색하여 불러올 속성 또는 수식으로서, 2개 이상의 테이블을 대상으로 검색할 때는 '테이블명.속성명'으로 사용된다.
    - AS : 속성 및 연산의 이름을 다른 제목으로 표시하기 위해 사용된다.
- FROM절 : 검색할 데이터가 들어있는 테이블명을 기술한다.
- WHERE절 : 검색할 조건을 기술한다. 다양한 조건 연산자의 사용이 가능하며, 이때 각 연산자의 처리 순서는 연산자 우선순위를 따른다.
- GROUP BY절 : 특정 속성을 기준으로 그룹화하여 검색할 때 사용한다. 일반적으로 GROUP BY절은 그룹 함수와 함께 사용한다.
- HAVING절 : 그룹에 대한 조건을 기술한다.
- ORDER BY절 : 특정 속성을 기준으로 정렬하여 검색할 때 사용한다.
    - 속성명 : 정렬의 기준이 되는 속성명을 기술한다.
    - [ASC | DESC] : 정렬 방식을 기술한다. ASC는 기본값으로서 오름차순, DESC는 내림차순 정렬을 나타낸다.
## 2. 기본 검색
## 3. 조건 지정 검색
## 4. 정렬
## 5. 그룹 검색
## 6. 하위 질의
## 7. 복수 테이블 검색
## 8. 통합(UNION) 질의


# #071. SQL - JOIN
## 1.
## 2.
## 3.

# #072. SQL - DML
## 1.
## 2.
## 3.

# #073. SQL - DCL
## 1.
## 2.
## 3.

# #074. 뷰(VIEW)
## 1.
## 2.
## 3.

# #075. 내장 SQL
## 1.
## 2.
## 3.

# #076. 스토어드 프로시저(Stored Procedure)
## 1.
## 2.
## 3.