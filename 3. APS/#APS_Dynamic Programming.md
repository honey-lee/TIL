# Dynamic Programming

- Dynamic Programming의 조건
    - 최적 부분 구조  (Optimal Substructure)
    - 중복되는 부분 문제 (Overlapping Subproblems)

## 📌 1. 최적 부분 구조 (Optimal Substructure)

- 부분 문제들의 최적의 답을 이용해서 기존 문제의 최적의 답을 구할 수 있다

![Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled.png](Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled.png)

![Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%201.png](Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%201.png)

## 📌 2. 중복되는 부분 문제 (Overlapping Subproblems)

- 중복된 부분 문제들이 중첩되어 있는 형태, 다만 합병정렬의 경우 부분 문제 (각 리스트 정렬)로 나눠지긴하나 독립적으로 합병을 실행하기 때문에 중복되지 않는 부분 문제에 속한다.

![Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%202.png](Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%202.png)

## 📌 3. Dynamic Programming

1. 최적 부분구조가 있다
2. 부분 문제들의 최적의 답을 이용해서 기존 문제를 풀 수 있다 (기존 문제를 부분 문제로 나눠서 풀 수 있다)
3. 중복되는 부분 문제들이 있을 수 있다
4. 이 때, 중복되는 문제들을 계속해서 중복으로 풀면 비효율적이다. 이런 비효율을 해결하는 것이 DP이다. 
- `Dynamic Programming` : 한 번 계산한 결과를 재활용하는 방식
    1. Memoization
    2. Tabulation
    

## 📌 4. Memoization

- 중복되는 계산은 한 번만 계산 후 메모해두는 방식
- Cache에 기록해둠
- 하향식 접근

![Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%203.png](Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%203.png)

- 피보나치 수열 Memoization
    
    ```python
    def fib_memo(n, cache):
    	# base case
    	if n < 3:
    		return 1
    	
    	# 이미 n 번째 피보나치를 계산했으면 저장된 값을 바로 리턴
    	if n in cache:
    		return cache[n]
    	
    	# 아직 n 번째 피보나치를 계산하지 않았으면 계산을 한 후 cache에 저장 
    	cache[n] = fib_memo(n - 1, cache) + fib_memo(n - 2, cache)
    
    	# 계산된 값 리턴
    	return cache[n]
    
    def fibo(n):
    	# n번째 피보나치 수를 담는 사전
    	fib_cache = {}
    
    	return fib_memo(n, fib_cache)
    ```
    

## 📌 5. Tabulation

- 상향식 접근
- 테이블 방식으로 표를 채워나가며 정리하는 방식

![Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%204.png](Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%204.png)

- 피보나치 수열 Tabulation

```python
def fib_tab(n):
    # 이미 계산된 피보나치 수를 담는 리스트
    fib_table = [0, 1, 1]

    # n번째 피보나치 수까지 리스트를 하나씩 채워 나간다
    for i in range(3, n + 1):
        fib_table.append(fib_table[i - 1] + fib_table[i - 2])

    # 피보나치 n번째 수를 리턴한다
    return fib_table[n]
```

## 📌 6. `Memoization` vs `Tabulation`

- 둘 다 중복되는 부분 문제의 비효율을 제거한다는 공통점이 있음
- Memoization : 재귀, Stack의 누적으로 인한 과부하가 걸릴 위험이 있음
- Tabulation : 반복문, 처음부터 모두 계산하기 때문에 필요없는 부분도 계산할 수 있는 비효율성이 있음

## 📌 7. Dynamic Programming 공간 최적화

- Tabulation의 피보나치 수열 복잡도
    - 시간 복잡도 : O(n)
    - 공간 복잡도 : O(n)
- 복잡도를 개선하기 위해 모든 값을 계산하는 리스트 방식 대신 **이전의 두개 변수만 저장하는 방식**으로 current, previous 등의 변수를 사용할 수 있다.
- 공간복잡도는 O(1)이 된다.

```python
def fib_optimization(n):
	prev, cur = 0, 1
	
	if n == 1:
		return cur	

	# 반복적으로 위의 변수들을 업데이트 한다.
	for i in range(1, n):
		prev, cur = cur, prev + cur

	return cur
```

## 📌 최대 수익내기 문제

![Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%205.png](Dynamic%20Programming%205e8e249065b04e7c952daa80ad2c714b/Untitled%205.png)

```python
def max_profit_memo(price_list, count, cache):
    # Base Case: 0개 혹은 1개면 부분 문제로 나눌 필요가 없기 때문에 가격을 바로 리턴한다
    if count < 2:
        cache[count] = price_list[count]
        return price_list[count]

    # 이미 계산한 값이면 cache에 저장된 값을 리턴한다
    if count in cache:
        return cache[count]

    # profit은 count개를 팔아서 가능한 최대 수익을 저장하는 변수
    # 팔려고 하는 총개수에 대한 가격이 price_list에 없으면 일단 0으로 설정
    # 팔려고 하는 총개수에 대한 가격이 price_list에 있으면 일단 그 가격으로 설정
    if count < len(price_list):
        profit = price_list[count]
    else:
        profit = 0

    # count개를 팔 수 있는 조합들을 비교해서, 가능한 최대 수익을 profit에 저장
    for i in range(1, count // 2 + 1):
        profit = max(profit, max_profit_memo(price_list, i, cache) 
                 + max_profit_memo(price_list, count - i, cache))

    # 계산된 최대 수익을 cache에 저장
    cache[count] = profit

    return profit

def max_profit(price_list, count):
    max_profit_cache = {}

    return max_profit_memo(price_list, count, max_profit_cache)

```

```python
def max_profit(price_list, count):
    # 개수별로 가능한 최대 수익을 저장하는 리스트
    # 새꼼달꼼 0개면 0원
    profit_table = [0]

    # 개수 1부터 count까지 계산하기 위해 반복문
    for i in range(1, count + 1):
        # profit은 count개를 팔아서 가능한 최대 수익을 저장하는 변수
        # 팔려고 하는 총개수에 대한 가격이 price_list에 있으면 일단 그 가격으로 설정
        # 팔려고 하는 총개수에 대한 가격이 price_list에 없으면 일단 0으로 설정   
        if i < len(price_list):
            profit = price_list[i]
        else:
            profit = 0

        # count개를 팔 수 있는 조합들을 비교해서, 가능한 최대 수익을 찾는다
        for j in range(1, i // 2 + 1):
            profit = max(profit, profit_table[j] + profit_table[i - j])

        profit_table.append(profit)

    return profit_table[count]
```