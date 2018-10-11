# 브라우저 최적화

## 브라우저는 어떻게 동작하는가?

HTML을 파싱할 떄 중요한 것이 예외처리다. 예외가 발생할 경우 DOM Tree가 달라지고
원하는 결과를 얻을 수 없다.

## JavaScript Engine
다양한 경로로 실행이됩니다. 

## Recalculate Style
Parsing된 CSS결과를 Render Tree에 적용하는 과정
HTML에는 어떻게 렌더링 하라는 정보를 가지고 있지 않고 CSS가 가지고 있음
css 처리 과정은 devtool에서 볼 수 없다.

DOM과 비슷하게 Tree를 사용하는데 상속하는 구조를 사용하귀 쉽기 때문이다.

## Render Tree
DOM Tree를 가지고 CSS를 Look up하여 만드는 것
DOM Tree + CSSOM Tree
화면에 보이는 요소들을 중심으로 구성
HTML HEAD는 사용하지 않음

display: none; 은 Tree에 반영되지 않음

## Layout

CSS 2.1 Box Model
박스의 크기와 위치를 계산하는 과정

window size가 변경되거나 font size가 변경될 경우 layout이 발생함

block은 아래로만 쌓을 수 있고
inline은 옆으로만 쌓을 수 있습니다.

## Paint

## New Version!

* JS
* Recalc Style
  Render Tree
* Layout
* Update Layer Tree(NEW)
  렌더링에 사용될 최종
* Paint
* Composite(NEW)
  레이어들을 합성하여 한장의 bitmap으로 만드는 과정
  Paint는 각 Layer별로 Print를 하며, Tiled Backing Store기법을 사용함
  여러개의 layer를 가지지 않을경우 하나가 바뀌면 다시 그려야함.
  
=> 이 모든 과정이 VSync 주기 안에 모두 완료되어야 합니다.

## VSync Overview
## 브라우저는 하나의 코어밖에 사용할 수 없음.
자료구조들이 Main Thread에서만 동작해야함
1. HTML과 JS는 병렬로 처리할 수 없는 구조입니다.
2. 자료구조가 용량이 커서 복사하여 처리할 수 없습니다.




