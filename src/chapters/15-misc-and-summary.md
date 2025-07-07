# 기타

이 장에서는 제가 추천하는 몇 가지 기타 플러그인에 대해 설명합니다.

## 기본적인 IDE 기능

Neovim은 IDE의 모든 예상 기능을 제공하지는 않지만, 플러그인이 그 부족한 부분을 채워줍니다.

### 세션 관리자

저는 [auto-session](https://github.com/rmagatti/auto-session)을 사용합니다.
[다른 세션 관리자](https://github.com/rockerBOO/awesome-neovim#session)

### [주석(Comment)](https://github.com/numToStr/Comment.nvim)

주석 작업을 추가합니다.

### [마지막 위치(Last Place)](https://github.com/ethanholz/nvim-lastplace)

버퍼를 마지막으로 편집한 위치를 기억합니다.

### [들여쓰기 추측(Guess Indent)](https://github.com/NMAC427/guess-indent.nvim)

파일의 들여쓰기를 추측하고 들여쓰기 설정을 덮어씁니다.

### [자동 페어(Auto Pairs)](https://github.com/windwp/nvim-autopairs)

페어에 대한 닫는 괄호를 자동으로 추가합니다. 예를 들어, `(`를 입력하면 `()`로 만들고 커서를 가운데에 놓습니다.

### [자동 저장(Auto Save)](https://github.com/Pocco81/auto-save.nvim)

텍스트가 편집되면 파일을 자동으로 저장하여 데이터 손실을 걱정할 필요가 없습니다.

### [후행 공백(Trailing whitespace)](https://github.com/ntpeters/vim-better-whitespace)

좋은 프로그래머가 되어 Git에 불필요한 공백을 남기지 마세요.

### [다중 커서(Multi cursor)](https://github.com/mg979/vim-visual-multi)

이미 다중 커서에 능숙하다면 그 기술을 Neovim에서도 활용하세요. 그렇지 않다면 매크로 사용을 고려해 보세요.

### [Neovim 내 터미널(Terminal in nvim)](https://github.com/akinsho/toggleterm.nvim)

Neovim 내에 통합 터미널을 활성화합니다.

### [파스타(pasta)](https://github.com/hrsh7th/nvim-pasta)

Neovim의 기본 붙여넣기 관련 문제를 해결합니다.

## 추가 기능

### [Surround](https://github.com/kylechui/nvim-surround)

코드의 일부를 `[]`/`()`/`{}`로 빠르게 감쌉니다.

### [Undotree](https://github.com/mbbill/undotree)

실행 취소 브랜치를 시각화하여 다시는 실행 취소/다시 실행 기록을 잃어버리지 마세요\!

### [Unimpaired](https://github.com/tpope/vim-unimpaired)

자연스럽게 느껴지는 페어 매핑(`][`)을 추가합니다.

### [vim-repeat](https://github.com/tpope/vim-repeat)

점 반복(dot-repeat) 동작을 확장합니다.

### [Todo Comments](https://github.com/folke/todo-comments.nvim)

`TODO` 주석을 강조 표시하고, 작업 공간의 모든 todo 주석으로 퀵픽스 목록을 채웁니다.

### [Debug print](https://github.com/andrewferrier/debugprint.nvim)

변수에 대한 디버그 출력을 빠르게 추가합니다.

### [leap.nvim](https://github.com/ggandor/leap.nvim)

vimium, EasyMotion, hop 등과 같은 리프 모션을 Neovim에 추가합니다.
[clever-f](https://github.com/rhysd/clever-f.vim)가 마음에 들었다면 [flit.nvim](https://github.com/ggandor/flit.nvim)을 좋아할 것입니다.

### [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator)

Tmux를 사용하고 있다면 Neovim 간의 창 전환을 원활하게 만들어 줍니다. 필수 플러그인입니다!

### [suda.vim](https://github.com/lambdalisue/suda.vim)

sudo 권한이 필요한 파일을 Neovim을 sudo로 실행하지 않고 읽거나 씁니다.

### [impatient.nvim](https://github.com/lewis6991/impatient.nvim)

시작 시간을 개선합니다.

### Man 페이지 뷰어

Neovim을 man 페이지 뷰어로 사용하는 것을 고려해 보세요. 에디터를 제어하는 것처럼 man 페이지를 제어할 수 있어 정말 좋습니다.
`.shellrc`에 다음을 추가하세요:

```bashrc
# Neovim을 man 뷰어로 사용
export MANPAGER='nvim +Man! .'
export MANWIDTH=999
```

### 더 많은 정보

Neovim에는 훨씬 더 많은 플러그인이 있습니다. [awesome-neovim](https://github.com/rockerBOO/awesome-neovim)을 확인해볼 수 있으며, 제 목록인 - [packer.lua](https://github.com/ofirgall/dotfiles/blob/master/editors/nvim/lua/plugins/packer.lua)도 확인해볼 수 있습니다.

-----

# 요약

읽어주셔서 감사합니다\! 이 가이드가 Neovim을 배우는 데 도움이 되었기를 바랍니다.
이 가이드가 모든 것을 다루지는 않지만, 텍스트 편집기에 대해 계속 배우고 실력을 향상시키세요.

실수를 발견했다면 [이슈 섹션](https://github.com/ofirgall/learn-nvim/issues)에 피드백을 남겨주세요.
이 가이드가 마음에 들었다면 `star`를 남겨주세요.

새로운 플러그인과 업데이트를 확인하려면 다음을 권장합니다:

  * [awesome-neovim](https://github.com/rockerBOO/awesome-neovim)을 Watch하여 새로운 PR(플러그인) 알림을 받으세요.
  * [/r/neovim](https://www.reddit.com/r/neovim/)을 구독하세요.