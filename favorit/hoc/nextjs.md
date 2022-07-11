# NEXTJS HOC SSR PROPS

```js
import axios from "axios";
import { GetServerSideProps, GetServerSidePropsContext } from "next";

export const withHOC = (server: GetServerSideProps) => {
  return async (ctx: GetServerSidePropsContext) => {
    const { data } = await axios.get(
      "https://jsonplaceholder.typicode.com/posts"
    );

    const { props }: { [key: string]: any } = await server(ctx);

    return {
      props: {
        ...props,
        post: data,
      },
    };
  };
};
```
