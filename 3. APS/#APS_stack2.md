# 스택2 (stack)

> - 계산기
> - 백트래킹
> - 분할 정복



## 계산기

- `후위표기법` : 연산자를 피연산자 뒤에 표기하는 방법 
  - AB+
- 컴퓨터는 입력을 후위표기법으로 바꿔서 계산하고 다시 중위표기법으로 바꿔준다

**1) 중위 표기식 --> 후위 표기식**

​	1) 수식의 각 연산자에 대해 우선순위에 따라 괄호를 사용하여 다시 표현 

​    2) 각 연산자를 그에 대응하는 오른쪽 괄호의 뒤쪽으로 이동

​    3) 괄호 제거

```MARKDO
예) A * B - C / D

1단계 : ((A * B) - (C / D))
2단계 : ((A B) * (C D)/)-
3단계 : AB*CD/-
```



**2) 중위 표기식 --> 후위 표기식 변환 알고리즘 (스택)**

```MARKDOWN
1단계 : 토큰을 읽는다 (각각의 원소 하나를 토큰이라고 함)
2-1단계 : 토큰이 피연산자이면 출력 (숫자, 알파벳 등)
2-2단계 : 토큰이 연산자이면(+, -, *, / 등 괄호 포함) 이 토큰이 스택top의 연산자의 우선순위가 토큰의 우선순위보다 높으면 스택에 push / 그렇지 않으면 top의 연산자의 우선순위가 토큰의 우선순위보다 작을 때까지 스택에서 pop한 후 토큰의 연산자를 push
2-3단계 : 토큰이 오른쪽 괄호 ')'이면 스택 top에 왼쪽 괄호 '('가 올 때까지 스택에 pop연산을 수행하고 pop한 연산자를 출력한다. 왼쪽 괄호를 만나면 pop만 하고 출력하지는 않는다.
3단계 : 중위 표기식에 더 읽을 것이 없다면 중지하고 더 읽을 것이 있다면 1단계부터 다시 반복한다 
4단계 : 스택에 남아있는 연산자를 모두 pop하여 출력한다.

*주의* 스택 밖의 왼쪽 괄호는 우선순위가 가장 높으며 스택 안의 왼쪽 괄호는 우선 순위가 가장 낮다 
```

|      | isp (in-stack priority) | icp (in-coming priority) |
| ---- | ----------------------- | ------------------------ |
| *, / | 2                       | 2                        |
| +,-  | 1                       | 1                        |
| ()   | 0                       | 3                        |

예시) 

5 + (7 + 4  / 2 * (5 - 4 + 5) * 1 / 2 + 1)

스택  

출력  5 7 4 2 / 5 4 - 5 + * 1 * 2 / + 1 + +

**중위표기법을 위한 내장함수 `eval()`이 있다**



## 백트래킹

- 해를 찾는 도중에 막히면 (즉, 해가 아니면) 되돌아가서 다시 해를 찾는 기법
- `최적화 문제`와 `결정 문제(문제의 조건을 만족하는 해가 존재하는지 여부를 y/n으로 답하는 문제)`를 해결할 수 있다
- 미로 찾기
  - n-Queen 문제
  - Map coloring
  - 부분집합의 합 문제
- 어떤 노드의 `유망성`을 점검한 후에 유망하지 않으면 그 노드의 부모로 되돌아가 다음 자식 노드로 간다 
- 어떤 노드를 방문해서 그 노드를 포함한 경로가 해답이 될 수 없으면 그 노드는 유망하지 않다고 함, 반대로 해답의 가능성이 있으면 유망하다고 함
- `가지치기(pruning)` : 유망하지 않은 노드가 포함되는 경로는 더 이상 고려하지 않는다



**백트래킹과 깊이우선탐색의 차이**

- 어떤 노드에서 출발하는 경로가 해결책으로 이어질 것 같지 않으면 더 이상 그 경로를 따라가지 않음으로써 시도의 횟수를 줄임
- 깊이 우선탐색이 모든 경로를 추적하는데 비해 백트래킹은 불필요한 경로를 조기에 차단 
- 깊이 우선 탐색을 하기에는 경우의 수가 너무 많은 경우 (N! 가지의 경우의 수를 가진 문제)에 처리 불가능한 문제를 처리
- 일반적으로 경우의 수가 줄어들지만 최악의 경우에(완전탐색이 됨) 지수함수 시간을 요하므로 처리 불가능, 조건이 잘못 들어갈 경우 정답의 경우도 차단될 수 있다



### 백트래킹을 이용한 알고리즘의 절차

1. 상태 공간 트리의 깊이 우선 검색 실시
2. 각 노드가 유망한지 점검
3. 만일 그 노드가 유망하지 않으면 그 노드의 부모 노드로 돌아가서 검색을 계속한다 

```python
def checknode(v):
if promising(v):
    if there is a solution at v:
        write the solution
    else:
        for u in each child of v:
            checknode(u)
```



**부분집합 구하기**

- `powerset` : 어떤 집합의 공집합과 자기자신을 포함한 모든 부분집합

```python
def backtrack(a, k, input):
    global MAXCANDIDATES
    c = [0] * MAXCANDIDATES #yes or no 저장
    
    if k == input:
        process_solution(a, k) #답이면 원하는 작업을 한다
    else:
        k += 1
        ncandidates = construct_candidates(a, k, input, c)
        for i in range(ncandidates):
            a[k] = c[i]
            backtrack(a, k, input)
            
def construct_candidates(a, k, input, c):
    c[0] = True
    c[1] = False
    return 2

MAXCANDIDATES = 100  #임의로 100 크기로 세팅 
NMAX = 100 
a = [0] * NMAX  #a는 해당 원소를 사용했는지 여부를 보여줌  
backtrack(a, 0, 3)
```

```python
N = 3

arr = [1, 2, 3]   #우리가 활용할 데이터

sel = [0] * N     #a리스트 (내가 해당 원소를 뽑았는지)

def powerset(idx):
    if idx == N:
        print(sel, ':', end = '  ')
        for i in range(N):	
            if sel[i]:
                print(arr[i], end = ' ')
        print()
        
        return
    #idx 자리의 원소를 뽑고간다
    sel[idx] = 1
    powerset(idx+1)
    #idx자리를 안뽑고 간다
    sel[idx] = 0
    powerset(idx+1)
    
powerset(0)
```



## 순열 생성

### 단순한 방법

```python
for i1 in range(1, 4):
    for i2 in range(1, 4):
        if i2 != i1:
            for i3 in range(1, 4):
                if i3 != i1 and i3 != i2:
                    print(i1, i2, i3)
```
### 백트래킹

```python
def backtrack(a, k, input):
    global MAXCANDIDATES
    c = [0] * MAXCANDIDATES
    
    if k == input:
       for i in range(1, K+1):
           print(a[i], end = ' ')
    else:
        k += 1
        ncandidates = construct_candidates(a, k, input, c)
        for i in range(ncandidates):
            a[k] = c[i]
            backtrack
```



## 퀵 정렬

