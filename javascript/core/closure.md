# Closure

**클로저 ( Closure ) 란?**

> 중단하다, 폐쇄하다

```javascript
var outer = function () {
  var a = 1;

  var inner = function () {
    var b = 5;
    var c = 6;

    a = a + b + c;

    console.log(a); // 12;
    // inner 함수에서는 자신을 포함한 부모의 변수에 접근이 가능하다.
  };
  inner();
};
outer();
```

```javascript
///////////////////////////////////////
// 외부 함수보다 내부함수가 오래 살아 남는 경우 //
///////////////////////////////////////

var outer = function () {
  var a = 1;

  var inner = function () {
    var b = 5;
    var c = 6;

    a = a + b + c;
    console.log(a); // 12;
  };
  // 이 시점에서 외부로 내보낸 순간
  // outer 함수에서 나간다.
  // 그 시점에서 inner 함수는 a의 값을 접근할 수 있을까?
  // inner는 outer에서 반환된 후에도 outer의 a에 접근이 가능하다.
  return inner;
};

var newInner = outer(); // inner를 리턴
newInner(); // outer 함수를 실행 -> 12
```

```javascript
///////////////////////////////////////
//        내부에 접근이 불가능한 함수       //
///////////////////////////////////////

// 즉시실행 함수
var person = (function () {
  var age = 15;

  return {
    name: "JB",
    getAge: function () {
      console.log(age);
      return age;
    },
    setAge: function (value) {
      age = value;
      console.log(age);
    },
  };
})();

person.getAge(); // 15
person.setAge(20);
person.getAge(); // 20;

person.age = 30;
person.getAge(); // 15;
// person 에 age 값은 객체 접근방식으로는 접근이 안된다.
// person.getAge()와 person.setAge(value)로만 age값에 접근한다.
```

<br />

**정리**

1. 자바스크립트 내부 함수에서 자신을 포함하는 외부함수의 스코프에 접근할 수 있다.
2. 내부 함수가 살아있는 상태에서 외부 함수가 파괴되면 외부 함수의 변수들에 대한 접근권한은 내부 함수만 가지게 된다.
3. 폐쇄된 공간에 대한 접근권한을 가지는 함수가 클로저이다.
