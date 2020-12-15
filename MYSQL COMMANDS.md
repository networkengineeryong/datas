# 용어
Database : 데이터가 적재되는 테이블들을 분류하는 상위 개념

Table : 데이터가 저장되는 저장소

Schema : 테이블에 적재될 데이터의 구조와 형식을 정의 하는 것

* 테이블 리스트 조회
<pre><code>SHOW TABLES;</code></pre>

* 테이블 스키마 열람
<pre><code>DESC 'TABLE_NAME';</code></pre>

* 테이블 제거
<pre><code>DROP TABLE 'TABLE_NAME';</code></pre>

# 데이터 타입
<pre><code>CHAR : 0 ~ 255 고정 

VARCHAR : 0 ~ 65535 가변 

TINYTEXT : ~ 255 

TEXT : ~ 65535 

BLOB : ~ 65535 

MEDIUMTEXT : ~ 16777215 

MEDIUMBLOP : ~ 16777215 

LONGTEXT : ~ 4294967295 

LONGBLOP : ~ 4294967295

TINYINT : -128 ~ 127 (INT), 0 ~ 255 (UNSIGNED_INT)

SMALLINT : - 32768 ~ 32767 (INT), 0 ~ 65535 (UNSIGNED_INT)

MEDIUMINT : - 8388608 ~ 8388607 (INT), 0 ~ 16777215 (UNSIGNED_INT)

INT : - 2147483648 ~ 2147483647 (INT), 0 ~ 4294967295 (UNSIGNED_INT)

BIGINT : - 9223372036854775808 ~ 9223372036854775807 (INT), 0 ~ 

18446744073709551615 (UNSIGNED_INT)

FLOAT : 작은 부동소수점

DOUBLE : 큰 부동소수점

DATE : YYYY-MM-DD

DATETIME : YYYY-MM-DD-HH:MM:SS

TIMESTAMP : YYYYMMDDHHMMSS

TIME : HH:MM:SS

ENUM : 캐릭터형 데이터 타입, 칼럼에 들어올 수 있는 값을 지정한다. </code></pre>

# 명령어
* 데이터베이스 생성
<pre><code>create database 'DATABASE_NAME';</code></pre>

* 데이터베이스 선택
<pre><code>use 'DATABASE_NAME';</code></pre>

* 테이블 생성
<pre><code>create table 'TABLE_NAME' (
     column1_name value_type,
     column2_name value_type
     )</code></pre>

* 테이블에 데이터 추가
<pre><code>insert into 'TABLE_NAME' values ('VALUE1',....);</code></pre>

* 테이블의 데이터 삭제
<pre><code>delete from 'TABLE_NAME' where {ID}={VALUE};</code></pre>

* 테이블의 데이터 모두 변경
<pre><code>update 'TABLE_NAME' set {ID}={VALUE};</code></pre>

* 테이블의 데이터 선택 변경
<pre><code>update 'TABLE_NAME' set {ID}={VALUE} where {CONDITION};</code></pre>

* 테이블의 데이터 n개 선택 변경
<pre><code>update 'TABLE_NAME' set {ID}={VALUE}, {ID}={VALUE}, ... where {CONDITION};</code></pre>

* 테이블의 모든 데이터 조회
<pre><code>select * from 'TABLE_NAME';</code></pre>

* 테이블의 데이터 선택 조회
<pre><code>select * from 'TABLE_NAME' where {CONDITION};</code></pre>

* 테이블의 데이터 n개 선택 조회
<pre><code>select * from 'TABLE_NAME' where {CONDITION} LIMIT n;</code></pre>
