# Greedy Algorithm

## 📌 1. Greedy Algorithm 소개

- 미래를 내다보지 않고 당장 눈 앞에 보이는 최적의 선택을 하는 방식
- 목표를 달성하기 위해 매 순간 탐욕적인 선택을 한다
- 장점 : 간단하고 빠르다
    - Divide : 부분 문제로 분할
    - Conquer : 각 부분 문제 정복
    - Combine : 부분 문제들의 솔루션을 합쳐서 기존 문제 해결
- 단점 : 최적의 답이 보장되지 않는다 - 치명적인 단점이다

![Greedy%20Algorithm%2060b622552a6542209bbcdea095d63c1d/Untitled.png](Greedy%20Algorithm%2060b622552a6542209bbcdea095d63c1d/Untitled.png)

## 📌 2. 언제 Greedy Algorithm을 사용할까?

- 문제를 해결하는 다른 알고리즘이 너무 느린 경우 대안으로 사용
- 최적의 답이 필요없을 때
- **Greedy Algorithm이 최적의 답을 보장해주는 경우도 있다**
    - 최적 부분 구조 : 부분 문제들의 최적의 답을 이용해서 기존 문제의 최적의 답을 구할 수 있다는 것
    - 탐욕적 선택 속성 : 각 단계에서의 탐욕스런 선택이 최종 답을 구하기 위한 최적의 선택
    - ***위의 두 속성을 모두 갖췄다면 Greedy Algorithm을 사용해 최적의 답을 찾을 수 있다!***
        
        ***(ex. 동전을 최대한 적게 사용해서 거스름돈 주기)***
        
        ***최적 부분 구조***
        
    
    ![Greedy%20Algorithm%2060b622552a6542209bbcdea095d63c1d/Untitled%201.png](Greedy%20Algorithm%2060b622552a6542209bbcdea095d63c1d/Untitled%201.png)
    
    ***탐욕적 선택 속성***
    
    ![Greedy%20Algorithm%2060b622552a6542209bbcdea095d63c1d/Untitled%202.png](Greedy%20Algorithm%2060b622552a6542209bbcdea095d63c1d/Untitled%202.png)
    

## 📌 3. 동전을 최대한 적게 사용하기

```python
def min_coin_count(value, coin_list):
	# 누적 동전 갯수
	answer = 0
	
	# coin_list의 값들을 큰 순서대로 본다 
	for coin in sorted(coin_list, reverse=True):
		# 현재 동전으로 몇 개 거슬러 줄 수 있는지 확인
		answer += (value // coin)

		# 잔액 계산
		value %= coin
	
	return answer

# 테스트
default_coin_list = [100, 500, 10, 50]
print(min_coin_count(1440, default_coin_list))
print(min_coin_count(1700, default_coin_list))
print(min_coin_count(23520, default_coin_list))
print(min_coin_count(32590, default_coin_list))
```

## 📌 4. 최대 곱 구하기

### **힌트 1**

Brute Force 방식으로 하면 가능한 모든 곱을 구한 후 비교할 수 있지만, 굉장히 비효율적입니다. Greedy Algorithm으로 비효율을 해결해 봅시다.

이 문제를 풀 때, 각 단계에서 어떤 탐욕적 선택을 할 수 있을까요?

### **힌트 2**

이 문제에서 할 수 있는 탐욕적 선택은 각 뭉치에서 가장 큰 값을 선택하는 것입니다.

```python
def max_product(card_lists):
		# 누적된 곱을 저장하는 변수
    answer = 1
    
		# 반복문을 돌면서 카드 뭉치를 하나씩 본다 
    for card in card_lists:
				# 각 뭉치의 최댓값을 곱해준다
        answer *= max(card)
        
    return answer

# 테스트
test_cards1 = [[1, 6, 5], [4, 2, 3]]
print(max_product(test_cards1))

test_cards2 = [[9, 7, 8], [9, 2, 3], [9, 8, 1], [2, 8, 3], [1, 3, 6], [7, 7, 4]]
print(max_product(test_cards2))

test_cards3 = [[1, 2, 3], [4, 6, 1], [8, 2, 4], [3, 2, 5], [5, 2, 3], [3, 2, 1]]
print(max_product(test_cards3))

test_cards4 = [[5, 5, 5], [4, 3, 5], [1, 1, 1], [9, 8, 3], [2, 8, 4], [5, 7, 4]]
print(max_product(test_cards4))
```

## 📌 5. 지각 벌금 적게 내기

### **힌트 1**

Brute Force로 가능한 모든 조합들을 비교하는 방법도 있습니다. 하지만 너무 오래 걸리겠죠.

이 문제에는 최적 부분 구조와 탐욕적 선택 속성이 있기 때문에, Greedy Algorithm 방식으로 효율적이면서도 정확한 함수를 구현할 수 있습니다.

이 문제에서, 매 단계마다 가장 좋아 보이는 선택은 무엇일까요?

### **힌트 2**

기다리는 시간을 최소화하기 위해서는, 페이지 수가 적은 사람 순으로 출력하면 됩니다. 즉, **`pages_to_print`**를 오름차순으로 정렬하면 된다는 거죠.

```python
def min_fee(pages_to_print):
    fee = 0
    # 인원
    people = len(pages_to_print)
    
		# 정렬된 리스트에서 총 벌금 계산
    for i in sorted(pages_to_print):
        fee += (i * people)
        people -= 1
        
    return fee
    

# 테스트
print(min_fee([6, 11, 4, 1]))
print(min_fee([3, 2, 1]))
print(min_fee([3, 1, 4, 3, 2]))
print(min_fee([8, 4, 2, 3, 9, 23, 6, 8]))
```

