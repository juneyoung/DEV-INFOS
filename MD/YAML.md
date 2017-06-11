## YAML 작성하기 



### 개요
사람이 쉽게 읽을 수 있는 ~~개발자한테는 JSON 보다 불편한~~ 데이터 양식.
`키/값` 쌍으로 이루어져 있음. 아래와 같은 특징들이 있음.

- `공백문자` 들여쓰기가 구분자
- `Tab` 으로 들여쓰기하면 구분 못함
- 문자열 값을 표현할 때 그냥 써도 되고 `"` 나  `'` 로 둘러도 무관
- 주석은 bash 처럼 `#` 로 사용
- 문자열 내 특문은 `\` 로 사용. `\n` 


### 복합 오브젝트의 표현
원본 `JSON` 오브젝트
```
{
    "name" : "철수"
    , "age" : "30"
    , "assets" : [
    	{
        	"type" : "liquid asset"
            , "label" : "cat"
        }
        , {
        	"type" : "solid asset"
            , "label" : "building"
        }
    ]
}
```

`yaml` 의 표현 #1.
```
name: 철수
age: 30
assets: 
    -
    type: liquid asset
    label: cat
    -
    type: solid asset
    label: building
```

`yaml` 의 표현 #2.
```
name: "철수"
age: 30
assets: [{type : 'liquid asset', label : 'cat'}, {type : 'solid asset', label : 'building'}]
```

`yaml` 의 표현 #3.
```
{ name: "철수", age: 30, assets: [{type : 'liquid asset', label : 'cat'}, {type : 'solid asset', label : 'building'}] }
```

### 예약어
~~언제쓰는지는 모르지만~~ `@`, `''`, `|`, `>`, `---`, `...`, `@YAML`, `@TAG` 은 예약어라고 함.

- `---` 와 `...` 는 쌍으로 사용되며 문서의 시작과 끝을 표현한다고 함. 여기서 `문서` 가 뭔지는 ...
- `|` 와 `>` 는 보존과 접기라는데, 뭘 접겠다는 건지 ... 


### 참고 문서

- [위키](https://ko.wikipedia.org/wiki/YAML)
- [스프링 매핑](http://blog.saltfactory.net/load-yaml-file-in-spring/)

### History

- 11.06.2017 : 초안 
