### CentOS 레퍼런스

[메인으로](https://github.com/juneyoung/DEV-INFOS)

#### 개요
현재 가장 핫한 `el7` 기준 작성임.

#### 항목
- [시스템 디렉토리]()
- [환경변수 설정하기](https://github.com/juneyoung/DEV-INFOS/blob/master/CentOS/system/env.md)
- [프로그램 설치](https://github.com/juneyoung/DEV-INFOS/blob/master/CentOS/program/program.md)
- [OS 구동시 시작될 프로그램 등록](https://github.com/juneyoung/DEV-INFOS/blob/master/CentOS/system/boot.md)
- [기본 명령어](https://github.com/juneyoung/DEV-INFOS/blob/master/CentOS/cli/README.md)

#### 미분류 항목
- 장치 메모리 조회 : `vi /proc/meminfo` - 노출되는 단위는 KB.
- `ssh` 원격 접속 오류 중 아래와 같은 메세지에 대처 : 원인 `OS 재설치`
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
SHA256:#######################################.
Please contact your system administrator.
Add correct host key in /Users/juneyoungoh/.ssh/known_hosts to get rid of this message.
Offending RSA key in /Users/juneyoungoh/.ssh/known_hosts:11
RSA host key for ###.###.###.### has changed and you have requested strict checking.
Host key verification failed.
```
해결방안 : 호스트에서
```
$ > ssh-keygen -R ###.###.###.###
```


#### History
- 2017.04.29 : 초안작성
