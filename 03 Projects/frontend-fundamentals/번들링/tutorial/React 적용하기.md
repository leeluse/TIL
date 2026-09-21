---
aliases:
  - 웹팩으로 배우는 번들링
tags:
  - 번들링
  - tutorial
---
이번 단계에서는 프로젝트에 `React`를 도입하고, 컴포넌트 기반으로 UI를 재구성해 볼 것이다
React는 JavaScript 라이브러리지만, [[JSX]]라는 특별한 문법을 사용하기 때문에 웹팩의 도움이 필요하다


### React 개발 환경 설정하기
---
먼저 React와 관련 패키지들을 설치해 보자

```bash
$ npm install react react-dom
$ npm install --save-dev @types/react @types/react-dom
```

- `react`: React 코어 라이브러리
- `react-dom`: React를 웹 브라우저에서 사용할 수 있게 해주는 라이브러리
- `@types/react`, `@types/react-dom`: 타입스크립트에서 React를 사용할 때 필요한 타입 정의

### tsconfig.json에 JSX 설정 추가하기
---
타입스크립트가 JSX를 이해할 수 있도록 `tsconfig.json` 파일에 JSX 관련 설정을 추가해야 한다

```json
{
  "compilerOptions": {
    // ... 기존 설정 유지
    "jsx": "react", // JSX를 React 문법으로 변환해요
    "esModuleInterop": true // React를 ESM으로 import할 수 있게 해줘요
  }
}
```


###  웹팩에 바벨 로더 설정 추가하기
---
지금까지는 타입스크립트를 웹팩에서 다룰 때 `ts-loader`를 사용했다
이번엔 React의 JSX 문법도 함께 다뤄야 하기 때문에 [[바벨(Babel)]]을 사용하는 방식으로 바꿔볼 것이다

다음과 같이 도구를 설치하고 웹팩에 연결하자

```bash
$ npm install --save-dev @babel/core babel-loader @babel/preset-env @babel/preset-react @babel/preset-typescript
```

- `@babel/core`: JavaScript 코드를 변환해 주는 도구
- `babel-loader`: 웹팩에서 바벨을 사용할 수 있도록 연결해 주는 역할
- `@babel/preset-react`: 바벨에게 JSX를 어떻게 변환할지 알려주는 설정
- `@babel/preset-typescript`: 바벨에게 타입스크립트를 어떻게 변환할지 알려주는 설정
- `@babel/preset-env`: 최신 JavaScript 문법을 구버전 브라우저에서도 작동하게 변환
	React를 해석하는데 필수는 아니지만, 최신 JavaScript 문법을 쓸 계획이 있다면 넣는 걸 추천해요



그리고 `webpack.config.js` 파일의 `entry`, `module.rules`, `resolve`를 다음과 같이 수정해 주세요.

```js
module.exports = {
  // ... 기존 설정 유지
  entry: "./main.tsx", // 웹팩이 읽기 시작할 파일을 .tsx로 변경했어요.
  module: {
    rules: [
      {
        test: /\.(ts|tsx)$/, // .ts와 .tsx 파일을 대상으로
        use: [
          {
            loader: "babel-loader",
            options: {
              presets: [
                "@babel/preset-env", // 최신 JS 문법을 변환해요
                "@babel/preset-react", // JSX를 변환해요
                "@babel/preset-typescript" // 타입스크립트를 변환해요
              ]
            }
          }
        ],
        exclude: /node_modules/  // 외부 모듈은 제외해요.
      }
    ]
  },
  resolve: {
    extensions: [".tsx", ".ts", ".js"] // .tsx 확장자도 처리할 수 있게 해요
  }
};
```



### HTML을 React 컴포넌트로 변환하기
---
이제 HTML을 React 컴포넌트로 변환하기 위해 먼저 `index.html`을 수정하자

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Emoji of the Day</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="./style.css">
</head>
<body>
  <!-- 기존 HTML을 모두 잘라냈어요 -->
  <div id="root"></div>
  <script src="./dist/bundle.js"></script>
</body>
</html>
```

그리고 `App.tsx` 컴포넌트를 만든다

```tsx
import React from "react";
import { emojis } from "./emoji";
import { format } from "date-fns";

const App = () => {
  const [selectedEmoji, setSelectedEmoji] = React.useState(emojis[0]);

  // main.ts에 있던 showRandomEmoji 함수를 가져오되, React 상태에 저장하도록 수정했어요
  const showRandomEmoji = () => {
    const randomIndex = Math.floor(Math.random() * emojis.length);
    setSelectedEmoji(emojis[randomIndex]);
  };

  return (
    <div className="container">
      <img src="./assets/logo.svg" alt="Logo" className="logo"></img>
      <h1>Emoji of the Day</h1>
      <div className="date-display">{format(new Date(), "MMMM d, yyyy")}</div>
      <div className="emoji-container">
        <div className="emoji">{selectedEmoji.icon}</div>
        <div className="emoji-name">{selectedEmoji.name}</div>
        {/* 다른 이모지 보기 기능을 추가했어요 */}
        <button onClick={showRandomEmoji}>See other emoji</button>
      </div>
    </div>
  );
};

export default App;
```

마지막으로 `main.ts`파일 이름을 `main.tsx`로 변경하고, `App.tsx`에 만들었던 React 앱을 그리도록 수정해 준다

```tsx
import React from "react";
import { createRoot } from "react-dom/client";
import App from "./App";

createRoot(document.getElementById("root")!).render(<App />);
```



###  React 앱 빌드하기
---
이제 코드를 빌드한다

```
npm run build
```

`index.html` 파일을 브라우저에서 열었을 때 'See other emoji' 버튼이 추가되고, 잘 동작한다면 이제 우리 프로젝트는 React 컴포넌트로 구성된 앱이 된 거다!


### 관련
---
- [[이미지 등 정적 자원 다루기|웹팩으로 배우는 번들링]]
- https://frontend-fundamentals.com/bundling/webpack-tutorial/react.html
- [[바벨(Babel)]]
- [[JSX]]
