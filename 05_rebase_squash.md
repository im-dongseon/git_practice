# Conflict 를 줄이려면?

* PR / Merge 전에 원본의 변경 사항 확인
* 내 커밋을 원본의 최신 변경 사항 이후로 이동 (git rebase)

![014](./image/014.png)

---

# git rebase

* 내 브랜치의 커밋들을 **대상 브랜치의 최신 커밋 이후로 재배치**

  → 마치 원본에서 새로 작업을 시작한 것처럼 이력이 깔끔해짐
* 단, rebase는 **기존 커밋을 다시 만드는 작업**이라 커밋 해시가 바뀌는 **이력 재작성(history rewrite)** 입니다.
* 이미 다른 사람과 공유한 브랜치에서 무분별하게 rebase하면 협업 이력이 꼬일 수 있으므로, 보통은 **개인 브랜치** 또는 **PR 정리 단계**에서 주로 사용합니다.

## 기본 사용법

* `main` 브랜치의 최신 변경을 내 브랜치에 적용하려면
* 이때 **현재 브랜치는 `main`이 아니라 내 작업 브랜치(feature 브랜치)** 여야 합니다.

```bash
git switch feature/my-branch
git rebase main
```

## rebase 도중 충돌 처리

* rebase 중 충돌이 발생하면 아래 순서로 처리

```bash
# 1. 충돌 파일 직접 수정 후
git add <파일>

# 2. rebase 계속 진행
git rebase --continue

# 3. rebase 중단 (원래 상태로 되돌리기)
git rebase --abort

# 4. 현재 커밋 건너뛰기
git rebase --skip
```

---

# 커밋 정리 (Interactive Rebase / Squash)

* PR 전에 커밋 정리 필요 — 작업 중 쌓인 불필요한 커밋을 정리해서 깔끔하게 만들기

## git rebase -i (Interactive Rebase)

![010](./image/010.png)

* 최근 N개의 커밋을 대화형으로 편집

```bash
git rebase -i HEAD~3
```

* 실행 후 에디터가 열리며 아래와 같은 화면이 표시됨

```
pick abc1111 feat: 로그인 UI 구현
pick abc2222 fix: 타이포 수정
pick abc3333 refactor: 불필요한 주석 제거
```

* 각 줄의 `pick` 을 아래 키워드로 변경하여 동작을 지정

| 키워드 | 약어 | 설명 |
|--------|------|------|
| `pick` | `p` | 커밋 유지 (기본값) |
| `squash` | `s` | 이전 커밋에 합치기 (커밋 메시지 편집 가능) |
| `fixup` | `f` | 이전 커밋에 합치기 (커밋 메시지 버림) |
| `reword` | `r` | 커밋 메시지 수정 |
| `drop` | `d` | 커밋 삭제 |

## git merge --squash

![011](./image/011.png)

* feature 브랜치의 모든 커밋을 **하나의 커밋으로 합쳐 현재 브랜치에 병합**

```bash
git switch main
git merge --squash feature/add-profile
git commit -m "feat: 프로필 기능 추가"
```

## rebase -i vs merge --squash 차이

| 항목 | `rebase -i` | `merge --squash` |
|------|-------------|------------------|
| 대상 | 내 브랜치 커밋 재편집 | 다른 브랜치를 하나로 합쳐 병합 |
| 이력 | 커밋 이력 재작성 | 단일 커밋으로 통합 |
| 주요 용도 | PR 전 커밋 정리 | 브랜치 병합 시 이력 단순화 |

---

## 실습 시나리오 — 3개 커밋을 1개로 합치기

```bash
# 1. 실습용 브랜치 생성 후 커밋 3개 만들기
git switch -c practice/squash
echo "A" >> test.txt && git add . && git commit -m "작업 A"
echo "B" >> test.txt && git add . && git commit -m "작업 B"
echo "C" >> test.txt && git add . && git commit -m "작업 C"

# 2. 최근 3개 커밋 interactive rebase 시작
git rebase -i HEAD~3

# 3. 에디터에서 2~3번째 커밋의 pick → squash 로 변경 후 저장
# pick abc1111 작업 A
# squash abc2222 작업 B
# squash abc3333 작업 C

# 4. 최종 커밋 메시지 입력 후 저장

# 5. 결과 확인
git log --oneline
```

---

* 이미 만든 커밋이나 변경을 되돌려야 하는 경우는 다음 문서 `06_reset_revert.md` 에서 이어집니다.
