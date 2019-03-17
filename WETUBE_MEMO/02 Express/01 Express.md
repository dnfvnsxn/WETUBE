# Express

**Express.js는 프레임워크**

- 프레임워크: 아주 많은 코드로 원하는 작업을 쉽고 빠르게 해낼 수 있도록 만들어 놓은것
- Express.js는 Node.js로 작동하는 프레임워크로 서버 생성을 도와줌
- Django는 파이썬의 프레임워크
- Rails는 Ruby의 프레임워크
- Laravel는 PHP의 프레임워크

## express 설치

- npm을 실행할 때는 꼭 프로젝트 폴데에 package.json이 있는 폴더에서 실행
- 그렇지 않으면 package.json을 또 따른 곳에 생성해버림

```sh
npm install express
```

- node_modules와 package-lock.json 생성
- package.json에 dependency가 추가됨

```json
  "dependencies": {
    "express": "^4.16.4"
  }
```

- dependencies
  - 프로젝트가 생존하는 방식
  - package.json에 dependencies에 express의 버전이 기록
  - node_modules와 package-lock.json가 없어도 package.json이 있는 상태에서 npm install을 하면 필요한 것들을 알아서 설치

```sh
npm install
```
