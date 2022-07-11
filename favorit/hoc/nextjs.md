# NEXTJS HOC SSR PROPS

![code](https://user-images.githubusercontent.com/85790271/178291959-3647696b-70f3-4393-b6da-0a9699b8d2b7.png)


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
