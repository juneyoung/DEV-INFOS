### ElasticSearch

#### 트러블슈팅
- 증상 1 : 구동시 `max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]` 라는 오류가 뜨며 실패
- 해결 1 : 장치에 사용가능한 가상 메모리가 부족해서 구동실패한 경우로 가상메모리 사용량을 늘려주면 해결됨. `CentOS7` 기준으로 `echo 262144 > /proc/sys/vm/max_map_count`. 숫자는 시스템에 따라 다를 수 있음

#### History
- 2017.05.10 : 초안작성
