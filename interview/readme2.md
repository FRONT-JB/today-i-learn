# Redux 와 context api의 차이점

`Redux` : 전역상태를 생성하고 관리하기 위한 라이브러리(타 프레임워크에서 사용가능) + 그 외에 여러 기능 제공

    Store : 전역 상태 보관소
    Reducer : Store에 접근시킴
    Action : Reducer에 Action을 지시

`ContextAPI` : 상태의 중앙 관리를 위한 상태 관리 도구. React에서만 사용 가능하고 Redux와 다르게 여러 저장소가 존재할 수 있다.

    Context : 전역 상태 보관소
    Provider : 전역 상태를 제공
    Consumer : 전역 상태를 받아 사용

<br />

---

# Typescript에서의 Generic

[TypeScript | Generic 제네릭 (feat. TypeScript 두 달차 후기)](https://velog.io/@edie_ko/TypeScript-Generic-%EC%A0%9C%EB%84%A4%EB%A6%AD-feat.-TypeScript-%EB%91%90-%EB%8B%AC%EC%B0%A8-%ED%9B%84%EA%B8%B0)

[Generic 사용법](https://darrengwon.tistory.com/802)

<br />

---

# Styled-Component를 사용하는 이유? (CSS-IN-JS)

1. 자유로운 CSS 커스텀 컴포넌트를 만들 수 있다.

   style과 component간의 매핑이 제거됨 (style이 component의 필수 부분이 됨)

2. 인라인 스타일링의 단점

   위에서 자세하게 설명했다.

3. 모바일 지원

   React Native로 모바일 개발을 할 때, 재사용할 수 있다!

4. 스코프

   해당 컴포넌트에 대해서의 스타일만을 정의하므로, 스타일 적용범위가 한정적이라서 사이드 이펙트 확률이 줄어든다.

5. No-class policy가 가능

6. 서버사이드 렌더링

7. 단위 테스팅

   styled-component도 실제 컴포넌트이기 때문에 단위 테스트를 수행할 수 있습니다!

8. SASS도 적용가능!

9. 유명하다 (인기많고 안정적이다.)

<br />

---

# Redux-Saga와 Redux-Thunk의 차이

`Redux-Thunk`

    Redux-Thunk

    객체가 아닌, 동기 또는 비동기 작업을 수행할 수 있는 함수를 말한다.
    썽크를 사용하려면 액션 생성자는 객체가 아닌 이 함수를 반환해야 한다.
    이는 리덕스 스토어와의 상호작용을 위해 getState(), dispatch() 함수를 인자로 받는다.
    따라서 리덕스 스토어의 상태에 접근하거나 또 다른 액션을 디스패치 하는 것이 가능하다.

<br />

    썽크 미들웨어

    디스패치 된 액션의 타입이 객체가 아닌 함수(= 썽크)인 경우, 이를 직접 처리한다.
    이때 인자로 store.dispatch(), store.getState() 함수를 넘기며 해당 썽크를 호출한다.
    참고로 여기서 전달받은 dispatch() 함수를 호출하면 다음 미들웨어의 dispatch() 함수를 호출하는 것이 아니라 스토어의 dispatch() 함수를 호출하는 것이기 때문에 미들웨어 체인의 맨 처음으로 다시 돌아가게 된다.
    만약 액션의 타입이 객체라면, 다음 미들웨어의 dispatch() 함수로 이를 처리한다(다음 미들웨어에게 넘긴다).

<br />

`Redux-Saga`

    사가 (= 제네레이터 함수)

    제네레이터를 반환하는 함수이다.
    해당 제네레이터의 next() 함수를 호출함으로써 사가를 실행할 수 있다.
    사가는 yield 표현식을 만날 때마다 실행이 중단되며, 해당 표현식의 값은 next() 함수의 반환 값에 포함된다.
    next() 함수의 인자로 넘기는 값은 해당 사가의 실행이 중단되어 있는 위치의 yield 표현식 자리를 채워준다.

<br />

    사가의 실행 흐름

    사가 미들웨어의 run 메소드가 엔트리 포인트에 해당하는 루트 사가를 실행한다.
    사가의 실행은 해당 제네레이터 함수를 호출하여 반복 가능한 제네레이터를 획득하는 것으로 시작한다.
    이제 해당 제네레이터의 next() 함수를 통해 이펙트를 읽고 지시된 동작을 수행하는 작업을 반복한다.
    그러다가 fork 이펙트를 읽으면, 해당 사가를 실행하는 또 다른 새로운 실행 맥락을 하나 만들어낸다.

<br />

    사가 미들웨어의 구현

    사가 미들웨어도 다른 미들웨어와 똑같이 store => next => dispatch 시그니쳐를 가지는 함수이다.
    그런데 사가 미들웨어에는 특별히 루트 사가의 실행을 위한 하나의 함수가 run 메소드로서 부착된다.
    그리고 사가 미들웨어는 호출되는 순간 그 함수에 store의 두 메소드를 바인딩시켜주도록 구현된다.
    따라서 run 메소드는 루트 사가를 실행하는 동안, 리덕스의 스토어와 직접적인 상호작용이 가능하다.
    그래서 select, put 이펙트를 각각 getState(), dispatch() 함수로 처리할 수 있게 되는 것이다.

<br />

    일반적인 사가 사용 패턴

    루트 사가는 여러 개의 Watcher 사가를 fork 한다. 각 Watcher 사가는 특정 액션을 기다린다.
    각 Watcher 사가는 특정 액션이 디스패치 될 때 이를 감지하여 해당 Worker 사가를 fork 한다.

<br />

    사가 미들웨어의 역할

    사가 미들웨어는 디스패치 된 액션을 캐치해서 이를 Watcher 사가에게 알리는 역할만 수행할 뿐이다.
    따라서 해당 액션이 리듀서에 도달했는지 다른 미들웨어에 의해 중간에 변형되었는지는 알지 못한다.
    즉, 다른 미들웨어들과 달리 액션을 디스패치 하는 과정 자체에는 직접적으로 관여하지 않는다.

<br />

    이펙트

    사가를 실행하는 실행부에게 어떠한 동작을 수행해야 할지 알려주는 일반 객체(Plain Object)이다.
    일반적으로 put(), call(), select() 등의 헬퍼 함수를 호출함으로써 해당 이펙트 객체를 생성한다.
    이펙트 자체는 단순 객체이므로 아무런 사이드 이펙트를 발생시키지 않는다. 따라서 테스트가 용이하다.

<br />

    주요 이펙트

```javascript
call(fn, ...args); // (비동기 혹은 동기) 함수 fn을 호출한다.

select(selector); // selector를 이용하여 리덕스 스토어의 상태를 읽어온다. (= store.getState() 함수)

put(action); // action을 디스패치 한다. (= store.dispatch() 함수)

take(actionType); // actionType의 액션이 디스패치 될 때까지 기다린다.

fork(saga, ...args); // 새로운 실행 맥락으로 saga를 실행한다.

takeEvery(actionType, saga, ...args); // 사가를 하나 fork 하는 헬퍼 함수이다. 해당 사가는 actionType의 액션을 기다렸다가 saga를 fork 하는 작업을 무한히 반복한다.
```

---
