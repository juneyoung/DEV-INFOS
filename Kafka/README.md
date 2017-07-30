# Apache-Kafka setting

[메인으로](https://github.com/juneyoung/DEV-INFOS/)

### 개요

 공식에 의하면 `a distributed streaming platform`. 레코드가 생성될 때 전달할 수 있게 해준다. 메세지 큐처럼 발생하는 메세지를 스트리밍으로 밀어주는 역할. 
 
 카프카는 다수의 서버에서 클러스터로 동작하고 각 클러스터는 레코드를 `토픽(topic)` 이라는 구조로 저장함. 각각의 레코드는 `키`와 `값`, `타임스탬프`로 구성이 되어 있다.

### 제공하는 코어 API

- Producer API : 애플리케이션이 레코드 스트림을 카프카 토픽으로 발행할 수 있음
- Comsumer API : 애플리케이션이 발행된 토픽을 구독할 수 있음. 
- Streams API : 애플리케이션이 하나의 `stream processor` 로 작동할 수 있게 함
- Connector API : 카프카 토픽에 접근할 수 있는 Producer 와 Consumer 를 사용할 수 있게 함

### 구동 절차

- [다운로드](https://kafka.apache.org/quickstart)
- `$KAFKA_HOME/bin/zookeeper-server-start.sh $KAFKA_HOME/config/zookeeper.properties` : zookeeper 서버 실행
- `$KAFKA_HOME/bin/kafka-server-start.sh $KAFKA_HOME/config/server.properties` : kafka 서버 실행  


### 테스트 절차 
~~시키는대로 했는데 안됨~~


### History
- 2017.07.31 : 초안작성 
