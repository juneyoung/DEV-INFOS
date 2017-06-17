# Ansible - Playbook 설치 가이드

[Ansible 항목으로](https://github.com/juneyoung/DEV-INFOS/edit/master/Ansible)

### 개요

Ansible 을 CentOS 에 설치하고 playbook 을 구동하는 부분까지를 다루고 있음.

### Ansible 설치 

CentOS 기준으로 패키지 관리자 `yum` 을 통해 설치한다. 바이너리 타르볼로 설치도 가능하지만 공식 홈페이지에서도 패키지 관리자를 사용하는 것을 권장하고 있다.
* 공식 홈페이지처럼 바로 `yum install ansible` 할 경우, `No package ansible available` 오류가 발생
>ansible 은 `Extra Packages for Enterprise Linux (EPEL)`
 스펙에 포함되기에 `epel-release` 패키지 설치를 선행해야 함
 
```
# yum 리파지토리 클린 후 ansible 설치까지
# -y 옵션은 중간에 프롬프트에서 질의처리되는 부분을 자동으로 넘겨줌

$ > yum -y clean all
$ > yum -y update
$ > yum -y install epel-release
$ > yum -y install ansible 
```

### 설치 확인

`ansible --version` 명령어로 설치된 ansible 의 정보를 볼 수 있음

```
$ > ansible --version

# 결과 출력
ansible 2.3.0.0
  config file = /etc/ansible/ansible.cfg
  configured module search path = Default w/o overrides
  python version = 2.7.5 (default, Nov  6 2016, 00:28:07) [GCC 4.8.5 20150623 (Red Hat 4.8.5-11)]
```

### 설정 만지기

기본적으로 `yaml` 포멧임


### Playbook 설정
특징
- `Playbooks` 은 ansible 의 빌드, 배포, 오케스트레이션 `언어` (Playbooks are Ansible’s configuration, deployment, and orchestration language)
- `Playbook` 파일 안에 있는 개별 프로파일을 `play` 라고 부름. 각 플레이는 `yml` 의 문법에 따라 `---` 로 구분됨

항목별 처리
- `hosts` : `/etc/ansible/hosts` 에 설정된 키(`[]` 로 쌓인 부분)로 가져올 수 있음. 복수는 `:` 로 연결함
- `become`, `become_method` : 사용자 변경시 사용. 가령 `become` 이 `root` 라면 `become_method`는 `sudo`.
- `tasks` : 실행 명령 목록


#### Docker image 예제

간단하게 원격지에 `centos:latest` 도커 이미지를 풀링하는 설정

> 1. `/etc/ansible/hosts` 파일 : `[]` 는 그룹을 나타낸다
> ```
> [docker-hosts]
> 127.0.0.1:9800
> 127.0.0.1:9801
> ```

> 2. `playbook.yml` : 간단하게 `centos:latest` 이미지를 풀링함
> ```
> ---
> # This playbook deploys a docker image centos:latest
> 
> - hosts: docker-hosts
>   remote_user: root
>   become: yes
>   become_method: sudo
> 
>   tasks:
>     - name: pulling docker image
>       docker_image:
>         name: centos
> ```

> 3. Playbook 실행
> ```
> # yml 이 있는 폴더에서
> $ > ansible-playbook playbook.yml -f 10
> ```

> 4. 17 일 상황으로는 에러가 남(알아보는 중)
> ```
> PLAY [docker-hosts] ************************************************************
>
> TASK [Gathering Facts] *********************************************************
> fatal: [127.0.0.1]: UNREACHABLE! => {"changed": false, "msg": "[Errno None] Unable to > connect to port 9800 on 127.0.0.1", "unreachable": true}
> 	to retry, use: --limit @/home/ansible/playbook/playbook.retry
> 
> PLAY RECAP *********************************************************************
> 127.0.0.1                  : ok=0    changed=0    unreachable=1    failed=0   
> ```





### 덧.
- [`yml` 이 맞는지 `yaml` 맞는지](https://stackoverflow.com/questions/21059124/is-it-yaml-or-yml)


### History

- 2017.06.17 - 초안 작성 

