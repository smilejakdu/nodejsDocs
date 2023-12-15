# find

JavaScript의 `find` 메서드는 배열 내에서 주어진 테스트 함수를 만족하는 첫 번째 요소의 값을 반환합니다. 만약 어떤 요소도 주어진 테스트 함수를 만족하지 않으면 `undefined`가 반환됩니다. `find` 메서드는 원본 배열을 변경하지 않습니다.

#### `find()` 메서드의 기본 구조:

```javascript
const foundElement = array.find(function(element, index, array) {
    // 조건을 반환하는 로직
    return condition;
});
```

* **element**: 현재 처리 중인 배열의 요소입니다.
* **index**: (선택적) 현재 요소의 인덱스입니다.
* **array**: (선택적) `find` 메서드가 호출된 원본 배열입니다.

`find` 함수 내에서 제공된 테스트 함수는 배열의 각 요소에 대해 호출되며, 조건이 `true`로 평가되는 첫 번째 요소의 값을 반환합니다.

#### `find` 사용 예시

1.  **특정 조건을 만족하는 요소 찾기:**

    ```javascript
    const numbers = [1, 2, 3, 4, 5];
    const firstEven = numbers.find(number => number % 2 === 0);
    console.log(firstEven); // 2
    ```

    이 예시에서는 `numbers` 배열에서 처음으로 짝수인 요소를 찾습니다.
2.  **객체 배열에서 조건에 맞는 요소 찾기:**

    ```javascript
    const people = [
      { name: 'Alice', age: 25 },
      { name: 'Bob', age: 30 },
      { name: 'Carol', age: 35 }
    ];
    const person = people.find(p => p.age >= 30);
    console.log(person); // { name: 'Bob', age: 30 }
    ```

    여기서는 나이가 30 이상인 첫번째 사람을 찾습니다.
3.  **ID를 기반으로 특정 요소 찾기:**

    ```javascript
    const items = [
      { id: 1, name: 'Pencil' },
      { id: 2, name: 'Notebook' },
      { id: 3, name: 'Backpack' }
    ];
    const item = items.find(item => item.id === 2);
    console.log(item); // { id: 2, name: 'Notebook' }
    ```

    이 예시에서는 ID가 2인 항목을 찾습니다.

`find` 메서드는 주로 배열 내에서 특정 조건을 만족하는 첫 번째 요소를 찾을 때 유용합니다. 배열의 각 요소를 순회하면서 조건을 검사하고, 조건을 만족하는 첫 번째 요소의 값을 반환합니다.

## 만약 조건이 만족하는것을 모두 받으려면 ?? -> filter 메서드 사용

모두 받으려면 filter 를 사용하면 된다.

```typescript
const numbers = [1, 2, 3, 4, 5];
const evenList = numbers.filter(number => number % 2 === 0);
console.log(evenList); // [2, 4]

const people = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 30 },
  { name: 'Carol', age: 35 }
];

const personList = people.filter(p => p.age >= 30);
console.log(personList); // [ { name: 'Bob', age: 30 }, { name: 'Carol', age: 35 } ]
```

