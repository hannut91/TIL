# Webpack TypeScript

웹팩에서 타입스크립트 사용하기

## Basic Setup

```bash
npm install --save-dev typescript ts-loader
```

project
```
  webpack-demo
  |- package.json
+ |- tsconfig.json
  |- webpack.config.js
  |- /dist
    |- bundle.js
    |- index.html
  |- /src
    |- index.js
+   |- index.ts
  |- /node_modules
```

tsconfig.json
```
{
  "compilerOptions": {
    "outDir": "./dist/",
    "noImplicitAny": true,
    "module": "es6",
    "target": "es5",
    "jsx": "react",
    "allowJs": true
  }
}
```

webpack.config.js
```javascript
const path = require('path');

module.exports = {
  entry: './src/index.ts',
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: 'ts-loader',
        exclude: /node_modules/
      }
    ]
  },
  resolve: {
    extensions: [ '.tsx', '.ts', '.js' ]
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

## Loader

* 이 예제에서는 `ts-loader`를 사용합니다.

## Source Maps

* 소스 맵을 사용하려면 컴파일 된 JavaScript 파일에 인라인 소스 맵을 출력하도록 
  다음과 같이 `tsconfig.json`을 수정해야 합니다.
 
```
  {
    "compilerOptions": {
      "outDir": "./dist/",
+     "sourceMap": true,
      "noImplicitAny": true,
      "module": "commonjs",
      "target": "es5",
      "jsx": "react",
      "allowJs": true
    }
  }
```

* 이제 웹팩설정에서 source map을 따로 추출하도록 다음과 같이 설정해야합니다.

```javascript
  const path = require('path');

  module.exports = {
    entry: './src/index.ts',
+   devtool: 'inline-source-map',
    module: {
      rules: [
        {
          test: /\.tsx?$/,
          use: 'ts-loader',
          exclude: /node_modules/
        }
      ]
    },
    resolve: {
      extensions: [ '.tsx', '.ts', '.js' ]
    },
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'dist')
    }
  };
```

## Using Third Party Libraries

* 써드파티를 설치할 때 typing definition을 설치해야 합니다.
* 이런 타입들은 [TypeSearch](http://microsoft.github.io/TypeSearch/)에서 찾아
  볼 수 있습니다.
* 만약 `loadsh`를 설치하고 싶다면 다음과 같이 설치할 수 있습니다.

```bash
npm install --save-dev @types/lodash
```

## Importing other Assets

* TypeScript로 다른 코드가 아닌 자원을 사용하기위해 type을 만들어줘야 합니다.
* 그러기 위해서는 custom definition을 만들어줘야 하는데 다음과 같이 만들 수
  있습니다.

custom.d.ts

```ts
declare module "*.svg" {
  const content: any;
  export default content;
}
```

## Source

https://webpack.js.org/guides/typescript/
