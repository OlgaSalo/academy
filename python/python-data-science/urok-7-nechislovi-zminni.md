# Урок 7: Нечислові змінні

Нечислові змінні \(також: **категоріальні** змінні\) трапляються кількох типів:

1. Розгляньте опитування, яке запитує, як часто ви снідаєте, і пропонує чотири варіанти: "Ніколи", "Рідко", "Більшість днів" або "Кожен день". У цьому випадку дані є категоріальними, оскільки відповіді потрапляють у фіксований набір категорій.
2. Якби люди відповіли на опитування про те, якою маркою автомобілів вони володіли, відповіді потрапляли б у такі категорії, як "Honda", "Toyota" та "Ford". У цьому випадку дані також категоріальні.

Ви отримаєте помилку, якщо спробуєте підключити ці змінні до більшості моделей машинного навчання в Python без попередньої обробки. На цьому уроці ми порівняємо три підходи, які ви можете використовувати для підготовки своїх категоріальних даних.

**Три підходи**

1\) _Видаліть категоріальні змінні_

Найпростіший підхід до роботи з категоріальними змінними - це просто видалити їх із набору даних. Цей підхід буде добре працювати, лише якщо стовпці не містять корисної інформації.

2\) _Кодування лейблами \(ярликами\)_

Кодування міток присвоює кожне унікальне значення якомусь цілому числу.

![](../../.gitbook/assets/image%20%2883%29.png)

Цей підхід передбачає створення зв'язку: "Never" \(0\) &lt; "Rarely" \(1\) &lt; "Most days" \(2\) &lt; "Every day" \(3\).

Це припущення має сенс у цьому прикладі, оскільки існує однозначний рейтинг категорій. Не всі категоріальні змінні мають чітке впорядкування значень, але ми посилаємось на них, як на порядкові змінні. Для моделей на основі дерев \(таких як дерева рішень та random forests\) можна очікувати, що кодування ярликами буде добре працювати з порядковими змінними.

**3\) One-hot encoding**

One-hot encoding створює нові стовпці, що вказують на наявність \(або відсутність\) кожного можливого значення у вихідних даних. Щоб зрозуміти це, розгляньмо на прикладі.

В оригінальному наборі даних "Колір" - це категоріальна змінна з трьома категоріями: "Червоний", "Жовтий" та "Зелений". Відповідний one-hot encoding містить один стовпець для кожного можливого значення та один рядок для кожного рядка у вихідному наборі даних. Там, де початковим значенням було "Червоне", ми ставимо 1 у стовпці "Червоне"; якщо початкове значення було "Жовтий", ми ставимо 1 у стовпці "Жовтий" тощо.

На відміну від кодування ярликами, one-hot encoding не передбачає впорядкування категорій. Таким чином, ви можете очікувати, що такий підхід спрацює особливо добре, якщо в категоріальних даних немає чіткого впорядкування \(наприклад, "Червоний" - це ні більше, ні менше, ніж "Жовтий"\). Ми називаємо категоріальні змінні без внутрішнього ранжування іменними змінними.

Як правило, one-hot encoding погано працює, якщо категоріальна змінна приймає велику кількість значень \(тобто, як правило, ви не будете використовувати one-hot encoding для змінних, що приймають більше 15 різних значень\).

![](../../.gitbook/assets/image%20%2891%29.png)

###  **Практика**

Завантаження даних

```text
import pandas as pd
from sklearn.model_selection import train_test_split

# Локалізовуємо дані
data = pd.read_csv('/content/drive/MyDrive/melb_data.csv')

# Відділяємо ціль для прогнозу від параметрів
y = data.Price
X = data.drop(['Price'], axis=1)

# Ділимо дані на навчальні та перевірочні підмасиви
X_train_full, X_valid_full, y_train, y_valid = train_test_split(X, y, train_size=0.8, test_size=0.2,
                                                                random_state=0)

# Дропаємо всі колонки з пропущеними значеннями (найпростіший підхід)
cols_with_missing = [col for col in X_train_full.columns if X_train_full[col].isnull().any()] 
X_train_full.drop(cols_with_missing, axis=1, inplace=True)
X_valid_full.drop(cols_with_missing, axis=1, inplace=True)

# "Кардинальність" означає к-сть унікальних значень у стовбці
# Оберіть колонки з низькою кардинальністю (прийнято брати 10, але це довільне значення)
low_cardinality_cols = [cname for cname in X_train_full.columns if X_train_full[cname].nunique() < 10 and 
                        X_train_full[cname].dtype == "object"]

# Обери колонки з числовими значеннями
numerical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].dtype in ['int64', 'float64']]

# Лишаємось лише з вибраними колонками
my_cols = low_cardinality_cols + numerical_cols
X_train = X_train_full[my_cols].copy()
X_valid = X_valid_full[my_cols].copy()
```

```text
/usr/local/lib/python3.7/dist-packages/pandas/core/frame.py:4174: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  errors=errors,
```

Гляньмо на нашу щойно організовану таблицю

```text
X_train.head() #head -- верхні 5 рядків
```

