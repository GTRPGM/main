# Branching Strategy

이 문서는 프로젝트 전반에서 사용하는 브랜치 전략을 정의합니다.
모든 팀원은 아래 규칙을 기준으로 브랜치를 생성하고 작업합니다.

---

## 0. 요약

- `main`, `dev` 제외 1브랜치 1인 - 공유 브랜치는 별도 명시
- 기능 개발 완료 시 feature/\* → dev 로 PR 병합
- 마이너 버전 완료 시 dev → main 으로 PR 병합
- 병합 이후 반드시 브랜치 동기화 수행

```text
# Merge Flow (병합 흐름)
main   <-[ PR | Squash ]-   dev   <--[ PR | Merge ]--   feature/*

# Sync Flow (동기화 흐름)
main   --[ PR | Merge ]->   dev   --[ local merge ]->   feature/*
```

- main: 안정 브랜치
- dev: 통합 브랜치
- feature/\*: 작업 브랜치

---

## 1. 기본 브랜치

### main

- 항상 배포 가능한 상태를 유지합니다.
- 직접 커밋하지 않습니다.
- feature/\* 브랜치는 main으로 직접 병합하지 않습니다.
- `dev` 브랜치에서만 PR을 통해 **Squash Merge**로만 병합합니다.
  - `main` 브랜치는 배포/보여주는 대상이기에 깔끔하게 관리하고자 합니다.
  - 레포 관리자에 의해 사전 공지하고, dev의 안정성을 확인한다음 병합합니다.
  - main 브랜치의 push 단위는 마이너 버전 업입니다.
  - 해당 브랜치로의 커밋 메시지는 다음만 허용합니다. (x는 버전)

    ```text
    vx.x.x: version detail
    ```

### dev

- 기능 통합 및 검증을 위한 브랜치입니다.
- 모든 `feature`/`docs` 브랜치는 `dev`를 기준으로 생성합니다.
- 직접 커밋하지 않으며 PR을 통해 **Merge Commit**로 병합합니다.
  - 필요 시 squash 병합을 사용할 수 있으나, 사유를 PR에 명시합니다.
  - 병합 전 반드시 한명 이상의 팀원과 리뷰합니다.

---

## 2. 공유 브랜치

- 공동 작업 브랜치입니다.
- 이름 끝에 `-co`를 붙입니다.
- `dev` 브랜치에서 분기합니다.
- 작업 완료 후 `dev`로 PR을 생성합니다.
- 해당 브랜치에는 히스토리 변경(`push --force`, `rebase`, `squash`)를 금지합니다.

예시:

```text
docs/scratch-co
```

---

## 3. 작업 브랜치

### feature/\*

- 새로운 기능, 설정을 위한 브랜치입니다.
- `dev` 브랜치에서 분기합니다.
- 작업 완료 후 `dev`로 PR을 생성합니다.

예시:

```text
feature/ci
feature/docs-setup
feature/rule-graph
```

### docs/\*

- 문서 변경을 위한 브랜치입니다.
- `dev` 브랜치에서 분기합니다.
- 작업 완료 후 `dev`로 PR을 생성합니다.

예시:

```text
docs/workflow
docs/tutorial
```

### fix/{issue number}-{issue name}

- 버그 수정을 위한 브랜치입니다.
- 버그가 생길 때, issue 번호로 생성합니다.
- `dev` 브랜치에서 분기합니다.
  - 작업 완료 후 `dev`로 PR을 생성합니다.
  - 반드시 **_이슈 넘버를 PR 메시지에 포함_** 시켜주세요.

예시:

```text
fix/22-type_error
```

PR 예시:

```text
fix: type error from somthing(#22)
```

---

### hotfix/{issue number}-{issue name}

- 예외 브랜치입니다.
- `main`브랜치에서 발견된 치명적인 버그 수정을 위한 브랜치입니다.
- 버그가 생길 때, issue 번호로 생성합니다.
- `main` 브랜치에서 분기합니다.
  - 작업 완료 후 `main`로 PR을 생성합니다.
  - 반드시 **Squash Merge**로 병합합니다.
  - 반드시 **_이슈 넘버를 PR 메시지에 포함_** 시켜주세요.
  - 병합 이후 `dev`에 **Merge Commit**로 반영합니다.

```text
hotfix/22-type_error
```

PR 예시:

```text
hotfix: type error from somthing(#22)
```

---

## 3. 병합 규칙

- 모든 변경 사항은 PR을 통해 병합합니다.
  - dev 브랜치 PR 병합 시 기본적으로 **Merge Commit** 방식을 사용합니다.
  - main 브랜치 PR 병합은 반드시 **Squash Merge** 방식을 사용합니다.
  - 기본 브랜치 병합은 반드시 사전 공지합니다.
- 병합 이후 다음을 수행합니다.
  - 브랜치 병합 이후, 구현 완료한 브랜치는 삭제합니다.
  - main으로 병합 이후 dev에 **Merge Commit**로 PR하여 반영합니다.
  - dev로 병합 이후, 기능 개발 중인 브랜치는
    dev 브랜치를 **각 작업자가 로컬에서 merge** 하여 반영합니다.

---

## 4. 히스토리 관리 원칙

- `main`, `dev` 브랜치에서는 rebase, force push 등 히스토리 수정을 금지합니다.
- 개인 작업 브랜치(`feature/*`)에서만 히스토리 수정을 허용합니다.
- 실수한 커밋은 새로운 커밋으로 수정하거나 PR에서 정리합니다.

---
