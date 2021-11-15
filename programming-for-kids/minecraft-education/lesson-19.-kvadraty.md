# Урок 19. Вкладені квадрати

## 0. Описание занятия

В первой части занятия студенты овладеют навыком использования вложенных циклов: а. создания квадарта из блоков и цветов; б. создания полисадников (квадарт полностью заполненный цветами) и площадок из блоков; в. создания пирамиды (на примере маяка). Во второй части занятияв студенты овладевают навыком использования переменных (передачи параметра при команде чата), а также создания вложенных циклов

## 1. Создание квадрата последовательными циклами

Переход к вложенному циклу осуществляется через создание квадрата 4-мя последовательными линейными циклами:

### Берем - созданную линию

![](<../../.gitbook/assets/Minecraft Education Edition (1).jpg>)

### Добавляем букву s к команде чата

![](<../../.gitbook/assets/Minecraft Education Edition1 (3).jpg>)

### ДублируеУрокм блок повторения размещения блока 4 раза

![](<../../.gitbook/assets/Minecraft Education Edition2 (3).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition3 (3).jpg>)

### Между каждым блоком цикла ставим блок "Повернуться налево"

![](<../../.gitbook/assets/Minecraft Education Edition4 (3).jpg>)

### Получаем результат

![](<../../.gitbook/assets/Minecraft Education Edition5 (3).jpg>)

## 2. Создание квадрата вложенными циклами



### Дублируем квадрат из 4-х циклов (команда lines)

![](<../../.gitbook/assets/Minecraft Education Edition (2).jpg>)

### Меняем команду с lines на q

![](<../../.gitbook/assets/Minecraft Education Edition1 (4).jpg>)

### Показываем, что предыдущий алгоритм цикличный (повторяющийся)

![](<../../.gitbook/assets/Minecraft Education Edition2 (4).jpg>)

### Убираем и удаляем блоки, которые повторяются

![](<../../.gitbook/assets/Minecraft Education Edition3 (4).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition4 (4).jpg>)

### Берем блок "Повторить 4 раза" и оборачиваем им повторяемую часть

![](<../../.gitbook/assets/Minecraft Education Edition5 (4).jpg>)

### Получаем квадрат

![](<../../.gitbook/assets/Minecraft Education Edition6 (3).jpg>)

[Задания 1 и 2](https://makecode.com/\_AgviCpRy52pP)

## 3. Создание вложенных квадратов

### Дублируем блок q

![](<../../.gitbook/assets/Minecraft Education Edition (5).jpg>)

### Меняем команду чата на inq

![](<../../.gitbook/assets/Minecraft Education Edition1 (7).jpg>)

### Дублируем блок повторения

![](<../../.gitbook/assets/Minecraft Education Edition2 (6).jpg>)

### Добавляем блоки "переместиться вперед, переместиться влево", меняем кол-во повторений с 5 на 3

![](<../../.gitbook/assets/Minecraft Education Edition3 (6).jpg>)

### Еще раз добавляем блоки "переместиться вперед, переместиться влево"

![](<../../.gitbook/assets/Minecraft Education Edition4 (6).jpg>)

### Еще раз добавляем блок повторения

![](<../../.gitbook/assets/Minecraft Education Edition5 (6).jpg>)

### Меняем кол-во повторений с 3 на 1.

![](<../../.gitbook/assets/Minecraft Education Edition6 (4).jpg>)

### Получаем результат

![](<../../.gitbook/assets/Minecraft Education Edition7 (3).jpg>)

{% embed url="https://makecode.com/_dkchPyFo80pH" %}

## 4. Создание пирамиды

\


![](<../../.gitbook/assets/Minecraft Education Edition (3).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition1 (5).jpg>)

{% embed url="https://makecode.com/_AeLi9wEtkMbX" %}

## 5. Линия заданной длинны

Удобно, когда мы можем из чата создать линию такой длины, которая нам необходима.&#x20;

![](<../../.gitbook/assets/Minecraft Education Edition.jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition1 (2).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition2 (2).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition3 (2).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition4 (2).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition5 (2).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition6 (2).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition7 (2).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition8 (2).jpg>)

_Задания:_\
1\. Посадите _n_ тюльпанов по команде _tulips_. 2. Поставьте в ряд _n_ булыжников по команде _stone_ 3. Сделайте заготовку для дороги (выкопайте _n_ ямок и поставьте в них _n_ булыжника). Выполните по команде _road_. _n_ - получите при вводе команды как параметр.

## 6. Прямоугольник c параметрами

Задайте размер прямоугольника с помощью параметра.\


![](<../../.gitbook/assets/Minecraft Education Edition (4).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition1 (6).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition2 (5).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition3 (5).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition4 (5).jpg>)

![](<../../.gitbook/assets/Minecraft Education Edition5 (5).jpg>)

**Задания.**\
Выполните задания с использованием передаваемого параметра. 1. Огородите свою территорию, создав квадрат из булыжника размером 50х50. 2. Создайте квадрат 5х5 из деревянных блоков и наполните его водой (вручную). 3. С помощью команд, после которой агент создает квадрат создайте полностью заполненный квадрат (набор вложенных квадратов с командами 6, 4, 2).&#x20;

![](../../.gitbook/assets/q642.jpg)
