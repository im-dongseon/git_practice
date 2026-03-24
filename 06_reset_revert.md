# 잘못된 변경 되돌리기 (Reset / Revert)

* 실수한 커밋을 되돌리고 싶다

---

## git checkout \<file\> — 단일 파일 되돌리기

* 아직 `git add`를 하지 않은 파일을 마지막 커밋 상태로 되돌리기

```bash
git checkout <file>
```

---

## git reset — 커밋 이력 되돌리기

* 로컬에서 아직 push하지 않은 커밋을 되돌릴 때 사용

```bash
git reset --hard HEAD~1
```

### --soft / --mixed / --hard 옵션 비교

| 옵션 | 커밋 이력 | Staging Area (Index) | Working Directory |
|------|-----------|----------------------|-------------------|
| `--soft` | 되돌림 | 유지 (변경 내용 staged 상태) | 유지 |
| `--mixed` (기본값) | 되돌림 | 초기화 (변경 내용 unstaged) | 유지 |
| `--hard` | 되돌림 | 초기화 | 초기화 (변경 내용 삭제!) |

> ⚠️ `--hard` 는 작업 내용이 완전히 삭제되므로 신중하게 사용

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
| 단일 파일만 되돌리고 싶을 때 | `git checkout <file>` |

---

## 실습 (Reset / Revert)

* 커밋 이력을 직접 되돌려보며 각각의 차이점을 확인합니다.

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
