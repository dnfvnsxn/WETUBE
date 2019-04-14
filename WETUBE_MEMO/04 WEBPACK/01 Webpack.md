# Webpack

- module bundler
- 많은 파일들을 가져와서 webpack에게 주면, webpack은 그것들이, 완전히 호환이 되는 static 파일들로 변환

## 설치

```sh
npm install webpack webpack-cli
npm install cross-env
npm install @babel/polyfill
```

- webpack: webpack 파일에서 webpack을 사용하기 위함
- webpack-cli: 터미널에서 webpack을 쓸 수 있게 함

## package.json 설정 변경

- package.json에서 아래 부분을 삭제

```json
"scripts": {
    "start": "nodemon --exec babel-node init.js --delay 2"
}
```

- 이제 실행시 `npm start` 사용하지 않음
- `npm run dev:server`와 `npm run dev:assets`로 각자 다른 콘솔에서 실행
- dev:assets: webpack을 불러오도록 설정
  - webpack은 자동으로 webpack.config.js 파일을 찾음
  - `WEBPACK_ENV=development` 모드 설정
- build:assets: 코드를 서버에 올려줌
- package.json 아래와 같이 수정
```json
"scripts": {
    "dev:server": "nodemon --exec babel-node init.js --delay 2",
    "dev:assets": "cross-env WEBPACK_ENV=development webpack -w",
    "build:assets": "WEBPACK_ENV=production webpack"
}
```
## webpack.config.js 생성
- 기본적인 규칙: webpack은 exported configuration object를 찾음
- config 파일은 server 코드와는 연관시키지 않음, 100% client code
- babel node를 사용할 수 없으므로 예전 자바스크립트 코드로 작성
- webpack은 entry와 output를 가지고 있음
  - entry: 파일들이 어디에서 왔는가? 
  - output: 그것 어디에 넣을 것인가?
- assets폴더 생성
```sh
└─ assets
    ├─ js
    │   └─main.js
    └─ scss
        └─ styles.scss 
```
- main.ja
```js
import "../scss/styles.scss"
```
- styles.scss
```scss
body {
    background-color: red;
}
```
- webpack.config.js
```js
const path = require("path");
const autoprefixer = require("autoprefixer");
const ExtractCSS = require("extract-text-webpack-plugin");

const MODE = process.env.WEBPACK_ENV;
const ENTRY_FILE = path.resolve(__dirname, "assets", "js", "main.js");
const OUTPUT_DIR = path.join(__dirname, "static");

const config = {
    entry: ["@babel/polyfill", ENTRY_FILE],
    mode: MODE,
    module: {
        rules: [
            {
                test: /\.(js)$/,
                use: [
                    {
                        loader: "babel-loader"
                    }
                ]
            },
            {
                test: /\.(scss)$/,
                use: ExtractCSS.extract([
                    {
                        loader: "css-loader"
                    },
                    {
                        loader: "postcss-loader",
                        options: {
                            plugins() {
                                return [
                                    autoprefixer({ browsers: "cover 99.5%" })
                                ];
                            }
                        }
                    },
                    {
                        loader: "sass-loader"
                    }
                ])
            }
        ]
    },
    output: {
        path: OUTPUT_DIR,
        filename: "[name].js"
    },
    plugins: [new ExtractCSS("styles.css")]
};

module.exports = config;

```
- path: Node.js에 기본으로 설치되어있는 패키지
  - __dirname은 현재 프로젝트 디렉토리, 어디서든 접근 가능한 Node.js 전역변수
## rules 지정
- webpack이 module을 만났을 때 따르는 규칙
- rules 는 config라는 object안의 array
- 확장자가 scss인 파일을 만날때 마다 어떤 loader를 실행하도록 지정
- loader랑 webpack에게 파일을 처리하는 방법을 알려줌
- 먼저 condition을 test하여 scss인지 알아봄, 정규식 사용 
```js 
test: /\.(scss)$/
```
- scss파일을 찾았을 떄는 css로 바꾸고, 전체 텍스트 중 css 텍스트로 추출하고 추출된 css를 분리된 하나의 파일로 만듬
- extract-text-webpack-plugin 설치
- loader 설치
- autoprefixer 설치
- node-sass 설치
```sh
npm install extract-text-webpack-plugin@next
npm install css-loader postcss-loader sass-loader
npm install autoprefixer
npm install node-sass
npm install babel-loader
```
```js
module: {
    rules: [
        {
            test: /\.(scss)$/,
            use: ExtractCSS.extract([
                {
                    loader: "css-loader"
                },
                {
                    loader: "postcss-loader",
                    options: {
                        plugin() {
                            return [
                                autoprefixer({ browsers: "cover 99.5%" })
                            ];
                        }
                    }
                },
                {
                    loader: "sass-loader"
                }
            ])
        }
    ]
}
```
- module을 발견할 때마다 test하여 scss로 끝나는 module을 만나면 ExtractCSS plugin을 사용 하여 일반적인 css로 통역
