CMD ( 공백 주의)
mysql -u(username 공백가능) -p(패스워드 공백X) : mysql 서버 접속

   SQL문 사용시 명령어 끝에 ;(세미콜론)을 사용해야 한다

현재 사용중인 DB확인(;필수)
show databases; : db 목록확인
select databases(); : 현재 사용중인 db확인
use (db이름) : 사용 할 DB선택
show tables; : db안의 table 목록 확인
desc 테이블 : 해당 테이블의 타입을 정렬한다.

SQL내의 연산
사칙연산 중 + / 우선순위이며 + - 후순위이다
NULL값에 사칙연산을 하면 NULL이다
복잡한 연산을 할 때는 내장함수를 이용한다.
round(대상, 반올림 위치) : 반올림한다(-쓰면 정수자리)
select round(a,3),round(b,-3) from test : a의 소수 3번째자리까지 반올림하고 b의 정수 3번째 자리까지 반올림한다 
sqrt(대상) : 대상에 대해서 루트를 씌운다.
select sqrt(a) from test;
concat(문자1(행), 문자2(행)) :문자1과 문자2를 더한다
select concat(a,b) from * : a,b 열을 합친다
subtring(대상, 기준점, 갯수) : 대상의 기준점을 기준으로 해당 갯수만큼 출력
select substring(a,1,2) from test : test테이블의 a열의  1번째에서 2개 만큼 출력
TRIM : 스페이스 제거
trim ('abc     ') = 'abc
charater_length : sql에서 len은 뭘까? 
날짜연산
current_timestamp : PC의 시간 기준
select current_timestamp;
select current_timestamp + interval (더할 날짜) (일,주,년)
select current_timestamp + interval 1 day : 하루를 더한다
select current_timestamp + interval 2 week : 2주일을 더한다
DATEDIFF(날짜1,날짜2) : 날짜1 - 날짜2
select datediff(current_timestamp(),'2018-06-19'); : 오늘날짜 기준으로 2018-12-31를 뺀다
CASE문
조건에 맞는 값을 출력한다.
CASE : CASE문을 시작한다
WHEN (조건) THEN (출력) : 조건문에 해당하는 THEN으로 출력한다
WHEN a = 1 THEN '남자'
ELSE (출력) :
ELSE a = '미지정'
END (열이름) : CASE문에 출력되는 행을 생성한다
END 'hi' : hi라는 행 생성


데이터 검색(select)
DML의 언어이다.
select (열이름) from (테이블명) : 열만 지정
select (열이름) from (테이블명) where (조건식) : 열과 행 지정
열 이름의 *(아스테리크)를 사용하면 전부를 뜻한다
ex) select * from test (test테이블의 모든 열 검색)
조건식
 = : 같다
<> : 같지 않다.
< > <= >= : 비교연산자
and or not(and가 or 우선순위 높다)
like (패턴)
패턴 -> % 임의의 여러문자, _ : 임의의 문자하나

order by (정렬기준 열): 정렬명령어
default로는 오름차순으로 되어있다.
desc : 내림차순으로 정렬한다.
문자열 정렬 기준 : 사전순
order by (기준열1),(기준열2) : 순서중요  구분은 ,(쉼표)
ex) select * from test order by a,b desc : 테스트 테이블에 대해 a로 오름차순 후 b로 내림차순 한다
NULL은 가장 작은값으로 취급한다.
LIMIT (출력할 행수) OFFSET(시작행+1) :  결과 값 제한
select * from test limit 2 offset 0 : 첫번째 열을 시작으로 2개의 값 출력

데이터추가(insert into)
 DML의 언어이다.  
insert into (테이블명) values(값1, 값2,...값n) : 행에 맞게 값 입력
insert into test values(1,'안녕') : test 테이블에 1의 값과 '안녕'을 추가
insert into 테이블명(특정 열) values(특정열에 맞는 값) : 특정 열에만 값을 입력
insert into test(a) values(1) : a의 열의 1이라는 값 입력
데이터수정(update)
 DML의 언어이다.  
update 테이블명 set 수정할 값 (where {조건})
update test set a = 2 where b = '헬로우' : test테이블의 b의 값이 헬로우인 a의 값을 2로 수정한다

