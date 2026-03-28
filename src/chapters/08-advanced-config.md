# 고급 설정 가이드
Vim의 기초를 어느 정도 익혔다면, 이제 Neovim을 단순한 도구에서 강력한 무기로 진화시킬 차례입니다. 이번 챕터에서는 풍부한 플러그인 생태계와 설정의 자유로움을 극대화하는 방법을 다루겠습니다.

---

## 개인 설정 vs 사전 구성된 설정 (Distro)
어떤 방식으로 Neovim을 시작할지는 사용자마다 다를 수 있습니다. 각 방식의 장단점을 명확히 알고 선택하는 것이 중요합니다.

#### 사전 구성된 설정 (Pre-configured Distros)
대표적으로 **LunarVim**, **AstroNvim**, **NvChad** 등이 있습니다. 커뮤니티에서 검증된 훌륭한 설정을 즉시 사용할 수 있다는 게 큰 장점입니다. 하지만 설정 위에 또 다른 '추상화 계층'이 생기기 때문에, 기본 제공되지 않는 플러그인을 추가하거나 내부 동작을 세세하게 바꾸려 할 때 예상치 못한 복잡함에 부딪힐 수 있습니다.

마치 **'풀 옵션으로 인테리어가 끝난 월셋집'**에 들어가는 것과 같습니다. 살기에는 매우 편하지만, 벽 하나를 허물거나 배관 구조를 바꾸고 싶을 때 모든 게 내 마음대로 되지 않을 수도 있죠.

#### 개인 설정 (Personal Config)
자신만의 설정을 처음부터 쌓아 올리는 건 **'자신만의 집을 직접 짓는 것'**과 같습니다. 전선이 어디로 지나가는지, 수도관이 어떻게 연결되었는지 정확히 알 수 있죠.

개인 설정은 곧 자신만의 코드베이스입니다. 모든 파일을 내가 직접 만들고 관리하기 때문에, 설정의 흐름을 완벽히 장악할 수 있습니다. 사전 설정된 거대한 코드베이스를 분석하며 헤맬 필요가 없다는 것이 가장 큰 매력입니다.

#### 결론
저는 개인 설정을 유지하고 관리하는 방식을 강력히 추천합니다. 초기에는 시간과 노력이 꽤 들겠지만, 그만한 가치가 충분합니다. 물론 누구나 처음부터 전문가가 될 필요는 없습니다. 사전 설정으로 감을 잡은 뒤에 천천히 자신만의 세계를 구축해 보셔도 늦지 않습니다.

---

## 왜 프로그래밍 언어(Lua)로 편집기를 설정할까요?
처음에는 "편집기 설정을 위해 굳이 Lua를 배워야 하나?" 싶었지만, 금세 그것이 Neovim의 진정한 가치라는 걸 깨달았습니다. 코딩 실력을 활용해 편집 환경을 개선하는 즐거움이 생각보다 큽니다.

가장 좋은 예시는 커스텀 `정의로 이동(Go to Definition)` 기능입니다.
```lua
goto_def = function()
	local ft = vim.api.nvim_buf_get_option(0, 'filetype')
	if ft == 'man' then
		-- man 페이지에서는 Man 명령 실행
		vim.api.nvim_command(':Man ' .. vim.fn.expand('<cWORD>'))
	elseif ft == 'help' then
		-- 도움말 페이지에서는 help 명령 실행
		vim.api.nvim_command(':help ' .. vim.fn.expand('<cword>'))
	else
		-- 일반 코드에서는 LSP 기능 활용
		require('telescope.builtin').lsp_definitions()
	end
end
```
이 짧은 코드로 도움말, Man 페이지, 소스 코드를 가리지 않고 하나의 단축키로 '정의'를 찾아갈 수 있습니다. 다른 편집기라면 JSON 설정의 값만으로는 구현할 수 없어 별도의 플러그인을 개발해야 했을 기능입니다.

---

## Lua 기초 이해하기
Neovim 설정을 깊이 있게 다루려면 Lua를 조금은 알아야 합니다. 다행히 파이썬처럼 배우기 매우 쉬운 언어입니다.

[Neovim Lua 가이드](https://github.com/nanotee/nvim-lua-guide)를 참고해 보세요. 처음에는 필요할 때마다 찾아보는 참조용으로 쓰시다가, 점차 `:help nvim_*` 명령어로 익숙해지시는 걸 추천합니다.

#### 핵심 개념: 테이블(Table)
Lua의 유일무이하고 강력한 데이터 구조입니다. 배열, 사전, 레코드, 큐 등 거의 모든 데이터 형식을 이 테이블 하나로 표현합니다. Neovim이 엄청나게 빠른 이유 중 하나이기도 하죠.

<details><summary>테이블 활용 예시 (클릭)</summary>

```lua
-- 사전(Dictionary)처럼 사용
local my_dict = {
	name = "ofir",
	job = "developer"
}
print(my_dict.name) -- ofir

-- 배열(Array)처럼 사용 (인덱스가 1부터 시작함에 주의!)
local my_array = { 10, 20, 30 }
print(my_array[1]) -- 10
```
</details>

---

## 나만의 설정 구축하기
### 독립된 환경에서 연습하기
기존 설정을 망가뜨리지 않고 새로운 설정을 시작하려면 별도의 디렉토리를 사용하는 것이 좋습니다.
```bash
XDG_CONFIG_HOME=~/test_config/ XDG_DATA_HOME=~/.local/share/test_nvim nvim
```
이렇게 하면 `~/test_config/nvim`에서 설정을 불러오며, 플러그인과 상태 정보도 별도의 경로에 저장됩니다. 새로운 설정이 안정될 때까지 별칭(alias)을 만들어 연습해 보세요.

### 폴더 구조 설계하기
깔끔한 설정을 유지하려면 처음부터 구조를 잘 잡아야 합니다. 파일 하나에 모든 설정을 몰아넣기보다, 역할별로 파일을 나누는 것이 장기적으로 훨씬 유리합니다.

#### 추천하는 폴더 구조 예시
```text
📂 ~/.config/nvim
├── 🌑 init.lua        # 진입점 (가장 먼저 실행됨)
└── 📂 lua
   ├── 🌑 settings.lua    # 일반 옵션 (vim.opt)
   ├── 🌑 keymaps.lua     # 단축키 설정
   ├── 🌑 autocmds.lua    # 자동 실행 명령 (Autocmds)
   ├── 🌑 plugins.lua     # 플러그인 목록 및 설치 설정
   └── 📂 conf            # 각 플러그인의 상세 설정
      ├── 🌑 lsp.lua
      ├── 🌑 telescope.lua
      └── 🌑 ui.lua
```

### 시작은 `init.lua`부터
`init.lua`에서 다른 파일들을 불러오도록 구성하세요.
```lua
require('settings')
require('keymaps')
require('plugins')
```

---

## Neovim Lua API 활용
Neovim의 거의 모든 기능은 Lua API를 통해 접근할 수 있습니다. 궁금한 함수가 있다면 `:help nvim_`으로 시작하는 도움말을 찾아보세요.

* `:h vim.opt`: 옵션 관리
* `:h lua-vim-variables`: 변수 접근 (`vim.g`, `vim.b` 등)
* `:h nvim_create_user_command`: 사용자 명령어 정의
* `:h vim.fn`: Vim 내장 함수 실행

Lua의 힘을 빌려 여러분만의 완벽한 편집 환경을 만들어 나가시길 응원합니다!
