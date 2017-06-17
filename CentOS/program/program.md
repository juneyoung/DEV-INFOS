### CentOS 에서 프로그램 설치하기

[CentOS 항목으로](https://github.com/juneyoung/DEV-INFOS/edit/master/CentOS)

#### 패키지 매니저를 이용한 설치 (yum)
`yum` 을 사용하면 설치가 간편하고 PATH 에 별도로 작업을 하지 않아도 되서 편리하다. 
다만 일부 라이브러리는 최신이 아닐 수 있기 때문에 유의가 필요함.
(예를 들면 mariadb 같은 경우, 설치 이후에 별도로 `mysql_upgrade` 명령으로 버전업 시켜줘야 함)
```
# 기존 설치 목록 확인하기
$> yum list installed

# 설치가능 목록. 보통 grep 이랑 같이 쓰임
$> yum list
$> yum list | grep [프로그램명]

# 이미 설치되어 있는 패키지를 업데이트. -y 옵션은 추가 다운로드 및 설치에 대해서 무조건 yes 하겠다는 플래그
$> yum update

# 설치하기 
$> yum install [프로그램명]
$> yum install java-1.8.0-openjdk.x86_64

# 제거하기
$> yum remove [프로그램명]
```

#### 패키지 매니저를 이용한 설치 (rpm)
`rpm` 사용할 경우, 바이너리보다는 쉽지만 패키지 의존성 오류에 걸릴 확률이 높다. 
설치 전 반드시 `uname -an` 으로 자신의 운영체제를 확인하고 맞는 패키지로 설치할 것.
```
# 기존 설치 목록 확인하기 
$> rpm -qa

# 패키지 업데이트 하기
$> rpm -Uvh [패키지명]

# 설치하기
$> rpm -ivh [패키지명]

# 제거하기
$> rpm -ev [패키지명]
```
- `-a` : all
- `-v` : verbose. 내용을 보여줌
- `-U` : upgrade
- `-h` : hash
- `-i` : install
- `-e` : erase
`rpm` 이라고 치면 기타옵션을 확인할 수 있다

#### 바이너리 파일을 이용한 설치
```
# wget 이나 scp 를 통해서 작업하는 장비로 바이너리 파일을 옮겨온다.
$> wget [바이너리파일의 url]
$> scp [바이너리 파일] [원격계정]@[원격 IP]:[원격 경로]

# 원하는 곳으로 옮긴 후 압축해제
$> mv [바이너리 파일] [설치할 경로]
$> tar -xvf [파이너리 파일]

# .bash_profile 에 PATH 추가 (연관항목 참조)
# 적용
$> source .bash_profile
```
[.bash_porile 작성하기](https://github.com/juneyoung/DEV-INFOS/blob/master/CentOS/system/env.md) 

#### History
- 2017.05.02 : 초안작성
