
## 인덱스(Index)
Table이나 Materialized View에 적용가능

멀티 컬럼 인덱스나 조건절이 가능, 소팅 가능

어떠한 Query를 실행 했을때 어떤 Index를 사용할지 말지는 Query Planner가 결정함. 특정 케이스에서는 
Index를 사용하는 것 보다 Serial Scan이 더 빠를때도 있음. 내가 하는 Query를 어떤 Index를 쓰는지 
보려면 `EXPLAIN ANALYZE`를 사용하면 됨.

인덱스를 추가하면 SELECT와 같은 Query의 속도에 큰 도움이 되지만, Write에 오버헤드가 생기기 때문에
무차별적으로 Index를 추가하는것은 좋지 않다. 거의 쓰지 않는 Index의 경우 삭제하는게 맞다.


 - Index를 생성할때 읽기는 가능하지만, Insert, update, delete 는 안됨.
 - 서비스 중일때 큰 Table에 Index를 추가 하고 싶을때 CONCURRENTLY 인덱스를 사용하면 Write lock이 안되기 때문에 고려.
 - Multi Column Index는 B-tree, GiST, GIN만 지원함.
 - Parital Index를 통해서 큰 Table에서 쿼리에 사용되는 부분만 Index를 걸수 있어서 더 빠른 검색이 가능하다.
 - Unique Index를 통해서 어떤 컬럼에 중복된 값이 들어가는것을 막는다.

## 인덱스의 종류

### Btree
Index 종류를 지정하지 않으면 기본적으로 생성되는 타입이다. `<`, `<=`, `=`, `>=`, `>` 연산자를 사용할때 효율적이다.

### Hash
`=`연산자에서만 사용되며 크래쉬 되거나 했을때 REINDEX를 해야 하고, Replication도 되지 않는 여러가지 이유 때문에 왠만해서
사용하지 않아야 한다.

### GIN(Generalized Inverted Indexes)
여러개의 값에 대한 Index를 생성할때 사용되며 array type이나 Full text search와 같은 쿼리에 사용된다.

### GiST(Generalized Search Tree)
General Balanced Tree형태로 Index를 생성한다. Equality나 Range 연산자에 사용된다. Geometry type이나 full text search에 사용된다. 

## Reference
 - http://www.postgresql.org/docs/9.4/static/indexes.html
 - https://devcenter.heroku.com/articles/postgresql-indexes
 - http://instagram-engineering.tumblr.com/post/40781627982/handling-growth-with-postgres-5-tips-from
 - http://www.postgresql.org/docs/9.4/static/sql-createindex.html
 - http://www.postgresguide.com/performance/indexes.html 