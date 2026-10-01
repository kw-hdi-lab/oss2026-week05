# 5주차 실습 — Branches, Undo, and Remotes

오늘은 브랜치를 만들고 합치고, 잘못된 커밋을 되돌리고, 원격과 어긋난 히스토리를 맞추는 것까지를 **한 저장소 안에서** 해 봅니다. 마지막에는 그 저장소를 Node 프로젝트로 만들어 패키지 하나를 설치해 봅니다.
막히면 맨 아래 **부록: 흔한 오류**를 먼저 보고, 그래도 안 되면 손을 드세요.

- **문제**: P0 부터 P8 까지, 순서대로. 문제마다 파일이 따로 있고 아래 표에서 엽니다.
- **확인 방법**: 평소와 같습니다. `<본인 GitHub ID>/oss-week05` 저장소의 파일·커밋·브랜치를 봅니다.
- **네트워크**: P0·P6·P7 의 GitHub, P8 의 `npm install` 에서 필요합니다. 나머지는 전부 로컬에서 됩니다.

이번 주는 **템플릿을 복사하지 않습니다.** 빈 폴더에서 `git init` 으로 저장소를 직접 만들고, GitHub 에 빈 저장소를 만들어 연결합니다. 이 README 는 문제지일 뿐이니 clone 하지 마세요.

## 규칙

- 저장소 이름은 정확히 **`oss-week05`**, Public. (확인 스크립트가 이 이름을 찾습니다.)
- 문제마다 지정된 **커밋 메시지**를 그대로 씁니다. 예: `p1: file states`. 따로 제출하는 파일은 없습니다. 저장소의 커밋과 파일이 곧 답안입니다.
- 마지막 단계는 항상 **눈으로 확인**입니다. 확인이 안 되면 그 문제는 끝난 게 아닙니다.
- **push 는 문제지가 하라고 할 때만 합니다.** P3·P5 에서 커밋을 고치고 지우는 연습을 하는데, 이미 push 한 커밋을 고치면 다음 push 가 거부됩니다. 첫 push 는 P6 입니다.

쓰는 Git 명령은 이론 강의에 나온 것뿐입니다: `init`, `config`, `status`, `add`, `commit`(`-m`, `-a`, `--amend`), `restore`, `rm --cached`, `.gitignore`, `branch`, `checkout`, `merge`, `log`, `reset`, `reflog`, `revert`, `remote`, `fetch`, `push`, `pull`. P8 에서만 `npm init`, `npm install` 을 씁니다.

---

## 문제

| # | 문제 | 남는 것 |
|---|---|---|
| [P0](problems/P0_setup.md) | [처음부터 만들기](problems/P0_setup.md) | 커밋 `chore: init project`, 원격 `origin` |
| [P1](problems/P1_status.md) | [status 네 상태](problems/P1_status.md) | 커밋 `p1: file states` |
| [P2](problems/P2_gitignore.md) | [.gitignore](problems/P2_gitignore.md) | 커밋 `oops: add secret`, `p2: gitignore`, `.gitignore` |
| [P3](problems/P3_undo.md) | [되돌리기 ① restore 와 amend](problems/P3_undo.md) | 커밋 `p3: undo` (`notes.txt` 포함) |
| [P4](problems/P4_branch.md) | [브랜치·머지·충돌](problems/P4_branch.md) | 커밋 `feat: …` 셋 + 머지 커밋, `greeting.txt` |
| [P5](problems/P5_reset.md) | [되돌리기 ② reset 과 reflog](problems/P5_reset.md) | 커밋 `sandbox: one`·`two`·`three`, `sandbox/` |
| [P6](problems/P6_revert.md) | [되돌리기 ③ revert](problems/P6_revert.md) | 커밋 `mistake: bad line` + `Revert "…"` |
| [P7](problems/P7_remote.md) | [원격 충돌](problems/P7_remote.md) | 커밋 `web: edit greeting`, `local: edit greeting` + 머지 커밋 |
| [P8](problems/P8_node.md) | [Node 프로젝트 처음부터](problems/P8_node.md) | 커밋 `p8: …` 셋, `package.json`, `package-lock.json`, `main.js` |

