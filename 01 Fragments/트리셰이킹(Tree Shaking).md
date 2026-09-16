---
aliases:
tags:
  - fragments
  - 번들링
  - toss-article
---

### 트리셰이킹이란?
---
트리 셰이킹은 프로젝트 내에서 사용되지 않는 코드를 제거하는 최적화하는 기법이다

마치 나무를 흔들어 불필요한 (예를 들어 죽은 나뭇잎)을 떨어뜨리듯, 실제로 사용되지 않고 있는 코드(일명 `Dead Code`)가 번들 파일에 포함되지 않도록 한다

- **예를 들어 ...**
라이브러리에서 특정 함수 하나만 사용했다고 하자
그럼에도 전체 코드가 번들에 포함돼 파일 크기가 불필요하게 커지는 문제가 발생할 수 있다
이럴 경우 트리셰이킹을 적용하면 실제로 사용하는 코드만 번들에 남기기 때문에 번들 크기를 줄일 수 있다

번들 크기가 줄어들면 어플리케이션의 로딩 속도가 빨라지고 사용자 경험도 개선 가능하다

<br />
### 트리셰이킹이 동작하는 환경
---
트리세이킹은 **정적 분석(Static Analysis) 기반**으로 작동한다

> **정적 분석(Static Analysis)이란?**
> 정적 분석은 코드가 실행되기 전에 구조를 분석해서 사용되지 않는 코드를 정확히 찾아낼 수 있는 기법이다

*따라서 트리셰이킹은 `코드를 분석하고 번들링하는 빌드 타임에 적용된다`*


트리셰이킹이 잘 동작하려면, **번들러가 모듈 간의 관계를 명확하게 분석할 수 있도록 모듈**이 구성되어 있어야 한다

- **자바스크립트의 모듈 시스템**
	자바스크립트의 모듈 시스템에는 [[ESM과 CJS]] 두 가지 방식이 있다
	 

> **트리셰이킹이 EMS에서 효과적인 이유?**
> `ESM`: 정적인 구조를 가지기 때문에 빌드 타임에 분석 가능하고 트리셰이킹이 효과적으로 적용 
> 	- 자세한 내용은 [[ESM과 CJS]] 참고


<br />

## 사이드 이펙트가 없는 코드 제거
---
사이드 이펙트(Side-Effect)는 코드가 예상치 못한 방식으로 애플리케이션의 동작에 부작용을 줄 수 있는 가능성을 의미한다

> 즉, 사이드 이펙트가 없는 코드란 **번들링된 코드가 실행될 때 동작에 영향을 주지 않는 코드**다


#### 사이드 이펙트가 존재하는 코드
---
**예시 1**. 호출될 때 외부 상태를 변경하는 함수

```js
let count = 0;

function incrementCount() {
  count = count + 1; // 함수가 호출될 때마다 전역 변수 값이 변경됨 (사이드 이펙트 발생)
}

incrementCount();
```

**예시 2**. 직접적으로 DOM 변경

```js
function updateDOM() {
  document.body.innerHTML = "<h1>Hi Toss!</h1>"; // DOM이 변경됨
}
```


**예시 3**. 조회를 할 때마다 다른 결과 반환

```js
const user = {};

// Object.defineProperty를 이용한 속성 조작
Object.defineProperty(user, "name", {
  get() {
    console.log("이름이 뭐예요?");
    this._name = this._name ? this._name + "!" : "Hany"; // 값을 변경하는 부작용 발생
    return this._name;
  }
});

console.log(user.name); // "이름이 뭐에요?" 출력 후 "Hany"
console.log(user.name); // "이름이 뭐에요?" 출력 후 "Hany!"
console.log(user.name); // "이름이 뭐에요?" 출력 후 "Hany!!"
```



#### 사이드 이펙트가 없는 코드
---
**예시 1**. 순수함수: 외부 변수나 전역 상태를 변경하지 않고, 입력값에 따라 항상 동일한 결과 반환

```js
function add(a, b) {
  return a + b;
}

const result = add(2, 3);
console.log(result);
```

**예시 2**. 조회 시 동일한 결과를 반환

