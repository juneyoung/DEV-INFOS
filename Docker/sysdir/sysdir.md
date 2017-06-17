### Docker 시스템 디렉토리(리눅스 계열)

[Docker 항목으로](https://github.com/juneyoung/DEV-INFOS/edit/master/Docker)

#### 개요
리눅스 기반 OS 에서 docker 시스템에서 사용하는 디렉토리 정보.

#### `/etc/docker`
`key.json` 이 있는 디렉토리. 만약 docker daemon 이 구동되는 설정값을 변경하려면 여기에 [docker.json](https://github.com/juneyoung/DEV-INFOS/blob/master/Docker/daemon/daemon.md)을 작성하면 된다.

#### `/var/lib/docker`
docker 에서 기본으로 생성하는 이미지, 컨테이너 정보가 모두 들어간다.(동시에 기본 `docker root dir`임) 데이터 백업이 필요한 경우, 이 부분을 압축하면 됨. 컨테이너나 이미지가 추가될 때마다 용량을 늘리므로 SSD 같은 부분으로 빼는게 좋음

#### History
- 2017.05.02 : 초안작성
