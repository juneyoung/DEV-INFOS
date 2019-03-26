[![npm][npm]][npm-url]
[![deps][deps]][deps-url]
[![test][test]][test-url]
[![coverage][cover]][cover-url]
[![chat][chat]][chat-url]

<div align="center">
  <a href="https://webpack.js.org/">
    <img width="200" height="200" vspace="" hspace="25" src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon-square-big.svg">
  </a>
  <h1>thread-loader</h1>
  <p>로더들의 워커 풀에서 기동할 수 있도록 지원.</p>
</div>

<h2 align="center">Install</h2>

```bash
npm install --save-dev thread-loader
```

<h2 align="center">Usage</h2>

thread-loader 를 다른 로더들의 앞에 배치해야 함. 그래야 이후에 기술된 로더들이 워커 풀에서 작동함.

워커풀로 로더를 사용하는데에는 몇가지 제약이 있음. 예를 들면:

* 로더들을 파일을 변경/생성(emit)할 수 없음.
* 로더들은 커스텀 로더 API 를 사용할 수 없음. (예. plugins )
* 로더들은 웹팩 options 에 접근할 수 없음.

각각의 워커는 최대 600ms 오버헤드를 가지는 별도의 node.js 프로세스로 기동됨. 또한 인터프로세스 커뮤니케이션을 위한 추가 오버헤드를 가질 수 있음.

thread-loader 를 고비용 작업에서만 사용하시오!

<h2 align="center">용례</h2>

**webpack.config.js**

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        include: path.resolve("src"),
        use: [
          "thread-loader",
          // your expensive loader (e.g babel-loader)
        ]
      }
    ]
  }
}
```

**with options**

```js
use: [
  {
    loader: "thread-loader",
    // loaders with equal options will share worker pools
    options: {
      // 생성될 워커의 수, 기본값은 cpu -1 임
      // require('os').cpus() 가 undefined 일 때 자동으로 1로 새팅됨
      workers: 2,

      // 워커프로세스에서 병렬로 처리될 작업의 수.
      // 기본값은 20
      workerParallelJobs: 50,

      // 워커프로세스에서 사용할 node 명령어의 옵션
      workerNodeArgs: ['--max-old-space-size=1024'],
      
      // 죽은 워커 재생성 여부
      // 재생성은 전체 컴파일을 느리게 할 수 있음
      // development 에서는 반드시 false 로 새팅되어야 함
      poolRespawn: false,
      
      // idle 상태의 워커를 죽일 대기시간
      // 기본값 500 (ms)
      // 빌드를 체크하기 위해서 워커를 살려두려면 Infinity 로 새팅하면 됨
      poolTimeout: 2000,
      
      //  number of jobs the poll distributes to the workers
      // 기본값은 200
      // 효율성을 조금 떨어뜨리지만 공평하게 작업이 분배됨
      poolParallelJobs: 50,

      // 워커 풀의 이름
      // 풀을 구분할 수 있는 식별가능한 옵션
      name: "my-pool"
    }
  },
  // your expensive loader (e.g babel-loader)
]
```

**prewarming**

워커를 시작할 때 지연이 생기는 것을 방지하기 위해 워커풀을 미리 웜업 해둘 수 있음

이 작업은 풀에 지정된 최대 수의 워커를 기동하고 지정된 모듈들을 node.js 모듈 캐시로 로드함

``` js
const threadLoader = require('thread-loader');

threadLoader.warmup({
  // pool options, like passed to loader options
  // must match loader options to boot the correct pool
}, [
  // modules to load
  // can be any module, i. e.
  'babel-loader',
  'babel-preset-es2015',
  'sass-loader',
]);
```


<h2 align="center">Maintainers</h2>

<table>
  <tbody>
    <tr>
      <td align="center">
        <a href="https://github.com/sokra">
          <img width="150" height="150" src="https://github.com/sokra.png?size=150">
          </br>
          sokra
        </a>
      </td>
    </tr>
  <tbody>
</table>


[npm]: https://img.shields.io/npm/v/thread-loader.svg
[npm-url]: https://npmjs.com/package/thread-loader

[deps]: https://david-dm.org/webpack-contrib/thread-loader.svg
[deps-url]: https://david-dm.org/webpack-contrib/thread-loader

[chat]: https://img.shields.io/badge/gitter-webpack%2Fwebpack-brightgreen.svg
[chat-url]: https://gitter.im/webpack/webpack

[test]: http://img.shields.io/travis/webpack-contrib/thread-loader.svg
[test-url]: https://travis-ci.org/webpack-contrib/thread-loader

[cover]: https://codecov.io/gh/webpack-contrib/thread-loader/branch/master/graph/badge.svg
[cover-url]: https://codecov.io/gh/webpack-contrib/thread-loader
