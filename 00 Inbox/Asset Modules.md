---
aliases:
  - Webpack
tags:
  - inbox
---
### Asset Modules란?
---
예전에는 이미지나 폰트 같은 정적 자원을 웹팩에서 처리하기 위해 `file-loader`, `url-loader`, `raw-loader` 같은 별도 로더를 설치했다

하지만 `웹팩 5`부터는 이런 작업을 훨씬 쉽게 해주는 기능인 `Asset Modules`가 내장되었다

이제는 따로 로더를 설치하지 않아도 웹팩이 이미지, 폰트, 아이콘 같은 파일을 자동으로 처리하고, 필요하면 압축하거나 `base64` 형태로 변환해서 JavaScript 코드 안에 바로 포함시켜 주기도 한다


### 관련
---
- [[이미지 등 정적 자원 다루기]]