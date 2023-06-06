# 연속 부분 수열 합의 개수

### 문제 설명

---

철호는 수열을 가지고 놀기 좋아합니다. 어느 날 철호는 어떤 자연수로 이루어진 원형 수열의 연속하는 부분 수열의 합으로 만들 수 있는 수가 모두 몇 가지인지 알아보고 싶어졌습니다. 원형 수열이란 일반적인 수열에서 처음과 끝이 연결된 형태의 수열을 말합니다. 예를 들어 수열 [7, 9, 1, 1, 4] 로 원형 수열을 만들면 다음과 같습니다.
<img src="https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/f207cd37-34dc-4cbd-96bb-83435bd6efd4/%EA%B7%B8%EB%A6%BC.png">
원형 수열은 처음과 끝이 연결되어 끊기는 부분이 없기 때문에 연속하는 부분 수열도 일반적인 수열보다 많아집니다.
원형 수열의 모든 원소 elements가 순서대로 주어질 때, 원형 수열의 연속 부분 수열 합으로 만들 수 있는 수의 개수를 return 하도록 solution 함수를 완성해주세요.

### 제한 사항

---

3 ≤ elements의 길이 ≤ 1,000
1 ≤ elements의 원소 ≤ 1,000

### 내 풀이

```javascript
function solution(elements) {
  var answer = 0;
  let temp = [];
  for (let j = 1; j < elements.length + 1; j++) {
    for (let i = 0; i < elements.length; i++) {
      let sum = 0;
      for (let k = i; k < i + j; k++) {
        if (k >= elements.length) {
          sum += elements[k - elements.length];
        } else {
          sum += elements[k];
        }
      }
      temp.push(sum);
    }
  }
  answer = [...new Set(temp)];
  return answer.length;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(elements) {
  const circular = elements.concat(elements);
  const set = new Set();
  for (let i = 0; i < elements.length; i++) {
    let sum = 0;
    for (let j = 0; j < elements.length; j++) {
      sum += circular[i + j];
      set.add(sum);
    }
  }
  return set.size;
}
```

### 내 생각

나의 풀이 방법은 3중 for문을 사용하기도 하였고 보기에 가독성도 좋지 않다
하지만 인상적인 풀이에서는 원본 배열을 2개 합쳐서 circular를 만들었고
2중 for문을 사용하여 연속 수열의 합을 구하였다 아래의 방법이 더 깔끔하고 가독성이 좋아서 다음에 푼다면 이렇게 해야겠다
