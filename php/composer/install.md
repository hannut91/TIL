# Composer install

PHP 패키지매니저 컴포저 설치하기

## wget으로 설치하기

```bash
$ wget https://raw.githubusercontent.com/composer/getcomposer.org/1b137f8bf6db3e79a38a5bc45324414a6b1f9df2/web/installer -O - -q | php -- --quiet
```

* `wget`이 없다면 `brew`를 이용해서 설치합니다.

```bash
brew install wget
```

* 만약 글로벌로 설치하고 싶다면 다음 명령어도 실행합니다.

```bash
$ mv composer.phar /usr/local/bin/composer
```

* 권한때문에 실패하는 경우 `sudo`를 붙여서 실행합니다.

## Sources

* https://modernpug.github.io/php-the-right-way/
* https://getcomposer.org/download/

