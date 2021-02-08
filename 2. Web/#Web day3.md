## 미디어 쿼리

> - 반응형 디자인의 핵심 구성 요소

```html
<style>
    #print할 때 빨간색으로 처리 
    @media print {
        body {
            color: red;
        }
    }
</style>
```

```html
#600보다 작을때는 빨간색
@media (max-width: 600px) {
	body {
		color: red;
}
}

#600보다 클 때는 빨간색
@media (min-width: 600px) {
	body {
		color: red;
}
}

#가로 모드일 때 보라색 
@media(orientatioin: landscape) {
	body {
		color: rebeccadpurple;
}
}

#혼합도 가능 
@media (min-width: 400px) and (orientation: landscape)


div {
	border: 2px solid black;
	background-color: brown;
	width: 100px;
	height: 100px;
}

@media (max-width: 576px) {
	div {
		width: 100%;
	}
}

@media (max-width: 750px) {
	div {
		width: 40%
}
}
```





## 애니메이션

```html
div {
	border: 2px solid black;
	background-color: brown;
	width: 100px;
	height: 100px;
	animation: move;
	animation-duration: 3s;
}

@keyframes move {
	0% {
		margin-left: 0px;
}
	100% {
		margin-left: 200px;
}
}


@keyframes color-change {
	from {
		background-color: brown;
	}
	to {
		background-color: red;
	}
}
```

