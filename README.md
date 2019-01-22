## 가끔 필요한데 찾으려면 귀찮은 것들 모음

- 찾으려면 귀찮은걸 덜 귀찮기 위해 귀찮음을 무릅쓰고 만듦. 아아 귀찮아...
- 쓰게 될 때, 생각 날 때마다 하나씩 추가 함 ㅇㅇ;
- 뭐하다 쓰게 됐는지 기록해도 재밌을 듯!

---

### TOC
- [AWS](#aws)
  - [ElastiCache](#elasticache)
  - [S3](#s3)
- [Database](#database)
  - [MySQL](#mysql)
  - [PostgreSQL](#postgresql)
- [Docker](#docker)
- [Git](#git)
- [Linux](#linux)
  - [Debian](#debian)
- [macOS](#macos)
- [Node.js](#nodejs)
  - [NVM]($nvm)
- [VSCode](#vscode)

---

### AWS

#### ElastiCache
- [보안상의 이유로 VPC 외부에서 직접 접속 할 수 없다.](https://aws.amazon.com/ko/elasticache/faqs/)
  - [ElastiCache에 직접 접근하는 EC2 인스턴스에 접속해서 접속하자.](https://docs.aws.amazon.com/ko_kr/AmazonElastiCache/latest/red-ug/GettingStarted.ConnectToCacheNode.html)

#### S3
- 정적 웹 호스팅 모드로 서빙할때 퍼블릭 권한을 잘 줬는데도 `AccessDenied` 뜰 때
  - 엔드포인트가 잘못된 경우이다. `https://s3.ap-northeast-2.amazonaws.com/bucket-name/` 이게 아니고 `http://bucket-name.s3-website.ap-northeast-2.amazonaws.com/` 이걸 쓰자. (전자는 각 파일의 속성을 클릭했을때 나오는 주소고, 후자는 정적 웹 호스팅 설정 속성에서 확인할수 있다.)

---

### Database

#### MySQL
- DB 생성
```shell
$ mysql -u{username} -p{password} -h{host}
mysql> CREATE DATABASE {database} CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

- [Table 'performance_schema.session_variables' doesn't exist](https://stackoverflow.com/a/33481982/3242865)
  - MySQL 5.6을 삭제하고 5.7을 새로 설치했을때 MySQLWorkbench로 최초 접속시 발생
```shell
$ mysql_upgrade -u{username} -p{password} (--force)
# it needs restart server
$ /usr/local/opt/mysql@5.7/bin/mysql.server restart
```

- DB 이름 변경: [How do I quickly rename a MySQL database (change schema name)?](https://stackoverflow.com/a/2298602/3242865)
  - `ALTER`로 될줄 알았지...
  - 먼저, 비어있는 DB를 생성하고 아래 명령어를 활용
```shell
$ mysql -u{username} -p{password} {old_db} -sNe 'show tables' | while read table; \ 
    do mysql -u{username} -p{password} -sNe "RENAME TABLE {old_db}.$table TO {new_db}.$table"; done
```

- 미리 생성된 테이블에 `INT` 컬럼을 추가할때 `NOT NULL` 속성으로 만들면 기존 데이터들의 추가될 컬럼의 기본값은 `0`이 된다.


#### PostgreSQL
- DB, USER 생성 및 권한 부여
```shell
# DB 생성
$ createdb {DB_NAME}
# psql 콘솔 접속
$ psql {DB_NAME}
psql (10.5)
Type "help" for help.
# USER 생성
{DB_NAME}# CREATE USER {USER_NAME} WITH ENCRYPTED PASSWORD {PASSWORD};
CREATE ROLE
# USER에 DB의 모든 접근 권한 부여
{DB_NAME}# GRANT ALL PRIVILEGES ON DATABASE {DB_NAME} TO {USER_NAME};
GRANT
```

---

### Docker
- 터미널에서 `docker run`등의 명령어를 실행 했을 때 `Error response from daemon: Bad response from Docker engine` 해결 방법
  - `Preferences > Reset > Reset to factory defaults`
  - Docker Desktop을 오랜만에(1달 이상?) 실행 시켰고, 업데이트가 있길래 설치했더니 발생

---


### Git
- [브랜치 삭제](https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-both-locally-and-remotely)
```shell
# remote
$ git push --delete origin <branch_name>
# local
$ git branch -d <branch_name>
```

- [https://www.gitignore.io/](https://www.gitignore.io/)
  - 프로젝트 처음 설정시 `.gitignore` 만들때 참고

- 로컬에서 `master` 브랜치를 제외한 모든 브랜치 삭제
```shell
$ git branch | grep -v "master" | xargs git branch -D
```

---

### Linux
#### Debian
- 기본 타임존 변경
  - [List of tz](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
```shell
$ echo "Asia/Seoul" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
```

---

### macOS
- [xcrun: error: invalid active developer path ...](https://apple.stackexchange.com/a/254381)
```shell
$ xcode-select --install
```
- 터미널에서 현재 디렉토리를 파인더로 바로 열기
```shell
$ open .
```

---

### Node.js
#### NVM
- [Calling nvm use automatically in a directory with a .nvmrc file](https://github.com/creationix/nvm#calling-nvm-use-automatically-in-a-directory-with-a-nvmrc-file)

---

### VSCode
- TS 프로젝트에서 하단 `문제` 패널에서 `tslint`가 두번씩 뜨는데, `TSLint` 플러그인과 `TSLint Vue` 플러그인을 같이 사용해서 발생했던 문제. `Vue`를 사용하지 않는 프로젝트였으므로 플러그인 패널에서 작업 영업에서 사용하지 않도록 설정하여 해결

