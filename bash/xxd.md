# xxd 명령어로 hex dump출력하기

파일에서 hex dump를 출력하는 방법

## 정의

* `xxd`명령어는 파일이나 표준 입력으로부터 `hex dump`를 만듭니다.
* 원래의 바이너리형식에서 `hex dump`를 만들수도 있습니다.

### hex dump

* `hex dump`란 컴퓨터의 저장장지에 있는 데이터를 16진법으로 출력하는 방법을
  말합니다.

## 사용법

```bash
xxd [file]
```

## 예제

```bash
xxd example.txt
```

```bash
00000000: 7878 6420 2063 7265 6174 6573 2061 2068  xxd  creates a h
00000010: 6578 2064 756d 7020 6f66 2061 2067 6976  ex dump of a giv
00000020: 656e 2066 696c 6520 6f72 2073 7461 6e64  en file or stand
00000030: 6172 6420 696e 7075 742e 0a              ard input..
```

## 옵션

### -b | -bits

* 결과를 hex가아닌 2진법으로 결과를 출력합니다.

```bash
xxd -b example.txt
```

```bash
00000000: 01111000 01111000 01100100 00100000 00100000 01100011  xxd  c
00000006: 01110010 01100101 01100001 01110100 01100101 01110011  reates
0000000c: 00100000 01100001 00100000 01101000 01100101 01111000   a hex
00000012: 00100000 01100100 01110101 01101101 01110000 00100000   dump 
00000018: 01101111 01100110 00100000 01100001 00100000 01100111  of a g
0000001e: 01101001 01110110 01100101 01101110 00100000 01100110  iven f
00000024: 01101001 01101100 01100101 00100000 01101111 01110010  ile or
0000002a: 00100000 01110011 01110100 01100001 01101110 01100100   stand
00000030: 01100001 01110010 01100100 00100000 01101001 01101110  ard in
00000036: 01110000 01110101 01110100 00101110 00001010           put..
```

### -c | -cols [cols]

* 각 라인에 출력할 바이트 수를 설정합니다.

```bash
xxd -c 4 example.txt
```

```bash
00000000: 7878 6420  xxd 
00000004: 2063 7265   cre
00000008: 6174 6573  ates
0000000c: 2061 2068   a h
00000010: 6578 2064  ex d
00000014: 756d 7020  ump 
00000018: 6f66 2061  of a
0000001c: 2067 6976   giv
00000020: 656e 2066  en f
00000024: 696c 6520  ile 
00000028: 6f72 2073  or s
0000002c: 7461 6e64  tand
00000030: 6172 6420  ard 
00000034: 696e 7075  inpu
00000038: 742e 0a    t..
```

### -e

* hex dump를 리틀 엔디안으로 변경합니다. 
* hex dump값만 변경하고 ASCII표현은 바뀌지 않습니다.

```bash
xxd -e example.txt
```

```bash
00000000: 20647878 65726320 73657461 68206120  xxd  creates a h
00000010: 64207865 20706d75 6120666f 76696720  ex dump of a giv
00000020: 66206e65 20656c69 7320726f 646e6174  en file or stand
00000030: 20647261 75706e69   0a2e74           ard input..
```

### -g | -groupsize [bytes]

* 출력하는 바이트들을 구분해서 출력하는데 몇 개씩 구분해서 출력할 것인지
  설정하는 옵션입니다.
* 기본값은 2입니다.

### -l | -len [len]

* 총 출력할 바이트 수를 정합니다. 입력한 수 까지 출력후 멈추게 됩니다.

```bash
xxd -l 4 example.txt
```

```bash
00000000: 7878 6420                                xxd 
```

### -u

* 출력하는 hex값을 대문자(upper case)로 출력합니다. 기본값은 소문자입니다.

```bash
xxd -u example.txt
```

```bash
00000000: 7878 6420 2063 7265 6174 6573 2061 2068  xxd  creates a h
00000010: 6578 2064 756D 7020 6F66 2061 2067 6976  ex dump of a giv
00000020: 656E 2066 696C 6520 6F72 2073 7461 6E64  en file or stand
00000030: 6172 6420 696E 7075 742E 0A              ard input..
```