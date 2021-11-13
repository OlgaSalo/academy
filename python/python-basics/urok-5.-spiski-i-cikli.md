# Урок 5. – Списки і цикли

### **Мета** заняття:

Отримати знання стосовно організації списків, їх структури, вбудованих функцій для їх обробки.

### &#xD;Актуалізація опорних знань

1. Змінні і типи даних, оголошення змінних
2. Оператор перевірки умови if..else
3. Циклічні оператори Переривання циклів

### Основні питання, що будуть розглянуті

1. Поняття списків, доступ до їх елементів
2. Методи для роботи з елементами списків
3. Методи для роботи зі списками

Список — **упорядоченный изменяемый** контейнер данных. Списки не диктуют разработчику тип данных, который можно поместить в этот контейнер и могут содержать любые типы данных в любом удобном порядке.

A list is a sequence of values (similar to an array in other programming languages but more versatile). The values in a list are called items or sometimes elements.

The important properties of Python lists are as follows:

* Lists are ordered – Lists remember the order of items inserted.
* Accessed by index – Items in a list can be accessed using an index.
* Lists can contain any sort of object – It can be [numbers](https://www.learnbyexample.org/python-numbers/), [strings](https://www.learnbyexample.org/python-string/), [tuples](https://www.learnbyexample.org/python-tuple/) and even other lists.
* Lists are changeable (mutable) – You can change a list in-place, add new items, and delete or update existing items.

Для создания пустого списка есть два способа:

`my_list = list()`

`empty_list = []`

**Чтобы создать заполненный список:**

`not_empty = [1, 2, 'user']`

You can convert other data types to lists using Python’s [list()](https://www.learnbyexample.org/python-list-function/) constructor.

### Практична робота

* Створити список, який буде містити послідовність символів.
* Створити список, який буде містити числові значення
* Створити список, який буде ім’я, прізвище і кількість повних років учня.

`chars = list('abc')`

`print(chars)`

&#x20;`numbers= list((1, 2, 3))`

`print(numbers)`

`pupil_info = list(('Ivan', 'Ivanov', 15))`

`print(pupil_info)`

### Упорядоченные контейнеры

#### Доступ по индексу

Под упорядоченностью следует понимать свойство контейнера сохранять порядок элементов при работе с ним, удаляя элемент, добавляя новый делая вставку/удаление с конца/начала/средины вы гарантируете что все элементы кроме тех, которых непосредственно коснулась операция, сохраняют порядок.

Самым полезным свойством упорядоченности является возможность доступа к элементам контейнера по индексу этого элемента в контейнере.

![](<../../.gitbook/assets/image (139).png>)

В Python синтаксис доступа по индексу выглядит так:

`some_iterable = ["a", "b", "c"]`

`first_letter = some_iterable[0]`

`middle_one = some_iterable[1]`

`last_letter = some_iterable[2]`

В первой строке мы создали список из трёх первых букв английского алфавита.

Во второй стоке мы сохранили в переменную `first_letter` букву `"a"`, первый элемент `some_iterable`.

**Индекс** в Python начинается с `0`, как и в большинстве языков программирования и индексом `"a"` есть `0`.

Третья строка — это обращение ко второму элементу `some_iterable`, его индекс равен 1 — это буква `"b"` и мы сохраняем её в `middle_one`. Четвертая строка — это обращение к последнему элементу `some_iterable`, букве `"c"`, мы сохраним её в `last_letter` и её индекс равен 2.

Python поддерживает индексирование элементов с конца. Для этого надо добавить - и указать номер элемента с конца. Поскольку в Python `-0 == 0`, то первый элемент с конца — это -1, второй — -2 и так далее. Наш пример можно переписать используя индексирование с конца вот так:

`some_iterable = ["a", "b", "c"]`

`first_letter = some_iterable[-3]`

`middle_one = some_iterable[-2]`

`last_letter = some_iterable[-1]`

### Access Nested List Items

Similarly, you can access individual items in a nested list using multiple indexes. The first index determines which list to use, and the second indicates the value within that list.

The indexes for the items in a nested list are illustrated as below:

![](<../../.gitbook/assets/image (140).png>)

```
L = ['a', 'b', ['cc', 'dd', ['eee', 'fff']], 'g', 'h']

print(L[2][2])
# Prints ['eee', 'fff']

print(L[2][2][0])
# Prints eee
```

### Использование методов объектов

Объект в программировании — некоторая сущность в цифровом пространстве, обладающая определённым состоянием и поведением, имеющая определённые свойства (атрибуты) и операции над ними (методы).

Доступ к методам объектов в Python синтаксически происходит с помощью символа точки после имени объекта и указания имени метода или атрибута к которому нужно получить доступ.

```
numbers = ['a', 'b']
numbers.append('c')
print(numbers)  # ['a', 'b', 'c']
```

В этом примере мы использовали метод append, который есть у списков и он есть у списка `numbers`. Этот метод добавляет новый элемент в конец списка. В качестве аргумента этот метод получает элемент, который надо добавить в список. Аргументы указываются в скобках.

Если метод не требует аргументов (например метод clear), то скобки будут пустыми:

```
num = [1, 2]
num.clear()
print(num)  # []
```

### Методы списков

Добавление элемента в конец списка: `my_list.append(element)`

```
chars = ['a', 'b']
chars.append('c')
print(chars)  # ['a', 'b', 'c']
```

удаление элемента из списка, вызовет ошибку если такого элемента нет в списке: `my_list.remove(element)`

```
chars = ['a', 'b']
chars.remove('b')
print(chars)  # ['a']
```

But keep in mind that if more than one instance of the given item is present in the list, then this method removes only the first instance.

Вернуть i-ый элемент и удалить его из списка i\_element = my\_list.pop(i). По-умолчанию i = -1

```
chars = ['a', 'b']
last = chars.pop(1)
print(chars)  # ['a']
print(last)  # 'b'
```

If you don’t need the removed value, use the del statement.

```
chars = ['a', 'b']
del chars[1]
print(chars)  # ['a']
```

Расширить список a\_list элементами из b\_list: a\_list.extend(b\_list)

```
chars = ['a', 'b']
numbers = [1, 2]
 
chars.extend(numbers)
print(chars)  # ['a', 'b', 1, 2]
```

Вставить x на на позицию с индексом i: my\_list.insert(i, x)

```
chars = ["a", "b"]
chars.insert(1, "c")
print(chars)  # ['a', 'c', 'b']
```

Очистить список: my\_list.clear()

```
chars = ['a', 'b']
last =  chars.clear() print(chars) # []
```

Найти индекс первого элемента в списке равного x: index = my\_list.index(x)

```
chars = ['a', 'b', 'c', 'd']
c_ind = chars.index('c') print(c_ind) #2
```

Вернуть количество элементов в списке равных x: x\_number = my\_list.count(x)

```
chars = ['a', 'b', 'c', 'a']
a_count = chars.count('a')
print(a_count) # 2
```

Отсортировать список по возрастанию: my\_list.sort(key=None, reverse=False)

```
chars = ['z', 'a', 'b']
chars.sort()
print(chars) # ['a', 'b', 'z']
```

Поменять порядок элементов в списке на обратный: my\_list.reverse()

```
chars = ['a', 'b']
chars.reverse()
print(chars) # ['b', 'a']
```

Вернуть копию списка: copy\_of\_my\_list = my\_list.copy()

```
chars =  ['a', 'b']
chars_copy = chars.copy()
chars == chars_copy # True
```

Find List Length

To find the number of items in a list, use len() method.

```
chars = ['a', 'b']
print(len(chars)) # 2
```

Check if item exists in a list

To determine whether a value is or isn’t in a list, you can use in and not in operators with [if statement](https://www.learnbyexample.org/python-if-else-elif-statement/).

```
chars = ['a', 'b']
if 'a' in chars:
    print('yes')
	
if 'www' not in chars:
    print('no')
```

**Iterate through a List**

The most common way to iterate through a list is with a [for loop](https://www.learnbyexample.org/python-for-loop/).

```
chars = ['a', 'b', 'c']
 
for item in chars:
	print(item)
```

### **Практична робота**

Уявимо, що ми розробляємо інформаційну систему продуктового магазину, яка має виконувати наступні функції

* Показ всіх наявних товарів (виведення елементів списку)
* Постачання нових товарів (додавання елементів, об’єднання списків)
* Продаж товарів (пошук елементу списку і видалення його)
* Заміна проданих продуктів на нові (вставка елементу)
* Виведення списку проданих продуктів за день
* Показати історію продажів (виведення списку в зворотньому порядку)

```
products = ['Апельсин', 'Банан']
products_sold = list()
 
print('Продукти в наявності:')
number = 1
for product in products:
	print(number, product)
	number +=1
 
 
print('Постачання продуктів')
print('Введіть назву продукту або 0 для виходу')
while True:
	product = input()
	
	if product == '0' :
    	break
	else:
    	products.append(product)
 
products_new = ['Картопля', 'Цибуля']
products.extend(products_new)
 
 
print('Продукти в наявності:')
number = 1
for product in products:
	print(number, product)
	number +=1
print('Продаж продуктів за назвою:')
print('Введіть назву продукту, який бажаєте купити')
product = input()
if product in products:
	# видаляємо - продано, більше немає
    products.remove(product)
    products_sold.append(product)
	print('Дякуємо за покупку')
else:
    print('Вказаного продукту немає в наявності')
	
 
print('Продаж продуктів за номером:')
print('Введіть номер продукту, який бажаєте купити')
product_index = int(input())
if 0 <= product_index < len(products):
	# видалямо - це продано, більше немає
	product = products.pop(product_index)
    products_sold.append(product)
	print('Ви купили', product)
	print('Дякуємо за покупку')
else:
    print('Неправильно вказаний номер')   
	
 
print('Оновлення продукту:')
product_index = products.index('Картопля')
products.insert(product_index, 'Картопля молода')
	
print('Продукти на кіцець дня:')
number = 1
for product in products:
    print(number, product)
    number +=1
   
	
print('Продукти продані за день:')
products_sold.reverse()
 
for product in products_sold:
    print(product)
```

### **Домашня робота**

* Створити список материків західної півкулі. Доповнити список материками зі східної півкулі. Відсортувати материки за алфавітом і вивести на екран
* Створити список, елементами якого є інші списки, що містять інформацію про ім’я та прізвище студентів. Порахувати скільки людей мають ім’я «Андрій»
