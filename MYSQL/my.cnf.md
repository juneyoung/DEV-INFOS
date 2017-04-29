### MYSQL my.cnf 작성하기

#### 문서의 목적
MYSQL 을 관리적 목적에서 제어하기 위해서는 `my.cnf` 파일을 다룰 줄 알아야 하는데,
영어 읽기는 귀찮고 한국어로 자세하게 매뉴얼이 제공되어 있지는 않아 경험한 부분을 남기는 방법을 택했음.
하기 항목을 모두 적용할 필요는 없고, 그 때 상황에 맞게 사용하면 되겠다.

```
[client-server]

!includedir /etc/my.cnf.d

[client]
default-character-set = utf8mb4

[mysqld]
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
wait_timeout = 120
skip-name-resolve

back_log = 70
max_connections = 400


table_open_cache = 2048

max_allowed_packet = 16M

binlog_cache_size = 1M

max_heap_table_size = 64M

read_buffer_size = 4M

read_rnd_buffer_size = 8M

sort_buffer_size = 16M

join_buffer_size = 8M
thread_cache_size = 8

query_cache_size = 128M
query_cache_limit = 2M
ft_min_word_len = 4

transaction_isolation = READ-COMMITTED
tmp_table_size = 64M

slow_query_log = 1
long_query_time = 3



#*** MyISAM Specific options
key_buffer_size = 32M
bulk_insert_buffer_size = 64M

myisam_sort_buffer_size = 128M
myisam_max_sort_file_size = 10G
myisam_repair_threads = 1
myisam_recover

#*** InnoDB Specific options

innodb_buffer_pool_size = 5G

innodb_data_file_path = ibdata1:10M:autoextend
innodb_data_file_path = ibdata1:500M;ibdata2:500M;ibdata3:500M;ibdata4:500M;ibdata5:500M;ibdata6:500M;ibdata7:500M;ibdata8:500M;ibdata9:500M;ibdata10:500M;ibdata11:200M:autoextend

innodb_data_home_dir = /var/lib/mysql/innoDB/
innodb_write_io_threads = 8
innodb_read_io_threads = 8
innodb_thread_concurrency = 16
innodb_flush_log_at_trx_commit = 1 
innodb_log_buffer_size = 8M
innodb_log_file_size = 400M
innodb_log_files_in_group = 3
innodb_log_group_home_dir = /var/lib/mysql/innoDB/
innodb_max_dirty_pages_pct = 80
innodb_lock_wait_timeout = 50


[mysqldump]
default-character-set = utf8mb4
quick

max_allowed_packet = 16M

[mysql]
default-character-set = utf8mb4
no-auto-rehash

[myisamchk]
key_buffer_size = 512M
sort_buffer_size = 512M
read_buffer = 8M
write_buffer = 8M

[mysqlhotcopy]
interactive-timeout

[mysqld_safe]
open-files-limit = 8192
```
##### 항목별
- [문자열](https://github.com/juneyoung/DEV-INFOS/blob/master/MYSQL/sublink/chartset.md)
- [패킷](https://github.com/juneyoung/DEV-INFOS/blob/master/MYSQL/sublink/packet.md)
- [이노디비](https://github.com/juneyoung/DEV-INFOS/blob/master/MYSQL/sublink/innodb.md)
- [슬로우쿼리](https://github.com/juneyoung/DEV-INFOS/blob/master/MYSQL/sublink/slowquery.md)

#### History
- 2017.04.29. 초안작성
