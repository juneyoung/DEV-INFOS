# React.js Tic Tac Toe 따라하기

[react.js 항목으로](https://github.com/juneyoung/DEV-INFOS/tree/master/reactjs)

#### 0. 개요
 react.js 를 사용하는 건 좋지만 알고 써야 제 맛. 공식 홈페이지에 제공되는 예제로 감을 잡아보자. [HelloWorld](https://github.com/juneyoung/DEV-INFOS/blob/master/reactjs/experience/hello-react.md) 에 이은 두 번째 연습. 원본 페이지는 [여기](https://facebook.github.io/react/tutorial/tutorial.html#what-were-building). 
 
 당연히 `A-Z` 같은 가이드는 아니고 개념이 안맞아서 고생했던 부분 위주 정리.
 
#### 1. 시작하기 전에
 현 시점에 이 예제를 따라하는 작성자의 기본 소양 및 요구는 아래와 같았음
 
 - ES6 스펙의 `class` 개념에 대해 전무함. 예전에 js 로 `OO` 를 흉내는 내봤음
 - `setState`, `componentDidMount`, `componentWillMount` 따위의 기본 펑션에 대해 들어본 적 있음
 - `node.js` 는 해봐서 `package.json` 이나 `import`, `export` 에 대해 어렴풋이 알고는 있음
 - `서버 사이드 렌더링` 이나 `react.js` 의 장점에 대해 모르며 공감도 안하고 있음
 - `state` 는 자신, `props` 는 상위로부터 전달받은 요소라고 인지하고 있음
 - `Java` 로얄리스트 : 자바가 짱이라고 생각함
 - [ 요구 1 ] : 당연히 `class` 라면 용도별로 분리되어야 함
 - [ 요구 2 ] : `Component` 가 모듈이라면 당연히 각 모듈은 독립적이어야 함

#### 2. 공부방법

 완성한 시점에 아래와 같은 공부 방식이 도움이 되었던 것 같다. 공홈 가이드는 진짜 `quick glance` 같은 느낌이라서 여러모로 마음에 들지 않았다. 나만의 방식으로 변경하는 부분에서 나와있지 않은 에러도 많이 마주쳤고 그래서 더 개념 잡는데 도움이 된 듯. 추천함 :+1:

- 가이드 읽기
- 상식 + 가이드로 구현
- 디버깅

#### 3. `import` / `export` 구문

 공홈에서 제공되는 소스는 각 1 개의 `js`, `css`, `html` 로 구성되어 있다. 특히 개인적으로 마음에 들지 않았던 부분은 하나의 js 에 각기 다른 기능을 하는 `class` 가 3개나 들어가 있는 부분이었고, `import` 구문과 `export` 구문을 사용해서 해결할 수 있었다.
 
- `import` : `import` 구문은 `js`  파일의 최상단에 위치하며 아래와 같은 형식으로 사용될 수 있다. 선언이 된 경우, `render` 같은 펑션에서 `<[클래스명]></[클래스명]>` 으로 사용가능
```
// 파일경로는 문자열로, 클래스명은 변수처럼 그냥 쓰면 됨
import [클래스 명] from '[파일 경로]'
```

좀 더 구체적 예시를 들자면 `import Board from './vo/board.js'` 같은 식이다. 파일 확장을 생략하면 곤란함

이렇게 구현을 했는데 `[클래스 명] is not defined` 라고 에러메세지가 출력되는 경우(구체적으로는 `export`/`import` 구문을 체크하라는 메세지가 나옴)는 import 된 파일의 `export` 구문을 의심해 볼 수 있음

- `export` : `export` 을 사용해서 현재 파일에 정의된 클래스를 다른 파일과 공유할 수 있다. 위의 예시에 연장을 하자면 이 `export` 구문은 `board.js` 파일에 들어가야 한다.

`export` 선언 방식 1 : 클래스의 선언부에서 사용
```
export default class Board extends React.Component {
	... 중략
}
```

`export` 선언 방식 2 : 클래스 파일의 마지막에 아래와 같이 사용

```
// class 선언 밖 최상위 레벨에서 
export default Board;
```


#### 4. `render` 함수

`render` 의 `return` 구문은 반드시 함수 형태로 반환되어야 한다. 만약 별다른 에러가 없는데 출력이 되지 않는다면 의심해 볼만 하다.

잘못된 예 :
```
render () {
	return 
    	<div className = 'game-borad'>
        	<Board />
        </div>
}
```

정상 :
```
render () {
	reutrn (
    	<div className = 'game-board'>
        	<Board />
        </div>
    )
}
```

#### 5. `function` 의 선언

예제 중간에 `Square` 클래스를 `function` 으로 변경하는 부분이 나온다. 파일을 `game.js`, `board.js`, `square.js` 로 나눴다면, 해당 펑션을 어디다 놓아야 할지 난감하다.

1. 상위 클래스 선언 아래에 넣은 경우 (X) : function 키워드를 사용할 수 없음. 예제에서는 펑션 선언 후, `<Square />`  와 같은 방식으로 사용하고 있는데, 이 방식으로는 사용할 수 없음 
```
class Board extends React.Component {
	// function 키워드를 사용할 수 없음
    Square (props) {
      return (
          <button className='square' onClick={props.onClick}>
              {props.value}
          </button>
      )
	}
}
```
2.  파일의 `전역` 영역 (O) : `class` 선언과 동일한 레벨에 올려두면 `<Square/>` 로 참조 가능함
```
function Square (props) {
	return (
		<button className='square' onClick={props.onClick}>
			{props.value}
		</button>
	)
}

export default class Board extends React.Component {
	... 중략 ...
}
```

#### 98. 참고 프로젝트
- [비트버킷](https://bitbucket.org/juneyoung/react_practice) : 파일 분리 버전 20170805

 
#### 99. History
- 20170805 : 초안 작성
