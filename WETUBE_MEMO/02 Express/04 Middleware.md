# Middleware

## express에서의 middleware

처리가 끝날 때까지 연결되는 있는 것

- 어떻게 연결이 시작되는가(request는 어떻게 시작되는가)
  - 시작은 브라우저, 웹사이트에 접속하려고 할때가 시작
  - index.js파일 실행
  - 우리의 application이 route가 존재하는지 살펴봄
  - home을 요청하는 것을 확인 후 handlehome이라는 함수를 실행
  - handlehome은 응답을 전송
- index.js

```js
app.get("/", handlehome);
```

- middleware
  - 보통 연결의 흐름은 간단하지 않고 유저와 마지막 응답사이에 무엇인가 존재하는 것이 middleware
  - 유저가 home(/)을 요청하고 handlehome으로 응답하는 사이에 middleware 생성
  - 문제는 구글 크롬으로부터 온 요청을 계속처리할지에 대해 권한을 주지 않아 무한로딩
- index.js

```js
const betweenhome = (req, res, next) => console.log("between");

app.get("/", betweenhome, handlehome);
```

- key 사용

  - express의 모든 route와 connection을 다루는 것들은 request, response, next를 가지고 있음
  - next가 handlehome을 호출

- index.js

```js
const betweenhome = (req, res, next) => {
  console.log("between");
  next();
};
app.get("/", betweenhome, handlehome);
```

## middleware 사용 예시

- 유저의 로그인 여부 확인
- 파일 전송중 중간에서 가로채기
- 로그 작성
- 특정 IP 차단

## 모든 route에 middleware 적용

- 웹사이트에서 일어나는 모든 것에 대해 middleware사용
- 순서가 중요 -> 접속이 있을떄 위에서 아래로 실행
- index.js

```js
app.use(betweenhome);

app.get("/", handlehome);

app.get("/profile", handleprofile);
```

- middleware가 연결을 끊을 수 있음
- middleware가 res.send를 실행하는 함수를 발동하면 연결 끊어짐

## 다양한 middleware

### morgan

- logging에 도움을 줌
- 어디서 무슨일이 일었났는지 기록

```sh
npm install margan
```

- middleware 추가
- tiny, combined, common, dev 등의 로깅 옵션이 존재
- index.js

```js
import morgan from "morgan";
app.use(morgan("dev"));
```

### halmet

- node.js 보안을 위한 것
- application이 안전하도록 만들어줌

```sh
npm install helmet
```

- middleware 추가
- index.js

```js
import helmet from "helmet";

app.use(helmet());
```

### cookie-parser, body-parser

**서버가 유저로부터 받은 데이터를 이해하는 방법**
**유저로부터 받은 cookie를 이해하는 방법**

- cookie parser
  - cookie 다루는 것을 도와줌
  - cookie를 전달받아서 사용할 수 있도록 만들어주는 미들웨어
  - 사용자 인증 같은 곳에서 쿠키를 검사할 떄 사용
- body parser
  - body 다루는 것을 도와줌
  - 사용자가 웹사이트로 전달하는 정보들을 검사하는 미들웨어
  - request 정보에서 form이나 json형태로 된 body를 검사
- 누군가가 form을 전송한다면 서버에 의해 특정한 형태로 받아져야 함
- body-parser는 그 데이터를 가지고 있는 request object에 접근을 도와줌
- cookie는 유저 정보를 저장

```sh
npm install body-parser
npm install cookie-parser
```

- middleware 추가
- index.js

```js
import bodyparser from "body-parser";
import cookieparser from "cookie-parser";

app.use(cookieparser());
app.use(bodyparser.json());
app.use(bodyparser.urlencoded({ extended: true }));
```
