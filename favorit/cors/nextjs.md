# NEXTJS CORS

    NEXTJS에서 CORS 오류가 발생할 경우
    next.config.js에서 도메인을 서버로 변경하면 CORS 에러가 발생하지 않는다.

```js
// next.config.js
{
	async rewrites() {
    return [
      {
        source: `/변경할URL/:path*`,
        destination: `원본URL/:path*`
      },
    ]
  }
}
```