```js
const user = {
  _name: "Hany",
  get name() {
    console.log("이름이 뭐예요?");
    return this._name; // 값을 변경하지 않고 그대로 반환
  }
};

console.log(user.name); // "이름이 뭐예요?" 출력 후 "Hany"
console.log(user.name); // "이름이 뭐예요?" 출력 후 "Hany"
console.log(user.name); // "이름이 뭐예요?" 출력 후 "Hany"
```


**예시 3**. 원본 데이터를 변경하지 않고 새로운 값을 반환하는 내장 함수

```js
arr.slice(1);
arr.map((num) => num * 2);
arr.filter((num) => num > 1);

str.toUpperCase();
str.repeat(3);

Math.floor(4.8);
Math.abs(-10);
```


이처럼 사이드 이펙트가 없는 코드는 번들러가 안전하다고 판단하면 최종 번들에서 제거된다


<br />

### 트리셰이킹 최적화를 위한 추가 설정
---
실제로 작성하는 코드에는 사이드 이펙트가 포함될 때가 많다
번들러가 올바르게 처리할 수 있도록, 개발자가 직접 정보를 제공하거나 번들러가 자동으로 최적화를 수행할 수도 있다

#### 1. 주석 설정 (`/* @__PURE__ */`)

**`/* @__PURE__ */`** 주석은 이 코드가 실행되더라도 사이드 이펙트가 없다는 것을 번들러에게 명시적으로 알리는 역할을 한다. 즉, 외부 상태에 영향을 주지 않는다고 단언하는 것이다

트리셰이킹 최적화를 위해 번들러가 번들링 과정에서 자동으로 추가할 수도 있고, 개발자가 직접 명시적으로 추가할 수도 있다

다음과 같이 `/* @__PURE__ */` 주석이 포함된 코드를 번들링하면, 번들러는 해당 코드가 사이드 이펙트가 없다고 판단할 수 있다

```jsx
const Icon = /* @__PURE__ */ React.createElement(...);
```

그 결과, 최적화 과정에서 필요하지 않은 경우 아래처럼 제거될 수 있다

```jsx
const Icon = /* @__PURE__ */ React.createElement(...);
```


#### 2. sideEffect 필드 활용

`package.json` 파일의 `sideEffects` 필드는 특정 파일이나 코드가 번들링 과정에서 제거되지 않도록 번들러에 알려주는 역할을 한다

<br />

- **모든 파일에 사이드 이펙트가 없다고 선언하기**

```js
// package.json
{
  "sideEffects": false
}
```

이렇게 설정하면, 번들러는 사용되지 않는 모든 파일을 안전하게 제거할 수 있다

<br />

- **특정 파일이나 디렉토리를 제거하지 않도록 설정하기**

```js
// package.json
{
  "sideEffects": ["*.css", "./src/global.js"]
}
```

이 설정은 CSS 파일과 특정 자바스크립트 파일이 제거되지 않도록 명시하는 방식이다

예를 들어, `global.js` 파일이 전역 변수를 설정하거나 애플리케이션의 초기화를 담당하는 경우, 트리셰이킹 과정에서 실수로 제거되지 않도록 보호할 수 있다

이렇게 필요한 파일을 지정하면, 트리셰이킹의 효과를 유지하면서도 필수적인 코드가 번들에서 빠지는 문제를 방지할 수 있다

이로써 빌드 성능을 최적화할 수 있다!

<br />

## 번들러 세팅 가이드
---
트리셰이킹으로 사용하지 않는 코드를 제거하더라도, 빌드 결과물에는 여전히 불필요한 공백, 주석, 최적화되지 않은 표현 등이 남아 있을 수 있다

==프로덕션 빌드에서는 이 잔여 요소를 압축(minify)해 코드 크기를 추가로 줄여야 최종 번들의 성능을 극대화할 수 있다==

- **설치 방법**

```
npm install --save-dev terser-webpack-plugin
```

- **설정 예시**

```js
// webpack.config.js
const TerserPlugin = require("terser-webpack-plugin");

module.exports = {
  optimization: {
    minimize: true,
    minimizer: [new TerserPlugin()]
  }
};
```

```js
// vite.config.js
import { defineConfig } from "vite";

export default defineConfig({
  build: {
    minify: "esbuild"
  }
});
```



<br />



## 관련
---
- [[ESM과 CJS]]
- https://frontend-fundamentals.com/bundling/deep-dive/optimization/tree-shaking.html