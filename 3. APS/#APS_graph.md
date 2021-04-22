# 그래프

> - 그래프
> - 그래프 탐색
> - 서로소 집합들
> - 최소 신장 트리 (MST)
> - 최단 경로



## 그래프

> - 무한 그래프 (Undirected Graph)
> - 유향 그래프 (Directed Graph)
> - 가중치 그래프 (Weighted Graph)
> - 사이클 없는 방향그래프 (DAG, Directed Acyclic Graph)
> - 완전 그래프 : 정점들에 대해 가능한 모든 간선들을 가진 그래프
> - 부분 그래프 : 원래 그래프에서 일부의 정점이나 간선을 제외한 그래프





## 그래프 경로

- 경로란 간선들을 순서대로 나열한 것
  - 간선들 : (0, 2), (2, 4), (4, 6)
  - 정점들 : 0 - 2 - 4- 6
  - 사이클 : 시작한 정점에서 끝나는 경로 1- 3 - 5 - 1
- 인접 리스트 : 각 정점에 대한 인접 정점들을 순차적으로 표현



## 깊이 우선 탐색

- 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법 





## 상호 배타 집합

> - 교집합이 없는 집합 (서로소 집합)

- 연산

  - Make-Set(a) ~ Make-Set(f) :  유일한 멤버 x를 포함하는 새로운 집합을 생성하는 연산

    ```python
    Make-Set(x)
    	p[x] = x
    ```

    

  - Union (c, d) : c와 d를  포함하는 두 집합을 통합하는 연산 

    - d가 c를 가리키게 함

    ```python
    Union(x, y):
        p[Find-Set(y)] = Find-Set(x)
    ```

    

  - Find-set(d) : d를 포함하는 집합을 찾는 연산

    ```python
    Find-Set(x)
    	if x == p[x]:
            return x
        else:
            return find_set(p[x])
    ```



- 연산의 효율을 높이는 방법
  - Rank를 이용한 Union
    - 두 집합을 합칠 때 rank가 낮은 집합을 rank가 높은 집합에 붙인다 



## 최소 신장 트리(MST)

> - 무방향 가중치 그래프에서 신장 트리를 구성하는 간선들의 가중치의 합이 최소인 신장 트리