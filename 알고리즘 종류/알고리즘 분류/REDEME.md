# 조합 (Combinations)

> 조합은 n개 중에 r개를 뽑는 경우의 수를 구할 때 **순서를 고려하지 않는 개념**이다

<details>
<summary>조합 설명</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 예제

```javascript
Input: [1, 2, 3, 4];
Output: [
  [1, 2, 3],
  [1, 2, 4],
  [1, 3, 4],
  [2, 3, 4],
];
```

4C3은 4개중에 3개씩 선택할 때 나올 수 있는 모든 조합을 구한다는 말이다.
위 처럼 조합은 순서는 상관이없다. 즉 **[1, 2, 3] = [3, 2, 1]** 이렇게 순서가 바뀌어도
같은 구성이기 때문에 하나의 조합으로 취급한다.

### 수도 코드

```
시작
  1을 선택하고 -> 나머지 [2, 3, 4] 중에서 2개씩 조합을 구한다.
     -> [1, 2, 3],[1, 2, 4],[1, 3, 4]
  2를 선택하고 -> 나머지 [3, 4] 중에서 2개씩 조합을 구한다.
     -> [2, 3, 4]
  3을 선택하고 -> 나머지 [4] 중에서 2개씩 조합을 구한다.
     -> []
  4를 선택하고 -> 나머지 [] 중에서 2개씩 조합을 구한다.
     -> []
종료
```

나머지에 대해서 일을 위임할 때에는 재귀(Recursion)함수를 사용하는 것이 좋다! 왜냐하면 계속해서 반복 될 일(조합을 구하는 코드)에 대해서 한번만 명시 해 놓고,
들어가는 인자(나를 뺀 나머지)를 바꾸어 주기만 하면 되기 때문이다.

> 만약 nCr 에서 r이 3이하일 경우에는 for문을 사용하여 하는게 더 빠르다.

</details>

<details>
<summary>조합 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

## 조합 코드(JS)

### 조합

```javascript
const getCombinations = (arr, selectNumber) => {
  const results = [];

  // n개중에서 1개 선택할 때(nC1), 바로 모든 배열의 원소 return
  if (selectNumber === 1) return arr.map((el) => [el]);

  arr.forEach((fixed, index, origin) => {
    // 해당하는 fixed를 제외한 나머지 뒤
    const rest = origin.slice(index + 1);
    // 나머지에 대해서 조합을 구한다.
    const combinations = getCombinations(rest, selectNumber - 1);
    //  돌아온 조합에 떼 놓은(fixed) 값 붙이기
    const attached = combinations.map((el) => [fixed, ...el]);
    // 배열 spread syntax 로 모두다 push
    results.push(...attached);
  });

  return results; // 결과 담긴 results return
};
```

### 중복 조합

```javascript
const getCombinations = (arr, selectNumber) => {
  const results = [];

  // n개중에서 1개 선택할 때(nC1), 바로 모든 배열의 원소 return
  if (selectNumber === 1) return arr.map((el) => [el]);

  arr.forEach((fixed, index, origin) => {
    // 해당하는 fixed를 제외한 나머지 뒤
    const rest = origin.slice(index);
    // 나머지에 대해서 조합을 구한다.
    const combinations = getCombinations(rest, selectNumber - 1);
    //  돌아온 조합에 떼 놓은(fixed) 값 붙이기
    const attached = combinations.map((el) => [fixed, ...el]);
    // 배열 spread syntax 로 모두다 push
    results.push(...attached);
  });

  return results; // 결과 담긴 results return
};
```

</details>

# 순열 (Combinations)

> 순열은 n개 중에 r개를 뽑는 경우의 수를 구할 때 **순서를 고려하는 개념**이다

<details>
<summary>순열 설명</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 예제

서로 다른 n개의 물건 중에서 r개를 택하여 한 줄로 배열하는 것을 n개의 물건에서
r개 택하는 순열이라 하고, 이 순열의 수를 기호로 nPr와 같이 나타낸다.
조합은 순서에 상관없이 선택한 것이라면, 순열은 순서가 중요하다.
실제로 순열을 구하는 공식도 조합으로부터 도출 가능하다.

```javascript
Input: [1, 2, 3, 4];
Output: [
  [1, 2, 3],
  [1, 2, 4],
  [1, 3, 2],
  [1, 3, 4],
  [1, 4, 2],
  [1, 4, 3],
  [2, 1, 3],
  [2, 1, 4],
  [2, 3, 1],
  [2, 3, 4],
  [2, 4, 1],
  [2, 4, 3],
  [3, 1, 2],
  [3, 1, 4],
  [3, 2, 1],
  [3, 2, 4],
  [3, 4, 1],
  [3, 4, 2],
  [4, 1, 2],
  [4, 1, 3],
  [4, 2, 1],
  [4, 2, 3],
  [4, 3, 1],
  [4, 3, 2],
];
```

### 수도 코드

