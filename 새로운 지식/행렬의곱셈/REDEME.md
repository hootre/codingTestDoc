##행렬의 곱셈
행렬의 곱셈이란
A의 행과
B의 열을 곱하는 것이다.

<img src='https://velog.velcdn.com/images%2Fsisofiy626%2Fpost%2Fc00a870b-e144-45b9-b5f6-5da4322ee286%2F%EC%BA%A1%EC%B2%98_2022_02_18_20_45_06_658.png'>

> result[0, 0] = ( arr1[0, 0] _ arr2[0, 0] ) + ( arr1[0, 1] _ arr2[1, 0] ) + ( arr1[0, 2] \* arr2[2, 0] )

되게 수학적으로 뭐가 많은 부분인데 알고리즘을 풀 때는
이정도만 알고 있으면 될 것같다.

```javascript
function solution(arr1, arr2) {
  const newArr = [];

  for (let i = 0; i < arr1.length; i++) {
    let result = [];
    for (let j = 0; j < arr2[0].length; j++) {
      let elem = 0;
      for (let k = 0; k < arr2.length; k++) {
        // arr1[0].length도 가능.
        elem += arr1[i][k] * arr2[k][j];
      }
      result.push(elem);
    }
    newArr.push(result);
  }
  return newArr;
}
```

[행렬의 곱셈](https://velog.io/@sisofiy626/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-Lv.2-%ED%96%89%EB%A0%AC%EC%9D%98-%EA%B3%B1%EC%85%88-JavaScript)
