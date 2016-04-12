## JSON
Postgres에서는 JSON data type을 9.2 버전 부터 지원한다. 9.4 버전부터는 좀 더 다양한 기능을 제공해서, 
NoSQL처럼 unstructured data를 저장하고 쿼리 할 수 있다.

9.4 이전 버전에서는 text type을 쓰는것 보다, 제대로 된 JSON 포멧인지 정도 체르를 해주고 
`Array`나 `Object`에서 데이터를 꺼내서 `SELECT`할 수 있다.

 - https://www.compose.io/articles/is-postgresql-your-next-json-database/