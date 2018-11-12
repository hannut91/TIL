# 빠르다는 것 그 이상 으로 구현하기 힘든 Isomorphic PWA

* 페이지 로딩속도가 사용자 경험에 많은 영향을 줍니다.
* 5초 이내에 (TTI)
* 2초이내에 나머지 로드

## SPA

* 초기구동속도가 느리다.
* JavaScript Bytes는 JPEG Bytes는 값이 같더라도 처리하는 속도는 다르다. 로딩이
  다 된 이후에도 처리하는 로직이 있기 때문입니다.

## PRPL Pattern

* 웹앱을 배포할 떄 UX를 최적화하기 위한 도구
* Push Render Pre-cache Lazy-load

