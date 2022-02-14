# 코테에서 dangerousHTML을 사용한 이유?
**쓰면 안되는 이유? 이걸 자주 사용하는지?**

> 리스트 데이터에서 별점 1≤5 를 아래의 코드를 사용해서 별모양 출력

&#10029; -> `&#10029;`

&#10025; -> `&#10025;`

배열로 만들어서 map으로 돌렸을때 왜 제대로 출력이 안됐을까?

```jsx
<span>&#10025;</span>
<span>&#10029;</span>
```
<br />
<img width="934" alt="image" src="https://user-images.githubusercontent.com/85790271/153864354-4243dfd3-5bda-43fd-961d-62eb3985321c.png">


---

<br />

# Redux, Mobx, Context API 차이, 장단점 [Github](https://github.com/rangyu/TIL/blob/master/react/Redux-vs-MobX-vs-Context-API.md)

## **Redux (리덕스)**

- Flux 패턴 기반의 상태관리 라이브러리.
- 리액트스러운 개발 방식.
  - **`함수형 프로그래밍`**
  - **`불변성 강조`**
- **`단일 store 원칙. store는 오직 한 개만 가능.`**
- 러닝 커브가 가파르다. (배워야할 것이 많음)
  - 가장 많은 개발자들이 사용. 커뮤니티 활발.

## **MobX (모벡스)**

- 리액트스럽지 않은 개발 방식.
  - **`객체형 프로그래밍`**
  - **`불변성 무시 (알아서 해줌)`**
- **`store 여러 개 만들 수 있음.`**
- 러닝 커브가 완만한다. (배우기 쉬운 편)
  - 리덕스에 비하면 사용자 수 적은편

## **Context API**

- Context API는 (Redux나 MobX와 같은 외부 라이브러리가 아니라) 새로 추가된 리액트 자체 기능.
  - 리액트 16.3 버전부터 사용가능
- 별도 상태관리 라이브러리 없이도 간단하게 글로벌 상태관리가 가능하다.
- Context API를 활용한 가벼운 상태관리 라이브러리들도 나오고 있다
 
<br />

<img width="1041" alt="image" src="https://user-images.githubusercontent.com/85790271/153864173-2a0136aa-079d-4736-8f25-8b97816332fe.png">

---

<br />

# useMemo, useCallback 에서의 deps 역할?

