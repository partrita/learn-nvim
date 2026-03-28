# 디버깅 환경 구축
코드 작성만큼이나 중요한 것이 바로 디버깅입니다. Neovim에서도 IDE 못지않은 강력한 디버깅 환경을 구축할 수 있습니다. 

---

## DAP (Debug Adapter Protocol)
LSP가 코드 분석을 위한 표준이라면, **DAP**는 디버깅을 위한 표준 프로토콜입니다. Neovim에서 이를 활용하려면 [nvim-dap](https://github.com/mfussenegger/nvim-dap) 플러그인이 필요합니다.

nvim-dap은 디버깅의 핵심 로직을 담당하는 프레임워크이며, 다양한 확장 플러그인을 통해 기능을 완성합니다.

### 추천 확장 플러그인
* **[nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui)**: 디버깅 시 변수 목록, 호출 스택, 중단점 등을 시각적으로 보여주는 필수 UI 플러그인입니다.
* **[mason-nvim-dap.nvim](https://github.com/jay-babu/mason-nvim-dap.nvim)**: Mason을 통해 디버그 어댑터를 간편하게 설치하고 관리하게 해줍니다.
* **[persistent-breakpoints.nvim](https://github.com/Weissle/persistent-breakpoints.nvim)**: Neovim을 껐다 켜도 설정해둔 중단점(Breakpoint)이 사라지지 않게 저장해 줍니다.
* **[goto-breakpoints.nvim](https://github.com/ofirgall/goto-breakpoints.nvim)**: 중단점 사이를 단축키로 빠르게 이동할 수 있게 해줍니다. (제가 직접 만든 플러그인입니다!)

더 많은 디버깅 관련 도구는 [awesome-neovim](https://github.com/rockerBOO/awesome-neovim#debugging)에서 찾아보실 수 있습니다.
