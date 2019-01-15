# Docker Composer overview

Docker Compose에 대한 기초지식

## Overview

* `Compose`는 여러 컨테이너를 가지고있는 `Docker`앱을 정의하고 동작시키는 도구
  입니다. 
* `Compose`는 어플리케이션 서비스들을 설정하기 위해 YAML파일을 사용합니다.
* 하나의 커맨드로 설정파일로부터 모든 서비스를 생성하고 시작할 수 있습니다.
* `Compose`는 production, staging, development, testing, CI workflows등 모든
  환경에서 동작합니다.
* `Compose`를 사용하는것은 기본적으로 3단계 입니다.
  1. 다른곳에서 재사용될 수 있도록 `Dockerfile`로 앱의 환경을 정의합니다.
  2.  격리된 환경에서 같이 실행될 수 있도록 `docker-compose.yml`에서 만들 
    서비스들을 정의해줍니다.
  3. `docker-compose up`을 실행하면 `Compose`가 시작하고 전체 앱을 실행합니다.
* `Compose`는 앱 라이프사이클을 관리하는 커맨드들을 가지고 있습니다.
  * 서비스들을 시작하고 중지, 재빌드
  * 동작하는 서비스들의 상태를 볼 수 있음
  * 동작하는 서비스들에대해서 로그를 출력할 수 있음
  * 동작하는 서비스들의 로그 출력을 스트림할 수 있음
  * 서비스에서 일회성 명령을 실행할 수 있음

### docker-compose.yml example

```yml
version: '3'
services:
  web:
    build: .
    ports:
    - "5000:5000"
    volumes:
    - .:/code
    - logvolume01:/var/log
    links:
    - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

## Features

### Multiple isolated environments on a single host

* Compose는 프로젝트 이름을 사용하여 서로 환경을 격리합니다.
* 여러 다른 상황에서이 프로젝트 이름을 사용할 수 있습니다.
  * dev 호스트에서 프로젝트의 각 지형지 물 지점에 대해 안정적인 복사본을
    실행하려는 경우와 같이 단일 환경의 여러 복사본을 만들 수 있습니다.
  * CI서버에서 빌드가 서로 간섭하지 않도록 하려면 이름을 유니크한 빌드 번호로 
    설정할 수 있습니다.
  * 공유된 호스트 혹은 개발 호스트에서 같은 서비스 이름들을 사용하고 있는 다른 
    프로젝트들을 서로 간섭을 방지하기위해 사용할 수 있습니다.
* 기본 프로젝트 이름은 프로젝트 폴더의 기본이름입니다.
* 커맨드라인 옵션으로 `-p`를 이용하여 이름을 정할 수 있습니다.

### Preserve volume data when containers are created

* `Compose`는 서비스들에 의해 사용되는 모든 볼륨들을 유지합니다. 
* `docker-compose up`이 실행되었을 때 만약 이전에 동작시켰던 컨테이너들을
  찾는다면 이전 컨테이너를 새로운 컨테이너로 복사합니다.
* 이 과정을 통해 이전 데이터가 사라지지 않고 유지됩니다.

### Only recreate containers that have changed

* `Compose`는 컨테이너를 만들때 사용된 설정을 캐싱합니다.
* 변경되지 않은 서비스를 재시작할 때 `Compose`는 존재하는 컨테이너들을
  재사용합니다.
* 컨테이너를 재사용함으로써 환경을 빠르게 바꿀 수 있습니다.

## Common use cases

### Development environments

* 소프트웨어를 개발할 때 독립된 환경에서 앱을 실행시키고 상호작용하는 것은
  굉장히 중요한 일입니다.
* `Compose`커맨드 라인 도구로 환경을 만들고 상호작용할 수 있습니다.
* `Compose file`는 어플리케이션의 서비스 의존성들을 설정하고 문서화 하는 기능을
  제공합니다.
* 커맨드라인 도구의 하나의 명령어로 여러개의 컨테이너를 실행할 수 있습니다.
* 이렇게 설정하면 개발자가 프로젝트를 시작할 때 복잡한 시작과정없이 시작할 수
  있습니다.

### Automated testing environments

* `Continuous Deployment`혹은 `Continuous Integration`에서 중요한 부분은
  자동화된 테스트입니다.
* 자동화된 e2e테스트를 위해서는 환경이 필요합니다.
* `Compose`는 테스트를 위한 격리된 테스트 환경을 만드는데 편리한 방법을
  제공합니다.
* `Config file`에서 환경을 정의함으로써 환경을 만들고 삭제할 수 있습니다.

```bash
$ docker-compose up -d
$ ./run_tests
$ docker-compose down
```

### Single host deployments

* Compose는 전통적으로 워크 플로 개발 및 테스트에 중점을 두었지만 각 릴리스마다
  더 많은 생산 지향 기능을 개발하고 있습니다.
* Compose를 사용하여 원격 Docker Engine에 배포 할 수 있습니다.
* Docker Engine은 Docker Machine 또는 전체 Docker Swarm 클러스터로 프로비저닝
  된 단일 인스턴스 일 수 있습니다.

## Sources

* https://docs.docker.com/compose/overview/
