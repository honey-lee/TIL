# 분할 정복 / 백트래킹

> - 분할 정복 : 문제를 분할해서 해결하는 분할 정복 기법 (퀵 정렬, 병합 정렬 등)
> - 백 트래킹 : 상태 공간 트리의 모든 노드를 검색



## 분할 정복

> - 분할 : 해결할 문제를 여러 개의 작은 부분으로 나눈다
> - 정복 : 나눈 작은 문제를 각각 해결한다
> - 통합 : (필요하다면) 해결된 해답을 모은다

- 반복 알고리즘 : O(n)

- 분할 정복 기반의 알고리즘
  $$
  C^8 = C^4 * C^4 = ((C^2)^2)^2
  $$
  

```python
Recursive_Power(x, n):
    if n == 1:
        return x
    if n is even:
        y = Recursive_Power(x, n/2)
        return y * y
    else:
        y = Recursive_Power(x, (n-1)/2)
        return y * y * x
```



### 병합 정렬 : 2개의 부분집합을 정렬하면서 하나의 집합으로 병합

```python
mergesort(list, m):
    if length(m) == 1:
        return m
    list left, right
    middle = length(m) / 2
    for x in m before middle:
		add x to left
    for x in m after or equal middle:
        add x to right
        
    left = mergesort(left)
    right = mergesort(right)
    
    return merge(left, right)
```



### 퀵 정렬 

- Hoare-Partition 알고리즘
  - pivot보다 큰값은 오른쪽, 작은 값은 왼쪽에 위치하도록 하고 pivot은 중간에 

```python
partition(A[], l, r)
	# pivot
	p = A[l]
    # i는 왼쪽에서 오른쪽으로, j는 오른쪽에서 왼쪽으로 
    # i는 큰값을 찾아가고 j는 작은 값을 찾아간다
    i = l, j =r
    while i <= j:
        while A[i] <= p:
            i += 1
        while A[j] >= p:
            j -= 1
        if i < j: swap(A[i], A[j])
    
    # 맨 왼쪽이던 pivot을 경계점으로 바꿈
    swap(A[l], A[j])
   	return j
```



- Lomuto partition 알고리즘

```python
partition(A[], p, r)

	x = A[r]
    i = p - 1
    
    for j in range(p, r-1):
        if A[j] <= x:
            i += 1, swap(A[i], A[j])
    swap(A[i+1], A[r])
    return i + 1
```



### 이진 검색

- 검색 과정
  1. 자료의 중앙에 있는 원소를 고른다
  2. 중앙 원소의 값과 찾고자 하는 목표값을 비교
  3. 목표 값이 중앙 원소의 값보다 작으면 자료의 왼쪽 반에 대해서 새로 검색을 수행, 크다면 자료 오른쪽 반에 대해서 새로 검색을 수행
  4. 찾고자 하는 값을 찾을 때 까지 위의 과정을 반복

```python
binary_search(n, S[], k)

low = 0
high = n - 1

while low <= high and location == 0:
    mid = low + (high - low) / 2
    
    if S[mid] == key:
        return mid
    elif S[mid] > key:
        high = mid - 1
    elif S[mid] < key:
        low = mid + 1
return -1
```



## 백트래킹

> - 여러 가지 선택지들이 존재하는 상황에서 한가지를 선택한다
> - 선택이 이루어지면 새로운 **선택지들의 집합**이 생성됨
> - 이런 선택을 반복하면서 최종 상태에 도달
>   - 올바른 선택을 계속하면 최종 상태에 도달



```python
make_candidates(a[], k, n, c[], ncands)

	in_perm[NMAX] = False
    
    for i in range(1, k-1):
        in_perm[a[i]] = True
        
    ncand = 0
    for i in range(1, n):
        if in_perm[i] == False:
            c[ncands] = i
            ncands += 1
            
process_solution(a[], k)
for i in range(1, k):
    print(a[i])
```

