# k진수에서 소수 개수 구하기

### 문제 설명

---

양의 정수 n이 주어집니다. 이 숫자를 k진수로 바꿨을 때, 변환된 수 안에 아래 조건에 맞는 소수(Prime number)가 몇 개인지 알아보려 합니다.

0P0처럼 소수 양쪽에 0이 있는 경우
P0처럼 소수 오른쪽에만 0이 있고 왼쪽에는 아무것도 없는 경우
0P처럼 소수 왼쪽에만 0이 있고 오른쪽에는 아무것도 없는 경우
P처럼 소수 양쪽에 아무것도 없는 경우
단, P는 각 자릿수에 0을 포함하지 않는 소수입니다.
예를 들어, 101은 P가 될 수 없습니다.
예를 들어, 437674을 3진수로 바꾸면 211020101011입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 211, 2, 11이 있으며, 총 3개입니다. (211, 2, 11을 k진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의합니다.) 211은 P0 형태에서 찾을 수 있으며, 2는 0P0에서, 11은 0P에서 찾을 수 있습니다.

정수 n과 k가 매개변수로 주어집니다. n을 k진수로 바꿨을 때, 변환된 수 안에서 찾을 수 있는 위 조건에 맞는 소수의 개수를 return 하도록 solution 함수를 완성해 주세요.

### 제한 사항

---

1 ≤ n ≤ 1,000,000
3 ≤ k ≤ 10

### 내 풀이

```javascript
const isPrime = (num) => {
  if (num === 1) return false;
  for (let i = 2; i <= Math.sqrt(num); i++) {
    if (num % i === 0) return false;
  }
  return true;
};

function solution(n, k) {
  let answer = 0;
  let regex = /[1-9]+/g;
  let arr = n.toString(k).match(regex);
  for (let i = 0; i < arr.length; i++) {
    if (isPrime(arr[i]) && arr[i] != 1) answer++;
  }
  return answer;
}
```

### 인상적이였던 풀이 방법

```javascript
function isPrime(num) {
  if (!num || num === 1) return false;
  for (let i = 2; i <= +Math.sqrt(num); i++) {
    if (num % i === 0) return false;
  }
  return true;
}

function solution(n, k) {
  // k진법으로 나눈 후 split
  const candidates = n.toString(k).split("0");
  // 소수 개수 세기
  return candidates.filter((v) => isPrime(+v)).length;
}

console.log(solution(930909, 10));
```

### 내 생각

일단 제일 중요한 소수 판별은 인터넷을 검색해서 제곱근을 사용한 방법의 함수를 가져왔다
그 다음에는 나는 정규식을 기준으로 소수만 잘라냈고 인상깊던 풀이에서는 split을 사용하여 분리하였다 그 후론 나는 if를 사용하여 1만 제거하여 return 인상적인 풀이는 filter를 사용하여
소수인것만 length로 뽑아냈다 확실히 나도 answer은 굳이 안쓰고 했을 수 있을것같다
