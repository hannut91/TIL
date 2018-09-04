# Vim

### 붙여넣기
p: 라인에 붙여넣기
P: 윗 라인에 붙여넣기

### 복사하기
yy, Y: 한줄복사하기

### 잘라내기
d: 잘라내기
dd: 한줄 잘라내기
D: 맨 끝라인 까지 잘라내기

### 편집하기
shift-j: 아랫줄 현재줄 맨 뒤에 붙이기

### 함수정의로 이동하기
shift-k: 함수정의로 이동하기

### insert모드에서 삭제하기
ctrl-h: 한글자 삭제하기
ctrl-w: 한 단어 삭제하기

### 화면 이동
shift-h: 화면 맨 위로 커서 이동하기
shift-l: 화면 맨 아래로 커서 이동하기

### input모드에서 삭제시 라인넘어서까지 지워지게하기
set bs=2

### Find and replace
#### Current Line
:s/original/result/g

#### All line
:%s/original/result/g

#### Range
:5,12s/original/result/g
