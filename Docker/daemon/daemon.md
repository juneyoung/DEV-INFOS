### `daemon.json` 작성하기

[Docker 항목으로](https://github.com/juneyoung/DEV-INFOS/edit/master/Docker)

#### 개요
docker 사용시, 출력되는 정보를 수정한다. default 설정 기준으로 볼 때, `/etc/docker` 에 생성해야 한다.

#### `daemon.json` 수정
필요한 부분만 수정하면 된다. 가령 루트 디렉토리를 변경하고자 하면 아래와 같이 적용하면 된다. 언급되지 않은 부분은 `service start docker` 에 사용되는 부분 중 default 로 적용됨
```
{
    "graph" : "/data/docker"
}
```

#### Linux 계열 `daemon.json`
2017.05.02 시점의 리눅스 사용가능 옵션이다. 필요한 부분만 명시하도록 한다.(`default` 옵션을 넣고자 아래처럼 키는 있는데 값을 비워넣으면 작동하지 않음)
```
{
    "api-cors-header": "",
    "authorization-plugins": [],
    "bip": "",
    "bridge": "",
    "cgroup-parent": "",
    "cluster-store": "",
    "cluster-store-opts": {},
    "cluster-advertise": "",
    "debug": true,
    "default-gateway": "",
    "default-gateway-v6": "",
    "default-runtime": "runc",
    "default-ulimits": {},
    "disable-legacy-registry": false,
    "dns": [],
    "dns-opts": [],
    "dns-search": [],
    "exec-opts": [],
    "exec-root": "",
    "fixed-cidr": "",
    "fixed-cidr-v6": "",
    "graph": "",
    "group": "",
    "hosts": [],
    "icc": false,
    "insecure-registries": [],
    "ip": "0.0.0.0",
    "iptables": false,
    "ipv6": false,
    "ip-forward": false,
    "ip-masq": false,
    "labels": [],
    "live-restore": true,
    "log-driver": "",
    "log-level": "",
    "log-opts": {},
    "max-concurrent-downloads": 3,
    "max-concurrent-uploads": 5,
    "mtu": 0,
    "oom-score-adjust": -500,
    "pidfile": "",
    "raw-logs": false,
    "registry-mirrors": [],
    "runtimes": {
        "runc": {
            "path": "runc"
        },
        "custom": {
            "path": "/usr/local/bin/my-runc-replacement",
            "runtimeArgs": [
                "--debug"
            ]
        }
    },
    "selinux-enabled": false,
    "storage-driver": "",
    "storage-opts": [],
    "swarm-default-advertise-addr": "",
    "tls": true,
    "tlscacert": "",
    "tlscert": "",
    "tlskey": "",
    "tlsverify": true,
    "userland-proxy": false,
    "userns-remap": ""
}
```
변경 후, 데몬을 실행하고, `docker info` 명령어로 수정 부분이 적용되었는지 확인한다.

#### History
- 2017.05.02 : 초안작성
