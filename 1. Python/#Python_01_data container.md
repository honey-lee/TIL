# 01 data container

> 컨테이너 : 여러 개의 값을 저장할 수 있는 객체 
>
> - 시퀀스형 : 순서가 있는 데이터
> - 비 시퀀스형 : 순서가 없는 데이터 



## 1.1 시퀀스형 컨테이너: 데이터가 순서대로 나열된 형식

> 나열된 것이 `정렬되었다(sorted)`라는 뜻은 아니다 .
>
> - 순서를 가질 수 있다.
> - 특정 위치의 데이터를 가리킬 수 있다. 
> - **리스트, 튜플, 레인지, 문자형**



### 1)list: `[]`형태 , 수정 가능 

  - 0부터 30까지의 숫자를 3씩 증가시킨 리스트로 만들기

    sample_list = list(range(0, 31))
    print(sample_list[0::3])

  - list에 담긴 특정한 요소의 갯수 확인하기 

    a = [1, 1, 2]
    a.count(1)

### 2) tuple: `()`형태, 수정 불가, 내용물을 바꾸지 않을 때 사용, 가지고 있는 요소 변경 불가능 

  - 직접 만들어서 사용하기 보다 파이썬 내에서 다양한 용도로 쓰여짐

```python
#하나의 항목으로 구성된 튜플은 값 뒤에 쉼표를 붙여서 만든다.

single_tuple = ('hello', )
```

### 3) range: `range(n, m, s)`형태, 숫자 n부터 m-1까지 s의 간격으로 출력
### 4) string: `' '` 형태



#### 시퀀스에서 활용할 수 있는 연산자/함수

|    operation |                    설명 |
| -----------: | ----------------------: |
|     x `in` s |        containment test |
| x `not in` s |        containment test |
|    s1 `+` s2 |           concatenation |
|      s `*` n | n번만큼 반복하여 더하기 |
|       `s[i]` |                indexing |
|     `s[i:j]` |                 slicing |
|   `s[i:j:k`] |       k간격으로 slicing |
|       len(s) |                    길이 |
|       min(s) |                  최솟값 |
|       max(s) |                  최댓값 |
|   s.count(x) |                x의 개수 |



## 1.2 비 시퀀스형 컨테이너: 순서가 없는 자료구조

- set: `{}`형태, 순서가 보장되어 있지 않은 집합 구조, 중복이 허용되지 않기 때문에 중복되는 값은 삭제됨, 중복을 제거할 때 유용하게 사용될 수 있음
- dictionary: `{key : value}` 형태, 중복된 key값이 존재하지 않아 속도를 빠르게 한다.



![image-20210118150718218](C:\Users\leejo\AppData\Roaming\Typora\typora-user-images\image-20210118150718218.png)



### 데이터의 분류

`화살표 뒤쪽이 바뀔  수 있으면 Mutable, 재할당을 통해서만 바뀔 수 있으면 Immutable`

#### 변경 불가능한 (immutable) 데이터

변경 불가능한(immutable) 데이터 : dictionary의 key값으로 사용가능 하다

- literal
  - Number
  - String
  - Bool
- range()
- tuple()

#### 변경 가능한 (mutable) 데이터

- list
- dict
- set
