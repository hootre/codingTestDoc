# 프로세스

### 문제 설명

---

운영체제의 역할 중 하나는 컴퓨터 시스템의 자원을 효율적으로 관리하는 것입니다. 이 문제에서는 운영체제가 다음 규칙에 따라 프로세스를 관리할 경우 특정 프로세스가 몇 번째로 실행되는지 알아내면 됩니다.

> 1. 실행 대기 큐(Queue)에서 대기중인 프로세스 하나를 꺼냅니다.
> 2. 큐에 대기중인 프로세스 중 우선순위가 더 높은 프로세스가 있다면 방금 꺼낸 프로세스를 다시 큐에 넣습니다.
> 3. 만약 그런 프로세스가 없다면 방금 꺼낸 프로세스를 실행합니다.
>    3.1 한 번 실행한 프로세스는 다시 큐에 넣지 않고 그대로 종료됩니다.
>    예를 들어 프로세스 4개 [A, B, C, D]가 순서대로 실행 대기 큐에 들어있고, 우선순위가 [2, 1, 3, 2]라면 [C, D, A, B] 순으로 실행하게 됩니다.

현재 실행 대기 큐(Queue)에 있는 프로세스의 중요도가 순서대로 담긴 배열 priorities와, 몇 번째로 실행되는지 알고싶은 프로세스의 위치를 알려주는 location이 매개변수로 주어질 때, 해당 프로세스가 몇 번째로 실행되는지 return 하도록 solution 함수를 작성해주세요.

### 제한 사항

---

priorities의 길이는 1 이상 100 이하입니다.
priorities의 원소는 1 이상 9 이하의 정수입니다.
priorities의 원소는 우선순위를 나타내며 숫자가 클 수록 우선순위가 높습니다.
location은 0 이상 (대기 큐에 있는 프로세스 수 - 1) 이하의 값을 가집니다.
priorities의 가장 앞에 있으면 0, 두 번째에 있으면 1 … 과 같이 표현합니다.

### 내 풀이

```javascript
function solution(priorities, location) {
  var answer = 0;
  let queue = [...priorities];
  let cnt_que = Array(priorities.length).fill(0);
  cnt_que[location] = 1;
  while (true) {
    let cur_pro = queue.shift();
    let cnt_pro = cnt_que.shift();
    let cur_queue = queue.filter((item) => item > cur_pro);
    if (cur_queue.length) {
      queue.push(cur_pro);
      cnt_que.push(cnt_pro);
    } else {
      answer++;
      if (cnt_pro) {
        break;
      }
    }
  }
  return answer;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(priorities, location) {
  var list = priorities.map((t, i) => ({
    my: i === location,
    val: t,
  }));
  var count = 0;
  while (true) {
    var cur = list.splice(0, 1)[0];
    if (list.some((t) => t.val > cur.val)) {
      list.push(cur);
    } else {
      count++;
      if (cur.my) return count;
    }
  }
}
```

### 내 생각

이번에도 어찌보면 형식은 비슷하다 하지만 함수를 쓰는 차이가 엄청났다

인상적인 풀이에서는 map을 통해서 배열안에 객체로 location을 지정하였는데
내가 풀이한것은 그냥 똑같은 배열을 하나 더 만들어서 해결했다 이는 비효율적이다.
그런 후에 array.some을 통해서 filter함수를 대신하였다 some이 더 용도에 알맞는 함수이이다.
some은 bol값을 리턴하고 filter은 arr를 리턴하기에 용도가 다르다고 볼 수 있다. 위에 알고리즘에 맞는 용도는 some이다.
some을 통해서 현재 값보다 우선되느 프로세스가 있는 경우 다시 list.push하고 없다면 count++을 통해서 프로세스 방출을 한다.
그리고 방출하는 프로세스값에서 my 값을 읽어 location인 경우 return count를 통해서 결과값을 도출한다.

참 이런것을 보면 아직도 활용하는 방법이 무궁무진하고 아직 나는 멀었다는게 느껴진다.
