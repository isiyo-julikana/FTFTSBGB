# Создание базы данных
### В подключенном MySQL репозитории создать базу данных "Human Friends"
```
CREATE DATABASE HumanFriends;
USE  HumanFriends;
```
### Создание и заполение таблиц в соотвествии с иерархией диограммы классов

```
CREATE  TABLE Animal (
id INT PRIMARY KEY AUTO_INCREMENT,
type_animal VARCHAR(50) NOT NULL);
INSERT INTO animal (type_animal)
VALUES
('Pets'),
('Paсk Animals');

CREATE TABLE Pets (
id INT PRIMARY KEY AUTO_INCREMENT,
type_animal INT NOT NULL,
FOREIGN KEY (type_animal) REFERENCES animal (id),
genus_animal VARCHAR(50) NOT NULL);

INSERT INTO Pets (type_animal, genus_animal)
VALUES
(1,'Dog'),
(1,'Cat'),
(1,'Hamster');

CREATE TABLE PackAnimal (
id INT PRIMARY KEY AUTO_INCREMENT,
type_animal INT NOT NULL,
FOREIGN KEY (type_animal) REFERENCES animal (id),
genus_animal VARCHAR(50) NOT NULL);

INSERT INTO PackAnimal (type_animal, genus_animal)
VALUES
(2,'Horse'),
(2,'Camel'),
(2,'Donkey');

CREATE TABLE Dog (
id INT PRIMARY KEY AUTO_INCREMENT,
genus_animal INT NOT NULL,
FOREIGN KEY (genus_animal) REFERENCES pets (id),
name VARCHAR(50) NOT NULL,
birthday DATE NOT NULL,
comands VARCHAR(255) NOT NULL
)

INSERT INTO Dog (genus_animal,name,birthday,comands)
VALUES 
(1,'Юкс',   '2020-02-02','seat guard run voice'),
(1,'Мегги', '2021-03-09','seat guard run voice'),
(1,'Лэдис', '2024-03-05','seat guard run voice'),
(1,'Зурна', '2022-01-21','seat guard run voice'),
(1,'Алгир', '2019-03-04','seat guard run voice');

CREATE TABLE Cat (
id INT PRIMARY KEY AUTO_INCREMENT,
genus_animal INT NOT NULL,
FOREIGN KEY (genus_animal) REFERENCES pets (id),
name VARCHAR(50) NOT NULL,
birthday DATE NOT NULL,
comands VARCHAR(255) NOT NULL
)

INSERT INTO Cat (genus_animal,name,birthday,comands)
VALUES 
(2,'Айва',  '2018-06-10','seat climb voice sleep'),
(2,'Айкар', '2019-01-30','seat climb voice sleep'),
(2,'Майя',  '2020-05-31','seat climb voice sleep'),
(2,'Гул',   '2023-04-30','seat climb voice sleep'),
(2,'Вики',  '2021-08-01','seat climb voice sleep');

CREATE TABLE Hamster (
id INT PRIMARY KEY AUTO_INCREMENT,
genus_animal INT NOT NULL,
FOREIGN KEY (genus_animal) REFERENCES pets (id),
name VARCHAR(50) NOT NULL,
birthday DATE NOT NULL,
comands VARCHAR(255) NOT NULL
)

INSERT INTO Hamster (genus_animal,name,birthday,comands)
VALUES 
(3,'Борей','2022-03-29','seat run eat'),
(3,'Ярга', '2021-04-10','seat run eat'),
(3,'Морж', '2020-07-21','seat run eat'),
(3,'Анга', '2019-01-09','seat run eat'),
(3,'Торро','2020-06-14','seat run eat');

CREATE TABLE Horse (
id INT PRIMARY KEY AUTO_INCREMENT,
genus_animal INT NOT NULL,
FOREIGN KEY (genus_animal) REFERENCES petanimal (id),
name VARCHAR(50) NOT NULL,
birthday DATE NOT NULL,
comands VARCHAR(255) NOT NULL
)

INSERT INTO Horse (genus_animal,name,birthday,comands)
VALUES 
(1,'Баста', '2019-10-06','seat run eat load-cargo'),
(1,'Пиккер','2018-04-06','seat run eat load-cargo'),
(1,'Сарма', '2021-08-02','seat run eat load-cargo'),
(1,'Амани', '2019-12-30','seat run eat load-cargo'),
(1,'Чазета','2020-07-04','seat run eat load-cargo');

CREATE TABLE Camel (
id INT PRIMARY KEY AUTO_INCREMENT,
genus_animal INT NOT NULL,
FOREIGN KEY (genus_animal) REFERENCES petanimal (id),
name VARCHAR(50) NOT NULL,
birthday DATE NOT NULL,
comands VARCHAR(255) NOT NULL
)

INSERT INTO Camel (genus_animal,name,birthday,comands)
VALUES
(2,'Солли', '2021-05-28','seat run eat load-cargo'),
(2,'Весла', '2019-01-27','seat run eat load-cargo'),
(2,'Ружа',  '2020-06-25','seat run eat load-cargo'),
(2,'Айна',  '2021-01-02','seat run eat load-cargo'),
(2,'Аян',   '2018-08-16','seat run eat load-cargo');

CREATE TABLE Donkey  (
id INT PRIMARY KEY AUTO_INCREMENT,
genus_animal INT NOT NULL,
FOREIGN KEY (genus_animal) REFERENCES petanimal (id),
name VARCHAR(50) NOT NULL,
birthday DATE NOT NULL,
comands VARCHAR(255) NOT NULL
)

INSERT INTO Donkey (genus_animal,name,birthday,comands)
VALUES 
(3,'Стоил',     '2018-07-01','seat run eat load-cargo'),
(3,'Хазар',     '2019-04-12','seat run eat load-cargo'),
(3,'Сулейка',   '2019-10-10','seat run eat load-cargo'),
(3,'Скат',      '2020-02-27','seat run eat load-cargo'),
(3,'Юнгар',     '2021-06-25','seat run eat load-cargo');

```

