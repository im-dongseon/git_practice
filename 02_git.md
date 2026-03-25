# 버전 관리?

* 어떤 파일이 마지막 파일이지?
  * ex) report_final_final_진짜마지막.docx
* 여러명이 하나의 앱을 개발하면?
  * 수정한 코드를 어떻게 합치지?

> Git은 ‘시간을 되돌릴 수 있는 저장소’입니다.



# Git vs Github

> Git은 개인용 버전관리, GitHub는 협업을 위한 무대

| 항목 | Git            | Github            |
| ---- | -------------- | ----------------- |
| 역할 | 버전 관리 도구 | 협업 플랫폼       |
| 위치 | 내 컴퓨터      | 클라우드          |
| 기능 | commit, branch | PR, Issue, Review |

* 회사에 따라서 Github, Gitlab, Gerrit, bitbucket 등 다양한 솔루션중에서 하나를 사용

---

# Git의 내부 구조

Git 명령어를 잘 이해하려면 파일이 어느 단계에 있는지 먼저 알아두면 좋습니다.

![git-internals](./image/git-internals.png)

| 영역 | 의미 | 자주 쓰는 명령어 |
|------|------|------------------|
| Working Directory | 내가 현재 수정 중인 파일이 있는 작업 공간 | `git restore <file>`, `git add` |
| Staging Area (Index) | 다음 커밋에 담을 변경사항을 고르는 임시 공간 | `git add`, `git restore --staged <file>` |
| Local Repository | 커밋 이력이 저장되는 로컬 저장소 | `git commit`, `git reset`, `git revert` |

간단히 흐름으로 보면 아래와 같습니다.

```text
Working Directory --(git add)--> Staging Area --(git commit)--> Local Repository
```

이 구조를 알고 나면 각 명령이 어디에 영향을 주는지 구분하기 쉬워집니다.

- `git restore <file>`: 작업 중인 파일을 마지막 상태로 되돌림
- `git restore --staged <file>`: staging area에서만 제외하고 작업 파일은 유지
- `git reset`: 로컬 커밋 이력을 되돌림
- `git revert`: 기존 커밋을 취소하는 새 커밋을 만듦
- `git stash`: working directory와 staging area의 변경사항을 임시 보관

# GUI vs CLI

## GUI

* 별도 프로그램 설치 없이 **시각적으로 Git 작업** 가능

| 도구 | 특징 | 공식 URL |
|------|------|----------|
| **GitHub Desktop** | 입문자 친화적, 단순한 UI | https://desktop.github.com |
| **SourceTree** | 무료, Atlassian 제공, 고급 기능 풍부 | https://www.sourcetreeapp.com |
| **Fork** | 빠른 속도, 직관적 UI, Mac/Windows 지원 | https://git-fork.com |

* GitHub Desktop

  ![002](./image/002.png)

* SourceTree

  ![sourcetree](./image/sourcetree.png)

* Fork

  ![fork](./image/fork.png)

* VSCode 확장기능을 활용하면 별도 도구 없이 에디터 안에서 Git 작업 가능

  | 확장기능 | 설명 |
  |----------|------|
  | **GitLens** | 코드 라인별 커밋 작성자/시간 표시, 브랜치 비교 등 고급 기능 |
  | **Git Graph** | 브랜치 그래프를 시각적으로 확인, GUI처럼 커밋 이력 탐색 |

---

### 💡 AI 기반 효율화: GitHub Copilot 활용

* **GitHub Copilot 이란?**
  * 코드 자동 완성, AI 채팅, 각종 명령어 작성 및 Git 작업까지 도와주는 인공지능 코딩 어시스턴트입니다.

* **설치 및 연동 방법**
  1. VSCode 좌측 Extensions(확장, `Ctrl+Shift+X` / `Cmd+Shift+X`) 탭 클릭
  2. 검색창에 `GitHub Copilot` 검색 후 📥 **Install** 클릭
  3. 설치 완료 후 우측 하단 프롬프트를 따라 GitHub 계정 연동 (유료 구독 또는 평가판 필요)

* **Git 작업 시 핵심 활용 (AI 커밋 프로그램)**
  * 변경 사항을 **Staged** 영역에 올린 뒤, 소스 제어(Source Control) 입력창 안의 **반짝이는 별(Sparkle) 아이콘 (`✨`)**을 클릭하세요.
  * AI가 변경된 코드들을 분석해 적절한 **커밋 메시지(Commit Message)**를 자동으로 작성해 줍니다!
  * 이를 활용하면 `Commit Message Rule`(feat, fix 등)을 훨씬 손쉽게 따를 수 있습니다.

---

## CLI

```shell
git init
git add .
git commit -m "Initial commit"
git remote add origin <repo-url>
git push -u origin main
```

* GUI 를 사용하지 못하는 환경에서는 → CLI 사용
