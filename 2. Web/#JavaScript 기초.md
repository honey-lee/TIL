# JavaScript 기초

## 1. 프로그래밍 시작하기 in JavaScript

### 01 자바스크립트 첫 걸음

자바스크립트가 처음 등장했을 때는 '근본없는 언어'라고 불릴 정도로 인기가 없었는데 2015년부터 인기 대폭발!!!! 그 이후로 단순히 웹개발 언어가 아닌 모바일앱, 게임, VR과 같은 3D컨텐츠, 블록체인에도 사용되면서 다양한 분야에 활용되는 범용적인 기술이 됨. 차별력있는 개발자가 되기 위해서는 꼭 해야하는 자바스크립트 😍 

**JS 파일 생성하기** : 확장자 : `js` 

```jsx
// 브라우저의 콘솔 창에 메시지 입력
console.log('hello')

// 결과는 모두 15
console.log(10 + 5)
console.log(20 - 5) 
console.log(3 * 5) // 자바스크립트에서 곱셈기호는 x 대신 * 로 표기합니다. 
console.log(30 / 2) // 자바스크립트에서 나눔기호는 ÷ 대신 / 로 표기합니다.
console.log(6 + 1 + 8) // 다항식도 문제없이 동작합니다.
console.log(3 * (4 + 1)) // 괄호가 있을 경우에는 기본적인 우선순위에 따라 연산합니다.
```

### 02 프로그래밍 맛보기

1. 세미콜론 `;` 
    - 문장을 구분할 때 세미콜론을 붙임
    - 세미콜론을 붙이지 않더라도 줄이 바뀌면 자동으로 세미콜론으로 인식함
2. 코멘트 `//`

```jsx
/지금 이코드는 
줄바꿈이 있지만
모두 다
주석 
/
```

3. 추상화 : 불필요한것들은 빼고 목적에 맞게 간결화하는것, 단순하고 간결하게 표현하면서도 그 핵심만큼은 명확하게 드러냄, 프로그래밍은 추상화의 연속이다

변수를 사용하는것도 추상화의 일종이다

**4. JavaScript Rule**

1. JavaScript 식별자는 문자 `(a-z, A-Z)`, 밑줄 `(_)` 혹은 달러 기호 `($)` 로 시작한다. 두 번째 글자부터는 숫자 `0~9`도 가능하다.
2. 대문자와 소문자를 구별해야 한다. myname과 myName은 다른 이름이다.
3. 예약어는 사용하면 안된다. (ex. if, for, let...)

