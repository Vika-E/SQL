# Решенные задачки с sql-ex.ru
**1. Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd
select model, speed, hd from PC**
where Price<500

**2. Найдите производителей принтеров. Вывести: maker**
select distinct maker from product 
where type='Printer'

**3. Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.**
select model, ram, screen from laptop 
where price>1000

**4. Найдите все записи таблицы Printer для цветных принтеров.**
select * from Printer where color = 'y'

**5. Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.**
Select model, speed, hd from PC 
where (cd = '12x' or cd = '24x') and price<600

**6. Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.**
select distinct product.maker, laptop.speed 
from product join laptop 
on product.model=laptop.model where hd>=10

**7. Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).**
select product.model, price
from product join pc on product.model=pc.model
where product.maker='B'
union
select product.model, price
from product join laptop on product.model=laptop.model
where product.maker='B'
union
select product.model, price
from product join printer on product.model=printer.model
where product.maker='B'

**8. Найдите производителя, выпускающего ПК, но не ПК-блокноты.**
select maker from product 
where type='pc'
except
select maker from product 
where type='laptop'

**9. Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker**
select distinct maker
from product join pc on product.model=pc.model
where speed>=450

**10. Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price**
select model, price
from printer 
where price = (select max(price) from printer)

**11. Найдите среднюю скорость ПК**
select avg(speed) from PC

**12. Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол**
select avg(speed) from laptop where price > 1000


**13. Найдите среднюю скорость ПК, выпущенных производителем A**
select avg(speed) 
from pc inner join product 
on pc.model = product.model 
where maker = 'A'

**14. Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий**
select ships.class, ships.name, classes.country 
from ships inner join classes 
on ships.class=classes.class 
where numGuns>=10

**15. Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD**
select hd from pc 
group by hd 
having count(model)>=2