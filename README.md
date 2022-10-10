# filmorate-db
![схема бд](https://github.com/marialyahovskaya/filmorate-db/blob/main/Filmorate_DataBase.drawio.png)

Запросы:
1. Получить список подтвержденных друзей юзера N.
```sql
SELECT friend_id
FROM friendship
WHERE user_id = 1 AND status = TRUE

UNION

SELECT user_id
FROM fruendship
WHERE friend_id = 1 AND status = TRUE
```

2. Получить список друзей юзера N, которые ожидают его подтверждения на дружбу.
```sql
SELECT user_id 
FROM friendship 
WHERE friend_id = N AND status = FALSE;
```


3. Получить список кому юзер N отправил запросы на дружбу и их ещё не подтвердили.
```sql
SELECT friend_id 
FROM friendship 
WHERE user_id = N AND status = FALSE;
```

4. Получить топ 10 фильмов и количество их лайков.
```sql
SELECT f.name,
    COUNT(l.user_id) AS likes
FROM film AS f
    INNER JOIN like AS l ON f.film_id=l.film_id
GROUP BY f.film_id
ORDER BY likes DESC
LIMIT 10;
```
