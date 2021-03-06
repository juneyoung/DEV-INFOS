### Docker 

[메인으로](https://github.com/juneyoung/DEV-INFOS)

#### 개요
도커 사용간 고생했던 부분을 정리한다.

#### 항목
- [명령어](https://github.com/juneyoung/DEV-INFOS/blob/master/Docker/command/command.md)
- [시스템 디렉토리](https://github.com/juneyoung/DEV-INFOS/blob/master/Docker/sysdir/sysdir.md)
- [daemon.json](https://github.com/juneyoung/DEV-INFOS/blob/master/Docker/daemon/daemon.md)

#### 용례
경험 상 docker 는 아래와 같은 절차로 실행한다.
1. docker 설치
2. `docker pull image` : 이미지 준비
3. `docker run image` : 컨테이너 생성
4. `docker exec` : 컨테이너 실행해서 필요한 작업 수행
5. `docker commit` : 컨테이너에서 작업한 내용을 이미지로 등록

#### 예외처리
1. docker 컨테이너가 정상동작이 안하는 경우(바로 상태가 `Exited` 로 빠진다던가) `logs` 명령으로 로그를 볼 수 있다.

```
$> docker logs [컨테이너 ID / 이름]
```
리눅스의 경우 `-d` 로 띄우지 않거나 `dockerfile` 을 사용함에 `init` 을 하지 않으면 바로 종료된다

2. 왠지 모르게 docker 가 용량을 많이 먹을 때 : 미사용 이미지를 정리한다

```
# 미사용 이미지 출력
$> docker images -f "dangling=true"

# 미사용 이미지 삭제 - 위 리스트에서 이미지 아이디로 docker rmi <이미지 아이디> 해도 됨
$> docker rmi $(docker images --quiet --filter "dangling=true")
```

3. docker 컨테이너의 상태가 `DEAD` 라서 추가도 삭제도 안되는 상황. [참조](https://github.com/kubevirt/kubevirt/issues/321). 자주하지 말자. 에러남.
비정상 세마포어를 모두 지우는 듯.[예시](https://github.com/juneyoung/DEV-INFOS/blob/master/Docker/references/killSempaphore.md)

```
#이 명령어 이후에 docker rm [컨테이너명]
$> echo 'y' | sudo dmsetup udevcomplete_all
```
4. `docker exec` 에러. 이 경우 데몬을 재시작하면 된다. `3` 과 연관되어 semaphore 지울 때 문제가 생기는 듯. 
```
$> docker exec -it mysql /bin/bash
rpc error: code = 2 desc = oci runtime error: exec failed: container_linux.go:262: starting container process caused "process_linux.go:73: starting setns process caused \"fork/exec /proc/self/exe: no such file or directory\""
```


#### 기타
a. `dockerd` 와 `service start docker` 
> - `dockerd` : 부모 프로세스가 `1` 이 아니므로 잘못되면 `kill` 명령어로 죽이면 된다
> - `service start docker` : `service` 로 띄우게 되면 부모가 `1` 이라 죽일 수 없다. `<defunc>`에 빠졌다면 장치 재기동 외에는 답이 없다

b. [`Dockerfile` 예제](https://github.com/juneyoung/docker-edu) 

#### 이미지 별
- [elk-sebp](https://github.com/juneyoung/DEV-INFOS/blob/master/Docker/images/docker_elk_sebp.md) : ELK 가 한번에 묶여 있는 이미지. elastic.co 에서 공식으로 제공되는 이미지가 아니다

#### History
- 2017.04.29 : 초안작성
- 2017.06.16 : 이미지별 항목 작성
- 2017.08.16 : DEAD 상태처리 추가
