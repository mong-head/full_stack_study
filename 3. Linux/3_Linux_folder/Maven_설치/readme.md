# Maven 설치

- maven : java build tool
- server : git으로 소스 다운 후 pom.xml가 있으면 maven으로 build하여 jar등의 파일을 만듦

1. maven download

    ```bash
    # /root에서 작업
    wget https://mirror.navercorp.com/apache/maven/maven-3/3.8.1/binaries/apache-maven-3.8.1-bin.tar.gz
    ```

2. 압축 풀기

    ```bash
    tar xvfz apache-maven-3.8.1-bin.tar.gz
    ```

3. 설치

    ```bash
    mv apache-maven-3.8.1 /usr/local/douzone2021/maven3.8
    # 확인 (douzone은 루트에서 링크로 걸어놓았음)
    /douzone/maven/bin/mvn -version
    ```

4. 링크 걸기 (버전관리)

    ```bash
    cd /usr/local/douzone2021
    ln -s maven3.8 maven
    ```

5. 설정(/etc/profile)

    ```bash
    vi /etc/profile
    ######################추가
    # maven
    export PATH=$PATH:/usr/local/douzone2021/maven/bin
    ######################

    #적용
    source /etc/profile
    ```

6. 실행해보기

    ```bash
    #git으로 maven project(java)받아오기
    git clone ~~
    #git pull ~~
    #나는 javastudy가 그 파일
    cd /dowork/javastudy

    #jar/war만들기
    mvn clean package 
    #jar 확인
    ls -l /network/target
    #실행 (cp : classpath)
    java -cp network/target/network-0.0.1-SNAPSHOT.jar httpd.SimpleHttpServer

    # cf) Jenkins : git pull, mvn clean package등등 코드 내려받고 빌드하는 귀찮은 과정 편하게 만들어 준 것 
    ```