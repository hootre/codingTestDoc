# 귤 고르기

### 문제 설명

---

경화는 과수원에서 귤을 수확했습니다. 경화는 수확한 귤 중 'k'개를 골라 상자 하나에 담아 판매하려고 합니다. 그런데 수확한 귤의 크기가 일정하지 않아 보기에 좋지 않다고 생각한 경화는 귤을 크기별로 분류했을 때 서로 다른 종류의 수를 최소화하고 싶습니다.

예를 들어, 경화가 수확한 귤 8개의 크기가 [1, 3, 2, 5, 4, 5, 2, 3] 이라고 합시다. 경화가 귤 6개를 판매하고 싶다면, 크기가 1, 4인 귤을 제외한 여섯 개의 귤을 상자에 담으면, 귤의 크기의 종류가 2, 3, 5로 총 3가지가 되며 이때가 서로 다른 종류가 최소일 때입니다.

경화가 한 상자에 담으려는 귤의 개수 k와 귤의 크기를 담은 배열 tangerine이 매개변수로 주어집니다. 경화가 귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

### 제한 사항

---

1 ≤ k ≤ tangerine의 길이 ≤ 100,000
1 ≤ tangerine의 원소 ≤ 10,000,000

### 내 풀이

```javascript
function solution(k, tangerine) {
  var answer = 0;
  let cnt = 1;
  let stack = [];
  tangerine.sort((a, b) => b - a);
  for (let i = 0; i < tangerine.length; i++) {
    if (tangerine[i] === tangerine[i + 1]) {
      cnt++;
    } else {
      stack.push(cnt);
      cnt = 1;
    }
  }
  stack.sort((a, b) => b - a);
  let temp = 0;
  for (let j = 0; j < stack.length; j++) {
    if (k > temp) {
      temp += stack[j];
    } else {
      break;
    }
    answer++;
  }
  return answer ? answer : 1;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(k, tangerine) {
  let answer = 0;
  const tDict = {};
  tangerine.forEach((t) => (tDict[t] = (tDict[t] || 0) + 1));
  const tArr = Object.values(tDict).sort((a, b) => b - a);
  for (const t of tArr) {
    answer++;
    if (k > t) k -= t;
    else break;
  }
  return answer;
}
```

### 내 생각

꾸역 꾸역 풀긴 했다.
처음에는 배열로 하려고 했는데 숫자가 10,000,000이 넘어가서 이 방법은 아닌 것 같고
사실 객체로 푸는 것 같았는데 잘 몰라서 일단
수치만 필요하단 사실을 알고 sort를 통해서 개수를 구하고 거기서 최대치를 구해서
k 값을 넘어가는 순간 break하여 answer를 도출하였다.

인상적이였던 풀이 방법은 객체를 사용하여 더욱 깔끔하게 푼 것 같아서 저런식으로 기능을 알면
깔끔하게 풀 것 같다.

forEach()를 통해 객체 tDict[t] = (tDict[t] || 0) + 1 이 부분이 인상적이였다
처음 방문했다면 0 그 이후에 방문하면 1씩 더하는 로직인데 매우 심플해보인다.
또한 Object.values(tDict).sort((a,b)=> b-a) 부분도 깔끔하게 객체를 sort 하는것 같다.
배워야 할게 아직 많다.
