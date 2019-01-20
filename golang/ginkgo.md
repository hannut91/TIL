# Ginkgo

BDD-style Go testing framework

## Getting started

### Install
```
$ go get github.com/onsi/ginkgo/ginkgo
$ go get github.com/onsi/gomega/...
```

### Bootstrapping a Suite
Ginkgo테스트를 실행하기 위해서는 test suit파일을 만들어야 합니다.
```
$ cd path/to/books
$ ginkgo bootstrap
```

bootstrap을 실행하면 books_stuite_test.go파일이 다음과같이 생성된다.
```
package books_test

import (
    . "github.com/onsi/ginkgo"
    . "github.com/onsi/gomega"
    "testing"
)

func TestBooks(t *testing.T) {
    RegisterFailHandler(Fail)
    RunSpecs(t, "Books Suite")
}
```

package 이름이 books가 아니라 books_test인것을 볼 수 있는데 books패키지의 캡슐화를 할 수 있다.
이는 필수가 아닌 옵션으로 필요가 없다면 books로 패키지이름을 변경하면 된다.
`TestBooks`가 go lang에서 `testing` tset인데 Go의 테스트 러너가 이 함수를 실행한다.
`RegisterFailHandler(Fail)`은 함수를 Gomega로 보낼 때 사용하는 함수이다.
`RunSpecs`는 Ginkko가 test suite를 실행하도록 명령내리는 것입니다. 

`go test` 혹은 `ginkgo`를 실행하여 테스트를 실행할 수 있습니다.

### Adding Specs to a Suite
ginkgo generate를 이용하여 테스트를 작성할 수 있습니다. 

```
$ ginkgo generate book
```

### Marking specs as failed
테스트가 실패하는 경우 다음과 같이 작성하여 테스트를 실패시킬 수 있다.
```
Fail("Failure reason")
```

Fail이 실행 될 경우 현재 테스트 되고 있는 spec은 멈춘다. panic은 rescue되어 다음 테스트로 넘어가게 된다.
하지만 만약 테스트가 goroutine을 실행하고 있을 경우 Ginkgo가 panic을 rescue할 수 없다.
이럴경우는 다음과같이 goroutine안에 `GinkgoRecover()`를 실행하여야 한다.

```
It("panics in a goroutine", func(done Done) {
    go func() {
        defer GinkgoRecover()

        Ω(doSomething()).Should(BeTrue())

        close(done)
    }()
})
```

오메가가 만약 false를 리턴한다면 Gomega는 Fail함수를 실행할 것이고 panic이 발생할 것입니다. GinkgoRecover가 recover하여 test suite가 멈추는것을
방지할 수 있습니다.

### Logging output
`GinkgoWriter`라는 `io.Writer`전역변수가 있는데 이 Wirter에 Write하면 테스트가 실패할 경우 결과들을 출력해준다. 이는 테스트를 실행할 떄
```
$ ginkgo -v 

or

$ go test -ginko.v
```

라고 실행하여야 결과를 볼 수 있다.

만약 테스트가 실행중에 강제로 테스트가 종료된다면 지금까지 가지고 있는 데이터들을 출력해준다.

### IDE Support
`ginkgo watch`는 파일이 변경될 때마다 테스트를 실행할 수 있도록 기능을 제공합니다.

## Structuring Your Specs
### Individual specs: `It`
`It`는 하나의 스펙을 작성할 떄 사용된다. 이는 Describe나 Context아래에서 작성됩니다.

### The `Specify` Alias
 
