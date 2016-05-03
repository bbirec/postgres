Function
--------
Mysql에서 Stored Procedure라고 부르는 함수는 Postgres에서는 Function이라고 부른다.

Postgres에서는 다양한 언어로 Function을 구현할수 있게 제공한다.

 - pgSQL
 - Tcl
 - Perl
 - Python
 - [Javascript](https://github.com/plv8/plv8)

## Pros & Cons
Function을 사용하면 좋은 점과 안좋은 점이 있는데, 대략 적으로 정리해보면 다음과 같다.

**좋은점**
 - 복잡한 SQL쿼리를 함수로 따로 정의함으로써 재사용이 가능하다.
 - 비교적 큰 쿼리의 경우, DB서버에 매번 긴 쿼리 String을 보내지 않아도 되므로 이점이 될수 있다.
 - 쿼리 Planner가 Plan을 캐쉬하므로 비슷한 동작을 하는 쿼리를 만들어두면, 쿼리 Plan을 매번 하는 시간을 아낄수 있다.
 - Function안에 정의된 여러개의 쿼리는 자동으로 Transaction처리 되므로 편리하다.

**안좋은점**
 - DB상에 함수가 저장되므로 버전관리가 힘들다.
 - Table이나 View를 리턴하는 함수가 있는 경우, 해당 Table이나 View를 바꾸기 전에 Function을 지우고 변경한뒤 다시 생성해줘야 한다.
 - Function안에 있는 쿼리의 Plan을 확인할수 없다.(EXPLAIN이 되지 않는다.)

되도록이면 Function은 Immutable function으로만 만들어서 재사용하고, 실제 Query를 묶어서 Function으로 만들어 두는 것은 
서버 코드 관리상 좋지 않은 습관인듯하다.


## Performance
일반적인 쿼리를 날리는것과 Function으로 정의해서 여러가지 쿼리를 동시에 날리는 경우 성능의 차이가 나기도 한다.

- http://dba.stackexchange.com/questions/84414/explain-analyze-shows-no-details-for-queries-inside-a-plpgsql-function
- http://dba.stackexchange.com/questions/8119/postgresql-stored-procedure-performance/8189#8189
