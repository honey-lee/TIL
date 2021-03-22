# Django 04

> - Authentication & Authorization
>   - Authentication : 인증
>   - Authorization : 권한, 허가 



## Django Authentication System

- 인증과 권한 부여를 함께 제공하며, 어느 정도 결합되어 있기 때문에 일반적으로 authentication system(인증 시스템)이라고 함
- **User object**(유저에 대한 인증)와 **Web request**(요청에 대한 인증)



### Authentication in Web requests

- django는 세션과 미들웨어를 사용하여 인증 시스템을 request 객체에 연결
- 이를 통해 사용자를 나타내는 모든 요청에 `request.user`를 제공
- 현재 사용자가 로그인하지 않는 경우 `AnonymousUser`클래스의 인스턴스로 설정되며, 그렇지 않으면 `User`의 인스턴스로 설정됨 



## Login & Logout

### 로그인

 - Session을 Create하는 로직과 같음 
 - `login()`
   - 현재 세션이 연결하려는 인증된 사용자가 있는 경우 login()함수로 로그인 진행
   - request 객체와 User 객체를 통해 로그인 진행
   - Django의 session framework를 통해 사용자의 ID를 세션에 저장 



### 로그 아웃

- Session을 Delete 하는 로직과 같음
- `logout()`
  - request 객체를 받으며 return이 없음
  - 현재 요청에 대한 DB의 세션 데이터를 삭제하고 클라이언트 쿠키에서도 `sessionid`를 삭제



#### (참고) HTTP

- 웹 상에서 이루어지는 모든 데이터 교환의 기초
- 클라이언트 - 서버의 구조
- 요청
  
  - 클라이언트에 의해 전송되는 메시지
- 응답
  
  - 서버에서 응답으로 전송되는 메시지
- **특징**
  
  - 비연결지향
    
    - 서버는 응답 후 접속을 끊음
  - 무상태
    
    - 접속이 끊어지면 상태를 저장하지 않음
    
    

#### Cookie

- 서버가 사용자의 웹 브라우저에 전송하는 작은 데이터 조각 
- 브라우저는 전송 받은 쿠키를 로컬에 key-value의 데이터 형식으로 저장 
  - 동일한 서버에 재요청 시 저장된 쿠키를 함께 전송 
- 웹 페이지에 접속하면 요청한 웹페이지를 받으며 쿠키를 로컬에 저장함
- 쿠키의 목적
  1. 세션 관리
     - 로그인, 아이디 자동완성, 공지 하루 안보기, 팝업 체크, 장바구니 등의 정보 관리
  2. 개인화
     - 사용자 선호, 테마 등의 개인 세팅
  3. 트래킹
     - 사용자 행동을 기록 및 분석하는 용도 

##### lifetime

1. session cookie
   - 현재 세션이 종료되면 삭제
   - 브라우저는 현재 세션이 종료되는 시기를 정의
   - 일부 브라우저는 다시 시작할 때 세션 복원을 사용해 계속 지속될 수 있도록 함
2. permanent cookie
   - Expires 속성에 지정된 날짜가 되면 사라짐 



#### Session

- 사이트와 특정 브라우저 사이의 상태를 유지시키는 것
- 클라이언트가 서버에 접속하면 서버가 특정 session id를 발급하고 클라이언트는 session id를 쿠키를 사용해 저장, 클라이언트가 다시 서버에 접속할 때 해당 쿠키를 이용해 요청을 보냄
- Django는 특정 session id를 포함하는 쿠키를 서용해서 저장 (`django.contrib.sessions`)



###### **Cookie는 클라이언트 로컬 파일에 저장, Session은 서버에 저장됨**

###### 결론적으로 **HTTP 쿠키는 상태가 있는 세션을 만들도록 해준다**













## Django의 2가지 HTML input 요소 표현 방법

1. Form fields

   - input에 대한 유효성 검사 로직을 처리하며 템플릿에서 직접 사용됨

2. Widgets : django의 HTML input element 표현

   - HTML 렌더링을 처리

   - 웹 페이지의 HTML input 요소 렌더링 및 제출된 원시 데이터 추출을 처리
   - 하지만 widgets은 반드시 form fields에 할당됨
   - Form Fields는 input 유효성 검사를 처리, widgets는 웹페이지에서 input element의 단순 raw한 렌더링 처리



## ModelForm Class 작성

```python
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    # 데이터에 대한 데이터(모델 클래스에 대한 정보 등록)
    class Meta:
        # form이 어떤 모델을 기반으로 만들어지는지 정의
        model = Article
        # field 전체를 들고오기
        fields = '__all__'
        # field에서 일부 지정하여 들고오기
        fields = ('title', 'content')
```



### Form & ModelForm

- Form
  - model에 연관되지 않은 데이터를 받을 때 사용
  - cleaned_data 딕셔너리를 생성해 정보를 받아와야 함
- ModelForm
  - django가 해당 model에서 양식에 필요한 대부분의 정보를 이미 정의
  - 어떤 레코드를 만들어야 할지 알고 있으므로 바로 `.save()` 호출 가능 



## Django View Decorators

- decorator
  - 어떤 함수에 기능을 추가하고 싶을 때, 해당 함수를 수정하지 않고 기능을 **연장**해주는 함수
- Allowed HTTP methods
  - 요청 메서드에 따라 view함수에 대한 액세스를 제한
  - 요청이 조건을 충족시키지 못하면 `HttpResponseNotAllowed`를 return
  - `require_http_methods()`, `require_GET()`, `require_POST()`, `require_safe()`

```python
# 함수 위에 데코레이터를 붙여서 사용
@require_http_methods(['GET', 'POST'])
def func(request):
```



## static

> static files(정적 파일) : 웹 사이트의 구성 요소 중에서 image, css, js파일과 같이 해당 내용이 고정되어 응답을 할 때 별도의 처리 없이 파일 내용을 그대로 보여주면 되는 파일
>
> 즉, 사용자의 요청에 따라 내용이 바뀌는 것이 아니라 요청한 것을 그대로 응답하면 되는 파일 
>
> - 기본 static 경로 
>   - app_name/static/

![image-20210318144705484](Django 03.assets/image-20210318144705484.png)

![image-20210318144736342](Django 03.assets/image-20210318144736342.png)

```python
{% load static %}
<img src="{% static 'articles/sample.png' %}" alt="sample">
```







