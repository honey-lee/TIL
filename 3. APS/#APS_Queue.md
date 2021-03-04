# 큐 (Queue)

> - 큐
> - 우선순위 큐
> - **BFS (너비 우선 탐색)**
> - 큐의 활용 : 버퍼



## 큐의 특성

- 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
  - 큐의 뒤에서는 삽입만 하고, 큐의 앞에서는 삭제만 이루어지는 구조
- **선입선출구조 (FIFO)** : 큐에 삽입한 순서대로 원소가 저장되어 가장 먼저 삽입(In)된 원소는 가장 먼저 삭제(Out)된다
  - 큐의 예 : 서비스 대기행렬
- `Front` : 저장된 원소 중 첫 번째 머리 원소,  `Rear` : 저장된 원소 중 마지막 꼬리 원소
- 주요 연산
| 연산          | 기능                                                   |
| ------------- | ------------------------------------------------------ |
| enQueue(item) | 큐의 뒤쪽(rear 다음)에 원소를 삽입 (rear 한 칸 증가)   |
| deQueue()     | 큐의 앞쪽(front)에서 원소를 삭제하고 반환 (front 증가) |
| createQueue() | 공백 상태의 큐를 생선                                  |
| isEmpty()     | 큐가 공백상태인지를 확인하는 연산                      |
| isFull()      | 큐가 포화상태인지를 확인하는 연산                      |
| Qpeek()       | 큐의 앞쪽(front)에서 원소를 삭제없이 반환              |


## 1. 선형큐

- **1차원 배열을 이용한 큐**

- 큐의 크기 = 배열의 크기

- 상태 표현

  - 초기 상태 : front = rear = -1
  - 공백 상태 : front = rear
  - 포화 상태: rear = n-1 (n : 배열의 크기, n-1 : 배열의 마지막 인덱스)

  

### 큐 생성 및 구현 

1. 초기 공백 큐 생성
   1. 크기 n인 1차원 배열 생성
   2. front와 rear를 -1로 초기화
2. 삽입 : `enQueue(item)` : 마지막 원소 뒤에 새로운 원소를 삽입 
   1. rear 값을 하나 증가 시켜 새로운 원소의 자리 마련
   2. 그 인덱스에 해당하는 배열원소 Q[rear]에 item을 저장 

```python
def enQueue(item):
    global rear
    if isfull(): print('Queue Full')
    else:
        rear += 1
        Q[rear] = item
```

3. 삭제 : `deQueue()` : 가장 앞에 있는 원소 삭제
   1. front값을 하나 증가시켜 큐에 남아있는 첫번째 원소 이동
   2. 새로운 첫 번째 원소를 리턴함으로써 삭제와 동일한 기능

```python
def deQueue():
    global front
    if isempty(): print('Queue Empty')
    else:
        front += 1
        return Q[front]
```

4. 공백 및 포화 상태 검사 : `isEmpty()`, `isFull()`
   - 공백 상태 : front = rear
   - 포화 상태 : rear = n-1

```python
def isEmpty():
    return front == rear
def iSFull():
    return rear == len(Q)-1
```

5. 검색 : `Qpeek()`
   - 가장 앞에 있는 원소를 검색하여 반환
   - 현재 front의 한자리 뒤에 있는 원소, 즉 큐의 첫 번째 원소를 반환

```python
def Qpeek():
    if isEmpty(): print('Queue Empty')
    else: return Q[front+1]
```

* 잘못된 포화상태 인식 
  * 선형 큐를 이용해 원소의 삽입과 삭제를 계속할 경우 배열의 앞부분에 활용할 공간이 있음에도 rear = n-1인 상태, 즉 포화상태로 인식해 더 이상의 삽입을 수행하지 않게 됨
  * **해결방법 1** : 매 연산이 이루어질 때마다 저장된 원소들을 배열의 앞부분으로 모두 이동시킴, 원소 이동에 많은 시간이 소요되어 큐의 효율성이 급격히 떨어진다는 단점이 있음
  * **해결방법 2** : 1차원 배열을 사용하된 논리적으로는 배열의 처음과 끝이 연결되어 **원형 형태의 큐**를 이룬다고 가정하고 사용, 물리적인 연결이 아닌 논리적인 연결 



## 2. 원형 큐

- 초기 공백 상태 : `front = rear = 0`
- Index의 순환 
  - front와 rear의 위치가 배열의 마지막 인덱스인 n-1을 가리킨 후 그 다음에는 논리적 순환을 이루어 배열의 처음 인덱스인 0으로 이동해야 함
  - 이를 위해 나머지 연산자 `%`를 사용함 
- front 변수 : 공백 상태와 포화상태 구분을 위해 front자리는 사용하지 않고 빈자리로 둠
- 삽입 및 삭제 위치

|             | 삽입 위치             | 삭제 위치               |
| ----------- | --------------------- | ----------------------- |
| **선형 큐** | rear = rear + 1       | front = front + 1       |
| **원형 큐** | rear = (rear + 1) % n | front = (front + 1) % n |



### 큐 생성 및 구현

1. 초기 공백 큐 생성
   1. 크기 n인 1차원 배열 생성
   2. front와 rear를 0으로 초기화
2. 공백 및 포화 상태 검사
   1. 공백 상태 : front = rear
   2. 포화 상태 : (rear+1) % n = front

```python
def isEmpty():
    return front == rear
def isFull():
    return (rear+1) % len(cQ) == front
```

3. 삽입 : `enQueue(item)` 
   - 마지막 원소 뒤에 새로운 원소를 삽입하기 위해 
     1. rear값을 조정하여 새로운 원소가 삽입될 자리 마련
     2. 그 인덱스에 해당하는 배열원소 cQ[item]에 item을 저장 

```python
def enQueue(item):
    global rear
    if isFull():
        print('Queue Full')
    else:
        rear = (rear + 1) % len(cQ)
        cQ[rear] = item
```

4. 삭제 : `deQueue()`, `delete()`
   - 가장 앞에 있는 원소를 삭제하기 위해 
     1. front값을 조정해 삭제할 자리를 준비
     2. 새로운 front원소를 리턴함으로써 삭제와 동일한 기능

```python
def deQueue():
    global front
    if isEmpty():
        print('Queue Empty')
    else:
        front = (front + 1) % len(cQ)
        return cQ[front]
```



## 3. 연결 큐

- **단순 연결 리스트를 이용한 큐**
- 큐의 원소 : 단순 연결 리스트의 노드
- 큐의 원소 순서 : 노드의 연결 순서, 링크로 연결됨
- `front` : 첫 번째 노드를 가리키는 링크, `rear` : 마지막 노드를 가리키는 링크 

### 상태 표현

- 초기 상태 : front = rear = None
- 공백 상태 : front = rear = None

### 생성 및 구현  (이미지 넣기)

1. 공백 큐 생성 : `createLinkedQueue()`
2. 원소 A삽입 : `enQueue(A)`



## 4. 우선순위 큐 

- 우선순위를 가진 항목들을 저장하는 큐 
- FIFO가 아니라 우선순위가 높은 항목들이 먼저 나가게 된다 

### 생성 및 구현 

- 배열을 이용한 자료 저장 
- 원소 삽입 과정에서 우선순위를 비교하여 적절한 위치에 삽입
- **가장 앞에 최고 우선순위의 원소가 위치**
- 문제점 : 배열을 사용해 삽입이나 삭제 연산이 일어날 때 원소가 재배치됨 --> 메모리 낭비 

## 5. 버퍼

- 데이터를 한 곳에서 다른 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 영역 
- `버퍼링` : 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작 