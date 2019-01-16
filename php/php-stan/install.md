# PHP Stan - PHP Static Anlysis Toll

PHP Stan 설치하기

## Install

```bash
composer require --dev phpstan/phpstan
```

## Run 

* `analyse`커맨드를 사용하여 실행할 수 있습니다.

```bash
./vendor/bin/phpstan analyse src
```

* 기본으로 Rule level이 0인데 최대로 설정하고 싶다면 `--level max`혹은 0 부터
  7까지 숫자를 입력하면 Rule level을 설정하여 실행할 수 있습니다.

## Errors

```bash
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - nette/neon v2.4.3 requires ext-iconv * -> the requested PHP extension iconv is missing from your system.
    - nette/neon v2.4.2 requires ext-iconv * -> the requested PHP extension iconv is missing from your system.
    - nette/neon v2.4.1 requires ext-iconv * -> the requested PHP extension iconv is missing from your system.
    - nette/neon v2.4.0 requires ext-iconv * -> the requested PHP extension iconv is missing from your system.
    - nette/neon v2.3.5 requires ext-iconv * -> the requested PHP extension iconv is missing from your system.
    - nette/neon v2.3.4 requires ext-iconv * -> the requested PHP extension iconv is missing from your system.
    - nette/neon v2.3.3 requires ext-iconv * -> the requested PHP extension iconv is missing from your system.
    - phpstan/phpstan 0.10.8 requires nette/di ^2.4.7 || ^3.0 -> satisfiable by nette/di[v2.4.10, v2.4.11, v2.4.12, v2.4.13, v2.4.14, v2.4.7, v2.4.8, v2.4.9].
    - nette/di v2.4.10 requires nette/neon ^2.3.3 || ~3.0.0 -> satisfiable by nette/neon[v2.3.3, v2.3.4, v2.3.5, v2.4.0, v2.4.1, v2.4.2, v2.4.3].
    - nette/di v2.4.11 requires nette/neon ^2.3.3 || ~3.0.0 -> satisfiable by nette/neon[v2.3.3, v2.3.4, v2.3.5, v2.4.0, v2.4.1, v2.4.2, v2.4.3].
    - nette/di v2.4.12 requires nette/neon ^2.3.3 || ~3.0.0 -> satisfiable by nette/neon[v2.3.3, v2.3.4, v2.3.5, v2.4.0, v2.4.1, v2.4.2, v2.4.3].
    - nette/di v2.4.13 requires nette/neon ^2.3.3 || ~3.0.0 -> satisfiable by nette/neon[v2.3.3, v2.3.4, v2.3.5, v2.4.0, v2.4.1, v2.4.2, v2.4.3].
    - nette/di v2.4.14 requires nette/neon ^2.3.3 || ~3.0.0 -> satisfiable by nette/neon[v2.3.3, v2.3.4, v2.3.5, v2.4.0, v2.4.1, v2.4.2, v2.4.3].
    - nette/di v2.4.7 requires nette/neon ^2.3.3 || ~3.0.0 -> satisfiable by nette/neon[v2.3.3, v2.3.4, v2.3.5, v2.4.0, v2.4.1, v2.4.2, v2.4.3].
    - nette/di v2.4.8 requires nette/neon ^2.3.3 || ~3.0.0 -> satisfiable by nette/neon[v2.3.3, v2.3.4, v2.3.5, v2.4.0, v2.4.1, v2.4.2, v2.4.3].
    - nette/di v2.4.9 requires nette/neon ^2.3.3 || ~3.0.0 -> satisfiable by nette/neon[v2.3.3, v2.3.4, v2.3.5, v2.4.0, v2.4.1, v2.4.2, v2.4.3].
    - Installation request for phpstan/phpstan ^0.10.8 -> satisfiable by phpstan/phpstan[0.10.8].

  To enable extensions, verify that they are enabled in your .ini files:
    - /Users/yunseok/.phpbrew/php/php-7.3.0/etc/php.ini
  You can also run `php --ini` inside terminal to see which files are used by PHP in CLI mode.

Installation failed, reverting ./composer.json to its original content.
```

* 만약 설치 중 dnldhk 같은 에러가 발생한 경우 php extension `iconv`가 설치되어
  있지 않아 생기는 문제입니다. 이를 확인하기 위해서는 `php -m`으로 설치된
  모듈들을 확인할 수 있습니다. 없다면 설치를 해야합니다.
* `phpbrew`를 사용하고 있을 경우 다음과 같이 설치합니다.

```bash
phpbrew ext install iconv
```

* 만약 설치 중 다음과 같은 에러가 발생한다면 `build.log`에서 에러를 확인합니다.

```bash
Error: Command failed: ./configure --with-php-config=/Users/yunseok/.phpbrew/php/php-7.3.0/bin/php-config >> /Users/yunseok/.phpbrew/build/php-7.3.0/ext/iconv/build.log 2>&1 returns:

# in build.log
configure: error: Please specify the install prefix of iconv with --with-iconv=<DIR>
```

* 에러를 확인했는데 위와 같다면 `iconv`를 빌드하여 경로를 지정해주어야 합니다.

```bash
phpbrew ext install iconv --with-iconv=<DIR>
```

* `<DIR>`은 iconv를 다운받아 빌드한 경로를 입력해줘야합니다.
* https://www.gnu.org/software/libiconv/#downloading에서 iconv를 다운받은 후
  압축을 풀고 그 폴더에서 다음과 같이 실행합니다.

```bash
./configure --prefix=/usr/local
make
make install
```

* 위의 명령어를 다 실행한 후 해당 경로를 아래 `<DIR>`에 입력해주면 설치가
  진행됩니다.

```bash
phpbrew ext install iconv --with-iconv=<DIR>
```

* 그리고 다시 `phpstan`설치를 진행하면 됩니다.
