# 슬로우 쿼리 설정

#### 개요
slow-query 는 시간이 오래 걸리는 쿼리를 찾아 로그를 쌓는 작업이다. 튜닝이 필요한 쿼리를 알 수 있다.
`[mysqld]` 아래에 작성하도록 한다.

#### 항목
- `slow_query_log` : 디폴트는 꺼져있다. `1` 은 사용, `0` 은 미사용
- `long_query_time` : slow-qury 로 판단할 기준을 정한다. 단위는 초.
- `slow_query_log_file` : 명시적으로 경로를 지정할 수 있음.
