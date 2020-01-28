# React.js

[메인으로](https://github.com/juneyoung/DEV-INFOS)

#### 개요

SPA 와 SSR - 기존의 `react.js` 방식으로 SPA 를 구현하기 수월하지만 SEO 에 난점이 있음. 그래서 MPA 을 만들 수 있도록 지원하는 프레임워크가 나옴 - `Next.js`

테스트 및 작성은 OSX 에서 하였음

#### 준비물
- node.js
- npm

#### 설치하기

[공식 사이트](https://nextjs.org/)에 따르면 `create-react-app` 보다 `nodejs` 로 시작해서 변경하는 방식으로 권장됨

```
$ > mkdir your_prj
$ > cd your_prj
$ > npm init -y
```
노드 프로젝트 생성 이후, react 와 next 관련 설정을 해줘야 함
```
$ > npm i --save react react-dom next
$ > mkdir pages
```
`pages` 디렉토리는 next 에서 페이지 라우팅을 처리하기 위한 내장 디렉토리이며 일종의 예약 디렉토리이다. `Vue` 진영의 `Nuxt` 의 `pages` 와 동일함

아래와 같이 `package.json` 에 기동 스크립트를 추가해 줘야 함

```
"scripts" : {
	"dev" : "next",
	"build" : "next build",
    "start" : "next start"
}
```
기동 준비가 완료되었고 `npm run dev` 로 기동이 가능 - 진입점은 최상위의 `index.js`

#### 라우팅

##### 01. 정적 라우팅
작성 중 ...

##### 02. 동적 라우팅
작성 중 ...

#### 컴포넌트와 레이아웃

##### 01. 컴포넌트 

##### 02. 레이아웃


#### 일반 규칙

##### 01. 명명 규칙
아래 규칙은 공홈의 튜토리얼의 규칙을 따름
- 컴포넌트는 파일명과 클래스 이름을 모두 대문자로 시작
- 페이지는 파일명을 카멜케이스지만 클래스 이름은 대문자로 시작 

#### 하위 속성
- Redux[미작성]


 #### History
 - 2020.01.28 : 초안 작성


