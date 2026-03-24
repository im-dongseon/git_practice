# Quick setup

> 강의 자료 저장소: https://github.com/im-dongseon/git_practice

## 1. 강의 자료 Fork 하기

* GitHub에서 강의 저장소에 접속 후 내 계정으로 Fork

1. https://github.com/im-dongseon/git_practice 접속
2. 우측 상단 **Fork** 버튼 클릭 → 내 계정에 복제본 생성

* Fork한 내 저장소를 로컬로 clone

```shell
git clone https://github.com/{your-id}/git_practice.git
cd git_practice
```

* 원본 강의 저장소를 `upstream`으로 등록 (강의 자료 업데이트 수신용)

```shell
git remote add upstream https://github.com/im-dongseon/git_practice.git
git remote -v
```

---

## 2. 새 저장소 직접 만들기 (선택)

```shell
echo "# git_practice" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/{your-id}/git_practice.git
git push -u origin main
```

OR

```shell
mkdir git_practice
cd git_practice
git clone https://github.com/{your-id}/git_practice.git .
```



## Personal access tokens (classic)

* GitHub는 보안상 비밀번호 대신 **Personal Access Token(PAT)**을 사용하여 인증
* HTTPS로 push/pull 할 때 비밀번호 대신 PAT를 입력

**발급 방법**
1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. `Generate new token` 클릭
3. `repo` 권한 체크 후 토큰 생성
4. 생성된 토큰을 복사해두기 (다시 보기 불가)

![001](./image/001.png)