먼저, 재귀의 종료 조건은 조합을 구하는 함수와 동일하다.
왜냐하면, 한 개씩 선택한다고 하면 순서가 의미가 없어지기 때문이다.
[1,2,3,4] 에서 3개를 선택해서 순열을 만드는 코드의 내부를 의사코드로 적어보면 다음과 같다.
1, 2, 3, 4를 각각 순서대로 픽스하고 나머지 요소만으로 이루어진 배열에서
(seletNumber-1)만큼을 선택하여 또 순열을 구한다.(재귀)

```
1(fixed) => permutation([2, 3, 4]) => 2(fixed) => permutation([3, 4]) => ...
2(fixed) => permutation([1, 3, 4]) => 1(fixed) => permutation([3, 4]) => ...
3(fixed) => permutation([1, 2, 4]) ... 위와 동일...
4(fixed) => permutation([1, 2, 3])
```

> 만약 nPr 에서 r이 3이하일 경우에는 for문을 사용하여 하는게 더 빠르다.

</details>

<details>
<summary>순열 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 순열 코드(JS)

```javascript
const getPermutations = function (arr, selectNumber) {
  if (selectNumber === 1) return arr.map((el) => [el]);
  const results = [];
  arr.forEach((fixed, index, origin) => {
    const rest = [...origin.slice(0, index), ...origin.slice(index + 1)];
    const permutations = getPermutations(rest, selectNumber - 1);
    const attached = permutations.map((el) => [fixed, ...el]);

    results.push(...attached);
  });

  return results;
};
```

### 중복순열 코드(JS)

```javascript
const getPermutations = function (arr, selectNumber) {
  if (selectNumber === 1) return arr.map((el) => [el]);
  const results = [];
  arr.forEach((fixed, index) => {
    const permutations = getPermutations(arr, selectNumber - 1);
    const attached = permutations.map((el) => [fixed, ...el]);

    results.push(...attached);
  });

  return results;
};
```

</details>

# 누적합 (Prefix sum)

> 어떠한 배열을 기반으로 앞에서부터 요소들의 누적된 합을 저장해 새로이 배열을 만들어서 이를 활용하는 것을 말한다.

<details>
<summary>누적합 설명</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 예제

누적합을 만들땐 0번째에는 아무값도 담지 않고, 1번째부터 담아야한다.
보통 배열을 만들땐 0번째부터 시작하지만 prefix sum을 만들땐, 1번째부터 배열을 담아놔야 만들기가 쉽다.

```javascript
let arr = [1, 10, 11, 100];
//0번째 x, 첫번째 1, 두번째10, 세번째11, 네번째100
```

prefix sum의 첫번째 요소는 arr의 첫번째 1 합한것, -> 1 = 1
두번째는 arr의 두번째 10까지 합한것, -> 1 + 10 = 11
세번째는 11까지 합한것, -> 1 + 10 + 11 = 21
네번째는 100까지 합한것 -> 1 + 10 + 11 + 100 = 121

앞에서부터 더한 것을 기반으로 배열을 만든다.
이렇게 더한 것을 어떠한 연산에 활용할 수 가 있다는 것이다.

> 배열의 요소가 정적인 배열에만 누적합을 사용할 수 있다.

</details>

<details>
<summary>누적합 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 누적합 코드(JS)

```javascript
for (let i = 1; i <= n; i++) {
  psum[i] = psum[i - 1] + arr[i];
}
for (let i = 0; i < m; i++) {
  count = psum[c] - psum[b - 1];
}
return 0;
```

</details>

# 큐 (Queue)

> 기본 배열로 할 수 있지만 더 빠른 시간복잡도를 원하는 경우

<details>
<summary>큐 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 큐 코드(JS)

```javascript
class Queue {
  constructor() {
    this.storage = {};
    this.front = 0;
    this.rear = 0;
  }

  size() {
    if (this.storage[this.rear] === undefined) {
      return 0;
    } else {
      return this.rear - this.rear + 1;
    }
  }

  add(value) {
    if (this.size() === 0) {
      this.storage["0"] = value;
    } else {
      this.rear += 1;
      this.storage[this.rear] = value;
    }
  }

  popleft() {
    let temp;
    if (this.front === this.rear) {
      temp = this.storage[this.front];
      delete this.storage[this.front];
      this.front = 0;
      this.rear = 0;
    } else {
      temp = this.storage[this.front];
      delete this.storage[this.front];
      this.front += 1;
    }
    return temp;
  }
}
```

</details>

---

# 이진탐색트리 (BinarySearchTree )

> 기본 배열로 할 수 있지만 더 빠른 시간복잡도를 원하는 경우

<details>
<summary>이진탐색트리 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 이진탐색트리 코드(JS)

```javascript
// 기본 노드
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}
// 이진 탐색 트리
class BinarySearchTree {
  constructor() {
    this.root = null;
  }
  insert(value) {
    let newNode = new Node(value);
    if (this.root === null) {
      this.root = newNode;
      return this;
    } else {
      let current = this.root;
      function traverse(node) {
        if (node.left) traverse(node.left);
        if (node.right) traverse(node.right);
        if (node.left === null) {
          let leftNode = new Node(-value);
          let rightNode = new Node(value);
          node.left = leftNode;
          node.right = rightNode;
        }
      }
      traverse(current);
      return this;
    }
  }
}
```

</details>

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
