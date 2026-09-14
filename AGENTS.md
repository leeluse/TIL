# My Knowledge Vault

개발하면서 알게 된 개념, 문제 해결 과정, 프로젝트에서의 판단을 기록하는 개인 Knowledge Vault.

이 Vault의 목적은 지식을 완벽하게 분류하는 것이 아니라,
**개발하다가 발견한 내용을 빠르게 기록하고 서로 연결하는 것**이다.

기술별 폴더 분류보다 `[[wikilink]]`를 통한 지식 연결을 우선한다.

---

## Structure

```text
My-Knowledge-Vault/
│
├── 00 Inbox/
│
├── 01 Fragments/
│
├── 02 Notes/
│
├── 03 Projects/
│
├── 99 Attachments/
│
└── README.md
```

### 00 Inbox

아직 정리되지 않은 임시 기록을 저장한다.

예:

* 웹에서 발견한 링크
* 갑자기 생긴 아이디어
* 정리되지 않은 코드 조각
* 공부하다가 나중에 확인하고 싶은 내용
* 어디에 기록할지 아직 결정하지 않은 메모

Inbox의 목적은 **분류를 고민하지 않고 일단 기록하는 것**이다.

필요한 내용은 이후 `02 Notes`나 `03 Projects`로 이동한다.

---

### 01 Fragments

하루 동안 공부하거나 개발하면서 발생한 내용, 생각의 파편을 기록하는 작업 공간 (Daily / Scratchpad).

```text
01 Fragments/
├── 2026-09-14.md
├── 2026-09-15.md
└── ...
```

Fragment Note(Daily)는 완성된 문서가 아니다.

다음과 같은 내용을 자유롭게 기록한다.

```md
## 오늘 본 것

[[Storybook]]을 처음 제대로 살펴봤다.

단순한 UI Preview 도구라고 생각했는데,
컴포넌트의 여러 상태를 독립적으로 관리하는 역할도 한다.

궁금한 것:

- Story는 정확히 무엇인가?
- [[Visual Testing]]과 어떤 관계인가?
- [[Vitest]]와 역할이 겹치지는 않는가?
```

Fragments에서 중요하다고 판단되는 내용은 별도의 Note로 분리한다.

```text
Fragments
  ↓
발견 / 질문 / 문제
  ↓
[[새로운 Note]]
```

---

### 02 Notes

재사용할 가치가 있는 개발 지식을 저장하는 공간.

가장 핵심이 되는 폴더이며 **Flat 구조를 유지한다.**

```text
02 Notes/
├── React Compiler.md
├── Memoization.md
├── Referential Equality.md
├── Storybook.md
├── Component Driven Development.md
├── Vite Library Mode.md
├── package exports.md
├── npm publish.md
└── Monorepo.md
```

다음과 같은 기술별 하위 폴더는 만들지 않는다.

```text
❌ React/
❌ JavaScript/
❌ Testing/
❌ Build/
❌ npm/
```

기술의 소속보다 개념 사이의 관계를 중요하게 생각한다.

예:

```text
[[Component Library]]
        ↓
[[Vite Library Mode]]
        ↓
[[package exports]]
        ↓
[[npm publish]]
```

또는

```text
[[React Compiler]]
      ↓
[[Memoization]]
      ↓
[[Referential Equality]]
      ↓
[[useMemo]]
      ↓
[[Effect Dependencies]]
```

하나의 노트에는 가능하면 하나의 핵심 주제를 기록한다.

---

## Note 작성 방식

모든 노트가 동일한 구조를 가질 필요는 없다.

개념에 따라 필요한 섹션만 사용한다.

기본적으로 다음 흐름을 선호한다.

```md
# 제목

## 시작점

이 주제를 왜 찾아보게 되었는지,
처음 어떤 의문이 생겼는지 기록한다.

## 배경

이 기술이나 개념이 등장하기 전에는 어떻게 했는지 기록한다.

## 기존 방식

기존 코드나 접근 방법을 작성한다.

## 문제점

기존 방식이 가진 한계나 내가 헷갈렸던 부분을 기록한다.

## 새로운 방식

새로운 개념이나 해결 방법을 작성한다.

## 그래서 항상 이걸 쓰면 되나?

언제 사용해야 하는지,
언제 사용하지 않아야 하는지 생각한다.

## 예외 / 주의할 점

자동으로 해결되지 않는 부분이나
자주 오해하는 내용을 기록한다.

## 내가 이해한 결론

내 언어로 다시 설명한다.

## 연결

- [[관련 개념]]
- [[관련 개념]]

## Reference

-
```

중요한 것은 문서를 완성하는 것이 아니라
**내가 이해한 흐름을 남기는 것**이다.

---

### 03 Projects

특정 프로젝트의 맥락에서 발생한 기록을 저장한다.

```text
03 Projects/
├── Shannon/
└── SCARF-F/
```

여기에는 일반적인 기술 설명보다 프로젝트에 종속적인 내용을 기록한다.

예:

