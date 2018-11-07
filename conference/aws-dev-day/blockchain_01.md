# Blockchain on AWS

## 블럭체인 개발시 고려할 사항들

1. 퍼블릭과 프라이빗
2. 합의 알고리즘
3. 처리 성능(TPS)
4. 트랜잭션의 응답시간
5. 처리비용은 얼마나 드는가?(GAS)
6. 직접 구축 vs 서비스를 사용

## 블록체인 트릴레마

* 확장성
* 보안성
* 탈중앙화

3가지를 모두 만족시키는 어렵다.

## 어떤 합의 알고리즙을 사용할 것인가?
* PoA
  * Parity
* PBFT
  * Hyperledger
  * Tendermint
* DPoS
  * EOS
  * Steemit
  * LISK
* PoS
  * CASPER
  * QTUM
  * Wanchain
* PoW
  * Bitcoin
  * Ethereum

* Centralized
  * 블럭 생성 시간 빠름
  * 높은 성능
  * Trust

## 블럭체인 라이프 사이클

* 블럭의 생성
* 블럭의 전파
* 블럭의 검증
* 블록의 확정
* 보상과 패널티

## 이더리움 pow

## 이더리움 PoA(Clique)

* 권하능력을 가진 사람들이 순서대로 돌아가면서 블록 생성
* 확정 시간 빠름
* 보상 없음, 순번이 되지않은 signer에 대한 패널티 있음
* 전파 속도가 빠르고 포크가 발생할 일이 없음
* 참여 노드 누구나 블록 생성장의 서명 검증(별도 검증단 없음)

# Let's build a. rivate Ethereum Network on Kubernetes (K8s)!