|  Type | Method | Regionname | Rooms | Distance | Postcode | Bedroom2 | Bathroom | Landsize | Lattitude | Longtitude | Propertycount |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 12167 | u | S | Southern Metropolitan | 1 | 5.0 | 3182.0 | 1.0 | 1.0 | 0.0 | -37.85984 | 144.9867 | 13240.0 |
| 6524 | h | SA | Western Metropolitan | 2 | 8.0 | 3016.0 | 2.0 | 2.0 | 193.0 | -37.85800 | 144.9005 | 6380.0 |
| 8413 | h | S | Western Metropolitan | 3 | 12.6 | 3020.0 | 3.0 | 1.0 | 555.0 | -37.79880 | 144.8220 | 3755.0 |
| 2919 | u | SP | Northern Metropolitan | 3 | 13.0 | 3046.0 | 3.0 | 1.0 | 265.0 | -37.70830 | 144.9158 | 8870.0 |
| 6043 | h | S | Western Metropolitan | 3 | 13.3 | 3020.0 | 3.0 | 1.0 | 673.0 | -37.76230 | 144.8272 | 4217.0 |

Далі ми отримуємо список усіх категоріальних змінних у навчальних даних.

Ми робимо це, перевіряючи тип даних \(`dtype`\) кожного стовпця. Об'єкт `dtype` перевіряє чи в стовпці є текст \(є й інші речі, які теоретично можуть бути корисними, але це неважливо для наших цілей\). Для цього набору даних **стовпці з текстом** позначають **категоріальні змінні.**

```text
s = (X_train.dtypes == 'object')
object_cols = list(s[s].index)

print("Категоріальні змінні:")
print(object_cols)
```

```text
Категоріальні змінні:
['Type', 'Method', 'Regionname']
```

 Створимо функцію `score_dataset`, яка оцінить якість кожного підходу

```text
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

def score_dataset(X_train, X_valid, y_train, y_valid):
    model = RandomForestRegressor(n_estimators=100, random_state=0)
    model.fit(X_train, y_train)
    preds = model.predict(X_valid)
    return mean_absolute_error(y_valid, preds)
```

 **Підхід 1: видалення**

 Дропаємо `object` через функцію `select_dtypes`

```text
drop_X_train = X_train.select_dtypes(exclude=['object'])
drop_X_valid = X_valid.select_dtypes(exclude=['object'])

print("MAE через підхід 1:")
print(score_dataset(drop_X_train, drop_X_valid, y_train, y_valid))
```

```text
MAE через підхід 1:
175703.48185157913
```

 **Підхід 2: ярликування**

`Scikit-learn` має клас `LabelEncoder`, який можна використовувати для отримання кодування ярликуванням. Ми перебираємо категоріальні змінні та застосовуємо лейбли окремо до кожного стовпця.

```text
from sklearn.preprocessing import LabelEncoder

# робимо копію, щоб уникнути змінення оригінальних даних
label_X_train = X_train.copy()
label_X_valid = X_valid.copy()

# Застосовуємо label encoder до кожної колонки з категоріальними даними
label_encoder = LabelEncoder()
for col in object_cols:
    label_X_train[col] = label_encoder.fit_transform(X_train[col])
    label_X_valid[col] = label_encoder.transform(X_valid[col])

print("MAE через підхід 2:") 
print(score_dataset(label_X_train, label_X_valid, y_train, y_valid))
```

```text
MAE через підхід 2:
165936.40548390493
```

 **Підхід 3: one-hot encoding**

Ми використовуємо клас `OneHotEncoder` від `scikit-learn`, щоб отримати one-hot encoding. Існує ряд параметрів, за допомогою яких можна налаштувати його поведінку.

Ми встановлюємо `handle_unknown = 'ignore'`, щоб уникнути помилок, коли дані перевірки містять класи, які не представлені в навчальних даних, і установлюємо `sparse = False`, що гарантує, що закодовані стовпці повертаються як `numpy`-масив \(замість sparse matrix\).

Для використання one-hot encoding ми надаємо лише категоріальним стовпцям one-hot encoding. Наприклад, для кодування навчальних даних ми локалізовуємо `X_train [object_cols]`. \(`object_cols` у комірці нижче - це перелік назв стовпців із категоріальними даними, і тому `X_train [object_cols]` містить усі категоріальні дані у навчальному наборі.\)

```text
from sklearn.preprocessing import OneHotEncoder

# Застосуємо one-hot encoder до кожної колонки з категоріальними даними
OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[object_cols]))
OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[object_cols]))

# One-hot encoding видалили індекси; вернімо їх!
OH_cols_train.index = X_train.index
OH_cols_valid.index = X_valid.index

# Вилучаємо категоріальні стовбці (доповнимо їх потім через one-hot encoding)
num_X_train = X_train.drop(object_cols, axis=1)
num_X_valid = X_valid.drop(object_cols, axis=1)

# Зливаємо one-hot encoded стовбці з числовими стовбцями
OH_X_train = pd.concat([num_X_train, OH_cols_train], axis=1)
OH_X_valid = pd.concat([num_X_valid, OH_cols_valid], axis=1)

print("MAE через Підхід 3:") 
print(score_dataset(OH_X_train, OH_X_valid, y_train, y_valid))
```

```text
MAE через Підхід 3:
166089.4893009678
```

У цьому випадку відмова від категорійних стовпців \(Підхід 1\) виявилася найгіршою, оскільки вона мала найвищий бал MAE. Що стосується інших двох підходів, оскільки повернені оцінки MAE досить близькі за значенням, здається, ніякої суттєвої різниці немає.

Як правило, **one-hot encoding** \(Підхід 3\), формує найкращі результати, а скидання категоріальних стовпців \(Підхід 1\), як правило, найгірше, але залежить від випадку до випадку.

