# P1. status 네 상태 — `a.txt`, `b.txt`, `README.md` — `p1: file states`

Git 은 폴더 안의 파일을 네 가지 상태로 봅니다.
- untracked — 아직 Git 이 모르는 파일
- unmodified — 마지막 커밋과 같음
- modified — 고쳤지만 add 안 함
- staged — add 해서 다음 커밋에 들어갈 준비가 됨

`git status` 는 이 상태를 보여 주는 명령이고, 앞으로 모든 문제에서 가장 자주 치게 됩니다.

이 문제에서 하는 것: **네 상태를 일부러 하나씩 만들어 `status` 출력이 어떻게 달라지는지 봅니다.**

1. VS Code 에서 새 파일 `a.txt` 를 만들고 아무 내용이나 한 줄 적고 저장합니다. **add 는 하지 않습니다.** 이 파일은 Git 이 아직 모르는 상태(untracked)입니다.
2. VS Code 에서 `README.md` 를 열고, `# oss-week05` 아래에 `Week 5 practice` 한 줄을 적고 저장합니다(`Ctrl+S`). **add 는 하지 않습니다.** 이미 커밋된 파일을 고쳤으니 modified 입니다.
3. 새 파일 `b.txt` 를 만들고 저장한 뒤, 터미널에서 add 합니다. 이 파일은 staged 입니다.
   ```
   git add b.txt
   ```
4. 터미널에서 짧은 형식의 status 를 칩니다.
   ```
   git status --short
   ```
   아래처럼 나와야 합니다. 파일마다 앞에 두 글자가 붙는데, **왼쪽 글자는 인덱스(add 된 것)의 상태, 오른쪽 글자는 작업 폴더의 상태**입니다. `A ` 는 add 됨(staged), ` M` 은 고쳤지만 add 안 함(modified), `??` 는 Git 이 모르는 파일(untracked)입니다.
   ```
   $ git status --short
    M README.md
   A  b.txt
   ?? a.txt
   ```
5. 출력을 읽으면 이렇게 됩니다.
   - `?? a.txt` — untracked. 1번에서 만들고 add 하지 않았다.
   - ` M README.md` — modified. 2번에서 고치고 add 하지 않았다.
   - `A  b.txt` — staged. 3번에서 add 했다.
   - 네 번째 상태 unmodified 는 **목록에 아예 안 나옵니다.** 마지막 커밋과 같아서 보고할 것이 없기 때문입니다. 다음 단계에서 봅니다.
   자기 화면의 세 줄이 이와 같으면 됩니다. 다르면 1~3번 중 add 를 했거나 안 했거나가 뒤바뀐 것입니다.

6. 세 파일을 전부 add 하고 status 를 다시 봅니다.
   ```
   git add .
   git status --short
   ```
   세 줄이 전부 **왼쪽 글자**(`A `, `M `)로 옮겨 갔습니다. add 는 "다음 커밋에 넣을 준비" 이고, 어느 상태에서든 add 하면 staged 가 됩니다.
7. 커밋하고 status 를 한 번 더 봅니다.
   ```
   git commit -m "p1: file states"
   git status --short
   ```
   **아무것도 안 나옵니다.** 세 파일이 전부 마지막 커밋과 같아졌으니 이제 전부 unmodified 이고, unmodified 는 표시되지 않습니다.

---

[← 문제 목록](../README.md#문제) · [이전: P0](P0_setup.md) · [다음: P2](P2_gitignore.md) · [부록: 흔한 오류](../README.md#부록-흔한-오류)
