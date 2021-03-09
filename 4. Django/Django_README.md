# Django Intro 

## 설치 

```shell
# 최신 버전 설치
$ pip install django

# 버전 명시
$ pip install django==3.0.8
```

## 버전 확인 

``` shell
$ python -m django --version
```

## 프로젝트 생성 

```shell
# django-admin startproject 프로젝트이름 경로
# .을 적게되면 현재 경로에 바로 생성
# 안쓰면 폴더 하나 더 만들고 그 안에 생성 
$ django-admin startproject firstpjt . 
# admin 명령어가 작동하지 않을 경우
$ python -m django startproject firstpjt .
```
## gitignore  & README 작성하기 

`.gitignore`

`README.md`

## 프로젝트 폴더 구성

`settings.py`
- django의 설정 사항 

`urls.py`
- url과 함수를 연결
- 대장 url

`asgi.py`
- django가 비동기식 웹 서버와 연결하는 것을 도와줌

`wsgi.py`
- 웹 서버와 연결하는 것을 설정

## 프로젝트 실행 🚀
```shell
# 현재 경로에 manage.py가 있는지 확인이 필요
# 프로젝트 생성 이후에는 manage.py한테 전부 시킨다
$ python manage.py runserver
```

## 애플리케이션 생성

```shell
# python manage.py startapp 앱이름
# 이 때, 앱이름은 복수형으로 쓰는 것이 일반적이다!
$ python manage.py startapp articles
```

## 애플리케이션 등록

> 앱 생성 이후에는 반드시 등록! (잊어버리기 전에)
>
> 반드시 생성 후에 등록! (순서를 잘 지키자)
>
> 여러개의 앱이 있다면 settings에 등록된 순서대로 찾는다(템플릿 조회 순서, 위에 위치한 것을 찾으면 아래를 찾지 않고 바로 값을 보여준다)

```python
# 프로젝트메인폴더/settings.py
# firstpjt/settings.py

INSTALLED_APPS = [
    # 사용자 생성 앱
    'articles',

    # 3rd

    #built-in
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

## 애플리케이션 폴더

`migrations/`
- 마이그레이션 파일들이 들어감

`templates/`
- 탬플릿 폴더 (생성해야함!)
- `s` 오타주의! 

`models.py`

- 앱에서 사용하는 모델을 정의

`urls.py`

- 생성해야함!(url을 분리할 때!)

`views.py`

- url이랑 연결할 함수들을 정의

`admin.py`
- 관리자 페이지를 위한 설정 

`tests.py`

- 테스트 코드를 작성

`apps.py`

- 앱에 관한 설정 


---

## 요청 처리하기 

> HTTP request에 따라 각기 다른 동작을 결정
>
> - 메인 페이지 보여주세요 => 메인 페이지를 돌려준다
>
> - 회원가입 페이지 보여주세요 => 회원가입 페이지를 돌려준다
>

요청을 구분하는 2가지

- **url**
- **method**

url과 method의 조합으로 각기 다른 동작을 결정

### 요청하기 - (1) URL과 views 함수 연결하기 

모든 요청은 메인 프로젝트 폴더의 `urls.py`로 전달된다고 생각하자!

```python
from django.contrib import admin
from django.urls import path
#articles 라는 앱의 views 파이썬 파일을 불러오고
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
    #불러온 view파일의 함수를 개발자가 의도한 url과 연결
    path('index/', views.index),
]
```



### 요청 처리하기 - (2) views함수 작성하기

```python
def index(request): # 첫번째 인자는 반드시 request
    return render(request, 'index.html') # render 함수의 첫번째 인자는 반드시 request
```



### 요청 처리하기 - (3) template 작성하기 

> `index.html`은 반드시 `articles`라는 앱의 `templates` 폴더에 위치해야 한다

```python
{% extends 'base.html' %}

{% block content %}
  <h1>Hello</h1>
  <h2>만나서 반가워요 {{ name }}님!!!</h2>

  <a href="{% url 'index' %}">뒤로</a>
{% endblock %}
```



정리) 기본적인 요청 처리 순서(uvt)

1. url - 함수 연결하기 
2. views - 함수 작성하기
3. templates - 함수의 동작에 따른 템플릿 작성

장고 디자인 패턴 (MTV - MVC)

1. Model
2. Template
3. View

## Django Template Language

> 파이썬 문법과는 별개의 문법이다

### DTL - Variable : {{ }}
render()를 사용하여 views.py에서 정의한 변수를 template 파일로 넘겨 사용

### DTL - Filter : |
표시할 변수를 수정할 때 사용

### DTL - Tag : {% %}
반복문 실행 

- for
- if
- extends
- block
- comment
- url : {% url '별명' %}

### DTL - Comments : {# #}
HTML 주석은 개발자 도구에 표시되고 
DTL comment는 표시되지 않는다 

## 템플릿 상속하기 

```python
# settings.py
# BASE_DIR / 'subdirectory' / 상속대상
'DIRS' = [BASE_DIR / 'firstpjt' / 'template']
'DIRS' = [BASE_DIR / 'template']
```