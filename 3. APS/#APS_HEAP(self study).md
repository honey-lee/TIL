# 🧡🍯 HEAP에 관한 모든 것 (A-Z about HEAP)

[toc]

## 🌳힙이란?

**2개의 조건을 만족하는 트리**

**대표적으로 1. 정렬, 2.우선순위 큐를 위해 사용한다**

1. 형태 속성 : 완전 이진 트리 

2. 힙 속성 : 부모 노드의 데이터는 자식 노드와 비교할 때 최소 혹은 최대이다 (최소힙, 최대힙) 

   1. 최대 힙(max heap)
      - 부모노드의 키 값 > 자식노드의 키 값
      - 루트 노드 : 키 값이 가장 큰 노드
   2. 최소 힙(min heap)
      - 부모노드의 키 값 < 자식노드의 키 값
      - 루트 노드 : 키 값이 가장 작은 노드 

   ![백준 11279번 최대 힙 [Heap] :: 마이구미 :: 마이구미의 HelloWorld](https://t1.daumcdn.net/cfile/tistory/25335F4357A4226509)



### 1. 힙 구현

- 완전 이진 트리이기 때문에 **동적 배열**로 구현할 수 있음

  - 왼쪽 자식 인덱스 : `idx * 2`
  - 오른쪽 자식 인덱스 : `idx * 2 + 1`

- `heapify` : 힙의 힙 속성이 만족될 때까지 부모 노드와 자식 노드를 재배치 한다

  - 시간복잡도
    - 최악의 경우 : 루트 노드부터 가장 하단의 리프 노드까지 교환이 일어나는 경우 O(log(n)), 즉 트리의 높이만큼의 시간복잡도이다.

- 힙이 생성될 때 시간복잡도 : O(nlog(n)) => n 층의 트리에 대해 log(n)만큼의 시간복잡도가 발생하기 때문 

  ```python
  # heapify를 통해 최대힙 구현
  
  def heapify(tree, index, tree_size):
      # 부모 노드와 왼쪽 자식, 오른쪽 자식
      largest = index
      left_index = 2 * index 
      right_index = 2 * index + 1
      
      # 왼쪽 자식이 존재하고 부모 노드의 값보다 크면 서로 교체
      if left_index < tree_size and tree[left_index] > tree[largest]:
          largest = left_index
      # 오른쪽 자식이 존재하고 부모 노드의 값보다 크면 서로 교체
      if right_index < heap_size and tree[right_index] > tree[largest]:
          largest = right_index
      # 부모노드의 값이 최대값이 아니면
      if largest != index:
          # 교체
          tree[largest], tree[index] = tree[index], tree[largest]
          
  heapify(tree, largest, heap_size)
  ```



## 📌힙 정렬

- 힙 정렬의 과정

  1. 힙 생성
  2. root와 마지막 뿌리 노드 교환
  3. (바꾼 노드는 없는 노드 취급)
  4. 새로운 노드가 힙 속성을 지킬 수 있게 heapify

  ```python
  # 완전 이진트리에서 두개 노드의 위치를 바꿔주는 함수
  def swap(tree, index_1, index_2):
  	tree[index_1], tree[index_2] = tree[index_2], tree[index_1]
      
  # 힙 정렬
  def heapsort(tree):
      
      tree_size = len(tree)
      
      # 마지막 인덱스부터 처음인덱스까지 heapify
      for index in range(tree_size, 0, -1):
          heapify(tree, index, tree_size)
      
      # 마지막 인덱스 부터 처음인덱스까지 
      for i in range(tree_size-1, 0, -1):
          # root노드와 마지막 인덱스를 바꿔준 후
          swap(tree, 1, i)
          # heapify
          heapify(tree, 1, i)
  ```




- 힙 정렬의 효율성 : 퀵 정렬과 유사한 정도의 빠른 축에 속함
  1. 힙 생성  => O(nlog(n))
  2. root와 마지막 뿌리 노드 교환 => O(1)
  3. (바꾼 노드는 없는 노드 취급) 
  4. 새로운 노드가 힙 속성을 지킬 수 있게 heapify => O(nlog(n))

![image-20210413161715757](C:\Users\leejo\AppData\Roaming\Typora\typora-user-images\image-20210413161715757.png)





## 📌 우선순위 큐

- 큐나 스택과 같은 **추상자료형** (내부적인 구현보다 기능에 집중하게 해주는 개념)
- 기능 
  - 데이터를 저장
  - 저장한 데이터가 **우선순위 순서대로** 나온다
  - 우선순위가 있기 때문에 일상 업무 시 유용하게 사용 가능 
    - 예)  우선순위가 높은 고객의 요청 먼저 처리, 자주 접수된 불만사항 우선처리 등 



