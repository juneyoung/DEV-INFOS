### Javascript DOM 컨트롤하기

#### 개요
jQuery 제외한 방식으로 DOM 을 컨트롤하는 방식에 대한 기술. 
`IE`같은 낙후 기술에 대한 호환은 고려하지 않았음.
jQuery 호환을 위해서는 `jQueryElement.get(0)` 한 상태에서 사용하면 됨.

#### 엘리먼트 조작하기
```
# 엘리먼트 생성하기
# 이 때 엘리먼트는 속성 지정 등 조작할 수는 있지만 화면에는 나타나지 않는다.
var div = document.createElement('div');

# 엘리먼트 속성 추가 변경/삭제
div.setAttribute('name', 'dog');
div.removeAttribute('name');

# 엘리먼트 DOM 에 추가하기. 
# DOM 객체라면 document.body 대신 어떤 엘리먼트라도 상관없음
document.body.appendChild(div);

# 엘리먼트 제거하기
document.removeChild(div);

# 스타일 조작하기 
div.style.width = '500px'; 
``` 

#### Native 엘레멘트 셀렉터
```
# DOM 에서 div 태그 중 가장 상위 하나 가져오기
var elem = document.querySelector('div');

# DOM 에서 div 태그 모두 가져오기
var elems = document.querySelectorAll('div');

# div 중에서 name 속성이 black 인 엘리먼트 가져오기
var blackDiv = document.querySelector('div[name="black"]');

# 부모 엘리먼트 가져오기 
var parent = blackDiv.parentNode;

# 같은 레벨에서 이전/다음 엘리먼트
var elderBrother = blackDiv.previousSibling;
var youngerBrother = blackDiv.nextSibling;

# 자식 엘리먼트 조회
var children = parent.children;

# 형제 모두 조회
var siblings = me.parentNode.children;

```

#### History
- 2017.05.02 : 초안작성

