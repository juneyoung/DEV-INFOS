# Logback 을 이용하여 Logstash 연동하기

[Logstash 항목으로](https://github.com/juneyoung/DEV-INFOS/edit/master/ELK/LogStash)

#### 개요
`tcp` 프로토콜을 이용하여 로그스태시로 전송

#### 0. `build.gradle` 에 `logstash logback encoder` 추가 (애플리케이션 서버)
```
#dependencies 항목 아래에 밀어넣는다
compile('net.logstash.logback:logstash-logback-encoder:4.8+')
```

#### 1. `spring-boot` `application.yml` 에 `logback` 새팅 (애플리케이션 서버)
`yml` 형식에서 tab 을 구분자로 인지하지 않으니 유의
```
# 아래 항목을 추가한다
logging:
  config:
    - classpath: logback.xml
```

#### 2. `classpath` 경로의 `logback.xml` 에 아래와 같이 설정한다 (애플리케이션 서버)
```
<appender name="STASH" class="net.logstash.appender.LogstashTcpSocketAppender">
  <destination>${yourLogstashUrl:youLogstashPort}</destination>
  <encoder class="net.logstash.logback.encoder.LogstashEncoder" />
  <reconnectionDelay>1 seconde</reconnectionDelay>
</appender>

<root level="${logLevel}">
  <!-- 위에 설정한 appender 의 name 에 맵핑 -->
  <appender-ref ref="STASH"/>
</root>
```

#### 3. `logstash` 설정 (로그스태시 서버)
- `LogstashEncoder` 로 넘어오는 데이터의 `codec` 은 `json_lines` 가 아니다.(이 경우 `json_parsefailure[0]` 이라는 메세지가 출력되며 로그가 제대로 쌓이지 않음)
- `output` 항목에 `elasticseash` 를 넣어서 전달받은 로그를 쌓아 `Kibana` 에서 참조 가능
```
input {
  tcp {
    port => 5000
    codec => multiline {
      pattern => "^{"
      negate => "true"
      what => "previous"
    }
  }
}

filter {
  json {
    source => "message"
  }
}

output {
  elasticsearch {
    hosts => ['localhost:9200']
    index => 'logstash-%{+YYYY.MM.dd}'
  }
  stdout { codec => rubydebug }
}
```

#### 참고 항목
[로그스태시-로그백 인코더 공식 가이드](https://github.com/logstash/logstash-logback-encoder)

#### History
- 2017.06.20 : 초안작성
