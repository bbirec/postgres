Function
--------
Mysql에서 Stored Procedure라고 부르는 함수는 Postgres에서는 Function이라고 부른다.

Postgres에서는 다양한 언어로 Function을 구현할수 있게 제공한다.

 - pgSQL
 - Tcl
 - Perl
 - Python
 - [Javascript](https://github.com/plv8/plv8)


## Performance
일반적인 쿼리를 날리는것과 Function으로 정의해서 여러가지 쿼리를 동시에 날리는 경우 성능의 차이가 나기도 한다.

- http://dba.stackexchange.com/questions/84414/explain-analyze-shows-no-details-for-queries-inside-a-plpgsql-function
- http://dba.stackexchange.com/questions/8119/postgresql-stored-procedure-performance/8189#8189
