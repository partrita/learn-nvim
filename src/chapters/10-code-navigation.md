# 코드 탐색 및 이동
단순히 텍스트를 고치는 수준을 넘어, Neovim을 IDE처럼 '똑똑하게' 만들어주는 핵심 기술이 바로 LSP와 Telescope입니다.

---

## LSP (Language Server Protocol)
Neovim에 지능을 부여하려면 LSP 서버를 설치하고 내장 LSP 클라이언트에 연결해야 합니다. 이를 통해 코드 자동 완성, 정의 이동, 실시간 진단 등의 기능을 누릴 수 있습니다.

설정 방법에는 크게 두 가지가 있습니다.
1. **[mason.nvim](https://github.com/williamboman/mason.nvim) 활용**: LSP 서버, Linter, Formatter 등을 Neovim 안에서 GUI처럼 편리하게 관리하고 설치할 수 있습니다. 대부분의 사전 설정(LunarVim 등)이 이 방식을 택하고 있습니다.
2. **수동 설정**: `nvim-lspconfig`를 사용해 시스템에 설치된 LSP 바이너리를 직접 연결합니다. 설정 파일(dotfiles)을 통해 환경을 더 세밀하게 통제하고 싶은 분들께 적합합니다.

---

## [Telescope](https://github.com/nvim-telescope/telescope.nvim)
LSP가 제공하는 강력한 정보들을 검색하고 활용할 수 있게 해주는 필수 프레임워크입니다. 파일 검색부터 코드 탐색까지, 거의 모든 찾기 작업을 Telescope 하나로 해결할 수 있습니다.

### 주요 기능
* **실시간 Grep**: 프로젝트 전체에서 특정 텍스트를 순식간에 찾아냅니다. (IDE의 `Ctrl + Shift + F`)
* **파일 찾기**: 파일 이름으로 빠르게 점프합니다. (IDE의 `Ctrl + P`)
* **정의 이동**: 함수나 변수가 선언된 위치를 즉시 찾아줍니다. (`F12`)
* **참조/구현 검색**: 해당 심볼이 어디서 쓰이고 있는지 목록으로 보여줍니다.
* **심볼 검색**: 현재 파일이나 전체 작업 공간 내의 함수 목록을 필터링해 찾아갑니다.

---

## 탐색 경험을 높여주는 추천 플러그인
* [lspsaga.nvim](https://github.com/nvimdev/lspsaga.nvim): 호버(Hover), 이름 바꾸기, 코드 액션 등을 위한 미려한 UI를 제공합니다.
* [vim-illuminate](https://github.com/RRethy/vim-illuminate): 커서 아래의 단어와 같은 단어들을 자동으로 강조해주고, 그 사이를 빠르게 이동할 수 있게 해줍니다.
* [fidget.nvim](https://github.com/j-hui/fidget.nvim): LSP 서버의 동작 상태(인덱싱 등)를 오른쪽 하단에 세련된 애니메이션으로 보여줍니다.
* [lsp_lines.nvim](https://git.sr.ht/~whynothugo/lsp_lines.nvim): 코드 에러나 경고를 훨씬 직관적인 그래프 형태로 표시해 줍니다.
* [nvim-navic](https://github.com/SmiteshP/nvim-navic): 현재 커서가 어떤 클래스의 어떤 함수 안에 있는지 상태 표시줄에 경로로 보여줍니다.

더 많은 LSP 관련 플러그인은 [awesome-neovim](https://github.com/rockerBOO/awesome-neovim#lsp)에서 확인해 보세요.