## 📌 6. 수강 신청 분석

가능한 선택을 살펴봅시다.

1. **가장 먼저 시작하는 수업을 고른다.**
2. **겹치는 수업이 가장 적은 수업을 고른다.**
3. **가장 짧은 수업을 고른다.**
4. **가장 먼저 끝나는 수업을 고른다.**

이 네 가지 정도가 있는데요. 어떤 방법을 선택하는 게 가장 좋을까요?

각 경우에 대해서 반례(틀리다고 증명하는 예시)를 찾아봅시다.

(1) 가장 일찍 시작하는 수업을 고른다.

```
course_selection([(2, 5), (8, 10), (5, 9), (1, 16), (2, 6), (13, 16), (9, 11)])

```

위 경우 가장 일찍 시작하는 수업인 **`(1, 16)`**을 선택하면, 나머지 모든 수업들을 못 듣게 됩니다. 그러니 당연히 이 방법으로는 정답을 찾을 수 없겠죠?

(2) 겹치는 수업이 가장 적은 수업을 고른다.

```
course_selection([(2, 5), (2, 5), (2, 5), (1, 3), (4, 7), (6, 9), (8, 11), (12, 14), (10, 13), (10, 13), (10, 13)])

```

위 경우 가장 적게 겹치는 수업부터 고르면 **`[(6, 9), (2, 5), (10, 13)]`**을 듣게 됩니다. 하지만 실제로는 **`[(1, 3), (4, 7), (8, 11), (12, 14)]`**와 같이 4개의 수업을 들을 수 있죠.

반례를 찾았으니 이 방식은 최선이 아니라는 것을 알 수 있습니다.

(3) 가장 짧은 수업들을 고른다.

```
course_selection([(1, 6), (2, 6), (5, 8), (7, 11), (7, 12), (7, 13)])

```

이 경우에는 가장 짧은 수업인 **`(5, 8)`**을 선택하면, 나머지 모든 수업들을 못 듣게 됩니다. 따라서 이 방법으로도 정답을 찾을 수 없습니다.

(4) 가장 먼저 끝나는 수업을 고른다.

이 방법은 딱히 반례가 떠오르지 않는데요. 그럼 아예 거꾸로 생각해서, 정답 리스트에 가장 일찍 끝나는 수업이 포함되어 있지 않다고 가정합시다.

그 정답 리스트를 **`answer`**라고 하고, 전체 목록을 끝나는 순으로 정렬한 것을 **`sorted_list`**라고 할게요.

![https://i.imgur.com/KgJ1ojc.jpg](https://i.imgur.com/KgJ1ojc.jpg)

보시다시피 정답 리스트인 **`answer`**에는 가장 일찍 끝나는 수업 1이 포함되어 있지 않습니다. 하지만 우리가 원한다면 수업 2를 수업 1로 교체할 수도 있겠죠? 즉, 수업 개수를 바꾸지 않고 **`answer`**에 수업 1을 포함시킬 수 있다는 것입니다.

혹은 이렇게 해석할 수도 있습니다.

> 남은 수업 중 가장 먼저 끝나는 수업을 선택하면, 늘 최선의 결과를 이뤄낼 수 있다.
> 

이 문제는 탐욕적 선택 속성이 있군요!

```python
# 나의 풀이
def course_selection(course_list):
		# 수업을 끝나는 순서로 정렬한다
    course_list = sorted(course_list, key=lambda x: x[1])
    now = course_list[0][1]
		# 가장 먼저 끝나는 수업은 무조건 듣는다
    answer = [course_list[0]]
    
		# 이미 선택한 수업과 안 겹치는 수업 중 가장 빨리 끝나는 수업을 고른다
    for i in range(1, len(course_list)):
				# 마지막 수업이 끝나기 전에 새 수업이 시작하면 겹친다
        if course_list[i][0] > now:
            answer.append(course_list[i])
            now = course_list[i][1]
        else:
            continue
    
    return answer

# 테스트
print(course_selection([(6, 10), (2, 3), (4, 5), (1, 7), (6, 8), (9, 10)]))
print(course_selection([(1, 2), (3, 4), (0, 6), (5, 7), (8, 9), (5, 9)]))
print(course_selection([(4, 7), (2, 5), (1, 3), (8, 10), (5, 9), (2, 5), (13, 16), (9, 11), (1, 8)]))
```

```python
# 코드잇 풀이
def course_selection(course_list):
    # 수업을 끝나는 순서로 정렬한다
    sorted_list = sorted(course_list, key=lambda x: x[1])

    # 가장 먼저 끝나는 수업은 무조건 듣는다
    my_selection = [sorted_list[0]]

    # 이미 선택한 수업과 안 겹치는 수업 중 가장 빨리 끝나는 수업을 고른다
    for course in sorted_list:
        # 마지막 수업이 끝나기 전에 새 수업이 시작하면 겹친다
        if course[0] > my_selection[-1][1]:
            my_selection.append(course)

    return my_selection

# 테스트
print(course_selection([(6, 10), (2, 3), (4, 5), (1, 7), (6, 8), (9, 10)]))
print(course_selection([(1, 2), (3, 4), (0, 6), (5, 7), (8, 9), (5, 9)]))
print(course_selection([(4, 7), (2, 5), (1, 3), (8, 10), (5, 9), (2, 5), (13, 16), (9, 11), (1, 8)]))
```