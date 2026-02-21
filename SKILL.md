---
name: custom-skill
description: >-
  Use this skill when the user asks about Git conventions, commit messages, or branch naming.
  Trigger when the user:
  - Asks about commit message format, convention, or style (커밋 메시지, 커밋 컨벤션, commit convention)
  - Wants to commit code and needs guidance on the message (커밋, commit, git commit)
  - Asks about commit types like feat, fix, refactor, chore, docs, test, style, perf
  - Asks how to split or separate commits (커밋 분리, atomic commit)
  - Asks about branch naming or branch strategy (브랜치 전략, 브랜치 이름, branch naming)
  - Asks about Git workflow rules or best practices (Git 작업 규칙, Git 가이드)
  Do NOT trigger for general Git usage questions unrelated to conventions (e.g., "how to rebase", "how to resolve merge conflicts").
---

# 개발 공통 가이드

한국어로 대답

## Git 커밋 컨벤션

### 커밋 메시지 형식

```
<type>: <subject>
```

### 타입

| 타입       | 설명                                   |
| ---------- | -------------------------------------- |
| `feat`     | 새로운 기능 추가                       |
| `fix`      | 버그 수정                              |
| `refactor` | 리팩토링 (기능 변경 없음)              |
| `style`    | 코드 스타일 변경 (포매팅, 세미콜론 등) |
| `docs`     | 문서 수정                              |
| `test`     | 테스트 추가/수정                       |
| `chore`    | 빌드, 설정 파일 변경                   |
| `perf`     | 성능 개선                              |

### 커밋 메시지 규칙

- 한국어로 작성한다
- 제목은 간결하게 작성한다 (50자 이내 권장)
- 제목 끝에 마침표를 붙이지 않는다
- 관련 이슈가 있으면 `closes #번호` 또는 `refs #번호`를 붙인다

### 예시

```
feat: 사용자 프로필 페이지 추가 closes #42
fix: 로그인 시 토큰 만료 처리 수정 refs #15
refactor: API 호출 로직 공통 서비스로 분리
chore: Node.js 버전 업데이트
```

## Git 브랜치 전략

- `main` 또는 `master`: 운영 브랜치
- `develop`: 개발 브랜치
- `feat/*`: 기능 개발 브랜치
- `fix/*`: 버그 수정 브랜치
- `release/*`: 릴리스 준비 브랜치

## 커밋 분리 규칙 (Atomic Commits)

커밋은 최대한 작은 단위로 쪼갠다. 하나의 커밋은 하나의 논리적 변경만 포함해야 한다.

### 분리 기준

- **파일 역할별 분리**: 컴포넌트, 서비스, 스타일, 타입 등 역할이 다른 변경은 별도 커밋
- **기능 단위 분리**: 하나의 기능 내에서도 독립적인 단계가 있으면 나눈다
- **리팩토링과 기능 변경 분리**: 리팩토링과 새 기능/버그 수정을 같은 커밋에 섞지 않는다
- **설정 변경 분리**: 패키지 설치, 설정 파일 변경은 별도 커밋

### 분리 예시

하나의 API 기능을 추가할 때:

```
1. feat: 사용자 조회 API DTO 타입 정의
2. feat: 사용자 조회 API 서비스 구현
3. feat: 사용자 목록 테이블 컴포넌트 추가
4. feat: 사용자 관리 페이지에 목록 테이블 연동
5. style: 사용자 목록 테이블 반응형 스타일 적용
```

버그 수정 시:

```
1. fix: 날짜 포맷 유틸 함수 null 처리 수정
2. test: 날짜 포맷 유틸 함수 테스트 추가
```

### 금지 사항

- 여러 기능을 한 커밋에 몰아넣지 않는다
- "작업 중", "수정" 같은 모호한 커밋을 만들지 않는다
- 스타일 변경과 로직 변경을 하나의 커밋에 섞지 않는다

## Git 작업 규칙

- 커밋 전 변경사항을 확인한다 (`git status`, `git diff`)
- 관련 없는 변경사항은 별도 커밋으로 분리한다
- force push는 사용자가 명시적으로 요청한 경우에만 수행한다
- `.env`, 인증 정보 등 민감한 파일은 커밋하지 않는다
