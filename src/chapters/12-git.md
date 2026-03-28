# Git 연동하기
저 역시 오랫동안 Git CLI(터미널 명령어)만 고집해 왔지만, Neovim의 강력한 Git 플러그인들을 경험한 뒤로는 완전히 정착했습니다. 편집기를 떠나지 않고도 Git의 모든 기능을 직관적으로 활용할 수 있는 핵심 도구들을 소개합니다.

---

## [Fugitive](https://github.com/tpope/vim-fugitive)
Vim의 Git 플러그인 중 단연 독보적인 존재입니다. `:G` 명령어 하나로 Git의 모든 기능을 편집기 내에서 실행할 수 있습니다.

특히 아무 인자 없이 `:G`를 입력하면 나타나는 **대화형 상태(Status) 창**이 백미입니다. 파일들의 변경 사항을 확인하고, `s` 키로 스테이징하거나 `cc`로 커밋하는 등 매우 빠르고 간편한 워크플로를 제공합니다.

---

## [Gitsigns](https://github.com/lewis6991/gitsigns.nvim)
코드의 줄 번호 옆에 현재 변경 사항(Hunk)을 실시간으로 표시해 줍니다.
단축키로 헝크 단위로 이동하거나, 즉석에서 스테이징/되돌리기/미리보기가 가능해 작업 중인 코드의 상태를 파악하기에 최적입니다.

---

## [Git blame](https://github.com/f-person/git-blame.nvim)
현재 줄을 누가, 언제, 어떤 커밋으로 수정했는지 상태 표시줄이나 코드 옆에 조용히 보여줍니다. 협업 시 "이 코드는 왜 이렇게 짜였을까?"라는 궁금증을 즉각 해소해 주는 유용한 도구입니다.

---

## Git 로그 탐색 (git log)
[vim-flog](https://github.com/rbong/vim-flog)는 Git의 커밋 히스토리를 아름다운 그래프 형태로 보여줍니다.
로그에서 바로 엔터를 눌러 상세 diff를 확인하거나, 대화형 리베이스(Rebase)를 수행하는 등 로그 탐색 그 이상의 기능을 제공합니다.

---

## [Diffview](https://github.com/sindrets/diffview.nvim)
복잡한 변경 사항(Diff)을 한눈에 파악하기 위한 최고의 도구입니다.
여러 파일의 변경 사항을 사이드바와 함께 보여주며, 파일의 히스토리 탐색이나 충돌(Conflict) 해결 상황에서도 압도적인 가독성을 자랑합니다.

---

## 헝크 기록 (Hunk History)
가끔 `git blame`을 봐도 그저 "들여쓰기 수정" 같은 사소한 커밋만 남겨져 있어 답답할 때가 있죠.
[git-messenger.vim](https://github.com/rhysd/git-messenger.vim)은 해당 위치의 **이전 커밋 기록**들을 거슬러 올라가며 보여줍니다. 이 코드가 진짜 어떤 의도로 처음 작성되었는지 파악하는 데 결정적인 도움을 줍니다.
