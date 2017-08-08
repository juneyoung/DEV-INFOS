# KanbanBoard 예제

[react.js 항목으로](https://github.com/juneyoung/DEV-INFOS/tree/master/reactjs)

#### 0. 개요
`프로리액트(위키북스), 2016`  책의 칸반보드 예제를 바탕으로 작성하였음. 최신 기술이다보니 `Deprecated` 된 부분, 변경된 부분을 기록함.

#### 1. 초기화 방식의 변경
책에서 안내되고 있는 방식은 

1. `npm init`
2. `package.json` 수정.
```
{
	"name" : "app"
    , "version" : "0.0.1"
    , "description" : ""
    , "author" : "owner"
    , "devDependencies" : {
    	"babel-core" : "^5.8.*"
        , "babel-loader" : "^5.3.*"
        , "webpack" : "^1.12.*"
        , "webpack-dev-server" : "^1.10.*"
    }
    , "dependencies" : {
    	"react" : "^0.13.*"
    }
    , "scripts" {
    	"start" : "node_modules/.bin/webpack-dev-server --progress"
    }
}
```
3. `webpack.config.js` 수정 
```
module.exports = {
	entry : [
    	'./source/App.js'
    ]
    , output : {
    	path : __dirname
        , filename : 'bundle.js'
    }
    , module : {
    	loaders : [
        	{
            	test: /\.jsx?$/
                , loader : 'babel'
            }
        ]
    }
}
```

상기와 같은 절차에 따라 처리되고 있다. 

`20170807` 시점에는 `create-react-app {앱이름}` 명령 한줄로 간단하게 초기화할 수 있음.


#### 2. `React.render`, `registerServiceWorker`
이 부분은 `index.js` 파일을 기준으로 함. 
- 기존에 `React.render` 로 사용되던 부분이 `ReactDOM.render` 로 변경되었음. 사용법은 동일함.
- `registerServiceWorker`라는 펑션이 추가 되었음. [서비스워커](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers?hl=ko)

#### 3. `render` 함수 내에서 `jsx` 반환
 책에는 나와있지 않은 부분으로 `return` 구문 다음 개행이 있으면 인식을 하지 못하는 문제가 있음
```
let cards = this.props.cards.map((card) => {
	// return 다음에 줄 넘겨쓰면 인식 못함 
	return  <Card id={card.id}
				key={card.id}
				title={card.title}
				color={card.color}
				description={card.description}
				tasks={card.tasks}/>;
});
```
 
#### 4. `constructor` 주의사항
- `constructor`는 반드시 `super()` 로 시작(생략 불가능)
- `super` 를 생략한 경우, `super` 가 없다는 메세지가 아니라 다음 구문이 이 자리에 올 수 없다는 식의 메세지가 출력됨

```
constructor () { 
	/*
		- constructor 에 반드시 super() 로 시작해야 함
		- super() 를 호출하지 않은 경우에는 여기에 this 스테이트먼트를 사용할 수 없다는 메세지 출력됨  
		- 여기에서 state 를 명시하지 않으면 this.state 를 참조할 수 없다(자체가 내장은 아니다)
	*/

	super();
	this.state = {
		fileName : 'KanbanBoard'
	}
}
```

#### 5. 템플릿 문자열(`${}`) 사용
`ES6` 기준에서는 템플릿 문자열을 반드시 백쿼트-백틱- 으로 둘러야 한다. 싱글쿼트 혹은 더블쿼트 사용 시에는 아래와 같은 경고 메세지 출력

```
Unexpected template string expression no-template-curly-in-string
```

#### 6. `PropTypes` 의 패키지가 변경

책의 예제는 `import Proptypes from 'react'` 로 사용하고 있는데 `v15` 이후부터 `PropTypes` 를 메인에서 가져오는 방식이 `deprecated` 되었다.

- `npm install --save prop-types`
-  사용할 때는 `import PropTypes from 'prop-types'` 로 사용한다.

#### 98. References
- [KanbanBoard 비트버킷](https://bitbucket.org/juneyoung/kanbanboard) 

#### 99. History 
- 20170808 : 초안작성 (~ `p.75`) 
