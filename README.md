# My Knowledge Vault

개발 학습과 실무 경험을 축적하기 위한 Obsidian 기반 개인 지식 저장소입니다.

## Structure

```text
My-Knowledge-Vault/
├── 00 Inbox/
├── 01 Fragments/
├── 02 Notes/
├── 03 Projects/
├── 99 Attachments/
└── _templates/
```

| Path             | Purpose          |
| ---------------- | ---------------- |
| `00 Inbox`       | 정리 전 임시 메모 및 자료  |
| `01 Fragments`   | 날짜별 학습 및 작업 기록, 생각의 파편 (Daily / Scratchpad) |
| `02 Notes`       | 재사용 가능한 개발 지식 (Atomic Notes) |
| `03 Projects`    | 프로젝트별 기술 결정 및 경험 (ADR, 회고) |
| `99 Attachments` | 이미지 및 기타 첨부파일    |
| `_templates`     | 폴더별 템플릿 가이드       |

## Workflow

```text
Capture
  ↓
Fragments / Inbox
  ↓
Refine
  ↓
Notes
  ↓
Connect
  ↓
Projects
```

## Principles

* **Capture first** — 분류보다 기록을 우선한다.
* **Keep it flat** — 기술별 하위 폴더를 만들지 않는다.
* **One note, one topic** — 하나의 노트는 하나의 핵심 주제를 다룬다.
* **Link over folders** — 분류보다 `[[wikilink]]` 연결을 우선한다.
* **Write what I understood** — 자료를 옮기는 대신 이해한 내용을 기록한다.
* **Refine when needed** — 모든 메모를 완성된 문서로 만들 필요는 없다.

## Templates

> **"템플릿은 빈칸을 모두 채우는 양식이 아니라, 생각을 시작하게 해주는 가이드다."**

폴더별로 기본 템플릿을 따로 두되 작성을 강제하지 않습니다. 불필요한 항목은 자유롭게 지우고 작성합니다.

```text
_templates/
├── Inbox.md       # 초경량 링크/메모 스크랩
├── Fragment.md    # 생각/질문/관찰 중심 파편
├── Note.md        # 벨로그 스타일의 탄탄한 지식 정리
└── Project.md     # 의사결정(ADR), 대안(Alternatives), 맥락 중심
```

### 템플릿 운영 기준

```text
빠른 메모          → 템플릿 안 씀
조금 남길 가치 있음 → Fragment 템플릿
다시 참고할 지식    → Note 템플릿
프로젝트 판단 기록  → Project 템플릿
```

## Example

```text
[[Component Library]]
├── [[Storybook]]
├── [[Vite Library Mode]]
├── [[package exports]]
└── [[npm publish]]
```

기술의 소속을 분류하는 대신, 관련된 지식을 연결하면서 확장합니다.

## Note Lifecycle

```text
Inbox
  ↓
Fragments
  ↓
Note
  ↓
Project Context
```

모든 기록이 `Note`가 될 필요는 없습니다.

다시 참고하거나 다른 지식과 연결할 가치가 있는 내용만 `02 Notes`에 남깁니다.

---

**Capture quickly. Refine selectively. Connect continuously.**
