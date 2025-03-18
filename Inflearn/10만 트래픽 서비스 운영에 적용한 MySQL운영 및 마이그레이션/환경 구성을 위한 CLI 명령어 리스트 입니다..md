```bash
sudo vi /etc/ssh/sshd_config 

- ssh 설정을 위한 환경 파일 위치 입니다.
```

```sql
sudo dnf install https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm 

- Amazon Linux 2023에서 dnf를 활용한 MySQL RPM파일 가져오는 명령어 입니다.
```

```markdown
sudo dnf install mysql-community-server 

- MySQL 설치 명령어 입니다.
```

```cpp
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022 

- GPG키 에러에 따른 해결법 입니다.
```

```bash
sudo systemctl stop mysqld

sudo chmod -R 755 /var/lib/mysql/

sudo chown -R mysql:mysql /var/lib/mysql/

sudo systemctl start mysqld

- MySQL 최초 구동시에 mysql.sock 에러를 해결하기 위한 순서 입니다.
```

```bash
sudo cat /var/log/mysqld.log 

- MySQL 초기 비밀번호 추출을 위한 로그 파일 입니다.
```

```sql
ALTER USER 'root'@'localhost' identified by '<원하는 비밀번호>';

- MySQL 비밀번호 설정을 위한 쿼리 입니다.
```

```sql
create user '<원하는 이름>'@'IP허용대' identified by '<비밀번호>'

- MySQL 새로운 유저를 추가하는 명령어 입니다.
```

```sql
GRANT ALL PRIVILEGES ON *.* to 'trash-external'@'%';

- MySQL 유저에 대해서 권한을 설정하는 쿼리 입니다.
```