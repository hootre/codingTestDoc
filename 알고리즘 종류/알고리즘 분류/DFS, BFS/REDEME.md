# DFS (Depth First Search)

> DFS는 깊이 우선 탐색 방법으로 트리 구조의 데이터에서 노드마다 가장 깊이까지 탐색한 뒤 다음 노드로 이동하는 방법입니다.

<details>
<summary>DFS 설명</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 문제 종류

> 경로의 특징을 저장한다. 문제
> -> DFS 사용

- 깊이 우선 탐색

- 현재 나의 위치에서 연결된 브랜치를 모두 방문 후 다음 브랜치로 넘어가는 방법

- 미로를 탐색할 때 한 방향으로 갈 수 있을 때까지 계속 가다가 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로 돌아와서 이곳으로부터 다른 방향으로 다시 탐색을 진행하는 방법

인접리스트 : O(V+E) / 인접행렬 : O(V^2)

</details>

<details>
<summary>DFS 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### DFS 코드(JS)

```javascript
const graph = {
  A: ["B", "C"],
  B: ["A", "D"],
  C: ["A", "G", "H", "I"],
  D: ["B", "E", "F"],
  E: ["D"],
  F: ["D"],
  G: ["C"],
  H: ["C"],
  I: ["C", "J"],
  J: ["I"],
};

// (graph, 시작 정점)
const dfs = (graph, startNode) => {
  let needVisitStack = []; // 탐색을 해야 할 노드들
  let visitedQueue = []; // 탐색을 마친 노드들

  needVisitStack.push(startNode);

  // 탐색을 해야 할 노드가 남아 있다면
  while (needVisitStack.length !== 0) {
    const node = needVisitStack.pop();
    if (!visitedQueue.includes(node)) {
      visitedQueue.push(node);
      needVisitStack = [...needVisitStack, ...graph[node]];
    }
  }

  return visitedQueue;
};

console.log(dfs(graph, "A"));

// ["A", "C", "I", "J", "H", "G", "B", "D", "F", "E"]
```

### DFS (재귀)

```javascript
function solution(numbers, target) {
  let answer = 0;
  const length = numbers.length;

  function dfs(count, sum) {
    if (count === length) {
      if (target === sum) {
        answer++;
      }
      return;
    }

    dfs(count + 1, sum + numbers[count]);
    dfs(count + 1, sum - numbers[count]);
  }

  dfs(0, 0);

  return answer;
}
```

</details>

# BFS (Breadth First Search)

> BFS는 너비 우선 탐색 방법으로 트리 구조 데이터에서 노드의 인접 데이터를 모두 탐색한 뒤 다음 데이터로 이동하는 방법입니다.

<details>
<summary>BFS 설명</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 문제 종류

- 두 개의 큐를 사용한다.
- root와 가까운 node들부터 찾기 때문에 최단거리를 탐색할 때 유용하다.
- queue에 각 노드의 정보를 기록해야 하기 때문에 메모리를 많이 잡아 먹는다.
- 찾고자 하는 target node가 root node와 가까이 있다고 예상될 경우 BFS를 사용한다.
- 지도 어플에서 특정 위치까지의 최단거리 안내, 혹은 소셜미디어에서 친구 추천 등에 이용된다.

</details>

<details>
<summary>BFS 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### BFS 코드(JS)

```javascript
const graph = {
  A: ["B", "C"],
  B: ["A", "D"],
  C: ["A", "G", "H", "I"],
  D: ["B", "E", "F"],
  E: ["D"],
  F: ["D"],
  G: ["C"],
  H: ["C"],
  I: ["C", "J"],
  J: ["I"],
};

const bfs = (graph, startNode) => {
  let visited = []; // 탐색을 마친 노드들
  let needVisit = []; // 탐색해야할 노드들

  needVisit.push(startNode); // 노드 탐색 시작

  while (needVisit.length !== 0) {
    // 탐색해야할 노드가 남아있다면
    const node = needVisit.shift(); // queue이기 때문에 선입선출, shift()를 사용한다.
    if (!visited.includes(node)) {
      // 해당 노드가 탐색된 적 없다면
      visited.push(node);
      needVisit = [...needVisit, ...graph[node]];
    }
  }
  return visited;
};

console.log(bfs(graph, "A"));
// ["A", "B", "C", "D", "G", "H", "I", "E", "F", "J"]
```

</details>
