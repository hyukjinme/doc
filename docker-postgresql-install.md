# Docker & PostgreSQL 설치 

- pre-install
  - Docker
  - DBveaver



## docker 설치 

[download](https://www.docker.com/)


##  컨테이너 생성하기 
```
docker run -p 54320:5432 -v C:\docker_postgresql_dev_volume:/home/workspace -e POSTGRES_PASSWORD=asd123!@# --name postgresdev -d postgres
```

-p : 포트, 클라이언트 포트(현재PCOS) : 서버포트(컨테이너), 여러개 입력가능

-v : 볼륨, 파일공유할 수 있습니다. 클라이언트경로:서버경로 

-e : 환경변수(도커허브 이미지 참조)

(참고)컨테이너를 잘못만들었을경우 컨테이너를 새로 생성하는것을 권장 



## 컨테이너 접속하기
```
docker exec -it postgresdev /bin/bash
```
root@aca29b73a155:/# 

성공시 이렇게 보여지며 aca29b73a155는 컨테이너 아이디입니다.


## 유저생성하기
postgres 계정으로 변경

``` 
su postgres 

// ex) 
// root@aca29b73a155:/# su postgres
// postgres@aca29b73a155:/$
```

유저생성 명령어입력하기 
``` 
createuser --interactive

// ex)
// Enter name of role to add: super_admin
// Shall the new role be a superuser? (y/n) y
```

db 만들기 
```
createdb testdb
```

비밀번호 변경 
```
psql -U postgres
\password super_admin
```


---

## 튜토리얼

https://www.postgresqltutorial.com/postgresql-getting-started/postgresql-sample-database/

샘플 db 다운로드 

https://www.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip

zip 파일 압축해재
dvdrental.tar 파일을 C:\docker_postgresql_dev_volume 경로에 이동을 시킵니다.

db load 방법
https://www.postgresqltutorial.com/postgresql-getting-started/load-postgresql-sample-database/


```
psql  // psql 툴 실행 
CREATE DATABASE dvdrental; // "dvdrental" db 생성 

// exit 또는 \q 를 사용해서 root 계정으로 이동 
// ex) root@aca29b73a155:/# 

cd /home/workspace // 이동 (docker에서 -v 명령어로 볼륨을 설정할때의 서버경로입니다. 
// root@aca29b73a155:/home/workspace# cd /home/workspace

// dvdrental.tar데이터 dvdrental db으로 로드  
pg_restore -U postgres -d dvdrental
// root@aca29b73a155:/home/workspace# pg_restore -U postgres -d dvdrental dvdrental.tar 

// 경로를 이동하지 않았을경우 
// root@aca29b73a155: pg_restore -U postgres -d dvdrental /home/workspace/dvdrental.tar 
```

---

## DBeaver 실행 - Postgresql 연결 

입력이 필요한 값 

HOST  
Port   
Database  
Username  
Password  

#### HOST 

클라이언트(윈도우10) cmd 에서 ipconfig 입력 

이더넷 어댑터 vEthernet (Default Switch):

IPv4 주소 . . . . . . . . . : `XXX.XX.XX.1`  복사 

#### POST

도커에서 설정한 값 -p 54320:5432 여기에서 클라이언트 포트인 `54320` 입력

#### Database

생성한 db 

ex) `dvdrental` 또는 postgres 또는 testdb 

#### Username

`super_admin`

#### Password

`asd123!@#`

Test Connect 버튼으로 테스트
확인







