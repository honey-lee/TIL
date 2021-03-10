# Django 01

> Dynamic Web Application Program
>
> - `static web` : 미리 저장된 정적파일(HTML, CSS, JS)을 제공, 사용자에게 보여줄 것을 미리 준비했다가 그대로 보여주는 웹사이트
> - `Dynamic web` : 사용자의 요청의 변화에 따라 일하는 server-side의 작업 (`SQL`을 통해 데이터 베이스 처리를 함), client-side의 작업(정적파일)은 이미 준비되어 있음
>
>  `Python Web Framework` : 웹페이지를 개발하는 과정에서 겪는 어려움을 줄이는 것이 주목적, 기본적인 구조와 코드들을 제공해줌

 - spotify, Instagram, Dropbox, Delivery hero 등에서 사용됨
 - ridiculously fast, fully loaded, reassuringly secure, exceedingly scalable, incredibly versatile

## 디자인 패턴

`MVC` : 모델-뷰-컨프롤러 (소프트웨어 디자인 패턴)

django의 `MTV` 패턴
|    Model     |  데이터 베이스 관리  |
| :----------: | :------------------: |
| **Template** |    레이아웃(화면)    |
|   **View**   | 중심 컨트롤러 (심장) |



## 명령어

`django-admin startproject 프로젝트이름` : 프로젝트 생성

`python manage.py runserver` : 서버 구동 

`python manage.py startapp articles` : 앱 시작하기

## 생성되는 파일


- `__init__.py` : 개별요소에 패키지처럼 접근하게 해준다 
- `asgi.py` : 비공개 웹사이트와 연동 시 사용
- `settings.py`
- *`urls.py` : 사용자의 요청을 가장 먼저 맞닥뜨림 
- `wsgi.py` : 배포 시 사용
- `admins.py` : 관리파일
- `apps.py` 
- *`models.py` : MTV에서 `M`을 담당
- `tests.py` : 테스트 코드 작성
- *`views.py` : MTV에서 `V, 즉 중간관리자`의 역할 담당
- Template은 자동 생성되지 않음!!! 별도로 `templates` 폴더를 생성해서 만들어줘야 한다 이 때 이름은 반드시 `templates`여야한다.

## 웹사이트 동작 방식

![image-20210308093807222](C:\Users\leejo\AppData\Roaming\Typora\typora-user-images\image-20210308093807222.png)

> - 웹 브라우저 주소창에 URL 입력 후 엔터
> - URL을 이용해서 서버의 IP를 찾는다
> - IP를 이용해서 서버에 접속
> - URL에 해당하는 자료를 요청
> - 웹 어플리케이션이 URL을 해석해서 해당하는 코드가 동작
> - 코드의 동작 결과를 응답으로 돌려줌
> - 서버가 웹브라우저를 데이터로 보내줌
> - 웹 브라우저 응답받은 데이터를 화면에 표시 
> - JS(AJAX)

## Views.py

**view함수의 첫번째 인자는 반드시 `request`이다**



## Template

- 우리에게 보여지는 화면을 표현함
- 데이터 표현을 제어하는 도구이자 표현에 관련된 로직
- 사용하는 built-in system : `DTL, django template language`
  - 조건, 반복, 변수, 치환, 필터 등의 기능을 제공
  - 프로그래밍적 로직이 아니라 프레젠테이션을 표현하기 위한 것 
  - 파이썬과 문법구조가 비슷하지만 파이썬 프로그래밍이 실행되는 것은 아님 

### DTL syntax 

1. variable
   1. `{{ variable }}`
   2. render()를 사용하여 views.py에서 정의한 변수를 template 파일로 넘겨 사용
   3. `dot(.)`를 사용하여 변수 속성에 접근할 수 있음
   4. render()의 세번째 인자로 {'key' : 'value'}와 같이 딕셔너리 형태로  표현
2. Filters
   1. `{{ variable|filter }}`
   2. 표시할 변수를 수정할 때 사용
   3. chained가 가능하며 일부 필터는 인자를 받기도 함 
      1. `{{ variable|truncatewords:30 }}` : 변수를 30자까지만 잘라서 출력하겠다는 의미 
