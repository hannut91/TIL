# Vim에서 한글 입력

Vim insert모드에서 한글을 입력한 후 normal모드로 변경하였을 때 한글 키 이기 때문
에 영문입력으로 변경한 후 사용해야 합니다. 이게 번거롭기 때문에 normal모드로 변경
하였을 때 영문입력으로 변경하고 다시 insert모드로 돌아왔을 때 이전의 입력소스로
계속 입력할 수 있도록 설정하였습니다.

## 1. Command line input source switcher for mac 설치
```
git clone https://github.com/vovkasm/input-source-switcher.git
cd input-source-switcher
mkdir build && cd build
cmake ..
make
make install
```
## 2. vim-xkbswitch 설치
### VimPlug
.vimrc에 아래내용을 추가한 후 
```
Plug 'lyokha/vim-xkbswitch'
```

아래 커맨드를 실행
```
:PlugInstall
```

.vimrc에 다음 세팅등 추가
```
if has('mac') && filereadable('/usr/local/lib/libInputSourceSwitcher.dylib')
    let g:XkbSwitchEnabled = 1
    let g:XkbSwitchLib = '/usr/local/lib/libInputSourceSwitcher.dylib'
endif
```

## Source
https://github.com/vovkasm/input-source-switcher
https://github.com/lyokha/vim-xkbswitch
