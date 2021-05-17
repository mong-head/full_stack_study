# Tomcat 설치

1. tomcat8 download

    ```bash
    su -
    cd
    wget https://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.5.65/bin/apache-tomcat-8.5.65.tar.gz
    ```

2. 압축 풀기

    ```bash
    tar xvfz apache-tomcat-8.5.65.tar.gz 
    ```

3. 설치

    ```bash
    mv apache-tomcat-8.5.65 /usr/local/douzone2021/tomcat8.5
    ln -s /usr/local/douzone2021/tomcat8.5 /usr/local/douzone2021/tomcat #버전관리 관련
    ```

4. 설정 (/etc/profile , 안함)
5. 포트확인

    ```bash
    vi /usr/local/douzone2021/tomcat/conf/server.xml

    #8080 open 확인(8080이면 별 다른 편집없이 끝냄)
    ```

6. 실행

    ```bash
    /usr/local/douzone2021/tomcat/bin/catalina.sh start
    #켜졌는 지 확인
    ps -ef | grep tomcat
    ps -ef | grep java
    ```

7. 브라우저로 접근

    http://192.168.80.131:8080

8. 중지 시키기

    ```bash
    /usr/local/douzone2021/tomcat/bin/catalina.sh stop
    #꺼졌는 지 확인
    ps -ef | grep tomcat
    ps -ef | grep java
    ```

9. 서비스 등록하기

    ```bash
    #매번 catalina.sh start하지 않고, systemctl로 실행가능하도록 만듦
    vi /usr/lib/systemd/system/tomcat.service
    ################################
    [Unit]
    Description=tomcat7
    After=network.target syslog.target

    [Service]
    Type=forking

    Environment=JAVA_HOME=/usr/local/douzone2021/java
    User=root
    Group=root

    ExecStart=/usr/local/douzone2021/tomcat/bin/startup.sh
    ExecStop=/usr/local/douzone2021/tomcat/bin/shutdown.sh

    UMask=0007
    RestartSec=10
    Restart=always

    [Install]
    WantedBy=multi-user.target
    ##################################
    systemctl enable tomcat
    ```

10. tomcat service 실행,중지,재실행

    ```bash
    systemctl start tomcat
    systemctl stop tomcat
    systemctl restart tomcat
    ```

11. tomcat manager 설정

    1) tomcat-users.xml 설정

    ```bash
    vi /usr/local/douzone2021/tomcat/conf/tomcat-users.xml
    ####################################
    <tomcat-users>
      . . .
      . . . 
      <role rolename="manager"/>
      <role rolename="manager-gui" />
      <role rolename="manager-script" />
      <role rolename="manager-jmx" />
      <role rolename="manager-status" />
      <role rolename="admin"/>
      <user username="admin" password="manager" roles="admin,manager,manager-gui, manager-script, manager-jmx, manager-status"/>

    </tomcat-users>
    ####################################
    ```

    2) context.xml 설정

    ```bash
    #주석 처리
    <Context>
     ....
    </Context>

    #새로 다음내용 추가
    <Context antiResourceLocking="false" privileged="true" docBase="${catalina.home}/webapps/manager">
      <Valve className="org.apache.catalina.valves.RemoteAddrValve"
             allow="^.*$" />
    </Context>
    ```

12. tomcat 재시작

```bash
systemctl stop tomcat
ps -ef | grep tomcat
systemctl start tomcat
```

13. [https://192.168.254.40:8080/manager](https://192.168.254.40:8080/manager) 잘 동작하는 지 보기

id : admin, password : manager