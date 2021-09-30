# Урок 13. Практика \(flex-box - шапка сайту\)

### Мета:

* навчитися верстати шапку сайту відповідно до макету
* розвивати навички комбінаторного мислення та конструкторської уяви
* виховувати прагнення до написання чистого лаконічного коду

### І. Організація навчального процесу

Перевірка якості зв'язку та присутності студентів на занятті. Пропонуємо всім запустити редактор коду.

### ІІ. АОЗ

1. Як ви думаєте, в яких випадках варто змінювати порядок відображення елементів?
2. Без якої властивості не працює `flex-shrink`?
3. Продемонструйте синтаксис запису властивості `flex`.
4. Як працює властивість `align-self`?

### ІІІ. Мотивація

Сьогодні буде тільки практика! Майже кожен сайт має шапку. В ній міститься найважливіша інформація. Варто розробити її якнайкраще! То чому б не навчитись робити це прямо зараз?:\)

### IV. Практична робота

Починаємо зі створення окремої директорії \(папки\) для окремого проекту.

![](../.gitbook/assets/image%20%28148%29.png)

Я альтернативу, можна використовувати онлайн редактор [CodePen](https://codepen.io/)

#### Розмітка меню

{% file src="../.gitbook/assets/luxestate.psd" caption="Розмітка меню" %}

На практиці в шапці сайту на одному рівні разом із логотипом розташоване меню, та часто бувають кнопки авторизації на сайті.

Верстаемо наступного типу код:

```text
<!-- HTML розмітка -->

<header>
  <h1><a href="index.html" class="logo">luxestate</a></h1>
  <nav>
    <ul class="nav_menu">
      <li class="nav_menu_item">
        <a href="#" class="nav_menu_link">About</a>
      </li>
      <li class="nav_menu_item">
        <a href="#" class="nav_menu_link">Appartments</a>
      </li>
      <li class="nav_menu_item">
        <a href="#" class="nav_menu_link">How it works</a>
      </li>
      <li class="nav_menu_item">
        <a href="#" class="nav_menu_link">Agents</a>
      </li>
      <li class="nav_menu_item">
        <a href="#" class="nav_menu_link">Contact us</a>
      </li>
    </ul>
  </nav>
  <div class="join_block">
    <input type="button" value="Join us">
    <input type="button" value="Getting started">
  </div>
</header>
```

#### Стилимо хедер

Щоб вишикувати дочірні елементи шапки варто для `header` дати `display: flex;` Також варто встановити правильну ширину хедера відповідно до макету.

Таким чином пишемо наступні стилі:

```text
/* global styles */
body {
  font-family: 'Montserrat', serif;
  color: #1f373d;
}

a {
  color: #1f373d;
}

/* header */
header {
  width: 1024px;
  max-width: 100%;
  margin: 0 auto;
  padding: 35px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
```

#### Логотип

Прибираємо з логотипу сліди посилання та даємо правильні властивості шрифта. Викладачу варто узагальнити раніше набуті знання студентів про підключення шрифтів до проекту.

```text
.logo {
  text-decoration: none;
  font-size: 25px;
  font-weight: 600;
}
```

#### Меню

Меню здебільшого створюється через маркований список. Тому, в стилях ми прибираємо маркери, та вирівнюємо елементи списку в один ряд. Щоб, вирівняти елементи меню по ширині. дамо фіксовану ширину блоку `nav`.

```text
/* nav-menu */
nav {
  width: 65%;
}
.nav_menu {
  width: 100%;
  list-style: none;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.nav_menu a {
  font-size: 13px;
  font-weight: 400;
}
```

#### Кнопки авторизації

Такі кнопки варто створити, використовуючи елементи `<input type="button">`. Це полегшить їх стилізацію. А так як дизайн кнопок відрізняється, то пропоную розрізнити їх класами `.join` і `.started` відповідно.

Гарним тоном буде дати ховер-ефект для кнопок

```text
<!-- Додаємо класи до кнопок в HTML-розмітці -->

<input type="button" value="Join us" class="join">
<input type="button" value="Getting started" class="started">

/* CSS-стилі */

/* join_block */
.join {
  background: none;
  border: none;
  padding: 0 20px;
  transition: opacity .3s;
}
.started {
  background: #ffcc01;
  border: none;
  border-radius: 6px;
  padding: 14px 25px 13px;
  transition: opacity .3s;
}
.join:hover,
.started:hover {
  opacity: .7;
  cursor: pointer;
}
```

Ось такі прості дії дають нам готовий якісний результат і чистий код без зайвих символів.

В кінці заняття ми повинні отримати наступний код та результат: [https://codepen.io/mediol-git/pen/dyWWOOw?editors=1100](https://codepen.io/mediol-git/pen/dyWWOOw?editors=1100)

### V. Узагальнення отриманих навичок

1. Чому ми логотип пишемо через посилання?
2. Яким чином ми досягли горизонтального вирівнювання елементів меню?
3. Які стилі ми винесли в глобальний розділ CSS-таблиці і чому?
4. Як ми вирівняли шапку сайту по центру відносно вікна браузера?
5. Навіщо **header'у** дали властивість `max-width: 100%`?
6. Як ми досягли плавності ховер-ефектів кнопок?
7. Які особливості `transition` ви запам'ятали?

### VI. Домашнє завдання

Завершити стилізацію макета [за посиланням](https://app.schoology.com/attachment/1690243710/source/43c4de3c2e4527ba30dea723be71976d.psd)

