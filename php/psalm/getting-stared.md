# PHP 정적분석기 Psalm시작하기

PHP 정적분석기중 하나인 Psalm 시작하기

## Install

* composer를 이용해 설치합니다.

```bash
composer require --dev vimeo/psalm
```

## 설정 초기화

* config 파일을 생성하고 실행합니다.
* 기본소스 파일 경로와 분석 레벨을 입력합니다. 1 부터 8 까지 높을 수록 분석을
  더 깐깐하게 합니다.

```bash
./vendor/bin/psalm --init ./src 8
```

## 실행

```bash
./vendor/bin/psalm
```

## Sources

* <https://github.com/vimeo/psalm>

