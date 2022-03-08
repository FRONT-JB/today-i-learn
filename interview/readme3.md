# JS Shallow Copy, Deep Copy

[자바스크립트의 얕은 복사(shallow copy)](https://velog.io/@cjy9306/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%ACshallow-copy)

**react에서는 각 컴포넌트의 리렌더링을 최적화하기 위해 자바스크립트의 얕은 복사를 활용합니다. 얕은 복사로 렌더링할지 말지를 빠르게 결정하는 것입니다.**

## 1. Primitive type, Objects

`자바스크립트의 타입은 크게 2가지가 있습니다.`

Primitive type과 Object가 그것인데요. 다음과 같이 분류됩니다.

**Primitive type**

    Boolean, null, undefined, string, Number

    Primitive type들은 데이터 대입(전달)시 모두 실제 value가 복사됩니다.

**Objects (Objects 타입들은 모두 기술적으로 모두 object임)**

    Array, Function, Object

    Objects들은 데이터 대입(전달)시 모두 해당 객체의 주소값이 전달되며, reference가 전달되었다고 합니다.

## 2. 얕은 복사 예제

얕은 복사를 할 때에는 ES6이후 기준으로 Object.assign() 함수와 spread 연산자({...})를 사용합니다.

```javascript
let obj1 = { a: 1, b: { c: 1 } };
let obj2 = obj1;
let obj3 = { ...obj1 };
obj1.a = 2;
obj1.b.c = 3;

console.log(JSON.stringify(obj2)); // {"a":2,"b":{"c":3}}
console.log(JSON.stringify(obj3)); // {"a":1,"b":{"c":3}}
```

<br />

```javascript
let obj2 = obj1;
...
obj1.a = 2;
obj1.b.c = 3;
```

    위의 구문에선 obj2에 obj1의 reference(주소값)이 저장됩니다.
    따라서 obj1.a, obj1.b.c의 값이 변경됬을때 값이 같이 바뀌는 것을 볼 수 있습니다.

<br />

```javascript
let obj3 = { ...obj1 };
obj1.a = 2;
obj1.b.c = 3;
```

    위의 구문에선 spread 연산자를 사용하였습니다.
    위의 예시에서 {...obj1}은 obj1의 reference를 복사하는 것이 아니라
    obj1 객체의 내용안에 있는 값들을 복사합니다.

    따라서 obj1.a = 2를 했어도 a는 primitive type이기 때문에
    obj3에 복사될때 값이 복사가 되어 그대로 1이 출력되는 것을 볼 수있습니다.

    하지만 obj3.b.c의 값은 변경되었는데요.

    이것은 spread 연산자가 객체의 첫번째 depth에 해당하는 값만 복사하고,
    obj1.b는 객체타입이기 때문에 obj3.b에는 obj1.b의 refernece가 저장되었기 때문입니다.

<br />

---

[JS - 얕은 복사(Shallow Copy )와 깊은 복사(Deep Copy)](https://taenami.tistory.com/98?category=1181397)

**primitive type의 값을 복사할 때는, 다른 메모리에 할당하기 때문에 원래의 값과 복사된 값이 서로에게 영향을 미치지 않습니다.**

```javascript
const age = 29;
let nextYearAge = age;

nextYearAge += 1;

console.log(age); // 29
console.log(nextYearAge); // 30
```

**reference type의 값을 복사할 때는, 선언된 변수의 주소가 객체의 주소를 가리키고 있기 때문에, 아래와 같습니다**

```javascript
const me = {
  region: "seoul",
  age: 29,
};

let jackson = me;
jackson.age = 30;

console.log(me); // {region: 'seoul', age: 30}
console.log(jackson); // {region: 'seoul', age: 30}
```

jackson object의 내부 프로퍼티인 age의 값을 30으로 바꾸었는데
원치 않게 me object의 age 값도 바뀌어지게 되었습니다.

이러한 객체의 특징 때문에, 원본 객체를 복사하면서, 원본 객체의 프로퍼티의 값을 바꾸지 않게 하기 위해선 원본 객체를 복사할 때 그 `주소값`만 복사하는 방법을 고민해봐야 합니다.

`얕은 복사(Shallow Copy)`와 `깊은 복사(Deep Copy)`를 사용해야 합니다.

<br />

**얕은 복사 ( Shallow Copy )**

    얕은 복사란 객체를 복사할 때 원래 값과 복사된 값이 같은 참조를 가리키고 있는 것을 말합니다.
    얕은 복사를 하기 위한 방법으로 다음 2가지가 있습니다.

1. **Object.assign()**

   Object.assign 메소드는 원본 객체로부터 복사하고 새로운 객체를 반환합니다.
   첫 번째 요소로 들어온 객체에 다음 인자로 들어온 객체를 복사해줍니다.

```javascript
const me = {
  name: "taenam",
  region: "korea",
  lastYear: {
    age: 28,
  },
};

const jackson = Object.assign({}, me);
jackson.region = "us";
jackson.lastYear.age = 25;

console.log(me.region); // korea
console.log(jackson.region); // us

console.log(me.lastYear.age); // 25
console.log(jackson.lastYear.age); // 25
```

<br />

2. **Spread Operator**

```javascript
const me = {
  name: "taenam",
  region: "korea",
  lastYear: {
    age: 28,
  },
};

const jackson = { ...me };
jackson.region = "us";
jackson.lastYear.age = 25;

console.log(me.region); // korea
console.log(jackson.region); // us

console.log(me.lastYear.age); // 25
console.log(jackson.lastYear.age); // 25
```

    얕은 복사를 이용하면 객체의 바로 아래에 있는 프로퍼티의 값만 바꿀 수 있습니다.
    반면, 한 단계 더 들어간 내부 프로퍼티들은 기존 객체를 그대로 참조하고 있는 문제점이 있습니다.

<br />

**깊은 복사 ( Deep Copy )**

1. **재귀함수 이용**

```javascript
const me = {
  name: "taenam",
  region: "korea",
  lastYear: {
    age: 28,
  },
};

const copyObj = (obj) => {
  const result = {};

  for (let key in obj) {
    if (typeof obj[key] === "object" && obj[key] !== null) {
      result[key] = copyObj(obj[key]);
    } else {
      result[key] = obj[key];
    }
  }

  return result;
};

let jackson = copyObj(me);
jackson.region = "us";
jackson.lastYear.age = 25;

console.log(me.region); // korea
console.log(jackson.region); // us

console.log(me.lastYear.age); // 28
console.log(jackson.lastYear.age); // 25
```

    Object의 Depth가 길어질수록 Time Complexity(시간 복잡도)도 늘어나게 되는 단점이 있습니다.

<br />

2. **JSON 객체 method 이용**

```javascript
const me = {
  name: "taenam",
  region: "korea",
  lastYear: {
    age: 28,
  },
  greeting: () => {
    console.log("hello ~");
  },
};

const copyObj = (obj) => JSON.parse(JSON.stringify(obj));

let jackson = copyObj(me);
jackson.region = "us";
jackson.lastYear.age = 25;

console.log(me.region); // korea
console.log(jackson.region); // us

console.log(me.lastYear.age); // 28
console.log(jackson.lastYear.age); // 25

console.log(me.greeting());
// hello ~
console.log(jackson.greeting());
// Uncaught TypeError: jackson.greeting is not a function
```

    먼저, JSON.stringify로 자바스크립트 객체(object)를 JSON문자열로 변환시킨 뒤 JSON.
    parse는 JSON문자열을 자바스크립트 객체로 다시 변환시키면서 객체에 대한 참조가 없어진 것입니다.

    이 방법의 단점으로는 다른 방법에 비해서 성능적으로 느리다는 점과
    JSON.stringify 메소드가 function을 undefined로 처리한다는 점이 있기 때문에
    복사된 객체에서 함수를 호출하게 되면 에러가 발생합니다.

<br />

3. **Lodash의 deepclone 함수 사용**

```javascript
const clonedeep = require("lodash.clonedeep");

const me = {
  name: "taenam",
  region: "korea",
  lastYear: {
    age: 28,
  },
};

let jackson = clonedeep(me);
jackson.region = "us";
jackson.lastYear.age = 25;

console.log(me.region); // korea
console.log(jackson.region); // us

console.log(me.lastYear.age); // 28
console.log(jackson.lastYear.age); // 25
```

    Lodash는 많은 메서드들을 제공하는데, 그중 하나인 clonedeep method를 사용하면 깊은 복사가 가능합니다.

<br />

---
