# PHP 정적분석기 전격분석

PHP정적분석기가 굉장히 많다. eslint처럼 모든걸 다 해주는 정적분석기를 찾으면서 정리해보았습니다.

## 대상 코드

```
├── src
│   └── Calculator.php
│   └── Util
│       └── Logger.php
```

src/Calculator.php
```php
<?php

namespace src;

// 사용하지 않음 use
use src\Util\Logger;
// 존재하지않는 클래스
use src\Util\NotExist;

// 클래서 다음에 오는 중괄호는 빈줄이 있어야함
class Calculator {
    // 생성자에서 사용하지 않는 파라미터
    // 함수 다음의 중괄호는 빈줄이 있어야함
    // 생성자 함수는 퍼블릭으로 선언되어야함
    function __construct($a) {
    }

    // 함수에서 사용하지 않는 파라미터
    public function plus($a, $b) {
        $d = 4; // 사용하지 않는 변수

        return $a + $c; // 존재하지 않는 변수
    }

    // return 타입이 맞지 않음
    public function minus(int $a): string {
        return $a;
    }
}
```

src/Util/Logger.php
```php
<?php

namespace src\Util;

class Logger {
    function log($a) {
        echo $a;
    }
}
```



## phpstan

### 실행 결과

```bash
$ ./vendor/bin/phpstan analyse src/ --level=7
 2/2 [▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓] 100%

 ------ ----------------------------------------------------------------------
  Line   Calculator.php                                                       
 ------ ----------------------------------------------------------------------
  15     Constructor of class src\Calculator has an unused parameter $a.      
  22     Undefined variable: $c                                               
  27     Method src\Calculator::minus() should return string but returns int. 
 ------ ----------------------------------------------------------------------

                                                                              
 [ERROR] Found 3 errors                                                       
                                                                              
```

## phan

### Config 파일

```php
<?php

use Phan\Issue;

return [
    'target_php_version' => NULL,
    'allow_missing_properties' => false,
    'null_casts_as_any_type' => false,
    'null_casts_as_array' => false,
    'array_casts_as_null' => false,
    'scalar_implicit_cast' => false,
    'scalar_array_key_cast' => false,
    'scalar_implicit_partial' => [],
    'strict_method_checking' => true,
    'strict_param_checking' => true,
    'strict_return_checking' => true,
    'ignore_undeclared_variables_in_global_scope' => false,
    'ignore_undeclared_functions_with_known_signatures' => false,
    'backward_compatibility_checks' => false,
    'check_docblock_signature_return_type_match' => true,
    'prefer_narrowed_phpdoc_param_type' => true,
    'prefer_narrowed_phpdoc_return_type' => true,
    'analyze_signature_compatibility' => true,
    'phpdoc_type_mapping' => [],
    'dead_code_detection' => true,
    'unused_variable_detection' => true,
    'quick_mode' => false,
    'simplify_ast' => true,
    'generic_types_enabled' => true,
    'globals_type_map' => [],
    'minimum_severity' => Issue::SEVERITY_LOW,
    'suppress_issue_types' => [],
    'exclude_file_regex' => '@^vendor/.*/(tests?|Tests?)/@',
    'exclude_file_list' => [],
    'exclude_analysis_directory_list' => [
        'vendor/',
    ],
    'enable_include_path_checks' => true,
    'processes' => 1,
    'analyzed_file_extensions' => [
        'php',
    ],
    'autoload_internal_extension_signatures' => [],
    'plugins' => [
        'AlwaysReturnPlugin',
        'DollarDollarPlugin',
        'DuplicateArrayKeyPlugin',
        'PregRegexCheckerPlugin',
        'PrintfCheckerPlugin',
        'SleepCheckerPlugin',
        'UnreachableCodePlugin',
    ],
    'directory_list' => [
        'src',
        'vendor/kahlan/kahlan/src',
        'vendor/phan/phan/src/Phan',
        'vendor/phpstan/phpstan/src',
    ],
    'file_list' => [],
];
```

### 실행 결과

