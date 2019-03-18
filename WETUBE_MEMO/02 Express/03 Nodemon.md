# Nodemon

- 코드가 수정시 서버를 재시작하지 않아도 되도록 도와줌

## NOdemon 설치

- dependencies에 의존하지 않는 패키지 설치 (-D를 추가)
- 프로젝트에 필요한 것이 아닌 개발자에게 필요한 것

```sh
npm install nodemon -D
```

- package.json 수정

```json
  "scripts": {
    "start": "nodemon --exec babel-node index.js"
  }
```

- 저장할 때 마다 서버 새로시작

- 문제: 저장하면 두 번 재시작함
  - 일단 저장하면 재시작하고 babel이 코드의 변화를 감지하고 서버를 재시작
  - package.json 시작 딜레이 추가

```json
"scripts": {
    "start": "nodemon --exec babel-node index.js --delay 2"
  }
```
