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
