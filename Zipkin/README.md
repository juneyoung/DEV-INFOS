### Zipkin

[메인으로](https://github.com/juneyoung/DEV-INFOS)

#### 개요
트위터에서 개발한 MSA 트래킹 분석 시스템으로 Google Dapper 기반으로 만들어졌음. MSA 트랜젝션을 추적하기 위해 Tracer 가 필요한데, Java 진영에서 유명한 것은 `Brave` 임. `Spring sleuth` 에서 내부적으로 Brave 를 사용하고 있음

- sleuth : [공식 사이트](https://cloud.spring.io/spring-cloud-sleuth/single/spring-cloud-sleuth.html)의 `Terminalogy` 섹션에 의하면 Spring cloud 를 위한 분산 트레이싱 솔루션으로 정의할 수 있음. sleuth 는 로깅으로 표현됨.
- zipkin : [공식 사이트](https://zipkin.io/)의 `Home` 에 의하면 분산 트레이싱 시스템으로 정의할 수 있음. MSA 아키텍쳐 안에서 레이턴시 문제가 발생하는 부분을 추적할 수 있음.

시스템에서 하나의 작업을 `Trace` 라고하고 Trace 내부에서 다른 MSA Call 을 호출하는 것을 `Span` 이라고 함.

DevOps 관점에서 MSA 를 구성한 후, Sleuth 로 수집한 트레이싱 데이터를 zipkin 으로 보내서 분석하는 그림으로 이해하였음.

#### 나만의 용어 정리
사실 이해한 부분에 대한 확신이 없어 `나만의` 라는 접두를 붙였다.

- Trace : MSA 에서 하나의 작업(트렌젝션으로 묶을 수 있는?)
- Span : Trace 를 구성하는 MSA 내부의 호출
- RPC : `Remote Procedure Call`. `Brave` 에서 구현한 것이라고 하니, Spring Cloud 와 zipkin 을 연동하는 하나의 프로토콜 정도로 이해하였음. 공홈에서는 수동으로 `Interceptor`를 구성하는 방법이 소개되어 있음.


#### 준비물
zipkin 을 Spring 서버 자체로 띄울 수 있는 방법도 있는 것 같은데, 이번에는 모니터링을 총괄하는 별도의 시스템을 구성하는 것이 아니기에 zipkin 서버 1기, msa 서버 1기로 구성하였음.

Java 버전이 `반드시` 8 이상이어야 가능함

- zipkin 서버 (default port : 9411)
- spring msa 서버 (default port : 8080)

spring 에서 zipkin 으로의 호출은 기본으로 `HTTP` 임.

#### zipkin 실행하기

[사이트 퀵스타트 섹션](https://zipkin.io/pages/quickstart.html)을 참고하여 실행한다
```
$> curl -sSL https://zipkin.io/quickstart.sh | bash -s
$> java -jar zipkin.jar
```

개인적으로 서버에서 백드라운드 기동을 위하여 아래와 같은 방식으로 실행하였음
```
# 지속 기동을 위해 nohup 명령어를 사용함.
$> nohup java -jar /data/zipkin/zipkin.jar --prefix=/zipkin & > /dev/null
```


#### Gradle 필요 디펜던시 설정

넷상의 블로그를 종합해보면, 아래와 같은 플러그인이 필요함
- spring-cloud-starter-sleuth
- spring-cloud-starter-zipkin

테스트 환경에서는 간단하게 [Spring initializer](https://start.spring.io/) 를 사용하여 zipkin-client, sleuth 를 포함하여 프로젝트를 생성하였음.


#### Nginx 를 이용한 도메인 설정 (수정요 - 다음으로 건너뛰어도 무관)
이 부분은 작성 시점(2019.04.14)에 정상적으로 작동되고 있지 않음. 정상 기동을 위해서는 sub domain 없이 스프링 설정이 필요함. 향후 업데이트 예정.

1. zipkin 명령어에 sub domain 부여
```
$> java -jar zipkin.jar --prefix=/zipkin
```
2. nginx 설정에 location 설정(CentOS 기반 디폴트라면 `/etc/nginx/nginx.conf` 파일의 수정)
```
... 전략 ...

http {
    server {
        listen       80;
        server_name  localhost;
        
        ... 생략 ...

        location /zipkin {
            proxy_pass http://127.0.0.1:9411;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
            proxy_set_header   X-Real-IP        $remote_addr;
            proxy_set_header   X-Forwarded-Proto http;
            proxy_set_header X-Forwarded-Host $host;
            proxy_set_header X-Forwarded-Server $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }
}   
```
3. spring `application.yaml` 에 `base-url` 설정
```
spring.zipkin.base-url: http://localhost:9411/zipkin
```
 

#### Spring 프로젝트에서 sleuth 사용하기 
1. `application.yaml` 에 추가하기 
```
spring:
  # 수집된 정보를 전달할 zipkin URL 정보
  zipkin:
    base-url: http://localhost:9411
  # 기본 트레이서에 application name 을 참조한다. 이 이름으로 zipkin UI 에서 필터가 가능하다
  application:
    name: zipkinLocal
  profiles:
    active: dev
  # sleuth 로그 샘플링의 빈도임. 0 ~ 1까지 가능하고 예전 버전의 경우, probability 대신 percent 라는 키를 사용한다  
  sleuth:
    sampler:
      probability: 1.0
```
sleuth 에서 중요한 부분은 로깅인데 기본적으로 logback 에 연동되어 있다. 커스터마이즈가 필요한 경우에는 [공식 페이지](https://cloud.spring.io/spring-cloud-sleuth/single/spring-cloud-sleuth.html) 의 `Logback Setup` 항목을 참조한다.

2. Logging 보기

기본적으로 Logging 의 형식은 아래와 같다.
```
[spring.application.name][traceId][spanId][export] ...
```
마지막 `export` 항목은 이 로그가 다른 프로그램(`zipkin` 같은)에 연동되었는지 여부를 나타낸다.

실제로 기동해서 출력되는 예제 
```
# 예제                            
2019-04-14 18:40:50.748  INFO [zipkinLocal,a1fc341130c6d9a0,a1fc341130c6d9a0,true] 6469 --- [nio-8080-exec-1] o.owls.zipkin.test.ZipkinTestController  : doZipkinTest : Sun Apr 14 18:40:50 KST 2019
```


#### 예외 사항
테스트 중 발견한 사항으로 zipkin jar 실행시 `--prefix={서브도메인}` 옵션을 주면 추적 데이터가 전송되지 않는다.
```
# 아래 경우는 localhost:9411/zipkin 으로 zipkin 서버가 뜨지만 spring.zipkin.base-url 옵션에 url 을 기재해도 데이터가 전달되지 않음 
$> java -jar zipkin.jar --prefix=/zipkin

# 아래 경우는 정상적으로 데이터를 전달할 수 있음
$> java -jar zipkin.jar
```

테스트 상황의 경우, nginx 에서 특정 location(`/zipkin`) 으로 들어올 경우 `9411` 포트로 전달하도록 구성을 하였는데, 위와 같은 상황 때문에 해당 방식으로 구현할 수가 없었음.

#### 기타
대부분 예제에서 `@RestController` 를 사용하는데, `@Controller` 를 사용해도 문제가 없음.

#### History
- 2019.04.14 : 초안작성
