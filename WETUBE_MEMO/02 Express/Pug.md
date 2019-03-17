- Pug(view engine)
```!
npm install pug
```
- expressjs의 공식문서를 보면 설정해야할 부분은 set 함수
  - set함수는 name과 value가 필요
  - application의 설정을 하는 함수
- app.js에서 view engine의 설정을 pug로 바꿀것
  - 이후 확장자가 pug인것을 찾게됨
```js
app.set('view engine',"pug");
```
- view 설정을 변경하고 싶다면 application의 화면이 담긴 디렉토리나 디렉토리의 배열을 입력하면 됨
  - 기본 값은 포로젝트 디렉토리 + 'view'
  - view안에 템플릿을 만들게됨
- pug는 템플릿 언어(express의 vire engine)
  - pug는 html이 더 아름답게 보이도록 만들어줌
- views아래에 layouts 폴더를 만들고 layout을 만들어 html,css의 단순반복잡업을 피함
- main.pug
```pug
doctype html
html
    head
        title Wetube
    body
        header
            h1 Wetube
        main
            block content
        footer
            span &copy; Wetube

```
- home.pug
```pug
extends layouts/main

block content
    p Hello
```

- partials: 페이지의 일부분

- 템플릿에 정보를 추가
- 컨트롤러에 있는 정보응 템플릿에 추가 
- locals에 로컬 변수를 저장하면, 이 변수들을 템플릿에서 사용할 수 있음 
    전역적으로 사용항 수 있는 변수를 추가하는 방법임 
```js
import routes from "./routes";

export const localsMiddleware = (req, res, next) =>{
    res.locals.siteName = 'Wetube';
    res.locals.routes = routes;
    next();
};
```