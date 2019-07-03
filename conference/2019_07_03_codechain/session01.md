# CodeChain Mainnet Updates and Roadmap

## Mainnet Updates

## CodeChain 1.0 

* 노드의 개수는 30
* PoS
* 4개의 데이터 센터

### CodeChain 2.0

### Staking

* Tendermint(Delegated PoS)를 사용합니다.
* Valiator는 staking code을 통해 수수료를 받을 수 있고 검증할 수 있습니다.
* Staking하려면 nomination트랜잭션을 발생시키면 됩니다.
* 1시간 마다 30명의 후보자를 뽑습니다.

### Reward

* 트랜잭션 수수료를 재산에 따라 분배받습니다.
* 보상을 받기까지 1시간 delay가 있습니다.

### Punishment

* double-signing은 report한 사람에게 보상을 주고 deposit은 slash합니다.
* 노드가 비활성화 되거나 했을 때는 보상을 삭감하는 방식으로 처벌을 합니다.

### Jail

* 문제가 생긴 노드는 망에서 분리시킵니다. 24시간동안 망에 참여할 수 없습니다.

### CommonParams

* stakeholder의 절반 이상이 동의를 하면 주요 상수를 변경할 수 있습니다.

## RoadMap

### Builder SDK & Interchain

* 인프라를 활용하지만 private하게 이용할 수 있도록 SDK를 제공 할 예정입니다.
* SDK Language Support

### Snapshot Sync

* Block sync가 느려서 성능을 향상시킬려고 합니다.

### State Pruning

* 용량이 계속 증가하고 있습니다.

### VM X

* Inspired by Chain's TxVM
