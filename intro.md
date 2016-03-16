
## Postgres 소개
Mysql처럼 관계형 데이터베이스(RDBMS) 이며, 정확하게는 객체-관계형 데이터베이스(ORDBMS)이다. 보통 사용하는 SQL Standard를
따르고 있어 일반적인 SQL문을 사용해서 쿼리를 한다. 1995년 부터 오픈소스로 개발되어 왔고 Mysql을 포함하여 가장 유명한
오픈소스 데이터베이스 중 하나이다. Instagram, Skype, Apple등 유명한 회사의 실서비스에 사용 할 정도로 안정적이며
속도도 빠른것으로 소문이 나 있다.

## 왜 Postgres를 쓰는가
서비스를 만들때 어떤 데이터베이스를 사용할지 결정하는 것은 어떤 언어를 써서 개발을 하는 것 만큼 요구사항에 가장 적합한 것을
골라서 사용해야 한다. MongoDB, CouchDB와 같은 NoSQL이 최근 큰 유행을 했지만, RDBMS를 사용하기로 결정한 뒤에도 
다양한 데이터베이스 중 어떤 것을 골라야 할지는 고민스러울 수 밖에 없다.

Postgres가 Mysql 비해 모든 측면에서 월등히 좋다고 말할수는 없다. 대신 Postgres가 다른 데이터베이스에
비해서 좋은점이 충분히 많이 있다고 할 수 있다. 예를 들어 Mysql은 너무 유명해서 많은 사용기와 같은 리스소가 있는 반면,
데이터가 많이 있는 테이블에 컬럼을 추가하거나 인덱스를 추가하는 경우 테이블에 Lock이 걸리고 오랜 시간이 걸린다. 
이런 부분에 있어서는 Mysql에 비해 간단히 되기 때문에 Production레벨의 서비스에서 운영 및 관리가 편하다고 할 수 있다.
하지만 Postres에서는 테이블의 Row 개수를 구하는 쿼리를 하는 경우 항상 처음부터 끝까지 다 세어보기 때문에 
간단하게 구현할 수 없고, 캐쉬를 한다던지의 다른 방법을 강구해야만 한다.

스테이션3에서 Postgres를 선택했던 가장 큰 이유 중 하나는 PostGIS Extension이다. 다방 서비스는 
위치기반 서비스 이며 다양한 Geospatial 쿼리 함수가 필요했다. PostGIS Extension은 매우 강력하고, 다양한 위치기반 관련된
함수들을 제공하며, 빠르게 동작한다. 이런것 처럼 Postgres는 유명한 Extension이 잘 되어 있어서, Full-text search와 
같은 기능을 쉽게 추가 가능하다.


## Postgres 시작하기
가장 쉽게 시작하는 방법은 로컬에 설치하거나, 이미 클라우드 컴퓨팅 업체에서 호스팅 받아서 사용하는 것이다.

### OS X
맥에 Postres를 설치하기 가장 쉬운 방법은 Heroku에서 만든 Postgres.App(http://postgresapp.com/) 을 설치하는 
것이다. 일반적인 Application처럼 다운받아서 실행하기만 하면 Postgres 서버와 관련 tool을 사용할 수 있다. 게다가
자주 쓰는 Extension을 기본 탑재하고 있어서 PostGIS와 같은 Extension을 바로 사용해 볼 수 있는 장점이 있다.

### 클라우드
아래와 같은 클라우드 컴퓨팅 서비스를 제공하는 업체를 통해 무료 또는 유료로 호스팅 받아서 사용할 수 있다. 아무런 설치 과정이나
설정도 없이 바로 `postgres://...`와 같은 주소로 접근가능하다.

 - Heroku Postgres : https://www.heroku.com/postgres
 - AWS RDS : https://aws.amazon.com/rds
 - Compose : https://www.compose.io

## Postgres 사용하기
일단 설치 및 호스팅으로 부터 주소를 받으면 `psql`이라는 Postgres 전용 클라이언트 프로그램으로 쿼리를 실행해 볼 수 있다.
`psql`은 Postgres를 설치하면 함께 설치되는 커맨드라인 프로그램이다.

아래와 같이 `psql`을 실행하면 쿼리를 입력할 수 있는 입력창이 생긴다. 여기에 `SELECT`문과 같은 쿼리를 입력하면 그 결과가 출력된다.
```
$ psql 
psql (9.4.4)
Type "help" for help.

bbirec=#
```