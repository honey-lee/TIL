# 🧡🍯 Honey-tips 

[toc]

## 행과 열을 간단히 뒤집는 방법

> 행과 열을 뒤집기 위해서는 빈 리스트에 열 중심으로 순회하며 데이터를 넣어주는 법도 있다. 하지만 빠르고 간단하게 행열을 뒤집기 위해서는 아래와 같은 방법이 있다.

```python
#step 1
#data를 unpacking(*) 한 후 zip으로 모아준다.

for i in zip(*data):
    print(i)
#출력 결과, 열끼리 튜플 형태로 묶인다
'''
(1, 4, 7)
(2, 5, 8)
(3, 6, 9)
'''

#step 2
#묶어놓은 튜플을 빈 리스트에 리스트 형태로 넣어준다
for i in zip(*data):
    data.append(list(i))
#출력 결과, 행과 열이 뒤집힌다
'''
1  4  7
2  5  8
3  6  9
'''
```



```python
from pandas import DataFrame

data = [
    [1, 2, 3],
    [1, 2, 3],
    [1, 2, 3],
]
data2 = []
print(DataFrame(data))

print('############################')

for ele in zip(*data):  # 세로 데이터를 포함해서 200행 짜리 데이터를 만든다
    data2.append(list(ele))
print(DataFrame(data2))
```



## 함수 파라미터의 타입 지정하기 

> IDE의 도움받기
>
> 함수에 파라미터 타입을 지정하지 않아도 실행되지만 타입을 명시하면 IDE는 실행 함수를 표시해준다 

```python
def solution(data: list, start: int, end: int) -> int:
```



## Python default version 간단히 변경하기 

(windows 운영체제 기준)

1. `시스템 환경 변수 편집` 검색
2. `고급` 탭에서 `환경 변수(N)` 클릭
3. `Path` 더블 클릭 
4. 사용하고자 하는 파이썬의 버전을 `위로 이동`을 클릭하여 가장 위에 위치시킴
5. `git bash`에서 명령어 `python --version` 입력하여 파이썬 버전 변경 여부 확인 



## 순열과 조합 라이브러리로 간단히 찾기

> `itertools` 모듈에서 순열과 조합을 위한 라이브러리 import 후 간단히 사용 가능

```python
from itertools import permutations, product, combinations, combinations_with_replacement

list = [1, 2, 3, 4, 5]


# 순열 (중복 허용 x), permutations

list2 = permutations(list, 2)

for i in list2:
    print(i, end = '')

 
# (1, 2)(1, 3)(1, 4)(1, 5)(2, 1)(2, 3)(2, 4)(2, 5)(3, 1)(3, 2)(3, 4)(3, 5)(4, 1)(4, 2)(4, 3)(4, 5)(5, 1)(5, 2)(5, 3)(5, 4)

# 순열 (중복 허용 o), product
list3 = product(list, repeat = 2)

for i in list3:
    print(i, end = '')

    
# (1, 1)(1, 2)(1, 3)(1, 4)(1, 5)(2, 1)(2, 2)(2, 3)(2, 4)(2, 5)(3, 1)(3, 2)(3, 3)(3, 4)(3, 5)(4, 1)(4, 2)(4, 3)(4, 4)(4, 5)(5, 1)(5, 2)(5, 3)(5, 4)(5, 5)

# 조합 (중복 허용 x), combinations

list4 = combinations(list, 2)

for i in list4:
    print(i, end = '')


# (1, 2)(1, 3)(1, 4)(1, 5)(2, 3)(2, 4)(2, 5)(3, 4)(3, 5)(4, 5)
    
# 조합 (중복 허용 o), combinations_with_replacement

list5 = combinations_with_replacement(list, 2)

for i in list5:
    print(i, end = '')
    
# (1, 1)(1, 2)(1, 3)(1, 4)(1, 5)(2, 2)(2, 3)(2, 4)(2, 5)(3, 3)(3, 4)(3, 5)(4, 4)(4, 5)(5, 5)
```



## Bash에서 명령 단축어 지정하기

> `&&` 연산자를 통해 한번에 여러개의 명령어도 지정가능해 반복 타이핑이 번거로울때 사용하기 유용함 

```bash
code ~/.bashrc
# alias 명령어이름='명령'
alias pyvenv='python -m venv venv && source venv/Scripts/activate'
```



## 진법 변환 쉽게 하기

