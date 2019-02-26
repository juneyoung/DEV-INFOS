# Reactjs 16 정리노트

## 01. 변경점
##### A. 컴포넌트 선언 시 기존의 class 형 선언보다 함수형 선언

`hooks` 가 소개되면서 나온 방법론.(`Classes confuse both people and machines`) 
- 기존의 `class` 를 사용할 때는 javascript 의 `this` 개념을 꿰뚫고 있어야 했음 (이벤트 핸들러에 바인딩 한다던지)
- 최근에 팀이 `Prepack` 을 사용한 컴포넌트 폴딩 작업 중에 class 를 사용할 경우, 원치않는 패턴으로 컴파일되어 성능 저하를 초래하는 것으로 밝혀졌음 (`minify` 가 제대로 되지 않는다던지)

oldway
```
import React, { Component } from 'react';

export default class OldCounter extends Component {
    constructor (props) {
        super(props);
        this.state = {
            value : 0
        };
    }

    setValue (value) {
        this.setState({ value : this.state.value + value });
    }

    render () {
        return (<div>
            <p>Old Count(Class) : <b>{ this.state.value }</b></p>
            <button onClick={ () => this.setValue(1) }> +1 </button>
            <button onClick={ () => this.setValue(-1) }> -1 </button>
        </div>);
    }
}
```

ver 16
```
import React, { useState, useEffect } from 'react';

const counter = () => {
    const [ value, setValue ] = useState(0);

    useEffect(() => {
        console.log('counter useEffect :: After rendered ', value);
    });
    
    console.log('redering ', value);

    return (<div>
        <p>Count(Function) : <b>{ value }</b></p>
        <button onClick={ () => setValue( value + 1) }> +1 </button>
        <button onClick={ () => setValue( value - 1) }> -1 </button>
    </div>)
};

export default counter;
```


## 02. Hooks
- `hooks` 는 stateful 한 컴포넌트의 재사용성을 쉽게 높이기 위해 소개되었음 - 기존에 `render props` 나 `HOC` 같은 방법이 있었지만, 재사용시 들어가는 노력이 너무 크다는 판단(wrapper hell).
- 라이프사이클(`componentDidMount`, `componentDidUpdate` 같은)에 불필요한 로직이나 중복되는 작업이 많이 작성되는 것을 예방하고자 함
- 결론적으로 `hooks` 가 `useEffect` 와 같은 방법을 제시함으로 기능 위주로 stateful 컴포넌트를 보다 작게 나눌 수 있도록 지원한다고 함
- 함수형 컴포넌트의 탑 레벨에서만 사용되어야 함
- 반복이나 조건 안에서 사용할 수 없음

##### A. useState

state 를 관리하는 hook 으로 기존의 `setState` 와 동일한 용도
```
const [value, setValue] = useState(x);
```
`x` 를 최초값으로 가지는 `value` 를 변경하는 `setValue`의 선언문이다. 이후에 변경이 일어날 때는 `setValue(y)` 와 같이 할 수 있음. - 개인적으로 이전 구문과 비교했을 때 간결해진 것 같음.

##### B. useEffect

기존의 `componentDidMount`, `componentDidUpdate`, `componentWillUpdate` 와 같은 용도로 사용하기 위해 제공된 hook. 함수형 컴포넌트 안에서 여러번 사용할 수 있음 

예시1.
```
useEffect(() => {
    console.log('do x');
});
```
선언이 아니라 `useEffect` 라는 함수를 실행하는 형태로 사용함. 위와 같은 용도로 사용되는 렌더가 종료되는 시점이 트리거됨. 

예시2.
```
useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
        ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
}); 
```
렌더 종료 시점에 subscribe 를 하고, 컴포넌트가 unmount 될 때 , unsubscribe 를 함.

##### C. custom hook
- `use***` 의 네이밍 룰을 따를 것
- 어떠한 값이라도 반드시 반환해야 함(should)
- 서로 다른 컴포넌트에서 동일한 훅 `useA` 라는 걸 썼을 때, 사용되는 state 는 독립적으로(서로 공유되지 않음) 관리

이 부분은 예시가 더 나음. [useFreiendStatus](https://reactjs.org/docs/hooks-custom.html)

##### D. etc
```
function TodoExample() {
    // useContext hook.
    const locale = useContext(LocaleContext);
    const theme = useContext(ThemeContext);
    
    // useReducer hook
    const [todos, dispatch] = useReducer(todosReducer);
}
```


