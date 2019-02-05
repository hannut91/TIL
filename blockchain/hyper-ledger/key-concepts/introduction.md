# Hyperledger Fabric 소개

하이퍼렛저 페블릭에대한 기초지식

## Introduction

* 모듈러 구조를 가지고 있어 컴포넌트들을 교체 교체 가능할 수 있도록
  설계된 분산 원장 솔루션 플랫폽입니다.

## What is a Blockchain?

### A Distributed Ledger

* 블록 체인 네트워크에서 발생하는 모든 트랜잭션은 분산 원장으로 기록됩니다.
* 분산 원장은 네트워크 참여자에 의해 복사되어 저장돼 탈중앙화하게 됩니다.

![](https://hyperledger-fabric.readthedocs.io/en/latest/_images/basic_network.png)

* 암호화방식을 이용해서 블럭체인에 저장되는 정보들은 추가만 할 수 있는 형태가
  되어 트랜잭션이 한 번 원장에 더해지면 수정이 불가합니다.
* 이 속성은 우리는 `immutability`라고 부릅니다.

### Smart Contracts

* 스마트 컨트랙트로 원장에대해 제어된 접근을 허용하여 정보의 일관된 업데이트를
  지원합니다. 또한 참여자들에게 특정한 트랜잭션들을 자동으로 실행하도록 하기
  위해서 필요합니다.

![](https://hyperledger-fabric.readthedocs.io/en/latest/_images/Smart_Contract.png)

* 예를 들어, 스마트 컨트랙트는 물품이 도착하는 속도에 따라 운송료가 변동하는 품목
  운송 비용을 규정하도록 작성 될 수 있습니다. 양 당사자가 동의하고 원장에게
  서면으로 합의 된 조건에 따라, 해당 금액은 물품을 수령하면 자동으로
  변경됩니다.

### Consensus

* 원장 트랜잭션들을 네트워크끼리 동기화 유지하는 과정
* 적절한 참가자들에 의해 승인된 트랜잭션들로만 업데이트될 수 있고 같은
  트랜잭션들을 같은 순서대로 업데이트 합니다.

![](https://hyperledger-fabric.readthedocs.io/en/latest/_images/consensus.png)

* 블록체인이 스마트 컨트랙트를 통해 업데이트 되고 합의라는 과정을 통해
  지속적으로 동기화 된 공유 복제 트랜잭션 시스템이라고 생각하면 됩니다.

## Why is Blockchain useful?

### Today's Systems of Record

![](https://hyperledger-fabric.readthedocs.io/en/latest/_images/current_network.png)

* 비즈니스 네트워크의 구성원은 서로 거래하지만 거래에 대한 별도의 기록을
  유지합니다. 그리고 자신의 소유권을 증명하기 위해 그 출처를 설정해야 합니다.
* 네트워크 참여자의 신원을 관리하기 위한 통합 시스템이 존재하지 않으며, 출처를
  확립하는 것이 매우 힘들어서 증권 거래를 정리하는 데 많은 시간이 걸리며
  수동으로 계약서에 서명하고 실행해야하며 시스템의 모든 데이터 베이스는 고유한
  정보를 포함하므로 단일 실패 지점을 나타냅니다.
* 가시성과 신뢰의 필요성이 분명하더라도 비즈니스 네트워크에 걸친 기록 시스템을
  구축 하기 위해 정보 및 프로세스 공유에 대한 오늘날의 분열 된 접근법으로는
  불가능합니다.

### The Blockchain Difference

* 비즈니스 네트워크가 네트워크에서 ID를 설정하고, 트랜잭션을 실행하고, 데이터를
  저장하는 표준방법을 갖고 있다면 어떨까요?
* 일단 작성되면 변경이 불가능하고 신뢰할 수 있는 거래 목록을 살펴봄으로써
  자산의 출처를 결정할 수 있다면 어떨까요?

![](https://hyperledger-fabric.readthedocs.io/en/latest/_images/future_net.png)

* 위의 그림은 블럭체인네트워크를 나타냅니다. 모든 참가자가 자신만의 복사된
  분장을 가지고 있습니다.
* 오늘날의 시스템들과는 다르게 블럭체인시스템은 공유된 원장을 업데이트하는
  공유된 프로그램을 가지고 있어 분장 뿐만아니라 분장을 업데이트하는 과정 또한
  복사됩니다.
* 블록 대장 네트워크는 공유 원장을 통해 비즈니스 네트워크를 조정할 수 있으므로
  개인 정보 및 처리와 관련된 시간, 비용 및 위험을 줄이면서 신뢰와 가시성을
  향상시킬 수 있습니다.

## What is Hyperledger Fabric?

* Hyperledger에 있는 블럭체인 프로젝트중 하나 입니다.
* 다른 블럭체인 기술들과 같이 원장을 가지고 있고, 스마트 컨트랙트를 사용하며 각
  참가자들에 의해 트랜젹선들이 관리됩니다.
* 다른 블럭체인 시스템과 다른점은 `private`이고 `permissioned`라는 것입니다.
  아무나 참여할 수 있는 public블럭체인과 달리 하이퍼렛저 페브릭은 
  `Membership Service Provider(MSP)`에 의해 멤버들이 관리가 됩니다.
* 하이퍼렛저 페브릭은 교체가능한 옵션들을 가지고있어서 데이터를 다양한 포맷으로
  저장할 수 있고 합의방법을 변경할 수 있으며 다른 `MSP`들이 지원됩니다.
* 하이퍼렛저 페브릭은 채널을 만들 수 있어서 참가자들을 그룹으로 묶어 별도의
  트랜잭션들의 원장을 만들 수 있습니다.

### Shared Ledger

* 하이퍼렛저 페브릭 원장은 `world state`와 `transaction log`의 조합으로
  이루어져 있습니다.
* `world state`는 원장의 상태를 나타낸다.
* `transaction log`는 `world state`를 만들어낸 업데이트 기록으로 모든
  트랜잭션을 나타냅니다.

### Smart Contracts

* 하이퍼렛저 페브릭 스마트 컨트랜트들은 `chaincode`에 작정됩니다. 그리고
  블럭체인 외부의 어플리케이션이 원장과 교류할 때 실행됩니다.
* 일반적으로 chaincode는 원장의 데이터베스, world state와 교류하고 transaction
  log와는 교류하지 않습니다.
* 다양한 언어로 chaincode를 작성할 수 있는데 현재는 `Go`와 `Node`만 지원합니다.

### Privacy

* 네트워크의 필요에 따라 B2B 네트워크 참여자는 공유하는 정보의 양에 대해 매우 
  민감합니다.
* Hyperledger 패브릭은 개인 정보 (채널 사용)가 주요 운영 요구 사항 일뿐만 
  아니라 비교적 개방 된 네트워크를 지원합니다.

### Consensus

* 트랜잭션들은 만드시 순서대로 원장에 쓰여져야합니다.
* 거래 순서를 설정해야하고 원장에 실수로 혹은 악의적으로 삽입된 불량 거래를
  거부하는 방법을 마련해야 합니다.
* 하이퍼렛저 패브릭은 합의방법을 선택할 수 있도록 설계되어 있습니다.

## Sources

* <https://hyperledger-fabric.readthedocs.io/en/latest/functionalities.html>
