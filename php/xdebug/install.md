# Xdebug 설치

Xdebug 설치하기

* 디버깅과 개발을 돕는 PHP 확장 라이브러리입니다.
* IDE와 함께 사용하기 위해 [single step debugger](https://xdebug.org/docs/remote)를 포합합니다.
* PHP의 [var_dump()](https://xdebug.org/docs/display)를 업그레이드합니다.
* Notices, Warnings, Errors 그리고 Exceptions를 위한
  [stack_traces](https://xdebug.org/docs/stack_trace)를 추가합니다.
* 모든 함수 호출 및 변수 할당을 디스크에 기록하는 기능이 있습니다.
* 프로파일러가 포함되어 있습니다. 
* PHPUnit과 함께 사용할 수있는 코드 커버리지 기능을 제공합니다.

## Installation

* `PECL`을 이용하여 설치합니다.

```bash
pecl install xdebug
```

* 현재 PHP 버전 7.3을 사용하고 있다면 현재 버전 xdebug와 호환이 되지 않아서
  설치 시 에러가 발생합니다. 이럴 경우 현재 베타 버전으로 설치해야 합니다.
* 참고: https://bugs.xdebug.org/view.php?id=1584

```bash
pecl install xdebug-beta
```

```bash
Build process completed successfully
Installing '/Users/yunseok/.phpbrew/php/php-7.3.0/lib/php/extensions/no-debug-non-zts-20180731/xdebug.so'
install ok: channel://pecl.php.net/xdebug-2.7.0beta1
configuration option "php_ini" is not set to php.ini location
You should add "zend_extension=/Users/yunseok/.phpbrew/php/php-7.3.0/lib/php/extensions/no-debug-non-zts-20180731/xdebug.so" to php.ini
```

* 설치를 하게 되면 위와 같은 결과를 확인할 수 있습닏나. 현재 마지막 줄에 보면
  `php.ini`에 설정을 추가하라는 문장이 있습니다. 설정을 그대로 복사해서
  `php.ini`에 추가하면 됩니다.
* 현재 사용하고 있는 `php.ini`의 경로를 확인하고 싶다면 `php --ini`를 
  입력합니다.

## Sources

* https://xdebug.org/index.php
* https://xdebug.org/docs/install
* https://bugs.xdebug.org/view.php?id=1584
