### 마리아 DB 설치
  

- - -
맥에서는 홉브루를 통해 설치한다  

    $brew update
    $brew install mariadb



홈브루를 통해 설치해서 아래와 같은 명령어를 통해 상태 확인

    $brew services start mariadb  
    $brew services stop mariadb  
    $brew services list  


`$mysql -uroot` db에 접속한다

Access denied for user ‘root’@’localhost’ 오류 발생시

```
sudo mariadb-secure-installation  
mysql -uroot -p
```
root 비밀번호 초기화


GUI툴로 window에선 heidiSQL을 쓰지만 맥에선 work bench 사용
* * *
<br>

### 유저 생성

제일 먼저 root 계정으로 접속한다

```
--user 확인
--table에 query를 실행하려면 먼저 database 사용 명령어 실행해야한다
use mysql;
select user from user;

--데이터베이스 생성 및 확인
create database user05;
show databases;

-- user 생성
create user 'user05'@'localhost' identified by 'user05';
create user 'user05'@'%' identified by'user05';

-- 권한 적용3
grant all privileges on user05.* to 'user05'@'%';
grant all privileges on user05.* to 'user05'@'localhost';

flush privileges;
commit;
```


오라클에서는 파일 형태로 
MYsql은 폴더 형식으로 구분 ←폴더를 데이터베이스라고 부른다

각 유저들이 다른 유저들의 데이터 접근 못하게 하기 위해 폴더(db)를 만들고 그 폴더 안(db)에서 테이블을 만들어준다   

user01 @ % 여기서 %는 호스트라 부른다 유저가 로컬에서만 접근할지 네트워크 허용 할것인지 결정한다. %는 외부 모든 ip를 의미. %자리엔 localhost, 특정아이피가 온다
