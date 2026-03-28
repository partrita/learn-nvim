# 자동 완성 및 스니펫 엔진
LunarVim이나 AstroNvim 같은 사전 설정을 사용 중이라면, 이 기능들이 이미 최적화되어 있으므로 건너뛰셔도 좋습니다. 하지만 직접 설정을 꾸리고 싶다면 이 챕터를 꼭 확인해 보세요.

---

## 자동 완성 엔진 (Completion Engine)
Neovim은 기본적인 자동 완성 기능을 제공하지만, 현대적인 IDE처럼 퍼지 검색과 매끄러운 팝업 메뉴를 쓰려면 전용 엔진이 필요합니다. 현재 가장 널리 쓰이는 표준은 [nvim-cmp](https://github.com/hrsh7th/nvim-cmp)입니다.

### 데이터 소스 (Sources)
nvim-cmp는 독특한 구조를 가지고 있습니다. 엔진 자체는 빈 껍데기에 가깝고, 어디서 데이터를 가져올지 결정하는 '소스(Source)' 플러그인들을 추가해 기능을 확장합니다.

**추천 소스 목록:**
* **lsp**: 언어 서버로부터 자동 완성 후보를 가져옵니다. (필수!)
* **buffer**: 현재 열려 있는 파일 내의 단어들을 추천합니다.
* **path**: 파일 경로를 입력할 때 유용합니다.
* **cmp-git**: 커밋 해시나 GitHub 이슈 등을 자동 완성해 줍니다.
* **copilot-cmp**: GitHub Copilot의 제안을 자동 완성 목록에 포함합니다.

### 설정 커스터마이징
팝업 메뉴의 디자인부터 단축키 바인딩까지 거의 모든 요소를 취향껏 바꿀 수 있습니다. 처음에는 기본 설정을 유지하다가, 손에 익으면 조금씩 수정해 나가는 걸 추천합니다.

---

## 스니펫 엔진 (Snippet Engine)
스니펫 엔진은 `for` 같은 짧은 키워드를 반복되는 코드 덩어리로 바꿔주는 도구입니다. 크게 두 가지 역할을 수행합니다.
1. 스니펫 템플릿을 실제 코드로 확장합니다.
2. 확장된 코드 사이를 탭(Tab) 키 등으로 오가며 내용을 채울 수 있게 합니다.

추천하는 스니펫 엔진은 [nvim-snippy](https://github.com/dcampos/nvim-snippy)나 [LuaSnip](https://github.com/L3MON4D3/LuaSnip)입니다. 

**주의**: 스니펫을 쓰려면 스니펫 그 자체인 '데이터 셋'도 함께 설치해야 합니다. [vim-snippets](https://github.com/honza/vim-snippets)이나 [friendly-snippets](https://github.com/rafamadriz/friendly-snippets)가 가장 유명합니다.

---

더 구체적인 구현 예시는 저의 [개인 설정 코드](https://github.com/ofirgall/dotfiles/blob/master/editors/nvim/lua/plugins/autocomplete.lua)를 참고해 보세요.
