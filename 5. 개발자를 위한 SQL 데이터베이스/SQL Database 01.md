# 개발자를 위한 SQL 데이터베이스 



## SQL로 하는 데이터 분석

### 01. 데이터베이스 기본 개념

1. 데이터베이스와 테이블
   - `데이터베이스` : 일정한 체계 속에 저장된 데이터의 집합, 데이터베이스 내에 여러 개의 테이블이 존재할 수 있음(회원 정보, 상품 정보, 주문 정보...)
   - `테이블` : 데이터가 저장되는 기본 단위, 표 형태로 저장된 데이터의 집합
2. 테이블의 row와 column
   - `row (행)` : 개체 하나를 나타내는 단위
   - `column (열)` : 각 개체가 가지는 속성 하나를 나타냄 

![image-20210310234222018](SQL Database 01.assets/image-20210310234222018.png)

3. DMBS와 SQL
   - `DBMS` : DataBase Management System, 데이터베이스 관리 시스템, 데이터를 저장, 조회 등의 작업을 하게 해준다 
     - MySQL, SQLServer, Oracle, SQLite, MariaDB 등이 있음
   - `SQL` : Structured Query Language, DBMS에 명령을 내리기 위해 사용하는 언어, 국제 표준 SQL이 있어서 여러 DBMS간에 호환성이 있음
   
   ![image-20210313231713689](SQL Database 01.assets/image-20210313231713689.png)



4. DBMS의 주요 구성 요소

   1. client(클라이언트 프로그램) : 사용자가 server에 접속해서 원하는 데이터베이스 관련 작업을 할 수 있도록, SQL을 입력할 수 있는 화면 등을 제공하는 프로그램 
   2. server(서버 프로그램) : client로부터 SQL문을 전달받아 데이터베이스 관련작업을 직접 처리하는 프로그램

   **DBMS를 사용한다는 것은 실행되고 있는 server에 client를 이용해서 접속한 후 원하는 명령을 내린다는 뜻**

![image-20210315225420047](SQL Database 01.assets/image-20210315225420047.png)

5. 데이터베이스 생성하기 

   명령어 (CREATE DATABASE) + 데이터베이스 이름 입력

   상단 번개모양 클릭 후 좌측 새로고침 클릭

```MYSQL
CREATE DATABASE copang_main
```

6. sys 데이터베이스
   - MySQL 서버의 성능 관련 정보들을 갖고있는 데이터베이스 



### 02. 테이블 생성하기 

1. 테이블을 생성하는 법
   1. SQL 문으로 생성하기 
   2. CSV 파일 import 해서 테이블로 만들기 