# 응용프로그래밍개발 3조 프로젝트

---

# 팀 프로젝트 GitHub 사용법

## 1. 최초 작업 시 — 프로젝트 내려받기

1. Git을 설치하기 (https://git-scm.com/)
2. GitHub 레포지터에서 Code 페이지에서 **Code(파일 목록 상단 초록버) → HTTPS** 주소를 복사하기.
3. 사용할 컴퓨터 배경화면에 프로젝트용 새 폴더를 생성한 후, vsc 실행 후 터미널(ctrl + `)을 열어 git bash로 변경 후 해당 명령어 입력하기.

```bash
git clone 복사한 링크
```

커밋 작성자 정보를 아직 설정한적 없다면, 프로젝트 폴더에서 아래 예시를 본인 깃허브 이름과 GitHub에 등록된 이메일로 바꿔 명령어 입력하기.

```bash
git config user.name "내 이름"
git config user.email "me@example.com"
```

## 2. 새 작업을 시작하기 전 — 이슈 확인하고 담당자 지정하기

이슈(Issue)는 해야 할 작업을 적어두는 작업 카드.

1. GitHub 레포지터리의 Issues 탭에서 열린 이슈를 확인.
2. 진행할 이슈를 열어 작업 범위와 완료 기준을 체크. 예를 들어 #12 로그인 화면 추가라면 이슈 번호는 #12.
3. 오른쪽 Assignees에서 실제 작업할 사람을 지정. 본인이 맡으면 본인 계정을 선택.
4. 담당자가 정해지면 이슈 번호를 확인하고, 아래 단계에서 최신 main을 기준으로 작업 브랜치 만들기로 넘어가기.

## 3. 이슈 화면에서 작업 브랜치 만들기

1. 담당자로 지정된 이슈를 열고 오른쪽 **Development → Create a branch**를 누릅니다.
2. **Branch name**에 `feat/12-login-page`((기능 추가 - feat, 오류 수정 - fix) / (이슈 번호) - 작업한 기능)를 입력. 예를 들어 메뉴 오류 이슈가 `#15`라면 `fix/15-menu-button`.
3. 저장소는 팀 저장소를 선택. 이 가이드에서는 기본 브랜치인 `main`에서 작업 브랜치가 생성됨. **What's next**에서 로컬에서 작업하는 옵션을 선택한 뒤 **Create branch**를 누르기.
4. 내 컴퓨터의 프로젝트 폴더에서 `git status`를 실행. 이전 작업에서 아직 커밋하지 않은 변경사항이 있다면 먼저 정리한 뒤 아래 명령을 실행.

```bash
git fetch origin
git switch --track origin/feat/12-login-page
git branch --show-current
```

`git fetch origin`은 GitHub에서 만든 브랜치 정보를 가져옴. `git switch --track`은 내 컴퓨터에도 같은 이름의 브랜치를 만들고 그 브랜치로 이동. 처음에만 실행하고, 나중에 같은 작업으로 돌아올 때는 `git switch feat/12-login-page`를 사용. 마지막 줄에 `feat/12-login-page`가 나오면 작업을 시작.

## 4. 작업을 마쳤을 때 — 커밋하고 푸시하기

파일을 수정하고 프로젝트를 실행해 확인. 아래는 프로젝트 루트의 `index.html`을 수정한 예시. 실제로 수정한 파일 경로를 넣으세요. 올릴 파일이 여러 개라면 `git add` 뒤에 경로를 나열하면 됩.

```bash
git status
git diff
git add index.html
git diff --staged
git commit -m "로그인 화면 추가"
git push -u origin feat/login-page
```

- **커밋**은 선택한 변경사항을 내 컴퓨터의 Git 기록에 저장하는 단계입니다. **푸시**는 그 커밋을 GitHub에 올리는 단계입니다.
- `git diff --staged`에서 올릴 내용을 확인합니다. `.env`, 비밀번호, API 키 등은 커밋에 포함하지 않습니다.
- 해당 브랜치를 처음 올릴 때 `-u`를 붙입니다. 같은 브랜치의 다음 커밋부터는 `git push`만 실행하면 됩니다.
- HTTPS 인증 화면이 뜨면 초대를 수락한 GitHub 계정으로 로그인합니다.

## 4. GitHub에서 PR 올리기

**PR(Pull Request)** 은 내 작업 브랜치의 변경사항을 팀원이 확인하고 `main`에 합쳐 달라는 요청.

1. GitHub 저장소에서 **Compare & pull request**를 누릅니다. 버튼이 안 보이면 **Pull requests → New pull request**로 들어감.
2. **base**는 변경사항이 들어갈 `main`, **compare**는 내 작업 브랜치 `feat/login-page`로 설정.
3. 제목과 본문을 쓰고 **Create pull request**를 누릅니다. **Reviewers**에서 팀원에게 리뷰를 요청.

```markdown
## 변경한 내용
- 로그인 화면과 입력 폼을 추가했습니다.

## 확인한 방법
- 브라우저에서 화면을 열어 입력 칸과 버튼이 표시되는지 확인했습니다.
```

수정 요청을 받으면 **같은 작업 브랜치**에서 수정하고 다시 커밋한 뒤 `git push`합니다. 기존 PR에 변경사항이 자동으로 추가.

## 5. 리뷰하고 합치기

1. 팀원은 PR의 **Files changed**에서 변경사항을 보고, 필요하면 직접 실행해 확인.
2. 수정할 부분이 있으면 코멘트를 남기고, 확인이 끝났으면 승인.
3. 리뷰가 끝나면 GitHub에서 **Merge pull request**를 진행. 합친 작업 브랜치는 PR 화면에서 **Delete branch**로 정리할 수 있음.
4. 각자 프로젝트 폴더에서 `git switch main`과 `git pull --ff-only origin main`을 실행하면 합쳐진 코드가 내려옵니다. 다음 작업은 2번부터 반복.

[GitHub Flow 공식 문서](https://docs.github.com/en/get-started/using-github/github-flow) · [Pull Request 빠른 시작](https://docs.github.com/en/pull-requests/get-started/pull-request-quickstart)
