# Git 강의 자료 수정 계획서

> 작성일: 2026-03-24  
> 수정 완료: 2026-03-24  
> 근거 문서: [`review_2026_03_24.md`](./review_2026_03_24.md)  
> 상태: ✅ **전체 완료** (1~4단계 모두 적용 완료)

---

## 우선순위 분류

| 우선순위 | 기준 |
|----------|------|
| 🔴 P1 — 즉시 | 다른 환경에서 강의 자료가 동작하지 않는 버그 |
| 🟡 P2 — 단기 | 핵심 내용 누락으로 학습 목표 달성 불가 |
| 🟢 P3 — 장기 | 보완하면 좋으나 없어도 무방한 심화 내용 |

---

## ✅ P1 — 즉시 수정 완료 (버그)

### 1. 이미지 절대 경로 → 상대 경로 변환

**대상 파일**
- `02_git.md`
- `06_reset_revert.mkd`

**문제**  
이미지 경로가 `/Users/1004790/workspace/...` 로 하드코딩되어 있어, 다른 PC에서 강의 자료를 열면 이미지가 깨짐.

**수정 내용**

| 파일 | 현재 경로 | 변경 경로 |
|------|-----------|-----------|
| `02_git.md` | `/Users/1004790/workspace/git_practice/image/002.png` | `./image/002.png` |
| `06_reset_revert.mkd` | `/Users/1004790/workspace/git_practice/image/012.webp` | `./image/012.webp` |
| `06_reset_revert.mkd` | `/Users/1004790/workspace/git_practice/image/013.png` | `./image/013.png` |

---

### 2. 파일 확장자 `.mkd` → `.md` 변환

**대상 파일**
- `06_reset_revert.mkd` → `06_reset_revert.md`
- `07_tip.mkd` → `07_tip.md`

**문제**  
`.mkd`는 비표준 확장자로, 일부 에디터·뷰어에서 마크다운으로 인식하지 못할 수 있음.  
나머지 파일(.md)과 통일성 확보 필요.

**수정 방법**: 파일명 변경(rename), 내용은 그대로 유지.

---

## ✅ P2 — 단기 보강 완료 (핵심 내용 누락)

### 3. `05_rebase_squash.md` — 대폭 보강

**현 상태**: 21줄, 명령어만 나열, 실습 없음  
**목표**: `git rebase -i` 실제 동작 흐름 + 실습 시나리오 추가

**추가할 내용**
1. `git rebase -i HEAD~N` 실행 후 에디터 화면 설명
   - `pick` / `squash` / `fixup` / `reword` 옵션 비교표
2. **rebase vs merge --squash 차이** 설명
   - rebase: 커밋 이력 재작성 / squash: 단일 커밋으로 합치기
3. rebase 도중 충돌 처리 절차
   - `git rebase --continue` / `--abort` / `--skip`
4. 단계별 실습 시나리오 (3개 커밋 → 1개로 squash하기)

---

### 4. `06_reset_revert.md` — reset 옵션 상세 설명 추가

**현 상태**: reset/revert 명령어만 제시, 옵션 차이 없음  
**목표**: 옵션별 차이 및 상황별 사용 기준 제시

**추가할 내용**
1. `git reset` 3가지 옵션 비교

   | 옵션 | 커밋 이력 | Staging Area | Working Dir |
   |------|-----------|--------------|-------------|
   | `--soft` | 되돌림 | 유지 | 유지 |
   | `--mixed` (기본) | 되돌림 | 초기화 | 유지 |
   | `--hard` | 되돌림 | 초기화 | 초기화 |

2. **언제 reset vs revert?** 판단 기준
   - 로컬 전용(push 전) → `git reset`
   - 공유 브랜치(이미 push) → `git revert`
3. `git checkout <file>` — 단일 파일 되돌리기 설명

---

### 5. `04_conflict.md` — 충돌 해결 절차 추가

**현 상태**: conflict 발생 및 abort만 설명, 실제 해결 절차 없음  
**목표**: 충돌 발생 → 편집 → 완료 전체 흐름 추가

**추가할 내용**
1. conflict 마커 구조 설명
   ```
   <<<<<<< HEAD (내 변경)
   =======
   >>>>>>> feature/xxx (상대방 변경)
   ```
2. 해결 단계
   - 에디터에서 원하는 코드 선택하여 저장
   - `git add <파일>` → `git commit`
3. VSCode의 충돌 해결 UI 활용 방법 (Accept Current / Accept Incoming / Accept Both)
4. `git diff` 로 충돌 내용 미리 확인하는 방법

---

## ✅ P3 — 장기 심화 완료 (선택 사항)

### 6. 신규 챕터 추가 및 파일 넘버링 조정

> 💡 현재 `07_tip.mkd`는 `98_tip.md`로 변경하여 부록 영역으로 이동. 신규 챕터는 `07`번부터 순차 배치.

| 주제 | 설명 | 예상 파일명 |
|------|------|-------------|
| `.gitignore` | 버전 관리 제외 파일 설정, 실무 필수 | `07_gitignore.md` |
| `git tag` | 릴리즈 버전 태그 관리 | `08_tag.md` |
| GitHub Flow | Git Flow 외 경량 워크플로우 비교 | `99_etc.md` 에 추가 |

**파일 이동/변경**
- `07_tip.mkd` → `98_tip.md` (부록으로 이동, 확장자 동시 수정)

### 7. 기존 파일 소규모 개선

| 파일 | 개선 내용 |
|------|-----------|
| `01_readme.md` | 강사 소개 내용을 `00_instructor.md` 로 분리 + PAT 발급 절차 텍스트 추가 |
| `02_git.md` | GUI 도구 다양화 언급 (Fork, SourceTree, **VSCode GitLens/Git Graph 확장기능** 포함) |
| `03_start_new_feature.md` | `git checkout -b` 단축 명령어 소개 |
| `98_tip.md` | `git stash -u` 옵션, `stash branch` 명령어 추가 |
| `99_etc.md` | Commit Message 실제 예시 추가 |

**신규 파일**
- `00_instructor.md` : 강사 소개 전용 파일 (현재 `01_readme.md` 상단 소개 내용 이동)

### 8. 명령어 작성 원칙 추가 (전체 파일 공통)

> 새로운 명령어를 추가하는 경우, 명령어 블록 앞에 반드시 **용도/상황을 설명하는 소개 문구**를 함께 작성한다.

**예시**
```
❌ 현재 방식
git stash -u

✅ 개선 방식
* untracked 파일(새로 생성했지만 아직 git add 하지 않은 파일)까지 함께 stash에 저장하려면
git stash -u
```

---

## 작업 순서 (권장)

```
1단계 (P1): 파일 확장자 변경 (.mkd → .md) → 이미지 경로 수정 (절대 → 상대)
2단계 (P1+): 07_tip.mkd → 98_tip.md 이동 / 00_instructor.md 신규 생성
3단계 (P2): 05_rebase_squash.md 보강 → 06_reset_revert.md 보강 → 04_conflict.md 보강
4단계 (P3): 기존 파일 소규모 개선 (명령어 소개 문구 포함) → 신규 챕터 추가
```

---

> 각 단계 실행 시 명확히 지시해주시면 해당 항목만 수정하겠습니다.
