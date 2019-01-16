# Kahlan으로 Coverage확인하기

Kahlan프레임워크를 이용해서 PHP Coverage확인하는 방법

## coverage 결과 확인하기

```bash
./vendor/bin/kahlan --coverage=4
```

결과 예제
```bash
Coverage Summary
----------------
                                 Lines           %

 \                               1 / 1     100.00%
└── src\                         1 / 1     100.00%
   └── Calculator                1 / 1     100.00%
      └── Calculator::plus()     1 / 1     100.00%

Total: 100.00% (1/1)

Coverage collected in 0.003 seconds
```

* `--coverage=4`는 method단위까지 커버리지 결과를 보고싶을 때 사용되는
  옵션입니다. 0에서 4까지 프로젝트, 네임스페이스, 클래스, 메소드 단위로
  확인할 수 있습니다.
* 만약 특정 네임스페이스의 라인 별로 커버리지를 확인하고싶은 경우
  `--coverage="src\\"`로 지정하면 됩니다.
* 모든 네임스페이스를 라인 별로 커버리지를 확인하고 싶다면 `--coverage=""` 혹은
  `--coverage=`라고 입력하면 됩니다.

```bash
./vendor/bin/kahlan --coverage=""
```

결과
```bash
Coverage Summary
----------------
                           Lines           %

 src\Calculator            1 / 1     100.00%
└── Calculator::plus()     1 / 1     100.00%

File: /Users/yunseok/Development/php/src/Calculator.php

     1:      <?php
     2:      
     3:      namespace src;
     4:      
     5:      class Calculator
     6:      {
     7:          public function plus($a, $b)
     8:          {
     9:2             return $a + $b;
    10:          }
    11:      }



  Total: 100.00% (1/1)

Coverage collected in 0.003 seconds
```

## istanbul라이브러리를 이용해서 HTML로 결과 확인하기

### Requirement


* `istanbul`라이브러리가 설치되어 있어야 하므로 다음과 같이 설치합니다.

```bash
npm install -g istanbul

or

yarn global add istanbul
```

### 실행

```bash
./vendor/bin/kahlan --istanbul=coverage.json
istanbul report
open coverage/lcov-report/index.html 
```

## Sources

* https://kahlan.github.io/docs/pro-tips.html

