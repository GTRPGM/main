# 신규 팀원을 위한 개발 워크플로우 안내

이 문서는 프로젝트에 새로 참여한 팀원이 작업 흐름 전반을 이해하고 빠르게 적응할 수 있도록 돕기 위한 통합 가이드입니다. 아래 절차만 따라하면 기본적인 개발 과정에 참여할 수 있습니다.

더 상세한 규칙은 아래 문서들을 참고할 수 있습니다.

- [브랜치 전략 (Branching Strategy)](./branch-stratagy.md)
- [커밋 컨벤션 (Commit Convention)](./commit-convention.md)
- [PR 규칙 (Pull Request Rules)](./pull-request-rule.md)
- [이슈 작성 가이드 (Issue Creation Guide)](./issue-guide.md)
- [CI 범위 안내 (CI Scope Guide)](./CI-coverage.md)

---

## 빠른 참조 (Workflow Cheatsheet)

이 문서는 개발 과정 각 단계에서 필요한 핵심 규칙, 형식, 명령어를 요약한 빠른 참조 문서입니다.

| 단계          | 항목           | 내용                                                                   | 예시                                     |
| :------------ | :------------- | :--------------------------------------------------------------------- | :--------------------------------------- |
| **1. 이슈**   | 제목 형식      | `[타입] <내용 요약>` (타입 첫 글자 대문자)                             | `[Feat] 소셜 로그인 기능 추가`           |
|               | 타입           | `Feat`, `Fix`, `Docs`, `Refactor`, `Test`, `Chore`, `Ops`              |                                          |
|               | 템플릿 사용    | `issue-guide.md` 참고                                                  |                                          |
| **2. 브랜치** | 이름 형식      | `타입/이슈번호-이름` (타입은 소문자)                                   | `feat/11-new-login-page`                 |
|               | 타입           | `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ops` (+ `hotfix`) |                                          |
|               | 분기 대상      | `dev` (단, `hotfix`는 `main`)                                          |                                          |
|               | 타입 매핑      | `[Fix]` 이슈 → `fix/` 브랜치. 나머지는 이름 일치.                      |                                          |
|               | 생성 명령어    | `git checkout -b <브랜치명>`                                           | `git checkout -b feat/11-new-login-page` |
| **3. 커밋**   | 메시지 형식    | `타입: <요약>` (타입은 소문자)                                         | `feat: add login page structure`         |
|               | 타입           | `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ops`              |                                          |
|               | 명령어         | `git commit -m "<메시지>"`                                             |                                          |
| **4. PR**     | 제목 형식      | `타입: <요약>`                                                         | `feat: add login page structure`         |
|               | 대상 브랜치    | `dev` (단, `hotfix`는 `main`)                                          |                                          |
|               | 이슈 연결      | 본문 하단 `Closes`/`Fixes` 키워드 사용                                 | `Closes #11`                             |
|               | 푸시 명령어    | `git push origin <브랜치명>`                                           | `git push origin feat/11-new-login-page` |
| **5. 원칙**   | 셀프 머지      | **금지**                                                               |                                          |
|               | CI 실패        | **리뷰 요청 금지**                                                     |                                          |
| **6. 동기화** | `dev` 최신화   | `git checkout dev && git pull origin dev`                              |                                          |
|               | 내 브랜치 반영 | `git merge dev`                                                        | `git merge dev`                          |

---

## 전체 워크플로우 요약

우리 팀의 기본적인 개발 작업은 아래와 같은 흐름으로 진행됩니다.

> **1. 이슈 확인/생성 → 2. 브랜치 생성 → 3. 로컬 개발 및 커밋 → 4. PR 생성 → 5. 리뷰 및 논의 → 6. 병합 → 7. 동기화 및 정리**

---

## 단계별 상세 가이드

### 1단계: 작업 시작 - 이슈(Issue) 확인 및 생성

