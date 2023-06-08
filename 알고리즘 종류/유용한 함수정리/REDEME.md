# 유용한 함수 정리

## 교집합

arr1을 기준으로 중복된 값을 리턴한다.

```javasciprt
// 배열 선언
const arr1 = ['1','2','3','4','5'];
const arr2 = ['1','2'];

// 교집합(Intersection)
console.log(arr1.filter(x => arr2.includes(x)));
```

## 차집합

arr1을 기준으로 중복 된 요소외에 값을 리턴한다.

```javascript
// 배열 선언
const arr1 = ["1", "2", "3", "4", "5"];
const arr2 = ["1", "2"];

// 차집합(Difference)
console.log(arr1.filter((x) => !arr2.includes(x)));
```

## 대칭 차집합

대칭차집합은 두 배열을 비교하여 각 배열안에 공통된 원소의 나머지 것들을 구하는 방식이다.

```javascript
// 배열 선언
const arr1 = ["1", "2", "3", "4", "5"];
const arr2 = ["1", "2", "6", "7", "8"];

// 대칭차집합(Symmetric Difference)
let difference = arr1
  .filter((x) => !arr2.includes(x))
  .concat(arr2.filter((x) => !arr1.includes(x)));
```
