# Git 설치 (2.9.5)

1. 의존성 라이브러리

    ```bash
    yum install curl-devel
    yum install expat-devel
    yum install gettext-devel
    yum install openssl-devel
    yum install zlib-devel
    yum install perl-devel
    ```

2. download

    ```bash
    wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz
    ```

3. 압축풀기

    ```bash
    tar xvfz git-2.9.5.tar.gz
    ```

4. source directory

    ```bash
    cd git-2.9.5
    pwd #/root/git-2.9.5
    ```

5. configure 

    ```bash
    #C기반 특징
    ./configure --prefix=/usr/local/douzone2021/git #prefix : makefile만듦
    ```

6. build 

    ```bash
    #C기반 특징
    make all dox info
    ```

7. 설치

    ```bash
    make install install-doc install-html install-info

    #확인
    /usr/local/douzone2021/git/bin/git --version
    ```

8. 설정(/etc/profile)

    ```bash
    vi /etc/profile
    ####################
    #git
    export PATH=$PATH:/usr/local/douzone20201/git/bin
    #####################
    source /etc/profile

    #확인
    git --version
    #git version 1.8.3.1
    ```

9. git 환경 설정

    ```bash
    git config --global user.name "mong-head"
    git config --global user.email "camara1melon315@gmail.com"
    ```

10. 연습

    ```bash
    mkdir centos-practices
    cd centos-practices
    git init
    echo "# CentOS Practices" > README.md
    git add .
    git commit -m "first commit"
    git push -u origin master

    git clone (javastudy repository url)
    ```