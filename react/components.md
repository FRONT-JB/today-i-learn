# [컴포넌트의 추상화](https://kwoncheol.me/posts/break-the-component)

🔖 **`컴포넌트의 추상화는 어느 정도 수준으로 진행해야 적절하며, 확장성은 어느 정도를 고려해야 알맞은 가`**

    ❗ 소감 3줄 요약

\- 유연함을 지키는 컴포넌트 개발이 맞을까? 견고함을 지키는 컴포넌트 개발이 맞을까?

\- 우리의 컴포넌트는 자이언트 컴포넌트인가?

\- 잘못된 추상화를 어떻게 개선할 수 있을까?

<br />

    😃 블로그에서 기억하고 싶은 내용을 써보세요.

## [ 단단한 컴포넌트 부수기 ]

    잘못된 추상화
    - 추상화가 잘못된 컴포넌트는 시간이 지날수록 잘못된 방향으로 진화되고 결국 관리가 어려워져 쓰이지 않게 된다.

**`props가 많아지는 경우 발생하는 문제`**

\- 각 props가 어떤 역할을 하는지 파악하기 어려워진다.

\- 파악하기 어려운 props를 설명해주기 위한 주석이나 문서 작성 및 관리 필요

\- 요구사항이 복잡해질수록 기괴한 props명이 나올 확률 ↑ 작명 센스 필요

\- 위와 같은 이유들로 인해 컴포넌트를 변경하기가 어렵고 두려워진다.

<br />

**`비즈니스 로직이 컴포넌트 안에 들어있다.`**

\- 버튼 개수나 위치, 버튼의 배열, 일러스트의 위치, 이 모든 것들은 비즈니스 로직이다.

\- 우리는 비즈니스 로직을 밖으로 꺼내어야 한다.

<br />

**`리액트는 상속보다는 조합 `**

\- 하나의 큰덩어리로 컴포넌트를 구성하지 않고 조합하여 사용해야 한다.

```js
// 자이언트 컴포넌트
<Dialog
  iconAboveTitle="fancy-icon"
  title="안내"
  description="이것은 멋진 내용을 담고 있는 안내입니다."
  buttonPosition="bottom"
  buttonAlign="vertical"
  buttons={[{
    label: '확인',
    onClick: doSomething,
    type: 'cta',
  }, {
    label: '취소',
    onClick: doSomethingElse,
    type: 'secondary',
  },]}
/>


// 조합기반 컴포넌트
<Dialog>
  <Dialog.Icon type="fancy" />
  <Dialog.Content
    title="안내"
    description="이것은 멋진 내용을 담고 있는 안내입니다."
  />
  <Dialog.ButtonContainer align="vertical">
    <Dialog.Button type="secondary" onClick={doSomethingElse}>
      취소
    </Dialog.Button>
    <Dialog.Button type="primary" onClick={doSomething}>
      확인
    </Dialog.Button>
  </Dialog.ButtonContainer>
</Dialog>

```

    조합을 이용한 다이얼로그는 onClick, align, title 등 명확한 props만 남게 되기 때문에
    개발자가 각 props가 어떤 역할을 하는지 파악하기 수월하고 props가 명확하다.
    모호한 props가 없기 때문에 작명 고민을 할 필요도 없다.
    따라서 컴포넌트 명세를 변경해야할 때 어디를 고쳐야할지도 직관적이다.

<br />
