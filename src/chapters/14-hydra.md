# [Hydra](https://github.com/anuvyklack/hydra.nvim)
Hydra는 nvim 내부에 하위 모드(submode)를 만드는 프레임워크이며, 하위 모드를 `Hydra`라고 합니다.

키 바인딩이나 lua 명령으로 `body`에 들어가면, 기존 키 위에 사용자 지정 키 매핑을 만들어 다양한 작업을 수행할 수 있게 합니다. \
사용자 지정 Hydra도 매우 쉽게 만들 수 있습니다.

Hydra 예시:
* [창 및 버퍼 관리](https://github.com/anuvyklack/hydra.nvim/wiki/Windows-and-buffers-management), 기본 방법보다 훨씬 편리하여 필수라고 생각합니다.
* [Git](https://github.com/anuvyklack/hydra.nvim/wiki/Git) nvim 내부에서 git을 관리하는 또 다른 도구입니다.
* [여기에서 모든 커뮤니티 Hydra를 찾을 수 있습니다](https://github.com/anuvyklack/hydra.nvim/wiki)

버퍼의 함수를 빠르게 스크롤할 수 있게 해주는 제 "사용자 지정" Hydra 예시입니다:
```lua
local ts_move = require'nvim-treesitter.textobjects.move'
-- 함수 위/아래 이동
local curr = Hydra({
	hint = [[
 _j_ _J_ : 위로
 _k_ _K_ : 아래로
  _<Esc>_
	]],
	config = {
		timeout = 4000,
		hint = {
			border = 'rounded'
		}
	},
	mode = {'n', 'x'},
	heads = {
		{ 'j', function ()
			ts_move.goto_next_start('@function.outer')
			center_screen()
		end },
		{ 'J', function ()
			ts_move.goto_next_end('@function.outer')
			center_screen()
		end },
		{ 'k', function ()
			ts_move.goto_previous_start('@function.outer')
			center_screen()
		end },
		{ 'K', function ()
			ts_move.goto_previous_end('@function.outer')
			center_screen()
		end },
		{ '<Esc>', nil,  { exit = true }}
	}
})
map({'n', 'x'}, 'gj', function ()
	ts_move.goto_next_start('@function.outer')
	center_screen()
	curr:activate()
end)
map('o', 'gj', function () ts_move.goto_next_start('@function.outer') end)

map({'n', 'x'}, 'gk', function ()
	ts_move.goto_previous_start('@function.outer')
	center_screen()
	curr:activate()
end)
map('o', 'gk', function () ts_move.goto_previous_start('@function.outer') end)

map({'n', 'x'}, 'gJ', function ()
	ts_move.goto_next_end('@function.outer')
	center_screen()
	curr:activate()
end)
map('o', 'gJ', function () ts_move.goto_next_end('@function.outer') end)

map({'n', 'x'}, 'gK', function ()
	ts_move.goto_previous_end('@function.outer')
	center_screen()
	curr:activate()
end)
map('o', 'gK', function () ts_move.goto_previous_end('@function.outer') end)
```
