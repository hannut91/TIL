# PHP Code Sniffer install

PHP Code Sniffer 설치하기

## Install

### Composer

* `composer`로 설치합니다.

```bash
composer require --dev squizlabs/php_codesniffer
```

## Run

```bash
$ ./vendor/bin/phpcs src/ --standard=PSR2

FILE: /Users/yunseok/Development/php/src/Calculator.php
-----------------------------------------------------------------------------------
FOUND 2 ERRORS AFFECTING 2 LINES
-----------------------------------------------------------------------------------
 5 | ERROR | [x] Opening brace of a class must be on the line after the definition
 6 | ERROR | [x] Opening brace should be on a new line
-----------------------------------------------------------------------------------
PHPCBF CAN FIX THE 2 MARKED SNIFF VIOLATIONS AUTOMATICALLY
-----------------------------------------------------------------------------------

Time: 124ms; Memory: 6MB
```

* `PHP Code Sniffer`는 자동으로 수정하는 기능까지 제공하는데 다음과 같이 실행할
  수 있습니다.

```bash
$ ./vendor/bin/phpcbf src/ --standard=PSR2

PHPCBF RESULT SUMMARY
----------------------------------------------------------------------
FILE                                                  FIXED  REMAINING
----------------------------------------------------------------------
/Users/yunseok/Development/php/src/Calculator.php     2      0
----------------------------------------------------------------------
A TOTAL OF 2 ERRORS WERE FIXED IN 1 FILE
----------------------------------------------------------------------

Time: 58ms; Memory: 6MB
```

## Sources

* https://github.com/squizlabs/PHP_CodeSniffer
