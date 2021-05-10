### 미리아 DB 
 - - - 

1. 관계형 데이터베이스 SQL이다
2. MYsql이 오라클에 팔리자 개발자들이 오픈소스로 만들고자 나와서 만든것  
<br>


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
