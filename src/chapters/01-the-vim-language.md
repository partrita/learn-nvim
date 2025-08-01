# Vim 언어

## 버퍼, 분할/창 및 탭
* **버퍼 (Buffers)** - `버퍼`는 열려 있는 파일이며, 여러 `분할`에서 편집할 수 있습니다.
* **분할/창 (Splits/Windows)** - `분할` 또는 `창`은 이동할 수 있는 창 영역입니다.
* **탭 (Tabs)** - `탭`은 `분할`의 집합으로, `터미널`의 `탭`과 유사하지만, 사람들은 그다지 자주 사용하지 않습니다.

##### 바인딩
* `:e <파일>` - 새 파일(버퍼)을 엽니다.
* `:b <버퍼>` - 이미 열려 있는 파일(버퍼)로 전환합니다.
* `:vsplit` - 수직 분할을 엽니다.
* `:split` - 수평 분할을 엽니다.
* 탭에 대해 더 자세히 알아보려면 `:help tab-page`를 사용하세요 (탭은 그다지 필요하지 않습니다).

## 키 바인딩 (Keybinds)
종종 `ggyG`와 같이 설명되는 키 바인딩을 보게 될 것입니다. 이는 전체 `버퍼`를 복사합니다.
키 바인딩의 모든 기호는 `타이핑`하는 것처럼 누르도록 되어 있습니다.
이 바인딩을 실행하려면 다음을 눌러야 합니다:
* `gg` - 파일의 맨 위로 이동
* `y` - 복사 시작
* `shift+g` - 커서부터 파일 끝까지 복사 종료

Vim에서는 키 시퀀스를 완성하기 위해 키를 누르고 있지 않아도 되며, 키 입력 사이의 대기 시간을 늘리거나 줄이도록 `timeoutlen`을 설정할 수 있습니다.

### 키 바인딩 명명 규칙
키 바인딩을 외울 필요는 없습니다. 각 글자가 해당 동작을 나타내기 때문입니다.
* `y` - yank (끌어오기, 복사)
* `p` - paste (붙여넣기)

이 가이드에서 동작을 소개할 때마다, 해당 바인딩을 기억하는 데 사용하는 글자를 표시할 것입니다.

#### 특수 키
* `<cmd>` - 명령을 시작하는 `:`입니다.
* `<cr>` - `enter`입니다.
* `<Esc>` - `Escape`입니다.
* `<C-x>` - Ctrl+x입니다.
* `<M-x>` - alt+x입니다.
* `<M-X>` - alt+shift+x입니다.
* `<A-x>` - alt+x입니다.
* `<A-X>` - alt+shift+x입니다.
* `<leader>` - 리더 키입니다.

`:help <키>`를 입력하여 해당 키에 대한 `도움말` `분할`을 열 수 있습니다. 키는 `G`일 수도 있고 `<cr>`일 수도 있습니다.

###### 리더 (Leader)
Vim은 기본적으로 대부분의 키보드를 매핑합니다. `<leader>`는 사용자 지정 바인딩의 접두사 역할을 합니다.
리더는 다시 매핑할 수 있으며, 기본 매핑은 `,`이지만 대부분의 Vim 사용자는 `<Space>`로 변경합니다.

## 도움말 (Help)
모든 것에 대한 도움말 페이지가 있습니다. 가능한 한 빨리 사용하기 시작하세요. `man`과 비슷하지만 `vim`에 더 적합하고 좋습니다.

## 모드 (Modes)
Vim에는 많은 모드가 있으며, 중요한 모드들을 다룰 것입니다.
각 모드에서 일반 모드로 돌아가려면 `Escape`를 누르세요. 이를 `capslock`으로 다시 매핑하는 것을 추천합니다. 이 키를 많이 누르게 될 것이고, 손을 움직이지 않고 새끼손가락을 사용하는 것이 훨씬 쉬울 것입니다.

* 일반 (Normal) - 보통 이 모드에 있게 되며, 이 모드에서 이동, 복사 등 많은 작업을 할 수 있습니다.
* 입력 (Insert) (`i`) - 버퍼에 텍스트를 입력합니다. 실제로 텍스트를 입력할 때만 이 모드에 있어야 하며, 이 모드에서 이동하고 싶지는 않을 것입니다.
* 비주얼 (Visual) (`v`) - 텍스트를 선택하고 복사/교체합니다.
* 비주얼 라인 (Visual Line) (`V`) - 줄 단위로 텍스트를 선택하고 복사/교체합니다.
* 명령 (Command) (`:`,`/`) - 명령을 입력합니다.

### Capslock을 Escape로 매핑하는 방법
* GNOME (Ubuntu) - `gnome-tweak-tool`을 설치하고, `Tweaks`를 시작한 다음 `Keyboard & Mouse -> Additional Layout Options -> Caps Lock behavior`로 이동합니다.
* [macOS](https://vim.fandom.com/wiki/Map_caps_lock_to_escape_in_macOS)
* Windows - [AutoHotKey](https://www.autohotkey.com/)를 설치하고 `ahk` 스크립트에 `Capslock::Esc`를 추가합니다.
