# PHP phan 설치하기

PHP phan라이브러리 설치방법

## Install

### Depedencies

* PHP 7 이상
* PHP extension php-ast 0.1.5이상

### php-ast install

```bash
pecl install ast-1.0.0
```

* 설치 후 `php.ini`에 `extension=ast.so`를 추가합니다.
* 추가한 후 `php -m`으로 `ast`가 있는지 확인합니다.

### phan install

* `composer`를 이용해 설치합니다.

```bash
composer require --dev phan/phan
```

## Run

```bash
./vendor/bin/phan
```

## Sources

* https://github.com/phan/phan/wiki/Getting-Started

