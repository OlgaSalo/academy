# Урок 6. – Робота зі строками

### Мета заняття:

Отримати знання стосовно строк, їх структури, вбудованих функцій для їх обробки.

### Актуалізація опорних знань

1. Змінні і типи даних, оголошення змінних
2. Оператор перевірки умови if..else
3. Циклічні оператори
4. Переривання циклів

### Основні питання, що будуть розглянуті

1. Поняття строк, способи створення, доступ до їх елементів
2. Методи для роботи зі строками

A string is a sequence of characters.In Python, strings come with a powerful set of processing tools.

Для создания строк можно воспользоваться одинарными или двойными кавычками:

```
this_is_string = "Hi there!"
 
the_same_string = 'Hi there!'
 
this_is_string == the_same_string  # True
```

Но что делать, если нам нужен текст с переносами строк (когда в тексте более одной строки)? Для этого можно воспользоваться тройным повторением кавычек:

```
text = """This is first line
And second line
Last third line"""
 
song = '''Jingle bells, jingle bells
Jingle all the way
Oh, what fun it is to ride
In a one horse open sleigh'''
```

В этом примере переменная `text` содержит три строки, а `song` — четыре строки.

Когда интерпретатор обнаруживает кавычки повторенные трижды, он воспринимает все символы до следующих трех закрывающих кавычек как символы строки.

Обратная ситуация, у вас есть длинная строка, которая не должна содержать переносов, но в коде её неудобно отобразить одной строкой.

```
one_line_text = "Textual data in Python is handled with str objects, or strings. Strings are immutable sequences of Unicode code points. String literals are written in a variety of ways: single quotes, double quotes, triple quoted.
```

Чтобы структурировать код и не добавлять лишних переносов вы можете разбить одну строковую переменную на несколько частей:

```
one_line_text = "Textual data in Python is handled with str objects, or strings. "\
            	"Strings are immutable sequences of Unicode code points. "\
            	"String literals are written in a variety of ways."

```

Обратите внимание на символ  в конце первой и второй строк кода, он указывает интерпретатору игнорировать окончание строки и продолжить сразу со следующей.

`one_line_text` в обоих примерах будет содержать один и тот же текст без переносов.

### The str() Constructor

You can convert almost any object in Python to a string using a type constructor called str()

```
# an integer to a string
s = str(15)
print(s)
 
 
# a list to a string
s = str([12, 11])
print(s)
```

### **Access Characters by Index**

You can access individual characters in a string using an index in square brackets. The string indexing starts from 0.

You can also access a string by negative indexing. A negative string index counts from the end of the string.

```
# Indexing
S = 'ABCDEFGHI'
print(S[1])	# Prints B
print(S[4])	# Prints E
 
# Negative Indexing
S = 'ABCDEFGHI'
print(S[-2])	# Prints H
print(S[-6])	# Prints D
```

### **Практична робота**

Створити строку, яка складається з імені і прізвища учня. Порівняти, чи перша літера імені співпадає з першою літерою прізвища і вивести відповідне повідомлення. При отриманні літери прізвища використати від’ємний індекс.

```
pip = 'Ivan Ivanov'
first_name_start = pip[0]
last_name_start = pip[-6]
 
print(first_name_start)
print(last_name_start)
 
if first_name_start == last_name_start :
	print('first name and last name strts with', first_name_start)
```

### **Slicing a String**

A segment of a string is called a slice and you can extract one by using a slice operator. A slice of a string is also a string.

The slice operator \[n:m] returns the part of the string from the “n-th” item to the “m-th” item, including the first but excluding the last.

### **Практична робота**

Визначте результат роботи функції slice, не запускаючи код

```
s = 'abcdefghijk'
s[3:5]
s[:6]
s[3:]
s[::-1]
s[-3:]
s[:-5]
s[-1:-6:-2]
```

### **Modify a String**

It is tempting to use the \[] operator on the left side of an assignment, in order to convert a character into a string. for example:

```
S = 'Hello, World!'
S[0] = 'H'
```

```
TypeError: 'str' object does not support item assignment
```

The reason for the error is that the strings are unchangeable (immutable) and because of which you cannot change the existing string. The best you can do is create a new string that is a variation of the original:

### **String Concatenation**

You can concatenate strings using the concatenation operator `+` or the augmented assignment operator `+=`

```
S = 'Hello,' + ' World!'
print(S)
# Hello, World!
```

