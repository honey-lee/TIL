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

