```bash
$ ./vendor/bin/phan
[info] Disabling xdebug: Phan is around five times as slow when xdebug is enabled (xdebug only makes sense when debugging Phan itself)
[info] To run Phan with xdebug, set the environment variable PHAN_ALLOW_XDEBUG to 1.
[info] To disable this warning, set the environment variable PHAN_DISABLE_XDEBUG_WARN to 1.
[info] To include function signatures of xdebug, see .phan/internal_stubs/xdebug.phan_php
[debug] Checking PHAN_ALLOW_XDEBUG
[debug] The xdebug extension is loaded (2.7.0beta1)
[debug] Process restarting (PHAN_ALLOW_XDEBUG=internal|2.7.0beta1|1|*|*)
[debug] Running '/Users/yunseok/.phpbrew/php/php-7.3.0/bin/php' '-n' '-c' '/private/var/folders/cy/l0j4fl8j0_1dn73gq3_04rfw0000gn/T/IpI0ti' './vendor/bin/phan'
src/Calculator.php:6 PhanUnreferencedUseNormal Possibly zero references to use statement for classlike/namespace Logger (\src\Util\Logger)
src/Calculator.php:8 PhanUnreferencedUseNormal Possibly zero references to use statement for classlike/namespace NotExist (\src\Util\NotExist)
src/Calculator.php:11 PhanUnreferencedClass Possibly zero references to class \src\Calculator
src/Calculator.php:15 PhanUnusedPublicMethodParameter Parameter $a is never used
src/Calculator.php:19 PhanUnreferencedPublicMethod Possibly zero references to public method \src\Calculator::plus()
src/Calculator.php:19 PhanUnusedPublicMethodParameter Parameter $b is never used
src/Calculator.php:20 PhanUnusedVariable Unused definition of variable $d
src/Calculator.php:22 PhanUndeclaredVariable Variable $c is undeclared
src/Calculator.php:26 PhanUnreferencedPublicMethod Possibly zero references to public method \src\Calculator::minus()
src/Calculator.php:27 PhanTypeMismatchReturn Returning type int but minus() is declared to return string
src/Util/Logger.php:5 PhanUnreferencedClass Possibly zero references to class \src\Util\Logger
src/Util/Logger.php:6 PhanUnreferencedPublicMethod Possibly zero references to public method \src\Util\Logger::log()
[debug] Restarted process exited 1
```

## pslam

### 실행 결과

```bash
$ ./vendor/bin/psalm
Scanning files...
Analyzing files...

INFO: MissingParamType - src/Calculator.php:15:26 - Parameter $a has no provided type
    function __construct($a) {


INFO: MissingReturnType - src/Calculator.php:19:21 - Method src\Calculator::plus does not have a return type
    public function plus($a, $b) {


INFO: MissingParamType - src/Calculator.php:19:26 - Parameter $a has no provided type
    public function plus($a, $b) {


INFO: MissingParamType - src/Calculator.php:19:30 - Parameter $b has no provided type
    public function plus($a, $b) {


ERROR: UndefinedVariable - src/Calculator.php:22:21 - Cannot find referenced variable $c
        return $a + $c; // 존재하지 않는 변수


INFO: InvalidReturnType - src/Calculator.php:26:36 - The declared return type 'string' for src\Calculator::minus is incorrect, got 'int'
    public function minus(int $a): string {
        return $a;
    }


INFO: InvalidReturnStatement - src/Calculator.php:27:9 - The type 'int' does not match the declared return type 'string' for src\Calculator::minus
        return $a;


INFO: MissingReturnType - src/Util/Logger.php:6:14 - Method src\Util\Logger::log does not have a return type, expecting void
    function log($a) {


INFO: MissingParamType - src/Util/Logger.php:6:18 - Parameter $a has no provided type
    function log($a) {


------------------------------
1 errors found
------------------------------
8 other issues found.
You can hide them with --show-info=false
------------------------------

Checks took 0.11 seconds and used 28.438MB of memory
Psalm was able to infer types for 66.667% of analyzed code (2 files)
```

## PHP Code Sniffer

### 실행 결과

```bash
$ ./vendor/bin/phpcs src/ --standard=PSR2 --severity=5

FILE: /Users/yunseok/Development/php/src/Util/Logger.php
-----------------------------------------------------------------------------------
FOUND 3 ERRORS AFFECTING 2 LINES
-----------------------------------------------------------------------------------
 5 | ERROR | [x] Opening brace of a class must be on the line after the definition
 6 | ERROR | [ ] Visibility must be declared on method "log"
 6 | ERROR | [x] Opening brace should be on a new line
-----------------------------------------------------------------------------------
PHPCBF CAN FIX THE 2 MARKED SNIFF VIOLATIONS AUTOMATICALLY
-----------------------------------------------------------------------------------


FILE: /Users/yunseok/Development/php/src/Calculator.php
------------------------------------------------------------------------------------
FOUND 5 ERRORS AFFECTING 4 LINES
------------------------------------------------------------------------------------
 11 | ERROR | [x] Opening brace of a class must be on the line after the definition
 15 | ERROR | [ ] Visibility must be declared on method "__construct"
 15 | ERROR | [x] Opening brace should be on a new line
 19 | ERROR | [x] Opening brace should be on a new line
 26 | ERROR | [x] Opening brace should be on a new line
------------------------------------------------------------------------------------
PHPCBF CAN FIX THE 4 MARKED SNIFF VIOLATIONS AUTOMATICALLY
------------------------------------------------------------------------------------

Time: 47ms; Memory: 6MB
```

종류 | phpstan | phan | pslam | code sniffer
----|----|----|----|----
사용하지않는 alias | X | O | X | X
존재하지 않는 alias | X | X | X | X
PSR2 표준| X | X | X | X
생성자에서 사용하지 않는 파라미터 | O | O | X | X
생성자 함수는 퍼블릭으로 선언되어야함 | X | X | X | O
함수에서 사용하지 않는 파라미터 | X | O | X | X
사용하지 않는 변수 | X | O | X | X
존재하지 않는 변수 사용 | O | O | O | X
파라미터 리턴타입이 맞지않음 | X | O | O | X
함수 파라미터, 리턴 타입 있는지 확인 | X | X | O | X

## 결론

`phan`이 해주는게 가장 많으므로 `phan`으로 결정해야겠다.
