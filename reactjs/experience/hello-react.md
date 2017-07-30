# HelloWorld 삽질

[react.js 항목으로](https://github.com/juneyoung/DEV-INFOS/tree/master/reactjs)

#### 개요
~~빌어먹을~~ `HelloWorld` 찍기

#### 삽질의 원인

- `react.js` 공식 튜토리얼에 있는 코드를 어디 적용해야 할지 모름

#### 삽질의 과정

- 처음 `npm start` 실행시 나오는 문구는 `App.js` 에 있음
- 당연히 [CodePen](https://codepen.io/gaearon/pen/ZpvBNJ?editors=0010) 에 제공되는 js 를 여기 적용해야 된다고 추정
- 구동시 아래와 같은 에러 발생
- - `'React' must be in scope when using JSX` : 원래 있던 `import React from 'react';` 구문을 붙여넣으니 없어짐
- - `'ReactDOM' is not defined` : 인터넷에서 `import { ReactDOM } from 'react-dom';` 넣으라 해서 넣으니 없어짐. 대신 아래 에러 발생
- - `TypeError: Cannot read property 'render' of undefined` : 위에 추가한 구문에서 ReactDOM 주위의 `{}`를 제거해 줘야 함
- `npm start` 했는데 자꾸 `document.getElementById('root')` 가 `undefined` 라고 에러남 - 하지만 `App.js` 에 있는 구문을 지워도 나서 프로젝트 전체 검색 (`index.js` 에서 찾음)
- `App.js` 원복하고 해당 내용을 `index.js` 로 옮김 : 해결!

#### 남은 의문
- `npm init` 으로 프로젝트 생성시 기본으로 `index.js` 가 시작점이 되는 건 알겠는데, 여기서는 어디서 `index.js` 를 가르키고 있는지 모르겠음
- 시작점이 고정으로 `index.js` 인건지 확인 필요

#### History
- 2017.07.30 : 초안작성