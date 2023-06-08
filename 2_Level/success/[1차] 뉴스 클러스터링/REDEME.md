# [1차] 뉴스 클러스터링

### 문제 설명

---

여러 언론사에서 쏟아지는 뉴스, 특히 속보성 뉴스를 보면 비슷비슷한 제목의 기사가 많아 정작 필요한 기사를 찾기가 어렵다. Daum 뉴스의 개발 업무를 맡게 된 신입사원 튜브는 사용자들이 편리하게 다양한 뉴스를 찾아볼 수 있도록 문제점을 개선하는 업무를 맡게 되었다.

개발의 방향을 잡기 위해 튜브는 우선 최근 화제가 되고 있는 "카카오 신입 개발자 공채" 관련 기사를 검색해보았다.

카카오 첫 공채..'블라인드' 방식 채용
카카오, 합병 후 첫 공채.. 블라인드 전형으로 개발자 채용
카카오, 블라인드 전형으로 신입 개발자 공채
카카오 공채, 신입 개발자 코딩 능력만 본다
카카오, 신입 공채.. "코딩 실력만 본다"
카카오 "코딩 능력만으로 2018 신입 개발자 뽑는다"
기사의 제목을 기준으로 "블라인드 전형"에 주목하는 기사와 "코딩 테스트"에 주목하는 기사로 나뉘는 걸 발견했다. 튜브는 이들을 각각 묶어서 보여주면 카카오 공채 관련 기사를 찾아보는 사용자에게 유용할 듯싶었다.

유사한 기사를 묶는 기준을 정하기 위해서 논문과 자료를 조사하던 튜브는 "자카드 유사도"라는 방법을 찾아냈다.

자카드 유사도는 집합 간의 유사도를 검사하는 여러 방법 중의 하나로 알려져 있다. 두 집합 A, B 사이의 자카드 유사도 J(A, B)는 두 집합의 교집합 크기를 두 집합의 합집합 크기로 나눈 값으로 정의된다.

예를 들어 집합 A = {1, 2, 3}, 집합 B = {2, 3, 4}라고 할 때, 교집합 A ∩ B = {2, 3}, 합집합 A ∪ B = {1, 2, 3, 4}이 되므로, 집합 A, B 사이의 자카드 유사도 J(A, B) = 2/4 = 0.5가 된다. 집합 A와 집합 B가 모두 공집합일 경우에는 나눗셈이 정의되지 않으니 따로 J(A, B) = 1로 정의한다.

자카드 유사도는 원소의 중복을 허용하는 다중집합에 대해서 확장할 수 있다. 다중집합 A는 원소 "1"을 3개 가지고 있고, 다중집합 B는 원소 "1"을 5개 가지고 있다고 하자. 이 다중집합의 교집합 A ∩ B는 원소 "1"을 min(3, 5)인 3개, 합집합 A ∪ B는 원소 "1"을 max(3, 5)인 5개 가지게 된다. 다중집합 A = {1, 1, 2, 2, 3}, 다중집합 B = {1, 2, 2, 4, 5}라고 하면, 교집합 A ∩ B = {1, 2, 2}, 합집합 A ∪ B = {1, 1, 2, 2, 3, 4, 5}가 되므로, 자카드 유사도 J(A, B) = 3/7, 약 0.42가 된다.

이를 이용하여 문자열 사이의 유사도를 계산하는데 이용할 수 있다. 문자열 "FRANCE"와 "FRENCH"가 주어졌을 때, 이를 두 글자씩 끊어서 다중집합을 만들 수 있다. 각각 {FR, RA, AN, NC, CE}, {FR, RE, EN, NC, CH}가 되며, 교집합은 {FR, NC}, 합집합은 {FR, RA, AN, NC, CE, RE, EN, CH}가 되므로, 두 문자열 사이의 자카드 유사도 J("FRANCE", "FRENCH") = 2/8 = 0.25가 된다.

### 제한 사항

---

