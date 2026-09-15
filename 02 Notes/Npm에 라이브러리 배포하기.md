---
tags:
  - notes
aliases:
  - npm
---

## Vite 설정 변경하기

---

일반적으로 React + Vite는 웹 어플리케이션을 실행하고 배포하는 것을 목적으로 구성되어 있기 때문에

vite build를 실행할 경우 index.html을 기준으로 전체를 빌드하게 된다

```jsx
index.html → src/main.tsx → src/App.tsx → components
```

컴포넌트 라이브러리를 목적으로 배포하기 위해서는 라이브러리를 사용하는 다른 프로젝트가 필요한 컴포넌트를 가져가서 사용 가능해야 한다

따라서 빌드 시작점이 `index.html` 또는 `main.tsx`가 아닌 라이브러리가 외부에 공개할 모듈이 되어야 한다

**Vite**에서는 이를 위해 [[Vite Library Mode|Library Mode]]를 제공하며 `build.lib` 옵션을 사용한다

두 방식의 가장 큰 차이는 **빌드 결과물의 사용자**다

|구분|Application|Component Library|
|---|---|---|
|목적|브라우저에서 실행|다른 프로젝트에서 import|
|Entry|`index.html`, `main.tsx`|`src/index.ts`|
|결과물|완성된 웹 애플리케이션|JS / CSS 모듈|
|React 포함|일반적으로 포함|일반적으로 제외|
|사용 방법|URL 접속|`import { Button } ...`|

애플리케이션에서는 다음 코드가 실행의 시작점이다

```tsx
// src/main.tsx

import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

import App from './App';

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <App />
  </StrictMode>,
);
```

하지만 컴포넌트 라이브러리에서는 `createRoot()`를 실행할 필요가 없으며 대신 라이브러리에서 제공할 컴포넌트를 **export 하는 파일**이 필요하다

### Library Entry 생성

---

`Public Entry Point` 역할을 하는 `src/index.ts` 파일을 생성한다

```jsx
src/
 ├─ components/
 │ ├─ Button/ 
 │ ├─ Input/ 
 │ ├─ Badge/ 
 │ └─ ... 
 │ └─ index.ts
```

```jsx
export { default as Button } from './components/Button/Button';
export { default as Input } from './components/Input/Input';
export { default as Badge } from './components/Badge/Badge';
...
```

이렇게 만들어 두면 라이브러리를 설치한 프로젝트에서는 내부 디렉터리 구조를 알 필요 없이 다음처럼 사용 가능하다

```jsx
import { Button, Input, Badge } from '라이브러리'
```

### vite.config.ts를 Library Mode로 변경하기

---

초기 vite 설정은 React 애플리케이션을 실행하기 위한 기본적인 Vite 설정만 존재하기에 `build.lib` 설정을 추가한다

```jsx
export default defineConfig({
  plugins: [react()],
  // -------- build.lib 설정 ----------
  build: {
    lib: {
      // 라이브러리 빌드의 시작점
      entry: resolve(import.meta.dirname, 'src/index.tsx'),
      // 라이브러리를 어떤 JavaScript 모듈 형식으로 출력할지 지정
      formats: ['es', 'cjs'],
      // 빌드 후 생성되는 JavaScript 파일의 이름을 지정
      fileName: (format) => format === 'es' ? 'index.js' : 'index.cjs',
      // 빌드 결과물에 CSS 파일이 함께 생성
      cssFileName: 'style',
    }
  },
  // ----------------------------------
  resolve: {
    // path alias 추가
    alias: {
      '@': path.resolve(import.meta.dirname, './src'),
    },
  },
})
```


빌드 후 생성되는 결과물은 아래와 같이 나오게 된다

```jsx
dist/ 
├─ index.js  // ES Module
├─ index.cjs  // CommonJS
└─ style.css  // 컴포넌트 스타일
```

Vite Library Mode는 `es`, `cjs`, `umd`, `iife` 형식을 지원하며 필요한 형식은 `formats`를 통해 지정할 수 있다
출력 형식은 ES Module와 CommonJS 두 가지를 지원한다 ([[ES Module vs CommonJS]])





이 파일들은 이후 [[package.json]]의 [[package exports|exports]]와 연결된다

**❓React를 라이브러리에 포함시키면 안 되는 이유?**
	현재 상태에서 컴포넌트 라이브러리를 빌드하면 컴포넌트가 사용하는 React 관련 코드까지 번들에 포함될 가능성이 있다
```jsx
Application 
├─ react 
└─ @torch/ui
 └─ react
```
	만약 라이브러리를 사용하는 프로젝트 내에서도 React를 설치하였을 경우 바람직하지 않은 구조가 될 것이다



