---
tags:
  - notes
---

---

버전 관리 체계는 major, minor, patch로 구성되어 있다.

```jsx
major: 1 // 주 버전으로 주요 변경사항이나 업그레이드
minor: 2 // 부 버전으로 새로운 기능의 도입 또는 기존 기능 개선(기존 호환성 유지)
patch: 3 // 패치 버전으로 주로 버그 픽스, 코드 수정 등의 작은 변화
```

- npm 버전 명령어

```bash
// patch 한 단계 올림
npm version patch

// minor 한 단계 올림
npm version minor

// major 한 단계 올림
npm version major

// 직접 버전 변경
npm version [VERSION] 
```

## 연결
---
- [[Npm에 라이브러리 배포하기]]
- [[package.json]]
