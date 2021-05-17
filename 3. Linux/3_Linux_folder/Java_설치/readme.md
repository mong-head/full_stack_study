# Java 설치

1. Java JDK download (oracle가서 다운로드)
2. linux server에 upload

    ```bash
    #XShell에서...(연결된 거 있으면 연결끊고 시작)
    cd E:\배경화면\STUDY\DOUZONE\03.자료
    sftp webmaster@192.168.254.40
    put jdk-8u291-linux-x64.tar.gz

    #ssh webmaster@IP 접속 후 su - 해서 root계정 로긴
    cd /home/webmaster
    mv jdk-8u291-linux-x64.tar.gz /root
    cd ~
    tar xvfz jdk-8u291-linux-x64.tar.gz #압축해제
    ```

3. 더존 소프트웨어 설치 디렉토리 만들기

    ```bash
    mkdir -p /usr/local/douzone2021/java1.8
    mkdir -p /usr/local/douzone2021/git
    mkdir -p /usr/local/douzone2021/mariadb
    ```

4. 설치

    ```bash
    cd ~
    mv jdk1.8.0_291 /usr/local/douzone2021/java1.8
    ```

5. 링크 파일 생성(버전관리)

    ```bash
    # link ; update생길 수 있음(java1.9가 생길 수 있음)
    cd /usr/local/douzone2021
    ln -s java1.8 java #java로 링크달기
    #lrwxrwxrwx.  1 root root    7  5월 11 01:48 java -> java1.8
    # java1.9가 생기면 java링크만 옮기면 됨
    ```

6. 설정 (/etc/profile) ; 환경변수

    java쓰기 쉽도록 path잡아줌

    밑 코드 profile에 추가하기

    ```bash
    # java
    export JAVA_HOME=/usr/local/douzone2021/java
    export CLASSPATH=/usr/local/douzone2021/java/lib/tools.jar
    export PATH=$PATH:$JAVA_HOME/bin
    ```

7. 현재 shell 환경에 적용하기

    ```bash
    source /etc/profile
    ```

8. 확인

    ```bash
    java -version

    #java version "1.8.0_291"
    #Java(TM) SE Runtime Environment (build 1.8.0_291-b10)
    #Java HotSpot(TM) 64-Bit Server VM (build 25.291-b10, mixed mode)
    #[root@localhost douzone2021]# cd ~
    #[root@localhost ~]# java -version
    #java version "1.8.0_291"
    #Java(TM) SE Runtime Environment (build 1.8.0_291-b10)
    #Java HotSpot(TM) 64-Bit Server VM (build 25.291-b10, mixed mode)
    ```