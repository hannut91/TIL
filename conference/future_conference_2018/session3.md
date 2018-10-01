# 스마트 컨트랙트

분산화된 컴퓨터 플랫폼을 이더리움을 통해 구현하였음
한번 배포된 스마트컨트랙트는 변경될 수 없음

## Use case
* ICO
* Game(CryptoKitties)
* Exchange
 * 입금하는데 사용됨
* Gamble
* Multisig Wallet

## 해킹사건
DAO 해킹사건
* 스마트 컨트랙트 External call의 entrancy공격을 이용
* Partity재단 Multisig Wallet 동결
* SmartMesh ERC20 해킹

1. 해킹 트랜잭션 발생 상황 분석
2. 해킹에 필요한 배경지식 이해
 * Integer Overflow
3. 해킹 시나리오 분석
4. 해결방법 및 예빵책 제시

## Partity Multisig Wallet Freeze 사건
* Multisig Wallet
하나의 키가 아닌 여러개의 키를 이용해서 사인해야지 트랜잭션이 발생하는 지갑

EIP(Ethereum Imporvement Proposal) 999
## EIP란?
이더리움에게 기능들을 제안하는것

## Block Gas Limit
하나의 블록에서는 일정량 GAS제한을 넘게 처리할 수 없다.

ICO를 하게 되면 이더를 받고 토큰을 분배하게 됩니다.
토큰의 분배를 할때 너무 많은 투자자들을 포함하여 가스 제한을 넘어서 분배가 안되었던 사례가 있습니다.
## 제안사항
* Favor Pull over Push
투자자에게 토큰을 자등으로 전송하는 것보다 직접 토큰을 출금하게 만들 수 있음 함수 하나에서 transfer 함수 한 개를 호출함
대부분의 투자자들이 할 줄 모르므로 실제 실행하기에는 어려움이 있다.
* 가스 예상 사용량을 잘 계산하여 스마트 컨트랙트를 작성해야한다.
## Access Control
### Modifier
함수의 동작을 간단하게 변경하기 위해 사용된다. 예를들어 함수의 실행 전에 간단하게 조건을 체크하기 위해 사용된다.

## 안전한 스마트 컨트랙트 개발 방법
1. Dynamic Program Analysis
 * Unit Testing
   스마트 컨트랙트의 개별적인 코드 단위가 올바르게 동작하는지 확인하는 테스트 코드를 작성하는 것 
   Coverage를 100%에 맞춰 테스트되지 않은것이 있는지 확인해야합니다.
   TDD를 해야합니다.
2. Static/Symbolic Analysis

Gas Optimization