**[useEffect, useCallback, useMemo 비교](https://velog.io/@mementomori/useEffect-useCallback-useMemo-%EB%B9%84%EA%B5%90)**

## useEffect

```jsx
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    subscription.unsubscribe();
  };
}, [props.source]);
```

    💡 class component의 life cycle 함수(side effect)를 function component 에도 동일하게 사용가능 최초 컴포넌트 마운트 되는 경우, 컴포넌트 내 레이아웃 배치와 랜더링이 완료된 후에 실행 두 번째 인자(배열)의 요소로 지정하면, 해당 요소 값의 업데이트 되는 경우에만 실행 그러나, state나 props를 dependency로 지정하면, 불필요한 랜더링 발생 가능

- class component의 life cycle 함수(side effect)를 function component에도 동일하게 사용가능
- 최초 컴포넌트 마운트 되는 경우, 컴포넌트 내 레이아웃 배치와 랜더링이 완료된 후에 실행
- 두 번째 인자(배열)의 요소로 지정하면, 해당 요소 값의 업데이트 되는 경우에만 실행
- **그러나, `state나 props를 dependency로 지정하면, 불필요한 랜더링 발생 가능`**

## useCallback

```jsx
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

- **`memoization 된 콜백(함수) 자체를 반환`**
- **`useCallback(fn, deps)`은 `useMemo(() => fn, deps)`** 은 동일
- 의존성이 변경되는 경우, 이전에 기억하고 있던 함수 자체와 비교해서 다른 경우에만 리랜더

## useMemo

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

- **`memoization 된 값을 반환`**
- 의존성이 변경되는 경우, 이전에 기억하고 있던 리턴 값과 비교해서 다른 경우에만 리랜더
- useMemo에서 전달된 함수는 랜더링 중에 실행되므로, 랜더링 중에서 실행하지 않는 함수는 useEffect를 사용할 것
- useRef와의 차이는, useRef는 DOM element의 특정 속성 값을 기억한다면, useMemo는 특정 함수의 리턴 값을 기억하는 것

---

<br />

# Redux와 Mobx에서 차이점 중 불변성에 대해서 설명

### **Redux vs MobX** [상태 관리 라이브러리의 미학: Redux 또는 MobX 를 통한 상태 관리](https://velopert.com/3707)

    정말 어려운 질문이라고 생각합니다. 일단 사용률만 따지면 리덕스가 훨씬 높긴합니다. 
    그렇다고 해서 여러분들이 리덕스를 사용해야하는 것은 아닙니다. 저는 리덕스를 먼저 사용했고,
    MobX 는 나중에 가서 배웠는데 늦게 접한 것에 대해서 조금 후회했습니다. 왜냐하면 생각보다 너무 편했고 재미있었기 때문이죠.
    이 두 라이브러리는 위에서 언급했던 두가지 사항들을 충분히 만족합니다.
    하지만, 그 둘의 작동방식과, 추구하고자 하는 방향과, 개발 방식이 크게 다릅니다.
    

**`Redux`** 는 마치 상태관리의 교과서 같습니다. 그리고 매우 리액트스럽습니다. **`리액트 컴포넌트에서 동적인 상태를 관리 할 땐 state 에 담고 이를 수정할땐 꼭 setState 를 사용해줬었고, 또 컴포넌트의 업데이트 최적화를 위하여, 불변성을 꼭 지켜줘야했었죠?`** **`리덕스에서도 마찬가지로 불변성을 필수적으로 따라줘야 합니다`.** 추가적으로 함수형 프로그래밍 패러다임을 따르기 때문에 함수형 프로그래밍에 익숙하지 않은 개발자들은 처음엔 힘들수도 있다고 사람들이 주장하기는 하나 저는 딱히 그렇게 생각하지 않습니다. 단, 액션, 리듀서, 디스패치 등의 새로운 개념을 접하게 되는 것들이 처음엔 어려울 수도 있으나 좋은 설명만 있다면 큰 어려움은 없다고 생각합니다.

[Redux (4) Immutable.js 혹은 Immer.js 를 사용한 더 쉬운 불변성 관리](https://velog.io/@velopert/20180908-1909-%EC%9E%91%EC%84%B1%EB%90%A8-etjltaigd1)

**`MobX`** 는 조금 과장된 표현일수도 있겠지만 리액트에 흑마법을 끼얹은 느낌입니다. 리액트에서 그렇게 불변성을 유지하면서 개발을 해왔는데 **`MobX를 사용하고나면 불변성은 더 이상 신경쓰지 않아도 됩니다.`** 컴포넌트 업데이트 최적화는 컴포넌트 단위를 최대한 작게 만들고, 리스트를 렌더링 할 땐 리스트 내용 외의 값이 props 로 들어가는것을 방지하기만 하는 몇가지 규칙만 따라주면 알아서 최적화가 잘 됩니다. 그리고, 배우기에 굉장히 쉽고 또.. 재밌습니다. 리덕스 + 리액트만 쓰다가 MobX 쓰면 내가 리액트가 아닌 다른 프레임워크를 쓰고 있는게 아닌가 싶을정도로 신선합니다.

---

<br />

# Styled-Component의 장단점을 설명

[[React] CSS in JS 방법론 (feat. Styled-Component)](https://developer-adam.tistory.com/23)

<img width="883" alt="image" src="https://user-images.githubusercontent.com/85790271/153866881-b0f302b7-4a5f-4b60-84a0-54df9cd28164.png">


