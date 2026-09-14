---
aliases:
  - npm
tags:
  - notes
---
### Npm은 무엇인가?

---

```jsx
npm
├─ 패키지 설치
├─ 패키지 버전 관리
├─ 의존성 관리
├─ package.json 관리
├─ npm registry에서 패키지 다운로드
└─ package.json의 scripts 실행
```

`npm`은 **Node Package Manager**의 약자로, `JS/Node.js`와 같은 프로젝트에서 외부 라이브러리와 도구를 설치하고 관리하는 [[패키지(Package)]] 매니저이다

React 프로젝트에서 `Axios`를 쓰고 싶다면, `Axios` 코드를 직접 내려 받아 프로젝트에 넣는 대신 `npm` 명령어를 이용해서 설치할 수 있다

```jsx
npm install axios
```

`npm` 명령어를 사용하면 알아서 해당 패키지를 설치하고, 어떤 버전을 사용하는지 기록해 준다




### npm install을 하면 어떤 일이 일어날까?

---

```jsx
npm install axios
```

위 명령어를 실행했을 때 npm의 동작은 아래와 같다

1. npm Registry(패키지가 올라간 저장소)에서 axios를 검색
2. 필요한 버전을 결정
3. axios가 사용하는 다른 패키지도 확인
4. [[node_modules]]에 다운로드
5. [[package.json]]에 axios를 기록
6. [[package-lock.json]]에 정확한 버전을 기록

> **실제 프로젝트 내 폴더 구조**

```jsx
my-project/
├── node_modules/
├── package.json
├── package-lock.json
└── src/
```



## 관련 내용
---
- [[Yarn은 왜 등장했나]]
