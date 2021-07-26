# Урок 10: XGBoost

XGBoost - це провідна бібліотека програмного забезпечення для роботи зі стандартними табличними даними \(тип даних, які ви зберігаєте в`Pandas DataFrames`, на відміну від більш екзотичних типів даних, таких як зображення та відео\). Ретельно налаштувавши параметри, ви можете навчити високоточні моделі!

На цьому уроці ви дізнаєтеся, як будувати та оптимізувати моделі з **посиленням градієнта**. Цей метод досягає найдосконаліших результатів на різноманітних наборах даних.

### **Інтро**

Більшу частину цього курсу ви робили прогнози за допомогою методу `random forests`, який досягає кращих показників, ніж одне дерево рішень, просто шляхом пошуку середнього арифметичного серед прогнозів багатьох дерев рішень.

Ми називаємо метод `random forests`**"методом ансамблю"**. За визначенням, **ансамблеві методи** поєднують передбачення декількох моделей \(наприклад, декількох дерев, у випадку `random forests`\).

Далі ми дізнаємося про інший метод ансамблю, який називається **посиленням градієнта.**

### **Посилення градієнта**

**Посилення градієнта** - це метод, який проходить цикли, щоб ітеративно додавати моделі в ансамбль.

Починається з ініціалізації ансамблю однієї моделі, прогнози якої можуть бути досить наївними \(тобто примітивними\). Навіть якщо його прогнози надзвичайно неточні, наступні доповнення до ансамблю усунуть ці суттєві похибки.

Потім ми починаємо цикл:

1. По-перше, ми використовуємо поточний ансамбль для генерації прогнозів для кожного спостереження в наборі даних. Щоб зробити прогноз, ми враховуємо прогнози з усіх моделей ансамблю.
2. Ці прогнози використовуються для обчислення функції втрат \(_loss_\) \(наприклад, як середньоквадратична помилка\).
3. Потім ми використовуємо функцію втрат, щоб підібрати нову модель, яка буде додана до ансамблю. Зокрема, ми визначаємо параметри моделі, щоб додавання цієї нової моделі до ансамблю зменшило втрати. \(примітка: "Градієнт" у "посиленні градієнта" стосується того факту, що ми використовуватимемо _градієнтний спуск_ на функцію втрат для визначення параметрів у цій новій моделі.\) Нарешті, ми додаємо нову модель до ансамблю, і ... ... повторити!

### **Практика**

знову таки, готуємо наш датасет з нерухомістю:

```text
import pandas as pd
from sklearn.model_selection import train_test_split

# завантаж дані
melbourne_file_path = '/content/drive/MyDrive/melb_data.csv'
data = pd.read_csv(melbourne_file_path)

# Вибери параметри для передбачення
cols_to_use = ['Rooms', 'Distance', 'Landsize', 'BuildingArea', 'YearBuilt']
X = data[cols_to_use]

# Вибери ціль для прогнозування
y = data.Price

# Розділи дані на тренувальні та перевірочні підгрупи
X_train, X_valid, y_train, y_valid = train_test_split(X, y)
```

У цьому прикладі ви будете працювати з бібліотекою `XGBoost`. `XGBoost` означає екстремальне посилення градієнта _\(extreme gradient boosting_\), яке є реалізацією посилення градієнта з кількома додатковими функціями, орієнтованими на продуктивність та швидкість. \(`Scikit-learn` має ще одну версію посилення градієнта, але `XGBoost` має деякі технічні переваги.\)

У наступній комірці коду ми імпортуємо API `scikit-learn` для `XGBoost` \(`xgboost.XGBRegressor`\). Це дозволяє нам будувати та підганяти модель так само, як це було б при scikit-learn. Як ви побачите у вихідних даних, клас `XGBRegressor` має багато параметрів для налаштування - про них ви дізнаєтесь найближчим часом!

```text
from xgboost import XGBRegressor

my_model = XGBRegressor()
my_model.fit(X_train, y_train)
```

```text
[14:57:23] WARNING: /workspace/src/objective/regression_obj.cu:152: reg:linear is now deprecated in favor of reg:squarederror.
XGBRegressor(base_score=0.5, booster='gbtree', colsample_bylevel=1,
             colsample_bynode=1, colsample_bytree=1, gamma=0,
             importance_type='gain', learning_rate=0.1, max_delta_step=0,
             max_depth=3, min_child_weight=1, missing=None, n_estimators=100,
             n_jobs=1, nthread=None, objective='reg:linear', random_state=0,
             reg_alpha=0, reg_lambda=1, scale_pos_weight=1, seed=None,
             silent=None, subsample=1, verbosity=1)
```

Також, ми можемо оцінити точність моделі:

```text
from sklearn.metrics import mean_absolute_error

predictions = my_model.predict(X_valid)
print("Середня похибка: " + str(mean_absolute_error(predictions, y_valid)))
```

Середня похибка: 275108.022339838

###  **Налаштування параметрів**

**XGBoost** має кілька параметрів, які можуть суттєво вплинути на точність і швидкість навчання. Перші параметри, які ви повинні знати:

`n_estimators`

n\_estimators визначає, скільки разів пройти цикл моделювання, описаний вище. Це дорівнює кількості моделей, які ми включаємо в ансамбль.

* Занадто низьке значення спричиняє _недооснащення_, що призводить до неточних прогнозів як щодо даних тренувань, так і даних тестів.
* Занадто велике значення спричиняє _переоснащення_, що спричиняє точні прогнози щодо даних тренувань, але неточні прогнози щодо даних тестів \(що саме нас і цікавить\). Типові значення знаходяться в межах 100-1000, хоча це багато в чому залежить від параметру `learning_rate`, обговореного нижче.

