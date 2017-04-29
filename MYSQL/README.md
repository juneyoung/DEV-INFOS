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

#### History
- 2014.04.29 : 초안작성
