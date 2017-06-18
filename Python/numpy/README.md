# Numpy

[Python 으로](https://github.com/juneyoung/DEV-INFOS/blob/master/Python/)

`python3` 기준.

### 개요

`python` 의 산술 연산 라이브러리. numpy 배열이 별도로 존재하는데 아래에서 `numpyArray` 라고 사용되는 부분은 모두 넘파이 배열 타입으로 보면 됨

### 설치
패키지 관리자 `pip3` 를 이용하여 설치
```
$ > pip3 install numpy
```

### 특징
-  numpy 배열이 별도로 있음 
> ```
> import numpy as np
> 
> x = np.array([1.0, 2.0, 3.0])
> print(x)
> '''
> 결과는 [1. 2. 3.] 으로 출력
> '''
> ```
- numpy 배열의 `길이가 같을 때`, 사칙연산을 지원함
- 다중 배열의 경우는 `브로드캐스트` 가 일어남
- 배열 연산시, `좌측 인수보다 우측인수가 적으면 브로드캐스트`가 되지만, 역이라면 에러가 발생
- `numpyArray.shape` : 배열의 형태를 출력. 가령 `2x2` 다차원 배열이라면 결과는 `(2,2)`
- `numpyArray.dtype` : 배열 내용물의 자료형을 출력. 가령 위의 x 의 `dtype` 결과는 `dtype('float64')`
- 인덱스 접근은 다른 언어처럼 `array[x][y]` 로 하면됨
- 접근시 index 값에 numpy 배열을 넣어 복수 수집 가능
- 인덱스에 판별식을 넣어 사용할 수 있음. `X[X>3]`. X의 원소 중 3보다 큰것만 수집


### History

- 2017.06.18 - 초안 작성 

