# Factory pattern

    자바스크립트에서는 생성자를 사용하여 객체를 생성할 수 있습니다. 그러나 생성자를 사용하면 몇 가지 단점이 있습니다. 생성자의 가장 큰 문제 중 하나는 일반 함수처럼 보이지만 전혀 일반 함수처럼 작동하지 않는다는 것입니다. new 키워드 없이 생성자 함수를 사용하려고 하면 프로그램이 예상대로 작동하지 않지만 추적하기 쉬운 오류 메시지를 생성하지 않습니다. 객체 생성을 위한 더 나은 솔루션은 Factory functions 이라고 할 수 있습니다.

## Use factory pattern

    팩토리 함수 패턴은 생성자와 비슷하지만 new를 사용하여 객체를 생성하는 대신 팩토리 함수는 함수를 호출할 때 새 객체를 설정하고 반환하기만 하면 됩니다.

```javascript
const personFactory = (name, age) => {
  const sayHello = () => console.log("hello!");
  return { name, age, sayHello };
};

const jeff = personFactory("jeff", 27);

console.log(jeff.name); // 'jeff'

jeff.sayHello(); // hello!
```

---

<br />

    다음은 생성자 패턴을 사용하여 생성한 것과 동일한 것입니다.

```javascript
const Person = function (name, age) {
  this.sayHello = () => console.log("hello!");
  this.name = name;
  this.age = age;
};

const jeff = new Person("jeff", 27);
```

---

<br />

    팩토리 함수에서의 상속

```javascript
const Person = (name) => {
  const sayName = () => console.log(`my name is ${name}`);
  return { sayName };
};

const Nerd = (name) => {
  // 구조 분해 할당 구문으로 사람을 만들고 sayName 함수를 꺼냅니다.
  const { sayName } = Person(name);
  const doSomethingNerdy = () => console.log("nerd stuff");
  return { sayName, doSomethingNerdy };
};

const jeff = Nerd("jeff");

jeff.sayName(); //my name is jeff
jeff.doSomethingNerdy(); // nerd stuff
```

---

<br />

# Module pattern

    ES6에는 모듈 기능이 있습니다. 본질적으로 Javascript 파일 간에 모듈을 가져오고 내보내는 구문입니다. 그러나 그것들은 우리가 여기서 말하는 것이 아닙니다. 모듈은 실제로 팩토리 함수와 매우 유사합니다. 주요 차이점은 생성 방법입니다.

```javascript
const caculator = (() => {
  const add = (a, b) => a + b;
  const sub = (a, b) => a - b;
  const mul = (a, b) => a * b;
  const div = (a, b) => a / b;
  return {
    add,
    sub,
    mul,
    div,
  };
})();

console.log(caculator.add(3, 5)); // 8
console.log(caculator.sub(6, 2)); // 4
console.log(caculator.mul(14, 5534)); // 77476
```

    개념은 팩토리 기능과 정확히 동일합니다. 그러나 여러 객체를 생성하기 위해 반복해서 사용할 수 있는 팩토리를 생성하는 대신, 모듈 패턴은 IIFE(즉시 호출된 함수 표현식)에서 팩토리를 래핑합니다.

    위의 계산기 예제에서 IIFE 내부의 함수는 간단한 팩토리 함수이지만 계속 진행하여 변수 계산기에 객체를 할당할 수 있습니다. 이것은 계산기를 많이 만들지 않고 하나만 필요하기 때문에 유용합니다. 팩토리 함수와 마찬가지로 개인 함수와 변수를 원하는 만큼 가질 수 있으며 모듈 내부에 깔끔하게 정리되고 숨겨져 프로그램에서 실제로 사용하려는 함수만 노출됩니다.

---
