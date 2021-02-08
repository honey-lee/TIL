# CSS 심화

## CSS layout

> 웹 페이지에 포함되는 요소들을 취합하고 그것들이 어디에 놓일지 배치하는 기술 
>
> - Display
> - Position
> - Float
> - Flexbox
> - Grid



## Float

> - 이미지 좌,우측 주변으로 텍스트를 둘러싸는 레이아웃을 위해 도입
>
> - 더 나아가 이미지가 아닌 다른 요소들에도 적용해 웹 사이트의 전체 레이아웃을 만듬



**속성**

- none : 기본값
- left : 요소를 왼쪽으로 띄움
- right : 요소를 오른쪽으로 띄움



## Flexbox

> `CSS Flexible Box Layout`
>
> - 공간 배분과 정렬 기능을 위한 **1차원(단방향)** 레이아웃
>   - 요소
>     - container : container를 통해 조작
>     - item
>   - 축
>     - main axis(가로축)
>     - cross axis(세로축)



**속성**

- 부모 요소에 display: flex 혹은 inline: flex를 작성하는 것으로 시작

- 배치 방향 설정

  - `flex-direction`
    - row(default) (오른쪽으로)
    - row-reverse (왼쪽으로)
    - column (아래로)
    - column-reverse (위로)

- 메인축 방향 정렬

  - `justify-content`

- 교차축 방향 정렬

  - `align-items`, `align-self`, `align-content`

  

- 여러줄 : `content`

- 한 줄 : `items`

- flex-item 개별 요소 : `self`

- 감싸주기 : `flex-wrap`

- 남는 공간 분배: `flex-grow`

- 순서 (값이 작을 수록 앞으로): `order`

- `flex-flow`: `flex-direction`과 `flex-wrap`의 shorthand



## Bootstrap

> Build fast, responsive sites with Bootstrap
>
> one source, multi use : 하나의 코드로 다양하게 작동



**CSS 초기화**

> 부트스트랩 사용 시 기본적인 설정(마진값, 폰트 크기 등)이 다르다. 브라우저마다 디폴트 설정이 다르기 때문에 reset후 개발을 시작해야함

1) Reset : aggressive solution

2) Normalize : gentle solution



**CDN (Content Delivery Network)**

> 컨텐츠를 효율적으로 전달하기 위해 외부서버를 활용 



**spacing 종합**

1) .mt-1

2).mx-auto : 수평 중앙 정렬

3).py-0 : padding-top과 padding-bottom이 0





## Grid System

> 12(약수가 많아서)개의 column으로 이루어져있다. 
>
> 12칸 내에서 비율을 지정해서 작동한다.
>
> 6개의 grid breakpoints

```html
<div class="container">
    <div class="row">
        <div class="column">
        </div>
    </div>
</div>
```

그리드는 항상 컨테이너 안에서 진행된다

```html
<div class="container">
    <div class="row">
        <div class="col-3"></div>
        <div class="col-3"></div>
        <div class="col-3"></div>
        <div class="col-3"></div>
    </div>
</div>


<div class="container">
    <div class="row row-cols-3">
        <div class="col"></div>
        <div class="col"></div>
        <div class="col"></div>
        <div class="col"></div>
    </div>
</div>

<div class="container">
    #lg를 지나는 순간 4개, md보다 큰 경우 2개, 작은 경우 1개
    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-4">
        <div class="col"></div>
        <div class="col"></div>
        <div class="col"></div>
        <div class="col"></div>
    </div>
</div>

<div class="container">
    #lg를 지나는 순간 4개, md보다 큰 경우 2개, 작은 경우 1개
    <div class="row">
        <div class="col-12 col-md-6 col-lg-3"></div>
        <div class="col-12 col-md-6 col-lg-3"></div>
        <div class="col-12 col-md-6 col-lg-3"></div>
        <div class="col-12 col-md-6 col-lg-3"></div>
    </div>
</div>

#row에 작성 시 몇개 보여줄지, col에 작성 시 몇 칸 차지할지
```



![image-20210203221817013](C:\Users\leejo\AppData\Roaming\Typora\typora-user-images\image-20210203221817013.png)



## Offset

- 비어있는 공간을 생성
- breakpoint가 들어간다 

```html
<div class="container">
    #lg를 지나는 순간 4개, md보다 큰 경우 2개, 작은 경우 1개
    <div class="row">
        <div class="col-12 col-md-6 col-lg-3 offset-lg-1"></div>
        <div class="col-12 col-md-6 col-lg-3 offset-lg-1"></div>
        <div class="col-12 col-md-6 col-lg-3 offset-lg-1"></div>
        <div class="col-12 col-md-6 col-lg-3 offset-lg-1"></div>
    </div>
</div>
```

