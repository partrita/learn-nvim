# 기본 환경 설정
Neovim의 가장 큰 매력 중 하나는 사용자의 취향에 맞게 모든 요소를 커스터마이징할 수 있는 유연함입니다. 불필요한 장식은 덜어내고, 오직 코드에만 집중할 수 있는 깔끔한 환경을 구축하는 것부터 시작해 보겠습니다.

자신만의 설정을 처음부터 쌓아 올리는 것도 의미 있는 일이지만, 여기엔 상당한 시간과 인내가 필요합니다. 설정에 깊이 빠져들 준비가 된 분이 아니라면, 우선은 잘 구성된 '사전 설정(Pre-configured)'을 사용해 보시는 걸 추천합니다. 자세한 장점은 [고급 설정 가이드](chapters/08-advanced-config.md)에서 더 깊이 있게 다뤄보겠습니다.

---

## 터미널 에뮬레이터 고르기
Neovim을 전용 GUI 프로그램에서 실행할 수도 있지만, 본래의 맛을 제대로 느끼려면 터미널 에뮬레이터에서 사용하는 것이 좋습니다. 성능이 뛰어나고 최신 운영체제를 잘 지원하는 터미널을 선택하는 것이 중요합니다.

* [Alacritty](https://github.com/alacritty/alacritty): 속도가 매우 빠릅니다. 화면 분할과 세션 관리를 위해 [tmux](https://github.com/tmux/tmux)와 조합해 사용하는 걸 추천합니다. 저 역시 이 조합을 가장 선호합니다.
* [Kitty](https://github.com/kovidgoyal/kitty): 성능이 독보적이며, 다양한 부가 기능을 갖춘 인기 터미널입니다.
* [Wezterm](https://github.com/wez/wezterm): Lua 언어로 모든 설정을 제어할 수 있는 현대적인 터미널입니다.

### 너드 폰트 (Nerd Fonts) 필수 설치
터미널에서 다양한 아이콘과 특수 문자를 깨짐 없이 보려면 [너드 폰트](https://www.nerdfonts.com/)가 꼭 필요합니다. 많은 Neovim 플러그인이 이를 활용해 정보를 시각적으로 표현하기 때문이죠.
추천하는 폰트는 [JetBrains Mono Nerd Font](https://www.jetbrains.com/lp/mono/)나 [Cascadia Code Nerd Font](https://github.com/microsoft/cascadia-code)입니다.

### 터미널의 입력 제한 사항
전통적인 터미널 환경의 한계로 인해, 일부 터미널은 `Ctrl + Shift + <키>` 같은 복잡한 조합을 인식하지 못할 수 있습니다. [상세 내용](https://github.com/tmux/tmux/issues/674#issuecomment-263157843)을 참고해 보세요. 우회 방법이 있긴 하지만, 필수 기능은 아니니 크게 걱정하지 않으셔도 됩니다.

#### macOS에서 Option 키를 Alt로 사용하기
터미널에서 `Alt` 관련 단축키를 쓰려면 설정이 필요합니다.
* [Kitty 설정 가이드](https://sw.kovidgoyal.net/kitty/conf/#opt-kitty.macos_option_as_alt)
* [Alacritty 설정 가이드](https://github.com/alacritty/alacritty/issues/62)

---

## Neovim 설치하기
안정적인 사용을 위해 [최신 정식 릴리스](https://github.com/neovim/neovim/releases) 버전을 설치하는 것을 권장합니다. 매일 업데이트되는 나이틀리(Nightly) 빌드도 있지만, 입문 단계에서는 예상치 못한 버그로 고생할 수 있으니 정식 버전을 먼저 써보세요.

---

## [추천 사전 설정 (Configurations)](https://github.com/rockerBOO/awesome-neovim#preconfigured-configuration)
커뮤니티에서 가장 사랑받는 대표적인 설정 패키지들입니다.
* [LunarVim](https://github.com/LunarVim/LunarVim)
* [AstroNvim](https://github.com/AstroNvim/AstroNvim)
* [NvChad](https://github.com/NvChad/NvChad)

#### LunarVim으로 시작하기
직접 설정을 구축하는 것도 재미있지만, 입문자분들께는 [LunarVim](https://github.com/LunarVim/LunarVim)을 강력히 추천합니다. 설치가 매우 간편하고, 코딩에 필요한 필수 기능들이 이미 훌륭하게 세팅되어 있기 때문입니다. [공식 설치 가이드](https://www.lunarvim.org/docs/installation)를 따라 해보세요.

설치 후에는 다음 단축키로 기본 설정을 살펴볼 수 있습니다.
* 설정 파일 열기: `Space`, `L`, `c`
* 기본 단축키 확인: `Space`, `L`, `k`

---

## 플러그인 생태계 활용하기
Neovim의 진정한 재미는 플러그인으로 기능을 확장하는 데 있습니다.

#### 플러그인 관리의 원리
대부분의 플러그인은 GitHub 저장소 형태로 제공됩니다. 패키지 관리자가 이를 다운로드하고 최신 상태로 유지해 주죠. 현재는 [packer.nvim](https://github.com/wbthomason/packer.nvim)이나 [lazy.nvim](https://github.com/folke/lazy.nvim)이 주로 쓰입니다. LunarVim에는 이미 훌륭한 관리 도구가 포함되어 있습니다.

LunarVim 설정 파일에서 다음과 같이 플러그인을 추가할 수 있습니다.
```lua
-- 추가 플러그인 등록
lvim.plugins = {
    {"folke/tokyonight.nvim"},
    {
      "folke/trouble.nvim",
      cmd = "TroubleToggle",
    },
}
```

#### 플러그인 설정하기
대부분의 플러그인은 `setup` 함수를 호출해야 활성화됩니다. 이때 설정값(Table)을 전달해 상세 동작을 제어할 수 있습니다. 자세한 옵션은 각 플러그인의 `README`나 `:help <플러그인명>`으로 확인할 수 있습니다.

_**팁**_: `setup` 함수 근처에 플러그인의 GitHub 주소를 주석으로 남겨두면 나중에 참고하기 좋습니다. [open.nvim](https://github.com/ofirgall/open.nvim) 플러그인을 쓰면 브라우저에서 바로 열어볼 수도 있습니다.

#### 입문용 추천 플러그인 목록
* **색상 테마**: [awesome-neovim](https://github.com/rockerBOO/awesome-neovim#colorscheme)에서 마음에 드는 테마를 골라보세요.
* [auto-session](https://github.com/rmagatti/auto-session): 마지막 작업 세션을 자동으로 복구해 줍니다.
* [Comment.nvim](https://github.com/numToStr/Comment.nvim): 주석 처리를 빠르고 간편하게 만들어 줍니다.
* [nvim-autopairs](https://github.com/windwp/nvim-autopairs): 괄호를 자동으로 닫아줍니다.
* [guess-indent.nvim](https://github.com/NMAC427/guess-indent.nvim): 파일의 들여쓰기 스타일을 자동으로 감지합니다.

---

## 기본 옵션 설정 (Options)
옵션은 Neovim의 전반적인 동작을 결정합니다. `:set <옵션명>`으로 설정하고, 불리언 타입은 앞에 `no`를 붙여서 끌 수 있습니다. (예: `:set norelativenumber`)

더 자세한 정보는 `:h option-list`를 참고하세요.

### 자주 쓰이는 설정 예시
```lua
local opt = vim.opt

opt.number = true           -- 줄 번호 표시
opt.relativenumber = true   -- 상대 줄 번호 표시
opt.cursorline = true       -- 현재 커서가 있는 줄 강조
opt.ignorecase = true       -- 검색 시 대소문자 구분 안 함
opt.smartcase = true        -- 대문자가 포함되면 대소문자 구분
opt.splitright = true       -- 세로 분할 시 오른쪽에 창 열기
opt.splitbelow = true       -- 가로 분할 시 아래에 창 열기
opt.swapfile = false        -- 스왑 파일 생성 안 함
opt.wrap = false            -- 자동 줄 바꿈 비활성화
opt.updatetime = 250        -- 반응 속도 개선
```

---

## 단축키 매핑 (Key Mapping)
각 모드(`n`: 일반, `i`: 입력, `v`: 비주얼 등)에 맞춰 자신만의 단축키를 정의할 수 있습니다.

```lua
-- 단축키 설정 예시
vim.keymap.set('n', '<leader>w', ':w<CR>', { desc = '파일 저장' })
```

---

## 필수 백엔드 도구
검색과 분석 성능을 끌어올리기 위해 시스템에 미리 설치해 두면 좋은 도구들입니다.
* [ripgrep (rg)](https://github.com/BurntSushi/ripgrep): 가장 빠른 텍스트 검색 도구입니다.
* [fd](https://github.com/sharkdp/fd): 현대적인 파일 검색 도구입니다.
* **LSP (Language Server Protocol)**: IDE 수준의 코드 완성 기능을 제공합니다.
* **Treesitter**: 코드를 정확하게 분석해 화려한 문법 강조와 지능적인 조작을 돕습니다.
