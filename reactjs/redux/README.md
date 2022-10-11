# Redux

#### 개요
Redux 나 Recoil, Context API 는 지향점이 모두 비슷하다. 컴포넌트 간 자원 공유를 뎁스를 덜 신경쓰고 편리하게 하기 위해서이다.

#### Redux Flow
개념이 매우 어려운데, [생활코딩](https://www.youtube.com/watch?v=Jr9i3Lgb5Qc&list=PLuHgQVnccGMB-iGMgONoRPArZfjRuRNVc) 에서 잘 정리를 해주었다
- 전역에서 참조할 상태를 관리하는 store 가 있다
- 상태는 state 라고 칭한다
- 사용자는 정의된 action 을 통해서만 state 를 변경할 수 있다
- action 은 dispatch 라는 요소에 의해 접수 된다
- dispatch 는 reducer 를 사용해서 변경한다
- dispatch 는 state 가 변경되면 render 에게 변경 되었음을 전달한다

#### 현황
2022.10.11 시점에 아래 2 개 패키지를 이용하여 사용하는 게 권장되고 있다
```shell
$ npm install @reduxjs/toolkit react-redux
```
Slice, Selector 같은 개념이 추가되었지만 그냥 wrapper 이다.

#### 문제
redux 자체는 browser 기반으로 작동하기 때문에, SSR 을 사용할 수 있는 next.js 등과 함께 사용할 때 애로 사항이 꽃핀다
- 화면이 새로고침되면 당연히 데이터가 전부 날아감

#### 대안
- redux-persist
- next-redux-wrapper

처리 방식은 아래와 같다.
- configureStore 시 persistStore 도 함께 생산
- `store.__persistor = persistStore(store)` 로 store 와 관계를 설정해줌
- Slice 에 `HYDRATE` 핸들러를 추가하고, 해당 이벤트 변경 시에도 state 를 업데이트

연관 링크
- [next 에서 reduxStore 사용하기](https://github.com/kirill-konshin/next-redux-wrapper#usage-with-redux-persist)

#### 링크
- [Redux - getting started](https://ko.redux.js.org/introduction/getting-started/)