### 1. 힙에 데이터 삽입하기 

- 최대 힙일 경우 

    1. 힙의 마지막 인덱스에 데이터 삽입
    2. 삽입한 데이터와 부모노드의 데이터를 비교
    3. 부모 노드의 데이터가 더 작으면 위치 교환
    4. 2 ~ 3의 과정을 힙 속성을 충족할 때 까지 반복
    
    
    
    ```python
    def heapify(tree, index):
        # 부모 인덱스의 값은 자식 인덱스를 몫으로 2연산해서 구하고
        parent_index = index // 2
        # 부모 인덱스의 값이 유효하고 자식 인덱스 보다 작다면
        if 0 < parent_index <= len(tree) and tree[parent_index] < tree[index]:
            # 위에서 만든 swap 함수를 통해 서로 교환하고 
            swap(tree, parent_index, index)
            # heapify 작업 반복
            heapify(tree, parent_index)
    
    # 힙으로 구현한 우선순위 큐 
    class PriorityQueue:
        def __init__(self):
            self.heap = [None]
            
        def insert(self, data):
            self.heap.append(data)
            heapify(self.heap, len(self.heap)-1)
            
        def __str__(self):
            return str(self.heap)
    ```



- 시간 복잡도 : 최악의 경우 O(log(n))

    1. 힙의 마지막 인덱스에 데이터 삽입  => O(1)
    2. 삽입한 데이터와 부모노드의 데이터를 비교 => O(1)
    3. 부모 노드의 데이터가 더 작으면 위치 교환 => O(log(n)) (최악의 경우)
    4. 2 ~ 3의 과정을 힙 속성을 충족할 때 까지 반복



### 2. 힙에서 최고 우선순위 데이터 추출하기 

> 삭제 기능과 동일하게 동작

- 우선 순위를 가장 큰 수이며, 최대힙으로 정렬되어 있다고 가정 
  1. root 노드와 마지막 노드를 서로 교환
  2. 마지막 노드의 데이터를 저장
  3. 마지막 노드 삭제
  4. heapify를 통해 다시 힙 속성 회복
  5. 2번에서 저장한 데이터 리턴

```python
# 힙으로 구현한 우선순위 큐 
class PriorityQueue:
    def __init__(self):
        self.heap = [None]
        
    def insert(self, data):
        self.heap.append(data)
        heapify(self.heap, len(self.heap)-1)
        
    # 최고값 추출 메소드
    def extract_max(self):
        # root 노드와 마지막 노드 교환
        swap(self.heap, 1, len(self.heap)-1)
        # 원래 root에 있던 값이 pop되어서 max_value에 저장됨
		max_value = self.heap.pop()
        # 나머지 남은 heap은 다시 heapify를 통해 재정렬
        heapify(self.heap, 1, len(self.heap))
        return max_value
        
    def __str__(self):
        return str(self.heap)
```





## HEAP Summary

1. 퀵 정렬과 유사한 정도의 성능을 낼 수 있는 정렬 방법

![image-20210413153624174](C:\Users\leejo\AppData\Roaming\Typora\typora-user-images\image-20210413153624174.png)

2. 주로 우선순위 큐 구현에 사용됨

   - 우선 순위 큐 구현 시 `정렬된 동적 배열`, `정렬된 더블리 링크드 리스트` 를 사용하는 방법도 있다.

   - 힙으로 구현 시 데이터를 **삽입할 때** 다른 방법에 비해 더 효율적이다.

   - 왜 그런지 조금만 더 알아보자

     1. 정렬된 동적 배열

        1. 데이터 삽입 : 삽입될 위치를 찾고`이진 탐색 사용 시 O(log(n))` 데이터를 넣는다`O(n)`
        2. 데이터 추출 : O(1) - 정렬된 상태이므로 가장 앞이나 뒤에서 추출

     2. 정렬된 더블리 링크드 리스트

        > 더블리 링크드 리스트 :  노드와 노드가 서로 연결된 리스트 형태

        1. 데이터 삽입 : 정렬되어 있어서 삽입할 위치를 찾는 데 선형적으로 보니까 `O(n)` 이 걸리고 데이터를 넣는건 `O(1)`
        2. 데이터 추출 : 위와 마찬가지로 추출만 하면되서 O(1)

![image-20210413164415460](C:\Users\leejo\AppData\Roaming\Typora\typora-user-images\image-20210413164415460.png)

​	