Ось код для встановлення кількості моделей в ансамблі:

```text
my_model = XGBRegressor(n_estimators=500)
my_model.fit(X_train, y_train)
```

```text
[14:57:24] WARNING: /workspace/src/objective/regression_obj.cu:152: reg:linear is now deprecated in favor of reg:squarederror.
XGBRegressor(base_score=0.5, booster='gbtree', colsample_bylevel=1,
             colsample_bynode=1, colsample_bytree=1, gamma=0,
             importance_type='gain', learning_rate=0.1, max_delta_step=0,
             max_depth=3, min_child_weight=1, missing=None, n_estimators=500,
             n_jobs=1, nthread=None, objective='reg:linear', random_state=0,
             reg_alpha=0, reg_lambda=1, scale_pos_weight=1, seed=None,
             silent=None, subsample=1, verbosity=1)
```

`early_stopping_rounds`

early\_stopping\_rounds пропонує спосіб автоматичного пошуку ідеального значення для `n_estimators`. Рання зупинка змушує модель перестати повторюватись, коли оцінка перевірки перестає покращуватися, навіть якщо ми не знаходимося на жорсткій зупинці для n\_estimators. Розумно встановити високе значення для `n_estimators`, а потім використовувати `early_stopping_rounds`, щоб знайти оптимальний час для припинення ітерації.

Оскільки випадковість іноді спричиняє один раунд таких ітерацій, то коли оцінки валідації не покращуються, вам потрібно вказати число, скільки раундів прямого погіршення дозволити перед зупинкою. Встановлення `early_stopping_rounds = 5` є типовим вибором. У цьому випадку ми зупиняємося після 5 раундів погіршення балів перевірки.

При використанні early\_stopping\_rounds вам також потрібно виділити деякі дані для обчислення балів перевірки - це робиться шляхом встановлення параметра `eval_set`.

Змінимо код вище, щоб включити ранню зупинку:

```text
my_model = XGBRegressor(n_estimators=500)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)],
             verbose=False)
```

```text
[14:57:26] WARNING: /workspace/src/objective/regression_obj.cu:152: reg:linear is now deprecated in favor of reg:squarederror.
XGBRegressor(base_score=0.5, booster='gbtree', colsample_bylevel=1,
             colsample_bynode=1, colsample_bytree=1, gamma=0,
             importance_type='gain', learning_rate=0.1, max_delta_step=0,
             max_depth=3, min_child_weight=1, missing=None, n_estimators=500,
             n_jobs=1, nthread=None, objective='reg:linear', random_state=0,
             reg_alpha=0, reg_lambda=1, scale_pos_weight=1, seed=None,
             silent=None, subsample=1, verbosity=1)
```

`learning_rate`

Замість того, щоб отримувати прогнози, просто складаючи передбачення з кожної моделі компонентів, ми можемо помножити передбачення з кожної моделі на невелике значення \(відоме як швидкість навчання\) перед їх додаванням.

Це означає, що кожне дерево, яке ми додаємо до ансамблю, допомагає нам менше. Отже, ми можемо встановити вищі значення для n\_estimators, без `переоснащення`. Якщо ми застосуємо ранню зупинку, відповідна кількість дерев буде визначена автоматично.

Загалом, невелика швидкість навчання та велика кількість n\_estimators дадуть більш точні моделі XGBoost, хоча для навчання також знадобиться більше часу, оскільки вона робить більше ітерацій протягом циклу. За замовчуванням XGBoost встановлює швидкість навчання = 0,1.

Модифікація наведеного вище прикладу для зміни швидкості навчання дає такий код:

```text
my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)], 
             verbose=False)
```

```text
[14:57:27] WARNING: /workspace/src/objective/regression_obj.cu:152: reg:linear is now deprecated in favor of reg:squarederror.
XGBRegressor(base_score=0.5, booster='gbtree', colsample_bylevel=1,
             colsample_bynode=1, colsample_bytree=1, gamma=0,
             importance_type='gain', learning_rate=0.05, max_delta_step=0,
             max_depth=3, min_child_weight=1, missing=None, n_estimators=1000,
             n_jobs=1, nthread=None, objective='reg:linear', random_state=0,
             reg_alpha=0, reg_lambda=1, scale_pos_weight=1, seed=None,
             silent=None, subsample=1, verbosity=1)
```

`n_jobs`

У більших наборах даних, де час роботи є важливим, ви можете використовувати паралелізм, щоб швидше будувати свої моделі. Загальноприйнятим є встановлення параметра `n_jobs` рівним кількості ядер на вашому компуктері. На менших наборах даних це не допоможе.

Отримана модель не буде нічим кращою, тому мікрооптимізація часу підгонки, як правило, це ні що інше, як відволікання уваги :\) . Але це корисно у великих наборах даних, де ви в іншому випадку витратили б довше часу на очікування під час команди `fit`.

Ось модифікований приклад:

```text
my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05, n_jobs=4)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)], 
             verbose=False)
```

```text
[14:57:30] WARNING: /workspace/src/objective/regression_obj.cu:152: reg:linear is now deprecated in favor of reg:squarederror.
XGBRegressor(base_score=0.5, booster='gbtree', colsample_bylevel=1,
             colsample_bynode=1, colsample_bytree=1, gamma=0,
             importance_type='gain', learning_rate=0.05, max_delta_step=0,
             max_depth=3, min_child_weight=1, missing=None, n_estimators=1000,
             n_jobs=4, nthread=None, objective='reg:linear', random_state=0,
             reg_alpha=0, reg_lambda=1, scale_pos_weight=1, seed=None,
             silent=None, subsample=1, verbosity=1)
```

