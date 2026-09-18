---
tags:
  - inbox
---
### JSX란?
---
React는 JSX라는 특별한 문법을 사용한다
JSX는 JavaScript 안에 HTML과 비슷한 문법을 쓸 수 있게 해주는 문법이다
하지만 브라우저는 JSX를 이해하지 못하기 때문에, 이를 일반 JavaScript로 변환해야 한다

``` tsx
// JSX 문법
const element = <h1>Hello, {name}!</h1>;

// 변환된 JavaScript
const element = React.createElement("h1", null, "Hello, ", name, "!");
```

