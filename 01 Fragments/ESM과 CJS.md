---
tags:
  - fragments
  - 번들링
---
## ESM
---
**ESM**은 `import`와 `export` 구문으로 모듈 간의 관계를 분석해 [[의존성 그래프]]를 만든다
(의존성 그래프로 번들러가 불필요한 코드를 쉽게 판단하고 제거할 수 있다)
이러한 특성으로 ESM에서는 불필요한 코드를 쉽게 찾아 제거할 수 있는 것이다

-  **`import`한 모듈은 다른 값으로 재할당 불가능하다**
	- **ESM**의 `import`는 읽기 전용(immutable)이기 때문에 모듈을 재할당할 수 없다
	  
	  ```js
	  import { math } from "./math.js";
		math = {}; // Error
	  ```
	  
	<br/>
	
-  **`import` 및 `export`  구문은 항상 파일의 최상단에 위치해야 한다**
	-  `import` 및 `export` 가 코드가 실행되기 전에 정적으로 분석되므로, 실행 도중 동적으로 평가될 수 없다
		따라서 조건문 안에서  `import`를 사용할 수 없으며 항상 최상단에 위치해야 한다
		  
		  ```js
		if (condition) {
			  import { func } from "./module.js"; // Error
		}
		  ```
		
	<br />
	
-  ESM은 `import()` 구문을 지원해서 ==필요한 시점에 모듈을 동적==으로 불러, 이를 통해 초기 번들 크기를 줄일 수 있다
		  
	  ```js
	async function loadUtils() {
	  const { deepEqual } = await import("lodash-es");
	  console.log(deepEqual(a, b));
	}
	  ```
		


<br />

## CJS
---
**CJS**는 `equire`를 사용해 ==항상 동기 방식==으로 모듈을 불러온다
즉, 코드가 실행될 때 즉시 해당 모듈을 불러야 하고 비동기 로딩은 지원하지 않는다

<br />

#### CJS의 동작 예측이 어려운 CASE
---
##### 1. 함수나 조건문 안에서 동적으로 모듈을 로드할 때

다음 코드처럼 `require`나 `import` 같은 모듈 로드를 **함수나 조건문 안에서 동적으로 사용할 때**, 번들러는 코드 실행 전에는 정확히 어떤 모듈이 로드될지 알 수 없다

그래서 번들러가 전체 의존성을 미리 파악하거나 최적화하기 어려워진다

```js
	let foo;
	if (SOME_CONDITION) {
	  foo = require("something");
	} else {
	  foo = require("something_else");
	}
```

##### 2. 몽키 패칭 등으로 예상하지 못한 동작이 생길 때

[[몽키 패칭]]은 이미 존재하는 모듈이나 함수의 동작을 런타임 중에 덮어써서 원하는 대로 바꾸는 기법이다

이 경우도 마찬가지로, 번들러 입장에서는 코드가 실행되기 전에는 어떤 모듈이, 어떤 방식으로 변경될지 알 수 없기에 결과적으로 번들러는 코드 분석이 어려워지고, 예상하지 못한 동작이나 오류가 발생할 수 있다


<br />

### ESM 기반의 라이브러리를 사용해야 하는 이유
---
라이브러리에서 필요한 기능만 가져오더라도, 모듈 시스템이나 번들 설정이 제대로 되어 있지 않으면 전체 라이브러리가 포함돼 번들 크기가 커질 수 있다

예를 들어, `lodash` 라이브러리에서 `deepEqual` 함수 하나만 사용한다고 해보자

```
import { deepEqual } from "lodash";
```

**하지만 `lodash`는 CJS 방식으로 작성돼 트리셰이킹이 잘 적용되지 않는다**
결과적으로 `deepEqual` 외에도 `lodash`의 모든 코드가 번들에 포함될 수 있다

이 문제를 해결하려면 `lodash` 대신 **ESM**을 지원하는 `es-toolkit`을 사용해야 해요.

```
import { isEqual } from "es-toolkit";

const result = isEqual(a, b);
```

> `es-toolkit`는 **ESM** 구조를 사용해 필요한 함수만 선택적으로 가져올 수 있고, 트리셰이킹을 사용해 번들 크기를 효과적으로 줄일 수 있다



<br /><br />


ES Module과 CommonJS 차이
---
- `ES Module`: 현대적인 프론트엔드 프로젝트에서 사용하는 방식 Vite, Webpack, Rollup 등 최신 번들러가 지원 
- `CommonJS`: Node.js의 기존 CommonJS 환경이나 일부 도구와 호환성을 위해 제공 가능



관련
---
- [[Npm에 라이브러리 배포하기]]
- [[트리셰이킹(Tree Shaking)]]
- [[몽키 패칭]]
- [[es-toolkit]]
