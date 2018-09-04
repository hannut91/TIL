# Klaytn
Service-Oriented Enterprise-Grade Plubic Blockchain Platform

## Blockchain basics
### Blockchain
* Distributed Ledger Technology
* Distributed Consensus Mechanism
* Distributed Network
* Smart Contract & Dapp
* Token economy Model
* Decentralized Governance Model
  * Service의 주인이 없는 모델
+ Incentive Model

### Hash Pointer
데이터의 위치를 지정하는 것
=> 데이터의 무결성을 확인할 수 있음

Block의 Pointer를 Hash Pointer를 사용

### Block structure of Bitcoin

### Merkle Root
Binary tree with hash pointers
데이터의 양을 줄일 수 있음

### Merkle Proof
Verifying a Transaction in a Merkle tree

### P2P Network of Bitcoin
#### Full node
모든 데이터를 가지고 있는 노드
현재 약 10,000개 정도의 노드들이 동작하고 있음

### Bitcoin Consensus Algorithm
#### PoW
맞는 해쉬값을 찾는 것

* GroundX는 BFT를 사용하고 있음

### Ethereum
#### SmartContract
특정 코드를 실행할 때 가스를 소비하기 때문에 코드를 효율적으로 작성해야함
** 트래픽에 따라 가스비가 다르다?

## Blockchain scalabilty issue
비트코인과 이더리움은 처리할 수 있는 속도가 많이 느리다.
** 페이스북이 처리하는 데이터와 비트코인이 처리하는 데이터의 가치는 다르지 않나요?

## Scaling Solutions: On-Chain vs Off-Chain
### On-Chain
이더리룸의 속도를 높이는 방법 예를들면 샤딩
Intershard communication 문제를 어떻게 풀지가 문제다

### Off-Chain
#### State Channel
#### Plasma Sidechain

## Klaytn
플랫폼의 주인이 서비스를 돌리는 provider가 되어야 한다
1. Lack of Finality
2. Poor Performance
3. Uncertain Operation Costs
4. Absence of Enterprise Considerations
5. Inconvenient UX
합의는 Private, public aduiting

### Hybrid Architecture of Trust Model
믿을 만한 회사들이 노드들이 돌리게 할 것임
합의를 private에서 하기 떄문에 빠르게 할 수 있음

### Ranger Node & Open Validation
Write는 합의노드들, Read는 Ranger노드들

### Proof of Partifipation
Read에 대한 보상방법

#### Proof of Replication
Ensuring a RN stores the whole blocks

#### Proof of Serving Clients
Ensuring a RN serves read requests of clients

### Servicechain
속도향상의 한계가 있기 때문에 병렬적인 확장이 필요함
