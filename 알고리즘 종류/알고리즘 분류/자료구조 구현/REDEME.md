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
