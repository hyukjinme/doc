URL  
https://ide.goorm.io


회원가입 또는 로그인

- 새 컨테이너 선택
  - 이름
  - 소프트웨어스택 Blank 선택
  - 생성하기

- 생성한 컨테이너 항상켜두기 ON 
  - (2022_10_14 무료제공 종료됨)
  - 컨테이너 정지 이후 켜두기 가능

- 컨테이너 실행
  - 상단위 컨테이너 - SSH 설정 
    - 비밀번호 발급
  - 컨테이너 - 포트포워딩 설정 
    - 유형 PostgreSQL 등록

- Putty 또는 XShell로 SSH 접속
 
  - PostgresSQL 설치 
  
  ```
  sudo apt update && sudo apt install postgresql postgresql-contrib -y
  ```
  
 - 비밀번호 변경
  
 ```
 passwd postgres // OS
 
  su - postgres

  service postgresql start

  psql -U postgres

  \password postgres // AUTH
 ```
 
 - 설정
 ```
  cd /etc/postgresql/10/main

  vi pg_hba.conf // 맨 하단에 host all all 0.0.0.0/0 md5 삭제할거라 일단 전부허용 
  
  host    all             all             0.0.0.0/0               md5
  
  vi postgresql.conf  // listen_addresses = '*' 으로 변경 
  
  sudo service postgresql restart // 재시작 
 ```
 
 Dbeaver 접속
 

 
 
