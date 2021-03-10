# Django 02

> - Model

## Model

- **웹 어플리케이션의 데이터를 구조화하고 조작하기 위한 도구** 
- 단일한 데이터에 대한 정보를 가짐
  - 사용자가 저장한 데이터들의 필수적인 필드들과 동작들을 포함
- 저장된 데이터베이스의 구조
- 
- 일반적으로 각각의 model은 하나의 데이터베이스 테이블에 매핑 (**model != database**, model이 더 큰 개념)



## Database

- DB
  - 체계화된 데이터의 모임
- 쿼리
  - 데이터를 조회하기 위한 명령어 
  - 조건에 맞는 데이터를 추출하거나 조작하는 명령어

### Database의 기본 구조

1. 스키마 (Schema)

   - 데이터베이스에서 자료의 구조, 표현방법, 관계 등을 정의한 구조
   - `PK(primary key)` : 기본 키 (아래의 경우 id), 조회를 위해 반드시 유니크한 값으로 설정해야함, django의 경우 자동적으로 유니크하게 관리됨 

   |  id  | name | age  |     phone     |     email      |
   | :--: | :--: | :--: | :-----------: | :------------: |
   |  1   | lee  |  15  | 010-1234-5678 | lee@naver.com  |
   |  2   | kim  |  25  | 010-7473-1273 | kim@naver.com  |
   |  3   | park |  20  | 010-2881-3828 | park@naver.com |

   

2. 테이블(Table)

   - 필드 / 컬럼 / 속성  => 열
   - 레코드 / 행 / 튜플  => 행



## ORM

- `Object-Relational-Mapping` : 객체 지향 프로그래밍 언어를 사용하여 **호환되지 않는 유형의 시스템 간에 (Django-SQL) 데이터를 변환하는 프로그래밍 기술**
- 파이썬 코드로서 SQL코드를 직접 작성하지 않고도 SQL에 접근 가능
- 장점
  - SQL을 잘 알지 못해도 DB조작이 가능 
  - SQL의 절차적 접근이 아닌 객체 지향적 접근으로 높은 생산성
- 단점
  - ORM만으로 완전한 서비스를 구현하기 어려운 경우가 있음
- **현대 웹 프레임워크의 요점은 웹 개발의 속도를 높이는 것 (생산성)**
- **우리는 DB를 객체로 조작하기 위해, 서로 다른 시스템 간의 호환성을 위해 ORM을 사용한다**



## Migrations

- django가 model에 생긴 변화(필드 추가, 모델 삭제/수정 등)를 반영하는 방법

- (중요!!!) Migration 실행 및 DB 스키마를 다루기 위한 명령어

  - `makemigrations` : model 변경사항에 기반한 새로운 마이그레이션 (like 설계도)을 만들 때 사용, 변경한 사항이 있을 때 무조건 해야하는 과정

  - `migrate` : 위에서 만든 마이그레이션을 실제 DB에 반영 (설계도 실제 DB 반영)
    - 모델에서의 변경 사항들과 DB의 스키마가 동기화를 이룸
  - `sqlmigrate` : 마이그레이션에 대한 SQL 구문을 보기 위해 사용
    - 마이그레이션이 SQL문으로 어떻게 해석되어서 동작할지 미리 확인
  - `showmigrations` : 프로젝트 전체의 마이그레이션 상태를 확인하기 위해 사용 
    - 마이그레이션 파일들이 migrate됐는지 안됐는지 여부를 확인할 때 사용

### 반드시 기억해야할 3 단계

> 1. models.py
>    - model 변경사항 발생
> 2. python manage.py migrations
>    - migrations 파일 생성
> 3. python manage.py migrate
>    - DB 적용



## Database API

> - DB를 조작하기 위한 도구 
> - django가 기본적으로 ORM을 제공함에 따른 것으로 DB를 편하게 조작할 수 있도록 도와줌
> - `Article.objects.all()` : `Class Name.Manager.Queryset API`의 구조
>   - `Manager` : django 모델에 데이터베이스 query 작업이 제공되는 인터페이스
>   - `QuerySet` : 데이터베이스로부터 전달받은 객체 목록



## CRUD

- 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능
- 데이터 베이스 조작의 목적
  - `Create(생성), Read(읽기), Update(갱신), Delete(삭제)`





