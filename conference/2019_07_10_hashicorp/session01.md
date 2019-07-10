# 테라폼으로 글로벌 서비스 구성 - DRY 체험기

어떤 문제를 해결하기 위해 도구를 도입했는가?
DRY가 무엇이지?
=> Don't Repeat yourself

WET(Write Everthing Twice)
처음 작성한 코드들은 중복된 코드들이 많았다. 수정 및 재활용 하는데 많은 비용이
발생했다.

## 요구사항

여러개의 지역과 환경이 있다.
5개국 서비스 구성 시 15개 유사 인프라 구성과 관리를 해야한다.

## 인프라 구성 도구

Infrastructrue Provisioning
=> 테라폼, Terragrunt

Image Management => Packer
Configuration Management => Ansible
CI/CD => Jenkins, AWX

여러개의 인프라를 구성하기 위해 코드로 하기로 했다.

## IaC

인프라 스트럭쳐 as code
인프라의 생산성을 높일 수 있다.
빠르 실행속도를 가질 수 있다.
위험 관리에 좋다.
불확실성에 대한 유연함

## Terraform

HashiCorp에서 만든 오픈소스 도구이며 인프라를 코드 형태로 정의하는 간편한
선언형 프로그래밍 언어
프로바이더가 다양하다.
큰 커뮤니티를 가지고 있다.

**사실 그냥 해 보고 싶었다.**

## Phase 1 - 시작

일단 시작해보자
단순한 리소스를 나열하는 것으로는 15개의 인프라를 만들기 어렵다.
재활용이 불가능하고 비슷한 리소스의 대량 중복 발생
유지보수 불가능

## Phase 2 - Terraform Module

* Data를 변수 처리한 리소스 구성 파일 묶음

비슷한 리소스를 반복 정의 한느 고통에서 벗어날 수 있다.
사용자 정의 모듈 만들어 활용할 수 있다.
외부에서 이미 잘 만들어둔 모듈을 활용
리소스에는 버저닝이 안되지만 모듈에는 버저닝이 가능하다.
=> 모듈관 독립성을 확보하여 의존성을 제거할 수 있다.

## Phase 3 - Terragrunt

* gruntworks.io에서 개발하고 Terraform만으로는 부족한 기능 보완
* 단순한 인프라는 Terraform으로도 충분하지만 인프라 구성이 커질 수록 모듈간의
  연관 관계 및 중복이 발생한다.
* Orchestration = Terragrunt
  * 모듈 간의 코드 중복을 최소화
  * 모듈 간의 종속 관계 제거

Terragrunt up-all 실행시 Dependencies까지 함께 생성됨. 하지만 all로 생선된
모듈을 destroy할 경우 dependency가 있는 것들도 같이 삭제됨.

## Terraform & Terragrunt Structure

* Module Repo
* Service Repo
* Terragrunt Repo

## 고민

* Terraform을 통한 인프라 구성이 빠르지 않다.
  * Terraform 코드 개발 및 검증
  * 러닝커브
  * 손으로 작업 했던 경험
  * 이상과 현실
* Terragrunt도 사용해야 한다.

## 숙제

* 모듈 테스트 및 검증
* 프로덕션 환경 적용 후 리소스 삭제 방지
* tfstate 파일 시각화
  * 보기 굉장히 어렵다.
* Data Security (ssh key)

## 정리

* 상용 수준 인프라를 구성하고 운영하는 것은 매우 어렵다는 것을 인지하자
* (AWS) 기본 디자인을 잘하자
* DRY를 실천하기 위해 노력하자
  * 한 곳에 너무 많은 리소스를 정의 하지 말자
  * 중복을 최소화하고, 최대한 작게 서로 독립적으로 단순하게 구성 하자.
* 팀에서의 강력한 의지가 없다면 하지 말자
* 불확실성에 대한 보다 유연한 대응을 위해 노력해야 합니다.
