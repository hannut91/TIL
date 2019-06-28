# CodeceptJS 와 Selenium으로 E2E테스트 시작하기

Modern E2E testing framework CodeceptJS로 E2E테스트 시작하기

## 요약

* `codeceptjs`, `webdriverio`, `selenium-standalone`을 설치합니다.
* `codeceptjs`설정파일을 생성합니다.
* 테스트 작성 후 테스트를 실행합니다.

## Prerequisites

* Node.js가 설치되어 있어야 합니다.

## 설치

```bash
$ mkdir e2e-example && cd e2e-example
$ npm init

$ npm install codeceptjs webdriverio selenium-standalone --save-dev
```

## 설정파일 만들기

```bash
./node_modules/.bin/codeceptjs init
```

Chrome에서만 테스트를 실행한다면 `Puppeteer`를 선택해도 좋지만 Safari도 같이
테스트 하기 위해 `Webdriver`를 선택합니다.  다음으로 나오는 prompt들은 일단 
enter키를 눌러 넘어갑니다.

## 테스트 작성하기

```bash
$ ./node_modules/.bin/codeceptjs gt
```

테스트 파일 이름과 테스트 이름을 입력해줍니다.
그 후 테스트 파일을 아래와 같이 편집합니다.

```js
Feature('My First Test');

Scenario('test something', (I) => {
  I.amOnPage('https://github.com');
  I.see('GitHub');
});
```

## 웹드라이버 설치하기

```bash
./node_modules/.bin/selenium_standalone install
```

## 셀레늄 서버 실행하기

```bash
./node_modules/.bin/selenium_standalone start
```

## 테스트 실행하기

```bash
./node_modules/.bin/codeceptjs run
```

## Sources

* <https://github.com/vvo/selenium-standalone>

