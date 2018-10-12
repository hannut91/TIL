# 네이버에서 사용되는 여러가지 Data Platform, 그리고 MongoDB

## 네이버에서의 Data Platform

단순한 client server구조로 잘 운영이 되었지만 시간이 지남에 따라 더 빠른 속도를
원하기 시작해서 Cache를 사용하게 되었습니다.
RDBMS는 샤딩이안되어 큰 데이터를 다루기 힘들어졌습니다.
서비스 별로 데이터가 다르고 공통된 데이터를 관리하기가 어려워졌습니다.

### Mongodb
* 스키마가 없으며
  사전에 데이터에 대한 구조나 정의를 하지 않아도 됩니다.
  스키마가 없기 때문에 column정보도 같이 저장되어야해서 RDMBS보다 용량이 더
  많이 필요합니다. => 성능상 큰 취약점이 될 수 있습니다.
* 샤딩을 처리
  데이터 사이즈가 증가
* Secondary Index
  HBase는 secondary index를 지원하지 않습니다.
  MongoDB는 Chunk논리적으로 분리합니다.
* Transaction 처리가 가능한
  NoSQL을 사용하면서 Transaction기능을 원하는 경우가 있음.
  4.0부터 replica set에서 Multi-Document Transaction을 지원합니다.
* JSON 지원
  REST API사용이 확대되면서 메시지 포맷을 JSON으로 사용할 경우 Server와 DB데이터
  전송간에 JSON사용이 선호되었습니다.
* IDC DR 
  서비스가 커지고, 중요도가 높아짐에 따라 IDC(Disaster recovery)이중화
  MongoDB는 IDC간 Auto failover가 가능한 Data Platform
  IDC가 꼭 3개가 필요합니다. 한 쪽이 무너졌을 떄 50%가 넘어가면 제대로 fail over
  가 되지 않습니다.
MongoDB를 사용하게 되었습니다.


## 네이버에서 MongoDB를 사용하면서 겪은 에피소드들

### mongos 관리
제조사 권장은 mongos(router)를 client와 같이 배포 권장 => 사용하고 있지 않음.
MongoDB가 Main Data Platform이 아닌 경우 배포/관리의 어려움 때문(&권한 관리)

### L4와 getmore
Sharding 에서의. L4(network switch) 사용을 초기에는 권장했으나 getmore이슈로
제거
getmore는 이전에 요청했던곳에 다시 요청해야 하는데 L4를 사용할 경우 할 수가 없음

### mongos <-> shard 커넥션
Mongos와 shard server사이에 커넥션 관리에 문제가 있음. DB가 커넥션을 맺는것은
부하가 큰 작업이고 쿼리 처리보다 우선시 된다. 너무 많은 커넥션이 생기게 되면
부하가 생겨 장애가 발생할 수 있는데 기본 옵션은 커넥션 수가 unlimited로 되어 
있습니다. 이를 제한을 두어 장애가 발생하지 않도록 수정하여야 합니다.

### Node.js Driver
Node,js 모듈인 mongoose는 성능 이슈로 인해 권장하지 않음

### Storage Engine
WiredTiger 스토리지 엔진만 사용

### Storage Engine - evction problem
3.4이상 버전으로 업데이트를 권장합니다.
eviction memory buffer에서 오래된 데이터를 삭제하는것

### Storage Engine - Checkpoint
### Eviction & Checkpoint

### Background Index
background index 생성 가능
=> DB Lock을 유발시킨다. 컬렉션 뿐만 아니라 데이터베이스에 Lock에 걸린다.
=> 쿼리 응답이 지연될 수 있기 때문에 새벽시간에 진행함

### Compact
디스크 조각모음
작업 중 질의 수행이 안되기 때문에 서브에서 제외하고 진행해야합니다.

### Balancer
MongoDB Chunk Migration은 많은 비옹이 듦

### Clustered Index
해당 key 값 기준으로 실제 데이터가 정렬되어 있음.
MongoDB는 내부적으로 구현되어 있지만 우리가 사용할 순 없다.

### Unique Index
Sharding환경에서 unique index는 전체 shard 내에서 유니크 하지 않음
local기반 index이기 때문

### 개인정보 - 전자금융거래법
MongoDB 3.6버전의 authenticationRestrictions기능 사용중
bind_ip 는 DB ACL을 제한하는 기능이 아님

## MongoDB의 장단점
NoSQL의 특징과 RDBMS의 특징을 고루 가지고 있는 DBMS

### 성능과 안전성
### 전망

