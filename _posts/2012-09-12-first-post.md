---
title: First Post
author: Chris
layout: post
---


## 그래프 탐색 알고리즘
(그래프의 모든 노드를 방문)

# 1. 깊이 우선 탐색(DFS, Depth First Search)
    - 현재 정점에서 갈 수 있는 점들 중, 한 곳을 우선적으로 끝까지 탐색
    - 방법 : 스택이나 재귀함수로 구현
    - 단순 검색에 있어서는 BFS보다 느리지만 백트래킹, 미로 생성 알고리즘에 많이 쓰임
    - 찾는 노드가 있는 루트 이외의 무한 루트에 빠졌을 때 거기서 헤어 나오지 못함
    - 저장 공간이 많이 필요하지 않아서(재귀로 구현했을 경우) 모든 경우의 수 찾기에 적합

    *** 참고해야할 점
    - 방문했던 정점을 재 탐색 하지 않기위해, 따로 배열을 만들어서 방문한 곳인지 체크해야합니다.
    - 완전 탐색 입니다.
    - 트리에서 최단 거리 탐색 가능합니다.
    - 가중치 및 비가중치 그래프에서는 거의 사용되지 않습니다.(불가능하다, 가능은하나... 와 같은 여러 의견들이 있습니다)

> 1) DFS 수행 과정  
DFS란 스택을 이용하여 그래프를 탐색해 나가는 방법으로써 가능한 깊이 vertex를 들어간뒤 특정 vertex에서 더이상 갈곳이 없으면 그 vertex를 체크한뒤 다시 올라가서 갈 수 있는 모든 vertex를 탐색해나가는 기법  <br><br>
<span class="image center"><img src="{{ 'assets/images/dfs_1.png' | relative_url }}" alt="" /></span>  

> [깊이 우선 탐색의 수행 순서]  
⑴ 시작 정점 v를 결정하여 방문한다.  
⑵ 정점 v에 인접한 정점 중에서  
    ① 방문하지 않은 정점 w가 있으면, 정점 v를 스택에 push하고 정점 w를 방문한다. 그리고 w를 v로 하여 다시 ⑵를 반복한다.  
    ② 방문하지 않은 정점이 없으면, 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을 v로 하여 다시 ⑵를 반복한다.  
⑶ 스택이 공백이 될 때까지 ⑵를 반복한다.  

> 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면,  
가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 간선으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법.  
가장 마지막에 만났던 갈림길 간선의 정점으로 가장 먼저 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 스택 사용.  

> [알고리즘]  
<span class="image center"><img src="{{ 'assets/images/dfs_2.png' | relative_url }}" alt="" /></span>  

> ① 정점 A를 시작으로 깊이 우선 탐색을 시작  
visited[A]←true;  
<span class="image center"><img src="{{ 'assets/images/dfs_3.png' | relative_url }}" alt="" /></span>  

> ② 정점 A에 방문하지 않은 정점 B, C가 있으므로 A를 스택에 push 하고, 인접정점 B와 C 중에서 오름차순에 따라 B를 선택하여 탐색을 계속한다.  
push(stack, A);  
visited[B]←true;  
B 방문;  
<span class="image center"><img src="{{ 'assets/images/dfs_4.png' | relative_url }}" alt="" /></span>  

> ③ 정점 B에 방문하지 않은 정점 D, E가 있으므로 B를 스택에 push 하고, 인접정점 D와 E 중에서 오름차순에 따라 D를 선택하여 탐색을 계속한다.  
push(stack, B);  
visited[D]←true;  
D 방문;  
<span class="image center"><img src="{{ 'assets/images/dfs_5.png' | relative_url }}" alt="" /></span>  

> ④ 정점 D에 방문하지 않은 정점 G가 있으므로 D를 스택에 push 하고, 인접정점 G를 선택하여 탐색을 계속한다.  
push(stack, D);  
visited[G]←true;  
G 방문;  
<span class="image center"><img src="{{ 'assets/images/dfs_6.png' | relative_url }}" alt="" /></span>  

> ⑤ 정점 G에 방문하지 않은 정점 E, F가 있으므로 G를 스택에 push 하고, 인접정점 E와 F 중에서 오름차순에 따라 E를 선택하여 탐색을 계속한다.  
push(stack, G);  
visited[E]←true;  
E 방문;  
<span class="image center"><img src="{{ 'assets/images/dfs_7.png' | relative_url }}" alt="" /></span>  

> ⑥ 정점 E에 방문하지 않은 정점 C가 있으므로 E를 스택에 push 하고, 인접정점 C를 선택하여 탐색을 계속한다.  
push(stack, E);  
visited[C]←true;  
C 방문;  
<span class="image center"><img src="{{ 'assets/images/dfs_8.png' | relative_url }}" alt="" /></span>  

> ⑦ 정점 C에서 방문하지 않은 인접정점이 없으므로, 마지막 정점으로 돌아가기 위해 스택을 pop 하여 받은 정점 E에 대해서 방문하지 않은 인접정점이 있는지 확인한다.  
pop(stack);  
<span class="image center"><img src="{{ 'assets/images/dfs_9.png' | relative_url }}" alt="" /></span>  

