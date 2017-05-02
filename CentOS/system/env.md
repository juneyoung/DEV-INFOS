### 환경변수 설정하기

#### 개요
Linux 시스템은 사용자 별 환경변수를 설정할 수 있음. 
만약 `root` 계정에 `JAVA_HOME` 변수를 추가하였다면, `root` 계정에서는 `java` 명령어를 전역에서 사용가능하나 `juneyoungoh` 계정에서는 사용이 불가능하다. 
기본적으로 환경변수 파일인 `.bash_profile` 파일은 계정 홈 디렉토리에 위치하며 숨김 파일이기 때문에 `a` 옵션으로 조회해야 표기된다.

#### `.bash_profile`의 수정
기본 `.bash_profile`. 조금 다를 수 있으나 기본은 같음
```
# gradle 을 변수에 추가하는 예제. 
# $USER 는 OS 변수로 현재 사용자. 만약 root 라면 /root 로 대체가능
GRADLE_HOME=/Users/$USER/Documents/gradle-3.3

# PATH 변수를 덮어쓰지 않도록 유의
# 일반적으로 라이브러리 홈 디렉토리를 변수로 추가하고
# PATH 에 추가할 때는 ${변수}/bin 으로 함
# :(콜론)으로 추가할 수 있음
PATH=$PATH:$GRADLE_HOME/bin
```
`echo $PATH` 로 추가된 경로를 확인할 것
`ls` 같은 기본 명령이 안된다면 `PATH` 경로에 콜론 등의 신텍스 문제가 있는 것이니,
`root` 계정으로 변경 후, 현재 계정의 `.bash_profile` 을 재수정한다

#### 적용하기
`source` 명령으로 적용할 수 있다
```
$> source .bash_profile
```
