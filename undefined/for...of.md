# for...of 루프

ES6에서 도입된 `for...of` 구문은 배열의 각 요소에 대해 반복합니다.

`break` , `continue` , `return` 문을 사용할 수 있습니다.

```typescript
const array = [1, 2, 3, 4, 5];
for (const item of array) {
  console.log(item);
}

```



JavaScript에서 `for...of` 문은 ES6 (ECMAScript 2015)에서 도입된 반복문으로, 배열이나 문자열과 같은 반복 가능한 객체(iterable objects)를 쉽게 순회할 수 있게 해줍니다. `for...of`는 배열의 요소나 문자열의 문자 등 반복 가능한 객체의 개별 값에 직접 접근할 수 있어, 반복 작업을 간결하고 명확하게 작성할 수 있습니다.

#### `for...of` 루프의 기본 구조:

```javascript
for (const item of iterable) {
  // 반복적으로 실행할 코드
}
```

* **iterable**: 반복 가능한 객체 (예: 배열, 문자열, Map, Set 등)입니다.
* **item**: 반복할 때마다 `iterable`의 현재 요소 값이 이 변수에 할당됩니다.

#### 주요 특징과 장점:

1. **간결하고 명확함**: `for...of` 루프는 배열이나 다른 반복 가능한 객체의 요소를 순회할 때 코드를 간결하고 이해하기 쉽게 만들어 줍니다.
2. **유연한 제어문 사용**: `break`, `continue`, `return` 등의 제어문을 `for...of` 루프 안에서 사용할 수 있어, 복잡한 로직을 구현하는 데 유용합니다.
3. **다양한 객체에 적용 가능**: `for...of`는 배열뿐만 아니라 문자열, Map, Set 등 다양한 자료형에 대해 사용할 수 있습니다.

#### 사용 예시:

1.  **배열 순회**:

    ```javascript
    const array = [1, 2, 3, 4, 5];
    for (const value of array) {
      console.log(value);
    }
    // 출력: 1, 2, 3, 4, 5
    ```
2.  **문자열 순회**:

    ```javascript
    const string = "Hello";
    for (const char of string) {
      console.log(char);
    }
    // 출력: H, e, l, l, o
    ```
3.  **Map 구조 순회**:

    ```javascript
    const map = new Map([['a', 1], ['b', 2], ['c', 3]]);
    for (const [key, value] of map) {
      console.log(`${key}: ${value}`);
    }
    // 출력: a: 1, b: 2, c: 3

    ```
4. Object Map 구조 순회:\


```typescript
const people = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 30 },
  { name: 'Carol', age: 35 }
];

for (const person of people) {
  console.log(`${person.name} , ${person.age}`);
}
// Alice , 25
// Bob , 30
// Carol , 35
```

`for...of` 루프는 특히 순회할 객체의 구조가 복잡하거나 반복 작업을 좀 더 직관적으로 표현하고 싶을 때 매우 유용합니다.
