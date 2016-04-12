## Upsert

Postgres 9.5 버전 부터 Upsert기능이 제공된다. 이전 버전에서는 정확하게 구현하기 어렵다.

9.5버전 부터는 `INSERT`문 다음에 `ON CONFLICT`를 넣어서 기존에 있는 row와 충돌하는 경우 `UPDATE`를 할수 있게 한다.
이를 통해서 Upsert를 구현 할 수 있다.


### Reference
 - http://www.depesz.com/2012/06/10/why-is-upsert-so-complicated/
 - https://www.compose.io/articles/postgresqls-future-is-looking-upsert/


