# Урок 8: Конвеєр (pipeline)

Конвеєри - це простий спосіб організувати код моделювання даних. Зокрема, конвеєр поєднує кроки попередньої обробки та моделювання, щоб ви могли використовувати весь комплект так, немов це був би один крок.

Багато вчених наук про дані надають перевагу моделям без конвеєрів, але вони мають деякі важливі переваги. До них належать:

1. Чистіший код: Облік даних на кожному етапі попередньої обробки може бути безладним. За допомогою конвеєра вам не потрібно буде відстежувати навчальні дані та дані перевірки вручну на кожному кроці.
2. Менше помилок: менше можливостей неправильно виконати крок.
3. Простіші у запусці: може бути напрочуд важко перевести модель з прототипу на щось, що можна розгорнути в перспективі. Ми не будемо вдаватися до багатьох пов'язаних з цим проблем, але `pipelines` можуть допомогти.
4. Додаткові параметри перевірки моделі: розглянемо на наступному уроці про перехресну перевірку

&#x20;**Практика**

З минулого заняття:

```
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

#Категоріальні колонки
categorical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].nunique() < 10 and 
                        X_train_full[cname].dtype == "object"]

#Числові колонки
numerical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].dtype in ['int64', 'float64']]

# Лишаємо лише обрані колонки
my_cols = categorical_cols + numerical_cols
X_train = X_train_full[my_cols].copy()
X_valid = X_valid_full[my_cols].copy()
```

Ми зазирнемо до даних тренувань методом `head()` нижче. Зверніть увагу, що дані містять як категоріальні дані, так і стовпці з відсутніми значеннями. З конвеєрами легко впоратися з обома труднощами!

```
X_train.head()
```



| <p><br>Type</p> | Method | Regionname | Rooms | Distance | Postcode | Bedroom2 | Bathroom | Car | Landsize | BuildingArea | YearBuilt | Lattitude | Longtitude | Propertycount |
| --------------- | ------ | ---------- | ----- | -------- | -------- | -------- | -------- | --- | -------- | ------------ | --------- | --------- | ---------- | ------------- |

| 12167 | u | S | Southern Metropolitan | 1 | 5.0 | 3182.0 | 1.0 | 1.0 | 1.0 | 0.0 | NaN | 1940.0 | -37.85984 | 144.9867 | 13240.0 |
| ----- | - | - | --------------------- | - | --- | ------ | --- | --- | --- | --- | --- | ------ | --------- | -------- | ------- |

| 6524 | h | SA | Western Metropolitan | 2 | 8.0 | 3016.0 | 2.0 | 2.0 | 1.0 | 193.0 | NaN | NaN | -37.85800 | 144.9005 | 6380.0 |
| ---- | - | -- | -------------------- | - | --- | ------ | --- | --- | --- | ----- | --- | --- | --------- | -------- | ------ |

| 8413 | h | S | Western Metropolitan | 3 | 12.6 | 3020.0 | 3.0 | 1.0 | 1.0 | 555.0 | NaN | NaN | -37.79880 | 144.8220 | 3755.0 |
| ---- | - | - | -------------------- | - | ---- | ------ | --- | --- | --- | ----- | --- | --- | --------- | -------- | ------ |

| 2919 | u | SP | Northern Metropolitan | 3 | 13.0 | 3046.0 | 3.0 | 1.0 | 1.0 | 265.0 | NaN | 1995.0 | -37.70830 | 144.9158 | 8870.0 |
| ---- | - | -- | --------------------- | - | ---- | ------ | --- | --- | --- | ----- | --- | ------ | --------- | -------- | ------ |

| 6043 | h | S | Western Metropolitan | 3 | 13.3 | 3020.0 | 3.0 | 1.0 | 2.0 | 673.0 | 673.0 | 1970.0 | -37.76230 | 144.8272 | 4217.0 |
| ---- | - | - | -------------------- | - | ---- | ------ | --- | --- | --- | ----- | ----- | ------ | --------- | -------- | ------ |

&#x20;**Крок 1**

Подібно до того, як конвеєр об’єднує кроки попередньої обробки та моделювання, ми використовуємо клас `ColumnTransformer` для об’єднання різних кроків попередньої обробки. Код нижче:

1. вказує відсутні значення в числових даних
2. обчислює відсутні значення та застосовує one-hot encoding до категоріальних даних.

```
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder

# Preprocessing for numerical data
numerical_transformer = SimpleImputer(strategy='constant')

# Preprocessing for categorical data
categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])

# Bundle preprocessing for numerical and categorical data
preprocessor = ColumnTransformer(
    transformers=[
        ('num', numerical_transformer, numerical_cols),
        ('cat', categorical_transformer, categorical_cols)
    ])
```

&#x20;**Крок 2**: визначити тип моделі

Застосуємо random forest

```
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(n_estimators=100, random_state=0)
```

**Крок 3**: збираємо до купи

Нарешті, ми використовуємо клас `Pipeline`, щоб визначити конвеєр, який об’єднує етапи попередньої обробки та моделювання. Є кілька важливих речей, на які слід звернути увагу:

За допомогою конвеєра ми попередньо обробляємо навчальні дані та вміщуємо модель в один рядок коду. (без конвеєра нам довелося би розбити обчислення, one-hot encoding та навчання моделі на окремі етапи)

За допомогою конвеєра ми надаємо необроблені функції в `X_valid` до команди `predict()`, і конвеєр автоматично попередньо обробляє функції перед генеруванням прогнозів.

```
from sklearn.metrics import mean_absolute_error

my_pipeline = Pipeline(steps=[('preprocessor', preprocessor),
                              ('model', model)
                             ])

# Тренуємо модель
my_pipeline.fit(X_train, y_train)

# Створюємо масив передбачень
preds = my_pipeline.predict(X_valid)

# оцінюємо модель
score = mean_absolute_error(y_valid, preds)
print('MAE:', score)
```

```
MAE: 160679.18917034855
```
