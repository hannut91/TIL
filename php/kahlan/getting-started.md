# Getting Started

## 요구사항

* PHP 5.5+
* phpdbg or Xdebug (커버리지 분석에만 사용됨)

## 설치

* `Composer`를 이용해 프로젝트에 `development dependency`로 설치합니다.

```bash
composer require --dev kahlan/kahlan
```

## 실행

```php
├── spec
    └── ClassA.spec.php
```

* 위와 같이 파일을 만든 후 `ClassA.spec.php`를 수정합니다.

```
// ClassA.spec.php
<?php

describe("ToBe", function() {
    describe("::match()", function() {
        it("passes if true === true", function() {
            expect(true)->toBe(true);
        });
    });
});
```

```bash
$ ./vendor/bin/kahlan
```

* 기본으로 root폴더의 `spec`폴더를 기준으로 테스트파일을 찾아서 테스트합니다.
  만약 특정 파일 혹은 다른 폴더를 지정해서 테스트하고 싶다면 다음과 같이
  입력합니다.

```bash
./vendor/bin/kahlan --spec=yourDirectory
```

### 폴더 구조

* 권장하는 폴더 구조는 프로젝트 루트에 `spec`이라는 디렉토리를 만들고 그 폴더
  안에 source파일과 동일한 구조를 갖는 테스트 파일들을 만드는 것입니다.
* 테스트 파일이름은 `.spec.php`로 끝나거나 `Spec.php`로 끝나야 합니다.

```
├── spec                       # The directory containing your specs
│   └── ClassA.spec.php
│   └── subdir
│       └── ClassB.spec.php
├── src                        # The directory containing your source code
│   └── ClassA.php
│   └── subdir
│       └── ClassB.php
├── composer.json
└── README.md
```

## Sources

* https://kahlan.github.io/docs/getting-started.html
