#Graph(2020.11.10)
## 그래프(Graph)의 개념
- 단순히 노드(N, node)와 그 노드를 연결하는 간선(E, edge)을 하나로 모아 놓은 자료구조 
	- 즉 연결되어 있는 객체 간의 관계를 표현할 수 있는 자료 구조이다.
	- Ex) 지도, 지하철 노선도의 최단 경로, 전기 회로의 소자들, 도로(교차점과 일방 통행길), 선수 과목 등
	- 그래프는 여러 개의 고립된 부분 그래프(Isolated Subgraphs)로 구성될 수 있다. 
	
## 그래프(Graph)의 특징
- 그래프는 네트워크 모델이다.
- 2개 이상의 경로가 가능하다.
	- 즉, 노드들 사이에 무방향/방향에서 양방향 경로를 가질 수 있다. 
- self-loop 뿐 아니라 loop/circuit 모두 가능하다. 
- 루트 노드라는 개념이 없다.
- 부모-자식 관계라는 개념이 없다.
- 순회는 DFS나 BFS로 이루어진다. 
- 그래프는 순환(Cyclic) 혹은 비순환(Acyclic)이다. 
- 그래프는 크게 방향 그래프와 무방향 그래프가 있다.
- 간선의 유무는 그래프에 따라 다르다. 

## 그래프 용어 정리

### Undirected Graph와 Directed Graph(Digraph)
말 그대로 정점과 간선의 연결관계에 있어서 방향성 없는 그래프를 Undirected Graph라 하고, 간선에 방향성이 포함되어 있는 그래프를 Directed Graph라고 한다. 

- Directed Graph(Digraph)

```
V = {1, 2, 3, 4, 5, 6}
E = {(1, 4), (2,1), (3, 4), (3, 4), (5, 6)}
(u, v) = vertex u에서 vertex v로 가는 edge
```
- Undirected Graph
```
V = {1, 2, 3, 4, 5, 6}
E = {(1, 4), (2,1), (3, 4), (3, 4), (5, 6)}
(u, v) = vertex u와 vertex v를 연결하는 edge
```

### Degree
Undirected Graph에서 각 정점(Vertex)에 연결된 Edge의 개수를 Degree라 한다. Directed Graph에서는 간선에 방향성이 존재하기 때문에 Degree가 두 개로 나뉘게 된다. 각 정점으로부터 나가는 간선의 개수를 Outdegree라 하고, 들어오는 간선의 개수를 Indegree라고 한다. 

### 가중치 그래프(Weight Graph)와 부분 그래프(Sub Graph)
가중치 그래프란 간선에 가중치 정보를 두어서 구성한 그래프를 말한다. 반대 개념인 비가중치 그래프 즉, 모든 간선의 가중치가 동일한 그래프도 존재한다. 부분 집합과 유사한 개념으로 부분 그래프라는 것이 있다. 부분 그래프는 본래의 그래프의 일부 정점 및 간선으로 이루어진 그래프를 말한다. 


## 그래프를 구현하는 두 방법
### 인접 행렬(adjacent matrix) : 정방 행렬을 사용하는 방법 
해당하는 위치의 value 값을 통해서 vertex 간의 연결관계를 O(1)으로 파악할 수 있다. Edge 개수와는 무관하게 V^2의 Space Complexity를  갖는다. Dense Graph를 표현할 때 적절한 방법이다.

### 인접 리스트(adjacent list) : 연결 리스트를 사용하는 방법 
vertex의 adjacent list를 확인해봐야 하므로 vertex 간 연결되어 있는지 확인하는데 오래 걸린다. Space Complexity는 O(E + V)이다. Sparse graph를 표현하는데 적당한 방법이다. 

## 그래프 탐색
그래프는 정점의 구성 뿐만 아니라 간선의 연결에도 규칙이 존재하지 않기 때문에 탐색이 복잡하다. 따라서 그래프의 모든 정점을 탐색하기 위한 방법은 다음의 두 가지 알고리즘을 기반으로 한다. 

