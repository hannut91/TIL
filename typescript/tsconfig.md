# tsconfig.json

타입스크립트 설정파일 정리

## Overviw

* 폴더안에 `tsconfig.json`이 있으면 해당 폴더는 `TypeScript`의 
  프로젝트 파일입니다. 
* `tsconfig.json`은 루트 파일들과 컴파일러 옵션들을 정의 합니다. 

## Using tsconfig.json

* input 파일 입력 없이 `tsc`를 실행하면 컴파일러는 `tsconfig.json`을 찾습니다.
* input 파일 입력과 함께 `tsc`를 실행할 경우 `tsconfig.json`은 무시됩니다.

## Examples

* `files`속성으로 작성시에는 다음과 같이 작성합니다. 

```json
{
    "compilerOptions": {
        "module": "commonjs",
        "noImplicitAny": true,
        "removeComments": true,
        "preserveConstEnums": true,
        "sourceMap": true
    },
    "files": [
        "core.ts",
        "sys.ts",
        "types.ts",
        "scanner.ts",
        "parser.ts",
        "utilities.ts",
        "binder.ts",
        "checker.ts",
        "emitter.ts",
        "program.ts",
        "commandLineParser.ts",
        "tsc.ts",
        "diagnosticInformationMap.generated.ts"
    ]
}
```

* `include`와 `exclude` 속성으로 작성시에는 다음과 같이 작성합니다.

```json
{
    "compilerOptions": {
        "module": "system",
        "noImplicitAny": true,
        "removeComments": true,
        "preserveConstEnums": true,
        "outFile": "../../built/local/tsc.js",
        "sourceMap": true
    },
    "include": [
        "src/**/*"
    ],
    "exclude": [
        "node_modules",
        "**/*.spec.ts"
    ]
}
```

## Details

* `compilerOptions`은 생략될 수 있는데, 생략되면 기본 컴파일러옵션이
  사용됩니다. 
* `files`속성은 상대 혹은 절대경로들을 입력받습니다. 
* `include`와 `exclude`속성은 glob-like파일 패턴으로 값을 입력받습니다.
  * `*` 0 혹은 그 이상의 캐릭터들
  * `?` 한 문자와 일치합니다.
  * `**/` 재귀적으로 하위 폴더들과 일치합니다.
* glob패턴의 부분이 `*` 혹은 `.*`만 있다면 지원되는 확장자가있는 파일만
  포함됩니다.
  * .ts, .tsx, .d.ts ...
* `files`와 `include`둘다 없으면 컴파일러는 기본으로 모든 타입스크립트 파일을
  포함합니다.  

## Source

https://www.typescriptlang.org/docs/handbook/tsconfig-json.html
