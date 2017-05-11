### CentOS 에서 Ansible 설치하기

#### 절차
1. python3 설치
```
# Python3 다운로드
$> wget https://www.python.org/ftp/python/Python-3.6.1.tgz

# 압축해제
$> tar -xvf Python-3.6.1.tgz

# 혹은 su root
$> sudo su

# Python3 폴더 이동 후 configure /설치
$> cd Python-3.6.1
$> ./configure
$> make install

# 확인. 혹은 pip3
$> python3
```
2. ansible 설치
```
# ansible 설치시 자동으로 되지만 확실히 하기 위해 pyyaml 설치
$> sudo pip3 install pyyaml

# ansible 설치
$> sudo pip3 install ansible
```

#### Trouble shooting
- `python3: command not found` : `.bash_profile` 에 `/usr/local/bin` 들어가 있나 확인
- `permission denied` : `sudo` 권한 사용자로 수행

#### 참고
- [Python tarball repository](https://www.python.org/ftp/python/3.6.1/)

#### History
- 2017.05.11 : 초안작성
