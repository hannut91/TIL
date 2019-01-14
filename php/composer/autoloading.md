# Autoloading

PHP 패키지 매니저 composer로 autoloading 세팅하기

## PHP Autoload

* 각 파일마다 클래스 하나를 정의하여 객체지향 프로그래밍을 할 때 각 스크립트에
  파일들을 import하는 것은 굉장히 짜증나는 일이다.

## composer.json

* `composer.json`에 다음과 같이 추가합니다.

```json
"autoload": {
    "psr-4": {"Src\\": "src/"}
}
```

* 그리고 `composer update`로 업데이트 합니다.

```bash
composer update
```

## Example

composer.json
```
{
    "name": "yunseok/php-test",
    "description": "for php test",
    "authors": [
        {
            "name": "Yunseok Han",
            "email": "hannut91@gmail.com"
        }
    ],
    "scripts": {
        "test": "./vendor/bin/kahlan"
    },
    "require-dev": {
        "kahlan/kahlan": "^4.5"
    },
    "autoload": {
        "psr-4": {"Src\\": "src/"}
    }
}
```

src/Calculator.php
```php
<?php

namespace src;

class Calculator {
    function plus($a, $b) {
        return $a + $b;
    }
}
```

spec/Calculator.spec.php
```php
<?php

use Src\Calculator;

describe('Calculator', function() {
    given('calculator', function() { return new Calculator(); });

    describe('plus', function() {
        given('subject', function() {
            return $this->calculator->plus($this->augend, $this->addend);
        });

        given('augend', function() { return 3; });
        given('addend', function() { return 4; });
        given('summation', function() { return 3 + 4; });

        it('returns summation', function() {
            expect($this->subject)->toEqual($this->summation);
        });
    });
});
```

## Sources

* https://getcomposer.org/doc/01-basic-usage.md#autoloading
* http://php.net/manual/en/language.oop5.autoload.php
