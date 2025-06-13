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
 **_______________________**

---

## 2.  Добавить новый столбец в таблицу

```sql
ALTER TABLE persons ADD COLUMN email TEXT;
```
![alt text](./img/screen-3.png)
 **_______________________**

---

## 3.  Получить размер базы данных

```sql
SELECT pg_size_pretty(pg_database_size(current_database()));

```
![alt text](./img/screen-4.png)

 **_______________________**

---

## 4.  Подсчитать количество строк в таблице

```sql
SELECT COUNT(*) FROM persons;
```
![alt text](./img/screen-5.png)
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
 **_______________________**

---

## 6.  Получить первые 5 символов из каждой строки в столбце "М"

```sql
SELECT LEFT(description, 5) FROM persons;
```
![alt text](./img/screen-7.png)
**_______________________**

---

## 7.  Подсчитать количество символов в каждой строке столбца "М"

```sql
SELECT LENGTH(description) FROM persons;

```
![alt text](./img/screen-8.png)
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
 **_______________________**

---