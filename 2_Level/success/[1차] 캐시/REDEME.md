# [1차] 캐시

### 문제 설명

---

지도개발팀에서 근무하는 제이지는 지도에서 도시 이름을 검색하면 해당 도시와 관련된 맛집 게시물들을 데이터베이스에서 읽어 보여주는 서비스를 개발하고 있다.
이 프로그램의 테스팅 업무를 담당하고 있는 어피치는 서비스를 오픈하기 전 각 로직에 대한 성능 측정을 수행하였는데, 제이지가 작성한 부분 중 데이터베이스에서 게시물을 가져오는 부분의 실행시간이 너무 오래 걸린다는 것을 알게 되었다.
어피치는 제이지에게 해당 로직을 개선하라고 닦달하기 시작하였고, 제이지는 DB 캐시를 적용하여 성능 개선을 시도하고 있지만 캐시 크기를 얼마로 해야 효율적인지 몰라 난감한 상황이다.

어피치에게 시달리는 제이지를 도와, DB 캐시를 적용할 때 캐시 크기에 따른 실행시간 측정 프로그램을 작성하시오.

### 제한 사항

---

캐시 교체 알고리즘은 LRU(Least Recently Used)를 사용한다.
cache hit일 경우 실행시간은 1이다.
cache miss일 경우 실행시간은 5이다.

### 내 풀이

```javascript
function solution(cacheSize, cities) {
  let cacheList = Array(cacheSize).fill(0);
  let cnt = 0;
  cities.map((city, idx) => {
    city = city.toLowerCase();
    if (cacheList.includes(city)) {
      let temp = cacheList[cacheList.indexOf(city)];
      cacheList.splice(cacheList.indexOf(city), 1);
      cacheList.unshift(temp);
      cnt++;
    } else {
      cacheList.unshift(city);
      cacheList.pop();
      cnt += 5;
    }
  });
  return cnt;
}
```

### 인상적이였던 풀이 방법

```javascript
function solution(cacheSize, cities) {
  const map = new Map();
  const cacheHit = (city, map) => {
    map.delete(city);
    map.set(city, city);
    return 1;
  };
  const cacheMiss = (city, map, size) => {
    if (size === 0) return 5;
    map.size === size && map.delete(map.keys().next().value);
    map.set(city, city);
    return 5;
  };
  const getTimeCache = (city, map, size) =>
    (map.has(city.toLocaleLowerCase()) ? cacheHit : cacheMiss)(
      city.toLocaleLowerCase(),
      map,
      size
    );
  return cities
    .map((city) => getTimeCache(city.toLocaleLowerCase(), map, cacheSize))
    .reduce((a, c) => a + c, 0);
}
```

### 내 생각

카카오 코딩테스트 문제였는데
일단 LRU(Least Recently Used)라는 캐시 교체 알고리즘을 사용하라고 하였다
이는 사용 하는 것 위주로 캐시를 구성하는 알고리즘인데
오래된 데이터를 지우는 방식으로 진행하되 만약 캐시 내부에 있는 내용을 호출 할 경우
그 내용을 최상단으로 이동하여 캐시를 구성하는 알고리즘이다.
위에 인상깊은 내용은 객체지향이라고 해야할까? 너무 잘 구성해서 작성하였기에 이렇게
작성하는 법을 배워야 할 것 같아서 인상 깊었다.
