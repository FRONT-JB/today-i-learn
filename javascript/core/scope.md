# 스코프 ( Scope )

**스코프 ( Scope ) 란?**

`변수의 접근성과 생존 기간을 제어`

```javascript
var func1 = function () {
  var a = 1;
  var b = 2;
  console.log(a + b); // 3;
  return a + b;
};

var a = 20;
// 변수의 이름이 a지만 func1는 함수 스코프안에 있는 변수를 연산한다.
func1();
console.log(b); // error
// b 변수 역시 func1 함수 안에 있기때문에 error 발생
```

    스코프는 이름이 충돌하는 문제를 덜어주고, 자동으로 메모리를 관리

<br />

**자바스크립트의 유효 범위**

1. 전역 스코프
2. 함수 스코프
3. 블록 스코프 (es6)

**전역 스코프**

    스크립트의 어디서든 접근이 가능하기 때문에 사용이 쉽다.
    타인과 협업, 라이브러리 사용시 충돌의 가능성이 있다.

**함수 스코프**

```javascript
var func = function () {
  var a = 1;
  var b = 2;

  var func2 = function () {
    var b = 5;
    var c = 6;

    a = a + b + c;
    console.log(a); // 12;
    // 함수의 내부에서 선언된 변수라면 함수의 어느 부분에서도 접근
  };

  func2();
};
func();

////////////////////////////////////

function test() {
  val = "hello";
  var val2 = "world";
}

test();

console.log(val2); // error
console.log(val); // 'hello'
// val은 선언된 변수가 아니기 때문에 전역으로 읽는다.
```

    함수 내부에서 정의된 변수와 매개변수는 함수 외부에서 접근할 수 없다.
    함수 내부에서 정의된 변수라면 함수의 어느 부분에서도 접근할 수 있다.

**블록 스코프**

```javascript
if (true) {
  var value = "hello";
}

console.log(value); // 'hello'

if (true) {
  let value = "world";
}

console.log(value); // 'hello'
// let, const는 중괄호 (블록스코프 안에서만 접근)
```

<br />

**정리**

스코프는 `변수의 접근성과 생존 기간을 제어`한다.

스코프는 `이름이 충돌하는 문제를 덜어주고, 자동으로 메모리를 관리`

자바스크립트에는 `전역스코프`, `함수스코프`, `블록스코프가` 존재
