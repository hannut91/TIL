# Docker + Travis CI로 CI/CD 구축하기

Docker와 Travis CI를 이용하여 CI/CD 구축하기

## 요약

1. 배포할 패키지를 Dockerize합니다.
2. Travis CI에서 테스트가 통과되면 Docker image를 빌드하고 업로드 합니다.
3. 배포할 환경에서 image를 불러와서 배포합니다.

## Prerequisites

* Docker가 설치되어 있어야 합니다.
* docker-compose가 설치되어 있어야합니다. (Docker를 설치하면 자동으로
  설치됩니다.)
* Node.js가 설치되어 있어야 합니다.

## 따라하기

'Hello world'를 출력하는 간단한 Express app을 작성해봅시다.

```bash
$ mkdir express-example
$ cd express-example
$ npm init
$ npm i express
```

/app.js
```js
const express = require('express');

const GreetService = require('./services/greet.service');

const port = process.env.PROT || 3000;

const app = express();

app.get('/', (req, res) => {
  res.status(200).send(GreetService.greet(req.query.name));
});

app.listen(port, () => {
  console.log(`Listining to ${port}`);
});
```

/services/greet.service.test.js
```js
const GreetService = require('./greet.service');

test('Greet test', () => {
  expect(GreetService.greet('John Doe')).toBe('John Doe hello');
});
```

/services/greet.service.js
```js
exports.greet = (name) => `${name} hello`;
```

```bash
$ npm test
$ node app
$ open http://localhost:3000?name=Jane
```

화면에 "Jane hello"를 확인합니다.

## Dockerize

Dockerfile을 작성합니다.

/Dockerfile
```Dockerfile
FROM node:10.15.3
WORKDIR /u/app/
COPY package.json .
COPY package-lock.json .
RUN npm ci --only=production
COPY . .
```

Dockerize하는데 필요없는 파일들을 제외시키기 위해 dockerignore파일을 작성합니다.

/.dockerignore
```
node_modules
.git
```

ngnix config파일을 작성합니다.

/nginx/default.conf
```
server {
    listen 80;
    listen 443;

    server_name _;

    location / {
        proxy_pass http://app:3000;
    }
}
```

docker-compose.yml 파일을 작성합니다.
```yml
version: "3"

services:
  app:
    image: express-example
    build:
      dockerfile: Dockerfile
      context: .
    restart: always
    environment:
      - HOST=0.0.0.0
    expose:
      - "3000"
    command: node app

  nginx:
    image: nginx:1.17
    ports:
      - "80:80"
    volumes:
      - ./nginx:/etc/nginx/conf.d
    depends_on:
      - app
```

container를 실행합니다.
```bash
$ docker-compose up -d
$ open http://localhost?name=Jane # Jane hello 확인


# 종료
$ docker-compose down
```

dockerhub에서 repository를 생성한 후 .travis.yml을 작성합니다.

/.travis.yml
```yml
language: node_js

node_js: 10.15.3

env:
    - USER=yourDockerHubID REPO=DockerHubRepoName

install:
    - npm ci

script:
    - npm test

after_success:
    - docker login -u $DOCKER_USER -p $DOCKER_PASSWORD
    - docker build -t $USER/$REPO:${TRAVIS_COMMIT::7} .
    - docker push $USER/$REPO:${TRAVIS_COMMIT::7}
```

Github에 repo를 생성한 후 <https://travis-ci.org>에서 repo를 활성화해줍니다. 그
후 푸시를 한 후 pull request를 생성하여 build되는 것을 확인하고 docker
hub에도 커밋이름으로 태그가 붙은 이미지가 업로드되었는지 확인합니다.

이제 pull request를 보낼 때 마다 Travis CI에서 image를 빌드하여 docker hub로
업로드하게 되고 내가 원할 때 실제 동작할 서버에서 docker image를 pull받아서
실행할 수 있습니다. 만약 배포한 image에 문제가 있다면 전의 commit태그가 있는
image로 pull받아 docker를 실행하여 언제든 다시 쉽게 롤백이 가능합니다.
