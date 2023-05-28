##유클리드 호제법
A를 B로 나눈 나머지를 구합니다. 만약 나머지가 0이라면, B가 A의 약수이므로 B가 최대공약수가 됩니다.
그러나 나머지가 0이 아니라면, A를 B로, B를 나머지로 대체합니다. 이제 B를 나머지로 나누고, 나머지가 0이 될 때까지 이 과정을 반복합니다.
이 과정을 통해서 최대공약수와 최소 공배수를 얻을 수 있다.

```javascript
// 최대 공약수
let getGCD = (num1, num2) => {
  let gcd = 1;
  for (let i = 2; i <= Math.min(num1, num2); i++) {
    if (num1 % i === 0 && num2 % i === 0) {
      gcd = i;
    }
  }
  return gcd;
};
// 최소 공배수
let getLCM = (num1, num2) => {
  let lcm = 1;

  while (true) {
    if (lcm % num1 == 0 && lcm % num2 == 0) {
      break;
    }
    lcm++;
  }
  return lcm;
};

//정리
function solution(num1, num2) {
  const gcd = (a, b) => (a % b === 0 ? b : gcd(b, a % b));
  const lcm = (a, b) => (a * b) / gcd(a, b);
  return [gcd(num1, num2), lcm(num1, num2)];
}
```

[유클리드 호제법](https://velog.io/@yerin4847/W1-%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C-%ED%98%B8%EC%A0%9C%EB%B2%95)