### 깊이 우선 탐색(Depth First Search : DFS)
그래프 상에 존재하는 임의의 한 정점으로부터 연결되어 있는 한 정점으로만 나아간다라는 방법을 우선으로 탐색한다. 일단 연결된 정점으로 탐색하는 것이다. 연결할 수 있는 정점이 있을 때까지 계속 연결하다가 더 이상 연결되지 않은 정점이 없으면 바로 그 전 단계의 정점으로 돌아가서 연결할 수 있는 정점이 있는지 살펴봐야 할 것이다. 갔던 길을 되돌아 오는 상황이 존재하는 미로찾기처럼 구성하면 되는 것이다. Stack 자료구조를 이용해서 구현한다. 

**Time Complexity : O(V + E) -> Vertex 개수 + Edge 개수**

### 너비 우선 탐색(Breadth First Search : BFS)
그래프 상에 존재하는 임의의 한 정점으로부터 연결되어 있는 모든 정점으로 나아간다. Tree에서의 Level Order Transversal 형식으로 진행되는 것이다. BFS에서는 자료구조로 Queue를 사용한다. 연락을 취할 정점의 순서를 기록하기 위한 것이다. 우선, 탐색을 시작하는 정점을 Queue에 넣는다.(Enqueue) 그리고 dequeue를 하면서 dequeue 하는 정점과 간선으로 연결되어 있는 정점들을 enqueue 한다. 즉 vertex 들을 방문한 순서대로 queue 에 저장하는 방법을 사용하는 것이다.
**Time Complexity : O(V + E) -> Vertex 개수 + Edge 개수 , BFS로 구한 경로는 최단 경로이다.**


## Minimum Spanning Tree
그래프 G의 Spanning tree 중 edge weight의 합이 최소인 `spanning tree`를 말한다. 여기서 말하는 `spanning tree`란 그래프 G의 모든 vertex가 cycle이 없이 연결된 형태를 말한다. 

## Kruskal Algorithm
초기화 작업으로 `edge`없이 vertex들 만으로 그래프를 구성한다. 그리고 weight 가 제일 작은 edge 부터 검토한다. 그러기 위해선 Edge Set 을 non-decreasing 으로 sorting 해야 한다. 그리고 가장 작은 weight 에 해당하는 edge 를 추가하는데 추가할 때 그래프에 cycle 이 생기지 않는 경우에만 추가한다. spanning tree 가 완성되면 모든 vertex 들이 연결된 상태로 종료가 되고 완성될 수 없는 그래프에 대해서는 모든 edge 에 대해 판단이 이루어지면 종료된다.

### 어떻게 cycle 생성 여부를 판단하는가?
Graph의 각 vertex에 `set-id`라는 것을 추가적으로 부여한다. 그리고 초기화 과정에서 모두 1~n까지의 값으로 각각의 vertex들을 초기화한다. 여기서 0은 어떠한 edge와도 연결되지 않았음을 의미하게 된다. 그리고 연결할 때마다 `set-id`를 하나로 통일시키는데, 값이 동일한 `set-id`개수가 많은 `set-id`로 통일한다. 

### Time Complexity
1. Edge의 weight를 기준으로 sorting - O(E logE)
2. cycle 생성 여부를 검사하고 set-id를 통일 -O(E + Vlog V) => 전체 시간 복잡도 : O(E logE)

## Prim Algorithm
초기화 과정에서 한 개의 vertex 로 이루어진 초기 그래프 A 를 구성한다. 그리고나서 그래프 A 내부에 있는 vertex 로부터 외부에 있는 vertex 사이의 edge 를 연결하는데 그 중 가장 작은 weight 의 edge 를 통해 연결되는 vertex 를 추가한다. 어떤 vertex 건 간에 상관없이 edge 의 weight 를 기준으로 연결하는 것이다. 이렇게 연결된 vertex 는 그래프 A 에 포함된다. 위 과정을 반복하고 모든 vertex 들이 연결되면 종료한다.

### Time Complexity
=> 전체 시간 복잡도 : O(E log V)





