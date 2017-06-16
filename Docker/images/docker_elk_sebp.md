# Docker ELK (elk/sebp)

[메인으로 가기](https://github.com/juneyoung/DEV-INFOS/tree/master/Docker)

### 0. 공통

##### 공식 이미지를 사용하지 않는 이유

- Docker hub 의 elastic.co 이미지들이 deprecated 되었기 때문임
- 대체가 있긴한데, 설치가 복잡하고 네트워크 설정이 번거로움

##### 기본 설정

이미지가 뜰 때, 자동으로 elk 가 실행됨. 

- `/etc/init.d` 안에 `kibaba`, `logstash`, `elasticsearch` 파일 안에 변수로 설정 경로, 홈 경로, 로그 경로가 들어가 있음 
- 때문에 `시스템 home/conf` 폴더 안에서 변경해도 다른 곳에 커스텀 설정이 되어 있다면서 적용이 안됨.
- 아래는 시스템 별 기본 경로 (좌우 스크롤) 

| System  | *_HOME  | CONF  | DATA  | LOG  |
|---|---|---|---|---|
| Elasticsearch  | `/opt/elasticsearch`  | `/etc/elasticsearch`  | `/var/lib/elasticsearch`  | `/var/log/elasticsearch`  |
| Logstash  | `/opt/logstash`  | `/etc/logstash/conf.d`  |   | `var/log/logstash`  |
| Kibana  | `/opt/kibana`  |   |   |  `var/log/kibana` |


### 1. Elasticsearch

기본 container 에서 사용하는 port 는 `9200`

- Elasticsearch 에서 사용하는 데이터 구조는 `Index` > `Type` > `Document` 순
- 인덱스 목록 조회 방법 (Url) : `{Elastic url}/_cat/indices?v`
- 인덱스 정보 조회 방법 (Url) : `{Elastic url}/{Index}`


### 2. Logstash

로그 스태시에 데이터를 쌓기 위해서는 `input`, `output` 설정이 필수. `filter` 는 옵션인 듯하고, `grok` 은 플러그인일 뿐

- 기본 IO 설정은 `/etc/logstash/conf.d` 에 IO 별로 분리된 `*.conf` 파일임
- 파일은 분할해도 좋고 하나로 써도 좋음
- 데이터가 안들어갈 때는 `/var/log/logstash/logstash.stdout` 파일을 보면 어느 부분에서 오류가 발생했는지 찾기 용이함
- 설정 변경 후에는 `/etc/init.d` 폴더에 가서 `logstasg {start/stop/restart}` 로 재시작 해주어야 함
- 아래는 파일로 떨어진 json 을 읽어서(input) 엘라스틱서치의 `elk-{날짜}` 라는 인덱스로 보내는 conf 파일의 예시
```
// 멀티라인 json 처리와 싱글라인 json 의 처리가 다르니 유의할 것 
input {
  file {
    codec => multiline {
      pattern => '}'
      negate => true
      what => previous
    }
    path => '/etc/logstash/logs/log*.json'
  }
}

filter {
  json {
    source => 'message'
  }
}

output {
  elasticsearch {
    hosts => ['localhost:9200']
    index => 'elk-%{+YYYY.MM.dd}'
    document_type => 'log'
  }
  stdout { codec => rubydebug }
}

```


### 3. Kibana

기본 포트는 `5601`. 엘라스틱 서치의 데이터를 관리자가 시각적으로 관리할 수 있도록 도와주는 툴


- 처음 바운드시 UI 만 출력되고  default 인덱스가 설정되지 않았다는 경고 출력.
- 아무 인덱스나 기본적으로 넣어주면 `timeline` 이나 `discover` 메뉴에 노출됨. 



### *. History

- 17.06.14 : 초안작성
