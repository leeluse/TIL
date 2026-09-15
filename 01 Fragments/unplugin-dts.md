---
tags:
  - fragments
aliases:
  - npm
---

### unplugin-dts란?
---
`unplugin-dts`는 `.ts`, `.tsx` 소스에서 `.d.ts` 파일을 생성하는 플러그인이다

기존에 많이 사용되던 `vite-plugin-dts`에서 발전한 프로젝트이며, 현재 `vite-plugin-dts` 자체에서도 신규 프로젝트에는 `unplugin-dts` 사용을 권장하고 있다



### 왜 Vite build만으로 `.d.ts`가 만들어지지 않을까?
---
Vite는 기본적으로 TypeScript 코드를 JavaScript로 **변환**하지만 TypeScript 타입 선언 파일을 생성하는 TypeScript 컴파일러 역할까지 수행하지는 않는다.

즉 Vite의 기본 역할은 다음과 가깝다.

```
Button.tsx
   │
   │ Vite Build
   ▼
JavaScript
```

하지만 라이브러리에서는 추가로 다음 과정이 필요하다.

```
Button.tsx
   │
   ├──────────────→ JavaScript
   │
   └──────────────→ Type Declaration
                       │
                       ▼
                    Button.d.ts
```

따라서 Library Build에서 타입 선언을 생성하려면 TypeScript declaration 생성 도구를 추가해야 한다.



## 연결
---
- [[Npm에 라이브러리 배포하기]]
