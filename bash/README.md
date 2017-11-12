# Bash shell 작성하기

[목록으로](https://github.com/juneyoung/DEV-INFOS)

## 00. 매직 키워드 / 주석

```
# "#" 을 라인의 앞 쪽에 붙여넣게 되면 주석으로 간주한다
# 이것은 주석이다

# # 단, 아래 경우는 매직키워드로 배쉬 쉘을 시작한다는 의미로 사용됨
#! /bin/bash

# 일반적으로 터미널에서 사용되는 규약을 따름
# 멀티라인 출력 #1
echo "a\
b\
c"
# 멀티라인 출력 #2
echo -e "a
b
c"
```

## 01. 변수 선언
사용자 변수
```
#! /bin/bash

# 전역변수(export)의 선언 function 내부에서 외부 변경 값을 참조할 수 있음
# 변수 선언 시, 할당 연산자 좌우에 공백을 넣지 않도록 할 것
export GLOBAL_VAR="This is a global variable"
LOCAL_VAR="This is a local variable"

function printTest {
  # "This is a global variable" 출력
  echo $GLOBAL_VAR
  
  # LOCAL_VAR 찾을 수 없음
  echo $LOCAL_VAR
}
```
시스템 변수 : 시스템에서 제공되는 변수
```
#! /bin/bash

# 전달받은 파라미터의 수 (n 번째 파라미터 접근은 $n 으로 할 수 있음)
echo "Number of Parameters : $#"

# 이전 명령어의 결과를 출력할 수 있음. 0 이라면 성공, 그외는 실패.
# 여기서는 이전 라인인 echo 의 결과를 출력함
echo "Result of former command is : $?"

# 프로그램을 정상 종료함/ 파라미터를 1로 전송하면 오류로 간주됨 
exit 0
```


## 02. 집합 순회

`IFS` 는 `Internal Fields Separator` 를 의미함. 
`for`/`in`/`do`/`done` 키워드를 사용함 
```
#! /bin/bash

# 01. 조회한 디렉터리의 목록을 출력
IFS=$'\n' FILES=`ls -al`
for FILE in "${FILES[@]}"; do
    echo $FILE
done

# 02. 조회한 디렉터리의 목록을 출력 (인덱스 접근)
IFS=$'\n' FILES=(`ls -al`)
for i in "${!FILES[@]}"; do
    FILE_IDX=$i
    FILE=${FILES[$FILE_IDX]}
    echo $FILE
done
```

## 03. 조건문 처리

- `if`/`elif`/`else`/`fi` 키워드를 사용함  
- `case`/`in`/`)`/`;;`/`*)`/`esac` 키워드를 사용함
```
#! /bin/bash

if [ $1 -eq 0 ]; then
  echo "Number $1 is Zero"
elif [ $1 -gt 0 ]; then
  echo "Number $1 is possitive"
else
  echo "Number $1 is negative"
fi  
  
case in $1
  0)
    echo "Number $1 is Zero"
    ;;
  1)
    echo "Number $1 is 1"
    ;;
  *)
    echo "This is Default Action"
esac
    
exit 0    
```

## 04. 명령 리디렉션

백쿼트를 이용해서 다른 명령어의 결과를 변수로 받을 수 있음 
```
#! /bin/bash

LS_RS=`ls -al`
echo -e $LS_RS

exit 0
```

## 05. 네트워크 통신
`curl` 을 이용하면 여러가지 방식으로 호출할 수 있음
```
# SLACK webhook api 를 호출하는 예제 
# X 는 Method 옵션, H 는 헤더
curl -X POST -H 'Content-type: application/json' --data $SLACK_MSG_CTR $SLACK_URL
```

## 06. MYSQL 조회
`yum install mysql` 이 선행되어야 함(클라이언트만 필요). 단, MYSQL 의 경우, `\n` 이나 `\t` 같은 특문을 가공해야 함.
```
#! /bin/bash 

# QUERY_RS 라는 변수에 MYSQL NOW() 의 결과를 넣는 예제
QUERY_RS=`mysql -h $MYSQL_URL -u$MYSQL_USER -p$MYSQL_PW $MYSQL_SCHEMA -e "SELECT NOW() FROM DUAL;"`

echo $QUERY_RS

exit 0
```


## 97. 트러블 슈팅

- 잘되던 스크립트가 윈도우 운영체제를 거쳐 리눅스에 배포되었는데, 문법 오류가 남.
  이 경우는 `vim` binary mode 로 확인해 볼 것 - `^M` 이라는 특문을 제거. 
  
## 98. 유효성 검사
[ShellCheck.net](https://www.shellcheck.net/) : 스크립트 최적화를 위해 유효성을 검사해 주는 사이트 

## 99. Hostory
- 20171112 : 초안 작성 
