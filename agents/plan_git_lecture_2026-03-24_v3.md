# Git 강의 자료 추가 수정 계획서 (v3)

> 작성일: 2026-03-24  
> 상태: ✅ 전체 반영 완료

---

## 변경 항목 요약

| # | 대상 파일 | 작업 유형 | 내용 |
|---|-----------|-----------|------|
| 1 | `01_quick_setup.md` | 내용 추가 | GitHub Codespaces 사용 방법 추가 (웹 내장 에디터/실행 환경) |
| 2 | `02_git.md` | 내용 추가 | VSCode에 GitHub Copilot(AI 어시스턴트) 확장기능 설치 및 사용 방법 소개 |

---

## 상세 계획

### 1. `01_quick_setup.md` — GitHub Codespaces 소개 및 활용

**추가 위치**: 기존 `2. 새 저장소 직접 만들기 (선택)` 하단, `Personal access tokens` 섹션 위

**추가 내용**:
- **개념**: 내 컴퓨터(로컬)에 Git이나 VSCode를 설치하지 않고도, 웹 브라우저만 있으면 개발 환경과 터미널을 바로 띄울 수 있는 기능입니다.
- **실행 방법**:
  1. GitHub의 강의 자료(또는 Fork한) 저장소에 접속합니다.
  2. 우측 초록색 `<> Code` 버튼을 클릭합니다.
  3. `Codespaces` 탭을 선택하고 `Create codespace on main`을 클릭합니다.
- **장점**: 환경 구축(의존성 모듈 설치 등) 시간을 절약할 수 있으며 언제 어디서든 동일한 개발 환경으로 작업할 수 있습니다.

> 🖼️ **첨부 이미지 계획**
> - 출처: `https://earthdatascience.org/img/get-started/r-codespaces/12-launch.png`
> - 로컬 경로: `./image/codespaces.png` 저장 후 문서 내에 포함

---

### 2. `02_git.md` — GitHub Copilot 기반 효율적인 개발

**추가 위치**: 기존 항목 `## GUI` 내부 VSCode "GitLens, Git Graph" 확장기능 표 하단

**추가 내용**:
- **GitHub Copilot 이란?**: 코드 자동 완성, AI 채팅, 그리고 Git까지 도와주는 인공지능 코딩 어시스턴트입니다.
- **설치 및 연동 방법**:
  1. VSCode 좌측 Extensions(확장, `Ctrl+Shift+X` / `Cmd+Shift+X`) 탭 클릭
  2. 검색창에 `GitHub Copilot` 검색 후 📥 **Install** 클릭
  3. 설치 완료 후 우측 하단의 프롬프트를 따라 GitHub 계정에 로그인하여 연동
  *(유료 구독 혹은 평가판 권한 필요)*
- **Git 관점에서의 주요 활용법**:
  - 소스 제어(Source Control) 탭에서 변경 사항을 Staged 영역에 올린 뒤, 입력창 옆의 **반짝이는 별(Sparkle) 아이콘 (`✨`)**을 누르면 AI가 변경된 코드 파일들을 분석하여 **커밋 메시지(`Commit Message`)를 자동으로 생성**해 줍니다.
  - 이를 통해 Commit Message Rule 패턴(feat, fix 등)을 보다 손쉽게 작성할 수 있습니다.

---

## 작업 순서

```
1단계: 01_quick_setup.md — GitHub Codespaces 이미지 다운로드 (`./image/codespaces.png`)
2단계: 01_quick_setup.md — GitHub Codespaces 관련 내용 및 이미지 추가
3단계: 02_git.md — VSCode 확장기능 섹션에 GitHub Copilot 가이드 추가
```

---

> 각 내용이 적절한지 검토해 주시면, 확인 후 즉시 파일에 반영하겠습니다.
