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