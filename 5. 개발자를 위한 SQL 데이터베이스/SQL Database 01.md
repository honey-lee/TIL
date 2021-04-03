# 개발자를 위한 SQL 데이터베이스 



## SQL로 하는 데이터 분석

### 01. 데이터베이스 기본 개념

#### 1. 데이터베이스와 테이블
   - `데이터베이스` : 일정한 체계 속에 저장된 데이터의 집합, 데이터베이스 내에 여러 개의 테이블이 존재할 수 있음(회원 정보, 상품 정보, 주문 정보...)
   - `테이블` : 데이터가 저장되는 기본 단위, 표 형태로 저장된 데이터의 집합
#### 2. 테이블의 row와 column
   - `row (행)` : 개체 하나를 나타내는 단위
   - `column (열)` : 각 개체가 가지는 속성 하나를 나타냄 

![image-20210310234222018](SQL Database 01.assets/image-20210310234222018.png)

#### 3. DMBS와 SQL
   - `DBMS` : DataBase Management System, 데이터베이스 관리 시스템, 데이터를 저장, 조회 등의 작업을 하게 해준다 
     - MySQL, SQLServer, Oracle, SQLite, MariaDB 등이 있음
   - `SQL` : Structured Query Language, DBMS에 명령을 내리기 위해 사용하는 언어, 국제 표준 SQL이 있어서 여러 DBMS간에 호환성이 있음

   ![image-20210313231713689](SQL Database 01.assets/image-20210313231713689.png)



#### 4. DBMS의 주요 구성 요소

   1. client(클라이언트 프로그램) : 사용자가 server에 접속해서 원하는 데이터베이스 관련 작업을 할 수 있도록, SQL을 입력할 수 있는 화면 등을 제공하는 프로그램 
   2. server(서버 프로그램) : client로부터 SQL문을 전달받아 데이터베이스 관련작업을 직접 처리하는 프로그램

   **DBMS를 사용한다는 것은 실행되고 있는 server에 client를 이용해서 접속한 후 원하는 명령을 내린다는 뜻**

![image-20210315225420047](SQL Database 01.assets/image-20210315225420047.png)


#### 5. 데이터베이스 생성하기 

   명령어 (CREATE DATABASE) + 데이터베이스 이름 입력

   상단 번개모양 클릭 후 좌측 새로고침 클릭

```MYSQL
CREATE DATABASE copang_main
```


#### 6. sys 데이터베이스
   - MySQL 서버의 성능 관련 정보들을 갖고있는 데이터베이스 



### 02. 테이블 생성하기 

#### 1. 테이블을 생성하는 법

   1. SQL 문으로 생성하기 

   2. CSV 파일 import 해서 테이블로 만들기 

      **CSV 파일** : Comma Separated Values의 줄임말로 데이터 분석 분야에서 사용되는 파일 형식

   ```SHELL
   # 1.
   데이터베이스 이름에 커서를 대고 마우스 오른쪽 버튼을 눌러 `Table Data Import Wizard` 클릭
   
   # 2.
   CSV 파일 import
   
   # 3.
   스패너 모양 아이콘 클릭하여 `Field Separator`를 `,`(콤마)로 설정 
   
   # 4. 
   Field type 확인하여 데이터와 일치여부 확인 및 조정 
   ex) int, double(소수), text 등
   
   # 5.
   SCHEMAS 탭의 새로고침 버튼 클릭
   테이블 옆에 dropdown 생성
   ```


#### 2. 생성된 테이블 살펴보기

   ```SHELL
   # 1.
   테이블 드롭다운 클릭해 테이블 명을 마우스 오른쪽 버튼 클릭
   
   # 2.
   스패너 아이콘 클릭
   
   # 3. 
   컬럼값과 datatype 볼 수 있음
   
   `datatype`: 
   1) int : 정수형
   2) double : 소수점도 표현 가능한 실수형
   3) text : 문자형
   ```



#### 3. Primary Key 설정하기 

   `id column` : 데이터를 식별하기 위해 임의로 부여된 id

   `primary key` : 테이블에서 하나의 row를 고유하게 식별할 수 있도록 해주는 기본 키. PK를 클릭하여 primary key로 설정할 수 있다. primary key에는 두 가지 종류가 있다.

   1. `Natural Key` : 실제로 어떤 개체가 갖고 있는 속성을 나타내는 컬럼이 Primary Key가 된 경우 (회원 정보 테이블이 있을 때 테이블의 email 컬럼이 primary key가 된 경우)
   2. `Surrogate Key` : id컬럼과 같이 테이블 내의 정보의 속성을 직접적으로 나타내는 컬럼이 아닌 인위적으로 생성된 컬럼이 primary key가 되는 경우 

   여러 가지 상황에 따라 위의 두 키 중 적절한 것이 primary key가 되지만 보통은 surrogate key가 선택되는 경우가 많음



