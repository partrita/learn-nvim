# 분할 및 실제 탭

## 분할 (Splits) 또는 창 (Windows)
[챕터 1](01-the-vim-language.md)에서 분할이 무엇인지 이미 다루었지만, 제어하는 방법은 다루지 않았습니다.

* `:vsplit`/`:vs` - 수직 분할을 만듭니다.
* `:split` - 수평 분할을 만듭니다.
* `:q` - 분할을 닫습니다.
* `<C-w>` + `h`/`j`/`k`/`l` - 화살표 방향으로 분할을 이동합니다.
* `<C-w>=` - 모든 분할의 크기를 동일하게 조정합니다.
* `<C-w>>` - 너비를 늘립니다.
* `<C-w><` - 너비를 줄입니다.
* `<C-w>+` - 높이를 늘립니다.
* `<C-w>-` - 높이를 줄입니다.

### 설정 (Configure)
분할을 빠르게 이동, 생성 및 닫는 방법을 매핑하는 것을 추천합니다. (사전 구성된 설정을 사용하는 경우 일부 바인딩이 이미 설정되어 있을 수 있습니다.)

제 매핑:
```lua
map({'n', 't'}, '<C-h>', '<C-w>h')
map({'n', 't'}, '<C-j>', '<C-w>j')
map({'n', 't'}, '<C-k>', '<C-w>k')
map({'n', 't'}, '<C-l>', '<C-w>l')

map('n', '<M-e>', '<cmd>vsplit<cr>')
map('n', '<M-o>', '<cmd>split<cr>')

map('n', '<M-q>', '<cmd>q<cr>')
```

vim의 기본 분할 방향은 오늘날의 표준과 다릅니다. 이를 수정하려면 설정에 다음을 추가하세요:
```lua
vim.opt.splitright = true
vim.opt.splitbelow = true
```

#### 플러그인
tmux를 사용하는 경우 [Navigator.nvim](https://github.com/numToStr/Navigator.nvim)을 사용하여 vim 안팎으로 tmux 창 간을 원활하게 이동하는 것을 강력히 추천합니다.

---

## 실제 탭 (Actual Tabs)
실제 탭(다른 IDE에서처럼)을 구현하려면 `bufferline`/`tabline` 플러그인을 사용해야 합니다.

사전 구성된 설정에는 이미 하나가 있을 수 있지만, [여기](https://github.com/rockerBOO/awesome-neovim#tabline)에서 목록을 볼 수 있습니다. 저는 [bufferline.nvim](https://github.com/akinsho/bufferline.nvim)을 사용합니다.

탭을 빠르게 전환, 순환 및 닫는 키를 매핑해야 합니다.

제 설정:
```lua
-- Tabline 바인딩
map('n', '<C-q>', function() require('bufdelete').bufdelete(0, true) end) -- shift+Quit 현재 탭 닫기
map('n', 'g1', function() require('bufferline').go_to_buffer(1, true) end)
map('n', 'g2', function() require('bufferline').go_to_buffer(2, true) end)
map('n', 'g3', function() require('bufferline').go_to_buffer(3, true) end)
map('n', 'g4', function() require('bufferline').go_to_buffer(4, true) end)
map('n', 'g5', function() require('bufferline').go_to_buffer(5, true) end)
map('n', 'g6', function() require('bufferline').go_to_buffer(6, true) end)
map('n', 'g7', function() require('bufferline').go_to_buffer(7, true) end)
map('n', 'g8', function() require('bufferline').go_to_buffer(8, true) end)
map('n', 'g9', function() require('bufferline').go_to_buffer(9, true) end)
map('n', 'g0', function() require('bufferline').go_to_buffer(10, true) end)
map('n', '<M-j>', '<cmd>BufferLineCyclePrev<CR>') -- Alt+j 왼쪽으로 이동
map('n', '<M-k>', '<cmd>BufferLineCycleNext<CR>') -- Alt+k 오른쪽으로 이동
map('n', '<M-J>', '<cmd>BufferLineMovePrev<CR>') -- Alt+Shift+j 현재 탭을 왼쪽으로 이동
map('n', '<M-K>', '<cmd>BufferLineMoveNext<CR>') -- Alt+Shift+k 현재 탭을 오른쪽으로 이동
```