```python
print(int('1A', 16))   # 16진수인 1A를 10진법으로 변환하기
print(int('1A', 15))   # 15진수인 1A를 10진법으로 변환하기
print(int('1A', 14))   # 14진수인 1A를 10진법으로 변환하기
print(int('1A', 13))   # 13진수인 1A를 10진법으로 변환하기 
....
print(format(42, 'b')) # 숫자 42를 2진수로 바꾸기
```



## Re 모듈

[Re모듈](https://wikidocs.net/4308)

이제 컴파일된 패턴 객체를 사용하여 문자열 검색을 수행해 보자. 컴파일된 패턴 객체는 다음과 같은 4가지 메서드를 제공한다.

| Method     | 목적                                                         |
| :--------- | :----------------------------------------------------------- |
| match()    | 문자열의 처음부터 정규식과 매치되는지 조사한다.              |
| search()   | 문자열 전체를 검색하여 정규식과 매치되는지 조사한다.         |
| findall()  | 정규식과 매치되는 모든 문자열(substring)을 리스트로 돌려준다. |
| finditer() | 정규식과 매치되는 모든 문자열(substring)을 반복 가능한 객체로 돌려준다. |

match, search는 정규식과 매치될 때는 match 객체를 돌려주고, 매치되지 않을 때는 None을 돌려준다. 이들 메서드에 대한 간단한 예를 살펴보자.

> ※ match 객체란 정규식의 검색 결과로 돌려주는 객체이다.

우선 다음과 같은 패턴을 만들어 보자.

```
>>> import re
>>> p = re.compile('[a-z]+')
```

### match

match 메서드는 문자열의 처음부터 정규식과 매치되는지 조사한다. 위 패턴에 match 메서드를 수행해 보자.

```
>>> m = p.match("python")
>>> print(m)
<_sre.SRE_Match object at 0x01F3F9F8>
```

"python" 문자열은 `[a-z]+` 정규식에 부합되므로 match 객체를 돌려준다.

```
>>> m = p.match("3 python")
>>> print(m)
None
```

"3 python" 문자열은 처음에 나오는 문자 3이 정규식 `[a-z]+`에 부합되지 않으므로 None을 돌려준다.

match의 결과로 match 객체 또는 None을 돌려주기 때문에 파이썬 정규식 프로그램은 보통 다음과 같은 흐름으로 작성한다.

```
p = re.compile(정규표현식)
m = p.match( 'string goes here' )
if m:
    print('Match found: ', m.group())
else:
    print('No match')
```

즉 match의 결괏값이 있을 때만 그다음 작업을 수행하겠다는 것이다.

### search

컴파일된 패턴 객체 p를 가지고 이번에는 search 메서드를 수행해 보자.

```
>>> m = p.search("python")
>>> print(m)
<_sre.SRE_Match object at 0x01F3FA68>
```

"python" 문자열에 search 메서드를 수행하면 match 메서드를 수행했을 때와 동일하게 매치된다.

```
>>> m = p.search("3 python")
>>> print(m)
<_sre.SRE_Match object at 0x01F3FA30>
```

"3 python" 문자열의 첫 번째 문자는 "3"이지만 search는 문자열의 처음부터 검색하는 것이 아니라 문자열 전체를 검색하기 때문에 "3 " 이후의 "python" 문자열과 매치된다.

이렇듯 match 메서드와 search 메서드는 문자열의 처음부터 검색할지의 여부에 따라 다르게 사용해야 한다.

### findall

이번에는 findall 메서드를 수행해 보자.

```
>>> result = p.findall("life is too short")
>>> print(result)
['life', 'is', 'too', 'short']
```

"life is too short" 문자열의 'life', 'is', 'too', 'short' 단어를 각각 `[a-z]+` 정규식과 매치해서 리스트로 돌려준다.

### finditer

이번에는 finditer 메서드를 수행해 보자.

```
>>> result = p.finditer("life is too short")
>>> print(result)
<callable_iterator object at 0x01F5E390>
>>> for r in result: print(r)
...
<_sre.SRE_Match object at 0x01F3F9F8>
<_sre.SRE_Match object at 0x01F3FAD8>
<_sre.SRE_Match object at 0x01F3FAA0>
<_sre.SRE_Match object at 0x01F3F9F8>
```

finditer는 findall과 동일하지만 그 결과로 반복 가능한 객체(iterator object)를 돌려준다. 반복 가능한 객체가 포함하는 각각의 요소는 match 객체이다.