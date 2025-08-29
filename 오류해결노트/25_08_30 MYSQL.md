## 초기설치 시도 및 PHP5 패키지 오류
- `g++`,`libmysql++dev`,`php5`,`apache2`,`mysql-server`,`php5-mysql` 중에서
- `php5-mysql` 등은 공식 저장소에 없어서 오류 발생.
- 차선책으로 `php 최신버전`을 가져왔으나 `libmariadb-dev`와 `libmysqlclient-dev` 충돌 종속성 오류 발생.

## 종속성 오류
- `mysql-server` 설치가 중단되었다.
- 이전 MariaDB를 설치하려다 남은 잔여 파일 때문이다.
- `sudo systemctl start mysql` 명령어가 실패하였다.
- `systemctl status` 로그를 통해서 MYSQL 시작 전 데이터디렉터리(var/lib/mysql) 초기화 단계에서 오류가 발생하였음을 확인하였다.

# 반복 변수 오류 해결
- 데이터 디렉터리 초기화를 위해 `sudo mysqld --initialize` 명령어를 사용하려하였다.
> /etc/mysql/mariadb.conf.d/ 디렉터리에서 알수없는 변수를 삭제하여도
> `sudo grep -r "provider_bzip2" /etc/`
> `sudo grep -r "provider_lz4" /etc/`
> `sudo grep -r "provider_lzma" /etc/` 식으로 계속 알수없는 변수가 계속 나타나서,
- `sudo apt-get purge mariadb-*` 명령어로 관련패키지와 설정 파일까지 모두 삭제하였다.
- 위 단계를 거쳐 충돌을 일으키는 모든 파일을 정리한 후에야 MYSQL 데이터 디렉터리를 초기화할 수 있었고
- MYSQL 서버를 성공적으로 실행할 수 있었다.
