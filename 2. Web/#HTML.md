# HTML / CSS

> Web을 왜 배워야 할까?
>
> SW개발 방법 및 전반적인 학습 과정을 익히기 위해서 

## 웹 표준

현재의 웹 표준 : W3C, WHATWG 현재 웹에 대한 표준이 둘로 나뉘어져있지만 사실 상 대세는 WHATWG이다.

표준에 대한 점수를 매길 수 있는 사이트 (HTML5test)

## HTML이란

HTML : Hyper Text(정보가 동일선상이 아닌 다중으로 연결되어 있는 상태의 문서들, 사용자가 한 문서에서 다른 문서로 자유롭게 이동할 수 있다) Markup Language (태그 등을 이용하여 문서나 데이터의 구조를 명시하는 언어, 단순히 데이터를 표현)

​	ex) HTML, Markdown

- 웹 페이지를 작성하기 위한 언어
- **웹 컨텐츠의 의미와 구조를 정의**
- 최초 웹사이트 (참고)[info.cern.ch](유럽입자 물리 연구소, 첫 웹사이트)

## HTML 기본 구조

> <시작태그>내용</종료태그>
>
> `head`와 `body`부분으로 나누어진다

```HTML
<!DOCTYPE html>                    #웹브라우저에게 HTML 버전을 알려주는 역할
<html lang="en">							   #html의 최상위 요소(루트)
<head>
<title>My first Website</title>    #제목
<meta charset="utf-8">             #한글을 포함하는 대표적인 인코딩    
</head>
<h1>My First Page</h1>             #가장 큰 머릿말
<h2>I love HTML!</h2>              #두 번째로 큰 머릿말
<p>                                #문단
   Lorem ipsum dolor sit amet, .....
   이 부분은 <b>굵게</b>
   이 부분은 <i>날려서</i> 써주세요
</p>
</html>
```

```html
#굵게 표현
<b></b>  
#굵게 + 강조 
<strong></strong> 
#기울이기
<i></i>
#기울이고 강조(emphasize)
<em></em>
```



**DOM 트리**

> 각각의 태그들을 객체지향적으로 표현한 것 
>
> `부모 형제 관계`로도 표현한다



## **HTML 주요태그**

> `! tab` 누르면 기본적인 html 구성을 자동 구성해줌

> 	<html>
> 	<head>
> 	<style>
> 	</style>
> 	</head>
> 	<body>
> 	</body>
> 	</html>

1) HEAD

- 문서제목, 문자코드와 같이 해당 문서 정보를 담음

- `head` 부분은 브라우저에 나타나지 않는다 

- 링크를 보낼 때 과거에는 페이지만 보냈다면 최근엔 헤드에 들어있는 메타 데이터를 함께 보낸다. 

2) BODY

- 홈페이지에 보여질 부분을 감싸는 태그

3) html

- 모든 코드 내용 전체를 감싸서 html 코드임을 선언

4) a

- 하이퍼링크, 연결될 주소를 지정함
- 인라인 요소(컨텐츠 너비만큼만 공간차지)

```html
#외부 페이지로 연결
<a href="https://google.com">구글로 가는 링크</a>
#새로운 탭이 열림
<a href="https://google.com"target="_blank">구글로 가는 링크</a>
#홈페이지 내 이동
<a href="folder1/folder2/page2.html"</a>
#상위폴더로  ../
<a href="../index.html"</a>
```

5) img

- 이미지를 넣음
- 종료태그 없음

```html
<img src="https://이미지소스" width="300">
#width, height를 통해 이미지 크기 조정 가능, 자동비율 조정 적용
#width, height % 설정도 가능

#보유중인 이미지 사용 (이미지 경로 작성)
<img src="images/ice_cream.jpg"> 
```

6) div

- 구역을 나눠서 묶어주고 싶은 요소들을 감싸줌

7) link

- CSS 코드와 연결할 때 사용

```HTML
<link href="css/styles.css" rel="stylesheet">
```



**시맨틱 태그**

> 의미론적 요소를 담은 태그
>
> `header` , `nav`, `aside`, `section`, `article`, `footer`
>
> 의미가 명확해져 읽기 쉽고, 유지보수가 용이하다 
>
> 접근성도 높아진다 -> 검색엔진이 자동으로 전체 웹 태그를 분석해서 사용자에게 정리해서 보여줌
>
> 검색엔진최적화(SEO+)



**그룹 컨텐츠**

> `<p>` 
>
> `<hr>`
>
> `<ol>, <ul>` : 리스트 (번호 유무)
>
> `<pre>, <blockquote>` : 인용문
>
> `<div>`

**HTML style guide**

1) 공백 없고

2) 쌍따옴표 사용



table

```html
<tr></tr>, <td></td>, <th></th>
```



**중요** `<form>` 

- 서버에서 처리될 데이터를 제공하는 역할 -> 검색, 로그인
- 기본 속성
  - action
  - method

[developer.mozilla.org](웹 관련된 공식 문서, 튜토리얼)

- form 태그 내에 여러 `input` 태그가 있어서 실질적으로 데이터를 보내준다 -> password, checkbox



## 클라이언트와 서버

> 클라이언트 : 요청하는 컴퓨터  (프론트엔드)  
>
> - html, css (페이지를 꾸며주는 마크업 언어)
> - javascript(저장, 조건, 반복이 있는 프로그래밍 언어)
>
> 서버 : 요청을 들어주는 컴퓨터 (백엔드)
>
> - python, django



## URL의 구성

>  접근할 수 있는 정보의 위치를 명확하게 표현 

https://www.airbnb.co.kr/s/homes

프로토콜/ 도메인 / 정보의 위치 


