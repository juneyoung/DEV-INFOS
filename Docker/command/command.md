### Docker 명령어

[Docker 항목으로](https://github.com/juneyoung/DEV-INFOS/edit/master/Docker)

#### 개요
도커 사용간 비번하게 사용했던 명령어를 정리했다. 관리 명령어에서는 도커 이미지, 컨테이너, 리파지토리에 관련한 명령어를 다루고, 구동 명령어는 컨테이너 구동에 사용되는 명령어를 정리한다.

#### 관리 명령어
```
# 현재 로컬에 있는 이미지를 조회한다
$> docker images

# 리파지토리 이미지 목록을 검색한다
$> docker search [이미지명]
$> docker search centos

# 리파지토리에서 이미지를 로컬로 내려받는다. 
# 태그명이 생략된 경우 자동으로 latest 로 들어감.
$> docker pull [이미지명]:[태그명]
$> docker pull centos

# 컨테이너 목록조회하기
# a 는 all
$> docker ps -a

# 컨테이너 지우기
# 컨테이너 name 이 있으면 name 으로도 지울 수 있음 
$> docker rm [컨테이너 ID / 이름]
$> docker rm test-container

# 이미지 지우기
$> docker rmi [이미지명]:[태그명]
$> docker rmi centos

# 컨테이너로 이미지 만들기 
$> docker commit [컨테이너 ID / 이름] [생성할 이미지명]
$> docker commit test-container centos-test

# 도커파일로 이미지 빌드하기
$> docker build -t [생성할 이미지명] [도커파일 경로]
$> docker build -t centos-test .

# 도커 컨테이너 정보 조회하기
# json 형식으로 표준출력됨
$> docker inspect [컨테이너 ID / 이름]
```

#### 구동 명령어(기본)
```
# 도커 컨테이너 만들기 + 구동
# 당연하게 컨테이너가 없으면 아래의 start, stop, attach  등의 명령을 사용할 수 없음
$> docker run [이미지명]
$> docker run -d --name=test-container -p 8080:8080 -v /home/juneyoungoh:/home/test centos:latest

# 도커 컨테이너 멈추기
$> docker stop [컨테이너 ID / 이름]
$> docker kill [컨테이너 ID / 이름]
$> docker stop test-container

# 도커 컨테이너 시작하기(run 이후)
$> docker start [컨테이너 ID / 이름]
$> docker start test-container

# 도커 컨테이너 내부 명령 실행
$> docker exec [컨테이너 ID / 이름] [명령어]
$> docker exec -it test-container /bin/bash

# 도커 실행 중 컨테이너에 붙기
$> docker attach [컨테이너 ID / 이름]
$> docker attach test-container
```

#### 옵션
기본적으로 `-` 옵션이 있고, `--` 옵션이 있음. `-` 의 경우 공백 이후 전달 파라미터를 기술하고, `--` 의 경우 `=` 기호를 사용해서 연결함
- `-v`, `--volumes` : 호스트, 컨테이너 간 공유할 폴더를 지정함. 
```
-v [호스트 경로]:[컨테이너 경로]
$> docker run ... -v /home/juneyoungoh:/home/docker/ ...
$> docker run ... --volumes=/home/juneyoungoh:/home/docker ...
```
- `-d`, `--detach` : `run` 실행시, daemon 으로 실행함. 
```
$> docker run -d ...
$> docker run --detach
```
- `-i` : 표준 입출력을 사용. `-t` : 터미널 사용. 두개 거의 같이 씀
```
$> docker exec -it ...
```
- `-p`, `--publish` : 포트 포워딩
```
-p [호스트 포트]:[컨테이너 포트]
$> docker run ... -p 9080:8080 ...
$> docker run ... --publish=9080:8080 ...
```
- `--name` : 이름 지정하기
```
$> docker run ... --name=test-container ...
```
- `-a` : 작가 - author. `-m` : 메세지. `-p` : pause. 커밋시 컨테이너 자동 중단. `commit` 시 세트로 사용.
```
$> docker commit -a juneyoungoh -m 'Good Job' -p test-container xxxx
``` 

#### History
- 2017.05.02 : 초안작성
