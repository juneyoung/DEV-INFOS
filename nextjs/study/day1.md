# Next.js - day1

[메인으로](https://github.com/juneyoung/DEV-INFOS)

#### 요약

Next.js 에 페이지 이외의 요청(Restful API)도 처리할 수 있도록 분기한다. 9 버전부터는 별도로 express 를 사용하지 않고 처리가 가능하다고 하는데 신규 개발보다는 진행하고 있는 프로젝트나 유지보수 쪽으로 나갈 상황이 많을 것 같아 기존의 방식을 찾아서 공부함

#### 준비물
- next.js
- express.js - `yarn add express`

#### 01. 애플리케이션 시작점 작성하기

`server.js` 를 최상단에 생성한다. `src` 디렉토리 하위같은 곳에 생성해도 무관하지만 `package.json` 의 `scripts` 항목에서 참조해야 하니 경로가 간결한 것이 좋다

최초의 `server.js`

```
const express = require('express');
const next = require('next');

const devFlg = 'dev' === (process.env.NODE_ENV || 'dev');
const port = process.env.PORT || process.env.port || '3000';

const App = express();
const NextApp = next({
    devFlg, // Boolean value that defines dev mode or not
    quiet: devFlg,
    dir: '.', // Next project root dir, which has .next as a sub dir
    conf: { // Related to next.config.js
        webpack: {}
    }
});
const NextHandler = NextApp.getRequestHandler();
const NextRouter = express.Router();

NextRouter.get('*', (req, res) => {
    NextHandler(req, res);
});

NextApp.prepare()
    .then(() => {
        App.use('/', NextRouter);

        App.listen(port, err => {
            if(err) {
                console.error('Failed to activate the server on port : ', port, err);
            } else {
                console.log(`The server is listening on ${port}`);
            }
        })
    });
```
- `next` 가 자동으로 해주는 부분을 수동으로 변경함
- `next` 펑션에 넥스트 설정을 넣고, express 에는 포트나 미들웨어를 넣음
- `NextApplication` 객체에 `express.Router` 를 설정
- 최종적으로는 `NextApplication` 으로 `Express Application` 을 감싼 모양새

#### 02. `package.json` 에 변경 알려주기

기존의 `next` 명령어로 시작하던 부분을 `node` 명령어로 변경하였다

```
"scripts" : {
	// "dev" : "next",
    "dev" : "node server.js"
}
```
`cross-env` 나 `dotenv` 는 추후 확장하면서 다룰 예정

#### 03. 변경된 구조로 기동

기존에 `npm run dev` 로 하면 빌드하라고 오류가 난다.
```
$ > yarn build && yarn dev
```

#### 04. 라우터 추가하기

신규로 라우터 파일을 작성하고 `sever.js`에서 `Express Application` 으로 설정할 수 있다.

추가되는 항목
```
const ApiRouter = require('./routes/ApiRouter');

NextApp.prepare()
	.then(() => {
    	app.use('/api', ApiRouter);
    	app.use('/', NextRouter);
        app.listen(port, ... );
    })
```
- *주의점* 조건 검사 상, 서브 URL 을 가진 라우터가 전체 라우터보다 위로 와야 함

/routes/ApiRouter.js
```
const express = require('express');
const router = express.Router();
router.get('/', (req,res,nxt) => res.json({ result : 'success' }));
module.exports = router;
```


#### 98. 주의점

module 의 import, export 가 달라 혼동이 올 수 있다.

import
```
// react style => ClassName
import ApiRouter from './routes/ApiRouter';

// node style => FileName
require('./routes/ApiRouter');
```

export 
```
// react style #1
const ApiRouter = ...
export default ApiRouter;

// react style #2
export default [function | class] {
	...
}

// node style => FileName
const ApiRouter = ...
module.exports = APiRouter; // but export as file name
```
node 스타일에서 [이렇게](https://stackoverflow.com/questions/16631064/declare-multiple-module-exports-in-node-js) 한개 파일에서 여러개를 `exports` 가 가능하다고 함


#### 99. History
 - 2020.01.29 : 초안 작성


