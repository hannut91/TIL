# Error Control Operators

PHP는 error control operator를 제공하는데 `@`연산자로 사용할 수 있습니다.
PHP에서 표현식앞에 `@`문자가 있으면 표현식에서 발생하는 어떤 에러메세지든
무시가 됩니다.  
만약 `set_error_handler()`로 커스텀 에러처리 함수를 세팅했다면 여전히 이 함수는
불러질 것이고`@`에 의해 처리된 에러가 발생했을 때는 `0`을 리턴하는
`error_reporting()`을 호출할 수 있습니다.  
만약 [track_errors](https://secure.php.net/manual/en/errorfunc.configuration.php#ini.track-errors)
기능이 활성화 되어 있다면 표현식에 의해 어느 에러메세지가 발생하면
`$php_errormsg`에 젖아될 것입니다. 이 변수는 각 에러에 의해 overwrite될 수 있기
때문에 이것을 사용할려면 체크하고 사용하여야 합니다.

```php
<?php
/* Intentional file error */
$my_file = @file ('non_existent_file') or
    die ("Failed opening file: error was '$php_errormsg'");

// this works for any expression, not just functions:
$value = @$cache[$key];
// will not issue a notice if the index $key doesn't exist.

?>
```

## Note

* `@`연산자는 오직 표현식에서만 작동합니다.
* 무언가에 값을 사용하고 있다면 그것에 `@`를 사용할 수 있습니다.
* 변수, 함수, `include`호출, 상수들에 사용할 수 있습니다.
* 하지만 함수나 클래스 선언에는 사용할 수 없고 `if`나 `foreach`같은 조건문에는
  사용할 수 없습니다.

## Warning

* 현재 `@`는 스크립트를 종료시키는 치명적인 에러들에 대한 에러 리포팅을
  비활성화 합니다.
* 특정한 에러를 출력하지 않도록 `@`를 사용하게 되면 오타가 났거나 혹은 에러가
  발생했을 때 이유에 대한 알림없이 스크립트가 그 즉시 종료될 것입니다.

## Source

* https://secure.php.net/language.operators.errorcontrol
