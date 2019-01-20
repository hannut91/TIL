# Go tools

Golang에서 지원하는 도구들 사용하기

## Test

### Coverage 파일을 HTML로 확인하기

다음과같이 입력하여 Coverage결과를 저장한다.
```
$ go test -coverprofile=coverage.out
```

* Ginkgo를 사용한다면 다음과 같이 입력합니다.

```bash
$ ginkgo -cover -coverprofile=coverage.out
```

다음과같이 입력하여 결과를 웹에서 확인한다.
```
$ go tool cover -html=coverage.out
```

## See also
https://golang.org/pkg/testing
https://blog.golang.org/cover

## Go get
```
$ go get -t ./...
```
패키지가 테스를 실행하는데 필요한 패키지들을 다운로드 한다.
