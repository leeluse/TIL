---
aliases:
  - 웹팩으로 배우는 번들링
tags:
  - tutorial
---
TypeScript는 JavaScript에 타입 시스템을 추가한 언어다
하지만 브라우저는 TypeScript를 직접 실행할 수 없기 때문에, TypeScript 코드는 반드시 JavaScript로 변환(컴파일)해야 한다

이번 단계에서는 프로젝트에 TypeScript를 적용하고, 웹팩을 사용해 TypeScript 코드를 번들링하는 방법을 배워 보자


### 웹팩이 TypeScript를 이해하게 만드는 법: 로더(Loader)
---
웹팩은 기본적으로 `.js`와 `.json`만 이해할 수 있다
그래서 `.ts`나 `.scss`, `.png` 같은 파일을 처리하려면 [로더](https://frontend-fundamentals.com/bundling/deep-dive/bundling-process/loader.html)라는 도구가 필요하다
로더가 웹팩에게 통역사 역할을 해 주는 것이다

`ts-loader`라는 로더가 TypeScript 파일을 웹팩이 이해할 수 있는 JavaScript로 변환해 준다



### TypeScript 개발 환경 설정하기
---
먼저 TypeScript를 웹팩이 사용할 수 있도록 관련 패키지를 설치해 보자

```
npm install --save-dev typescript ts-loader
```

- `typescript`: TypeScript 언어 자체와 컴파일러를 포함한다
- `ts-loader`: 웹팩이 `.ts` 파일을 읽을 수 있도록 도와주는 로더다


### TypeScript 설정 파일 만들기
---
웹팩 설정 파일로 `webpack.config.js`가 있듯이, TypeScript도 컴파일러에게 코드를 어떻게 처리할지 알려주는 설정 파일이 있다

루트 폴더에 다음과 같이 `tsconfig.json` 파일을 만들자

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "esnext",
    "strict": true,
    "skipLibCheck": true,
    "moduleResolution": "node"
  },
  "include": ["./**/*.ts"],
  "exclude": ["node_modules", "dist"]
}
```


### 웹팩에 로더 설정 추가하기
---
이제 웹팩에게 `.ts` 파일을 어떻게 처리할지 알려줄 차례다
`ts-loader`는 TypeScript 파일을 JavaScript로 변환할 때 아까 만들었던 `tsconfig.json`의 설정을 참고한다

`webpack.config.js`를 다음과 같이 수정해 주자

```json
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './main.ts', // 웹팩이 읽기 시작할 파일을 .ts로 변경했어요.
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.ts$/, // .ts 파일들은
        use: 'ts-loader', // ts-loader를 거쳐 처리돼요.
        exclude: /node_modules/ // 외부 모듈은 제외해요.
      }
    ]
  },
  resolve: {
    extensions: ['.ts', '.js'] // 파일을 import할 때 확장자를 생략할 수 있어요. TypeScript와 JavaScript를 혼용하는 프로젝트에서 설정해두면 좋아요.
  }
};
```



### JavaScript 파일을 TypeScript로 변환하기
---
#### `emoji.ts`로 바꾸기

```ts
export interface Emoji {
  icon: string;
  name: string;
}

export const emojis: Emoji[] = [
  { icon: '😊', name: 'Smiling Face' },
  { icon: '🚀', name: 'Rocket' },
  { icon: '🍕', name: 'Pizza' },
  { icon: '🐱', name: 'Cat' },
  { icon: '🌈', name: 'Rainbow' },
  { icon: '🎸', name: 'Guitar' }
];
```

`interface Emoji`를 선언해서 이모지 데이터 구조를 명확하게 만들었다
이렇게 해두면 실수로 잘못된 형태의 데이터를 넣는 걸 막을 수 있다

#### `main.ts`로 바꾸기

```ts
import { emojis } from './emoji'; // webpack.config.js의 resolve설정 덕에 확장자 없이 import할 수 있어요.
import { format } from 'date-fns';

document.addEventListener('DOMContentLoaded', function() {
  const today = new Date();
  const formattedDate = format(today, 'MMMM d, yyyy');
  document.getElementById('dateDisplay')!.textContent = formattedDate; // 타입 문제를 임시로 해결해요

  showRandomEmoji();
});

function showRandomEmoji() {
  const randomIndex = Math.floor(Math.random() * emojis.length);
  const selectedEmoji = emojis[randomIndex];

  document.getElementById('emojiDisplay')!.textContent = selectedEmoji.icon; // 타입 문제를 임시로 해결해요
  document.getElementById('emojiName')!.textContent = selectedEmoji.name; // 타입 문제를 임시로 해결해요
}
```



### TypeScript 빌드하기
---

```
npm run build
```


이제 우리 프로젝트는 타입 안정성을 갖추게 됐다

`index.html` 파일을 브라우저에서 열면 우리가 코드를 TypeScript로 변환했지만, 브라우저에서 정상적으로 작동하는 것을 확인할 수 있다 👏



### 관련
---
- [[웹팩으로 배우는 번들링]]
- https://frontend-fundamentals.com/bundling/webpack-tutorial/typescript.html