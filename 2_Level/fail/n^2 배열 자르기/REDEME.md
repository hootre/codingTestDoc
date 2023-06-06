# n^2 배열 자르기

### 문제 설명

---

정수 n, left, right가 주어집니다. 다음 과정을 거쳐서 1차원 배열을 만들고자 합니다.

n행 n열 크기의 비어있는 2차원 배열을 만듭니다.
i = 1, 2, 3, ..., n에 대해서, 다음 과정을 반복합니다.
1행 1열부터 i행 i열까지의 영역 내의 모든 빈 칸을 숫자 i로 채웁니다.
1행, 2행, ..., n행을 잘라내어 모두 이어붙인 새로운 1차원 배열을 만듭니다.
새로운 1차원 배열을 arr이라 할 때, arr[left], arr[left+1], ..., arr[right]만 남기고 나머지는 지웁니다.
정수 n, left, right가 매개변수로 주어집니다. 주어진 과정대로 만들어진 1차원 배열을 return 하도록 solution 함수를 완성해주세요.

### 제한 사항

---

1 ≤ n ≤ 107
0 ≤ left ≤ right < n2
right - left < 105

### 내 풀이(실패)

```javascript
function solution(n, left, right) {
  var answer = [];
  while (left <= right) {
    answer.push(Math.max(Math.floor(left / n), left++ % n) + 1);
  }
  return answer;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(n, left, right) {
  var answer = [];
  while (left <= right) {
    answer.push(Math.max(Math.floor(left / n), left++ % n) + 1);
  }
  return answer;
}
```

### 내 생각

이 문제에 중요한 부분은
n제곱의 배열을 나열하지 않고 규칙을 찾아서 left right의 사이의 있는 수를 나타내는 것이였다.
일단 나는 그 규칙을 찾기 못해서 풀지 못했고
그 규칙은 좌표(r, c)의 값은 max(r, c) +1 이기 때문에 이를 대입하여 좌표값만 구하면 되는 문제였다.
