## Лабраторная работа
Поднимаем контейнеры и подключаемся к master
```
sudo docker compose up -d
psql -h localhost -p 5433 -U postgres
```
![img.png](imgs/img.png)

Создаём таблицу

```
CREATE TABLE students (id SERIAL, name TEXT);
INSERT INTO students (name) VALUES ('Ivan'), ('Denis');
SELECT * FROM students;
```
![img_1.png](imgs/img_1.png)
Подключаемся к standby
```
psql -h localhost -p 5434 -U postgres
```
Проверяем наличие данных

```
SELECT * FROM students;
```

![img_2.png](imgs/img_2.png)

```
INSERT INTO students (name) VALUES ('Pyrin'), ('Sayfutdinov');
```
![img_3.png](imgs/img_3.png)

Останавиваем контейнер master, переводим standby в master

```
docker stop primary
```
```
`SELECT pg_promote();`

INSERT INTO students (name) VALUES ('Pyrin'), ('Sayfutdinov');
SELECT * FROM students;
```

![img_4.png](imgs/img_4.png)
