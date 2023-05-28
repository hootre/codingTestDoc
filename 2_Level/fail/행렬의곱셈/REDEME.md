# 행렬의 곱셈

### 문제 설명

---

2차원 행렬 arr1과 arr2를 입력받아, arr1에 arr2를 곱한 결과를 반환하는 함수, solution을 완성해주세요.

### 제한 사항

---

행렬 arr1, arr2의 행과 열의 길이는 2 이상 100 이하입니다.
행렬 arr1, arr2의 원소는 -10 이상 20 이하인 자연수입니다.
곱할 수 있는 배열만 주어집니다.

### 내 풀이(실패)

```javascript
function solution(arr1, arr2) {
  var answer = [];
  for (let i = 0; i < arr1.length; i++) {
    let result = [];
    for (let j = 0; j < arr2[0].length; j++) {
      let temp = 0;
      for (let k = 0; k < arr2.length; k++) {
        temp += arr1[i][k] * arr2[k][j];
      }
      result.push(temp);
    }
    answer.push(result);
  }
  return answer;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(arr1, arr2) {
  return arr1.map((row) =>
    arr2[0].map((x, y) => row.reduce((a, b, c) => a + b * arr2[c][y], 0))
  );
}
```

### 내 생각

일단 행렬의 곱셈을 하는 법을 몰라서 검색해서 이해하였고
행렬의 곱셈이란 A의 행 B의 열들을 곱해서 결과값을 도출하는 것이였다.
위에 내 풀이가 검색해서 나온 for문 3개로 풀이하는 방법이고
다른 사람의 풀이를 봤을 때 가장 짧고 인상깊던게 아래 풀이방법이다.
아래의 풀이는 arr1.map을 하여 reduce를 통해서 행을 순회하였다
