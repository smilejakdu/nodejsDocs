# reduce

```typescript
array.reduce(function(accumulator, currentValue, currentIndex, array) {
  // 로직
}, initialValue);

```

* **accumulator (누산기)**: 리듀서 함수의 반환 값이 누적되는 변수입니다. 리듀서의 실행 결과는 이 변수에 저장됩니다.
* **currentValue (현재 값)**: 배열의 현재 처리 중인 요소입니다.
* **initialValue (초기 값)**: 누산기의 초기 값입니다. `reduce` 호출 시 제공됩니다.

쉽게 예시로 list 로하면&#x20;

```javascript
const arr = [1, 2, 3, 4, 5]
  
arr.reduce(function (acc, cur, idx) {
  console.log(acc, cur, idx);
  return acc + cur;
}, 0);
 
// arr cur idx
// 0 1 0
// 1 2 1
// 3 3 2
// 6 4 3
// 10 5 4


const arr = [1, 2, 3, 4, 5]

arr.reduce(function (acc, cur) {
  console.log(acc, cur);
  return acc + cur;
}, 0);

// 출력:
// 0 1
// 1 2
// 3 3
// 6 4
// 10 5

const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);

console.log(sum); // 출력 결과: 15
```

위와 같이 값이 출력된다.

```typescript
const products = [
  { name: "Product A", price: 100 },
  { name: "Product B", price: 200 },
  { name: "Product C", price: 300 }
];

const averagePrice = products.reduce((acc, product) => acc + product.price, 0) / products.length;
console.log(averagePrice); // 출력: 200

```

