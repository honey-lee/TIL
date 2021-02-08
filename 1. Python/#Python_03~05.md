# Python Day02

## 03 function_I

### 함수

- 특정한 기능을 하는 코드의 묶음
- 높은 가독성
- 재사용성
- 유지보수
  - 객체 지향 코드 등장

### 함수의 선언과 호출

- `def`로 시작하여 `:`으로 끝나고 다음은 `4spaces 들여쓰기`로 코드 블록을 만든다.

- 정의 -> 실행

- 동작 후에 `return`을 통해 결과값을 전달한다. `return`값이 없으면 `None`을 반환한다.

- `parameter(매개변수)`를 넘겨줄 수도 있다.

  - parameter는 함수의 정의 시 내부적으로 사용되는 input의 이름

  - def <함수이름> (parameter1, parameter2):

    <코드 블럭>

    return value

- 함수는 호출을 `func()`(호출이자 실행)을 통해 한다.



#### return vs print

return은 반환, print는 출력



### 함수의 Output

#### 함수의 `return`

- 함수는 반환되는 값이 있으며, 오직 한 개의 객체만 반환된다.
- 함수가 return 되거나 종료되면 함수를 호출한 곳으로 돌아간다.
- 어떤 것도 리턴하지 않는다면 자동으로 None을 반환한다.

