### 이노디비 새팅

#### 개요
데이터베이스에 데이터가 쌓이면 이에 비례해서 `ibdata1` 파일의 크기도 늘어난다. 데이터가 늘어났을 경우를 가정해 미리 파일 시스템을 분리하도록 한다.

#### 항목
- `innodb_data_file_path` : 이노디비 파일을 명시한다. 복수로 명시할 수 있고, 용량도 줄 수 있다. `autoextend` 는 자동으로 늘어나는 옵션이다. 사용법 `<파일명1>:<용량>;<파일명2>:autoextend`
- `innodb_data_home_dir` : 이노디비 파일의 홈 디렉토리
- `innodb_log_group_home_dir` : 이노디비 파일 그룹 디렉토리
- `innodb_write_io_threads`
- `innodb_read_io_threads`
- `innodb_thread_concurrency`
- `innodb_flush_log_at_trx_commit`
- `innodb_log_buffer_size`
- `innodb_log_file_size`
- `innodb_log_files_in_group`
- `innodb_max_dirty_pages_pct`
- `innodb_lock_wait_timeout`
