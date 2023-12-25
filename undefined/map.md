# map

JavaScript의 배열 메서드 `map`은 배열의 각 요소에 대해 주어진 함수를 호출하고, 그 결과를 모아 새로운 배열을 생성하는 데 사용됩니다. 이 메서드는 원본 배열을 변경하지 않으며, 원본 배열의 각 요소를 변형한 새로운 배열을 반환합니다. `map`은 배열의 각 요소에 동일한 연산을 적용할 때 매우 유용합니다.

#### `map()` 메서드의 기본 구조:

```javascript
let newArray = arr.map(function(element, index, array) {
    // 변환 로직
    return newValue;
});
```

* **element**: 배열의 현재 처리중인 요소입니다.
* **index**: (선택적) 현재 요소의 인덱스입니다.
* **array**: (선택적) `map` 메서드가 호출된 원본 배열입니다.

`map` 함수는 이 함수에 의해 반환된 값으로 구성된 새 배열을 생성합니다. 이 새 배열의 길이는 원본 배열의 길이와 동일합니다.

#### `map`의 사용 예시

1.  **각 요소의 제곱을 계산하는 예제:**

    ```javascript
    const numbers = [1, 2, 3, 4, 5];
    const squared = numbers.map(number => number * number);
    console.log(squared); // [1, 4, 9, 16, 25]
    ```
2.  **객체 배열에서 특정 속성 추출:**

    ```javascript
    const people = [
      { name: 'Alice', age: 25 },
      { name: 'Bob', age: 30 },
      { name: 'Carol', age: 35 }
    ];

    const names = people.map(person => person.name);
    console.log(names); // ['Alice', 'Bob', 'Carol']
    ```
3.  **복잡한 데이터 구조 변환:**

    ```javascript
    const strings = ['1', '2', '3', '4', '5'];
    const numbers = strings.map(str => parseInt(str));
    console.log(numbers); // [1, 2, 3, 4, 5]
    ```

`map`은 배열의 요소를 변환하거나, 원본 배열을 기반으로 새로운 형태의 데이터를 만들 때 매우 효과적인 메서드입니다.

조건문을 넣어서 구현할 수도 있다.

```javascript
const people = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Carol", age: 35 },
  { name: "Ash", age: 40 },
  { name: "Robert", age: 32 },
  { name: "Summer", age: 37 },
];

// nams for larger than 30
const names = people.map((person) => {
  if (person.age > 30) {
    return person;
  }
});

console.log(names);

// [
//   undefined,
//   undefined,
//   { name: 'Carol', age: 35 },
//   { name: 'Ash', age: 40 },
//   { name: 'Robert', age: 32 },
//   { name: 'Summer', age: 37 }
// ]
```

위와 같이 할 수 있지만 , 결과 값이 없을 때는 undefined 를 출력하게 된다 .그래서 이럴경우 filter 를 사용하는것이 더 좋다.

