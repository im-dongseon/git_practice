# 충돌(conflict) 해결

* 두 명이 같은 파일의 같은 부분을 수정하면 병합 시 충돌 발생

```bash
git merge main
```

OR

```bash
git cherry-pick {branch name or commit id}
```

---

## 충돌 발생 확인

* conflict 표시 확인(`<<<<<<<`, `=======`, `>>>>>>>`)

![009](./image/009.png)

* 충돌이 발생한 파일은 아래와 같이 마커로 구분됨

```
<<<<<<< HEAD
내가 수정한 내용 (현재 브랜치)
=======
상대방이 수정한 내용 (병합하려는 브랜치)
>>>>>>> feature/xxx
```

* `git diff`로 충돌 내용 미리 파악하기

```bash
git diff
```

---

## 충돌 해결 절차

1. **충돌 파일을 에디터에서 열어 원하는 내용만 남기고 저장**

   * 직접 편집: `<<<<<<<`, `=======`, `>>>>>>>` 마커를 모두 제거하고 최종 코드만 유지

2. **VSCode 활용** — 충돌 영역 위에 버튼이 자동으로 표시됨

    | 버튼 | 설명 |
    |------|------|
    | `Accept Current Change` | 내 변경 내용 채택 |
    | `Accept Incoming Change` | 상대방 변경 내용 채택 |
    | `Accept Both Changes` | 두 내용 모두 유지 |
    | `Compare Changes` | 두 버전 비교 |

   * 실제 실무에서는 둘 중 하나만 고르기보다, 두 변경을 참고해서 **최종 결과를 다시 정리하는 방식**이 더 자주 필요합니다.

3. **해결 완료 후 커밋**

```bash
# 해결한 파일을 staged 상태로 올리기
git add <파일>

# 충돌 해결 커밋 생성
git commit
```

4. **결과 확인**

```bash
git status
git log --graph --oneline --all
```

---

## 실습: 충돌 직접 만들어보고 해결하기

* `main` 브랜치와 `feature/add-profile` 브랜치에서 같은 파일을 수정하여 인위적으로 충돌을 발생시킵니다.

```shell
# 1. main 브랜치에서 README.md 변경
git switch main
echo "main의 변경" >> README.md
git add README.md && git commit -m "main: README 수정"

# 2. feature 브랜치에서 같은 위치(마지막 줄)에 다른 내용 추가
git switch feature/add-profile
echo "feature의 변경" >> README.md
git add README.md && git commit -m "feature: README 수정"

# 3. 브랜치 병합 시도 → 충돌 발생!
git switch main
git merge feature/add-profile

# 4. 파일 상태 확인 및 충돌 발생 파일(README.md) 열기
git status

# 5. 에디터에서 <<<<<<<, =======, >>>>>>> 마커를 지우고 내용을 하나로 합쳐서 저장

# 6. 충돌 해결을 Git에 알리고 병합 완료하기
git add README.md
git commit

# 7. 병합 결과 확인
git status
git log --graph --oneline --all
```

---

## 병합/cherry-pick 중단

* merge/cherry-pick 중단 (해결 포기 시)

```bash
git merge --abort
```

OR

```bash
git cherry-pick --abort
```

* 상태 확인

```bash
git status
```
