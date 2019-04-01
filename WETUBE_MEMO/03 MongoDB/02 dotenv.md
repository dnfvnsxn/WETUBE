# dotenv
- .env 생성
- PORT 변수에는 ;를 붙이지 않음
- .env
```env
MONGO_URL="mongodb://localhost:27017/wetube";
PORT=4000
```
- .env의 정보 접근
- dotenv.config 함수 사용
- db.js

```js
import mongoose, { mongo } from "mongoose"
import dotenv from "dotenv";

dotenv.config(); 

mongoose.connect(
  process.env.MONGO_URL,
  {
    useNewUrlParser:true,
    useFindAndModify: false
  }
);

const db = mongoose.connection;

const handleOpen = () => console.log("✅ Connected to DB");
const handleError = () => console.log("❌ Error on DB Connection:${error}")

db.once("open",handleOpen)
db.on("error",handleError)
```
- init.js
```js
import "./db";
import app from "./app"
import dotenv from "dotenv";
dotenv.config();

const PORT = process.env.PORT || 4000;

const handleListening = () => console.log(`✅Listening on http://localhost:${PORT}`);

app.listen(PORT, handleListening);
```