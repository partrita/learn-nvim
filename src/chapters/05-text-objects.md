# 텍스트 객체 (Text Objects)
텍스트 객체는 어떤 면에서든 vim을 다른 편집기보다 우월하게 만들어 준 기능입니다.

텍스트 객체는 연산자 뒤에서만 작동하는 "이동"입니다. 
텍스트 객체는 시작과 끝으로 구성됩니다. 
기본적이고 가장 많이 사용되는 것은 `inner`/`a` + `X`입니다.

수식어:
* `i` - **I**nner (안쪽).
* `a` - **A** (하나의).

예를 들어:
* `yiw` - `yank inner word` (안쪽 단어 복사), 현재 단어를 복사합니다.
* `ciw` - `change inner word` (안쪽 단어 변경), 현재 단어를 변경합니다.
* `daw` - `delete a word` (단어 삭제), 현재 단어와 그 앞의 공백을 삭제하여 문장에서 단어를 제거합니다.
* `ci'` - `change inner '` (안쪽 ' 변경), 다음/현재 `'` 쌍 안의 텍스트, 즉 문자열을 변경합니다.
* `ca(` - `delete a (` (`(` 삭제), 다음/현재 `(` 쌍 안의 텍스트와 `(`를 삭제합니다.

모든 쌍에 대해 이러한 작업을 수행할 수 있습니다: `(`/`{`/`'`/`"`. 
HTML 태그(`t`), 문단(`p`) 등에도 이러한 작업을 수행할 수 있습니다.

앞에 숫자를 입력하여 작업을 반복할 수 있습니다. 예: `3daw`는 현재 단어와 다음 두 단어를 삭제합니다.

비주얼 모드로 들어가서 어떻게 작동하는지 자유롭게 테스트해 보세요.

이에 대한 자세한 내용은 `:help text-objects`에서 읽을 수 있습니다.

---

제가 가장 좋아하는 텍스트 객체 중 하나는 `paragraph` (문단)입니다. 코드를 편집하는 것이 매우 자연스럽게 느껴집니다.

`boo`와 `goo`의 순서를 바꾸고 싶다면, `dap`로 `goo` 문단을 삭제하고, `{`로 이전 문단으로 돌아가서 삭제된 문단을 `p`로 붙여넣을 수 있습니다.
```python
def foo():
	result = boo()
	if result is not None:
		return result
	
	result = goo() # <--- 커서 위치
	if result is not None:
		return result
	
	return None
```

---

## Treesitter 텍스트 객체
[nvim-treesitter-textobjects](https://github.com/nvim-treesitter/nvim-treesitter-textobjects)는 treesitter 쿼리에서 텍스트 객체를 생성하는 멋진/필수 플러그인입니다. 즉, 실제 코드 부분에 대한 텍스트 객체입니다!

제가 사용하는 설정에서 `f`는 함수이므로, 현재 있는 함수의 내용을 변경하고 싶으면 `cif` (`change inner function`)를 누릅니다. 다른 코드 객체에 대해서도 이 작업을 수행할 수 있습니다.

커서를 어디로 어떻게 옮길지가 아니라 코드 객체 이동으로 코드 편집에 대한 생각을 바꾸게 합니다. 
예를 들어, 다음 함수의 세 번째 인수를 변경합니다.
```python
def foo(a: int, b: Any, c: Tuple[int, Optional[str]]):
	pass # <--- 커서 위치
```
`[m`을 사용하여 함수 시그니처로 이동한 다음, `]a`를 3번 누르고 (안타깝게도 [아직](https://github.com/nvim-treesitter/nvim-treesitter-textobjects/issues/231) `3]a`를 수행할 수는 없습니다), 그런 다음 `cia`를 눌러 `,`는 유지하지만 인수의 내용을 변경하거나 `cad`를 눌러 전체 인수를 삭제할 수 있습니다.

표준 편집기에서는 시그니처로 수동으로 이동하거나 역방향 검색을 사용하고, `ctrl`을 누른 상태에서 화살표를 눌러 `c`에 도달한 다음, `ctrl+shift`를 누른 상태에서 오른쪽 화살표를 9번 눌러야 합니다 (편집기에 따라 다름, sublime에서 테스트). 이는 지루한 작업입니다.

코드 요소와 관련된 커서 이동 방법을 생각하는 대신, 코드의 요소(`다음/이전 함수로 이동`, `안쪽 함수 복사`, `함수 삭제`, `안쪽 인수 변경`)로 생각하게 되어 코드 편집에 대한 제 생각을 바꾸었습니다.

---

### 설정 (Config)
제 설정 (쌍 이동도 추가):
```lua
textobjects = {
	move = {
		enable = true,
		set_jumps = true, -- 점프 목록에 점프를 설정할지 여부
		goto_next_start = {
			["]m"] = "@function.outer",
			["gj"] = "@function.outer",
			["]]"] = "@class.outer",
			["]b"] = "@block.outer",
			["]a"] = "@parameter.inner",
		},
		goto_next_end = {
			["]M"] = "@function.outer",
			["gJ"] = "@function.outer",
			["]["] = "@class.outer",
			["]B"] = "@block.outer",
			["]A"] = "@parameter.inner",
		},
		goto_previous_start = {
			["[m"] = "@function.outer",
			["gk"] = "@function.outer",
			["[["] = "@class.outer",
			["[b"] = "@block.outer",
			["[a"] = "@parameter.inner",
		},
		goto_previous_end = {
			["[M"] = "@function.outer",
			["gK"] = "@function.outer",
			["[]"] = "@class.outer",
			["[B"] = "@block.outer",
			["[A"] = "@parameter.inner",
		},
	},
	select = {
		enable = true,
		lookahead = true,
		keymaps = {
			["af"] = "@function.outer",
			["if"] = "@function.inner",
			["ac"] = "@class.outer",
			["ic"] = "@class.inner",
			["ab"] = "@block.outer",
			["ib"] = "@block.inner",
			["al"] = "@loop.outer",
			["il"] = "@loop.inner",
			["a/"] = "@comment.outer",
			["i/"] = "@comment.outer", -- 주석에는 inner 없음
			["aa"] = "@parameter.outer", -- 매개변수 -> 인수
			["ia"] = "@parameter.inner",
		},
	},
},
```

LunarVim용:
```lua
lvim.builtin.treesitter.textobjects.select = {
	enable = true,
	lookahead = true,
	keymaps = {
		["af"] = "@function.outer",
		["if"] = "@function.inner",
		["ac"] = "@class.outer",
		["ic"] = "@class.inner",
		["ab"] = "@block.outer",
		["ib"] = "@block.inner",
		["al"] = "@loop.outer",
		["il"] = "@loop.inner",
		["a/"] = "@comment.outer",
		["i/"] = "@comment.outer", -- 주석에는 inner 없음
		["aa"] = "@parameter.outer", -- 매개변수 -> 인수
		["ia"] = "@parameter.inner",
	},
}
lvim.builtin.treesitter.textobjects.move = {
	enable = true,
	set_jumps = true, -- 점프 목록에 점프를 설정할지 여부
	goto_next_start = {
		["]m"] = "@function.outer",
		["gj"] = "@function.outer",
		["]]"] = "@class.outer",
		["]b"] = "@block.outer",
		["]a"] = "@parameter.inner",
	},
	goto_next_end = {
		["]M"] = "@function.outer",
		["gJ"] = "@function.outer",
		["]["] = "@class.outer",
		["]B"] = "@block.outer",
		["]A"] = "@parameter.inner",
	},
	goto_previous_start = {
		["[m"] = "@function.outer",
		["gk"] = "@function.outer",
		["[["] = "@class.outer",
		["[b"] = "@block.outer",
		["[a"] = "@parameter.inner",
	},
	goto_previous_end = {
		["[M"] = "@function.outer",
		["gK"] = "@function.outer",
		["[]"] = "@class.outer",
		["[B"] = "@block.outer",
		["[A"] = "@parameter.inner",
	},
}
```
