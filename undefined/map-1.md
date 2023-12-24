# map

Array.prototype.map() 은 배열의 각 요소에 대해 주어진 함수를 호출하고, 그 결과를 새 배열로 반환합니다.

이 메서드는 원본 배열을 변경하지 않으며, 동일한 길이의 새 배열을 생성합니다.

각 요소에 대해 실행되는 함수는 해당 요소, 그 요소의 인덱스, 그리고 map 이 호출된 원본 배열을 인자로 받습니다.

```javascript
const numbers = [1, 2, 3, 4, 5];
const squared = numbers.map(num => num * num);

console.log(squared); // 출력: [1, 4, 9, 16, 25]

```

