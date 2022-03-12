# Constants

**개발과 배포** [Link](https://ko.reactjs.org/docs/codebase-overview.html#development-and-production)

> 의사 전역 변수 **DEV**를 사용하여 개발 시에만 작동하는 코드를 작성할 수 있습니다.

해당 변수는 컴파일 단계에서 한번에 처리되며, CommonJS 빌드 시에 process.env.NODE_ENV !== 'production'로 변환됩니다.

```javascript
if (__DEV__) {
  // This code will only run in development.
}
```

<br />