#### 4. Not Null의 의미

- `Null` : 특정 컬럼에서 값이 존재하지 않는 상태, **숫자 0 과는 전혀 다른 개념이다, 숫자 0이 들어가 있다면 값이 있는 상태이다. 빈 문자열과도 다르다. 빈 문자열이 있다면 빈 문자열이 값으로 있는 상태이다**
- `NN(Not Null)` : 해당 컬럼에는 Null이 있으면 안된다 -> 이 컬럼에는 반드시 어떤 값이 들어있어야 한다. primary key로 설정될 경우 자동으로 NN도 설정된다



#### 5. Primary key와 Auto Increment 속성

- `AI (Auto Increment)` : 자동 증가 속성, id값을 1씩 증가시키면서 고유한 값을 부여하게 함



#### 6. DATE 타입

- 날짜 column의 경우 datatype을 `Date`로 설정해주어야 편리함 -> 1년 후 날짜 계산 등 데이터를 날짜로 취급 가능 



#### 7. Workbench

![image-20210321215927427](SQL Database 01.assets/image-20210321215927427.png)

​	1) 쿼리 창 생성 아이콘

​		1번 아이콘을 클릭하면 3번과 같이 SQL 문을 쓸 수 있는 SQL 에디터(우리는 '쿼리 창'이라고 부릅시다) 탭을 새롭게 열 수 있습니다. 		그	때마다 2번 영역에서 탭의 개수가 늘어나게 될 겁니다.

​	2) 쿼리 창 탭 

​		쿼리 창 생성 아이콘을 누를 때마다 이 영역에 존재하는 탭의 개수가 늘어나게 됩니다. 

​	3) 쿼리 창

​		SQL 문을 입력할 수 있는 공간입니다. 

​	4) SQL 문 실행 아이콘 

​		쿼리창에 입력한 SQL 문을 실행해줍니다. 저는 영상에서 매번 SQL 문을 실행할 때마다 직접 이 아이콘을 클릭해줄 건데요. 혹시 단축		키를 사용하고 싶으신 분은 '시프트 + 커맨드(윈도우는 컨트롤) + 엔터'를 치셔도 됩니다.

​	5) 새로고침 아이콘 

​		데이터베이스를 새로 생성하거나, 데이터베이스에 테이블을 새로 추가했을 때 새로고침 버튼을 눌러야 그것을 확인할 수 있습니다. 

​	6) 테이블 조회 아이콘

​		6번 영역을 자세히 보면 지금 다음과 같이 2개의 아이콘이 있습니다. 

​			![image-20210321220045128](SQL Database 01.assets/image-20210321220045128.png)

​		이 중에서

​		(1) 왼쪽의 스패너 모양 아이콘은 해당 테이블의 컬럼과 각 컬럼의 데이터 타입 등을 볼 수 있게 해주는 아이콘이고,

​		(2) 오른쪽의 표 모양의 아이콘은 테이블의 전체 row를 조회할 수 있게 해주는 아이콘입니다.

​		지금 위에 보이는 Workbench 화면의 이미지는 (2) 오른쪽의 표 모양의 아이콘을 클릭했을 때의 결과입니다. 

​	7) SQL 문으로 테이블의 데이터를 조회했을 때 그 조회 결과가 출력되는 영역입니다. 

​	8) SQL 문을 실행했을 때, 실행이 잘 되었는지 등에 관한 정보를 보여주는 영역입니다. 

​		지금 보면 가장 왼쪽에 초록불이 떠있는데요. 이는 SQL 문이 정상 실행되었다는 뜻입니다.



### 03. 데이터 조회로 기본 다지기

#### 1. 데이터 조회의 핵심, SELECT와 WHERE

```SQL
-- * : asterisk, 모든 값을 다 조회함 
-- FROM : 어느 테이블로부터 데이터를 조회하는지 나타냄
-- copang_main DB의 member 테이블
SELECT * FROM copang_main.member;

-- 특정 컬럼을 조회
SELECT email, age, address FROM copang_main.member;

-- WHERE : 특정 조건을 만족하는 ROW만 조회 
SELECT * FROM copang_main.member WHERE email = 'abc@naver.com';
```



#### 2. SQL 작성형식

##### 	1. SQL문은 항상 `세미콜론`으로 끝난다

##### 	2. SQL 문 안에는 공백이나 개행 등을 자유롭게 넣을 수 있다	

##### 	3. 대소문자 구분문자