> ⑧ 정점 E는 방문하지 않은 인접정점이 없으므로, 다시 스택을 pop 하여 받은 정점 G에 대해서 방문하지 않은 인접정점이 있는지 확인한다.  
pop(stack);
<span class="image center"><img src="{{ 'assets/images/dfs_10.png' | relative_url }}" alt="" /></span>  

> ⑨ 정점 G에 방문하지 않은 정점 F가 있으므로 G를 스택에 push 하고, 인접정점 F를 선택하여 탐색을 계속한다.  
push(stack, G);  
visited[F]←true;  
F 방문;  
<span class="image center"><img src="{{ 'assets/images/dfs_11.png' | relative_url }}" alt="" /></span>  

> ⑩ 정점 F에서 방문하지 않은 인접정점이 없으므로, 마지막 정점으로 돌아가기 위해 스택을 pop 하여 받은 정점 G에 대해서 방문하지 않은 인접정점이 있는지 확인한다.  
pop(stack);
<span class="image center"><img src="{{ 'assets/images/dfs_12.png' | relative_url }}" alt="" /></span>  

> ⑪ 정점 G에서 방문하지 않은 인접정점이 없으므로, 다시 마지막 정점으로 돌아가기 위해 스택을 pop 하여 받은 정점 D에 대해서 방문하지 않은 인접정점이 있는지 확인한다.  
pop(stack);  
<span class="image center"><img src="{{ 'assets/images/dfs_13.png' | relative_url }}" alt="" /></span>  


> ⑫ 모두 pop을 한다.  

> ⑬ 현재 정점 A에서 방문하지 않은 인접 정점이 없으므로 마지막 정점으로 돌아가기 위해 스택을 pop하는데, 스택이 공백이므로 깊이 우선 탐색을 종료한다.  
<span class="image center"><img src="{{ 'assets/images/dfs_14.png' | relative_url }}" alt="" /></span>  

# 2. 너비 우선 탐색(BFS, Breadth first search)
    - 현재 정점에 연결된 가까운 점들부터 탐색
    - 방법 : 큐를 이용해서 구현
    - 검색에 유용, DFS처럼 무한 루프에 빠질 위험성이 적음
    - DFS와 다르게 최단 경로 찾아낼 수 있음
    - 공간 복잡도가 지수적으로 증가하기 때문에 오버플로가 쉽게 됨

    *** 참고해야할 점
    - 방문했던 곳을 재 방문 하지 않기위해, 따로 배열을 만들어서 체크해야합니다.
    - 완전 탐색입니다.
    - 트리에서 최단거리 탐색이 가능합니다.
    - 비가중치 그래프에서 최단거리 탐색이 가능합니다. (다익스트라보다 효율이 좋다고 합니다.)
    - 가중치 그래프에서는 잘 사용되지 않습니다.

> 2) BFS 수행 과정  
BFS란 큐를 이용하며 그래프를 탐색해 나가는 방법으로, 탐색에 대한 특징은 너비 우선 탐색은 깊이가 1인 모든 정점을 방문하고 나서, 그 다음에는 깊이가 2인 모든 정점을, 깊이가 3인 모든 정점을 방문하는 식으로 계속 방문하다가 더이상 방문할 곳이 없으면 탐색을 마치는 기법  <br><br>
<span class="image center"><img src="{{ 'assets/images/bfs_1.png' | relative_url }}" alt="" /></span>  


# 3. 휴리스틱(heuristic) 탐색
    - BFS에서 발전된 방식으로 휴리스틱의 방법을 이용해서 최선의 길 선택
    - 보통 힙으로 구현된 우선순위 큐(priority queue) 사용
     (휴리스틱: 시간이나 정보가 불충분하여 합리적인 판단을 할 수 없거나 굳이 체계적이고 합리적인 판단을 할 필요가 없는 상황에서
       사람들이 신속하게 사용하는 어림짐작)


# 4. 백트래킹(backtracking)
    - 왔던 길을 되추적하는 것을 의미
    - 한 루트를 쭉 검사하고 되돌아와서 다른 루트를 검사하는 DFS와 비슷

    - 깊이 우선 탐색에서는 한 루트를 끝까지 들여다보고 정답이 없을 시 처음으로 되돌아와서 다른 루트를 검사하는데,
    이 과정에서 깊은 탐색에는 유용하지만 해당 루트에 답이 없을 경우 많은 시간을 허비하게됨
    그래서 시간을 단축시키기 위해 특정 루트에 들어가기 전에 이 루트가 유망한지(정답이 있을 확률이 높은지)
    유망하지 않은지(정답이 있을 확률이 낮은지)를 판단하여 이 루트를 검사 할지 말지 판단하는데, 이를 가지치기라고 함
    - 루트를 참색하기 전에 최선의 길을 미리 판단한다는 휴리스틱 탐색과 비슷한 방법
