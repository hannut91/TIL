# 실전 SPA 상태관리 톺아보기

## SPA

* Single page application
* 새로 로드하는 대신에 현재 페이지를 다시 작성하여 사용자와 상호작용 합니다.
* 예: 페이스북

### View Library

* Angular
  * Framework입니다.
  * Change detection을 사용합니다.
* React
  * Virtual DOM을 사용합니다.
  * TypeScript를 완벽하게 지원합니다.
  * Vue보다 배우기 어렵습니다.
* Vue
  * Virtual DOM을 사용합니다.

### State Management

* Angular
  * 내장
* React
  * Redux
* Vue
  * Vuex

#### Redux

* SPA를 위한 예층 가능한 상태 컨테이너 입니다.
* 테스트하기 쉽습니다.
* 시간여행 디버깅이 가능합니다.
* State를 관리하기 위한 거대한 이벤트 루프
* Store의 State를 특정 컴포넌트에 주입합니다.

##### Architecture

* 액션
* 리듀서
* 스토어

##### 미들웨어들

* redux-thunk
  * 배우기 쉽지만 나쁜 소스코드를 만들기가 쉽습니다.
  * 테스트하기가 어렵습니다.
* redux-saga
  * side efeect를 사용한 Data orchestration 미들웨어
  * 중앙에서 액션을 watch하여 side effect를 발생시켜 데이터 제어를 시작합니다.
  * 배우기 어렵습니다.
  * 테스트하기 좋습니다.
  * 비동기 코드를 동기 코드처럼 작성할 수 있습니다.
  * ES6 Generator를 사용하여 동작을 제어합니다.
    * ES6에 추가된 coroutine
* redux-observable

#### MobX

* 일과성 없는 상태를 만들 수 없도록 상태 관리를 간단한게 만들었습니다.
* Functional reactive programming
* 어플리케이션을 MobX는 애플리케이션을 스프레드시트로 간주합니다.

