### `server.xml` 처리하기

#### 개요
운영 배포 간 필요한 `server.xml`의 변경사항을 기술 

#### port 변경하기 
가장 기본적인 설정만을 사용했을 때, `AJP`, `http`, `shutdown` 용으로 포트가 3개 필요함.
`netstat -an` 으로 사용중이지 않은 포트를 `Connector` 항목에 넣으면 됨.
`redirectPort` 는 겹쳐도 무관한 모양.
```
<Server port="8005" shutdown="SHUTDOWN">
    
    ...
    
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
   
    ...
    
    <Connector port="8009" protocol="AJP/1.3" 
               redirectPort="8443" />
</Server>
```

#### Encoding 변경하기
서버를 올렸는데 `UTF-8` 문자열이 깨질 경우, `server.xml` 에서 새팅할 수 있다.
```
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" 
               URIEncoding="UTF-8"/>
    
    <Connector port="8009" protocol="AJP/1.3" 
               redirectPort="8443" 
               URIEncoding="UTF-8"/>
```

#### HTTPS 프로토콜 새팅
```
    <!-- #1. 기본으로 제공되는 새팅 -->
    <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <SSLHostConfig>
            <Certificate certificateKeystoreFile="conf/localhost-rsa.jks"
                         type="RSA" />
        </SSLHostConfig>
    </Connector>

    <!-- #2. 사용했었던 새팅 -->
    <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true"
               schema="http" 
               secure="true"
               clientAuth="false"
               sslProtocol="TLS"/>
```
주석 해제하면 됨


#### History
- 2017.05.02 : 초안작성
