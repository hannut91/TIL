# InterfaceSlice

```go
var dataSlice []int = []int{1, 2, 3}
var interfaceSlice []interface{} = dataSlice
```

* 위와 같이 작성된 코드가 있습니다. 위의 코드를 컴파일 할 시 다음과 같은 
  에러가 발생합니다. 

```bash
cannot use dataSlice (type []int) as type []interface {} in assignment
```

## Why? 

* `[]interface{}`는 인터페이스가 아닙니다.
* `[]interface{}`는 각 element타입이 interface{}인 slice 입니다.
* 각 `interface{}`은 두 단어를 가지고 있는데 하나는 포함 된 데이터의 타입을 
  가리키고 다른 하나는 포함 된 데이터 혹은 포인터를 가지고 있습니다.
* 그 결과 길이 N의 slice `[]interface{}`는 Nx2의 길이의 데이터를 가지고
  있습니다.
* `[]int`는 길이 N의 slice `[]int`의 길이는 N * sizeof(int)의 길이만큼 데이터를
  가지고 있습니다.
* 따라서 `[]int`를 `[]interface{}`로 할당할 수 없습니다.

## Test

* 실제로 메모리를 어떻게 가지고 있는지 실험해보았습니다.

```go
func main() {
	PrintMemUsage()

	var dataSlice []int64 = make([]int64, 0, 1024*1024/8)

	PrintMemUsage()

	runtime.GC()

	var interfaceSlices []interface{} = make([]interface{}, 0, 1024*1024/8)

	PrintMemUsage()

	_ = dataSlice
	_ = interfaceSlices
}

func PrintMemUsage() {
	var m runtime.MemStats
	runtime.ReadMemStats(&m)
	fmt.Printf("Alloc = %v MiB", byteToMegaByte(m.Alloc))
	fmt.Printf("\tTotalAlloc = %v MiB", byteToMegaByte(m.TotalAlloc))
	fmt.Printf("\tSys = %v MiB", byteToMegaByte(m.Sys))
	fmt.Printf("\tNumGC = %v\n", m.NumGC)
}

func byteToMegaByte(b uint64) uint64 {
	return b / 1024 / 1024
}
```

```bash
Alloc = 0 MiB   TotalAlloc = 0 MiB      Sys = 66 MiB    NumGC = 0                              
Alloc = 1 MiB   TotalAlloc = 1 MiB      Sys = 68 MiB    NumGC = 0                              
Alloc = 2 MiB   TotalAlloc = 3 MiB      Sys = 68 MiB    NumGC = 1 
```

* 실험 결과는 위와 같습니다. 첫 출력시에 메모리가 0 이었는데 int64 slice를
  만들었을 때 `1MB`가 할당 되어 있습니다.
* 같은 길이의 interface{}의 슬라이스를 만든 이후에는 두배의 크기인 `2MB`가
  할당된 것을 확인할 수 있었습니다.


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

# Method of Interface

```go
type Duck interface {
	quack()
}

type DonaldDuck struct {
}

func (donald DonaldDuck) quack() {
	fmt.Println("Quack!")
}

func quack(duck Duck) {
	duck.quack()
}
```

* `Duck`라는 인터페이스는 `quack()`라는 메소드를 가지고 있습니다. 
* `DonaldDuck`타입은 `quack()`메소드를 구현하고 있으므로  `Duck`인터페이스를 
  구현하고 있습니다.
* `DonaldDuck`의 인스턴스가 포인터이든 아니든 상관없이 다음 테스트는 
  통과합니다.

```go
func ExampleQuack() {
	donaldDuck := DonaldDuck{}

	quack(donaldDuck)

	pointerDonaldDuck := &DonaldDuck{}

	quack(pointerDonaldDuck)

	// Output:
	// Quack!
	// Quack!
}
```

```bash
Ran 0 of 0 Specs in 0.000 seconds                                                              
SUCCESS! -- 0 Passed | 0 Failed | 0 Pending | 0 Skipped                                        
--- PASS: TestSliceInterface (0.00s)                                                           
=== RUN   ExampleQuack                                                                         
--- PASS: ExampleQuack (0.00s)                                                                 
PASS                                                                                           
ok      go-test/interface/slice_interface       0.013s
```

* 하지만 다음과 같이 만약 `DonaldDuck`가 `quack()`을 포인터 리시버로 
  구현한다면 결과는 어떻게 될까요? 

```go
func (donald *DonaldDuck) quack() {
	fmt.Println("Quack!")
}
```

```bash
# go-test/interface/slice_interface [go-test/interface/slice_interface.test]                   
./slice_interface_test.go:6:7: cannot use donaldDuck (type DonaldDuck) as type Duck in argument
 to quack:                                                                                     
        DonaldDuck does not implement Duck (quack method has pointer receiver)                 
FAIL    go-test/interface/slice_interface [build failed]
```

* 위와 같이 에러가 발생합니다.

## Source

* https://github.com/golang/go/wiki/InterfaceSlice
