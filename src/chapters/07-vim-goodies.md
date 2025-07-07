# Vim 유용한 기능들
이 챕터에서는 다양한 vim 기능 중 몇 가지를 간략하게 다룰 것입니다.

## 퀵픽스 목록 (Quickfix list)
퀵픽스 목록은 `파일`, `위치(행, 열)` 및 `텍스트` 항목을 포함하는 목록입니다. 
퀵픽스 목록을 채우는 방법은 여러 가지가 있으며, 개인적으로는 나중에 다룰 `:help make` 및 `telescope.nvim`을 사용하여 채웁니다.

주로 검색 결과 및 컴파일 오류를 저장하는 데 사용됩니다.

### 명령어
* `:copen` - 퀵픽스 목록을 엽니다.
* `:cclose` - 퀵픽스 목록을 닫습니다.
* `:cnext` - qf 목록의 다음 항목으로 이동합니다.
* `:cprev` - qf 목록의 이전 항목으로 이동합니다.

다음/이전 항목으로 이동하는 `]q` 및 `[q`를 추가하는 [vim-unimpaired](https://github.com/tpope/vim-unimpaired)를 설치하는 것을 추천합니다.

## 대체 명령 (Substitute Command)
`s` 명령은 현재 편집 중인 버퍼에서 검색 및 바꾸기를 하는 데 사용됩니다. 
구문은 `sed` cli 도구와 유사합니다.

이 명령은 매우 강력하며, `:help :substitute`에서 더 자세히 알아보거나 구글에서 검색할 수 있습니다.

몇 가지 예시:
* `:s/ofir/gal/` - 현재 줄에서 `ofir`의 첫 번째 발생을 찾아 `gal`로 바꿉니다.
* `:s/ofir/gal/g` - 현재 줄에서 `ofir`의 모든 발생을 찾아 `gal`로 바꿉니다.
* `:%s/ofir/gal/` - 현재 버퍼의 각 줄에서 `ofir`의 첫 번째 발생을 찾아 `gal`로 바꿉니다.
* `:%s/ofir/gal/g` - 위와 동일하지만 모든 발생에 대해 수행합니다.

커서 아래 단어의 이름을 바꾸는 추천 키맵:
```lua
-- 제 <F2>는 lsp rename에 바인딩되어 있습니다.
map('n', '<leader><F2>', '*:%s///g<left><left>') -- <leader>F2로 현재 단어 이름 바꾸기
map('x', '<F2>', '"hy:%s/<C-r>h//g<left><left>') -- 비주얼 모드에서 선택한 텍스트 이름 바꾸기
```

#### 플러그인
[text-case.nvim](https://github.com/johmsalas/text-case.nvim)을 사용하면 텍스트를 바꾸고 텍스트의 대소문자를 유지할 수 있습니다.

이 텍스트에 대해 `:Subs/ofir gal/amit tamari`를 실행하면:
```
OfirGal
ofirGal
```
다음과 같은 텍스트가 됩니다:
```
AmitTamari
amitTamari
```

또한 대소문자를 변경하는 lua API를 제공하며, 저는 대소문자를 빠르게 변경하기 위해 다음과 같은 사용자 명령을 만들었습니다.
```lua
local api = vim.api
local textcase = require('textcase')
textcase.setup {
}

api.nvim_create_user_command('UpperCase', function() textcase.current_word('to_upper_case') end, {})
api.nvim_create_user_command('LowerCase', function() textcase.current_word('to_lower_case') end, {})
api.nvim_create_user_command('SnakeCase', function() textcase.current_word('to_snake_case') end, {})
api.nvim_create_user_command('ConstantCase', function() textcase.current_word('to_dash_case') end, {})
api.nvim_create_user_command('DashCase', function() textcase.current_word('to_constant_case') end, {})
api.nvim_create_user_command('DotCase', function() textcase.current_word('to_dot_case') end, {})
api.nvim_create_user_command('CamelCase', function() textcase.current_word('to_camel_case') end, {})
api.nvim_create_user_command('PascalCase', function() textcase.current_word('to_pascal_case') end, {})
api.nvim_create_user_command('TitleCase', function() textcase.current_word('to_title_case') end, {})
api.nvim_create_user_command('PathCase', function() textcase.current_word('to_path_case') end, {})
api.nvim_create_user_command('PhraseCase', function() textcase.current_word('to_phrase_case') end, {})
```

## 전역 명령 (Global command)
`g` 명령은 패턴으로 줄을 필터링하여 버퍼 전체에 "vim" 명령을 적용하는 데 사용됩니다.

예를 들어:
* `:g/ofir/d` - `ofir`가 포함된 모든 줄을 삭제합니다.

이 명령은 매우 강력하며, `:help :global`에서 더 자세히 알아보거나 구글에서 검색할 수 있습니다.

## 매크로 (Macros)
유사한 변경 사항을 빠르게 적용하기 위해 매크로(키 입력 세트)를 기록하고 재생할 수 있습니다.

기록을 시작하려면 `q{a-z}`를 누릅니다. 왼쪽 하단에 `recording @{a-z}`가 표시되며, 기록을 중지하려면 `q`를 다시 누릅니다. 이렇게 하면 매크로가 `{a-z}`에 저장되어 나중에 사용할 수 있습니다. 
매크로를 재생하려면 `@{a-z}`를 누릅니다.

매크로를 한 번 기록하고 여러 줄에 여러 번 사용하세요.

#### 사용 예시
요일 목록이 있는데, 이 목록을 리스트 안에 저장해야 하며 모든 요일은 소문자여야 합니다. 
요일 enum이 있는 코드가 있지만 파이썬으로 마이그레이션해야 합니다.
```c
enum Days {
	Sunday = 0,
	Monday = 1,
	Tuesday = 2,
	Wednesday = 3,
	Thursday = 4,
	Friday = 5,
	Saturday = 6,
};
```
원하는 결과:
```python
days = [
	'sunday',
	'monday',
	'tuesday',
	'wednesday',
	'thursday',
	'friday',
	'saturday',
]
```

먼저 enum 내부의 모든 요일을 파이썬 파일로 가져오지만, 요일 이름만 있는 리스트로 만들어야 합니다. 
첫 글자의 대소문자를 변경하고, 숫자를 삭제하고, `'`를 추가하여 요일 문자열을 만드는 매크로를 기록할 수 있습니다.

매크로를 기록하는 동안 첫 번째 요일을 수동으로 변경할 것입니다.

매크로: `qa^guui'<Esc>ea'<Esc>ldt,jq`. 
분석:
1. `qa` - `a`에 매크로 기록 시작
1. `^` - 줄의 시작으로 이동
1. `guu` - 현재 문자를 소문자로 변경
1. `i'<Esc>` - 입력 모드로 들어가서 `'`를 추가하고 입력 모드에서 나옵니다.
1. `e` - 단어 끝으로 이동
1. `a'<Esc>` - 단어 뒤에서 입력 모드로 들어가서 `'`를 추가하고 입력 모드에서 나옵니다.
1. `l` - 방금 추가한 `'`에서 오른쪽으로 이동
1. `dt,` - `,`까지 내용 삭제 (`= <숫자>`)
1. `j` - 다음 줄로 이동하여 매크로를 반복할 수 있도록 합니다.
1. `q` - 매크로 기록 완료.

첫 번째 요일 위에 매크로를 기록한 후 6일이 남았습니다. `6@a`를 누르면 매크로가 6번 반복되어 모든 요일이 변경됩니다.

#### 플러그인

[vim-buffest](https://github.com/rbong/vim-buffest)를 사용하여 기록 후 매크로를 편집할 수 있습니다.

## 점(.)으로 반복
방금 수행한 작업을 반복하려면 `.`을 누를 수 있습니다. 
마지막으로 수행한 작업만 저장하는 매크로라고 생각할 수 있습니다.

#### 사용 예시
```
apple banana orange
```
모든 과일을 `fruit`로 바꾸고 싶지만, `apple`을 `ciwfruit<Esc>`를 사용하여 `fruit`로 이미 변경한 후에야 깨달았고 매크로를 다시 기록하고 싶지 않습니다.

변경한 후 다음 단어(가급적 `w` 사용)로 이동하여 `.`을 누르면 현재 단어가 `fruit`로 변경됩니다.

`:help gn`과 결합하면 멋진 작업을 수행할 수 있습니다.

## 외부 명령 (External Command)
vim에서 외부 터미널 명령을 실행할 수 있습니다. 예: `!ls`

## 접기 (Folds)
vim은 접기를 지원하지만, 개인적으로 이 기능이 필요하다고 생각한 적은 없습니다. 자동으로 접히지 않도록 설정했지만, [여기](https://vim.fandom.com/wiki/Folding)에서 접기에 대해 더 자세히 알아보고 [nvim-ufo](https://github.com/kevinhwang91/nvim-ufo)를 확인해 보세요.

```lua
opt.foldlevelstart = 99 -- 자동 접기 안 함
```