3. Tags
   1. `{{ %tag% }}`
   2. 출력 텍스트를 만들거나, 반복 또는 논리를 수행하여 제어 흐름을 만드는 등 변수보다 복잡한 일들을 수행
   3. 일부 태그는 시작과 종료 태그가 필요
4. Comments
   1. `{# lorem ipsum #}`
   2. django template에서 줄의 주석을 표현하기 위해 사용
   3. 한 줄 주석에만 사용할 수 있음

## 디자인 패턴 

개발 설계 상 발생하는 문제를 해결하기 위한 해결책 (디자이너, 프론트, 엔드를 분리)

MTV : Model(데이터베이스), Template(화면-프론트), View(계산, 처리-백엔드)



## Template inheritance

> - 기본적으로 코드의 재사용성에 초점을 맞춤
> - 템플릿 상속을 사용하면 사이트의 모든 공통 요소를 포함하고 하위 템플릿이 재정의(override)할 수 있는 블록을 정의하는 기본 'skeleton' 템플릿을 만들 수 있음

### Tags

- `{% extends %}` : 자식 템플릿이 부모 템플릿을 확장한다는 것을 알림

  - 반드시 템플릿 최상단에 작성

- `{% block %}` : 하위 템플릿에서 재지정(override)할 수 있는 블록을 정의

  - 즉, 하위 템플릿이 채울 수 있는 공간

  

## Template system 설계 철학

### 표현과 로직을 분리

- 템플릿 시스템은 표현을 제어하는 도구이자 표현에 관련된 로직일 뿐 
- 기본 목표를 넘어서는 기능을 지원하지 말아야 한다

### 중복을 배제

- 대다수의 동적 웹사이트는 공통 header, footer, navbar같은 공통 디자인응ㄹ 갖는다
- 이러한 요소를 한 곳에 저장하기 쉽게 하여 중복 코드를 없애야 한다
- 이것이 템플릿 상속의 기초가 되는 철학 



## HTML form

> 웹에서 사용자 정보를 입력하는 여러 방식 (text, button, checkbox, file 등)을 제공하고 , 사용자로부터 할당된 데이터를 서버로 전송하는 역할을 담당
>
> - 핵심 속성
>   - action : 입력데이터가 전송될 URL 지정
>   - method : 입력데이터 전달 방식 지정, method 지정 안하면 기본적으로 `get`이 디폴트

### HTML input element

- 사용자로부터 데이터를 입력받기 위해 사용
- type 속성에 따라 동작 방식이 달라짐
- 핵심 속성
  - name
  - 중복 가능, 양식을 제출했을 때 name이라는 이름에 설정된 값을 넘겨서 값을 가져올 수 있음
  - 주요 용도는 GET/POST 방식으로 서버에 전달하는 파라미터(name은 key, value는 value로)로 `?key=value&key=value`형태로 전달 
    - ex) 네이버와 구글에 삼성을 검색하면 각각 다음과 같은 파라미터로 넘어간다 `?query=삼성`, `?q=삼성`

### HTTP

- HyperText Transfer Protocol (secure)
- 웹에서 이루어지는 모든 데이터 교환의 기초
- 주어진 리소스가 수행할 원하는 작업을 나타내는 request methods를 정의
- HTTP request method 종류
  - GET, POST, PUT, DELETE....

#### HTTP request method - get

- 서버로부터 정보를 **조회**하는데 사용 (대표적으로 검색할 때 사용, 데이터에 접촉 X)
- 데이터를 가져올 때만 사용해야 함
- 데이터를 서버로 전송할 때 body가 아닌 Query String parameters를 통해 전송

## URL

### Django URLs

- app의 view함수가 많아지면서 사용하는 path() 또한 많아지고 app 또한 더 작성되기 때문에 프로젝트의 urls.py에서 모두 관리하는 것은 코드 유지보수에 좋지 않음
- 이제는 각 app에 urls.py를 작성하게 됨 