# Python

[메인으로](https://github.com/juneyoung/DEV-INFOS)

### 개요

`Deep learning` 을 위한 선수 조건으로서의 파이선. `2.x` 버전은 지원이 중단되었기에 `3.x` 기준으로 작성

### 곁가지
-  [numpy 라이브러리](https://github.com/juneyoung/DEV-INFOS/blob/master/Python/numpy)
- [matplotlib 라이브러리](https://github.com/juneyoung/DEV-INFOS/blob/master/Python/matplotlib)
-  [django 프레임워크]()
- [pandas 라이브러리](https://github.com/juneyoung/DEV-INFOS/blob/master/Python/pandas/Pandas_Study.ipynb)


### `Class` 선언
- 생성자는 `__init__` 으로 예약
- 내부 메소드도 첫번째 인자는 `self`로 고정
- 별도의 종료 문법은 없음
```
class Test:
	def __init__(self, param)
    	self.param = param

	def display
    	print('param : ' + param)
```

### `Method` 선언
- `def` 키워드 사용
> ```
> def hello():
> 	print('Hello')
>     
> def sum(x, y):
> 	return x + y    
> ```
- 파라미터의 순서를 caller 가 변경 가능
> ```
> def hi(name, greetings):
> 	print(greetings + name)
> 
> # 아래 구문은 결과가 같음
> hi('June', 'Hello')
> hi(greetings='Hello', name='June')
> ```
- `default` 를 줄 수 있음
> ```
> def hi(name='June', greetings='Hello'):
> 	print(greetings +  name)
>
> hi()
> ```
- `*` 를 사용해서 파라미터 수를 유동적으로 처리가능
>```
> def hi(*param):
> 	print(param)
>
> hi('June', 'Hello', 1, 2, 2)
>```

### History

- 2017.06.18 - 초안 작성 