You can replicate substrings in a string using the replication operator `*`

```
delimiter = '-' * 25
print(delimiter)
 
s = 'abc' * 3
print(s)
```

### **Специальные символы**

Мы неоднократно упоминали символ переноса строки. Это один из "специальных" или "управляющих" символов. Управляющие символы — это символы переноса строки, табуляции, возврата каретки и другие символы, которые нельзя или неудобно ввести с клавиатуры.

Для того, чтобы можно было вводить символы, которые с клавиатуры неудобно или нельзя ввести, придумали добавлять **экранирующий символ** '\\' который обозначает, что следующий за ним знак надо воспринимать как специальный символ, а не буквально.

Вот некоторые управляющие символы:

| **Обозначение в коде** | **Описание**                 |
| ---------------------- | ---------------------------- |
| **\n**                 | **Перевод строки**           |
| **\f**                 | **Перевод страницы**         |
| **\r**                 | **Возврат каретки**          |
| **\t**                 | **Горизонтальная табуляция** |
| **\v**                 | **Вертикальная табуляция**   |

Например, текст с явным разбиением на строки:

```
jingle_bells = "Jingle bells, jingle bells\nJingle all the way\nOh, what fun it is to ride\nIn a one horse open sleigh"

print(jingle_bells)

Jingle bells, jingle bells
Jingle all the way
Oh, what fun it is to ride
In a one horse open sleigh
```

### **Методы строк**

Мы уже познакомились с некоторыми методами строк, сейчас разберем методы связанные с поиском в строках и их созданием новых строк.

### **Find String Length**