데이터삭제(delete)
 DML의 언어이다.  
delete from 테이블명 (where {조건}) : 해당 테이블의 값을 삭제한다
delete from test : 테스트 테이블 값 삭제
where문이 없을 경우 데이터 삭제 / 조건문이 있을 시 해당 조건문에 해당하는 값만 삭제
테이블 자체 삭제가 아님 

테이블 추가(CREATE)
DDL의 언어이다.
CREATE TABLE 테이블이름 (열이름 열타입 속성) : 테이블이름명으로 테이블을 생성한다.
CREATE TABLE test_2 ( 
                            no int not null,
                            a varchar(10),
                            b date);
                    : test_2라는 테이블을 생성하면서 no라는 int형을 만들고 NULL값을 허용안한다.
                     a는 varchar(10)으로 생성하고, b는 date형식으로 생성한다.
테이블 중복명은 허용되지 않는다.


ALTER TABLE 테이블명 명령어(ADD,DROP,MODIFY,CHANGE)  : 추가 수정 변경 삭제
DDL의 언어이다.
ADD 행이름 행타입 : 열을 추가한다
alter table test add c int(10) : c열을 추가하고 int형으로 선언한다
alter table test add d varchar(10) : d열을 추가하고 varchar(10)으로 선언
,(쉼표)를 통해 여러열을 한번에 추가 가능
after (열이름) : 해당 열 다음으로 추가한다
after b : b열 다음으로 열 추가
first : 열 맨처음으로 추가한다 
DROP 행이름: 행을 삭제한다
alter table test drop d : d행을 삭제한다.
삭제시 복구 불가능
MODIFY 행이름 행타입 (새로운 조건 추가)  : 행의 타입 변경
alter table test modify c char(10) : C행의 형식을 int에서 char(10)으로 변경한다.
새로운 조건은 is not null과 unique 등이 있다.
CHANGE 원래행이름 바꿀행이름 (바꿀형식) : 행의 이름과 타입변경 :
alter table test change c d : 행 C의 이름을 D로 변경한다.
alter table test change c d date : 행 C를 D로 이름변경하면서 형식을 date로 한다

테이블 삭제(DROP)
DDL의 언어이다.
DROP TABLE 테이블명 : 테이블명의 정의된 테이블을 완전삭제한다.
DROP TABLE test : test의 테이블을 삭제한다.
복구불가능하다.

내부함수
COUNT(열이름 or * ) : 행의 갯수를 출력한다.
select count(*) from test : test의 행 갯수를 출력한다
where 문을 이용하여 조건에 맞는 갯수를 출력할 수 있다.
count(distant 열이름)으로 고유의 값만 셀 수 있다.
SUM(열이름 / * 불가능) : 합계를 출력한다. 
select sum(a) from test : test의 a열의 모든 값을 합해서 출력한다
* 는 불가능하다 (열들이 전부 int형도 불가능)
문자형은 연산불가능
AVG(열이름 / * 불가능) : 평균을 출력한다.
select avg(a) from test : test의 a열의 평균값을 출력한다.
sum 내용과 동일 
MIN(열이름 / * 불가능) : 해당열의 최솟값을 출력한다.
select min(a) from test : test의 a열의 최솟값을 출력한다
sum 내용과 동일
MAX(열이름 / * 불가능) : 해당열의 최댓값을 출력한다.
select max(a)  from test : test의 열의 최댓값을 출력한다.
sum 내용와 동일
DISTANT : 중복을 제거한다
select distant * from test : 테스트의 중복값을 제거하고 출력한다.
IN(값) : 값일 일치하는것만 출력
select * from a IN (1,2,3,4,5) : a의 값이 1,2,3,4,5 일치할경우 출력한다.
COALESCE(바꿀 값) : NULL값을 변경한다. 
select coalesce(a) from test;

속성(attribute)
NOT NULL : NULL 값을 허용하지 않는다
PRIMARY KEY : 기본키로 설정한다. 
기본키는 기본적으로 NOT NULL로 해야한다.
중복되지 않은 값으로 해야한다
UNIQUE : 중복되지 않은 값만 허용한다.

