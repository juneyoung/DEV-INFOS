### CocoaPods 레퍼런스

#### 개요
xCode 프로젝트의 라이브러리를 용이하게 관리하게 해줌

#### 설치
```
$> sudo gem install cocoapods
```

#### 트러블 슈팅
1. 설치시 `gem` 인증서 오류(`SSL`)
메세지 
```
ERROR: While executing gem ... (Gem::RemoteFetcher::FetchError)
SSL_connect returned=1 errno=0 state=error: certificate verify failed (https://api.rubygems.org/specs.4.8.gz)
```
> a. `gem` [버전 업데이트]()
> b. a 로 해결되지 않으면 `rvm` [인증서 수동 업데이트]()

#### History
- 2017.05.18 : 초안작성
