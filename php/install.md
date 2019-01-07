# PHP Install

```bash
$ brew install php
$ php -v
```

* 만약 설치 중 다음과 같은 에러가 출력된다면

```bash
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink sbin/php-fpm
/usr/local/sbin is not writable.

You can try again using:
  brew link php
```

* 다음과 같이 입력하이 다시 시도할 수 있습니다.

```bash
$ brew link php
```

* 그런데 만약 다음과 같이 에러가 발생한다면 `/usr/local/sbin` 폴더가 없어서
  발생합니다.

```bash
Linking /usr/local/Cellar/php/7.3.0_1... 
Error: Could not symlink sbin/php-fpm
/usr/local/sbin is not writable.
```

* 따라서 다음과 같이 만들어주고 권한을 설정하면 해결이 됩니다.

```bash
$ sudo chown -R $(whoami) $(brew --prefix)/sbin
$ brew link php
$ php -v
```

## Source

* https://github.com/Homebrew/homebrew-php/issues/4527#issuecomment-346712194
