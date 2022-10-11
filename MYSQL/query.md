### MYSQL 쿼리

#### 사용자 관련
```sql
# 생성하기. 접근에는 % - 전부허용, localhost - 로컬, <ip> 올 수 있음
> CREATE USER '[사용자명]'@'[접근]' IDENTIFIED BY '[비밀번호]';

# 모든 권한 주기
> GRANT ALL PRIVILEGES ON [스키마명].[테이블 ex) *] to '[사용자명]'@'[접근]';
> FLUSH PRIVILEGES;
```

#### 문자열 관련
```sql
# 테이블에 적용
> ALTER TABLE [테이블] CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# 칼럼에 적용
> ALTER TABLE [테이블] CHANGE [칼럼명] [칼럼명] [칼럼타입] CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```
#### 스키마 조회하기
`INFORMATION_SCHEMA` 를 참조하여 메타 정보 조회 가능함
```sql
# 칼럼 조회
> SELECT * FROM INFORMATION_SCHEMA.COLOUMN;

# 펑션/프로시저 조회
> SELECT * FROM INFORMATION_SCHEMA.ROUTINES;
```

#### 동시 접근을 제어하기 위한 Read lock, Write lock
lock 은 레코드 단위로 걸 수 있다. 아래와 같은 경우 락을 사용한다
- 쓰기가 오랜 시간이 걸리는데, 읽을 때 데이터는 항상 온전해야 하는 경우
- table lock 은 별도로 있다 - 전체가 잠기므로 자제 요망
- LOCK 명령어는 테이블, FOR SHARE/FOR UPDATE 는 레코드 단위

```sql
# auto commit 은 false로 해둔다. commit 을 하는 순간 잡은 lock 을 해제한다

# 이 경우 read lock 을 취득하며, 쓰기 연산을 막는다
# SHARED LOCK 이 취득한 경우, EXCLUSIVE LOCK 을 얻을 수 없기 때문이다
SELECT a_field FROM a_table FOR SHARE

# 이 경우 write lock 을 취득하며, 읽기 시 락을 취득하지 못했다는 오류를 발생시킨다
SELECT a_field FROM a_table FOR UPDATE

# table lock
LOCK TABLE a_table READ;
LOCK TABLE a_table WRITE;
```

#### History
- 2017.05.02 : 초안작성
- 2022.10.11 : LOCK 추가