Group by 
특정 열을 기준으로 집계를 하고 자 할 때 사용
특정 조건을 충족하는 것만 select하고 싶다면 having
select * from test group by a : test 테이블을 a로 그룹을 만들어 출력한다.
 select * from test group by a having a > 5 : a의 값이 5가 넘는 것들만 그룹화 하여 출력한다.
뒤에 order by 를 사용하여 정렬해서 출력이 가능하다.

Subquery
SQL안의 또 다른 SQL을 의미한다.
()를 통해서 서브쿼리를 선언한다
(select 열이름 from 테이블명)
select * from test where a = (select no from test_2) : test a의 값이 test_2의 no의 값이 같을 때만 출력한다.
select 문이 아닌 update나 insert 등 다른데에서 사용가능하다
exists로 선언하여 서로 다른테이블의 값을 비교한다
select * from test where exists (select  * from test_2 where a  = no) : 서브쿼리 안에서 test a의 값과 test_2의 no가 같을 때 출력


인덱스(INDEX on)
어떤 데이터가 어디에 있다는 위치를 알고있는 주소록
주소로 접근하기 때문에 속도가 빠르다.
create index 인덱스이름 on 테이블명(열이름) : 테이블의 열이름에 맞는 인덱스를 생성한다.
create index test_index on test(a) : test테이블의 a를 index_test로 지정한다
show index from 인덱스테이블명 : 인덱스테이블을 출력한다.
EXPLAIN(possible keys, key) : 인덱스 확인
ex) explain select * from test_index;
drop index 인덱스명 on 테이블명 : 테이블 중에 인덱스명에 해당하는 인덱스를 삭제한다
ex) drop index test_index on test 

뷰(VIEW as)
가상테이블이다.
삽입, 삭제, 갱신, 연산이 가능하지만 제약이 따른다
ALTER VIEW로 뷰의 정의를 변경이 불가능하다.
기존정의된 테이블이 사라지면 뷰도 사라진다.
create view 뷰이름 as select 열이름 from 테이블명  : 뷰를 생성한다
ex) create view test_view as select * from test 
drop view 뷰이름 : 뷰를 삭제하는 명령어
ex) drop view test_view : test_view를 삭제한다.

조인(JOIN)
UNION : 합집합
select 열이름 from 테이블1 union select 열이름 from 테이블2 : 테이블1과 테이블2를 합집합한다.
ex) select * from test union select * from test_2 
합집합시 중복된 데이터는 지워진다.
중복 허용시 union all로 지정한다.
두 개의 테이블만 결합되는 것이 아닌 여러개의 테이블도 가능하다.
ex) select * from test union select * from test_2 union select * from test_3
INTERSECT : 교집합(mysql에서 지원안됨)
ex) select 열이름 from 테이블명  intersect select 열이름 from 테이블명2
EXCEPT : 차집합 (mysql에서 지원안됨)
ex) select 열이름 from 테이블명 EXCEPT select 열이름 from 테이블명2
select * from 테이블1, 테이블2, : 공집합
ex) select * from test,test_2
합집합은 두 개의 테이블을 합해서 출력하지만 공집합은 테이블X테이블을 하여 출력한다.
INNER JOIN : 두 개의 테이블을 합한다.
select 열이름 from 테이블명 inner join 테이블명2 on 비교값
ex) select * from test inner join test_2 on test.a = test_2.no 
열이름을 선언 할 때 테이블의 이름이 중복되지 않으면 테이블명을 생략할 수 있다.
ex  select * from test inner join test_2 on a = no 
합할 때 NULL값이 존재할 경우 해당 행은 무시하고 결합한다.
LEFT JOIN : 두 개의 테이블은 좌측 테이블 기준으로 합한다.
select 열이름 from 테이블명 left join 테이블명2 on 비교값
ex) select * from test left join test_2 on a = no
NULL값이 있어도 결합이 가능하다.
RIGHT JOIN   : 두 개의 테이블은 우측 테이블 기준으로 합한다.
select 열이름 from 테이블명 right join 테이블명2 on 비교값
ex) select * from test left join test_2 on a = no
NULL값이 있어도 결합이 가능하다.