## 끝날 때 갖춰져 있어야 하는 상태

- `<ID>/oss-week05` 가 Public 으로 있고 이름이 정확히 `oss-week05`
- 위 표의 커밋이 전부 있고 push 됨 (GitHub 커밋 목록에서 확인)
- `git status --short` 가 비어 있음, `git branch` 에 `main` 만
- GitHub 에 `secret.txt` 는 마지막 커밋에 없음 (`oops` 커밋에는 있어도 됨), `node_modules/` 없음, `package-lock.json` 은 있음
- `git log --oneline --graph` 에 머지 커밋이 둘 (P4, P7)

---

## 부록: 흔한 오류

| 증상 | 원인 → 해결 |
|---|---|
| `fatal: not a git repository` | 저장소 폴더 밖에서 실행. `pwd` 로 위치 확인 → `cd oss-week05` |
| `Author identity unknown` / `Please tell me who you are` | `user.name`·`user.email` 미설정 → P0 3번의 `git config --global` 두 줄 |
| P0 의 push 가 `! [rejected]` … `remote contains work that you do not have` | GitHub 에서 저장소를 만들 때 "Add a README" 를 체크함 → GitHub 저장소를 지우고 **README 없이** 다시 만들기 |
| 커밋했더니 편집기가 열림 | `-m` 없는 commit, 머지, revert 는 원래 열립니다. VS Code 면 `Ctrl+S` 뒤 탭 닫기. 검은 화면의 Vim 이면 `Esc` → `:wq` Enter. 취소는 `:q!` |
| `.gitignore` 에 넣었는데 `status` 에 계속 나옴 | 이미 추적 중인 파일 → `git rm --cached <file>` (P2) |
| 브랜치가 `master` 로 만들어짐 | `init.defaultBranch` 미설정 → `git branch -M main` 한 번 |
| `checkout` 이 `Your local changes would be overwritten` 으로 거부됨 | 커밋 안 한 수정이 있음 → 먼저 커밋하고 옮기기 |
| 머지 뒤 파일에 `<<<<<<<` 가 남아 있음 | 마커를 안 지우고 add·commit 함 → 파일을 고쳐 다시 커밋 (P4 13번) |
| 머지 중에 뭐가 뭔지 모르겠음 | `git merge --abort` 로 머지 전으로 돌아가 다시 시작 |
| `git restore` 했는데 안 돌아옴 | add 한 뒤 고친 거라면 restore 는 **인덱스 내용**으로 돌림. 커밋 내용으로 돌리려면 `restore --staged` 먼저, 그 다음 `restore` |
| `reset --hard` 뒤 `HEAD@{1}` 이 엉뚱한 커밋임 | reset 뒤에 다른 명령을 쳤음. `git reflog` 에서 `commit: sandbox: three` 줄을 찾아 그 해시로 `git reset --hard <해시>` |
| P6 의 첫 push 가 `! [rejected]` (P0 은 됐는데) | P3·P5 에서 커밋을 고치기 **전에** 중간에 push 한 경우. 이번 저장소는 혼자 쓰므로 이번만 `git push --force`. 팀 저장소에서는 절대 안 됨 |
| P7 에서 pull 했는데 충돌이 안 남 | 웹과 로컬이 **같은 줄**을 고치지 않음 → 웹 커밋을 하나 더 만들어 같은 줄을 다시 고치고 반복 |
| P7 에서 `pull` 이 `divergent branches` 어쩌고로 멈춤 | `git config --global pull.rebase false` 한 번 실행 후 다시 `git pull` |
| P8 `node main.js` 가 `SyntaxError: Cannot use import statement outside a module` | `package.json` 의 `"type"` 이 `module` 이 아님 → P8 2번 |
| P8 `node main.js` 가 `Cannot find package 'chalk'` | `npm install chalk` 를 안 했거나 다른 폴더에서 실행함 → `pwd` 확인 후 저장소 폴더에서 `npm install chalk` |
| 한글 파일명·메시지가 깨져 보임 | `git config --global core.quotepath false` |
| `add` 할 때 `LF will be replaced by CRLF` 경고 | Windows 줄바꿈 안내일 뿐, 에러 아님. 그대로 진행 |
