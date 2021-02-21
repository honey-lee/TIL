# 배열2 (Array 2)



## 2차원 배열의 선언

> - 1차원 리스트를 묶어놓은 리스트
> - 2차원 이상의 다차원 리스트는 차원에 따라 인덱스 선언



## 순회 방식

> n * m 배열의 요소를 빠짐없니 순회하는 방법



**1) 행 우선순회**

```python
#행 고정
for i in range(len(array)):
    for j in range(len(array[i])):
        print(array[i][j])    
```

**1-2) 행 우선순회 (역)**

```python
for i in range(N):
    for j in range(M-1, -1, -1):
        print(arr[i][j])
```

**2) 열 우선순회**

```python
for j in range(M): #열의 길이
    for i in range(N): #행의 길이
        	print(arr[i][j])

for j in range(len(array[0])):
    for i in range(len(array)):
        print(array[i][j])
```

**2-2) 열 우선순회 (역)**

```python
for j in range(M):
    for i in range(N-1, -1, -1):
        print(arr[i][j])     
```

**3) 지그재그 순회**

```python
for i in range(len(array)):
    for j in range(len(array[0])):
        print(array[i][j + (m-1-2*j) * (i % 2)])
```



## 2차원 배열의 접근

**델타를 이용한 2차원 배열의 접근**

```python
arr = [[1, 2, 3],
      [4, 5, 6],
      [7, 8, 9]]

r = 1
c = 1

#상하좌우
dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]

#상하좌우
drc = [[-1, 0], [1, 0], [0, -1], [0, 1]]

for i in range(4):
    nr = r + dr[i]
    nc = c + dc[i]
    
    if nr < 0 or nr >= N or nc < 0 or nc >= N:
        continue
        #범위를 벗어나지 않도록 벽을 만든다
    print(arr[nr][nc])
    #2 8 4 6 상하좌우 값이 한번 씩 출력된다
    
# 그런데 여기서 r 값을 0 으로 바꿔서 똑같이 출력한다면
# 8 5 1 3이 나온다
# - 인덱스 값이 출력된다
```

대각선 값도 조정가능하다 

상좌 : 행 -1, 열 -1

상우 : 행 -1, 열+1

하좌 : 행 +1, 열 -1

하우 : 행 +1, 열 +1



**전치 행렬**

```python
arr = [[1, 2, 3],
      [4, 5, 6],
      [7, 8, 9]]

for i in range(3):
    for j in range(3):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
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
        if i & (1<<j):
            print(arr[j], end = '')
        print()  #줄바꿈
    print()      #줄바꿈
```



## 비트 연산

**비트 연산자**

- `&` : 비트 단위로 AND 연산을 한다

  - `i & (1 <<  j)` : i의 j번째 비트가 1인지 아닌지를 리턴한다

- `|` : 비트 단위로 OR 연산을 한다

- `<<` : 피연산자의 비트 열을 왼쪽으로 이동시킨다, 값을 2배씩 증가시킨다 

  - 1 << n : `2^n` 즉, 원소가 n 개일 경우의 모든 부분집합의 수를 의미한다

- `>>` : 피연산자의 비트 열을 오른쪽으로 이동시킨다

  

