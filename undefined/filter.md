# filter

JavaScript의 `filter` 메서드는 배열의 각 요소에 대해 주어진 테스트 함수를 실행하고, 이 테스트를 통과하는 모든 요소들로 구성된 새로운 배열을 생성합니다. 이 메서드는 원본 배열을 변경하지 않으며, 조건에 맞는 요소들만을 필터링하여 새로운 배열을 반환합니다.

#### `filter()` 메서드의 기본 구조:

```typescript
const newArray = array.filter(function(element, index, array) {
    // 테스트 조건
    return condition;
});
```

* **element**: 배열의 현재 처리 중인 요소입니다.
* **index**: (선택적) 현재 요소의 인덱스입니다.
* **array**: (선택적) `filter` 메서드가 호출된 원본 배열입니다.

`filter` 함수 내에서 반환되는 조건 (`condition`)은 불린 값이어야 합니다. 이 조건이 `true`로 평가되는 요소들만이 새로운 배열에 포함됩니다.

#### `filter`의 사용 예시

1.  **특정 조건을 만족하는 요소 필터링:**

    ```typescript
    const numbers = [1, 2, 3, 4, 5];
    const evenNumbers = numbers.filter(number => number % 2 === 0);
    console.log(evenNumbers); // [2, 4]
    ```
2.  **객체 배열에서 조건에 맞는 요소 추출:**

    ```typescript
    const people = [
      { name: 'Alice', age: 25 },
      { name: 'Bob', age: 30 },
      { name: 'Carol', age: 35 }
    ];

    const adults = people.filter(person => person.age >= 30);
    console.log(adults); // [{ name: 'Bob', age: 30 }, { name: 'Carol', age: 35 }]
    ```
3.  **특정 문자열을 포함하는 요소 필터링:**

    ```typescript
    const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
    const longWords = words.filter(word => word.length > 6);
    console.log(longWords); // ["exuberant", "destruction", "present"]
    ```

`filter` 메서드는 특정 조건에 따라 배열의 요소를 선택할 때 유용하며, 이를 통해 데이터 세트를 줄이거나 특정 기준에 맞는 요소들만 추출할 수 있습니다.



## 배열을 받고 새로운 배열을 return 한다.

`filter` 메서드는 반환값이 배열입니다. `filter` 메서드는 원본 배열의 각 요소에 대해 주어진 콜백 함수를 실행하고, 그 콜백 함수가 `true` 를 반환하는 요소들만을 모아 새로운 배열을 생성합니다.

`filter` 메서드가 새로운 배열을 생성하는 것이 비효율적인것 처럼 보일 수 있으나 JavaScript에서 배열을 처리하는 데 있어서는 일반적이고 효율적인 접근법입니다.

