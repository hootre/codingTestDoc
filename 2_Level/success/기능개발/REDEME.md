# 기능개발

### 문제 설명

---

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

### 제한 사항

---

작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
작업 진도는 100 미만의 자연수입니다.
작업 속도는 100 이하의 자연수입니다.
배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

### 내 풀이

```javascript
function solution(progresses, speeds) {
  var answer = [];
  let remain = 100 - progresses[0];
  let max_day = Math.ceil(remain / speeds[0]);
  let cnt = 1;
  for (let i = 1; i < progresses.length; i++) {
    remain = 100 - progresses[i];
    let cnt_max_day = Math.ceil(remain / speeds[i]);
    if (max_day >= cnt_max_day) {
      cnt++;
    } else {
      answer.push(cnt);
      max_day = cnt_max_day;
      cnt = 1;
    }
  }
  answer.push(cnt);
  return answer;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(progresses, speeds) {
  let answer = [0];
  let days = progresses.map((progress, index) =>
    Math.ceil((100 - progress) / speeds[index])
  );
  let maxDay = days[0];

  for (let i = 0, j = 0; i < days.length; i++) {
    if (days[i] <= maxDay) {
      answer[j] += 1;
    } else {
      maxDay = days[i];
      answer[++j] = 1;
    }
  }

  return answer;
}
```

### 내 생각

내가 푼 풀이와 인상적으로 봤던 풀이의 실행 방식은 똑같다
하지만 인상적이였던 풀이방법은 map으로 나머지 일수를 정리하여 배열로 만들었고
나는 그러하지 않은게 차이가 있다.
또한 인상적인 풀이가 더욱 읽기 편한 것 같다
