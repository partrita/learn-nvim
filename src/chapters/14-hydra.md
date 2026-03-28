# Hydra를 이용한 단축키 관리
[Hydra.nvim](https://github.com/anuvyklack/hydra.nvim)은 Neovim 내부에 일종의 '하위 모드(Submode)'를 만들 수 있게 해주는 프레임워크입니다. 이를 통해 여러 단축키를 하나의 테마로 묶어 효율적으로 관리할 수 있습니다.

Hydra 모드에 진입하면, 기존의 단축키들이 지정된 커스텀 조작으로 바뀝니다. 예를 들어 '화면 크기 조절 모드'에 들어갔다면, 평소에는 이동 키였던 `h, j, k, l`을 화면 너비와 높이를 조절하는 용도로 쓸 수 있게 되는 식이죠.

---

## 주요 활용 사례
* **화면 및 버퍼 관리**: 창 분할이나 탭 이동처럼 반복 조작이 많은 작업을 아주 쾌적하게 만들어 줍니다.
* **Git 조작**: Gitsigns와 연동해 헝크 단위로 이동하거나 스테이징하는 작업을 하나의 모드 안에서 처리할 수 있습니다.
* **커스텀 탐색**: [Hydra Wiki](https://github.com/anuvyklack/hydra.nvim/wiki)에서 커뮤니티가 만든 다양한 설정 예시를 확인해 보세요.

### 활용 예시: 함수 간 빠른 탐색
다음은 제가 직접 사용 중인, 현재 파일의 함수들 사이를 빠르게 오가는 Hydra 설정입니다. 
`gj` 키로 진입하면 `j, k` 키만으로 함수들 사이를 톡톡 튀어 다니듯 이동할 수 있습니다.

```lua
local ts_move = require('nvim-treesitter.textobjects.move')

local function center_screen()
    vim.cmd('normal! zz')
end

local function_nav = Hydra({
    hint = [[
 ^ ^  함수 탐색 모드  ^ ^
 ^ _j_ / _J_ : 다음 함수 시작/끝
 ^ _k_ / _K_ : 이전 함수 시작/끝
 ^    _<Esc>_ : 나가기
    ]],
    config = {
        timeout = 4000,
        hint = { border = 'rounded' }
    },
    mode = {'n', 'x'},
    heads = {
        { 'j', function() ts_move.goto_next_start('@function.outer'); center_screen() end },
        { 'J', function() ts_move.goto_next_end('@function.outer'); center_screen() end },
        { 'k', function() ts_move.goto_previous_start('@function.outer'); center_screen() end },
        { 'K', function() ts_move.goto_previous_end('@function.outer'); center_screen() end },
        { '<Esc>', nil, { exit = true } }
    }
})

-- 진입점 설정
vim.keymap.set({'n', 'x'}, 'gj', function()
    ts_move.goto_next_start('@function.outer')
    center_screen()
    function_nav:activate()
end, { desc = '함수 탐색 모드 진입' })
```

이처럼 Hydra를 활용하면 복잡한 키 조합 없이도 반복적인 작업을 우아하고 직관적으로 처리할 수 있습니다.
