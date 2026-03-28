# 기타 기능 및 마무리
이번 챕터에서는 앞서 다루지 못했던 유용한 플러그인들과 마무리 인사를 전해드립니다.

## 필수 IDE 기능 보완하기
Neovim은 순수 편집기에 가깝지만, 플러그인을 통해 완벽한 개발 환경으로 거듭납니다.

### 세션 및 편의 기능
* **[auto-session](https://github.com/rmagatti/auto-session)**: 작업 중이던 세션을 자동으로 저장하고 복구해 줍니다.
* **[nvim-lastplace](https://github.com/ethanholz/nvim-lastplace)**: 파일을 다시 열었을 때 마지막으로 편집했던 위치로 즉시 이동합니다.
* **[Comment.nvim](https://github.com/numToStr/Comment.nvim)**: 주석 처리를 빠르고 직관적으로 만들어 줍니다.
* **[guess-indent.nvim](https://github.com/NMAC427/guess-indent.nvim)**: 파일의 들여쓰기 설정을 자동으로 감지합니다.
* **[nvim-autopairs](https://github.com/windwp/nvim-autopairs)**: 괄호나 따옴표를 자동으로 닫아줍니다.
* **[auto-save.nvim](https://github.com/Pocco81/auto-save.nvim)**: 파일을 자동으로 저장해 데이터 손실을 방지합니다.

### 작업 효율성 향상
* **[vim-visual-multi](https://github.com/mg979/vim-visual-multi)**: 다중 커서(Multi-cursor) 기능을 추가합니다. 익숙해지면 강력하지만, 매크로를 먼저 연습해 보시는 것도 좋습니다.
* **[toggleterm.nvim](https://github.com/akinsho/toggleterm.nvim)**: Neovim 내부에서 터미널을 편리하게 띄우고 숨길 수 있게 해줍니다.
* **[vim-better-whitespace](https://github.com/ntpeters/vim-better-whitespace)**: 줄 끝의 불필요한 공백을 강조하고 제거해 깔끔한 코드를 유지하게 돕습니다.

---

## 추가 유용한 도구들
* **[nvim-surround](https://github.com/kylechui/nvim-surround)**: 코드 덩어리를 괄호나 태그로 빠르게 감싸거나 변경합니다. (매우 추천!)
* **[undotree](https://github.com/mbbill/undotree)**: 편집 기록(Undo history)을 트리 구조로 보여줍니다. 실수로 덮어쓴 작업도 되찾을 수 있습니다.
* **[todo-comments.nvim](https://github.com/folke/todo-comments.nvim)**: `TODO`, `FIXME` 같은 주석을 강조하고 목록으로 모아 보여줍니다.
* **[leap.nvim](https://github.com/ggandor/leap.nvim)**: 화면 내 어디든 단 몇 글자만으로 순식간에 점프할 수 있는 고급 이동 기능을 제공합니다.
* **[vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator)**: tmux와 Neovim 사이를 매끄럽게 오가기 위한 필수 플러그인입니다.
* **[suda.vim](https://github.com/lambdalisue/suda.vim)**: sudo 권한이 필요한 파일을 편집할 때 Neovim을 다시 실행할 필요 없이 권한을 부여받아 저장할 수 있게 해줍니다.

---

## 꿀팁: Neovim을 Man 페이지 뷰어로 사용하기
쉘 설정 파일(`.bashrc`나 `.zshrc`)에 아래 내용을 추가해 보세요. 리눅스/macOS의 `man` 페이지를 Neovim의 강력한 검색 및 탐색 기능을 사용해 읽을 수 있습니다.

```bash
export MANPAGER='nvim +Man! .'
export MANWIDTH=999
```

---

## 마치며
긴 여정을 함께해 주셔서 감사합니다! 이 가이드가 Neovim이라는 멋진 도구를 익히는 데 조금이나마 도움이 되었기를 바랍니다.

Neovim은 단순히 도구를 배우는 것을 넘어, 여러분의 편집 방식을 끊임없이 고민하고 개선해 나가는 과정 그 자체입니다. 가이드에서 다룬 내용은 시작일 뿐입니다. 새로운 플러그인과 설정을 탐구하며 여러분만의 완벽한 워크플로를 만들어 나가세요.

도움이 될 만한 곳들:
* **[awesome-neovim](https://github.com/rockerBOO/awesome-neovim)**: 가장 방대한 플러그인 큐레이션 사이트입니다.
* **[/r/neovim](https://www.reddit.com/r/neovim/)**: 전 세계 Neovim 사용자들이 소통하는 가장 큰 커뮤니티입니다.

실수를 발견했거나 더 나은 제안이 있다면 언제든 [이슈 섹션](https://github.com/ofirgall/learn-nvim/issues)에 남겨주세요. 여러분의 Neovim 여행에 즐거움만 가득하시길 바랍니다!
