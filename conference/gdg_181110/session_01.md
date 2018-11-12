# Chrome Devetools를 활용한 웹 프론트엔드 성능 측정과 개선

## 성능이란?

* 성능이란 UX이다.
  * 사용자의 경험을 해치지 않아야 합니다.
* 측정할 수 없다는 개선할 수 없습니다.

## 측정
### RAIL
  * Response 입력 지연 시간이 100ms 미만
  * Animation 각 프레임 작업의 완료 시간은 16ms미만
  * Idle
  * Load 페이지가 1000ms 이내에 사용할 준비

#### 아쉬운 점

* 귀찮음
* 이슈를 발견해도 파악이 어려움
* 해결한 후 다시 측정해야합니다.

### Audit

* Lighthouse를 개선한 것
* 크롬 devtool에서 선택할 수 있습니다.

#### Performance

* 그리는데 걸리는 속도를 측정 할 수 있습니다.

#### 접근성

* 어떻게 해결해야하는지 나옵니다.

#### Best practice

#### SEO details

## 개선

* 어떻게 개선할 수 있을까요?
* Request 개수
  * Webpack으로 번들링합니다.
  * Lazy loading을 사용합니다.
* Resource tkdlwm wnfdlrl
  * Webpack
  * Tree-shaking
  * Code-spliting
  * Obfuscation
  * Minify
    * DCE
  * 이미지 최적화
* Rendering 시간 단축
  * CRP 최적화
    * Script tag with async/defer keyword
  * Reflow 최소화
  * 부드러운 애니메이션

### 이미지 최적화

* 이미지에 meta data를 삭제하면 용량을 줄일 수 있습니다.

#### srcset attribute

* 디바이스 픽셀크기에 맞는 이미지 사용
* IE에서는 사용할 수 없습니다.

### 부드러운 애니메이션

#### 하드웨어 가속

* Chrome dev tool에서 layers에서 확인할 수 있습니다.

#### 스크롤 이벤트 튜닝

* 스크롤은 가벼워야 합니다.
* requestAnimationFrame
  * 초당 60회 rendering 하는 디바이스 브라우저에 최적화
  * animationFrame queue를 사용합니다.

* addEventListener에서 옵션으로 passive: false를 같이 넘기면 성능상 이득을 얻을
  수 있습니다.

### 로딩 과정

1. Connection
2. 서버로부터 bytes를 받는 시간

### IntersectionObserver

* 스크롤을 할 때 
* IE에선 지원하지 않으므로 polyfill을 사용해야 합니다.
* 이미지를 layy loading할 때 사용할 수 있습니다.
* custom element를 만들어서 viewport에 보일 떄 이미지 src에 url을 입력합니다.
* base64는 캐싱이 안되기 때문에 주의해서 사용해야 합니다.

## Source

MDN performance api