### Удаляем таблицу верблюдов и объеденяем лошадей и ослов
```
DROP TABLE Camel;

CREATE TABLE unionPackAn
AS( SELECT *
FROM Donkey
UNION
SELECT *
FROM Horse);

```

### Создать новую таблицу для животных в возрасте от 1 до 3 лет и вычислить их возраст с точностью до месяца.

```
CREATE TABLE YoungAnimal
  AS (
SELECT id, genus_animal,name, comands, (EXTRACT(YEAR FROM curdate())  - EXTRACT(YEAR FROM Cat.birthday)) * 12 +
(CASE WHEN  EXTRACT(MONTH FROM curdate()) < EXTRACT(MONTH FROM Cat.birthday)
		THEN EXTRACT(MONTH FROM Cat.birthday) - EXTRACT(MONTH FROM curdate())
  			WHEN  EXTRACT(MONTH FROM curdate()) > EXTRACT(MONTH FROM Cat.birthday)
  			THEN EXTRACT(MONTH FROM curdate()) - EXTRACT(MONTH FROM Cat.birthday)
  			    WHEN EXTRACT(MONTH FROM curdate()) = EXTRACT(MONTH FROM Cat.birthday)
  			    THEN 0
END) AS AgeMonth
FROM Cat
WHERE EXTRACT(YEAR FROM curdate()) - EXTRACT(YEAR FROM  Cat.birthday) BETWEEN 1 AND 3

UNION

SELECT id, genus_animal,name, comands, (EXTRACT(YEAR FROM curdate())  - EXTRACT(YEAR FROM Dog.birthday)) * 12 +
(CASE WHEN  EXTRACT(MONTH FROM curdate()) < EXTRACT(MONTH FROM Dog.birthday)
		THEN EXTRACT(MONTH FROM Dog.birthday) - EXTRACT(MONTH FROM curdate())
  			WHEN  EXTRACT(MONTH FROM curdate()) > EXTRACT(MONTH FROM Dog.birthday)
  			THEN EXTRACT(MONTH FROM curdate()) - EXTRACT(MONTH FROM Dog.birthday)
  			    WHEN EXTRACT(MONTH FROM curdate()) = EXTRACT(MONTH FROM Dog.birthday)
  			    THEN 0
END) AS AgeMonth
FROM Dog
WHERE EXTRACT(YEAR FROM curdate()) - EXTRACT(YEAR FROM  Dog.birthday) BETWEEN 1 AND 3

UNION

SELECT id, genus_animal,name, comands, (EXTRACT(YEAR FROM curdate())  - EXTRACT(YEAR FROM Hamster.birthday)) 
* 12 +
(CASE WHEN  EXTRACT(MONTH FROM curdate()) < EXTRACT(MONTH FROM Hamster.birthday)
		THEN EXTRACT(MONTH FROM Hamster.birthday) - EXTRACT(MONTH FROM curdate())
  			WHEN  EXTRACT(MONTH FROM curdate()) > EXTRACT(MONTH FROM Hamster.birthday)
  			THEN EXTRACT(MONTH FROM curdate()) - EXTRACT(MONTH FROM Hamster.birthday)
  			    WHEN EXTRACT(MONTH FROM curdate()) = EXTRACT(MONTH FROM Hamster.birthday)
  			    THEN 0
END) AS AgeMonth
FROM Hamster
WHERE EXTRACT(YEAR FROM curdate()) - EXTRACT(YEAR FROM  Hamster.birthday) BETWEEN 1 AND 3

UNION 

SELECT id, genus_animal,name, comands, (EXTRACT(YEAR FROM curdate())  - EXTRACT(YEAR FROM Horse.birthday)) * 12 +
(CASE WHEN  EXTRACT(MONTH FROM curdate()) < EXTRACT(MONTH FROM Horse.birthday)
		THEN EXTRACT(MONTH FROM Horse.birthday) - EXTRACT(MONTH FROM curdate())
  			WHEN  EXTRACT(MONTH FROM curdate()) > EXTRACT(MONTH FROM Horse.birthday)
  			THEN EXTRACT(MONTH FROM curdate()) - EXTRACT(MONTH FROM Horse.birthday)
  			    WHEN EXTRACT(MONTH FROM curdate()) = EXTRACT(MONTH FROM Horse.birthday)
  			    THEN 0
END) AS AgeMonth
FROM Horse
WHERE EXTRACT(YEAR FROM curdate()) - EXTRACT(YEAR FROM  Horse.birthday) BETWEEN 1 AND 3

UNION

SELECT id, genus_animal,name, comands, (EXTRACT(YEAR FROM curdate())  - EXTRACT(YEAR FROM Donkey.birthday)) 
* 12 +
(CASE WHEN  EXTRACT(MONTH FROM curdate()) < EXTRACT(MONTH FROM Donkey.birthday)
    THEN EXTRACT(MONTH FROM Donkey.birthday) - EXTRACT(MONTH FROM curdate())
        WHEN  EXTRACT(MONTH FROM curdate()) > EXTRACT(MONTH FROM Donkey.birthday)
        THEN EXTRACT(MONTH FROM curdate()) - EXTRACT(MONTH FROM Donkey.birthday)
            WHEN EXTRACT(MONTH FROM curdate()) = EXTRACT(MONTH FROM Donkey.birthday)
            THEN 0
END) AS AgeMonth
FROM Donkey
WHERE EXTRACT(YEAR FROM curdate()) - EXTRACT(YEAR FROM  Donkey.birthday) BETWEEN 1 AND 3

);
```

### Объединить все созданные таблицы в одну, сохраняя информацию о принадлежности к исходным таблицам.

```
CREATE TABLE UnionAnimalDB
AS(
SELECT * FROM Cat UNION
SELECT * FROM Dog UNION
SELECT * FROM Hamster UNION
SELECT * FROM Horse UNION
SELECT * FROM Donkey);

```