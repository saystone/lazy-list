## 가끔 필요한데 찾으려면 귀찮은 것들 모음

- 찾으려면 귀찮은걸 덜 귀찮기 위해 귀찮음을 무릅쓰고 만듦. 아아 귀찮아...
- 쓰게 될 때, 생각 날 때마다 하나씩 추가 함 ㅇㅇ;
- 뭐하다 쓰게 됐는지 기록해도 재밌을 듯!

---

### TOC
- [AWS](#aws)
  - [ElastiCache](#elasticache)
- [Database](#database)
  - [PostgreSQL](#postgresql)
- [Git](#git)
- [Linux](#linux)
  - [Debian](#debian)
- [macOS](#macos)

---

### AWS

#### ElastiCache
- [보안상의 이유로 VPC 외부에서 직접 접속 할 수 없다.](https://aws.amazon.com/ko/elasticache/faqs/)

---

### Database

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

---

###  Linux
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

---

