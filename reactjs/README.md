# React.js

[메인으로](https://github.com/juneyoung/DEV-INFOS)

#### 개요

사내 주요 언어가 `Java` 에서 `js` 로 바뀌면서 공부하게 된 `react.js` 의 특징을 정리

#### 하위 페이지
- [nextjs](https://github.com/juneyoung/DEV-INFOS/tree/main/reactjs/nextjs/README.md)
- [redux](https://github.com/juneyoung/DEV-INFOS/tree/main/reactjs/redux/README.md)

#### 준비물
- node.js
- npm
- create-react-app
- bzip2 (CentOS) 

#### 설치하기

```
$ > sudo npm install -g create-react-app
$ > create-react-app projectA
```
 `create-react-app` 이 내부에 필요한 `package.json` 등을 다 만들기 때문에 별도의 작업이 필요없다.

 일반적으로 프로젝트를 폴더를 생성하고 `git` 새팅을 하고 `react` 를 시작하는데, 이 경우 쓸데없이 디렉토리 뎁스가 증가한다. `create-react-app` 으로 앱을 만든 경우, 생성 후 앱폴더 내에서 `git` 새팅하자.
 
 안좋은 예 :
 ```
 # 이 경우, git root 경로는 ./projectA 이지만, 앱의 루트는 ./projectA/projectA 이다
 $ > mkdir projectA && cd projectA
 $ > git init
 $ > create-react-app projectA
 ```
 수정 :
 ```
 # git 루트와 앱 루트가 일치
 $ > create-react-app projectA
 $ > cd projectA && git init
 ```
#### 구동
 여기서부터는 일반 `node.js` 앱과 동일하다. `package.json` 내에 정의된 명령을 `npm ${명령어}` 형식으로 실행할 수 있음.
 ```
 # 기본 포트는 3000
 $ > npm start 
 ```
 
 #### 경험
 - [HelloWorld](https://github.com/juneyoung/DEV-INFOS/blob/master/reactjs/experience/hello-react.md) : 어디서부터 시작해야 되나?
 - [Tic Tac Toe](https://github.com/juneyoung/DEV-INFOS/blob/master/reactjs/experience/tic-tac-toe.md) : 기초 쌓기
 - [Kaban Board](https://github.com/juneyoung/DEV-INFOS/blob/master/reactjs/experience/kanban.md) : 프로리액트,위키북스,2016
 
 #### History
 - 2017.07.30 : 초안 작성
 - 2017.08.05 : tic tac toe 예제 추가

