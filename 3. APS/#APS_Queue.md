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


## 선형큐

- **1차원 배열을 이용한 큐**

- 큐의 크기 = 배열의 크기

- 상태 표현

  - 초기 상태 : front = rear = -1
  - 공백 상태 : front = rear
  - 포화 상태: rear = n-1 (n : 배열의 크기, n-1 : 배열의 마지막 인덱스)

  

## 큐 생성

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








