- first express
    - require: node module을 어딘가에서 가져오는 것
      - 이경우는 express라는 이름의 폴더를 내 파일들 속에서 찾으려고 할 것
      - 없다면 node_modules 안의 express 폴더안의 index.js를 찾음
    - application 생성
      - const로 선언한 변수 app에 express를 실행해서 담음
    - localhost:4000 으로 서버 생성
    - 실행은 node index.js
```js
const express = require('express');
const app = express();

app.listen(4000);
});
```
- npm을 이용한 실행
package.json에 아래와 같이 추가
```json
"scripts":{
    "start": "node index.js"
  }
```
npm start로 실행가능
  
- 4000포트로 서버생성후 서비가동시 실행되는 콜백함수 추가
```js
const express = require('express');
const app = express();

const PORT = 4000;

function handleListening(){
    console.log(`Listening on: http://localhost:${PORT}`)
}

app.listen(PORT,handleListening);
```
- 기본적인 작동방식: 서버를 생성하고 route를 생성하고 그것에 응답하는 방식
- [GET과 POST](https://hongsii.github.io/2017/08/02/what-is-the-difference-get-and-post/)
  - HTTP는 웹상에서 클라이언트와 서버 간에 요청/응답으로 데이터를 주고 받을 수 있는 프로토콜
  - GET: 서버로부터 정보를 조회하기 위해 설계된 메소드
    - GET은 요청을 전송할 때 필요한 데이터를 Body에 담지 않고, 쿼리스트링을 통해 전송
    - GET request로는 정보를 전달할 수 없음
  - POST: 리소스를 생성/변경하기 위해 설계
    - 전송해야될 데이터를 HTTP 메세지의 Body에 담아서 전송
  - 서버의 응답은 2개의 object
    - request object
    - response object
```js
function handlehome(req,res){
    res.send("Hello from home");
}

app.get("/",handlehome);
```

