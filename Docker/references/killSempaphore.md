[Docker 항목으로](https://github.com/juneyoung/DEV-INFOS/tree/master/Docker)

아래에서 보다시피 `dmsetup udevcomplete_all` 명령 이후에 비정상 장비가 모두 리셋됨 

```
[root@DCSF-DEV08 sendmail_test]# docker ps -a
CONTAINER ID        IMAGE                COMMAND                  CREATED             STATUS                     PORTS                                                                                                  NAMES
f03377cedb2c        redmine              "/docker-entrypoin..."   3 days ago          Up 2 days                  0.0.0.0:9809->3000/tcp                                                                                 redmine
babbb251c325        ion-elk              "/usr/local/bin/st..."   7 weeks ago         Exited (255) 6 weeks ago   0.0.0.0:5000-5001->5000-5001/tcp, 0.0.0.0:5601->5601/tcp, 5044/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   ion-elk
19e19db08bdf        ion-apifarm2         "/usr/sbin/init"         3 months ago        Exited (255) 6 weeks ago   9800/tcp                                                                                               testfarm
8b950a19145f        sebp/elk             "/usr/local/bin/st..."   3 months ago        Exited (0) 7 weeks ago                                                                                                            elk
3a8011af2cf1        40d61ab32184         "/usr/sbin/init"         3 months ago        Exited (137) 7 weeks ago   0.0.0.0:9800->9800/tcp                                                                                 ion-apifarm
74d13646e12c        be9cb076cb63         "/bin/tini -- /usr..."   3 months ago        Up 4 days                  0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp                                                       ion-jenkins
ecdbb884fbdd        gitlab/gitlab-ce     "/assets/wrapper"        3 months ago        Up 4 days (healthy)        0.0.0.0:8322->22/tcp, 0.0.0.0:8300->80/tcp, 0.0.0.0:8343->443/tcp                                      gitlab
618401b5f4a1        sonarqube            "./bin/run.sh"           3 months ago        Exited (255) 2 weeks ago   0.0.0.0:9000->9000/tcp, 0.0.0.0:9092->9092/tcp                                                         sonarqube
3dba2ba66d9d        mysql/mysql-server   "/entrypoint.sh my..."   3 months ago        Up 3 days                  0.0.0.0:3306->3306/tcp, 33060/tcp                                                                      mysql
94ba05856f5d        sonatype/nexus3      "bin/nexus run"          3 months ago        Exited (255) 6 weeks ago   0.0.0.0:9700->8081/tcp                                                                                 nexus
[root@DCSF-DEV08 sendmail_test]# docker start ion-elk
Error response from daemon: devmapper: Error activating devmapper device for '4ad92a72cd952463700593f3cac71d961d35e3257ad59d409afddeed005e7705': devicemapper: Can't set cookie dm_task_set_cookie failed
Error: failed to start containers: ion-elk
[root@DCSF-DEV08 sendmail_test]# echo 'y' | sudo dmsetup udevcomplete_all
This operation will destroy all semaphores with keys that have a prefix 3405 (0xd4d).
Do you really want to continue? [y/n]: 128 semaphores with keys prefixed by 3405 (0xd4d) destroyed. 0 skipped.


[root@DCSF-DEV08 sendmail_test]# docker ps -a
CONTAINER ID        IMAGE                COMMAND                  CREATED             STATUS                     PORTS                                                               NAMES
f03377cedb2c        redmine              "/docker-entrypoin..."   3 days ago          Up 2 days                  0.0.0.0:9809->3000/tcp                                              redmine
babbb251c325        ion-elk              "/usr/local/bin/st..."   7 weeks ago         Exited (255) 6 weeks ago                                                                       ion-elk
19e19db08bdf        ion-apifarm2         "/usr/sbin/init"         3 months ago        Exited (255) 6 weeks ago   9800/tcp                                                            testfarm
8b950a19145f        sebp/elk             "/usr/local/bin/st..."   3 months ago        Exited (0) 7 weeks ago                                                                         elk
3a8011af2cf1        40d61ab32184         "/usr/sbin/init"         3 months ago        Exited (137) 7 weeks ago   0.0.0.0:9800->9800/tcp                                              ion-apifarm
74d13646e12c        be9cb076cb63         "/bin/tini -- /usr..."   3 months ago        Up 4 days                  0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp                    ion-jenkins
ecdbb884fbdd        gitlab/gitlab-ce     "/assets/wrapper"        3 months ago        Up 4 days (healthy)        0.0.0.0:8322->22/tcp, 0.0.0.0:8300->80/tcp, 0.0.0.0:8343->443/tcp   gitlab
618401b5f4a1        sonarqube            "./bin/run.sh"           3 months ago        Exited (255) 2 weeks ago   0.0.0.0:9000->9000/tcp, 0.0.0.0:9092->9092/tcp                      sonarqube
3dba2ba66d9d        mysql/mysql-server   "/entrypoint.sh my..."   3 months ago        Up 3 days                  0.0.0.0:3306->3306/tcp, 33060/tcp                                   mysql
94ba05856f5d        sonatype/nexus3      "bin/nexus run"          3 months ago        Exited (255) 6 weeks ago   0.0.0.0:9700->8081/tcp                                              nexus



```
