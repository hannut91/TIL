# namespace

* 우리가 컴퓨터에서 파일을 관리할 때 한 폴더에 같은 이름의 파일을 만들려고 하면
  이름이 같아서 만들수가 없습니다.
* 하지만 다른 폴더에 같은 이름의 파일은 만들수가 있습니다.
* 이처럼 별도의 공간으로 분리할 수 있는게 `namespace`입니다.
* `inlcude`하는데 만약 같은 클래스, 함수 혹은 변수 이름을 사용하고 있다면
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

* 위의 예제 코드는 에러가 발생합니다. 두 개의 파일 모두 `welcome`라는 함수를
선언했기 때문입니다.
* 각각의 `welcome`을 실행하고 싶지만 이름이 같기 때문에 방법이 없습니다.
이런 경우 다음과 같이 `namespace`를 사용하여 해결할 수 있습니다.

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

## Defining namespaces

* namespace안에 어떤 코드든 작성될 수 있지만 클래스, 인터페이스, 함수 그리고
  상수들만 영향을 받습니다.
* `namespace`키워드로 선언할 수 있고 `declare`를 제외하고 반드시 코드보다 먼저
  작성되어야 합니다.

### Example #1

```php
<?php
namespace MyProject;

const CONNECT_OK = 1;
class Connection { /* ... */ }
function connect() { /* ... */  }
```

### Example #2

```php
<?php
namespace MyProject; // fatal error - namespace must be the first statement in the script
```

## Declaring sub-namespaces

* 디렉토리 - 파일 구조처럼 PHP네임스페이스도 계층을 가질 수 있습니다.
* 그래서 namespace이름을 하위레벨로 정의할 수 있습니다.

### Example #1

```php
<?php
namespace MyProject\Sub\Level;

const CONNECT_OK = 1;
class Connection { /* ... */ }
function connect() { /* ... */  }
```

* 위의 예는 3가지를 만듭니다.
  * MyProject\Sub\Level\CONNECT_OK
  * MyProject\Sub\Level\Connection
  * MyProject\Sub\Level\connect

## Defining multiple namespaces in the same file

* 하나의 파일에서 여러개의 namespace를 선언할 수 있습니다.

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

* 위와 같이 사용할 경우 구분이 잘 되지 않으므로 다음과 같이 작성할 수도
  있습니다.

```php
<?php

namespace language\en {
    function welcome() {
        return 'Hello world';
    }
}

namespace language\ko {
    function welcome() {
        return '안녕 세상아';
    }
}
```

* 하지만 하나의 파일에서 여러개의 네임스페이스를 사용하는 것은 권장되지
  않습니다. 
* 대부분 이렇게 사용하는 경우는 여러개의 파일들을 하나로 합칠 때
  사용합니다.
* 네임스페이스가 없는 파일들을 합치기 위해 사용됩니다.
* 그런데 만약 네임스페이스가 있는 파일과 네임스페이스가 없는 파일(글로벌 코드)
  를 합칠 떄는 다음과 같이 작성할 수 있습니다.
```php
<?php

namespace language\en {
    function welcome() {
        return 'Hello world';
    }
}

namespace {
    function welcome() {
        return '안녕 세상아';
    }
}
```

## Using namespaces: Basics

* PHP가 네임 스페이스로 구분 된 요소를 어떻게 요구 하는지를 이해하는 것이 
  중요합니다.
* namespace와 파일시스템을 비교하여 생각해봅시다.

1. `file.txt`같은 상대경로 파일이름의 경우 `currentdirectory/foo.txt`로
   해석됩니다. 만약 현재 위치가 `/home/foo`일 경우 `/home/foo/foo.txt`로
   해석됩니다.
2. `subdirectory/foo.txt`의 경우 `currentdirectory/subdirectory/foo.txt`로
   해석됩니다.
3. 절대경로인 `/main/foo.txt`는 `/main/foo.txt`로 해석됩니다.

* 같은 원리로 PHP namespace에도 적용이 될 수 있습니다.

1. `prefix`없이 사용될 때, 예를 들면 `$a = new foo()` 혹은 
  `foo::staticmethod()`
  * 만약 현재 namespace를 `currentnamespace`라고 한다면
    `currentanmespace\foo`로 해석합니다.
  * 만약 현재 namespace에서 정의되어있지 않은 경우 global변수로 해석합니다.
