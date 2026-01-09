# Commit Convention

이 문서는 프로젝트 전반에서 사용하는 커밋 메시지 규칙을 정의합니다.
모든 커밋은 아래 규칙을 따르는 것을 원칙으로 합니다.

---

## 1. 기본 형식

```text
<type>: <summary>
```

- 한 줄로 작성합니다.
- 영어를 사용합니다.
- summary는 변경 내용을 간결하게 설명합니다.
- 마침표(`.`)는 사용하지 않습니다.

---

## 2. 사용 가능한 타입

아래 타입만 사용합니다.

- **feat**: 새로운 기능 추가 (로직 추가)
- **fix**: 버그 수정
- **refactor**: 기능 변경 없는 코드 구조 개선 (로직이 변경 될 수 있으나 입출력 동일)
- **style**: 포맷, 공백, 린트 수정 등 (로직 변경 없음)
- **docs**: 문서 추가 또는 수정
- **test**: 테스트 코드 추가 또는 수정
- **chore**: 설정, 규칙, 도구, CI, 브랜치 시작, 기타 작업

> CI, 브랜치, 설정 관련 작업은 모두 `chore`를 사용합니다.

---

## 3. 예시

```text
chore: add initial collaboration rules
docs: add environment setup guide
feat: implement rule graph builder
fix: handle empty scenario input
```

---

## 4. 권장 규칙

- 한 커밋은 하나의 논리적인 변경만 포함합니다.
- 서로 다른 목적의 변경은 커밋을 분리합니다.
- 의미 없는 커밋 메시지는 지양합니다.

---

## 5. 금지 사항

아래와 같은 메시지는 사용하지 않습니다.

```text
init
update
fix bug
작업함
```

> 위와 같은 메시지는 변경 내용을 추적하기 어렵게 만듭니다.

---

## 6. 예외

브랜치의 첫 커밋에 한해 아래 메시지를 허용합니다. 아래 커멘드로 변경 사항 없는 커밋을 만들어 주세요. `{branch-name}`에 브랜치 이름을 넣어주세요.

```text
chore: introduce {branch-name} branch
```

```sh
git commit --allow-empty -m "chore: introduce {branch-name} branch"
```

## 7. 히스토리 수정(리라이트) 원칙

- 원격(공유) 브랜치(`main`, `dev`)에서는 rebase, force push 등 히스토리 수정을 하지 않습니다.
- 실수한 커밋은 새로운 커밋으로 수정하거나, PR에서 정리(squash)합니다.
- 예외: 개인 작업 브랜치에서는  rebase, force push 사용 가능합니다.

---
