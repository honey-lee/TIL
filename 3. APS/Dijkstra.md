# Dijkstra

## 변수

- Distance : 특정 노드까지의 최단 거리 예상치
- Predecessor : 현재까지의 최단 경로에서 바로 직전의 노드
- Complete : 노드까지의 최단 경로를 찾았다고 표시하기 위한 변수



# Edge Relaxation

- A에서 B를 방문하면서 B의 distance, predecessor를 바꾸는 것





- 시작점의 distance를 0으로, predecessor를 None으로
- 모든 노드가 complete일 때까지:
  - complete하지 않은 노드 중 distnace가 가장 작은 노드 선택
  - 이 노드에 인접한 노드 중 complete하지 않은 노드를 돌면서 :
    - 각 엣지를 relax한다
  - 현재 노드를 complete 처리한다