2. `$a = new subnamespace\foo()` 혹은 `subnamespace\foo::staticmethod()` 일
   경우
  * 현재 namespace가 `currentnamespace`일 때
    `currentnamespace\subnamespace\foo` 로 해석합니다.

  * 만약 namespace가 정의되어있지 않은 경우에는 `subnamespace\foo`로
    해석합니다.
3. `$a = new \currentnamespace\foo()` 혹은
   `\currentnamespace\foo::staticmethod();`일 경우에는
  *  이것은 항상 `currentnamespace\foo`로 해석됩니다.

### Example #1

file1.php
```php
<?php
namespace Foo\Bar\subnamespace;

const FOO = 1;
function foo() {}
class foo
{
    static function staticmethod() {}
}
```

file2.php
```php
<?php

namespace Foo\Bar;

include 'file1.php';

const FOO = 2;
function foo() {}
class foo
{
    static function staticmethod() {}
}

/* Unqualified name */
foo(); // resolves to function Foo\Bar\foo
foo::staticmethod(); // resolves to class Foo\Bar\foo, method staticmethod
echo FOO; // resolves to constant Foo\Bar\FOO

/* Qualified name */
subnamespace\foo(); // resolves to function Foo\Bar\subnamespace\foo
subnamespace\foo::staticmethod(); // resolves to class Foo\Bar\subnamespace\foo,
                                  // method staticmethod
echo subnamespace\FOO; // resolves to constant Foo\Bar\subnamespace\FOO
                                  
/* Fully qualified name */
\Foo\Bar\foo(); // resolves to function Foo\Bar\foo
\Foo\Bar\foo::staticmethod(); // resolves to class Foo\Bar\foo, method staticmethod
echo \Foo\Bar\FOO; // resolves to constant Foo\Bar\FOO
?>
```

### Example #2

* 만약 namespace에서 글로벌에서 이미 사용하고 있는 이름을 사용핧 경우
  글로벌것을 사용하기 위해서는 다음과 같이 사용해야 합니다.

```php
<?php
namespace Foo;

function strlen() {}
const INI_ALL = 3;
class Exception {}

$a = \strlen('hi'); // calls global function strlen
$b = \INI_ALL; // accesses global constant INI_ALL
$c = new \Exception('error'); // instantiates global class Exception
?>
```

## Namespaces and dynamic language features

* PHP의 네임 스페이스 구현은 프로그래밍 언어로서의 동적 특성에 영향을받습니다

### Example #1

example1.php
```php
<?php

class classname
{
    function __construct()
    {
        echo __METHOD__,"\n";
    }
}

function funcname()
{
    echo __FUNCTION__,"\n";
}

const constname = "global";

$a = 'classname';
$obj = new $a; // prints classname::__construct
$b = 'funcname';
$b(); // prints funcname
echo constant('constname'), "\n"; // prints global
?>
* 
```

### Example #2

```php
<?php
namespace namespacename;
class classname
{
    function __construct()
    {
        echo __METHOD__,"\n";
    }
}
function funcname()
{
    echo __FUNCTION__,"\n";
}
const constname = "namespaced";

include 'example1.php';

$a = 'classname';
$obj = new $a; // prints classname::__construct
$b = 'funcname';
$b(); // prints funcname
echo constant('constname'), "\n"; // prints global

/* note that if using double quotes, "\\namespacename\\classname" must be used */
$a = '\namespacename\classname';
$obj = new $a; // prints namespacename\classname::__construct
$a = 'namespacename\classname';
$obj = new $a; // also prints namespacename\classname::__construct
$b = 'namespacename\funcname';
$b(); // prints namespacename\funcname
$b = '\namespacename\funcname';
$b(); // also prints namespacename\funcname
echo constant('\namespacename\constname'), "\n"; // prints namespaced
echo constant('namespacename\constname'), "\n"; // also prints namespaced
?>
```

## Usting namespaces: Aliasing/Importing

PHP는 세가지의 aliasing혹은 importing을 지원합니다.
* 클래스 이름
* 인터페이스 이름
* 네임스페이스 이름

PHP5.6+에서는 함수와 상수이름도 가능합니다.

`use`오퍼레이터를 이용해서 aliasing을 할 수 있습니다.

## Sources

* http://php.net/manual/en/language.namespaces.rationale.php

