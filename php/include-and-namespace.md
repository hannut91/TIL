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

## namespace

우리가 컴퓨터에서 파일을 관리할 때 한 폴더에 같은 이름의 파일을 만들려고 하면
이름이 같아서 만들수가 없습니다. 하지만 다른 폴더에 같은 이름의 파일을 만들면
만들수가 있습니다. 이처럼 별도의 공간으로 분리할 수 있는게 `namespace`입니다. 
`inlcude`하는데 만약 같은 클래스 혹은 같은 함수나 변수 이름을 사용하고 있다면 
충돌이 나기 때문에 그런 문제를 해결하기 위해 사용됩니다.

greeting_en.php
```php
<?php

function welcome() {
    return 'Hello world';
}
```

greeting_ko.php
```php
<?php

function welcome() {
    return '안녕 세상아';
}
```

main.php
```php
require_once 'greeting_ko.php';
require_once 'greeting_en.php';

echo welcome();
echo welcome();
```

위의 예제 코드는 에러가 발생합니다. 두 개의 파일 모두 `welcome`라는 함수를
선언했기 때문입니다. 각각의 `welcome`을 실행하고 싶지만 이름이 같기 때문에
방법이 없습니다. 이런 경우 `namespace`를 사용할 수 있습니다.

greeting_en_ns.php
```php
<?php

namespace language\en;

function welcome() {
    return 'Hello world';
}
```

greeting_ko_ns.php
```php
<?php

namespace language\ko;

function welcome() {
    return '안녕 세상아';
}
```

main.php
```php
require_once 'greeting_ko.php';
require_once 'greeting_en.php';

echo language\ko\welcome();
echo language\en\welcome();
```

* 하나의 파일에서 여러개의 namespace를 가질 수 있습니다.

greeting_langs.php
```php
<?php

namespace language\en;

function welcome() {
    return 'Hello world';
}

namespace language\ko;

function welcome() {
    return '안녕 세상아';
}
```

main.php
```php
require_once 'greeting_langs.php';

echo language\ko\welcome();
echo language\en\welcome();
```

## Sources

* https://opentutorials.org/course/62/5138
