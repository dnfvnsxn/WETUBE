# MongoDB

- NoSQL의 한 종류
- 더 적은 규칙과 더 적은 절차로 작업이 간으한 데이터베이스
- 만른 Relationship이 필요없는 일반적인 프로젝트를 진행할 때 사용하는 것이 좋음

## 설치

- 다운로드: [MongoDB Community Server](https://www.mongodb.com/download-center/community)
- 우분투 설치

```sh
sudo apt install mongodb-server
```

- 실행

```sh
mongod
mongo
```
```sh
MongoDB shell version v4.0.8
connecting to: mongodb://127.0.0.1:27017/?gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("08120117-c5af-46ec-a5ae-c96d5841943e") }
MongoDB server version: 4.0.8
```

## 자바스크립트와 연결

- **Mongoose**를 통해 연결
- 설치

```sh
npm install mongoose
```

- **dotenv** 
- 코드에 있는 url로 부터 유저 데이터를 보는 것을 원하지 않을 떄 사용
- 데이터베이스를 숨겨 놓기 위해 사용
- 설치

```sh
npm install dotenv
```

- db.js
- mongoose.connect: url 및 configuration
```js
import mongoose, { mongo } from "mongoose"

mongoose.connect(
  "mongodb://localhost:27017/wetube",
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
- init.js에서 연결
- init.js
```js
import "./db";
```

## dotenv 구성
