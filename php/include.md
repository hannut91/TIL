# include and namespace

## include

현재 실행시키려 하는 PHP파일에서 다른 PHP파일을 포함시킬 때 사용하는 것

### Example

```php
// welcome.php
<?php

function welcome() {
    return 'Hello world';
}

```php
// main.php
<?php

include 'welcome.php';

echo welcome();
```

PHP는 외부의 php 파일을 로드하는 방법으로 4가지 형식을 제공합니다.

* include
* include_once
* require
* require_once

### `include`와 `require`의 차이점

* 불러오려는 파일을 사용할 수 없을 때 `include`는 `warning`에러가 발생합니다.
  하지만 `require`는 `fatal`에러가 발생합니다.

* 만약 include를 여러번 할 경우 여러번 php가 여러번 포함되어 중복되어 코드가
  실행됩니다.
* 하지만 `include_once`을 여러번 실행 할 경우 한 번만 php파일이 포함됩니다.
* include하는 파일이 다른 php파일을 include하고 그 include한 파일을 다시
  include할 경우 복수개에 php파일이 포함될 수 있습니다. 그래서 `include_once`를
  사용하는 것이 좋습니다.

## Usting namespaces: Aliasing/Importing

PHP는 세가지의 aliasing혹은 importing을 지원합니다.
* 클래스 이름
* 인터페이스 이름
* 네임스페이스 이름

PHP5.6+에서는 함수와 상수이름도 가능합니다.

`use`오퍼레이터를 이용해서 aliasing을 할 수 있습니다.

## Sources

* https://opentutorials.org/course/62/5138
* http://php.net/manual/en/language.namespaces.importing.php

