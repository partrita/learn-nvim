# 자동 완성 및 스니펫 엔진
사전 구성된 설정을 사용하는 경우 이 기능이 이미 구성 및 설치되어 있을 가능성이 높으므로 이 챕터를 건너뛸 수 있습니다.

## 자동 완성 엔진 (Complete Engine)
nvim은 기본 자동 완성 메뉴를 제공하지 않으므로, 퍼지 검색, 자동 완성, 스크롤 등이 포함된 메뉴가 필요합니다. \
이를 위해 자동 완성 엔진이 있으며, 모두가 사용하는 것은 [nvim-cmp](https://github.com/hrsh7th/nvim-cmp)입니다. \
권장 설정으로 시작하여 나중에 더 자세히 구성하는 것을 추천합니다.

### 소스 (Sources)
설정의 일부로 `sources`를 전달하는데, 이는 자동 완성 메뉴가 항목을 가져오는 위치입니다. 다른 플러그인을 사용하여 자동 완성의 `sources`를 확장할 수 있습니다.

기본 소스는 [nvim-cmp](https://github.com/hrsh7th/nvim-cmp)의 README에 나와 있습니다. \
원하는 소스 중 하나는 자동 완성 엔진 소스이며, 이에 대해서는 나중에 자세히 설명하겠습니다.

추가적인 멋진 소스:
* [cmp-git](https://github.com/petertriho/cmp-git) - 모든 커밋 해시에 대한 소스를 제공하고 github 및 gitlab과 통합됩니다.
* [cmp-jira](https://gitlab.com/msvechla/cmp-jira) - 티켓에 대한 소스를 제공합니다.
* [copilot-cmp](https://github.com/zbirenbaum/copilot-cmp) - nvim-cmp를 통해 github copilot을 nvim에 통합합니다.
* [더 많은 소스는 여기에서 찾을 수 있습니다](https://github.com/hrsh7th/nvim-cmp/wiki/List-of-sources)

### 포맷팅 및 창 (Formatting & Window)
메뉴 표시 방법을 제어할 수 있습니다.

### 바인딩 (Binds)
이 부분은 마음껏 설정할 수 있지만, 처음에는 기본 설정을 유지하고 나중에 생각하는 것을 추천합니다.

---

## 스니펫 엔진 (Snippet Engine)
스니펫 엔진에는 두 가지 부분이 있습니다. 스니펫 형식을 실제 스니펫으로 변환하는 부분과 완성해야 하는 스니펫 부분 사이를 이동할 수 있게 하는 부분입니다.

여러 스니펫 엔진이 있으며, 개인적으로 [nvim-snippy](https://github.com/dcampos/nvim-snippy)를 사용하며, 이는 [cmp-snippy](https://github.com/dcampos/cmp-snippy)를 [nvim-cmp](https://github.com/hrsh7th/nvim-cmp) 소스로 추가해야 합니다.

스니펫 엔진에는 스니펫 소스도 필요하며, 저는 원치 않는 스니펫을 제거하기 위해 [vim-snippets](https://github.com/honza/vim-snippets)의 개인 포크를 사용합니다.

---

# [나의 자동 완성 및 스니펫 엔진 설정](https://github.com/ofirgall/dotfiles/blob/master/editors/nvim/lua/plugins/autocomplete.lua)
