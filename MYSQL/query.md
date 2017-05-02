### MYSQL 쿼리

#### 사용자 관련
```
# 생성하기. 접근에는 % - 전부허용, localhost - 로컬, <ip> 올 수 있음
> CREATE USER '[사용자명]'@'[접근]' IDENTIFIED BY '[비밀번호]';

# 모든 권한 주기
> GRANT ALL PRIVILEGES ON [스키마명].[테이블 ex) *] to '[사용자명]'@'[접근]';
> FLUSH PRIVILEGES;
```

#### 문자열 관련
```
# 테이블에 적용
> ALTER TABLE [테이블] CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# 칼럼에 적용
> ALTER TABLE [테이블] CHANGE [칼럼명] [칼럼명] [칼럼타입] CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```
#### 스키마 조회하기
`INFORMATION_SCHEMA` 를 참조하여 메타 정보 조회 가능함
```
# 칼럼 조회
> SELECT * FROM INFORMATION_SCHEMA.COLOUMN;

# 펑션/프로시저 조회
> SELECT * FROM INFORMATION_SCHEMA.ROUTINES;
```
#### History
- 2017.05.02 : 초안작성
