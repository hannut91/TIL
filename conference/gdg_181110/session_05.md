# Chrominm과 Blink는 어떻게 동작하는가?

* 크롬브라우저의 오픈소스

## 내부를 알면 뭐가 좋을까요?

* 웹 표준 개발에 참여할 수 있습니다.
* 프론트엔드 개발시 성능 향상에 도움이 될 수 있습니다.
* 브라우저 및 웹 플랫폼 개발에 참여할 수 있습니다.

## Process vs Thread

* Process는 메모리 공간이 독립적입니다.
* Thread는 메모리 공간을 공유합니다.

## Multi-process Architecture

* Crash가 발생해도 죽지 않습니다.
* Site Isolation(OOPIF)
  * Iframe끼리의 메모리가 공유되지 않습니다.
* Renderer는 웹 컨텐츠를 담당합니다.
* Browser는 외부와 소통(예: 시스템 콜)을 합니다.

## Blink Rendering

* Parsing
* Style
* Layout
* Layerization
* Paint

### Parsing

* HTML을 파싱하여 DOM Tree를 만듭니다.

### Style

* HTML을 파싱하는 동안 StyleSheetContents를 만듭니다.
* Style Update는 DOM Tree가 만들어진 후에 동작합니다.

### Layout

* 실제로 화면에 표시 될 Object를 결정합니다.
* 어떤 위치에 어떤 사이즈로 배치를 할 지 결정합니다.

### Layerization

* paint과정에서 DOM Order로 그리는 것이 아니라 stacking order순서로 그리게
  됩니다. 
* 여기에 쓰이는 것을 만드는 역할을 합니다.
* 예) z-index가 설정될 경우 

### Paint

* Layer Tree까지 생성되면 그림을 그릴 수 있습니다.

## Off main-thread rendering

* 위의 작업들은 Main-thread에서 동작합니다.

### V-Sync Timeline

* 일반적인 모니터의 주사율은 60Hz입니다.
* 1초를 60으로 나누어서 16.7ms마다 돌아옵니다.
* 이 간격안에 그리는 작업이 끝나야 부드러운 애니메이션을 만들 수 있습니다.

## Frame Drop없이 웹페이지를 그리려면 

* 그림그리는 것을 미루자
* 그려야하는 작업들을 다른 쓰레드에게 위임합니다.

## Rendering 용어 정리

* Painting Rendering과정 전체, 좁은의미로 Recording
* Recording Blink 관점에서 Painting, 그림 그리는 연산을 기록하는 행위
* Rasterization Pixel Buffer에 그림을 실제로 그리는 행위
* Compositiong 여러장의 그림을 합성하는 행위
* Drawing 그림을 사용자가 볼 수 있는 화면에 출력하는 행위

## GPU가속

* OpenGL을 사용합니다.
* 각종 변환을 빠르게 할 수 있습니다.
* 텍스쳐를 빠르게 합성할 수 있습니다.

### GPU Composition

* 이미지를 GPU 메모리에 Cache했다가 Compositing하는 것
* GPU메모리에 Texture가 Upload되면 합성하거나 처리하는것은 굉장히 빠르다.
* width를 변경하면
  * Layout, Paint, Composite모두 발생
* 하지만 Transform을 사용하면
  * Composite만 발생합니다.

## Source

* https://csstriggers.com 에서 css속성들이 어떤 작업을 유발시키는지 확인할 수
  있습니다.