- MySQL에 기본으로 내장된 키워드들 (예약어)는 대문자로, 나머지 부분은 소문자로 써준다, 대문자로 작성하지 않아도 실행에는 지장이 없지만 convention이다.

##### 4. 데이터베이스 이름과 테이블 이름

- `데이터베이스이름.테이블이름` 형식으로 작성
- `USE` 명령어를 통해 사용할 데이터베이스를 지정한 후에 사용도 가능 



#### 3. 조건을 나타내는 다양한 방법

```sql
-- 27세 이상의 회원 조회
SELECT * FROM copang_main.member WHERE age >= 27;

-- 30 ~ 39세 회원 (BETWEEN:~사이)
SELECT * FROM copang_main.member WHERE age BETWEEN 30 AND 39;

-- 30대가 아닌 회원 조회
SELECT * FROM copang_main.member WHERE age NOT BETWEEN 30 AND 39;

-- 숫자 형식이 아니라도 조회 가능, 2019년 1월 1일 이후 가입자 
SELECT * FROM copang_main.member WHERE sign_up_day > '2019-01-01';

-- 2019년에 가입한 회원 조회
SELECT * FROM copang_main.member WHERE sign_up_day BETWEEN '2019-01-01' AND '2019-12-31';
```



#### 4. 문자열 패턴 매칭 조건

```SQL
--주소가 서울인 회원들만 조회
SELECT * FROM copang_main.member WHERE address LIKE '서울%';
```



#### 5. 그 밖의 조건 표현식

##### 1) 같지않음 : `!=`, `<>`

##### 2) 이 중에 있는 : `IN`

##### 3) 한 글자를 나타내는 : `_`



#### 6. DATA 타입

1. 연도, 월, 일 추출하기 

```SQL
-- 1992년 출생 조회 (YEAR 함수 사용)
SELECT * FROM copang_main.member WHERE YEAR(birthday) = '1992';

-- 여름에 가입한 회원들 조회 (MONTH 함수)
SELECT * FROM copang_main.member WHERE MONTH(sign_up_day) IN (6, 7, 8);

-- 각 달의 후반부에 가입했던 회원들 조회 (DAY 함수) (15일/31일도 포함해서 조회됨)
SELECT * FROM copang_main.member WHERE DAY(sign_up_day) BETWEEN 15 AND 31;
```

2. 날짜 간의 차이 구하기 (`DATEDIFF` 함수, `CURDATE()`함수)

```SQL
-- DATEDIFF(날짜a, 날짜b)를 사용하면 '날짜 a-날짜b'를 해서 차이 일수를 알려줌'
SELECT email, sign_up_day, DATEDIFF(sign_up_day, '2019-01-01') FROM copang_main.member;

-- CURDATE() : 오늘 날짜를 기준으로 함
SELECT email, sign_up_day, CURDATE(), DATEDIFF(sign_up_day, CURDATE()) FROM copang_main.member;
```

3. 날짜 더하기 빼기 (`DATE_ADD()`, `DATE_SUB()`)

```sql
-- 가입일 기준으로 300일 이후의 날짜 구하기
SELECT email, sign_up_day, DATE_ADD(sign_up_day, INTERVAL 300 DAY) FROM copang_main.member;

-- 가입일 기준으로 250일 이전의 날짜 구하기
SELECT email, sign_up_day, DATE_SUB(sign_up_day, INTERVAL 250 DAY) FROM copang_main.member;
```

4. UNIX Timestamp 값

   > `UNIX Timestamp` : 1970년 1월 1일을 기준으로 총 몇초가 지냈는지 나타내는 값, 굉장히 큰 값으로 나타나기 때문에 읽을 수 있는 형태로 변환해주어야 하는데 이 때 사용하는 것이 `FROM_UNIXTIME` 함수이다

```sql
SELECT email, sign_up_day, UNIX_TIMESTAMP(sign_up_day) FROM copang_main.member;
```

![image-20210403153632177](SQL Database 01.assets/image-20210403153632177.png)

```SQL
SELECT email, sign_up_day, FROM_UNIXTIME(UNIX_TIMESTAMP(sign_up_day)) FROM copang_main.member;
```

![image-20210403153745009](SQL Database 01.assets/image-20210403153745009.png)



#### 7. 여러 개의 조건 걸기 

```sql
-- 성별이 남자이면서 주소가 서울이면서 나이가 25~29세인 회원 (AND, 조건을 동시에 만족할 때 조회)
SELECT * FROM copang_main.member WHERE gender = m AND address = '서울%' AND age BETWEEN 25 and 29;

-- 이 중 하나라도 조건을 만족하는 회원 구하기
SELECT * FROM copang_main.member WHERE MONTH(sign_up_day) BETWEEN 3 AND 5
	OR MONTH(sign_up_day) BETWENN 9 AND 11;
	
SELECT * FROM copang_main.member WHERE (gender = 'm' AND height >= 180)
	OR (gender = 'f' AND height >= 170);
```

