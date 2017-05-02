### Docker 

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
docker 컨테이너가 정상동작이 안하는 경우(바로 상태가 `Exited` 로 빠진다던가) `logs` 명령으로 로그를 볼 수 있다.
```
$> docker logs [컨테이너 ID / 이름]
```

#### History
- 2017.04.29 : 초안작성
