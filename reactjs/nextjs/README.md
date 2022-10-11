# Next.js

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
리액트에서 사용하는 `react-dom-route` 의 기능이 녹아 있음. 그냥 내부의 `next/link` 를 임포트하고 `Link` 클래스를 활용할 수 있다. `next/router` 도 마찬가지...

```
import Link from `next/link`;

...

<Link href="/dest">
	<a> ... </a>
</Link>
...
```
단, `Link` 는 href 속성만 가지므로 `title` 과 같은 부가속성을 이용하려면 하부 돔 구조를 이용해야 함.
`href` 의 상대 경로를 사용할 경우 `pages` 디렉토리 하위로 연결됨  


##### 02. 동적 라우팅
파라미터에 따라 URL 을 변경할 수 있다. 가령 `/post/1` 같은 경우, `id` 변수에 따라 연결되는 파일을 핸들링한다. 파일명 규칙은 `[파라미터].js` 이다.

```
<Link href="/post/p/1"> ... </Link>
```
위와 같은 코드가 있으면 물리 파일은 `{prj_dir}/pages/p/[id].js` 로 연결되며 해당 파일 내에서 `id` 값은 `router` 를 통하여 취득할 수 있음

[id].js
```
import { useRouter } from 'next/router';

...

const router = useRouter();
const id = router.query.id;

...

```
예전에는 `this.router.[query | params ].[ variable ]` 같은 방식으로 접근했던 것 같은데 `hooks` 가 적용되면서 변경된 부분인 듯 함 

#### 컴포넌트와 레이아웃

컴포넌트와 레이아웃은 소스의 재사용성을 높이기 위한 컨셉이다.

##### 01. 컴포넌트 
리액트 컴포넌트와 같다. 단, 개인적으로 `components` 라는 디렉토리를 만들어 넣는 것을 좋아한다.(직관성) 

##### 02. 레이아웃
`Nuxt` 에는 `layout` 이라는 디렉토리가 있었던 것 같은데, 여기서는 수동으로 생성해 줘야 한다. `Layout` 클래스를 만들어서 해당 클래스를 사용하는 방법과 `HOC` - Higher Order Component 로 사용하는 방법이 있음.

Making `Layout` component - Define

```
...
const Layout = (props) => {
	...
	return (
    	<div>
        	{props.children}
        </div>
    );
}

export default Layout;
```
Making `Layout` component - Use
```
import Layout from `where/defined`;

...
return (
	<Layout>
    	{ pageContents }
    </Layout>
); 
...

```


Making `HOC` - Define
```
const withLayout = Page => {
	return (
    	<div>
        	<Page />
        </div>
    )
}

export default withLayout;
```

Making `HOC` - Use

```
import withLayout from `where/defined`;
const Page = props => (
	...
)

export default withLayout(Page); 
```


#### 일반 규칙

##### 01. 명명 규칙
아래 규칙은 공홈의 튜토리얼의 규칙을 따름
- 컴포넌트는 파일명과 클래스 이름을 모두 대문자로 시작
- 페이지는 파일명을 카멜케이스지만 클래스 이름은 대문자로 시작 

##### 02. react DOM 특수
- 반복이 될 경우, 하위에 `key` 속성을 주어야 함
- `label` 의 경우, `for` 속성을 사용할 수 없고 `htmlFor` 를 사용해야 함
- `class` 의 경우, `className` 을 사용해야 함 

#### 하위 속성
- Redux[미작성]

#### 자습 노트 
- [day1. express 연동](https://github.com/juneyoung/DEV-INFOS/blob/master/nextjs/study/day1.md)

 #### History
 - 2020.01.28 : 초안 작성


