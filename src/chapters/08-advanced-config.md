# 고급 설정
vim의 기초(그리고 nvim에 대한 약간)를 배웠습니다. 이 챕터부터는 nvim을 좋은 편집기에서 훌륭한 편집기로 만들어주는 풍부한 플러그인 생태계와 설정 유연성에 대해 주로 이야기할 것입니다.

## 개인 설정 vs 사전 구성된 설정
#### 사전 구성된 설정
사전 구성된 설정은 훌륭합니다. 커뮤니티에서 유지 관리하는 좋은 설정을 빠르게 얻을 수 있는 방법을 제공합니다. 하지만 설정에 추상화 "계층"을 추가합니다. 내장 플러그인과 상호 작용하지 않는 새 플러그인을 설치할 때는 모든 것이 작동하지만, 플러그인이 내장 플러그인과 상호 작용해야 하는 경우 까다로워질 수 있습니다.
사전 구성된 설정이 해당 옵션을 어떻게 노출하는지 읽어야 하는데, 이는 때때로 혼란스럽고 불편합니다.

마치 임대한 집에서 물건을 고치려는 것과 같습니다. 모든 것이 어떻게 작동하는지 정확히는 모르지만 시도하면서 배우게 됩니다. 때로는 그냥 건드리고 싶지 않을 때도 있습니다.

#### 개인 설정
자신만의 설정을 만들면 자신만의 집을 짓는 것과 같아서 전기가 어떻게 작동하는지, 배관이 어떻게 작동하는지, 모든 것이 어떻게 연결되어 있는지 정확히 알 수 있습니다.

자신의 설정 = 자신의 코드베이스, nvim 설정은 Lua로 작성됩니다. 자신만의 설정을 작성하면 미니 프로젝트를 작성하는 것입니다. 각 파일을 알고, 설정의 "흐름"을 알며, 사전 구성된 설정의 기존 코드베이스에 "뛰어드는" 대신 처음부터 자신만의 코드베이스를 관리합니다.

#### 결론
개인 설정을 유지 관리하는 것이 더 나은 선택이라고 생각합니다. 처음에는 시간과 노력이 들지만 그만한 가치가 있습니다. 모든 사람이 자신만의 설정을 작성해야 하는 것은 아니지만 시도해 보는 것을 제안합니다.

_**참고**_: 사전 구성된 설정을 계속 사용하는 경우 다음 챕터의 일부는 관련이 없습니다. 건너뛸 수 있도록 알려드리겠습니다.

---

## 왜 프로그래밍 언어를 사용하여 편집기를 설정해야 할까요?
처음에는 편집기를 설정하기 위해 왜 Lua를 배우고 사용해야 하는지 이해하지 못했지만, 곧 그것이 편집기를 설정하는 올바른 방법이라는 것을 이해하게 되었습니다. 
코딩 지식을 활용하여 편집기에서의 경험을 향상시킬 수 있는 능력을 제공합니다.

이에 대한 훌륭한 기본 예는 제 `정의로 이동` 키 바인딩입니다.
```lua
goto_def = function()
	local ft = api.nvim_buf_get_option(0, 'filetype')
	if ft == 'man' then
		api.nvim_command(':Man ' .. vim.fn.expand('<cWORD>'))
	elseif ft == 'help' then
		api.nvim_command(':help ' .. vim.fn.expand('<cword>'))
	else
		require'telescope.builtin'.lsp_definitions()
	end
end
```
이는 `man 페이지`, `도움말 페이지` 또는 일반 코드 블록에서 정의로 이동하는 기능을 제공하며, 모두 동일한 바인딩에 있습니다! man 페이지를 탐색할 때 코드를 탐색하는 것처럼 느껴집니다.

다른 편집기에서는 내장/플러그인 함수가 처리하는 `.json`의 `값`이 될 것이므로, 이러한 종류의 동작을 얻으려면 플러그인을 작성해야 합니다.

