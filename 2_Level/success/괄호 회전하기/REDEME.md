# 괄호 회전하기

### 문제 설명

---

다음 규칙을 지키는 문자열을 올바른 괄호 문자열이라고 정의합니다.

(), [], {} 는 모두 올바른 괄호 문자열입니다.
만약 A가 올바른 괄호 문자열이라면, (A), [A], {A} 도 올바른 괄호 문자열입니다. 예를 들어, [] 가 올바른 괄호 문자열이므로, ([]) 도 올바른 괄호 문자열입니다.
만약 A, B가 올바른 괄호 문자열이라면, AB 도 올바른 괄호 문자열입니다. 예를 들어, {} 와 ([]) 가 올바른 괄호 문자열이므로, {}([]) 도 올바른 괄호 문자열입니다.
대괄호, 중괄호, 그리고 소괄호로 이루어진 문자열 s가 매개변수로 주어집니다. 이 s를 왼쪽으로 x (0 ≤ x < (s의 길이)) 칸만큼 회전시켰을 때 s가 올바른 괄호 문자열이 되게 하는 x의 개수를 return 하도록 solution 함수를 완성해주세요.

### 제한 사항

---

s의 길이는 1 이상 1,000 이하입니다.

### 내 풀이

```javascript
function solution(s) {
  let answer = 0;
  let cnt = 0;
  for (let j = 0; j < s.length; j++) {
    let stack = [s[0]];
    for (let i = 1; i < s.length; i++) {
      if (s[i] === "]" && stack[stack.length - 1] === "[") {
        stack.pop();
      } else if (s[i] === "}" && stack[stack.length - 1] === "{") {
        stack.pop();
      } else if (s[i] === ")" && stack[stack.length - 1] === "(") {
        stack.pop();
      } else {
        stack.push(s[i]);
      }
    }
    if (!stack.length) {
      answer++;
    }
    s = s.substr(1, s.length) + s.substr(0, 1);
  }
  return answer;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(s) {
  let answer = 0;
  let cnt = 0;
  for (let j = 0; j < s.length; j++) {
    let stack = [s[0]];
    for (let i = 1; i < s.length; i++) {
      if (s[i] === "]" && stack[stack.length - 1] === "[") {
        stack.pop();
      } else if (s[i] === "}" && stack[stack.length - 1] === "{") {
        stack.pop();
      } else if (s[i] === ")" && stack[stack.length - 1] === "(") {
        stack.pop();
      } else {
        stack.push(s[i]);
      }
    }
    if (!stack.length) {
      answer++;
    }
    s = s.substr(1, s.length) + s.substr(0, 1);
  }
  return answer;
}
```

### 내 생각

stack으로 짝이 맞는 문자열이 stack을 비우게 하였다
너무 익숙한 stack문제였고 조금 응용으로 바뀐 문제라서 그렇게 어렵지 않았다.
