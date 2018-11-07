# elastic beanstalk

## version update 방법

* all at once
  * 한번에 업데이트
  * 업데이트하는 동안 `Downtime`이 발생함
* roliing
  * 한개 씩 업데이트
  * 단 업데이트하는중에 사용자가 v1과 v2를 따로 보는 문제가 생길 수 있음
* roling with additional batch
  * 현재 인스턴스가 4개라면 가용성을 포기하지않고 업데이트하는 방법
* immutable
* Blue/Green
  * `Downtime`이 없다.
  * 롤백이 굉장히 편하다.
  * 단점
    * 새로운 환경으로 인해 상대적으로 느리다.