[Javascript style guide]([https://github.com/ParkSB/javascript-style-guide](https://github.com/ParkSB/javascript-style-guide))

5. 변수 선언 `let`

```jsx
// let 변수이름 = 값;
let espressoPrice = 3000;

console.log(espressoPrice);
```

6. 함수 선언 `function`

```jsx
// 함수 선언
function 함수이름() {
	명령;
	명령;
}

// 여러 나라의 인삿말을 가지고 있는 함수 선언
function greetings() {
	console.log('hi');
	console.log('안녕');
	console.log('guten tag');
	console.log('hola');
	console.log('konichiwa');
}

greetings();
```

7. return문

```jsx
function getTwo() {
	return 2;
};
```

## 2. 프로그래밍 핵심 개념 in JavaScript

### 01 자료형

1. 숫자형

    숫자형은 JavaScript 내에서 연산이 가능

    기본적인 사칙연산과 나머지 연산, 거듭제곱 연산, 우선순위에 의한 연산이 가능하다

    ```jsx
    //나머지 
    console.log(7 % 3);

    //거듭제곱 (곱셈보다 우선순위 높음)
    console.log(2 ** 3);

    ```

2. 문자열

```jsx
//문자열은 따옴표 안에 표현
console.log('hello world');

//문자열 안에 따옴표가 들어갈 경우 따옴표 앞에 역슬래시 기입
console.log('He said \"I\'m Iron Man\"');

//백틱 사용
console.log(`He said "I'm Iron Man"`);

//문자열 연결
console.log('Hello' + 'world');
```

3. 불 대수

명제에 대한 참과 거짓을 나타내는 연산

`AND` 연산 : 모든 명제가 참일 경우에만 참

`OR`연산 : 두 명제 중 하나만 참이여도 참

`NOT`연산 : True는 False로, False는 True로 반대로 뒤집는 연산

4. 불린형 : 참과 거짓을 표현하는 자료형 

`===`, `!==` : 자료형도 같은지 다른지 비교하는 연산자 

```jsx
console.log(2 > 1); //True
console.log(3 >= 3); //True
console.log(3 != 3); //False

console.log('CodeIt' === 'CodeIt'); //True
console.log('CodeIt' !== 'CodeIat'); //True

// AND 연산, &&
console.log(True && True); // True

// OR 연산, ||
console.log(True || False); // True

// NOT 연산, !
console.log(!True); //False
console.log(!!True); //True
```

5. typeof 연산자

현재 사용중인 자료형이 어떤 자료형인지 알려주는 연산자

```jsx
console.log(typeof 101); //number
console.log(typeof 'CodeIt'); //string
console.log(typeof '1'); //number
console.log(typeof 1.0); //number (소수형을 구분하지 않음)
console.log(typeof true); //boolean

console.log(typeof 8 - 3); //NaN - Not a Number
//typeof 연산자는 우선순위가 높아서 8-3이 연산되기 전에 이미 연산됨
console.log(typeof (8 - 3)); //number

//string
console.log(typeof typeof (5+3);
console.log(typeof 'number');
```

[연산자 우선순위에 관한 공식문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

6. 형 변환 (Type conversion)

```jsx
//String, Number, Boolean
console.log(Number('10') + Number('5')); //15
console.log(String(10) + String(5)); //105

let x = 123;
console.log(String(x)); //123
console.log(typeof String(x)); //String

// '', 0, NaN <- falsy
Boolean(NaN); //false
Boolean(0); //false
```

**자바스크립트에서는 일정한 규칙에 따라 자동으로 형 변환을 한다**

```jsx
console.log('4' - true); //3
console.log(4 + '2'); //42 (덧셈에서는 한쪽이 문자열이면 양쪽 모두 문자열로 변환)
console.log('4' ** true); //4
console.log(4 / '2'); //2 (나눗셈에서는 한쪽이 숫자니까 양쪽 모두 숫자됨)

//등호 연산에서는 대개의 경우 숫자열로 인식 
console.log(2 < '3'); //true
console.log('2' <= false); //false
console.log('two' >= 1); //false 판단불가할 경우 false

//등호를 2개만 사용하면 형 변환이 일어남 
console.log(1 === '1'); //false 일치비교
console.log(1 === true); false
console.log(1 == '1'); // true 동등비교
console.log(1 == true); //true
```

7. 템플릿 문자열

백틱을 사용해서 생성

```jsx
//template : 일정한 틀, 형식
let year = 2021;
let month = 4;
let day = 23;

console.log(`생년월일은 ${year}년 ${month}월 ${day}일 입니다.`);

let myNumber = 3;

function getTwice(x) {
	return x * 2;
}

console.log(`${myNumber}의 두 배는 ${getTwice(myNumber)}입니다.`);
// 3의 두 배는 6입니다.
```

8. null과 undefined

`null`과 `undefined`는 값이 없다는 의미이다.

`null` : 의도적으로 값이 없음을 표현할 때 사용, 의도적인 없음

`undefined` : 값이없다는 것을 확인할 때 사용, 처음부터 그냥 값이 없음

```jsx
let codeit;
console.log(codeit); //undefined, 값을 선언만 하고 지정하지 않았음
codeit = null;
console.log(codeit); //null, 값이 없다는 것을 선언했음
```