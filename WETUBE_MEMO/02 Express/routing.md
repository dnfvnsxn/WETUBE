- ES6 JavaScript 모듈
  - 다른 파일의 코드를 우리 코드에 공유(import)
  - app.js에 마지막에 아래오 같은 부분을 추가
  - 누군가 파일을 불러올때 app object를 주겠다는 의미
```js
export default app;
```


- index.js -> init.js
``` json
"scripts": {
  "start": "nodemon --exec babel-node init.js --delay 2"
```

- init.js
```js
import app from "./app";

const PORT = 4000;

const handleListening = () => console.log(`✅ Listening on: http://localhost:${PORT}`);

app.listen(PORT,handleListening);
```
- router
  - route들의 복잡함을 쪼개주는데 사용
- router.js
```!
import express from "express"

export const userRouter = express.Router();

userRouter.get("/", (req,res) => res.send('user index'));

userRouter.get("/edit", (req,res) => res.send('user edit'));

userRouter.get("/password", (req,res) => res.send('user password'));

```
- export default가 아니므로 아래와 같이 import
  - get이 아니라 use 사용
  - user의 의미는 누군가 /user 경로에 접속하면 이 router전체를 사용하겠다는 의미
```js
import {userRouter} from "./router";

app.use("/user",userRouter);
```