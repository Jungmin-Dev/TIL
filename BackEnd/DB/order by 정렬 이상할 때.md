<h1> order by 정렬 이상할 때 </h1>

``` sql
SELECT
      content_id, user_email, title, created_at, updated_at
FROM
      CONTENT
ORDER BY to_number(CONTENT_ID)```

<h3> 위와 같이 to_number를 사용하면 해결 가능하다. </h3>
