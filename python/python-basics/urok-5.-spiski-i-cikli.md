# Урок 5. – Списки і цикли

### **Мета** заняття:

Отримати знання стосовно організації списків, їх структури, вбудованих функцій для їх обробки.

### Актуалізація опорних знань

1. Змінні і типи даних, оголошення змінних
2. Оператор перевірки умови if..else
3. Циклічні оператори Переривання циклів

### Основні питання, що будуть розглянуті

1. Поняття списків, доступ до їх елементів
2. Методи для роботи з елементами списків
3. Методи для роботи зі списками

Список — **упорядоченный изменяемый** контейнер данных. Списки не диктуют разработчику тип данных, который можно поместить в этот контейнер и могут содержать любые типы данных в любом удобном порядке.

A list is a sequence of values \(similar to an array in other programming languages but more versatile\). The values in a list are called items or sometimes elements.

The important properties of Python lists are as follows:

* Lists are ordered – Lists remember the order of items inserted.
* Accessed by index – Items in a list can be accessed using an index.
* Lists can contain any sort of object – It can be [numbers](https://www.learnbyexample.org/python-numbers/), [strings](https://www.learnbyexample.org/python-string/), [tuples](https://www.learnbyexample.org/python-tuple/) and even other lists.
* Lists are changeable \(mutable\) – You can change a list in-place, add new items, and delete or update existing items.

Для создания пустого списка есть два способа:

`my_list = list()`

`empty_list = []`

**Чтобы создать заполненный список:**

`not_empty = [1, 2, 'user']`

You can convert other data types to lists using Python’s [list\(\)](https://www.learnbyexample.org/python-list-function/) constructor.

### Практична робота

* Створити список, який буде містити послідовність символів.
* Створити список, який буде містити числові значення
* Створити список, який буде ім’я, прізвище і кількість повних років учня.

`chars = list('abc')`

`print(chars)`

 `numbers= list((1, 2, 3))`

`print(numbers)`

`pupil_info = list(('Ivan', 'Ivanov', 15))`

`print(pupil_info)`

### Упорядоченные контейнеры

#### Доступ по индексу

Под упорядоченностью следует понимать свойство контейнера сохранять порядок элементов при работе с ним, удаляя элемент, добавляя новый делая вставку/удаление с конца/начала/средины вы гарантируете что все элементы кроме тех, которых непосредственно коснулась операция, сохраняют порядок.

Самым полезным свойством упорядоченности является возможность доступа к элементам контейнера по индексу этого элемента в контейнере.

![](../../.gitbook/assets/image%20%28139%29.png)

В Python синтаксис доступа по индексу выглядит так:

**some\_iterable = \["a", "b", "c"\]**

first\_letter = some\_iterable\[0\]

middle\_one = some\_iterable\[1\]

last\_letter = some\_iterable\[2\]

В первой строке мы создали список из трёх первых букв английского алфавита.

Во второй стоке мы сохранили в переменную first\_letter букву "a", первый элемент some\_iterable.

