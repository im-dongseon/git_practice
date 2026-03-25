# 새로운 기능 개발 시작

## 1. 실습용 repo 준비

> 실습을 위한 개인 저장소를 만들고 초기화합니다.

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

---

## 2. 작업 중인 변경 사항 되돌리기 (git restore)

* **언제 사용?** `git add` 전/후 수정된 파일을 이전 상태로 되돌릴 때

| 상황 | 명령어 |
|------|--------|
| 작업 중 파일을 마지막 커밋 상태로 되돌리기 (unstaged) | `git restore <file>` |
| staged 상태인 파일을 unstaged로 되돌리기 | `git restore --staged <file>` |

### 실습

```shell
# 1. 파일 수정 후 실수로 되돌리고 싶을 때
echo "wrong content" >> README.md
git restore README.md

# 2. git add 한 파일을 unstaged로 되돌리고 싶을 때
echo "test content" >> README.md
git add README.md
git restore --staged README.md
```

---

## 기능 단위 브랜치 생성

```bash
git branch feature/add-profile
git switch feature/add-profile
```

* 또는 아래 명령어로 브랜치 생성과 이동을 한 번에 처리 가능

```bash
git switch -c feature/add-profile
```

* 예전 방식 Git에서는 아래처럼 `git checkout`으로 브랜치 생성/이동을 함께 처리하기도 했습니다.

```bash
git checkout -b feature/add-profile
```

### 확인

```bash
git log --graph --all --oneline
```

OR

```bash
git log --graph --simplify-by-decoration --pretty=format:'%d' --all
```

OR

![003](./image/003.png)

### Branch 란?

![005](./image/005.png)

* Branch : 가지, 분기

* 이해하기 쉽게 생각하면 평행세계
  ![006](./image/006.jpg)



## 기능 개발 중 변경사항 저장

```bash
echo "# profile" >> profile.md
git add .
git commit -m "add profile file"
git push origin feature/add-profile
```

## 코드 리뷰, 병합

* 팀원이 올린 PR(Pull Request)을 검토하고 병합 

  ```bash
  git merge feature/add-profile
  ```

  OR
  
  ```bash
  git cherry-pick {branch name or commit id}
  ```

### 🔀 git merge

* 두 브랜치 간의 공통 조상을 기준으로, **한 브랜치를 다른 브랜치에 통째로 합친다**.

  → merge commit 이 생성되며, 이력은 브랜치의 흐름을 유지.

* 프론트엔드와 백엔드를 나누어 작업을 하고, 기능 테스트를 위해 통합

* 서로 작업한 내역이 겹치면 **충돌(conflict)** 이 발생할 수 있음
* 다만 충돌이 난다고 병합이 불가능한 것은 아니며, 최종 결과를 정리해서 해결한 뒤 계속 진행 가능
* 역할이나 파일 범위를 나누어 작업하면 충돌 가능성을 줄일 수 있음

#### 예시

```bash
git switch main
git merge feature/login
```

![007](./image/007.png)

### 🍒 git cherry-pick

* 다른 브랜치의 **특정 커밋들만 선택해서 현재 브랜치에 복사하여 적용**

  → 적용한 커밋은 **새로운 해시 값을 가진 커밋**으로 생성 됨

#### 예시

```bash
git switch main
git cherry-pick abc1234
```

![008](./image/008.png)
