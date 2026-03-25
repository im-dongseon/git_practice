# git stash

> 본편 학습 후 읽으면 좋은 실무 보조 기능 모음입니다.

* **작업 중이던 변경사항(수정된 파일, 추가된 파일 등)을 임시로 저장해두고 작업 공간을 깨끗하게 리셋**
* 보통 **다른 브랜치로 잠깐 이동하거나 긴급 이슈를 처리해야 할 때** 유용하게 사용
* 현재 작업 중인 변경사항을 **스택에 저장(stash)** 후, 나중에 꺼내서(pop/apply) 이어서 작업할 수 있음
* 변경사항은 커밋으로 저장하지 않기 때문에, **히스토리에 영향을 주지 않음**.

```bash
git stash
git stash push -m "작업 내용 설명"
git stash list

# 적용 + stash 삭제
git stash pop

# 적용 + stash 목록 유지
git stash apply stash@{0}

# 특정 stash 삭제
git stash drop stash@{1}

# 모든 stash 삭제
git stash clear
```

* untracked 파일(새로 생성되었지만 아직 `git add` 하지 않은 파일)까지 함께 stash에 저장하려면

```bash
git stash -u
```

* `git stash pop` 은 적용 후 stash 목록에서 제거하고, `git stash apply` 는 적용만 하고 목록은 남겨둡니다.
* 둘 다 적용 과정에서 충돌이 날 수 있으므로, 중요한 작업 위에 바로 적용할 때는 현재 상태를 먼저 확인하는 것이 안전합니다.

* stash로 저장한 내용을 새 브랜치로 바로 복원하려면 (충돌 없이 새로운 브랜치를 만들면서 적용)

```bash
git stash branch <branch-name>
```

# git commit --amend

* **가장 최근에 만든 커밋을 수정**

```bash
git add newfile.txt
git commit --amend
# OR
git commit --amend -m "수정된 커밋 메시지"
```

* ❗ 원격 저장소에 이미 push한 커밋을 amend하면?
  * git commit --amend는 **커밋 해시를 바꿔버리기 때문에**, 이미 원격에 푸시한 커밋을 amend하면 강제 푸시가 필요
  * 이미 다른 사람과 공유한 커밋이라면 이력이 꼬일 수 있으므로 특히 주의해야 함
  * `git push --force-with-lease` 는 원격에 내가 모르는 새 변경이 생겼는지 한 번 더 확인한 뒤 push해서, `--force` 보다 더 안전합니다.

```bash
git commit --amend
git push --force-with-lease
```

* 커밋을 깔끔하게 관리할 때 유용
  * 커밋 메시지 오타가 있을 때
  * 빠뜨린 파일을 뒤늦게 넣어야 할 때
  * 짧은 작업이니 별도의 커밋을 만들고 싶지 않을 때
  * PR 검토 후 커밋 정리할 때 (squash + amend 조합)
