# 원시타입, 참조타입, 원시래퍼 타입

**원시타입의 종류**

- Boolean : true, false
- Number : 1, 2, 3 ...
- String : ‘Hello World’
- null
- undefined

**원시타입의 특징**

    원시값을 변수에 할당하면 값이 복사되어 들어간다.
    원시값이 할당된 변수들은 모두 자기 자신만의 고유한 값을 가지게 된다.

    typeof
    원시값의 종류를 할 수 있게 해주는 매서드
    Null의 타입에 주의

```javascript
console.log(typeof 1); // number
console.log(typeof "hi"); // string
console.log(typeof true); // boolean
console.log(typeof undefined); // undefined
console.log(typeof null); // object
```

<br />

**참조타입의 종류**

- Object : { }
- Array : [ ]
- Function : function
- Date
- 정규표현식 : RegExp

**참조타입의 특징**

    원시 타입 빼고 전부 참조타입으로 봐도 된다.
    참조 타입은 변수에 값을 직접 저장하지 않는다.
    변수에 저장되는 것은 메모리 안에서 객체의 위치를 가르키는 ‘포인터’
    무엇이 저장되느냐, 이것이 원시 타입과 참조타입의 가장 큰 차이

<br />

**원시래퍼타입의 종류**

- String
- Number
- Boolean
