# 짝지어 제거하기

### 문제 설명

---

짝지어 제거하기는, 알파벳 소문자로 이루어진 문자열을 가지고 시작합니다. 먼저 문자열에서 같은 알파벳이 2개 붙어 있는 짝을 찾습니다. 그다음, 그 둘을 제거한 뒤, 앞뒤로 문자열을 이어 붙입니다. 이 과정을 반복해서 문자열을 모두 제거한다면 짝지어 제거하기가 종료됩니다. 문자열 S가 주어졌을 때, 짝지어 제거하기를 성공적으로 수행할 수 있는지 반환하는 함수를 완성해 주세요. 성공적으로 수행할 수 있으면 1을, 아닐 경우 0을 리턴해주면 됩니다.

예를 들어, 문자열 S = baabaa 라면

b aa baa → bb aa → aa →

의 순서로 문자열을 모두 제거할 수 있으므로 1을 반환합니다.

### 제한 사항

---

문자열의 길이 : 1,000,000이하의 자연수
문자열은 모두 소문자로 이루어져 있습니다.

### 내 풀이(실패)

```javascript
function solution(s) {
  var answer = -1;
  let len = s.length;
  let rending = [s];
  while (len) {
    for (let i = 0; i < len; i++) {
      let after = i < len ? i + 1 : len;
      if (s[after] === s[i]) {
        rending.push(s.substring(0, i) + s.substring(after + 1, len));
        answer = 1;
      }
    }
    if (answer != 1) {
      answer = 0;
      break;
    }
    s = rending.pop();
    len = s.length;
    answer = 1;
  }

  return answer;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(n) {
  let answer = 0;
  for (let i = 1; i <= n; i++) {
    if (n % i === 0 && i % 2 === 1) answer++;
  }
  return answer;
}
```

### 내 생각

스택문제를 분명 많이 풀었는데도 생각하지 못하고 있었다
그냥 인형뽑기처럼 연산 값이 빌때까지 하는것은 전부 스택이라고 생각하면서 풀어야겠다.
가까이 있는 아이템과 붙어서 사라지는 문제들은 전부 스택문제이다!!!!