To find the number of characters in a string, use [len()](https://www.learnbyexample.org/python-len-function/) built-in function.

```
S = 'Hello, World!'

print(len(S))
```

### count() Method

The count() method returns the number of times the substring sub appears in the [string](https://www.learnbyexample.org/python-string/).

You can limit the search by specifying optional arguments start and end.

`string.count(sub,start,end)`

### **Iterate Through a String**

To iterate over the characters of a string, use a simple [for loop](https://www.learnbyexample.org/python-for-loop/).

```
s = 'Hello, World!'
for letter in s:
	print(letter, end=' ')
```

### **String Case Conversion**

Python provides five methods to perform case conversion on the target string viz. [lower()](https://www.learnbyexample.org/python-string-lower-method/), [upper()](https://www.learnbyexample.org/python-string-upper-method/), [capitalize()](https://www.learnbyexample.org/python-string-capitalize-method/), [swapcase()](https://www.learnbyexample.org/python-string-swapcase-method/) and [title()](https://www.learnbyexample.org/python-string-title-method/)

```
S = 'Hello, World!'
print(S.lower())
# Prints hello, world!
```

```
S = 'Hello, World!'
print(S.upper())
# Prints HELLO, WORLD!
```

```
S = 'Hello, World!'
print(S.capitalize())
# Prints Hello, world!
```

```
S = 'Hello, World!'
print(S.swapcase())
# Prints hELLO, wORLD!
```

```
S = 'hello, world!'
print(S.title())
# Prints Hello, World!
```

### **Поиск в строке**

Для поиска некоторого символа или подстроки в строке можно воспользоваться методом `find`:

```
s = "Hi there!"
 
start = 0
end = 5
 
print(s.find("er", start, end)) # -1
print(s.find("q"))  # -1
```

Этот метод выводит индекс начала первого совпадения в строке `s` начиная с `start` до `end`. Если `start` и `end` не указаны, то с начала и до конца строки. Возвращает -1, если последовательность не найдена.

The rfind() method searches for the last occurrence of the specified substring sub and returns its index. If specified substring is not found, it returns -1.

The optional arguments start and end are used to limit the search to a particular portion of the [string](https://www.learnbyexample.org/python-string/).

```
s = 'Some words'
s.rfind('o')  # 6
```

### **Практична робота**

Ввести довільне повідомлення з клавіатури. Якщо в повідомленні трапляються слова «купити», «продати», «реклама», то помітити це повідомлення як спам.

```
adv_words = ['купити', 'продати', 'реклама']
user_text = input()
not_found = -1
is_spam = False
 
for stop_word in adv_words :
	if user_text.find(stop_word) != not_found :
    	is_spam = True
    	break
	
message = 'Spam' if is_spam else 'Not Spam' 	
print(message)
```

### **Разбиение строки на несколько подстрок**

Частая ситуация, когда необходимо разбить строку на подстроки по некоторому символу, например, разбить текст на предложения по символу точки и пробела после точки, или предложение по словами.

```
s = "I am learning strings in Python. Some new methods got now."
sentences = s.split(". ")
 
print(sentences[0]) # I am learning strings in Python
print(sentences[1]) # Some new methods got now.
```

### **Практична робота**

Ввести довільне речення з клавіатури і порахувати кількість слів.

```
s = input().split()
print(s)
print(len(s))
```

### **Новые строки на основе строк**

Все строки неизменяемы, если мы хотим модифицировать строку, то есть только один способ — создать новую строку на основе исходной.

Все методы, которые как-то "модифицируют" строки возвращают новые строки никак не изменяя оригинальную.

Для объединения нескольких строк в одну через некоторый разделитель используется метод `join`:

```
sentences = ["I am learning strings in Python", "Some new methods got now."]
text = ". ".join(sentences)
print(text) # I am learning strings in Python. Some new methods got now.
```

По сути, это операция обратная `split`

Если нужно удалить лишние пробелы в начале и конце строки есть специальный метод `strip`:

```
clean = '   spacious   '.strip()
print(clean)  # spacious
```

Когда же нам надо заменить некоторую подстроку в строке мы можем воспользоваться методом `replace`:

```
dog_text = "All dogs bark like dogs."
cat_text = dog_text.replace("dogs", "cats")
print(cat_text) # All cats bark like cats.
```

### **Translate**

У строк есть метод translate, этот метод позволяет заменить символ в строке на другой из карты соответствия, которую можно задать.

В этом примере картой соответствия выступает словарь map и в этой карте мы устанавливаем соответствие между символами 'з' и 'z', и 'ю', и 'u'.

```
map = {ord('з'): 'z', ord('ю'): 'u'}
translated = 'зю'.translate(map)
print(translated) # zu
```

### **String Formatting/String Interpolation**

In Python, there are three major ways to embed variables inside a string.

* printf-style % String Formatting
* str.format() Built-in Method
* f-String Formatter

```
# printf-style % string formatting
S = 'Мене звати %s. Мені %d років.' % ('Олег', 14)
print(S)
```

```
# format() Built-in Method
S = 'Мене звати {1}. Мені {0} років.'.format(14, 'Олег')
print(S)
```

```
# f-String Formatter
name = 'Олег'
age = 14
S = f"Мене звати {name}. Мені {age} років."
print(S)
```

### **Спецификация**

Спецификация гораздо более сложный модификатор. С её помощью можно:

* менять точность представления дробных чисел (округлять до указанного количества знаков);

`print('pi: {:0.6}'.format(3.1415))`

* как отображать знак чисел:

`print('"{}" "{:+}" "{:-}" "{: }"'.format(1, 2, -3, 4)) # "1" "+2" "-3" " 4"`

* как выровнять положение элемента и чем (какими символами) дополнить;

`print("|{:<10}|{:*^10}|{:>10}|".format('left', 'center', 'right'))`

### **Практична робота**

Вивести таблицю проданих за день товарів в наступному форматі: номер, назва, кількість, ціна.

```
elimiter = '-' * 80
goods = [['Апельсин', 6, 150], ['Лимон', 8, 90], ['Картопля', 123, 445]]
 
total_sum = 0
number = 0
 
print(delimiter)
print("|{:^5}|{:<40}|{:>15}|{:>15}|".format('№', 'Товар', 'кількіть', 'вартість'))
print(delimiter)
 
for good in goods :
    name = good[0]
    count = good[1]
    money = good[2]
    number += 1;
    total_sum += money
    print("|{:^5}|{:<40}|{:>15}|{:>15}|".format(number, name, count, money))
 
print(delimiter)
print("|{:<62}|{:>15}|".format(' Продано всього', total_sum))
print(delimiter)
```

```
--------------------------------------------------------------------------------
|  №  |Товар                                   |       кількіть|       вартість|
--------------------------------------------------------------------------------
|  1  |Апельсин                                |              6|            150|
|  2  |Лимон                                   |              8|             90|
|  3  |Картопля                                |            123|            445|
--------------------------------------------------------------------------------
| Продано всього                                               |            685|
--------------------------------------------------------------------------------
```

### **Домашня робота**

* Порахувати, яка літера найбільш часто зустрічається у вашому прізвищі
* Ввести строку з клавіатури. Видалити з неї всі цифри. \
