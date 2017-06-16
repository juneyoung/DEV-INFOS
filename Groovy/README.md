## Groovy 문법

[메인으로가기](https://github.com/juneyoung/DEV-INFOS)

### 개요

`gradle` 이라는 패키지 관리자를 사용할 때, 사용하는 `Groovy` 문법을 정리. 그 외의 잡다한 특징들에 대해서는 다루지 않으니 [공식 페이지](http://www.groovy-lang.org/index.html)를 참조하길 :+1:


### 특징

- 문자열 내에서 `${}` 를 사용해서 위에서 선언된 변수를 삽입할 수 있음
- `${ 1 + 2 }` 처럼 내부에서 간단한 연산도 지원 
- `${home}` 이나 `$home` 동일하고 home 이 오브젝트라면 하위에 `$home.address` 로 접근가능
- 



### 기타

- 주석은 Java 와 동일함 `//` 한줄, `/*` 여러줄  
- `'''` 로 멀티라인 문자 변수를 지원
- `'` 도 문자열


### 참고사이트

- [Groovy 문법 공식](http://docs.groovy-lang.org/latest/html/documentation/#_syntax)


### History

- 2017.06.11 : 초안 작성
