# MVC
  - M(Model)   : data -> batabase
  - V(View)    : how does the data look -> template
  - C(Control) : function that looks for the data
- MVC는 패턴, 구조

## router 분리
- app.js
```js
import express from "express";
import morgan from "morgan";
import helmet from "helmet";
import bodyParser from "body-parser";
import cookieParser from "cookie-parser";
import userRouter from "./routers/userRouter"
import videoRouter from "./routers/videoRouter"
import globalRouter from "./routers/globalRouter"

const app = express();

app.use(cookieParser());
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(helmet());
app.use(morgan(("dev")))

app.use("/",globalRouter);
app.use("/users",userRouter);
app.use("/videos",videoRouter);


export default app;
```
- userRouter.js
```js
import express from "express"

const userRouter = express.Router();

export default userRouter
```
- videoRouter.js
```js
import express from "express"

const videoRouter = express.Router();

export default videoRouter
```
- globalRouter.js
```js
import express from "express"

const globalRouter = express.Router();

export default globalRouter
```

## Controller
- 보통 프로젝트에 있는 각 모델마다 컨트롤러를 만들게 됨
- 컨트롤러는 어떤일이 어떻게 발생하는지에 관한 로직


## 구조정리
- init.js에는 app.js에서 import 한 application이 있음
- application에 관한 코드들은 app.js에 담겨 있음
    - express를 import
    - express를 실행한 결과를 app상수로 만듬
    - middleware 추가
- 3개의 router 사용
  - 주소들은 모두 routes.js에 정의
    - 한파일이 바뀌면 모두 적용되도록 함
  - globalRouter: 각 URL이 포함
    - /home
    - /search
    - /join
    - /login
    - /logout
  - userRouter: /user/의 주소들
  - videoRouter
- router의 로직들은 모두 userController나 videoController에 정의
  - 로직은 모두 함수들
  - 이부분이 MVC의 C부분 