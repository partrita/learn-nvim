# 기본 설정
nvim의 강점 중 하나는 높은 설정 유연성입니다. 모든 것을 사용자 정의할 수 있습니다. \
보기 좋고 불필요한 버튼이나 요소로 채워지지 않도록 편집기를 설정하세요.

자신만의 설정을 만드는 것을 추천하지만, 시간과 노력이 필요합니다. \
[고급 설정 챕터](https://github.com/ofirgall/learn-nvim/blob/master/chapters/08-advanced-config.md)에서 장점에 대해 이야기하겠지만, 저처럼 설정에 열광하는 사람이 아니라면 지금은 사전 구성된 설정을 사용하는 것을 추천합니다.

---

## 터미널 에뮬레이터 설정
nvim은 GUI 프론트엔드 또는 원래 의도된 방식인 터미널 에뮬레이터에서 실행할 수 있습니다. \
최신 크로스 플랫폼 터미널 에뮬레이터 중 하나를 사용하는 것을 추천합니다:

* [Alacritty](https://github.com/alacritty/alacritty) - 분할 및 세션 관리를 위해 [tmux](https://github.com/tmux/tmux)/[i3](https://github.com/i3/i3)와 함께 사용하는 것을 추천합니다 (저는 Alacritty + tmux를 사용합니다).
* [Kitty](https://github.com/kovidgoyal/kitty) - 사용해 본 적은 없지만 사람들이 좋다고 합니다.
* [Wezterm](https://github.com/wez/wezterm) - Lua로 설정하는 터미널입니다. 개인적으로 디자인, 특히 커서 동작 방식이 마음에 들지 않지만, 커뮤니티에서는 좋아하는 것 같습니다.

### 너드 폰트 (Nerdfont)
터미널에서 아이콘을 지원하려면 [너드 폰트](https://www.nerdfonts.com/)를 설치하는 것이 좋습니다. 많은 플러그인이 이를 활용합니다. \
저는 [CascadiaCode](https://www.programmingfonts.org/#cascadia-code)를 사용하며, [JetBrainsMono](https://www.programmingfonts.org/#jetbrainsmono)도 좋습니다.

### 키 바인딩 제한
`ascii` 때문에 터미널은 `Ctrl+Shift+<X>` 키 바인딩을 지원하지 않습니다. [그 이유를 설명하는 훌륭한 댓글](https://github.com/tmux/tmux/issues/674#issuecomment-263157843)이 있습니다. \
일부 터미널에서는 해결 방법을 사용할 수 있지만, 필수는 아닙니다 (저는 Ctrl+Shift+X 바인딩을 사용하지 않습니다).

#### macOS에서 Alt로 옵션 키 사용
터미널에서 Alt 바인딩을 사용하려면 터미널 에뮬레이터를 설정해야 합니다.
* [Kitty용](https://sw.kovidgoyal.net/kitty/conf/#opt-kitty.macos_option_as_alt)
* [Alacritty용](https://github.com/alacritty/alacritty/issues/62)

---

## nvim 설치 방법
[최신 릴리스](https://github.com/neovim/neovim/releases)를 설치하는 것을 추천합니다. `Nvim development`는 나이틀리 빌드입니다. \
꽤 안정적이고 자주 깨지지 않는 [나이틀리 빌드](https://github.com/neovim/neovim/releases/tag/nightly)를 설치할 수도 있지만, 초보자로서 버그 문제로 골치 아프고 싶지는 않을 것입니다.

---

## [사전 구성된 설정 (Preconfigured Configurations)](https://github.com/rockerBOO/awesome-neovim#preconfigured-configuration)
몇 가지 사전 구성된 설정이 있으며, 다음은 인기 있는 것들입니다:
* [LunarVim](https://github.com/LunarVim/LunarVim)
* [AstroNvim](https://github.com/AstroNvim/AstroNvim)
* [NvChad](https://github.com/NvChad/NvChad)

#### LunarVim
개인적으로 사전 구성된 설정을 사용하는 것을 건너뛰었지만, 시작점으로 사용하는 것을 강력히 추천합니다. [LunarVim](https://github.com/LunarVim/LunarVim)이 가장 시작하기 쉽습니다. [설치 링크](https://www.lunarvim.org/docs/installation).

기본 설정을 읽고 자신의 취향에 맞게 편집해야 합니다. \
설정을 열려면 `Space`, `SHIFT+L`, `c`를 누르세요. \
키 바인딩을 보려면 `Space`, `SHIFT+L`, `k`를 누르세요.

---

## 플러그인 설치 방법
앞으로 몇 가지 플러그인을 추천할 것이니, 귀찮아하지 말고 설치하세요.

#### 플러그인 다운로드 방법
nvim 플러그인은 git 저장소이며, 패키지 관리자가 이를 다운로드하고 업데이트합니다. [packer](https://github.com/wbthomason/packer.nvim)가 표준이며 LunarVim에는 이미 설치되어 있습니다.

LunarVim 설정에서 다음을 찾을 수 있습니다:
```lua
-- Additional Plugins
lvim.plugins = {
    {"folke/tokyonight.nvim"},
    {
      "folke/trouble.nvim",
      cmd = "TroubleToggle",
    },
}
```

`lvim.plugins`는 [packer](https://github.com/wbthomason/packer.nvim)로 전달되며, `folke/tokyonight.nvim`은 [github.com/folke/tokyonight.nvim](https://github.com/folke/tokyonight.nvim)의 약자입니다. \
즉, 플러그인이 `use { 'plugin_author/plugin_name', more_options }`로 설치하라고 하면, `{ 'plugin_author/plugin_name', more_options }`를 복사하면 됩니다.

_**참고**_: LunarVim은 설정이 변경되면 자동으로 `:PackerInstall`을 실행합니다.

유용한 Packer 명령어:
* `:PackerInstall` - 새로 추가된 플러그인을 설치합니다.
* `:PackerStatus` - 설치된 모든 플러그인을 나열합니다.
* `:PackerSnapshot` - 현재 플러그인 버전의 스냅샷을 만듭니다 (업데이트 전에 유용합니다).
* `:PackerUpdate` - 모든 플러그인을 업데이트합니다.
* `:PackerClean` - 사용하지 않는 플러그인을 제거합니다.

#### 플러그인 설정 방법
일반적으로 플러그인은 플러그인의 동작을 설정하는 `setup` 함수를 제공하며, 대부분의 플러그인은 `setup` 함수가 호출되지 않으면 활성화되지 않습니다.

일반적으로 `setup` 함수는 `테이블`을 받으며, 대부분의 플러그인은 표준 재정의 방식을 사용합니다. 전달하는 테이블의 키는 기본값을 재정의하고, 다른 키는 기본값을 유지합니다. \
기본값은 일반적으로 플러그인 `README`와 `:help <플러그인>`에 있습니다.

_**참고**_: `setup` 함수 위에 GitHub 약자를 주석으로 추가하는 것을 추천합니다. [open.nvim](https://github.com/ofirgall/open.nvim)을 사용하여 플러그인 저장소에 빠르게 접근할 수 있습니다.

#### vim 플러그인 설치 방법
nvim은 vim 플러그인을 지원하며, 설치 방법은 nvim과 유사하지만 설정은 `setup` 함수 대신 vim 변수를 통해 이루어집니다.
플러그인의 문서는 일반적으로 다음과 같이 VimScript 형식으로 작성됩니다:
```vim
let g:cool_plugin_variable = 1
```
Lua에서 해당 줄은 다음과 같습니다:
```lua
vim.g.cool_plugin_variable = 1
```

vim 변수에 대한 자세한 내용은 `:help internal-variables`에서 읽을 수 있습니다.

#### 시작 시 추천 플러그인
* 마음에 드는 [색상 테마](https://github.com/rockerBOO/awesome-neovim#colorscheme)를 선택하거나 저처럼 직접 만드세요 ([ofirkai.nvim](https://github.com/ofirgall/ofirkai.nvim)).
* [auto-session](https://github.com/rmagatti/auto-session) - 세션을 자동으로 저장하여 nvim을 종료하거나 다시 시작한 후 세션으로 바로 돌아갈 수 있습니다.
* [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator) - tmux 사용자를 위한 훌륭한 플러그인입니다.
* [Comment.nvim](https://github.com/numToStr/Comment.nvim) - 주석 처리 기능을 추가합니다 (LunarVim의 [핵심 플러그인](https://www.lunarvim.org/docs/plugins/core-plugins-list)에 포함되어 있습니다).
* [lsp_signature.nvim](https://github.com/ray-x/lsp_signature.nvim) - 입력할 때 함수 시그니처를 보여줍니다.
* [guess-indent.nvim](https://github.com/NMAC427/guess-indent.nvim) - 자동 들여쓰기 스타일 감지.
* [nvim-autopairs](https://github.com/windwp/nvim-autopairs) - 자동 괄호 완성. 예를 들어 `(`를 입력하면 닫는 괄호를 추가하고 커서를 그 사이에 놓습니다. (LunarVim에 포함)
* [open.nvim](https://github.com/ofirgall/open.nvim) - vim에서 바로 GitHub 약자 등을 엽니다.

##### 프로그래밍 언어 지원
일부 언어는 특정 지원을 위한 플러그인이 있으며, 일반적으로 해당 플러그인이 LSP 설정(아래 참조)을 처리하므로 LSP를 두 번 이상 설정하지 않도록 주의하세요. 플러그인의 LSP 설정을 건너뛰고 직접 또는 mason으로 설정하는 것을 추천합니다.

* [rust-tools](https://github.com/simrat39/rust-tools.nvim)
* [flutter-tools](https://github.com/akinsho/flutter-tools.nvim)
* [go.nvim](https://github.com/ray-x/go.nvim)
* [neodev.nvim](https://github.com/folke/neodev.nvim) - nvim API용 Lua 개발 (LunarVim에 이미 설치됨)
* 다른 언어는 [awesome-neovim](https://github.com/rockerBOO/awesome-neovim#programming-languages-support)을 확인하세요.

##### [auto-save.nvim](https://github.com/Pocco81/auto-save.nvim)
다른 텍스트 편집기에서 자동 저장을 사용하는 것을 싫어했지만, vim은 모드가 있기 때문에 텍스트가 언제 변경되었는지 정확히 알 수 있습니다. \
입력 모드를 나올 때 트리거되는 `InsertLeave`와 일반 모드에서 텍스트가 변경될 때 트리거되는 `TextChanged` 시에 저장합니다.

자동 저장 + 자동 포맷 = 성가신 동작. 자동 포맷을 비활성화하세요. 버퍼를 전환할 때 포맷하도록 [간단한 플러그인](https://github.com/ofirgall/format-on-leave.nvim)을 만들었습니다.

LunarVim에서 자동 포맷을 비활성화하는 방법:
```lua
lvim.format_on_save = false
```

자동 저장 + 실시간 설정 새로고침 = 성가신 동작. 실시간 설정 새로고침을 좋아한다면 설정 파일에서 자동 저장을 비활성화하세요.\
LunarVim에서 이를 수행하는 예:

```lua
local user_config_file = require("lvim.config"):get_user_config_path()
require("auto-save").setup {
  enabled = true,

  condition = function(buf)
    local fn = vim.fn
    local utils = require("auto-save.utils.data")

    if vim.api.nvim_buf_get_name(buf) == user_config_file then
      return false
    end

    if fn.getbufvar(buf, "&modifiable") == 1 and
        utils.not_in(fn.getbufvar(buf, "&filetype"), {}) then
      return true -- 조건 충족, 저장 가능
    end
    return false -- 저장 불가
  end,
}
```

---

## 옵션 (Options)
옵션은 nvim의 동작을 제어하며, `boolean`, `number` 또는 `string`으로 설정할 수 있습니다. \
옵션을 설정하려면 `:set <옵션>`을 입력하고, 옵션의 현재 값을 보려면 `:set <옵션>?`을 사용하세요. \
boolean 옵션은 `:set <옵션>`으로 활성화하고 `:set no<옵션>`으로 비활성화합니다. \
예: `:set relativenumber`는 `relativenumber`를 활성화하고 `:set norelativenumber`는 비활성화합니다.

모든 옵션에는 도움말 태그가 있습니다. 예를 들어 `:h relativenumber` \
옵션 목록은 `:h option-list`에 있습니다.

nvim에서는 `vim.opt`를 통해 옵션에 접근할 수 있습니다.

### 유용한 옵션들
```lua
local opt = vim.opt

opt.number = true -- 줄 번호 활성화
opt.relativenumber = true -- 상대 줄 번호 활성화
opt.autoindent = true -- 자동 들여쓰기
opt.cursorline = true -- 커서 줄 활성화
opt.ignorecase = true -- 검색 시 대소문자 무시
opt.splitright = true -- 수직 분할 시 오른쪽에 분할
opt.splitbelow = true -- 수평 분할 시 아래쪽에 분할
opt.swapfile = false -- 스왑 파일 사용 안 함 (대신 auto-save.nvim 사용)
opt.wrap = true -- 줄 바꿈
opt.updatetime = 100 -- 주로 CursorHold 자동 명령을 활용하는 trld.nvim용
opt.formatoptions:append('cro') -- 다음 줄로 이동 시 주석 계속, C-u를 눌러 추가된 주석 접두사 제거
opt.sessionoptions:remove('options') -- 키맵과 로컬 옵션 저장 안 함
opt.foldlevelstart = 99 -- 자동 접기 안 함
```

---

## 키 매핑 (Key mapping)
키 맵은 특정 모드에 대해 설정할 수 있습니다. \
중요한 모드들:
* `n` - 일반 모드
* `i` - 입력 모드
* `x` - 비주얼 & 선택 모드
* `v` - 비주얼 모드
* 전체 모드 목록은 `:h map-commands` 참조

키맵을 설정하려면 `vim.keymap.set` 또는 `opts`에 대한 기본값이 있는 `map` 함수를 사용하는 것이 좋습니다.
```lua
local function map(mode, lhs, rhs, desc, opts)
	opts = opts or { slient = true }
	opts.desc = desc
	vim.keymap.set(mode, lhs, rhs, opts)
end
```
* `mode` - 키맵이 추가될 모드. 단일 모드 `'n'`, 모드 테이블 `{'n', 'x'}` 또는 모든 모드에 대해 빈 문자열 `''`일 수 있습니다.
* `lhs` - 키 맵을 활성화하기 위해 눌러야 하는 키
* `rhs` - 호출할 lua 함수이거나 vim이 "타이핑"하도록 하는 문자열일 수 있습니다. 예를 들어 `nzz`는 `n`을 실행한 다음 `zz`를 실행하며, 이는 `next`와 `recenter`에 바인딩됩니다.
* `desc` - 키맵에 대한 설명.
* `opts` - 키맵에 대한 옵션 테이블. 자세한 내용은 `:h map-arguments` 참조

__**참고:**__ LunarVim 키맵은 다르게 설정되므로 [이 내용](https://www.lunarvim.org/docs/configuration/keybindings)도 반드시 읽어보세요.

---

## 자동 명령 (Autocommands)
> 자동 명령은 파일 읽기 또는 쓰기, 버퍼 변경과 같은 특정 이벤트에 대한 응답으로 자동으로 실행되는 명령입니다.

예를 들어 복사된 텍스트를 강조 표시하는 좋은 자동 명령입니다.
```lua
-- 복사 시 강조 표시
vim.api.nvim_create_autocmd('TextYankPost', {
	pattern = '*',
	callback = function() vim.highlight.on_yank({timeout=350, higroup='Visual'}) end
})
```

플러그인도 사용자 지정 자동 명령을 추가할 수 있습니다! \
모든 내장 자동 명령은 `:h autocmd-list`를 참조하세요.

자세한 설명은 `:h nvim_create_autocmd`를 읽어보세요.

---

## 셸 설정 (Shell Setup)
nvim을 기본 터미널 편집기로 설정하는 것을 잊지 마세요:
```
export EDITOR='nvim'
```

---

## vim 바인딩을 사용하는 다른 유용한 도구들
* [Vimium](https://github.com/philc/vimium) - 브라우저용 Vim 바인딩.
* [btop](https://github.com/aristocratos/btop) - vim 바인딩을 사용하도록 설정할 수 있는 리소스 뷰어.

---

## 플러그인 도구 (Plugin Tools)
사전 구성된 설정은 LSP 및 Treesitter 설치를 처리하므로 직접 처리할 필요는 없지만, 다른 플러그인이 이러한 도구를 어떻게 활용하는지 이해하기 위해 두 도구 모두에 익숙해지는 것이 좋습니다.

### 백엔드 바이너리 (Backend Binaries)
일부 플러그인은 nvim을 빠르게 만들기 위해 외부 바이너리를 활용합니다. 설치하는 것을 추천합니다.
* [ripgrep aka rg](https://github.com/BurntSushi/ripgrep) - 더 나은 `grep`.
* [fd](https://github.com/sharkdp/fd) - 더 나은 `find`.

### [LSP](https://microsoft.github.io/language-server-protocol/)
> 언어 서버 프로토콜(LSP)의 기본 아이디어는 이러한 서버와 개발 도구가 통신하는 프로토콜을 표준화하는 것입니다. 이러한 방식으로 단일 언어 서버를 여러 개발 도구에서 재사용할 수 있으며, 개발 도구는 최소한의 노력으로 여러 언어를 지원할 수 있습니다.

즉, nvim/sublime/vscode가 동일한 Intellisense를 얻습니다. \
서버는 PC에서 로컬로 실행되며 빠르게 실행되도록 최적화되어 있습니다. \
nvim은 가장 빠른 lsp 클라이언트를 구현합니다.

[언어별 서버 목록](https://microsoft.github.io/language-server-protocol/implementors/servers/)

### [Treesitter](https://github.com/nvim-treesitter/nvim-treesitter)
> Tree-sitter는 파서 생성기 도구이자 증분 파싱 라이브러리입니다. 소스 파일에 대한 구체적인 구문 트리를 구축하고 소스 파일이 편집될 때 구문 트리를 효율적으로 업데이트할 수 있습니다. Tree-sitter는 다음을 목표로 합니다:
> * 모든 프로그래밍 언어를 파싱할 수 있을 만큼 **일반적**이어야 합니다.
> * 텍스트 편집기에서 모든 키 입력 시 파싱할 수 있을 만큼 **빨라야** 합니다.
> * 구문 오류가 있는 경우에도 유용한 결과를 제공할 수 있을 만큼 **견고해야** 합니다.
> * 런타임 라이브러리(순수 C로 작성됨)를 모든 애플리케이션에 포함할 수 있도록 **의존성이 없어야** 합니다.

기본적으로 다른 언어에 대해 빠르고 통일된 구문 쿼리를 제공하며, 이를 통해 통일된 구문 쿼리를 활용하는 플러그인을 구축할 수 있습니다.

예: [nvim-treesitter-textobjects](https://github.com/nvim-treesitter/nvim-treesitter-textobjects)는 `함수/클래스/인수/루프` 등을 `복사`하는 것과 같이 코드 컨텍스트에서 작업을 수행할 수 있게 하며, 이에 대해서는 나중에 자세히 설명하겠습니다.

_**참고:**_ `ensure_installed` 테이블에 추가하거나 `:TSUpdate {언어}`를 실행하여 해당 언어에 대한 treesitter 파서를 설치해야 합니다.
