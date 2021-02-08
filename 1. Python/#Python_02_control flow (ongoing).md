# 02 control flow (제어문)

> 특정 상황에 따라 코드를 선택적으로 실행하거나 동일한 코드를 계속해서 실행해야 할 때 **코드 실행의 순차적인 흐름을 제어**해야한다. 
>
> 이러한 순차적인 코드의 흐름을 제어하는 것을 **제어문**이라 하고 제어문은 크게 **조건문**과 **반복문**으로 나눌 수 있다.

## 2.1 조건문 (conditional statement)

### 1)`if` 조건문의 구성

- 반드시 참/거짓을 판단할 수 있는 조건과 함께 사용
- 들여쓰기 유의 (4spaces)
  - num = 5
    if num % 2 == 1:
        print('홀수')
    else:
        print('짝수')
  - input(): 사용자 입력을 받을 때 사용
    - input값은 형태가 입력되지 않으면 str값으로 처리된다.
- 조건은 항상 True or False를 반환한다


##### 중첩 조건문 (폴더)
- 코드는 항상 위에서부터 아래로 실행됨
  - if score >= 90:
        print('A')
        if score >= 95:
            print('참 잘했어요')

##### 조건 표현식

- 삼항 연산자
- 한 줄에 조건문 표현 가능 
  - num = int(input())
    value = '홀수' if num % 2 else '짝수'
    print(value)
- if/else 두 가지 조건으로 분리될 때 실용적 

### 반복문

#### `while` 반복문

- 조건문이 참일 경우 반복적으로 코드를 시행

  - while True:

    print('조건문이 참인 동안')

    print('계속 반복')

- 콜론 `:`이 반드시 필요, 들여쓰기 필요

- 종료조건 반드시 설정

#### `for` 반복문

- `string`, `tuple`, `list`, `range` 나 다른 순회가능한 객체의 요소들을 순회한다.
- for(start, end, step)

##### 반복제어(break, continue, for-else)

- break: 반복문 종료
- continue: 이후의 코드를 수행하지 않고 다음요소부터 계속하여 반복 수행
- else: 끝까지 반복문을 실행한 이후에 실행
  - 반복문에서 리스트의 소진 혹은 조건이 거짓으로 종료할 때 실행
  - break문으로 종료될 때는 실행되지 않는다.

##### 조건 표현식 



- `enumerate()` : 내장함수로 추가적인 변수 활용 가능, 열거 객체를 돌려준다.

```python
lunch = ['짜장면', '초밥', '피자', '햄버거']

print(list(enumerate(lunch)))
for idx, menu in enumerate(lunch):
    print(idx + 1)
    print(menu)
    
[(0, '짜장면'), (1, '초밥'), (2, '피자'), (3, '햄버거')]
1
짜장면
2
초밥
3
피자
4
햄버거
 
```





