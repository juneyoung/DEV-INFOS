### MYSQL 레퍼런스

#### 항목
- [쿼리](https://github.com/juneyoung/DEV-INFOS/blob/master/MYSQL/query.md)
- [펑션과 프로시저](https://github.com/juneyoung/DEV-INFOS/blob/master/MYSQL/plsql.md)
- [my.cnf](https://github.com/juneyoung/DEV-INFOS/blob/master/MYSQL/my.cnf.md)

#### 서비스 제어
CentOS
```
# service 명령으로 기동,정지,재시작 
$> service mysql start
$> service mysql stop
$> service mysql restart

# systemctl 명령으로 기동,정지,재시작,시작 프로그램 등록
$> systemctl mysqld start
$> systemctl mysqld stop
$> systemctl mysqld restart
$> systemctl mysqld enable
```

#### 데이터 백업과 복구
```
# 루틴을 포함하지 않고 백업 덤프 
$> mysqldump -u[사용자명] -p[비밀번호] [스키마명] > [덤프파일명]

# 루틴을 포함하여 백업 덤프
$> mysqldump -u[사용자명] -p[비밀번호] --routines [스키마명] > [덤프파일명]

# 복원
$> mysql -u[사용자명] -p[비밀번호] [스키마명] < [덤프파일명]
```

#### 서버 전체 데이터 백업과 복구 ([참조](https://stackoverflow.com/questions/9497869/export-and-import-all-mysql-databases-at-one-time))
```
# 백업 덤프
$> mysqldump -u root -p --all-databases > alldb.sql
$> mysqldump -u root -p --opt --all-databases > alldb.sql
$> mysqldump -u root -p --all-databases --skip-lock-tables > alldb.sql

# 복원
$> mysql -u root -p < alldb.sql
```

#### History
- 2017.04.29 : 초안작성
- 2017.08.28 : `서버 전체 데이터 백업과 복구` 항목 추가
