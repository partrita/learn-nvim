# 텍스트 객체
Vim을 다른 편집기보다 훨씬 강력하게 만들어 주는 가장 핵심적인 기능이 바로 '텍스트 객체(Text Objects)'입니다.

텍스트 객체는 연산자와 결합해 특정 범위를 지정하는 '이동'의 일종입니다. 텍스트의 시작과 끝을 일일이 지정할 필요 없이, 논리적인 단위(단어, 문장, 괄호 안 등)로 텍스트를 다룰 수 있게 해줍니다.

### 기본 구성: `i`(Inner)와 `a`(A)
가장 많이 쓰이는 형태는 `i`(안쪽) 또는 `a`(포함) 뒤에 대상 객체를 붙이는 것입니다.

* `i`: **I**nner (안쪽 내용만)
* `a`: **A** (객체 전체를 포함해서)

예를 들어 다음과 같은 조작이 가능합니다.
* `ciw`: **C**hange **I**nner **W**ord (현재 단어를 삭제하고 바로 입력 모드로 전환)
* `daw`: **D**elete **A** **W**ord (단어와 그 주변 공백까지 통째로 삭제)
* `ci'`: **C**hange **I**nner **'** (따옴표(`'`) 안의 문자열만 변경)
* `ca(`: **C**hange **A** **(** (괄호와 괄호 안의 내용 전체를 변경)

괄호(`()`, `{}`, `[]`), 따옴표(`'`, `"`), HTML 태그(`t`), 문단(`p`) 등 다양한 객체에 동일한 규칙이 적용됩니다.

앞에 숫자를 붙여서 작업을 반복할 수도 있습니다. 예: `3daw`는 현재 단어를 포함해 다음 세 단어를 모두 삭제합니다.

더 자세한 내용은 `:help text-objects`를 읽어보세요. 비주얼 모드(`v`)에서 직접 테스트해 보시는 것도 좋은 학습 방법입니다.

---

### 문단(Paragraph) 객체 활용하기
개인적으로 가장 좋아하는 객체 중 하나는 `p`(문단)입니다. 코드 덩어리를 옮길 때 정말 편리합니다.

함수 내에서 특정 코드 블록의 순서를 바꾸고 싶을 때, `dap`(문단 전체 삭제)를 사용해 지운 뒤 원하는 위치에서 `p`로 붙여넣으면 됩니다. 마우스로 영역을 잡을 필요 없이 단 세 번의 키 입력으로 해결됩니다.

```python
def foo():
    # 코드 블록 A
    result = boo()
    if result is not None:
        return result
    
    # 코드 블록 B <--- 이 위치에서 'dap' 수행
    result = goo() 
    if result is not None:
        return result
    
    return None
```

---

## Treesitter 텍스트 객체
[nvim-treesitter-textobjects](https://github.com/nvim-treesitter/nvim-treesitter-textobjects)는 프로그래밍 언어의 구조를 이해하는 텍스트 객체를 제공하는 필수 플러그인입니다.

기존의 단순한 괄호나 단어 단위를 넘어, 실제 코드의 의미적 단위(함수, 클래스, 매개변수 등)로 텍스트를 조작할 수 있게 해줍니다.

예를 들어 다음과 같은 조작이 가능해집니다.
* `cif`: **C**hange **I**nner **F**unction (현재 함수의 본문 전체를 수정)
* `cia`: **C**hange **I**nner **A**rgument (현재 함수의 특정 인자만 수정)

### 코드 편집에 대한 관점의 변화
이 기능을 쓰기 시작하면 '커서를 어디로 옮길까'가 아니라 '어떤 코드 객체를 다룰까'로 생각이 바뀌게 됩니다.

예를 들어, 세 번째 매개변수를 바꾸고 싶을 때 화살표 키나 마우스를 쓰는 대신, `]a`(다음 인자로 이동)와 `cia`(인자 수정)를 조합해 순식간에 작업을 마칠 수 있습니다.

```python
def foo(a: int, b: Any, c: Tuple[int, Optional[str]]):
    pass # <--- 커서 위치
```
표준 편집기라면 화살표 키를 수십 번 누르거나 검색 기능을 써야 하겠지만, Neovim에서는 `[m`(함수 시작으로 점프) -> `]a` (인자 이동) -> `cia`(인자 수정) 같은 식으로 명확한 의도를 가지고 조작할 수 있습니다.

---

### 추천 설정 예시 (LunarVim 기준)
```lua
lvim.builtin.treesitter.textobjects.select = {
    enable = true,
    lookahead = true,
    keymaps = {
        ["af"] = "@function.outer",
        ["if"] = "@function.inner",
        ["ac"] = "@class.outer",
        ["ic"] = "@class.inner",
        ["aa"] = "@parameter.outer",
        ["ia"] = "@parameter.inner",
    },
}

lvim.builtin.treesitter.textobjects.move = {
    enable = true,
    set_jumps = true,
    goto_next_start = {
        ["]m"] = "@function.outer",
        ["]]"] = "@class.outer",
        ["]a"] = "@parameter.inner",
    },
    goto_previous_start = {
        ["[m"] = "@function.outer",
        ["[["] = "@class.outer",
        ["[a"] = "@parameter.inner",
    },
}
```
이렇게 설정해 두면 코드 탐색과 수정이 이전과는 비교할 수 없을 정도로 빨라집니다.
