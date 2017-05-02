### OS 구동시 시작프로그램 등록하기

#### 개요
`MYSQL` 과 같이 장비나 OS가 재시작될 때 자동적으로 떠야 할 프로그램을 등록한다.

#### 자동 실행 프로그램 조회
`chkconfig` 로 조회하기
```
$> chkconfig --list
``` 
`systemctl` 로 조회하기
```
$> systemctl status [조회프로그램명]
```
출력된 내용 중 `enable` 이라고 되어 있으면 구동시 자동으로 실행되는 프로그램이다.


#### 프로그램 등록하기
- 자동실행 프로그램을 `bash` 쉘로 작성할 수 있으며, `/etc/init.d` 안에 놓도록 한다.
```
# root 계정 혹은 root 권한이 있는 계정으로 전환. 
$> su root
# 작업 경로로 이동
$> cd /etc/init.d
# 쉘 스크립트 작성
$> vi [프로그램 명]
```
- 쉘스크립트 작성하기 : 상황에 맞는 스크립트를 작성한다. 
```
#!/bin/bash
# TOMCAT 을 실행할 수 있는 스크립트
source /etc/profile
export TOMCAT_HOME = /home/$USER/apache-tomcat-8.5
case $1 in
    start)
        su - juneyoungoh -c $TOMCAT_HOME/bin/startup.sh
        ;;
    stop)
        su - juneyoungoh -c $TOMCAT_HOME/bin/shutdown.sh
        ;;
    *)
        exit 1
esac
exit 0
```
- `chkconfig` 에 등록하기
```
$> chkconfig add [위에서 추가된 파일명] 
```

#### History
- 2017.05.02 : 초안작성

