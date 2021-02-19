# 배열2 (Array 2)



## 2차원 배열의 선언

> - 1차원 리스트를 묶어놓은 리스트
> - 2차원 이상의 다차원 리스트는 차원에 따라 인덱스 선언



## 순회 방식

> n * m 배열의 요소를 빠짐없니 순회하는 방법



**1) 행 우선순회**

```python
for i in range(len(array)):
    for j in range(len(array[i])):
        print(array[i][j])    
```

**1-1) 행 우선순회 (역)**

```python
for i in range(len(array)):
    for j in range()
```

**2) 열 우선순회**

```python
for j in range(len(array[0])):
    for i in range(len(array)):
        print(array[i][j])
```

**3) 지그재그 순회**

```python
for i in range(len(array)):
    for j in range(len(array[0])):
        array[i][j + (m-1-2*j) * (i % 2)]
```



## 부분집합

> 집합의 원소가 n개일 때 공집합을 포함한 부분집합의 수는 2^n개이다.

```python
bit = [0, 0, 0, 0]

for i in range(2):
    bit[0] = i
    for j in range(2):
        bit[1] = j
        for k in range(2):
            bit[2] = k
            for l in range(2):
                bit[3] = l
                print(bit)
```

```python
arr = 

n = len(arr)

for i in range(1<<n):
    for j in range(n):
        if i & (1<<j)
```



## 비트 연산

