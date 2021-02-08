# 06 Data_structure_I

### 6-1. 문자열(String)

> Immutable, ordered, Iterable

#### 조회/탐색

##### 1) `.find(x)`

- x의 첫번째 위치를 반환, 없으면 `-1` 반환

```python
a = apple
a.find('a') #0
a.find('b') #-1, 없는 요소는 -1 
```

##### 2) `.index(x)`

- x의 첫번째 위치 반환, 없으면 오류 발생

```python
a = apple
a.index('a') #0
a.index('p') #1
a.index('c') #오류 발생
```



#### 값 변경

##### 3) `.replace(old, new [, count])`

- 바꿀 대상 글자를 새로운 글자로 바꿔서 반환 
- count 지정 시 해당 갯수만큼만 시행 

```python
z = 'zoo!yoyo!'
z.replace('o', '') #'z!yy!'
z.replace('o', '', 2) #'z!yoyo!'
```

#####  4)`.strip([chars])` 

- 특정한 문자들을 지정해 양쪽을 제거, 왼쪽(lstrip) 혹은 오른쪽 제거(rstrip)
- 지정하지 않으면 공백 제거

##### 5) `.split()`

```python
csv = '1, 홍길동, 01012344567'
#구분자를 기준으로 끊어서 리스트로 만들어준다.
csv.split(',') #['1', '홍길동', '01012344567']
```

##### 6) `'seperator'.join(iterable)`

- 반복가능한 컨테이너의 요소들을 구분자로 합쳐 문자열로 반환

```python
word = '배고파'
'!'.join(word) #'배!고!파'
```



#### 문자 변형

##### 7) `.capitalize(), .title(), .upper()`

- `.capitalize()` : 앞글자를 대문자로 만들어 반환한다
- `.title()` : 어포스트로피나 공백 이후를 대문자로 만들어 반환한다
- `.upper()` : 모두 대문자로 만들어 반환한다

##### 8) `.lower(), .swapcase()`

- `.lower()` : 모두 소문자로 만들어 반환한다
- `.swapcase()` : 대/소문자 변경하여 반환한다



#### 문자열 관련 검증 메소드 : 참 / 거짓 반환

##### 9) `.isalpha(),  .isdecimal(),  .isdigit(),  .isnumeric(),  .isspace(),  .isupper(),  .istitle(),  .islower()`



### 6-2. 리스트(List)

> Immutable, ordered, iterable

#### 값 추가 및 삭제


##### 1) `.append(x)`

- 값을 추가하며 원본값을 변경한다. 

##### 2) `.extend(iterable)`

- 리스트에 iterable (list, range, tuple, string) 값을 붙일 수 있다.

- append는 요소 하나, extend는 여러 개를 추가해준다.

- *** string 값을 넣으면 한 글자씩 분해됨*** 

##### 3) `.insert(i, x)`

- 정해진 위치`i`에  `x`값을 추가 

##### 4) `.remove(x)`

- 리스트에서 `x`값 삭제

- 요소값 자체로 삭제하며 동작은 한 번만 수행된다 

- x값이 없으면 오류가 발생한다.

##### 5) `.pop(x)`

- 가장 마지막 요소를 반환한다
- 원본이 변경된다 (return값 사라짐)

```python
a = [1, 2, 3, 4, 5, 6]

a.pop()  # 6
a.pop(0) # 1

print(a) # [2, 3, 4, 5]

# 별도의 변수에 저장할 수 있다
students = ['홍길동', '유재석']
bye = students.pop()
print(f'{bye} 학생이 떠나갔습니다! {students}') # 유재석 학생이 떠나갔습니다! ['홍길동']
```

##### 6)`.clear()`

- 리스트의 모든 항목 삭제

```python
a = [1, 2, 3]
a.clear()
a #[]
```



#### 탐색 및 정렬

##### 7) `.index(x)`

- `x`값을 찾아 해당 index 값을 반환
- index값이 없을 경우 오류가 발생함

```python
a = [1, 2, 3, 4, 5]
a.index(1) #0
```

##### 8)`.count(x)`

- 원하는 값의 갯수 확인

```python
a = [1, 2, 5, 1, 5, 1]
a.count(1) #3

#원하는 값을 모두 삭제하려면 
for i in range(a.count(1)):
    a.remove(1)
a #[2, 5, 5]
```

##### 9)`.sort()`

- 정렬
- 원본을 변형시키고 `None`을 리턴함

##### 10) `.reverse()`

- 정렬하지 않고 순서를 뒤집는다 
- 원본 변형

```python
classroom = ['Tom', 'David', 'Justin']
classroom.reverse()
classroom #['Justin', 'David', 'Tom']
```



#### 리스트 복사

#### shallow copy & deep copy

```python
#shallow copy

a = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

b = a

#다른 얕은 복사

c = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

d = c[:]

#deep copy
#중첩된 상황에서 복사, 내부 객체까지 새롭게 값이 변경됨

from copy import deepcopy

a = [[1, 2, 3], 2, 3]
b = deepcopy(a)

b[0][0] = 100

print(a, b) #[[1, 2, 3], 2, 3] [[100, 2, 3], 2, 3]

#deep copy2

import copy

copy.deepcopy(a)
```



#### List comprehension

> 표현식과 제어문을 통해 리스트 생성 
>
> 여러 줄의 코드를 한줄로 작성 가능 
>
> [expression for 변수 in iterable]

```python
#1~10까지의 숫자로 만든 세제곱 담긴 리스트 `cubic_list`
numbers = range(1, 11)

#반복문 활용
cubic_list = []
for number in numbers:
    cubic_list.append(number ** 3)
    
#List comprehension
[number ** 3 for number in numbers]
```

```python
#1~10까지의 숫자 중 짝수만 담긴 `even_list`

[i for i in range(1, 11) if i % 2 == 0]

#홀수, 짝수 표현
['홀수' if i % 2 == 1 else '짝수' for i in range(1, 11)]

#뒤에 조건식에는 else 사용 불가 
['홀수' for i in range(1, 11) if i % 2 == 1 else '짝수'] #오류 발생

#함수도 입력 가능 
def test(number):
    return '홀수' if number % 2 == 1 else '짝수'

[test(i) for i in range(1, 11)]
```



#### 데이터 구조에 적용가능한 Built-in Function

> iterable한 경우 적용 가능 
>
> `map(), filter(), zip()`

##### 1)`map(function, iterable)`

- 순회가능한 데이터 구조의 모든 요소에 function을 적용한 후 그 결과를 돌려준다

```python
numbers = [1, 2, 3]
[str(i) for i in numbers]  # ['1', '2', '3']
''.join([str(i)] for i in numbers)  #'123'

#다른 예
def cube(n):
    return n ** 3

numbers = [1, 2, 3]
new_numbers = list(map(cube, numbers))
print(new_numbers)  # => [1, 8, 27]
```



##### 2)`filter(function, iterable)`

- iterable에서 function의 반환된 결과가 True인 것들만 구성하여 반환
- `filter object`를 반환

```python
def odd(n):
    return n % 2

numbers = [1, 2, 3]
new_numbers = list(filter(odd, numbers))
print(new_numbers)  # => [1, 3]
```



##### 3)`zip(*iterables)`

- 복수의 iterable 객체를 모아준다
- 결과는 튜플의 모음으로 구성된 `zip object`를 반환

```python
girls = ['jane', 'ashley', 'mary', 'honey']
boys = ['justn', 'eric', 'david', 'ramy']

pair = list(zip(girls, boys))
print(pair)  # => [('jane', 'justin'), .... ('honey', 'ramy')]
```