- 모든 작업은 **이슈(Issue)** 에서 시작합니다. 이슈는 작업의 목적과 내용을 명확히 하는 역할을 합니다.
- 개발을 시작하기 전, GitHub 저장소의 `Issues` 탭에서 내가 맡을 작업에 대한 이슈가 있는지 확인합니다.
- 만약 이슈가 없다면, [이슈 작성 가이드](./issue-guide.md)에 따라 `[Feat]`, `[Fix]` 등 타입에 맞는 새로운 이슈를 생성합니다.

### 2단계: 브랜치(Branch) 생성

- 이슈를 기반으로 로컬에서 개발을 진행할 브랜치를 생성합니다. 브랜치 타입은 [브랜치 전략](./branch-stratagy.md)의 매핑 규칙을 따릅니다.
- 항상 최신 상태의 `dev` 브랜치에서 새로운 브랜치를 분기합니다.

```sh
# 1. 로컬 dev 브랜치로 이동
git checkout dev

# 2. 원격 저장소의 최신 내용을 dev 브랜치에 반영
git pull origin dev

# 3. 새로운 작업 브랜치 생성 및 이동 (규칙: 타입/이슈번호-이름)
# 예시: [Feat] 타입 이슈 #11에 대한 작업
git checkout -b feat/11-new-login-page
```

### 3단계: 로컬 개발 및 커밋(Commit)

- 생성한 브랜치에서 코드를 수정하거나 새로운 파일을 추가하며 기능을 개발합니다.
- 커밋 메시지는 [커밋 컨벤션](./commit-convention.md)을 반드시 따릅니다.

```sh
# 예시: feat/11-new-login-page 브랜치에서의 커밋
git commit -m "feat: add user login form"
```

- **Pre-commit 사용**: 우리 프로젝트는 커밋 시점에 코드 스타일을 자동으로 검사합니다. **최초 설정은 [환경 설정 문서](../setup.md)를 참고하여 `pre-commit install`을 먼저 실행해야 합니다.**

### 4단계: Pull Request(PR) 생성

- 로컬 개발이 완료되면, 변경 사항을 원격 저장소에 푸시(push)하고 `dev` 브랜치로 **Pull Request(PR)** 를 생성합니다.
- PR 제목과 본문은 [PR 규칙](./pull-request-rule.md)에 따라 상세히 작성합니다.
- 관련 이슈가 있다면 PR 본문 하단에 `Closes #[이슈번호]` 와 같이 연결합니다.

```sh
# 1. 내 작업 브랜치를 원격 저장소에 푸시
git push origin feat/11-new-login-page
```

### 5단계: 리뷰 및 논의(Review & Discussion)

- PR을 생성하면 CI(자동 검증)가 실행됩니다. **CI가 실패한 상태에서는 리뷰를 요청하지 않는 것을 원칙으로 합니다.**
- 리뷰어의 의견에 따라 코드를 수정해야 할 경우, 로컬 브랜치에서 추가 커밋을 하고 다시 푸시하면 PR에 자동으로 반영됩니다.

### 6단계: 병합(Merge)

- PR이 최종 승인되면, 담당자가 PR을 `dev` 브랜치에 병합합니다. **기본적으로 PR 작성자 본인이 직접 병합하지 않습니다.**
- 병합이 완료되면 내가 작성한 코드가 팀의 공용 브랜치에 공식적으로 반영됩니다.

### 7단계: 동기화 및 정리(Sync & Cleanup)

- 작업 브랜치 병합 후에는 뒷정리가 필요합니다.

1. **로컬 브랜치 동기화**: 진행 중인 다른 작업 브랜치가 있다면, 최신화된 `dev` 브랜치의 내용을 가져와 반영합니다.

   ```sh
   # 1. 로컬 dev 브랜치로 이동 후 최신화
   git checkout dev
   git pull origin dev

   # 2. (만약 다른 작업 브랜치가 있다면) 해당 브랜치로 이동 후 dev 병합
   git checkout fix/22-another-bug
   git merge dev
   ```

2. **작업 완료 브랜치 삭제**: 병합이 완료된 브랜치는 삭제합니다.

   ```sh
   # 로컬에서 작업 브랜치 삭제
   git branch -d feat/11-new-login-page

   # 원격 저장소에서 작업 브랜치 삭제
   git push origin --delete feat/11-new-login-page
   ```

---
