# Домашнее задание к занятию "`SQL. Часть 2`" - `Мурчин Артем`

### Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Решение 1

![alt text](https://github.com/artmur1/12-04-hw/blob/main/12-04-zad1.png)

SELECT s.store_id, CONCAT(s2.first_name, ' ', s2.last_name) AS Manager, c2.city, COUNT(c.customer_id) AS 'Number of users'

FROM customer c

LEFT JOIN store s ON s.store_id = c.store_id

LEFT JOIN staff s2 ON s2.staff_id = s.manager_staff_id

LEFT JOIN address a ON a.address_id  = s.address_id 

LEFT JOIN city c2 ON c2.city_id = a.city_id

GROUP BY s.store_id

HAVING COUNT(c.customer_id) > 300;

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Решение 2

![alt text](https://github.com/artmur1/12-04-hw/blob/main/12-04-zad2.png)

SELECT COUNT(film_id)

FROM film f

WHERE length > (SELECT AVG(`length`) FROM film f2);

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Решение 3

![alt text](https://github.com/artmur1/12-04-hw/blob/main/12-04-zad3.png)

SELECT MONTH(payment_date), SUM(amount), COUNT(rental_id)

FROM payment

GROUP BY MONTH(payment_date)

ORDER BY SUM(amount) DESC

LIMIT 1;

#### Доработка задания 3

![alt text](https://github.com/artmur1/12-04-hw/blob/main/12-04-zad3-1.png)

SELECT DATE_FORMAT(payment_date, '%M – 2005') AS Month, SUM(amount), COUNT(rental_id)

FROM payment

GROUP BY DATE_FORMAT(payment_date, '%M – 2005')

ORDER BY SUM(amount) DESC

LIMIT 1;

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.