**OR 사용시 주의점**

```sql
-- id가 1 혹은 2인 회원 조회
SELECT * FROM copang_main.member WHERE id = 1 OR id = 2;

-- 전체 row 출력됨
SELECT * FROM copang_main.member WHERE id = 1 OR 2;
-- id = 2 OR TRUE 로 인식되기 때문에
```

**AND과 OR간의 우선순위** : AND이 OR 보다 우선순위가 높아 먼저 실행된다

```SQL
-- 성별이 여자이거나 나이가 30세 미만이면서 키가 180이상인 회원들 
SELECT * FROM copang_main.member WHERE gender = 'f' OR age < 30 AND height > 180;

-- 성별이 여자이거나 나이가 30세 미만인 회원 중에 키가 180 이상인 회원들
SELECT * FROM copang_main.member WHERE (gender = 'f' OR age < 30) AND height > 180;
```



#### 8. 문자열 패턴 매칭 조건 사용 시 주의점

> 패턴 매칭 조건
>
> - LIKE
> - `%`
> - `_`

```sql
-- 역슬래쉬를 해당문자앞에 써주기

-- 문자로서의 % 나타내기 
SELECT * FROM copang_main.text WHERE sentence LIKE '%\%%';

-- 작은 따옴표 이스케이핑
SELECT * FROM copang_main.text WHERE sentence LIKE '%\'%';

-- 언더바 이스케이핑
SELECT * FROM copang_main.text WHERE sentence LIKE '%\_%';

-- 큰 따옴표 이스케이핑
SELECT * FROM copang_main.text WHERE sentence LIKE '%\"%\"%';


-----------------------------------------------------------------

-- 대소문자 구분하기 BINARY
SELECT * FROM copang_main.text WHERE sentence LIKE BINARY '%G%';
SELECT * FROM copang_main.text WHERE sentence LIKE BINARY '%g%';
```



#### 9. 데이터 정렬해서 보기

> 정렬 : row들을 특정 컬럼을 기준으로 순서대로 출력

```SQL
-- height 컬럼을 기준(오름차순)으로 row 출력, 기본으로 오름차순
SELECT * FROM copang_main.member
ORDER BY height (ASC);

-- 내림차순 정렬
SELECT * FROM copang_main.member
ORDER BY height DESC;

-- 여러개의 기준 두기(가입 연도 기준 내림차순 정렬, 다시 이메일 기준 오름차순 정렬)
SELECT * FROM copang_main.member
ORDER BY YEAR(sign_up_date) DESC, email ASC;
```



#### 10. 각 절의 작성 순서 지키기 & 정렬 시 주의점

1. **'SQL 문법 상 WHERE는 ORDER BY 앞에 나와야 한다'**

2. 정렬 기준의 데이터 타입이 숫자형인 경우와 문자형인 경우에 정렬 결과가 달라진다

   1. INT 타입의 값은 숫자의 대소를 기준으로 정렬
   2. TEXT 타입은 한 문자씩 그 문자 순서를 비교해 정렬 (120 - 19, 230 - 27), TEXT 타입인 컬럼의 숫자값들을 INT 형의 숫자 처럼 정렬하려면 `CAST`함수 사용

   ```SQL
   -- signed는 양수와 음수 포함 모든 정수를 나타낼 수 있는 데이터 타입
   SELECT * FROM test ORDER BY CAST(data AS signed) ASC;
   ```



#### 11. 데이터 일부만 추려보기 (LIMIT)

```sql
-- 가장 최근에 가입한 회원 10명만 추려보기 
SELECT * FROM copang_main.member 
ORDER BY sign_up_day DESC
LIMIT 10;

-- 최근에 9,10번째로 가입한 회원찾기 (row는 0번부터 카운팅됨)
SELECT * FROM copang_main.member 
ORDER BY sign_up_day DESC
LIMIT 8 2;
```



#### 12. LIMIT과 Pagination

- LIMIT과 Pagination은 서로 관계가 깊음 

```sql
-- Pagination 설정(가정)
1페이지 : SELECT * FROM db.search_result ~ ORDER BY registration_date DESC LIMIT 0, 10

2페이지 : SELECT * FROM db.search_result ~ ORDER BY registration_date DESC LIMIT 10, 10

3페이지 : SELECT * FROM db.search_result ~ ORDER BY registration_date DESC LIMIT 20, 10

4페이지 : SELECT * FROM db.search_result ~ ORDER BY registration_date DESC LIMIT 30, 10
```