입력으로는 str1과 str2의 두 문자열이 들어온다. 각 문자열의 길이는 2 이상, 1,000 이하이다.
입력으로 들어온 문자열은 두 글자씩 끊어서 다중집합의 원소로 만든다. 이때 영문자로 된 글자 쌍만 유효하고, 기타 공백이나 숫자, 특수 문자가 들어있는 경우는 그 글자 쌍을 버린다. 예를 들어 "ab+"가 입력으로 들어오면, "ab"만 다중집합의 원소로 삼고, "b+"는 버린다.
다중집합 원소 사이를 비교할 때, 대문자와 소문자의 차이는 무시한다. "AB"와 "Ab", "ab"는 같은 원소로 취급한다.

### 내 풀이

```javascript
function solution(str1, str2) {
  var answer = 0;
  function transEn(string) {
    string = string.toLowerCase();
    let arr = [];
    let isEn = /[a-z]/;
    for (let i = 0; i < string.length - 1; i++) {
      if (isEn.test(string[i]) && isEn.test(string[i + 1])) {
        arr.push(string[i] + string[i + 1]);
      }
    }
    return arr;
  }
  function cross(obj1, obj2) {
    const newObj = {};
    let count = 0;
    for (let att in obj1) {
      if (obj1[att] && obj2[att]) {
        newObj[att] = obj1[att] >= obj2[att] ? obj2[att] : obj1[att];
        count += newObj[att];
      }
    }

    return count;
  }
  function sum(obj1, obj2) {
    const newObj = {};
    let count = 0;
    for (let att in obj1) {
      newObj[att] = obj1[att];
    }

    for (let att in obj2) {
      newObj[att] = newObj[att] ? Math.max(newObj[att], obj2[att]) : obj2[att];
    }
    for (let att in newObj) {
      count += newObj[att];
    }

    return count;
  }
  let A_arr = {};
  transEn(str1).forEach((x) => (A_arr[x] = (A_arr[x] || 0) + 1));
  let B_arr = {};
  transEn(str2).forEach((x) => (B_arr[x] = (B_arr[x] || 0) + 1));

  let cross_n = cross(A_arr, B_arr);
  let sum_n = sum(A_arr, B_arr);
  answer = Math.floor((cross_n / sum_n) * 65536);
  if (cross_n === 0 && sum_n === 0) {
    answer = 65536;
  }
  return answer;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(str1, str2) {
  function explode(text) {
    const result = [];
    for (let i = 0; i < text.length - 1; i++) {
      const node = text.substr(i, 2);
      if (node.match(/[A-Za-z]{2}/)) {
        result.push(node.toLowerCase());
      }
    }
    return result;
  }

  const arr1 = explode(str1);
  const arr2 = explode(str2);
  const set = new Set([...arr1, ...arr2]);
  let union = 0;
  let intersection = 0;

  set.forEach((item) => {
    const has1 = arr1.filter((x) => x === item).length;
    const has2 = arr2.filter((x) => x === item).length;
    union += Math.max(has1, has2);
    intersection += Math.min(has1, has2);
  });
  return union === 0 ? 65536 : Math.floor((intersection / union) * 65536);
}
```

### 내 생각

카카오 코딩테스트 문제였는데
나도 나쁘지 않게 풀었다고 생각한다 이 문제 덕분에 정규표현식도 정리하면서 더 알 수 있었고
인상깊었던 것은 내가 처음에 생각했던 정규표현식 /[a-z | A-z]{2}/를 사용하게 인상깊었다.
그거를 전체를 적용한게 아니라 substring을 통해서 2개씩 짜르면서 그게 영어인지 구분하고 push 하였다.
그렇게 1번 문자열과 2번 문자열을 정리하고 그렇게 합집합을 구성하였고
그 합집합을 기준으로 1번배열과 2번배열에서 아이템 개수를 정리하였다
union에는 max값을 기준으로 합집합의 개수를
intersetion에는 min을 기준으로 교집합의 개수를 추정하였다
정말 깔끔하게 만든것같다 참..
