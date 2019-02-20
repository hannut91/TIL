# Hyperledger Fabric getting started

하이퍼렛저 페브릭 시작하기

## Introduction

* 하이퍼렛저 페브릭이 어떻게 동작하는지 간단히 알아보기 위해 sample프로그램을
  실행시켜봅시다.

## Prerequisites

* 이 예제를 실행하기 위해서는 다음과 같은 것들이 필요합니다.

* cURL
* Docker and Docker Compose
* Golang 1.11.x
* Node.js and NPM 8.9.x
* Python 2.7

## 1. Download the sample

* 코드를 clone한 후 스크립트를 이용하여 필요한 Docker이미지들과 바이너리들을
  다운로드 받습니다.
* 만약 다른버전의 하이퍼렛저 페브릭으로 시작하고싶은 경우 클론받을 때 태그를
  이용하여 버전을 변경하여야 합니다.

```bash
git clone https://github.com/hyperledger/fabric-samples
cd fabric-samples
./scripts/bootstrap.sh
```

* 스크립트를 실행하면 자동으로 필요한 바이너리를 설치하고 Docker이미지들을
  다운로드 받습니다.

## 2. Launch the network

```bash
# /fabcar
./startFabric.sh javascript
```

* peers, orderers, certificate authorities를 포함하는 블럭체인 네트워크를
  실행합니다.
* 서버를 실행하면서 자바스크립트 버전의 `FabCar`스마트 컨트랙트도 같이
  설치가 되고 인스턴스화됩니다.

## 3. Install the application

```bash
# /fabcar/javascript
npm install
```

* 어플리케이션에 필요한 dependencies를 설치합니다.

## 4. Enrolling the admin user

```bash
node enrollAdmin.js
```

* 네트워크를 만들었을 때 `admin`이 생성됩니다.
* 이 `admin`은 certificate authority(CA)에 접근할 수 있는 `registrar`입니다.
* 먼저 private key, public key, 그리고 X.509 certificate를 스크립트를 통해
  만듭니다.
* 이 과정은 `Certificate Signing Request(CSR)`을 사용하는데 private key와
  public key가 local에서 생성되고 `CA`로 public key가 전송됩니다. 그러면 인코딩
  된 certificate를 받습니다. 3개의 credential들은 월렛에 저장되고 관리자로서
  권한을 가지게 됩니다.

## 5. Register and enroll user1

```bash
node registerUser.js
```

* admin을 등록한 것과 마찬가지로 `user1`이라는 사용자를 만들어서 wallet에
  저장합니다.

## 6. Querying the ledger

```bash
$ node query.js
Wallet path: /Users/yunseok/Development/study/fabric/fabric-samples/fabcar/javascript/wallet
Transaction has been evaluated, result is: "[{\"Key\":\"CAR0\",\"Record\":{\"color\":\"blue\",\"docType\":\"car\",\"make\":\"Toyota\",\"model\":\"Prius\",\"owner\":\"Tomoko\"}},{\"Key\":\"CAR1\",\"Record\":{\"color\":\"red\",\"docType\":\"car\",\"make\":\"Ford\",\"model\":\"Mustang\",\"owner\":\"Brad\"}},{\"Key\":\"CAR2\",\"Record\":{\"color\":\"green\",\"docType\":\"car\",\"make\":\"Hyundai\",\"model\":\"Tucson\",\"owner\":\"Jin Soo\"}},{\"Key\":\"CAR3\",\"Record\":{\"color\":\"yellow\",\"docType\":\"car\",\"make\":\"Volkswagen\",\"model\":\"Passat\",\"owner\":\"Max\"}},{\"Key\":\"CAR4\",\"Record\":{\"color\":\"black\",\"docType\":\"car\",\"make\":\"Tesla\",\"model\":\"S\",\"owner\":\"Adriana\"}},{\"Key\":\"CAR5\",\"Record\":{\"color\":\"purple\",\"docType\":\"car\",\"make\":\"Peugeot\",\"model\":\"205\",\"owner\":\"Michel\"}},{\"Key\":\"CAR6\",\"Record\":{\"color\":\"white\",\"docType\":\"car\",\"make\":\"Chery\",\"model\":\"S22L\",\"owner\":\"Aarav\"}},{\"Key\":\"CAR7\",\"Record\":{\"color\":\"violet\",\"docType\":\"car\",\"make\":\"Fiat\",\"model\":\"Punto\",\"owner\":\"Pari\"}},{\"Key\":\"CAR8\",\"Record\":{\"color\":\"indigo\",\"docType\":\"car\",\"make\":\"Tata\",\"model\":\"Nano\",\"owner\":\"Valeria\"}},{\"Key\":\"CAR9\",\"Record\":{\"color\":\"brown\",\"docType\":\"car\",\"make\":\"Holden\",\"model\":\"Barina\",\"owner\":\"Shotaro\"}}]"
```

* 블럭체인 네트워크 호스트들에서 각 피어는 원장의 복사본을 가지고 있습니다.
* 어플리케이션은 스마트컨트랙트를 실행하도록 요청하여 query를 실행합니다.

## 7. Updating the ledger

```bash
$ node invoke.js
Wallet path: /Users/yunseok/Development/study/fabric/fabric-samples/fabcar/javascript/wallet
2019-02-20T04:46:42.563Z - info: [TransactionEventHandler]: _strategySuccess: strategy success for transaction "67384838d98b6d5953e0268ee16964d8f02751df28eea847deb449d91982a156"
Transaction has been submitted
```

```bash
$ node query.js
```

* 다시 쿼리를 통해 확인해보면 `CAR12`가 추가된 것을 확인할 수 있습니다.

## Sources

* <https://hyperledger-fabric.readthedocs.io/en/release-1.4/write_first_app.html>
