# DP(동적계획법)

> 일반 재귀함수의 불필요한 연산을 줄이기 위해 사용

<details>
<summary>DP(동적계획법) 설명</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 문제 종류

- 피보나치 수열

- 배낭 문제

### 방법

- Top-down 방식 : 하향식 방법으로, 가장 큰 문제를 방문 후 작은 문제를 호출하며 답을 찾는 방식이다. (메모이제이션+ 재귀함수를 호출해서 푼다.)

- Bottom-up 방식 : 상향식 방법으로, 작은 문제들부터 답을 구해가며 전체 문제의 답을 찾는 방식 (반복문을 가지고 푼다)

</details>

<details>
<summary>DFS 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### bottom_up

피보나치 수열 기준

```javascript
const bottom_up_fibo = (n) => {
  const table = Array(n).fill(0); // 값을 저장하기 위한 테이블 선언
  table[0] = 1; // 초기값 선언
  table[1] = 2;

  for (let i = 2; i < n; i++) {
    table[i] = table[i - 1] + table[i - 2]; // 점화식을 통한 계산
  }
  return table[n - 1]; // 테이블의 마지막 요소에 저장된 값을 반환.
};
```

### top_down

```javascript
const memo = Array(n + 1).fill(0); // 계산 결과를 저장하기 위한 배열 초기화

const top_down_fibo = (n) => {
  // 초기값인 0과 1에 도달하는 경우
  if (n < 2) {
    memo[n] = n;
    return n;
  }
  // 이미 계산된 결과가 있는 경우 해당 결과를 반환
  if (memo[n] > 0) return memo[n];
  memo[n] = top_down_fibo(n - 1) + top_down_fibo(n - 2);
  return memo[n];
};
```

</details>
