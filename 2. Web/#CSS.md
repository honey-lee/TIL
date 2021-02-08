# CSS

> cascading style sheet
>
> 스타일, 레이아웃 등을 통해 문서(HTML)를 표시하는 방법을 지정한 언어
>
> HTML과 CSS는 각각의 문법을 가지는 별개의 언어이다. 하지만 HTML은 CSS없이도 작성가능한 반면에 CSS는 HTML이 있어야 작성할 수 있다.



## CSS 구문

```CSS
h1 {                 #선택자
    color: blue;     #선언문(속성 : 값)을 선언
    font-size: 15px;
}
```



## CSS 정의방법

1. 인라인 - 해당 태그에 직접 <style>지정

2. 내부 참조 - head 태그 내에 <style> 지정

3. 외부 참조 - 분리된 CSS파일, 단독적인 파일이 있어 head에 link tag를 이용해서 연결한다, **가장 많이 사용되는 방법**

   <link rel="stylesheet" href="mystyle.css">



## CSS Selectors

> HTML 문서에서 특정한 요소를 선택하여 스타일링 하기 위해서는 반드시 `선택자`라는 개념이 필요하다. 

1. 기본 선택자 : 개별 선택만 가능 
   - 전체 선택자(`*`), 요소 선택자 (`h1` , `p`, `a` 등)
   - 클래스 선택자, 아이디 선택자, 속성 선택자
     - **Class 선택자** : 클래스 선택자는 마침표(.) 문자로 시작하며 해당 클래스가 적용된 문서의 모든 항목을 선택
     - **id 선택자** : `#`문자로 시작하며 기본적으로 클래스 선택자와 같은 방식으로 사용, 그러나 id는 문서 당 한 번만 사용할 수 있으며 요소에는 단일 id값만 적용할 수 있다.
     
     |            | class                    | id                       |
     | ---------- | ------------------------ | ------------------------ |
     | HTML표기법 | <p class="big-text"></p> | <p id="best-text"></p>   |
     | CSS 표기법 | .big-text {color: blue;} | #best-text{color: blue;} |
     |            | 중복 클래스 가능         | 중복 아이디 불가         |
     |            | 여러 요소 가능           | 한 요소만 가능           |
   
   
   
2. 결합자 : 여러 개를 선택
   - 자손 결합자, 자식 결합자
   - 일반 형제, 인접 형제 결합자
   
3. 의사 클래스 / 요소



**CSS 적용 우선순위**

- !important > Inline style(태그 안에 직접 작성) > id 선택자 > Class 선택자 > 요소 선택자 > 소스 순서

- 대부분의 경우 다른 상위 상속자 보다는  **class 선택자**가 사용된다 



## CSS 상속

- CSS는 상속을 통해 부모 요소의 속성을 자식에게 상속한다.
- 속성 중에는 상속이 되는 것과 되지 않는 것들이 있다.
  - 상속되는 것 : Text관련 요소(font, color), opacity, visibility
  - 상속되지 않는 것 : Box model(width, height, padding), position(position, top/right/bottom/left, z-index)



## CSS 단위

상대 크기 단위

- px(픽셀)
- % : 전체 브라우저 크기에 대한 퍼센트 
- em
  - 배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈를 가짐
- rem
  - 최상위 요소(html)의 사이즈를 기준으로 배수 단위를 가짐 
    - **html의 최상위 폰트 사이즈는 16px**

|           em           |       rem        |
| :--------------------: | :--------------: |
| 부모요소의 사이즈 기준 | html 사이즈 기준 |

- Viewport 기준 단위



## 색상 단위

1. 색상 키워드
2. RGB 색상
3. HSL 색상

```HTML
#색상 키워드
p{ color: black; }
#font-color가 아닌 color이다.

#RGB 색상
p{ color: #000; }
p{ color: rgb(0, 0, 0);}
```



## 📌CSS Box model

> HTML에서는 모든 것을 '네모'로 바라봐야 한다.
>
> 또 모든 것이 네 방향이다 

1. 구성

   `Margin > Border > Padding > Content`

   - Margin : 테두리 바깥의 외부 여백
   - Border : 테두리 영역
   - Padding : 테두리 안쪽과 컨텐츠 사이의  여백
   - content : 글이나 이미지 등 요소의 실제 내용 

2. 방향

   `top, bottom, left, right`

   - 한개만 쓰면 : 상하좌우 적용
   - 두개 쓰면 : 상하 / 좌우
   - 세개 쓰면 : 상 / 좌우 / 하
   - 네개 쓰면 : 상 / 우 / 하 / 좌 (시계 방향)

3. sizing
   
   - 기본적으로 모든  요소의 `box-sizing`은 `content box`
4. Box model
   
   - 마진 상쇄 : 인접 형제 요소 간의 margin이 겹쳐서 보임 (상하로만 적용되며 좌우로는 발생하지 않음)

**box-sizing**

1. content box : 기본적으로 모든 요소의 box-sizing은 content-box
2. border box : padding을 제외한 순수 contents 영역만을 box로 지정



## CSS Display

- `display` : `block`
  - 줄 바꿈이 일어나는 요소
  - 화면 크기 전체의 가로 폭을 차지한다
  - 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음
  - 대표적인 블록 레벨 요소 
    - div / ul, ol, li / p / hr / form 등
    - 블록은 기본 너비의 100%
- `display` : `inline-block`
  - block과 inline 레벨 요소의 특징을 모두 갖는다
  - inline 처럼 한 줄에 표시 가능하며 
  - block처럼 width, height, margin 속성을 모두 지정할 수 있다.
- `display` : `none`
  - 해당 요소를 화면에 표시하지 않음 (공간조차 사라진다)
  - 이와 비슷한 visibility : hidden은 해당 요소가 공간은 차지하나 화면에 표시만 하지 않는다

```html
#인라인 요소 수평 정렬
margin-left: auto;
margin-right: auto;

#블록 요소 수평 정렬
text-align: center;
```



## CSS Position

[참고][https://developer.mozilla.org/ko/docs/Web/CSS/position]

`static` : `top`, `left`와 같은 명령어가 영향을 주지 않음

`relative` : 자기 자신을 기준으로 `top`, `left`, `right`등 오프셋 지정 , 공간을 차지함

`absolute` : 가장 가까운 위치 지정 조상 요소에 대해 상대적으로 배치 -> 부모요소에서 `static`이 아닌요소를 찾아서 기준으로 함 

공중에 붕 뜬것 처럼 레이아웃 공간도 차지하지 않음

`fixed`: 특정 위치에 고정



참고) `z-index`: 겹쳐보일 때 z축을 움직여서 위로 보내기