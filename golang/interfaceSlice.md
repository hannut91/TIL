# InterfaceSlice

```go
var dataSlice []int = []int{1, 2, 3}
var interfaceSlice []interface{} = dataSlice
```

* 위와 같이 작성된 코드가 있다. 위의 코드를 컴파일 할 시 다음과 같은 에러가
  발생합니다. 

```bash
cannot use dataSlice (type []int) as type []interface {} in assignment
```

## Why? 

* 에러가 나는 이유 2가지가 있습니다.
  * `[]interface{}`는 인터페이스가 아닙니다.
  * `[]interface{}`는 각 element타입이 interface{}인 slice 입니다.
  * 각 `interface{}`은 두 단어를 가지고 있는데 하나는 포함 된 데이터의 타입을 
    가리키고 다른 하나는 포함 된 데이터 혹은 포인터를 가지고 있습니다.
  * 그 결과 길이 N의 slice `[]interface{}`는 Nx2의 길이의 데이터를 가지고
    있습니다.
  * `[]int`는 길이 N의 slice `[]int`의 길이는 N * sizeof(int)의 길이만큼 데이터를
    가지고 있습니다.
  * 따라서 `[]int`를 `[]interface{}`로 할당할 수 없습니다.


## What can I do instead?

* `dataSlice`의 타입을 `interface{}`로 사용하는 방법이 있습니다.
* 혹은 다음과 같이 작성하는 방법이 있습니다.

```go
var dataSlice []int = foo()
var interfaceSlice []interface{} = make([]interface{}, len(dataSlice))
for i, d := range dataSlice {
	interfaceSlice[i] = d
}
```

## Source

* https://github.com/golang/go/wiki/InterfaceSlice
