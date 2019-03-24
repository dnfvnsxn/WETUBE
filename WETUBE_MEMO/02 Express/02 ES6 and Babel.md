# Babel

- 최신의 자바스크립트 코드를 무난한 예전의 자바스크립트 코드로 변환해줌
- example

```js
const something = (a, b) => a * b;
```

위의 코드를 아래의 코드로 변환

```js
var something = function something(a, b) {
  return a * b;
};
```

## Babel를 사용하는 방법

- Babel을 사용하는 방법은 다양함(많은 Loader가 존재)

  - Babel node를 사용하는 방법

  ```sh
  npm install @babel/node
  ```

- Babel에는 많은 stage가 존재

  - 실험적이지 않으면서 안정적 (env)

  ```sh
  npm install @babel/preset-env
  ```

## .babelrc

- node.js와 JS와 관련된 모든 설정을 저장하는 문서
- Babel이 실행되기전 이 파일을 찾아보게 됨
- .babelrc

```json
{
  "presets": ["@babel/preset-env"]
}
```

- babel 동작 테스트: JS 최신 문법으로 전환
- index.js

```js
import express from "express";
const app = express();

const PORT = 4000;

const handleListening = () =>
  console.log(`Listening on: http://localhost:${PORT}`);

const handlehome = (req, res) => res.send("Hello from home");

const handleProfile = (req, res) => res.send("You are on my profile");

app.get("/", handlehome);
app.get("/profile", handleProfile);

app.listen(PORT, handleListening);
```

- package.json 전환

```json
"scripts": {
    "start": "babel-node index.js"
  }
```

- npm start 실행시 @babel/core를 찾을 수 없음

```sh
npm install @babel/core
```

- 실행

```sh
npm start
```