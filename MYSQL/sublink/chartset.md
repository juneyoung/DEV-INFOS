### 문자열 설정

#### 개요
기본적으로 다국어 서비스를 고려한다면 `utf8` 캐릭터를 사용해야 한다. 추가로 모바일 환경을 통한 이모티콘 정보를 수정하기 위해서는 `utf8mb4` 사용해야 하는데, `utf8` 이 한 글자를 3 바이트로 처리하는데 비해 `utf8mb4` 는 4 바이트로 처리하므로 스키마 전체를 `utf8mb4` 로 처리하기보다는 필요 테이블, 칼럼 단위로 적용하자.

#### 항목
- `[mysql]` 아래 : `default-character-set`
- `[mysqld]` 아래 : `character-set-server`, `collation-server`
- `[mysqldump]` 아래 : `default-character-set
- `[client]` 아래 : `default-character-set`

#### 곁가지
- [칼럼, 테이블 캐릭터셋 쿼리]() 
