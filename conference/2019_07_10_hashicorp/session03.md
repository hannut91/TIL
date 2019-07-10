# Infrastructure as Code 성공적으로 정착시키기 (박성훈)

## 현황

* AWS기반 서비스 인프라 전체
* AWS 로그인 방식과 권한 관리
* 효율적인 IaC 작업환경 구성
* 개인 테스트 환경을 매일 생성, 삭제하는 것이 가능

### 도구

* Terraform, Packer, Ansible, AWSCLI, AWS Secrets Manager

## 성공적인 구현을 위한 조건

* 조직 문화
* Git을 제대로 활용해야함
* 예제 제공
  * 누구나 실체를 만들어 볼 수 있는 예제 코드를 제공하는 것으로 시작해야 함.
* technical dept 쌓지 않기
* 코드 재사용
  * Ansible role, Terraform module등 활용
* 반복 업애기
  * 여러 도구의 공통 설정은 한 번만 하고 각 도구의 설정으로 변환
  * 반복 작업을 최소화하는 작업환경 제공 (코드화)
* 지속적인 개량과 단순화
* 도구간 코드 의존성 최소화
* 교육, 코드리뷰
* 진입장벽 없애기

## 기술의 목표

비즈니스 경쟁력을 높이기 위해

## 방법

* 자동화

### 자동화로 얻을 수 있는 것

* Speed
* Quality
* Cost

사람이 하지 못하는 것을 하는 것