# MariaDB 설치

1. 의존 라이브러리 설치

    ```bash
    #root 계정, root directory 작업
    #ncurses : 화면 커서 제어 라이브러리(이쁘게 만들어주는거)
    yum install gcc -y
    yum install gcc-c++ -y
    yum install libtermcap-devel -y
    yum install gdbm-devel -y
    yum install zlib* -y
    yum install libxml* -y
    yum install freetype* -y
    yum install libpng* -y
    yum install flex -y
    yum install gmp -y
    yum install ncurses -y
    yum install cmake.x86_64 -y
    yum install libaio -y

    #yum install iconv -y
    wget https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.16.tar.gz
    cd /lib
    ./configure --prefix=/usr/local
    make
    make install
    ```

2. 소스 다운로드

    ```bash
    #mariadb source download
    #10.1 version download
    wget https://downloads.mariadb.org/interstitial/mariadb-10.1.48/source/mariadb-10.1.48.tar.gz/from/https%3A//mirror.yongbok.net/mariadb/
    ```

3. 이름변경 및 압축해제

    ```bash
    mv index.html mariadb-10.1.48.tar.gz
    tar xvfz mariadb-10.1.48.tar.gz
    ```

4. 소스 이동

    ```bash
    cd mariadb-10.1.48
    ```

5. 빌드 환경 설정

    ```bash
    cmake -DCMAKE_INSTALL_PREFIX=/usr/local/douzone2021/mariadb -DMYSQL_USER=mysql -DMYSQL_TCP_PORT=3307 -DMYSQL_DATADIR=/usr/local/douzone2021/mariadb/data -DMYSQL_UNIX_ADDR=/usr/local/douzone2021/mariadb/tmp/mariadb.sock -DINSTALL_SYSCONFDIR=/usr/local/douzone2021/mariadb/etc -DINSTALL_SYSCONF2DIR=/usr/local/douzone2021/mariadb/etc/my.cnf.d -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci -DWITH_EXTRA_CHARSETS=all -DWITH_ARIA_STORAGE_ENGINE=1 -DWITH_XTRADB_STORAGE_ENGINE=1 -DWITH_ARCHIVE_STORAGE_ENGINE=1 -DWITH_INNOBASE_STORAGE_ENGINE=1 -DWITH_PARTITION_STORAGE_ENGINE=1 -DWITH_BLACKHOLE_STORAGE_ENGINE=1 -DWITH_FEDERATEDX_STORAGE_ENGINE=1 -DWITH_PERFSCHEMA_STORAGE_ENGINE=1 -DWITH_READLINE=1 -DWITH_SSL=bundled -DWITH_ZLIB=system
    ```

6. 빌드 및 설치

    ```bash
    #build
    make
    #설치
    make install
    ```

7. 계정 생성

    ```bash
    #root계정, root디렉토리
    cd

    groupadd mysql
    useradd -M -g mysql mysql #-M : home directory만들지 말고
    ```

8. install directory 소유자 변경

    ```bash
    chown -R mysql:mysql /usr/local/douzone2021/mariadb
    ```

9. 설정 파일 위치 변경

    ```bash
    cp -R /usr/local/douzone2021/mariadb/etc/my.cnf.d /etc
    ```

10. 기본(관리) DB(mysql) 생성
    - mysqld : DB관리 및 쿼리 보내기 등등
        - mysql : 시스템 DB (관리용) → 생성
        - webdb
        - ...

    ```bash
    /usr/local/douzone2021/mariadb/scripts/mysql_install_db --user=mysql --basedir=/usr/local/douzone2021/mariadb --defaults-file=/usr/local/douzone2021/mariadb/etc/my.cnf --datadir=/usr/local/douzone2021/mariadb/data
    ```

11. 서버 구동

    ```bash
    #백그라운드에서 실행
    /usr/local/douzone2021/mariadb/bin/mysqld_safe &

    #확인
    ps -ef | grep mysql
    ```

12. root password설정

    ```bash
    /usr/local/douzone2021/mariadb/bin/mysqladmin -u root password "비밀번호"
    ```

13. 데이터베이스 접속 test

    ```bash
    /usr/local/douzone2021/mariadb/bin/mysql -u root -p
    ```

14. path 설정

    ```bash
    vi /etc/profile
    #################################
    # mysql
    export PATH=$PATH:/usr/local/douzone2021/mariadb/bin
    #################################
    source /etc/profile

    # mysql실행해보기
    mysql -u root -p
    # mysql db 사용
    use mysql
    ```

15. service 등록 (daemon등록) 및 시작

    ```bash
    # root 계정, /root에서 하기; 밑은 확인
    whoami #root
    pwd #/root

    # 예전 스크립트 사용 (mariadb는 현재 예전 방식 지원)
    	# 참고 : 요즘 방식 - system에 service file저장
    	#cd /usr/lib/systemd/system
    	#vi tomcat.service # 확인
      #systemctl enable mariadb #centos7이상인 경우 사용
    #init.d 에 가져다가 놓기
    cp /usr/local/douzone2021/mariadb/support-files/mysql.server /etc/init.d/mariadb
    chkconfig mariadb on #check config #centos7미만인 경우 사용
    	#systemctl enable mariadb #centos7이상인 경우 사용

    # service 시작
    systemctl start mariadb

    #확인; 프로세스 명은 mysql
    systemctl status mariadb
    ps -ef | grep mysql

    mysql -u root -p

    # service 중지
    systemctl stop mariadb

    #다시 시작
    sync
    sync
    reboot

    # 서비스 되는 지 확인
    ps -ef | grep mysql
    ```