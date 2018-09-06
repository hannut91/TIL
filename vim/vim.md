# Vim

### 붙여넣기
p: 라인에 붙여넣기
P: 윗 라인에 붙여넣기

### 복사하기
y: 복사하기
yy, Y: 한줄복사하기

### 잘라내기
d: 삭제하기 => 문법 d대상 
dd: 한줄 잘라내기
D: 맨 끝라인 까지 잘라내기

u: UnDo
ctrl-r: ReDo

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

### Find
/text
* d/text 현재커서에서 검색된곳까지 지우기
?text 역방향 검색
n: Next
N: Previous

:w 저장
:wq 저장하고 닫기
:q, ZZ 종료하기
:cq, :q! 강제 종료

### File 다시 불러오기
:so %

### 이동하기
h,j,k,l: 왼쪽, 위, 아래, 오른쪽
^: 현재 라인의 첫번째 글자로 점프 
$: 현재 라인의 마지막으로 점프
0: 현재 라인의 가장 첫 번째 칼럼으로 점프
w: 다음 워드로 이동
b: 이전 워드로 이동
f<a-z>: 오른쪽으로 검색 fb: 가장 가까운 b로 점프
  ;: 다음으로 점프
  ,: 이전으로 점프
t<a-z> 오른쪽으로 검색하지만 커서는 하나 전으로 점프
F<a-z>: 왼쪽으로 검색 
숫자f: 숫자만큼 반복해서 검색

### Visual mode
v: 비주얼모드
V: 라인 비쥬얼모드
ctrl-v: 블럭 모드
선택하는 중에 o를 누르면 시작점과 끝점으로 이동할 수 있음

### 페이지 이동
ctrl-f: Page down
ctrl-b: Page up
zz: 현재 커서가 있는 라인을 화면의 가운데로 스크롤
ctrl-e: Scroll down
ctrl-y: Scroll up
3gg, 3G: Move to line
gg: Move to first line
G: Move to last line
:3: Move to line
H: Move to first line on screen
L: Move to last line on screen
M: Move to center line on screen
g; 이전에 편집한 곳으로 이동하기
g, 다음에 편집한 곳으로 이동하기

### Mark
m<a-z>: 마킹

### 화면
:vs 화면 세로로 분할하기 
:split 화면 가로로 분할하기
