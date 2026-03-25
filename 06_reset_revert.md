# 잘못된 변경 되돌리기 (Reset / Revert)

* 실수한 커밋을 되돌리고 싶다

---

## 현재 권장 방식: git restore \<file\> — 단일 파일 되돌리기

* 아직 `git add`를 하지 않은 파일을 마지막 커밋 상태로 되돌리기

```bash
git restore <file>
```

---

## 예전 방식: git checkout \<file\> / git reset \<file\>

예전에는 `git checkout <file>` 로 파일을 되돌리고, `git reset <file>` 로 staging 상태를 풀어내는 방식도 많이 사용했습니다.

하지만 `git checkout` 은 **브랜치 이동**과 **파일 복구**를 모두 담당해서 처음 배우는 사람에게 혼란을 주기 쉬웠습니다. 그래서 Git 2.23부터 역할을 분리한 아래 명령이 추가되었습니다.

- 브랜치 이동: `git switch`
- 파일 복구: `git restore`

### 신규 방식 vs 구방식

| 목적 | 현재 권장 | 예전 방식 |
|------|-----------|-----------|
| 브랜치 이동 | `git switch main` | `git checkout main` |
| 브랜치 생성 + 이동 | `git switch -c feature/test` | `git checkout -b feature/test` |
| 작업 파일 되돌리기 | `git restore <file>` | `git checkout <file>` |
| staged 해제 | `git restore --staged <file>` | `git reset <file>` |

강의에서는 앞으로 **브랜치 관련 동작은 `git switch`**, **파일 되돌리기는 `git restore`** 기준으로 이해하는 것을 권장합니다.

---

## git reset — 커밋 이력 되돌리기

* 로컬에서 아직 push하지 않은 커밋을 되돌릴 때 사용
* 특히 `git reset --hard` 는 **커밋 이력뿐 아니라 작업 파일까지 삭제**하므로, 실습 저장소에서 충분히 이해한 뒤에만 사용하세요.

```bash
git reset --hard HEAD~1
```

### --soft / --mixed / --hard 옵션 비교

| 옵션 | 커밋 이력 | Staging Area (Index) | Working Directory |
|------|-----------|----------------------|-------------------|
| `--soft` | 되돌림 | 유지 (변경 내용 staged 상태) | 유지 |
| `--mixed` (기본값) | 되돌림 | 초기화 (변경 내용 unstaged) | 유지 |
| `--hard` | 되돌림 | 초기화 | 초기화 (변경 내용 삭제!) |

> ⚠️ `--hard` 는 작업 내용이 완전히 삭제되므로 신중하게 사용하세요. 이미 중요한 작업이 있는 저장소에서는 특히 주의가 필요합니다.

```bash
# 마지막 커밋 취소, 변경 내용은 staged 상태로 유지
git reset --soft HEAD~1

# 마지막 커밋 취소, 변경 내용은 unstaged 상태로 유지 (기본값)
git reset --mixed HEAD~1

# 마지막 커밋 취소 + 변경 내용 완전 삭제
git reset --hard HEAD~1
```

* reset

![012](./image/012.webp)

---

## git revert — 커밋을 안전하게 되돌리기

* 이미 `push`한 커밋을 되돌릴 때 사용
* 되돌리는 새로운 커밋을 생성하므로 **팀원의 이력을 손상시키지 않음**

```bash
git revert <commit-hash>
```

* revert

![013](./image/013.png)

---

## 언제 reset vs revert?

| 상황 | 권장 명령어 |
|------|-------------|
| 아직 push 전, 로컬에서만 작업 중 | `git reset` |
| 이미 push하여 팀원과 공유된 브랜치 | `git revert` |
| 단일 파일만 되돌리고 싶을 때 | `git restore <file>` |

---

## 실습 (Reset / Revert)

* 커밋 이력을 직접 되돌려보며 각각의 차이점을 확인합니다.
* 아래 실습은 **실습용 저장소에서만** 진행하세요. 특히 `git reset --hard` 는 복구가 어려울 수 있습니다.

```shell
# 0. 실습을 위한 3개의 커밋 생성
echo "A" >> README.md && git add . && git commit -m "commit A"
echo "B" >> README.md && git add . && git commit -m "commit B"
echo "C" >> README.md && git add . && git commit -m "commit C"

# 1. --soft: 커밋 이력은 사라지지만, 방금 수정한 'C'의 내용은 파일에 그대로 있고 추가 대기(staged) 상태 유지
git reset --soft HEAD~1
git status

# 다시 커밋하여 원래 상태로 복구
git commit -m "commit C restored"

# 2. --mixed: 커밋 이력 사라짐, 파일 내용은 그대로 유지되나 staged 상태가 풀림 (다시 git add 필요)
git reset --mixed HEAD~1
git status

# 다시 추가 및 커밋하여 원래 상태로 복구
git add . && git commit -m "commit C restored"

# 3. --hard: 커밋 이력도 사라지고 파일 내용 'C' 도 완전 삭제됨 (복구 불가!)
git reset --hard HEAD~1
git log --oneline

# 4. revert: 이전 커밋 상태로 파일을 되돌리는 새로운 커밋 생성
git revert HEAD
git log --oneline
```
