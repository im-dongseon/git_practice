# Git 강의 자료 추가 수정 계획서

> 작성일: 2026-03-24  
> 이전 계획서: [`plan_git_lecture_2026-03-24.md`](./plan_git_lecture_2026-03-24.md)  
> 상태: ✅ 전체 반영 완료

---

## 변경 항목 요약

| # | 대상 파일 | 작업 유형 | 내용 |
|---|-----------|-----------|------|
| 1 | `01_quick_setup.md` | 내용 추가 | 강의 자료 git 주소 및 Fork 과정 추가 |
| 2 | `02_git.md` | 내용 추가 | SourceTree, Fork GUI 도구 소개 + 이미지 + URL |
| 3 | `03_start_new_feature.md` | 내용 변경 | Fork 단락 제거 + 실습용 repo init 과정 추가 + `git restore` 실습 추가 |
| 4 | `04_conflict.md` | 내용 추가 | 실습 브랜치에서 인위적 충돌 생성 후 해결하는 실습 추가 |
| 5 | `06_reset_revert.md` | 내용 추가 | reset / revert 단계별 실습 추가 |

---

## 상세 계획

---

### 1. `01_quick_setup.md` — 강의 자료 주소 및 Fork 과정 추가

**현재 상태**  
Quick setup 섹션이 일반적인 새 저장소 초기화 흐름만 다루고 있음.

**추가할 내용**

#### 1-1. 강의 자료 git 주소 안내

* `Quick setup` 섹션 상단에 강의 자료 저장소 URL 명시

```
강의 자료 저장소: https://github.com/im-dongseon/git_practice
```

#### 1-2. Fork하여 내 계정으로 가져오는 과정

* 아래 단계를 순서대로 설명

1. GitHub에서 강의 저장소(`im-dongseon/git_practice`) 접속
2. 우측 상단 **Fork** 버튼 클릭 → 내 계정에 복제본 생성
3. 내 저장소(`{your-id}/git_practice`)를 로컬로 clone

```shell
git clone https://github.com/{your-id}/git_practice.git
cd git_practice
```

4. 원본 저장소를 `upstream`으로 등록 (강의 자료 업데이트 수신용)

```shell
git remote add upstream https://github.com/im-dongseon/git_practice.git
git remote -v
```

---

### 2. `02_git.md` — SourceTree, Fork GUI 도구 추가

**현재 상태**  
GitHub Desktop + VSCode 확장기능만 소개되어 있음.

**추가할 내용**

#### 2-1. SourceTree, Fork 소개 추가

* 기존 GitHub Desktop 소개 뒤에 SourceTree, Fork 추가

| 도구 | 특징 | 공식 URL |
|------|------|----------|
| **GitHub Desktop** | 입문자 친화적, 단순한 UI | https://desktop.github.com |
| **SourceTree** | 무료, Atlassian 제공, 고급 기능 풍부 | https://www.sourcetreeapp.com |
| **Fork** | 빠른 속도, 직관적 UI, Mac/Windows 지원 | https://git-fork.com |

#### 2-2. 이미지 추가

* 각 도구 GUI 화면 이미지 생성 후 `./image/` 에 배치

| 이미지 파일 | 내용 |
|-------------|------|
| `image/sourcetree.png` | SourceTree 메인 화면 |
| `image/fork.png` | Fork 메인 화면 |

> 이미지 출처

| 이미지 파일 | 출처 | 방법 |
|-------------|------|---------|
| `image/sourcetree.png` | 기존 파일 활용 | 현재 `./image/sourcetree.png` 사용 |
| `image/fork.png` | Fork 공식 사이트 | `https://git-fork.com/images/image1.jpg` 다운로드 후 저장 |

---

### 3. `03_start_new_feature.md` — Fork 단락 제거

**현재 상태**

```markdown
## Fork 

* https://github.com/lim-dongsun/git_practice

* [repo init 은 readme 파일 참고](./01_readme.md)
```

**변경 내용**

* `## Fork` 단락 전체 삭제
* Fork 관련 내용은 `01_quick_setup.md`에서 다루므로 중복 제거

#### 3-1. 실습용 repo 초기화 과정 추가

* '링크로 참조' 방식 대신, 실습용 저장소를 직접 만들고 init하는 과정을 첫 단계부터 수록

```shell
mkdir my_git_practice
cd my_git_practice
git init
echo "# my git practice" >> README.md
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/{your-id}/my_git_practice.git
git push -u origin main
```

#### 3-2. `git restore` 실습 추가

* **언제 사용?** `git add` 전/후 수정된 파일을 이전 상태로 되돌릴 때

| 상황 | 명령어 |
|------|--------|
| 작업 중 파일을 마지막 커밋 상태로 되돌리기 (unstaged) | `git restore <file>` |
| staged 상태인 파일을 unstaged로 되돌리기 | `git restore --staged <file>` |

```shell
# 1. 파일 수정 후 실수로 되돌리고 싶을 때
echo "wrong content" >> README.md
git restore README.md

# 2. git add 한 파일을 unstaged로 되돌리고 싶을 때
git add README.md
git restore --staged README.md
```

---

### 4. `04_conflict.md` — 충돌 실습 추가

**추가할 내용**

* `03_start_new_feature.md`에서 만든 실습 브랜치를 활용하여, 예측 가능한 충돌을 인위적으로 만든 뒤 직접 해결하는 실습

```shell
# 1. main 브랜치와 feature 브랜치에서 같은 파일 동일 위치 수정
git checkout main
echo "main의 변경" >> README.md
git add README.md && git commit -m "main: README 수정"

git checkout feature/add-profile
echo "feature의 변경" >> README.md
git add README.md && git commit -m "feature: README 수정"

# 2. merge 시도 → 충돌 발생 확인
git checkout main
git merge feature/add-profile

# 3. 충돌 표시 확인 후 직접 편집
git status

# 4. 충돌 해결 후 커밋
git add README.md
git commit
```

---

### 5. `06_reset_revert.md` — reset / revert 실습 추가

**추가할 내용**

```shell
# 실습용 커밋 3개 생성
echo "A" >> README.md && git add . && git commit -m "commit A"
echo "B" >> README.md && git add . && git commit -m "commit B"
echo "C" >> README.md && git add . && git commit -m "commit C"

# 1. --soft: 커밋 이력만 되돌림, 변경사항은 staged 유지
git reset --soft HEAD~1
git status

# 2. --mixed: 커밋 + staged 조기화, 파일은 유지
git reset --mixed HEAD~1
git status

# 3. --hard: 전체 삭제 (철저 주의)
git reset --hard HEAD~1
git log --oneline

# 4. revert: 안전하게 되돌리기 (비공유 브랜치라면 reset 대신 revert 사용)
git revert HEAD
git log --oneline
```

---

## 작업 순서

```
1단계: `01_quick_setup.md` — 강의 자료 URL + Fork 과정 추가
2단계: Fork 이미지 다운로드 (`https://git-fork.com/images/image1.jpg` → `./image/fork.png`)
3단계: `02_git.md` — SourceTree, Fork 소개 + 이미지 + URL 추가
4단계: `03_start_new_feature.md` — Fork 단락 제거 + 실습용 repo init 과정 + git restore 실습 추가
5단계: `04_conflict.md` — 인위적 충돌 생성 및 해결 실습 추가
6단계: `06_reset_revert.md` — reset / revert 단계별 실습 추가
```

---

> 각 단계 실행 시 명확히 지시해주시면 해당 항목만 수정하겠습니다.
