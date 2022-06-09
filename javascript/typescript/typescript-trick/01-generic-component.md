# Generic Component

    데이터 타입에 따라 유연한 Props Type을 가진 컴포넌트 구성하기

```js
import React, { ReactNode } from "react";

interface TableProps {
  items: TItem[];
  renderItem: (item: TItem) => ReactNode;
}

export const Table = <TItem,>() => {
  return null;
};

export const Component = () => {
  return (
      <Table
        items={[{id: "1"}]}
        renderItem={(item) => {
          // 제네릭을 이용해 Items Props의 타입을 추론하여 값을 사용한다.
          // item.id
          return null;
        }}
      >
      ...
      </Table>;
  )
};
```
