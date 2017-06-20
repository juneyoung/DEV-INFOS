### Git 사용하기

[메인으로](https://github.com/juneyoung/DEV-INFOS)

#### Github 에서 사용하기
```
$> git init
$> git remote add origin [git url]
$> git pull origin master
$> git add -A .
$> git commit -m '[message]'
$> git push origin master
```


#### Branch 로부터 프로젝트 시작하기
```
# 작업할 폴더
$> git init
$> git remote add origin [git url]
$> git --set-upstream-to origin/[branch name]
```


#### 이미 사용중인 프로젝트 Gitlab 등록
```
# 이미 사용중인 프로젝트 폴더로 이동한 후 작업
$> git init
$> git remote add origin [새로운 git url]
$> git add -A .
$> git commit -m '[메세지]'
$> git push origin master
$> git --set-upstream-to origin/master
```

#### `IDE` 에서 `.ignore` 에 있는 파일들을 내려받거나 커밋하려고 할 때
```
$> git rm -r --cached .
$> git add .
$> git commit -m 'fixed untracked files'
```

#### 디렉토리명 바꾸기
```
# 일반적인 경우
$> git mv [현재 디렉토리명] [변경할 디렉토리명]

# 대소문자만 변경한 경우
$> git mv [현재 디렉토리명] tmp
$> git mv tmp [변경할 디렉토리명]
```


#### History
- 2017.05.11 : 초안작성
- 2017.06.20 : `디렉토리명 변경`, `캐시정리` 추가 
