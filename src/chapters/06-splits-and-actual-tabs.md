# 화면 분할과 탭 활용

## 화면 분할 (Splits) 또는 창 (Windows)
[챕터 1](01-the-vim-language.md)에서 화면 분할을 잠깐 언급했지만, 이번에는 이를 제어하는 구체적인 방법을 알아보겠습니다.

* `:vsplit` (또는 `:vs`): 화면을 세로로 나눕니다.
* `:split` (또는 `:sp`): 화면을 가로로 나눕니다.
* `:q`: 현재 분할된 창을 닫습니다.
* `Ctrl + w` 뒤에 `h/j/k/l`: 원하는 방향의 창으로 이동합니다.
* `Ctrl + w` 뒤에 `=`: 모든 창의 크기를 똑같이 맞춥니다.
* `Ctrl + w` 뒤에 `>` / `<`: 현재 창의 너비를 늘리거나 줄입니다.
* `Ctrl + w` 뒤에 `+` / `-`: 현재 창의 높이를 늘리거나 줄입니다.

### 편리한 단축키 설정
창 사이를 이동할 때마다 `Ctrl + w`를 누르는 건 다소 번거로운 일입니다. 다음과 같이 단축키를 지정해 두면 한결 편안하게 창을 오갈 수 있습니다.

```lua
-- 창 이동 간소화
vim.keymap.set({'n', 't'}, '<C-h>', '<C-w>h')
vim.keymap.set({'n', 't'}, '<C-j>', '<C-w>j')
vim.keymap.set({'n', 't'}, '<C-k>', '<C-w>k')
vim.keymap.set({'n', 't'}, '<C-l>', '<C-w>l')

-- 빠른 화면 분할 및 닫기
vim.keymap.set('n', '<M-e>', '<cmd>vsplit<cr>') -- Alt+e
vim.keymap.set('n', '<M-o>', '<cmd>split<cr>')  -- Alt+o
vim.keymap.set('n', '<M-q>', '<cmd>q<cr>')      -- Alt+q
```

또한 새로 분할된 창이 현대적인 방식대로 오른쪽이나 아래쪽에서 열리도록 설정하는 걸 추천합니다.
```lua
vim.opt.splitright = true
vim.opt.splitbelow = true
```

#### 추천 플러그인
tmux를 사용 중이라면 [Navigator.nvim](https://github.com/numToStr/Navigator.nvim)을 꼭 써보세요. Neovim의 창과 tmux의 패널 사이를 마치 하나의 프로그램처럼 매끄럽게 넘나들 수 있게 해줍니다.

---

## 실제 탭 (Actual Tabs) 활용
Vim에서의 탭은 다른 IDE의 탭과는 개념이 조금 다릅니다. 우리가 흔히 생각하는 '열린 파일 목록'으로서의 탭을 쓰려면 별도의 플러그인이 필요합니다.

커뮤니티에는 수많은 [탭라인(Tabline) 플러그인](https://github.com/rockerBOO/awesome-neovim#tabline)이 존재하며, 가장 인기 있는 선택지는 [bufferline.nvim](https://github.com/akinsho/bufferline.nvim)입니다.

### 탭 제어를 위한 단축키
탭을 빠르게 전환하거나 닫는 단축키를 설정해 두면 업무 효율이 크게 올라갑니다.

```lua
-- 버퍼라인(탭) 조작 예시
vim.keymap.set('n', '<M-j>', '<cmd>BufferLineCyclePrev<CR>') -- Alt+j 이전 탭
vim.keymap.set('n', '<M-k>', '<cmd>BufferLineCycleNext<CR>') -- Alt+k 다음 탭
vim.keymap.set('n', '<M-J>', '<cmd>BufferLineMovePrev<CR>')  -- Alt+Shift+j 탭 순서 앞으로
vim.keymap.set('n', '<M-K>', '<cmd>BufferLineMoveNext<CR>')  -- Alt+Shift+k 탭 순서 뒤로

-- 숫자 키로 특정 탭 바로 가기 (1~9)
for i = 1, 9 do
    vim.keymap.set('n', 'g' .. i, function() 
        require('bufferline').go_to_buffer(i, true) 
    end)
end
```
화면 분할과 탭 활용에 익숙해지면, 여러 파일을 동시에 오가는 작업이 이전과는 비교할 수 없을 정도로 쾌적해질 것입니다.
