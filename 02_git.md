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

## CLI

```shell
git init
git add .
git commit -m "Initial commit"
git remote add origin <repo-url>
git push -u origin main
```

* GUI 를 사용하지 못하는 환경에서는 → CLI 사용
