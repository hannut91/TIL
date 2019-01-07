# phpbrew install

## Requirement

* [`Homebrew`](https://brew.sh/)를 이용 중이라면 먼저 다음과 같이 기본적으로 필요한
  라이브러리들을 설치해야 합니다.

```bash
xcode-select --install
brew install automake autoconf curl pcre bison re2c mhash libtool icu4c gettext jpeg openssl libxml2 mcrypt gmp libevent
brew link icu4c
brew link --force openssl
brew link --force libxml2
```

## Install

```bash
curl -L -O https://github.com/phpbrew/phpbrew/raw/master/phpbrew
chmod +x phpbrew

# phpbrew를 $PATH로 옮깁니다. 
sudo mv phpbrew /usr/local/bin/phpbrew
```

* 위와 같이 입력하여 설치합니다.

## Setting

* 초기화를 해줍니다.

```bash
phpbrew init
```

* bash를 사용할 경우 다음과 같이 입력합니다.

```bash
echo "[[ -e ~/.phpbrew/bashrc ]] && source ~/.phpbrew/bashrc" >> ~/.bashrc
```

* 변경된 설정을 불러옵니다.

```bash
source ~/.phpbrew/bashrc
```

* php 정보를 불러옵니다.

```bash
phpbrew update
```

* 사용가능한 PHP버전 정보를 가져옵니다.

```bash
phpbrew known
```

* 사용가능한 variants를 불러옵니다.

```bash
phpbrew variants
```

* PHP를 설치합니다.

```bash
phpbrew install 7.3 +default
```

* 설치된 PHP 목록을 확인합니다.

```bash
phpbrew list
```

* 기본으로 사용할 버전을 선택합니다.

```bash
phpbrew switch php-7.3.0
```

## Errors

```bash
Error: Configure failed:
The last 5 lines in the log file:
checking if the location of ZLIB install directory is defined... no

checking whether to enable bc style precision math functions... yes

checking for BZip2 support... yes

checking for BZip2 in default path... not found

configure: error: Please reinstall the BZip2 distribution
```

* 만약 설치 중 위와 같은 에러가 발생한다면 설치시 BZip2의 경로를 같이 적어야
  합니다.
* BZip2가 설치되어 있지 않다면 `brew install BZip2`로 설치해주세요.

```bash
phpbrew install 7.3 +default +bz2=/usr/local/Cellar/bzip2/1.0.6_1/ 
```

```bash
Error: Configure failed:
The last 5 lines in the log file:
checking whether to enable zend-test extension... no

checking for zip archive read/writesupport... yes

checking pcre install prefix... /usr/local

checking libzip... yes

checking for the location of zlib... configure: error: zip support requires ZLIB. Use --with-zlib-dir=<DIR> to specify prefix where ZLIB include and library are located
```

* 만약 설치 중 위와 같은 에러가 발생한다면 설치시 `zlib`의 경로를 같이 적어야
  합니다.
* zlib가 설치되어 있지 않다면 `brew install zlib`로 설치해주세요.

```bash
phpbrew install 7.3 +default +bz2=/usr/local/Cellar/bzip2/1.0.6_1/ +zlib=/usr/local/Cellar/zlib/1.2.11/
```

## Sources

* https://github.com/phpbrew/phpbrew/wiki/Quick-Start
* https://github.com/phpbrew/phpbrew
* https://github.com/phpbrew/phpbrew/issues/966#issuecomment-427515474



