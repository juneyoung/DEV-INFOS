### OSX 에서 Ansible 설치하기

#### 개요
osx 에 기본으로 설치되어 있는 python 은 2.X 버전이므로 python 3.X 를 설치하는 방향으로 처리함 

#### 절차
1. python3 설치 : 사이트에서 다운로드 받아서 설치
2. `pip3` 를 이용한 `pyyaml` 설치
```
$> sudo pip3 install pyyaml
```
3. `pip3` 를 이용한 `ansible` 설치
```
$> sudo pip3 install ansible
```

#### trouble shooting
- `<module>` 을 찾을 수 없음 : 에러 메세지에 `python.2.X` 로 되어 있는지 확인하고, 3 로 변경. `pip install ansible` 의 경우 문법 에러 날 수 있음
- `permission denied` : `sudo` 권한으로 명령어 실행

#### History
- 2017.05.11 : 초안작성
