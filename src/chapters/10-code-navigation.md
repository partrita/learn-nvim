# 코드 탐색

## LSP (언어 서버 프로토콜)
nvim을 "똑똑하게" 만들려면 LSP 서버를 설치하고 nvim의 LSP 클라이언트에 연결해야 합니다.

이를 수행하는 두 가지 옵션이 있습니다:
1. [mason.nvim](https://github.com/williamboman/mason.nvim)과 [mason-lspconfig.nvim](https://github.com/williamboman/mason-lspconfig.nvim) 및 [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig)를 사용합니다. 이 세 가지 플러그인은 LSP 서버를 관리하고 설치하며, 사전 구성된 설정과 통합해야 합니다.
1. [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig)를 사용하고 LSP 서버 바이너리를 수동으로 유지 관리합니다 (개인적으로 dotfiles로 수행합니다). 사전 구성된 설정과 통합해야 합니다.

## [Telescope](https://github.com/nvim-telescope/telescope.nvim)
이제 LSP에서 제공하는 뛰어난 기능을 활용할 수 있는 도구가 필요합니다.

그중 하나는 검색, 미리보기 및 선택을 위한 프레임워크인 telescope입니다.

몇 가지 기능:
* 프로젝트 전체에서 실시간 grep을 수행할 수 있으며, "최신" IDE의 CTRL+SHIFT+F와 동일합니다.
* 파일을 찾을 수 있으며, "최신" IDE의 CTRL+p와 동일합니다.
* 함수의 모든 정의를 찾을 수 있으며 (LSP 사용), "최신" IDE의 F12와 동일합니다.
* 모든 참조/구현/유형 정의를 찾을 수 있습니다 (LSP 사용).
* 물론 LSP를 사용하여 로컬/작업 공간 심볼(함수)을 실시간으로 grep 할 수 있습니다.

사전 구성된 설정에는 이미 설치되어 있고 키에 바인딩되어 있을 가능성이 높습니다. 사용 방법을 알고 취향에 맞게 구성해야 하며 매우 유용합니다.

## LSP 유용한 기능들
* [LSP Saga](https://github.com/glepnir/lspsaga.nvim) - LSP "호버", 이름 바꾸기 및 코드 작업(힌트)을 위한 UI입니다.
* [vim-illuminate](https://github.com/RRethy/vim-illuminate) - 커서가 있는 심볼을 강조 표시하고 다음/이전 참조로 이동할 수 있게 하여 변수에 "무슨 일이 일어났는지" 아는 데 매우 유용합니다.
* [LSP Signature](https://github.com/ray-x/lsp_signature.nvim) - 함수 호출을 작성하는 동안 함수 시그니처를 표시합니다.
* [fidget.nvim](https://github.com/j-hui/fidget.nvim) - 오른쪽 하단 모서리에 LSP 서버 진행 상황을 표시합니다.
* [lsp_lines.nvim](https://git.sr.ht/~whynothugo/lsp_lines.nvim) - 진단을 직관적인 방식으로 표시합니다.
* [trld.nvim](https://github.com/Mofiqul/trld.nvim) - 버퍼의 오른쪽 상단 모서리에 현재 줄 진단을 표시합니다.
* [nvim-navic](https://github.com/SmiteshP/nvim-navic) - 상태/창 표시줄에 현재 컨텍스트를 표시합니다.
* [LSP와 통합되는 더 많은 플러그인](https://github.com/rockerBOO/awesome-neovim#lsp)
