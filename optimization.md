### EXPLAIN
실제로 DB에 쿼리를 날려보기 전에 *PostgreSQL planner*가 현재 Table, Index를 기반으로 어떻게 쿼리를 실행할지에 대한 계획을
확인해볼 수 있는 기능이다. Query를 실행하기 위해 어떤 Index를 사용할것인지에 대한 정보도 있기 때문에 내 예상대로 
Index를 사용하지는 볼 수 있다.

```
dabang=> explain select * from users where id='bbirec@gmail.com';
                                      QUERY PLAN                                       
---------------------------------------------------------------------------------------
 Index Scan using users_id_password_index on users  (cost=0.42..8.44 rows=1 width=735)
   Index Cond: ((id)::text = 'bbirec@gmail.com'::text)
(2 rows)
```

### EXPLAIN ANALYZE 
`EXPLAIN`과 다르게 *PostgreSQL planner*가 세운 계획대로 Query를 실행하고, 
실제로 어떻게 쿼리를 실행하고 얼마나 걸렸는지를 확인할 수 있다.

```
dabang=> explain analyze select * from users where id='bbirec@gmail.com';
                                                           QUERY PLAN                                                            
---------------------------------------------------------------------------------------------------------------------------------
 Index Scan using users_id_password_index on users  (cost=0.42..8.44 rows=1 width=735) (actual time=0.061..0.062 rows=1 loops=1)
   Index Cond: ((id)::text = 'bbirec@gmail.com'::text)
 Total runtime: 0.088 ms
(3 rows)
```

### 분석툴
 - http://explain.depesz.com
 - https://github.com/AlexTatiyants/pev