---

## 기본 Lua
사전 구성된 설정을 사용하든 개인 설정을 사용하든 관계없이 Lua를 약간 배워야 합니다. 다행히도 매우 간단한 언어이므로, 예를 들어 파이썬을 배우는 것과 같은 방식으로 배우는 것을 제안합니다.

[nvim의 Lua 리소스 및 기본 사항은 여기](https://github.com/nanotee/nvim-lua-guide)에서 찾을 수 있습니다. 긴 가이드이며, 처음에는 참조 문서로 사용했고, 그 후에는 나중에 다룰 `:help nvim_*` 방법으로 전환했습니다.

#### Lua 모듈, 패키지 및 테이블
`모듈`과 `패키지`가 어떻게 작동하는지 이해하려면 Lua에서 `테이블`이 무엇인지 이해해야 합니다.

##### Lua 테이블
> 테이블은 Lua의 주요 (사실상 유일한) 데이터 구조화 메커니즘이며 강력한 메커니즘입니다. 테이블을 사용하여 일반 배열, 심볼 테이블, 집합, 레코드, 큐 및 기타 데이터 구조를 간단하고 균일하며 효율적인 방식으로 나타냅니다.
제가 아는 한 이것이 Lua가 매우 빠른 이유입니다.

<details><summary>테이블 사용 예시 (클릭하여 확장)</summary>

```lua
local my_table = {
	ofir = "gal"
}

for key, value in pairs(my_table) do
	print("key: " .. key .. ", value: " .. value)
end
-- 출력:
--   key: ofir, value: gal
print(my_table.ofir) -- 출력: gal

-------------------------------

local my_array = { 5, 6, 7 }
for _, value in ipairs(my_array) do
	print(value)
end
-- 출력:
--  5
--  6
--  7

-------------------------------

for index, value in ipairs(my_array) do
	print(index, value)
end
-- 출력:
--  1       5
--  2       6
--  3       7

-------------------------------

local my_dict = {
	["ofir"] = "gal"
}

for key, value in pairs(my_dict) do
	print("key: " .. key .. ", value: " .. value)
end
-- 출력:
--   key: ofir, value: gal
print(my_dict.ofir) -- 출력: gal
print(my_dict["ofir"]) -- 출력: gal
print(my_table["ofir"]) -- 출력: gal

```
[더 많은 예시 보기](https://www.lua.org/pil/2.5.html)

---
</details>

###### Lua 모듈
모듈은 내보낸 함수와 변수의 테이블입니다.

<details><summary>모듈 예시 (클릭하여 확장)</summary>

`module_example.lua`:
```lua
local M = {} -- 모듈의 테이블 초기화

-- 비공개 함수 예시
local function private_func(input)
	print("Foo: " .. input)
end

-- 내보낸 함수 예시
M.public_func = function(input)
	private_func(input)
end

return M -- 내보낸 함수 테이블 반환
```

사용 예시:
```lua
require('module_example').public_func("ofir")

local mod = require('module_example')
mod.public_func("ofir")
```

---
</details>

#### Lua 패키지
Lua 패키지는 Lua 모듈인 `init.lua`를 포함하는 폴더입니다.

<details><summary>패키지 예시 (클릭하여 확장)</summary>

`package_example/init.lua`:
```lua
local M = {}
local submod = require('anothermodule')

M.boo = function()
	submod.goo("ofir gal")
end

M.goo = submod.goo -- 패키지를 통해 submod.goo 노출

return M
```

`package_example/anothermodule.lua`:
```lua
local M = {}

M.goo = function(input)
	print("submod.goo: ".. input)
end

return M
```

사용 예시:
```lua
require('package_example').boo()
require('package_example').goo("amit tamari")
require('package_example.anothermodule').goo("하위 모듈 직접 호출")
require('package_example/anothermodule').goo("하위 모듈 직접 호출하는 다른 방법")
```

</details>

---

## 개인 설정 만드는 방법
### 별도 환경에서 nvim 실행
가장 먼저 할 일은 git 저장소에서 설정을 시작하는 것입니다. 별도의 저장소에서 설정을 관리하고 dotfiles의 git 하위 모듈로 사용하거나 dotfiles 저장소의 일부로 만들 수 있습니다.

nvim은 기본적으로 `~/.config/nvim`에서 설정을 로드하지만, 다른 디렉토리에서 로드하도록 설정할 수 있습니다:
```bash
XDG_CONFIG_HOME=~/wip_config/ XDG_DATA_HOME=~/.local/share/wip_nvim XDG_STATE_HOME=~/.local/state/wip_nvim nvim
```
이 줄은 nvim을 실행하고, `~/wip_config/nvim`에서 설정을 로드하며, 플러그인을 `~/.local/share/wip_nvim`에 저장하고 상태를 `~/.local/state/wip_nvim`에 저장합니다.

이는 nvim을 위한 [virtualenv](https://virtualenv.pypa.io/en/latest/)와 유사한 설정을 만듭니다. 개인 설정이 충분히 안정될 때까지 `개인 nvim` (예: `pnv`)을 실행하는 별칭을 설정하는 것을 추천합니다.
### 폴더 구조
자신의 설정은 자신의 코드베이스이므로 순서를 유지해야 합니다. 깔끔한 설정을 위한 기본 사항 중 하나는 폴더 구조입니다.

플러그인을 편집/추가할 때 오버헤드가 발생하지 않는 깔끔한 설정을 유지할 수 있는 구조를 찾으세요.

#### 기본 설정 폴더 구조 예시
nvim이 설정을 로드하는 방법을 이해하기 위해 간단한 폴더 구조와 메모를 만들었습니다:
```bash
📂 ~/wip_config/nvim
├── 🌑 init.lua # <---- 진입점
├── 📂 lua
│  ├── 🌑 module_example.lua # <---- `require('module_example')`에서 해석됨
│  └── 📂 package_example
│     ├── 🌑 init.lua # <---- `require('package_example')`에서 해석됨
│     └── 🌑 anothermodule.lua # <---- `require('package_example/anothermodule')`에서 해석됨
├── 📂 vim  # <---- vimscript 설정 파일
└── 📁 pack # <---- `packer` 컴파일 디렉토리, .gitignore에 추가됨
```

#### 추천 폴더 구조
이는 nvim 설정을 관리하는 방법에 대한 제 개인적인 의견이며, 다른 dotfiles/nvim 설정에서 영감을 얻으세요.
```bash
📂 ~/wip_config/nvim
├── 🌑 init.lua # 진입점, 원하는 순서대로 lua/* 모듈을 요구합니다.
└── 📂 lua
   ├── 🌑 autocmds.lua    # 일반 자동 명령
   ├── 🌑 keymaps.lua     # 키맵
   ├── 🌑 plugin_list.lua # `packer` 설정 (플러그인 목록)
   ├── 🌑 settings.lua    # nvim 설정 (vim.opt)
   ├── 🌑 ui.lua          # UI 플러그인 설정 (다른 플러그인보다 먼저 로드됨)
   ├── 🌑 usercmds.lua    # 일반 사용자 명령
   ├── 🌑 utils.lua       # 유틸리티 함수 (패키지일 수도 있음)
   └── 📂 plugins
      ├── 🌑 init.lua         # 모든 하위 모듈 로드 (플러그인 설정)
      ├── 🌑 autocomplete.lua # 자동 완성 엔진 설정
      ├── 🌑 debug.lua        # 디버그 관련 플러그인
      ├── 🌑 git.lua          # Git 관련 플러그인
      ├── 🌑 hydra.lua        # Hydra
      ├── 🌑 lsp.lua          # LSP 설정 및 관련 플러그인
      ├── 🌑 misc.lua         # 기타 플러그인
      ├── 🌑 telescope.lua    # Telescope + 확장 기능 설정
      └── 🌑 treesitter.lua   # Treesitter + 확장 기능 설정
```

이 가이드를 읽으면서 이 폴더 구조를 다시 만들고 파일을 작성하는 것을 제안합니다.

### 설정 구성 (Config Setup)
`settings.lua`부터 시작하겠습니다. vim 옵션(`vim.opt.*`)을 `settings.lua`로 옮기세요. 
이제 `init.lua`가 `settings.lua`를 다음과 같이 요구하도록 설정하세요:
```lua
require('settings')
```

nvim을 다시 시작하고 vim 옵션이 설정되었는지 확인하세요. 
`print`를 사용할 수 있다는 것을 기억하세요.

그 후에는 `keymaps.lua`와 `autocmds.lua`를 작성하는 것을 추천합니다.

#### 첫 번째 플러그인 설치
`plugin_list.lua` 작성부터 시작하겠습니다. 이 파일에서 설치된 플러그인을 관리합니다. 
여러 패키지 관리자가 있으며, 잘 알려진 것 중 하나는 [packer](https://github.com/wbthomason/packer.nvim)입니다. 
요약: [이 내용](https://github.com/wbthomason/packer.nvim#bootstrapping)을 `plugin_list.lua`에 복사하여 붙여넣고 `-- My plugins here` 주석 아래에 `use '{github user}/{repo}'`를 추가하세요.

nvim을 재설정하면 `:Packer` 명령이 존재하지 않으므로, 다음과 같이 `init.lua`에서 요구해야 합니다:
```lua
require('plugin_list')
```
추가된 플러그인을 설치하려면 반드시 `:PackerInstall`을 실행하세요.

첫 번째 플러그인을 성공적으로 설치한 후에는 설정할 차례입니다.

`plugins/init.lua` 파일을 만들고 [여기](https://github.com/ofirgall/dotfiles/blob/master/editors/nvim/lua/plugins/init.lua)에서 모든 하위 모듈을 요구하는 코드를 복사한 다음 `init.lua`에 `require('plugins')`를 추가하세요.

이제 각 플러그인 설정을 해당 파일에 추가하고 nvim을 다시 시작할 수 있습니다.

---

### nvim에서의 Lua 사용 및 nvim lua API
nvim에는 거의 모든 것에 대한 lua API가 있으며, 각 lua 함수는 도움말 문서를 생성하며 `:help nvim_*`을 통해 접근할 수 있습니다.

예를 들어, `vim.api.nvim_buf_get_name`에 대한 문서는 `:h nvim_buf_get_name`을 사용하여 접근할 수 있습니다.

명령줄에서 lua를 실행할 수 있습니다: `:lua print(vim.api.nvim_buf_get_name(0))`

[nanotee/nvim-lua-guide](https://github.com/nanotee/nvim-lua-guide)의 중요한 참조 링크 및 `:help` 태그:
* [nvim 옵션 관리 (vim.opt)](https://github.com/nanotee/nvim-lua-guide#using-meta-accessors) 또는 `:h vim.opt`
* [vim 변수 접근 (예: let:g)](https://github.com/nanotee/nvim-lua-guide#using-meta-accessors-1) 또는 `:h lua-vim-variables`
* [lua에서 사용자 명령 정의](https://github.com/nanotee/nvim-lua-guide#defining-user-commands) 또는 `:h nvim_create_user_command`
* [lua에서 사용자 명령 실행](https://github.com/nanotee/nvim-lua-guide#vimapinvim_command) 또는 `:h nvim_command`
* [lua에서 vim 함수 실행](https://github.com/nanotee/nvim-lua-guide#calling-vimscript-functions) 또는 `:h vim.fn`
* [lua에서 vimscript 실행](https://github.com/nanotee/nvim-lua-guide#vimapinvim_exec) 또는 `:h nvim_exec`
