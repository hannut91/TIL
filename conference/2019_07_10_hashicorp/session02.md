# Advanced Terraform

고급기법을 사용하는 것일까? Production level과 글로벌, 대규모에서 사용하는 것

## Tips

* terraform to tf alias를 만들어라
* landscape
`$ tf plan`을 했을 떄 landscape를 하게 되면 추가 된 것과 변경되는 것을 쉽게
눈으로 확인이 가능합니다.
* fmt라는 커맨드가 있습니다. 포맷팅 해주는 것
tf fmt -check는 차이만 보여준다.

## Remote state

여러사람들과 같이 일할 때 문제를 방지하기 위해
* Remote state를 사용하고
* state locking을 사용하라
* atlantis를 사용하라(plan과 apply를 같은환경에서 할 수 있도록)

## Work Directory 설계

Input
Resource
Output

### Monolitic design

### Microservice design

## CI/CD Pipeline

* Ansible-pull 자기 스스로 코드를 가져와서 deploy
terraform => userdata.sh => ansible => cron(10분마다) => ansible

## Multi-cloud with Terraform
