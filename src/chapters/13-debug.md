# 디버그
LSP와 동일한 해결책이 디버깅에도 존재하며, 이를 `DAP`(디버그 어댑터 프로토콜)라고 합니다. 
이를 통합하려면 [nvim-dap](https://github.com/mfussenegger/nvim-dap)를 설치해야 합니다.

모든 좋은 nvim 플러그인과 마찬가지로 [nvim-dap](https://github.com/mfussenegger/nvim-dap)는 프레임워크이며 이를 확장하는 플러그인이 있습니다.

확장 기능:
* [nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui) - 디버깅을 위한 대화형 UI이며, 필수입니다!
* [dap-buddy.nvim](https://github.com/Pocco81/dap-buddy.nvim) - DAP 서버를 설치하며, 서버를 수동으로 설치하는 것을 선호한다면 이 단계를 건너뛸 수 있습니다.
* [persistent-breakpoints.nvim](https://github.com/Weissle/persistent-breakpoints.nvim) - nvim 재시작 시 중단점을 저장합니다.
* [goto-breakpoints.nvim](https://github.com/ofirgall/goto-breakpoints.nvim) - 중단점을 순환하는 쌍 바인딩이며, 제가 만든 플러그인입니다 :)
* [더 많은 확장 기능은 여기에서 찾을 수 있습니다](https://github.com/rockerBOO/awesome-neovim#debugging)
