# Урок 5: Random Forests

Ви вже кілька разів бачили як ми завантажуємо данні. Пригадаймо, що під кінець цього процесу у нас по суті є 4 підмасиви даних:

1. train\_X
2. val\_X
3. val\_y
4. train\_y

Згадаймо вкотре цей код:

```text
import pandas as pd

# посилання до датасету з даними про будинки Мельбурну
melbourne_file_path = '/content/drive/MyDrive/melb_data.csv'

# Створіть об'єкт, який міститиме в собі наш датасет
melbourne_data = pd.read_csv(melbourne_file_path) 

######################
melbourne_data.columns

# Дані будинків Мельбурну містять пусті комірки (деякі змінні деяких характеристик будинків не були записані)
# Ми навчимося як працювати з опущеними даними згодом 
# А поки, щоб уникнути труднощів, ми не враховуватимемо ВСІ будинки, у яких є пропущені змінні

melbourne_data = melbourne_data.dropna(axis=0)

y = melbourne_data.Price
melbourne_features = ['Rooms', 'Bathroom', 'Landsize', 'Lattitude', 'Longtitude']
X = melbourne_data[melbourne_features]

from sklearn.model_selection import train_test_split

# Тут ми розіб'ємо дані на навчальні та перевірочні: що для X та y
# Розбиття (далі: спліт) базується на основі генератора випадкових чисел.
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state = 0)
```

 Ми будуємо модель `випадкового лісу` аналогічно до того, як ми створювали дерево рішень у scikit-learn, але цього разу використовуємо клас `RandomForestRegressor` замість `DecisionTreeRegressor`.

```text
from sklen.metrics import mean_absolute_error

forest_model = RandomForestRegressor(random_state=1)
forest_model.fit(train_X, train_y)
melb_preds = forest_model.predict(val_X)
print(mean_absolute_error(val_y, melb_preds))
```

207190.6873773146

Тут явно є місце для подальшого вдосконалення, але це вже значне поліпшення порівняно з найбільшою помилкою дерева рішень у 250 000. Існують параметри, які дозволяють вам змінити ефективність `Random Forests` так само, як при зміні максимальної глибини дерева рішень. Але однією з найкращих особливостей моделей `Random Forest` є те, що вони, як правило, працюють розумно навіть без такої настройки.