```text
왜 이 상태를 Zustand로 관리했는가

왜 BookSpine 기능 범위를 MVP 수준으로 줄였는가

왜 해당 API 응답 구조를 변경했는가

왜 Storybook을 프로젝트에 도입하려고 했는가
```

프로젝트에서 발견한 일반적인 개념은 `02 Notes`와 연결한다.

```md
이번 컴포넌트 라이브러리 작업에서는
[[Vite Library Mode]]를 사용했다.

관련된 패키지 공개 범위는
[[package exports]] 참고.
```

즉,

```text
Project = 실제 적용 맥락
Notes   = 재사용 가능한 지식
```

으로 구분한다.

---

### 99 Attachments

Vault에서 사용하는 첨부파일을 저장한다.

```text
99 Attachments/
├── images/
├── screenshots/
└── diagrams/
```

예:

* 화면 캡처
* 개발자 도구 캡처
* 다이어그램
* 이미지
* PDF

노트 폴더 내부에 첨부파일이 섞이지 않도록 한곳에서 관리한다.

---

# 기록 원칙

## 1. 어디에 넣을지 고민되면 Inbox

분류 때문에 기록을 멈추지 않는다.

```text
모르겠음
↓
00 Inbox
```

나중에 정리하면 된다.

---

## 2. 공부하면서는 Fragments (Daily)

Fragments는 작업대다.

완벽하게 정리하려고 하지 않는다.

```text
오늘 공부
↓
생각
↓
질문
↓
실험
↓
링크
```

를 자유롭게 기록한다.

---

## 3. 다시 볼 가치가 있으면 Note

다음과 같은 경우 별도의 Note로 만든다.

* 다시 찾아볼 것 같다.
* 다른 개념과 연결된다.
* 프로젝트에서 반복해서 사용할 것 같다.
* 처음에 이해하기 어려웠다.
* 내가 잘못 알고 있던 내용이었다.

---

## 4. 폴더보다 링크

어떤 기술에 속하는지보다 어떤 개념과 연결되는지가 중요하다.

```md
[[Storybook]]은
[[Component Driven Development]] 방식과 연결된다.

컴포넌트 상태를 독립적으로 관리하면서
[[Visual Testing]]에도 활용할 수 있다.
```

가능하면 글 안에서 자연스럽게 링크한다.

---

## 5. 모르는 것도 링크한다

아직 공부하지 않은 개념도 링크할 수 있다.

```md
Storybook은 [[Visual Regression Testing]]과도 관련이 있다.
```

해당 노트가 아직 존재하지 않아도 괜찮다.

빈 링크는 곧

> 아직 내가 제대로 이해하지 않은 개념

을 의미한다.

나중에 필요할 때 작성한다.

---

# Tag

Tag는 지식 구조를 만드는 용도가 아니라 검색과 필터를 위한 보조 도구로 사용한다.

예:

```text
#frontend
#backend
#testing
#build
#browser
#network
```

기술 이름마다 태그를 만들지는 않는다.

```text
❌ #react
❌ #react-hook
❌ #react-component
❌ #react-state
❌ #react-rendering
```

필요한 경우에만 최소한으로 추가한다.

---

# Workflow

전체 기록 흐름은 다음과 같다.

```text
개발 / 공부
     ↓
01 Fragments
     ↓
발견 / 질문 / 문제
     ↓
중요한 내용인가?
     ↓
    YES
     ↓
02 Notes
     ↓
다른 Note와 [[연결]]
     ↓
프로젝트에서 적용
     ↓
03 Projects
```

정리되지 않은 자료는 언제든

```text
00 Inbox
```

로 들어간다.

---

# Example

Storybook을 공부한다고 가정한다.

Fragments에서 시작한다.

```md
# 2026-09-14

## Storybook

[[Storybook]]을 살펴봄.

처음에는 단순히 Component Preview 도구라고 생각했다.

그런데 여러 Component State를 Story로 정의해서
독립적으로 확인하는 구조인 것 같다.

관련:

[[Component Driven Development]]
[[Visual Testing]]
```

이후 필요하다면 각각 별도의 Note가 된다.

```text
[[Storybook]]
      │
      ├── [[Component Driven Development]]
      │
      ├── [[Story]]
      │
      ├── [[Visual Testing]]
      │
      └── [[Component Library]]
```

다른 공부를 하면서 기존 지식과 다시 연결될 수 있다.

```text
[[Component Library]]
       │
       ├── [[Storybook]]
       ├── [[Vite Library Mode]]
       ├── [[package exports]]
       └── [[npm publish]]
```

이렇게 연결이 쌓이면서 Vault 자체가 개발 지식 지도가 된다.

---

# 가장 중요한 규칙

이 Vault는 정리하기 위한 공간이 아니라
**생각하고, 이해하고, 다시 찾아보기 위한 공간이다.**

기록을 남기기 위해 구조를 고민하는 시간이
기록을 작성하는 시간보다 길어지면 구조를 단순화한다.

```text
완벽한 정리 < 빠른 기록
폴더 분류 < 개념 연결
복붙한 설명 < 내가 이해한 설명
많은 기록 < 다시 사용할 수 있는 기록
```