### React를 External Dependency로 설정하기

---

최신 Vite에서는 build.rolldownOptions를 제공하는데, 이를 통해서 ‘React를 우리 라이브러리 내부에 넣지 마라’고 설정 가능하다

```jsx
export default defineConfig({
  plugins: [react()],
  build: {
    ...
    rolldownOptions: {
      external: [ // React 등 외부 dependency를 번들에서 제외
        'react',
        'react-dom',
        'react/jsx-runtime'
      ]
    }
  },
 ...
})

```

만약 우리가 만든 컴포넌트 내부에서 React의 useState 훅을 사용하고 있다고 생각해 보자

```jsx
import { useState } from 'react'
```

이런 코드가 있다고 해도 React 자체를 dist/index.js 안에 복사해서 넣지 않는다는 의미이다

대신 최종 코드에 React를 외부 dependency로 사용하는 관계를 유지하도록 한다

## Package.json 설정하기

---

1. **private 변경 처리**

```json
{ "private": false, }
```

`private`은 npm publish 자체를 막을 것인지 결정한다

1. **version**

```json
{ "version": "0.0.0" }
```

`version`은 현재 배포하는 라이브러리의 버전을 의미한다.
- 구체적인 SemVer(major, minor, patch) 체계: [[Npm 버전 관리]] 


1. **type**

```json
{ "type": "module" }
```

이 설정은 `.js` 파일을 **ES Module로 해석한다**는 의미한다

1. **main & module**

```json
{ "main": "./dist/index.cjs" }
```

- `main:` 패키지의 기본 진입점을 지정하는 전통적인 설정이다
- `module:`ES Module 형식의 패키지 진입점을 번들러에게 알려주는 용도이다

1. **types**

```json
{ "types": "./dist/index.d.ts" }
```

JavaScript 파일만 배포한다면 라이브러리는 실행할 수 있지만 TypeScript는 해당 컴포넌트가 어떤 타입을 가지고 있는지 알 수 없다

빌드 과정에서 타입 선언 파일을 생성하면 다음과 같은 결과물이 만들어진다

```jsx
dist/ 
└─ index.d.ts // 이 라이브러리의 타입 정보는 dist/index.d.ts에
```

1. **files**

```json
{ "files": [ "dist" ] }
```

`files`는 **npm 패키지에 어떤 파일을 포함할 것인가**를 지정한

npm의 `files` 필드는 실제 패키지 tarball에 들어갈 파일과 디렉터리를 제한한다  
`files`를 지정하지 않으면 기본적으로 훨씬 넓은 파일 집합이 배포 대상이 될 수 있다

1. **exports**

```json
  "exports": {
    ".": {
      "import": "./dist/index.js",
      "require": "./dist/index.cjs"
    },
    "./style.css": "./dist/style.css"
  },
```

`exports`는 이 라이브러리에서 **외부에 공개할 진입점**을 정의한다 (쉽게 말하면 패키지의 Public API)

- **import**: ES Module 방식으로 라이브러리를 가져올 경우 사용할 파일
- **require**: CommonJS 방식으로 라이브러리를 가져올 경우 사용할 파일

이렇게 하나의 라이브러리가 두 가지 환경에서 사용하도록 제공하는 것을 `Conditional Exports`라고 한다

## [[unplugin-dts]] 플러그인 설치

---
개발 의존성으로 unplugin-dts를 설치한 후 vite.config.ts의 plugins에 dts를 추가한다

```jsx
import dts from 'unplugin-dts/vite'

...
plugins: [
    react(),
    dts({ 
      tsconfigPath: './tsconfig.app.json',
      include: ['src'], 
      exclude: ['src/**/*.stories.ts', 'src/**/*.stories.tsx']
     })
  ],
```

Vite의 기본 React + TypeScript 템플릿을 사용하고 있다면 다음처럼 TypeScript 설정이 분리되어 있을 수 있다.

```
tsconfig.json
tsconfig.app.json
tsconfig.node.json
```

이 경우 `unplugin-dts`에서도 실제 애플리케이션 TypeScript 설정을 명시해주는 편이 안전하다.


### Npm에 패키지 배포하기

---

1. npm 로그인
    
    ```jsx
    npm login
    ```
    
2. 명령어 배포
    
    ```jsx
    npm publish --access public
    ```
    

![[Pasted image 20260914160424.png]]

### Reference

---

[https://choewy.tistory.com/168#google_vignette](https://choewy.tistory.com/168#google_vignette)

## 연결

---

- [[Npm 버전 관리]]
- [[Vite Library Mode]]
- [[package exports]]
- [[package.json]]
- [[unplugin-dts]]