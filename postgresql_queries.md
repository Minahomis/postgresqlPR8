# Практическая работа №8


Предворительно создадим базу данных и таблицу 


```sql
CREATE TABLE persons (
    id SERIAL PRIMARY KEY,
    last_name TEXT,
    first_name TEXT,
    patronymic TEXT,
    description TEXT
);


```
![alt text](./img/screen-1.png)
---

## 1.  Добавить данные в таблицу (в виде строки)

```sql
INSERT INTO persons (last_name, first_name, patronymic, description)
VALUES ('Иванов', 'Иван', 'Иванович', 'Пример записи');
```
![alt text](./img/screen-2.png)

Пояснение:
```sql
INSERT INTO — добавляет новую строку в таблицу.

VALUES (...) — задаёт значения для перечисленных столбцов.
 ```
 **_______________________**

---

## 2.  Добавить новый столбец в таблицу

```sql
ALTER TABLE persons ADD COLUMN email TEXT;
```
![alt text](./img/screen-3.png)
Пояснение

```sql
ALTER TABLE — изменяет структуру таблицы.

ADD COLUMN — добавляет новый столбец.

TEXT — тип данных нового столбца.
 ```
 **_______________________**

---

## 3.  Получить размер базы данных

```sql
SELECT pg_size_pretty(pg_database_size(current_database()));

```
![alt text](./img/screen-4.png)
Пояснение

```sql
current_database() — возвращает имя текущей базы данных.

pg_database_size(name) — возвращает размер базы данных в байтах.

pg_size_pretty(size) — преобразует число байт в удобный формат (KB, MB, GB).
 ```
 **_______________________**

---

## 4.  Подсчитать количество строк в таблице

```sql
SELECT COUNT(*) FROM persons;
```
![alt text](./img/screen-5.png)
Пояснение

```sql
COUNT(*) — возвращает общее количество строк в таблице persons.
 ```
 **_______________________**

---

## 5.  Создать новую таблицу с данными

```sql
CREATE TABLE departments (
    id SERIAL PRIMARY KEY,
    department_name TEXT
);

INSERT INTO departments (department_name)
VALUES 
('Бухгалтерия'),
('Отдел кадров'),
('ИТ-отдел');

```
![alt text](./img/screen-6.png)
Пояснение

```sql
CREATE TABLE — создаёт таблицу departments.

SERIAL PRIMARY KEY — автоинкрементный первичный ключ.

INSERT INTO ... VALUES — добавляет новые строки в таблицу.
 ```
 **_______________________**

---

## 6.  Получить первые 5 символов из каждой строки в столбце "М"

```sql
SELECT LEFT(description, 5) FROM persons;

```

![alt text](./img/screen-7.png)
Пояснение

```sql
LEFT(string, n) — возвращает первые n символов строки.

Применяется к каждой строке столбца description.
 ```
**_______________________**

---

## 7.  Подсчитать количество символов в каждой строке столбца "М"

```sql
SELECT LENGTH(description) FROM persons;

```
![alt text](./img/screen-8.png)

Пояснение
```sql
LENGTH(string) — возвращает количество символов в каждой строке столбца description.
 ```
**_______________________**

---

## 8.  Преобразовать ФИО к правильному регистру

### Вариант 1: С первой буквой в верхнем регистре

```sql
SELECT
    LOWER(LEFT(last_name, 1)) || UPPER(SUBSTRING(last_name FROM 2)) AS "Фамилия",
    LOWER(LEFT(first_name, 1)) || UPPER(SUBSTRING(first_name FROM 2)) AS "Имя",
    LOWER(LEFT(patronymic, 1)) || UPPER(SUBSTRING(patronymic FROM 2)) AS "Отчество"
FROM persons
WHERE last_name = 'ИВаноВ' AND first_name = 'ИваН' AND patronymic = 'ИВАновИч';
```
![alt text](./img/screen-8.png)

Пояснение
```sql
LEFT(str, 1) — первая буква.

SUBSTRING(str FROM 2) — часть строки начиная со 2 символа.

LOWER(...) — приводит к нижнему регистру.

UPPER(...) — приводит к верхнему регистру.

|| — оператор конкатенации (склеивания строк).

WHERE — фильтрация записей по условиям.
 ```
 **_______________________**

---