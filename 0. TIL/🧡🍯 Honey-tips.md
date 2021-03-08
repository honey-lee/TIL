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