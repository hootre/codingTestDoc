# 조합 (Combinations)

> 조합은 n개 중에 r개를 뽑는 경우의 수를 구할 때 **순서를 고려하지 않는 개념**이다

<details>
<summary>조합 설명</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 예제

```javascript
Input: [1, 2, 3, 4];
Output: [
  [1, 2, 3],
  [1, 2, 4],
  [1, 3, 4],
  [2, 3, 4],
];
```

4C3은 4개중에 3개씩 선택할 때 나올 수 있는 모든 조합을 구한다는 말이다.
위 처럼 조합은 순서는 상관이없다. 즉 **[1, 2, 3] = [3, 2, 1]** 이렇게 순서가 바뀌어도
같은 구성이기 때문에 하나의 조합으로 취급한다.

### 수도 코드

```
시작
  1을 선택하고 -> 나머지 [2, 3, 4] 중에서 2개씩 조합을 구한다.
     -> [1, 2, 3],[1, 2, 4],[1, 3, 4]
  2를 선택하고 -> 나머지 [3, 4] 중에서 2개씩 조합을 구한다.
     -> [2, 3, 4]
  3을 선택하고 -> 나머지 [4] 중에서 2개씩 조합을 구한다.
     -> []
  4를 선택하고 -> 나머지 [] 중에서 2개씩 조합을 구한다.
     -> []
종료
```

나머지에 대해서 일을 위임할 때에는 재귀(Recursion)함수를 사용하는 것이 좋다! 왜냐하면 계속해서 반복 될 일(조합을 구하는 코드)에 대해서 한번만 명시 해 놓고,
들어가는 인자(나를 뺀 나머지)를 바꾸어 주기만 하면 되기 때문이다.

> 만약 nCr 에서 r이 3이하일 경우에는 for문을 사용하여 하는게 더 빠르다.

</details>

<details>
<summary>조합 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

## 조합 코드(JS)

### 조합

```javascript
const getCombinations = (arr, selectNumber) => {
  const results = [];

  // n개중에서 1개 선택할 때(nC1), 바로 모든 배열의 원소 return
  if (selectNumber === 1) return arr.map((el) => [el]);

  arr.forEach((fixed, index, origin) => {
    // 해당하는 fixed를 제외한 나머지 뒤
    const rest = origin.slice(index + 1);
    // 나머지에 대해서 조합을 구한다.
    const combinations = getCombinations(rest, selectNumber - 1);
    //  돌아온 조합에 떼 놓은(fixed) 값 붙이기
    const attached = combinations.map((el) => [fixed, ...el]);
    // 배열 spread syntax 로 모두다 push
    results.push(...attached);
  });

  return results; // 결과 담긴 results return
};
```

### 중복 조합

```javascript
const getCombinations = (arr, selectNumber) => {
  const results = [];

  // n개중에서 1개 선택할 때(nC1), 바로 모든 배열의 원소 return
  if (selectNumber === 1) return arr.map((el) => [el]);

  arr.forEach((fixed, index, origin) => {
    // 해당하는 fixed를 제외한 나머지 뒤
    const rest = origin.slice(index);
    // 나머지에 대해서 조합을 구한다.
    const combinations = getCombinations(rest, selectNumber - 1);
    //  돌아온 조합에 떼 놓은(fixed) 값 붙이기
    const attached = combinations.map((el) => [fixed, ...el]);
    // 배열 spread syntax 로 모두다 push
    results.push(...attached);
  });

  return results; // 결과 담긴 results return
};
```

</details>

# 순열 (Combinations)

> 순열은 n개 중에 r개를 뽑는 경우의 수를 구할 때 **순서를 고려하는 개념**이다

<details>
<summary>순열 설명</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 예제

서로 다른 n개의 물건 중에서 r개를 택하여 한 줄로 배열하는 것을 n개의 물건에서
r개 택하는 순열이라 하고, 이 순열의 수를 기호로 nPr와 같이 나타낸다.
조합은 순서에 상관없이 선택한 것이라면, 순열은 순서가 중요하다.
실제로 순열을 구하는 공식도 조합으로부터 도출 가능하다.

```javascript
Input: [1, 2, 3, 4];
Output: [
  [1, 2, 3],
  [1, 2, 4],
  [1, 3, 2],
  [1, 3, 4],
  [1, 4, 2],
  [1, 4, 3],
  [2, 1, 3],
  [2, 1, 4],
  [2, 3, 1],
  [2, 3, 4],
  [2, 4, 1],
  [2, 4, 3],
  [3, 1, 2],
  [3, 1, 4],
  [3, 2, 1],
  [3, 2, 4],
  [3, 4, 1],
  [3, 4, 2],
  [4, 1, 2],
  [4, 1, 3],
  [4, 2, 1],
  [4, 2, 3],
  [4, 3, 1],
  [4, 3, 2],
];
```

### 수도 코드

먼저, 재귀의 종료 조건은 조합을 구하는 함수와 동일하다.
왜냐하면, 한 개씩 선택한다고 하면 순서가 의미가 없어지기 때문이다.
[1,2,3,4] 에서 3개를 선택해서 순열을 만드는 코드의 내부를 의사코드로 적어보면 다음과 같다.
1, 2, 3, 4를 각각 순서대로 픽스하고 나머지 요소만으로 이루어진 배열에서
(seletNumber-1)만큼을 선택하여 또 순열을 구한다.(재귀)

```
1(fixed) => permutation([2, 3, 4]) => 2(fixed) => permutation([3, 4]) => ...
2(fixed) => permutation([1, 3, 4]) => 1(fixed) => permutation([3, 4]) => ...
3(fixed) => permutation([1, 2, 4]) ... 위와 동일...
4(fixed) => permutation([1, 2, 3])
```

> 만약 nPr 에서 r이 3이하일 경우에는 for문을 사용하여 하는게 더 빠르다.

</details>

<details>
<summary>순열 코드</summary>

<!-- summary 아래 한칸 공백 두어야함 -->

### 순열 코드(JS)

```javascript
const getPermutations = function (arr, selectNumber) {
  if (selectNumber === 1) return arr.map((el) => [el]);
  const results = [];
  arr.forEach((fixed, index, origin) => {
    const rest = [...origin.slice(0, index), ...origin.slice(index + 1)];
    const permutations = getPermutations(rest, selectNumber - 1);
    const attached = permutations.map((el) => [fixed, ...el]);

    results.push(...attached);
  });

  return results;
};
```

### 중복순열 코드(JS)

```javascript
const getPermutations = function (arr, selectNumber) {
  if (selectNumber === 1) return arr.map((el) => [el]);
  const results = [];
  arr.forEach((fixed, index) => {
    const permutations = getPermutations(arr, selectNumber - 1);
    const attached = permutations.map((el) => [fixed, ...el]);

    results.push(...attached);
  });

  return results;
};
```

</details>
