# Divide and Conquer

## 📌 1. Divide and Conquer (분할 정복) 소개

- 어떤 문제를 바로 풀기 어려운 경우 부분으로 나누어 부분문제를 풀고 부분 문제에 대한 solution을 활용해 전체문제를 풀어내는 방식
- 3 단계로 이뤄진다, 문제가 충분히 나눠질 때 까지 계속 나누는 과정이기 때문에 재귀에 대한 이해가 필요하다
    - Divide : 부분 문제로 분할
    - Conquer : 각 부분 문제 정복
    - Combine : 부분 문제들의 솔루션을 합쳐서 기존 문제 해결

![Divide%20and%20Conquer%20384b469c31274b51ba0c596dbc4e5f04/Untitled.png](Divide%20and%20Conquer%20384b469c31274b51ba0c596dbc4e5f04/Untitled.png)

## 📌 2. Divide and Conquer (분할 정복) 예시

![Divide%20and%20Conquer%20384b469c31274b51ba0c596dbc4e5f04/Untitled%201.png](Divide%20and%20Conquer%20384b469c31274b51ba0c596dbc4e5f04/Untitled%201.png)

```python
def consecutive_sum(start, end):
	if start == end:
		return start
	else:
		return consecutive_sum(start, (start + end) // 2) + consecutive_sum((start + end) // 2 + 1, end)
```

## 📌 3. 합병 정렬

- 크기 n인 배열을 입력받아, 배열의 크기가 1이 될때까지 두개로 나눈 후, 각 작은 배열을 재귀적으로 정렬하고 그 결과를 합병하는 방식

![Divide%20and%20Conquer%20384b469c31274b51ba0c596dbc4e5f04/Untitled%202.png](Divide%20and%20Conquer%20384b469c31274b51ba0c596dbc4e5f04/Untitled%202.png)

```python
# 2개의 리스트를 입력받아 하나의 정렬된 리스트로 합치는 함수
def merge(list1, list2):

	i = 0
	j = 0

	merged_list = []

	while i < len(list1) and j < len(list2):
		if list1[i] > list2[j]:
			merged_list.append(list2[j])
			j += 1
		else:
			merged_list.append(list1[i])
			i += 1

	if i == len(list1):
		merged_list += list2[j:]
	elif j == len(list2):
		merged_list += list1[i:]

	return merged_list

# 합병 정렬
def merge_sort(my_list):
    if len(my_list) < 2:
        return my_list
        
    else:
        mid = len(my_list) // 2
        arr1 = merge_sort(my_list[mid:])
        arr2 = merge_sort(my_list[:mid])
        
        return merge(arr1, arr2)
```

## 📌 4. 퀵 정렬

- 특정 파티션을 기준으로 파티션보다 작으면 좌측, 크면 우측에 정렬하며 정렬하는 방식
- Divide : 파티션
- Conquer : 정렬
- Combine : 역할이 없음

![Divide%20and%20Conquer%20384b469c31274b51ba0c596dbc4e5f04/Untitled%203.png](Divide%20and%20Conquer%20384b469c31274b51ba0c596dbc4e5f04/Untitled%203.png)

- Partition 함수 구현하기
    
    ```python
    # 두 요소의 위치를 바꿔주는 helper function
    def swap_elements(my_list, index1, index2):
        my_list[index1], my_list[index2] = my_list[index2], my_list[index1]
        
        return my_list
    
    # 퀵 정렬에서 사용되는 partition 함수
    def partition(my_list, start, end):
    		# big group의 시작점, index 
        b, i = 0, 0
        p = end
    
        # 범위안의 모든 값들을 볼 때까지 반복문을 돌린다
        while i < p:
            # i 인덱스의 값이 기준점보다 작으면 i와 b 인덱스에 있는 값들을 교환하고 b를 1 증가 시킨다
            if my_list[i] <= my_list[p]:
                swap_elements(my_list, i, b)
                b += 1
            i += 1
    
        # b와 기준점인 p 인덱스에 있는 값들을 바꿔준다
        swap_elements(my_list, b, p)
        p = b
    
        # pivot의 최종 인덱스를 리턴해 준다
        return p
    
    # 퀵 정렬
    def quicksort(my_list, start, end):
        # base case
        if end - start < 1:
            return
    
        # my_list를 두 부분으로 나누어주고,
        # partition 이후 pivot의 인덱스를 리턴받는다
        pivot = partition(my_list, start, end)
    
        # pivot의 왼쪽 부분 정렬
        quicksort(my_list, start, pivot - 1)
    
        # pivot의 오른쪽 부분 정렬
        quicksort(my_list, pivot + 1, end)
    
    # 테스트 1
    list1 = [4, 3, 6, 2, 7, 1, 5]
    pivot_index1 = partition(list1, 0, len(list1) - 1)
    print(list1)
    print(pivot_index1)
    
    # 테스트 2
    list2 = [6, 1, 2, 6, 3, 5, 4]
    pivot_index2 = partition(list2, 0, len(list2) - 1)
    print(list2)
    print(pivot_index2)
    
    # Optional Parameter로 좀 더 간단한 퀵정렬 구현하기 
    # 퀵 정렬
    def quicksort(my_list, start=0, end=None):
        if end == None:
            end = len(my_list) - 1
    
        # base case
        if end - start < 1:
            return
    
        # my_list를 두 부분으로 나누어주고,
        # partition 이후 pivot의 인덱스를 리턴받는다
        pivot = partition(my_list, start, end)
    
        # pivot의 왼쪽 부분 정렬
        quicksort(my_list, start, pivot - 1)
    
        # pivot의 오른쪽 부분 정렬
        quicksort(my_list, pivot + 1, end)
    ```