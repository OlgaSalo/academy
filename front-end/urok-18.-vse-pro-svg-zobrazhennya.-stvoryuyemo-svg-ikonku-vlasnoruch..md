# Урок 18. Все про SVG зображення. Створюємо SVG іконку власноруч.

## Мета:

* навчитись розуміти принципи побудови SVG зображень
* розвивати просторову уяву та навички застосування зображень на веб-сторінці
* виховувати прагнення до полегшення ваги сайту.

## І. Організація навчального процесу

Перевірка готовності учнів до уроку. Відповіді на запитання учнів стосовно ДЗ. Налагодження діалогу.

## ІІ. АОЗ

1. Що може сприяти прискоренню завантаження веб-сторінок?
2. Які формати варто використовувати для іконок?
3. Які недоліки підключення іконок через сторонні сервіси?

## ІІІ. Повідомлення теми, мети та завдань уроку

На цьому занятті ми розберемося із принципами побудови SVG іконок, а також спробуємо власноруч створити таке зображення.

## IV. Вивчення нового матеріалу

Ми можемо вважати Масштабовану Векторну Графіку \(Scalable Vector Graphics - SVG\) гнучкою графікою. SVG створений на основі формату XML, який дозволяє створювати зображення, використовуючи теги та атрибути. Наш код згенерує зображення, яке можна змінювати прямо в текстовому редакторі.

SVG безмежно масштабується, має дуже малу вагу файлу, може бути стилізований та анімований.

### **Векторні зображення проти растрових**

![&#x420;&#x430;&#x441;&#x442;&#x440;&#x43E;&#x432;&#x435; &#x437;&#x43E;&#x431;&#x440;&#x430;&#x436;&#x435;&#x43D;&#x43D;&#x44F;](../.gitbook/assets/tweet-rastr.gif)

![&#x412;&#x435;&#x43A;&#x442;&#x43E;&#x440;&#x43D;&#x435; &#x437;&#x43E;&#x431;&#x440;&#x430;&#x436;&#x435;&#x43D;&#x43D;&#x44F;](../.gitbook/assets/tweet-vector.gif)

### **SVG теги**

Тег `<svg>` впроваджує SVG-документ всередину поточного документа, наприклад HTML. Тег має власні координати X і Y, висоту та ширину, і унікальний id.

Приклад використання такого тегу:

```text
<svg width="580" height="400" xmlns="http://www.w3.org/2000/svg">
```

Тег `<g>` групує елементи разом і веде себе як контейнер для пов'язаних графічних елементів. Елемент `<g>` також може містити в собі такі ж елементи `<g>`.

Приклад такого тегу:

```text
<g>
  <title>background</title>
  <rect fill="#fff" id="canvas_background" height="402" width="582" y="-1" x="-1"/>
  <g display="none" overflow="visible" y="0" x="0" height="100%" width="100%" id="canvasGrid">
    <rect fill="url(#gridpattern)" stroke-width="0" y="0" x="0" height="100%" width="100%"/>
  </g>
</g>
```

Елемент `<rect>` являє собою базову фігуру SVG - прямокутник. Він може мати різні атрибути, такі як координати, висота, ширина, колір заливки, колір обводки та гострі або заокруглені кути.

Приклад:

```text
<rect id="svg_1" height="253" width="373" y="59" x="107.5" stroke-width="1.5" stroke="#000" fill="#fff"/>
```

Елемент `<use>` дозволяє клонувати і повторно використовувати графічні елементи SVG, в тому числі такі елементи як `<g>`, `<rect>`, а також інші `<use>` елементи.

Приклад його використання:

```text
<text y="15">black</text>
<use x="50" y="10" xlink:href="#Port" />

<text y="35">red</text>
<use x="50" y="30" xlink:href="#Port"/>

<text y="55">blue</text>
<use x="50" y="50" xlink:href="#Port" style="fill:blue"/>
```

Елемент `<path>` визначає шлях, що складається з координат точок для формування фігури. Код із використанням `<path>` може здатися магією, але не лякайтесь. Нижче в прикладі код можна прочитати так:

* «M150 0» — змістити на \(150,0\);
* «L75 200» — намалюй лінію до \(75,200\) від попередньої точки \(яка мала координати \(150,0\)\);
* «L255 200» — намалюй лінію до \(225,200\) від попередньої точки \(яка мала координати \(75,200\)\);
* «Z» — закрий шлях \(намалюй лінію до початкової точки\).

Вивчати такий код не обов'язково, так як його може згенерувати будь-який SVG редактор. Але буде дуже круто, якщо ви будете розуміти цей код.

Приклад:

```text
<svg height="210" width="400">
  <path d="M150 0 L75 200 L225 200 Z" />
</svg>
```

І, нарешті, елемент `<symbol>` визначає символи, які можуть бути використані повторно. Ці символи промальовуються тільки за допомогою тега `<use>`.

Приклад використання тега `<symbol>`:

```text
<svg>
  <symbol id="sym01" viewBox="0 0 150 110">
    <circle cx="50" cy="50" r="40" stroke-width="8" stroke="red" fill="red"/>
    <circle cx="90" cy="60" r="40" stroke-width="8" stroke="green" fill="white"/>
  </symbol>
  <use xlink:href="#sym01" x="0" y="0" width="100" height="50"/>
  <use xlink:href="#sym01" x="0" y="50" width="75" height="38"/>
  <use xlink:href="#sym01" x="0" y="100" width="50" height="25"/>
</svg>
```

## V. Закріплення знань на практиці

### **Створюємо SVG анімацію**

Для роботи ми використаємо простий [онлайн-редактор](https://editor.method.ac/).

* Створюємо коло.

![](../.gitbook/assets/image%20%28131%29.png)

* Потім додаємо більше кул та зберігаємо вихідний код.

![](../.gitbook/assets/image%20%28129%29.png)

### **CSS3-анімація**

SVG може бути анімований за допомогою додавання атрибутів `id` або `class` SVG-тегам, та їх стилізації за допомогою CSS. Нижче, приводжу приклад анімації SVG.

```text
<!-- HTML -->
<svg width="580" height="400" xmlns="http://www.w3.org/2000/svg">
 
 <g>
  <title>background</title>
  <rect fill="#fff" id="canvas_background" height="402" width="582" y="-1" x="-1"/>
  <g display="none" overflow="visible" y="0" x="0" height="100%" width="100%" id="canvasGrid">
   <rect fill="url(#gridpattern)" stroke-width="0" y="0" x="0" height="100%" width="100%"/>
  </g>
 </g>
 <g>
  <title>Layer 1</title>
  
  <ellipse id="circle1" stroke="#000" ry="119.5" rx="123.5" id="svg_6" cy="193.5" cx="298" fill-opacity="null" stroke-opacity="null" stroke-width="3" fill="#fff"/>
  <ellipse id="circle1" stroke="#000" ry="87" rx="93.00001" id="svg_9" cy="197" cx="300.5" fill-opacity="null" stroke-opacity="null" stroke-width="3" fill="none"/>
  <ellipse id="circle2" stroke="#000" ry="63" rx="64.5" id="svg_11" cy="197" cx="302" fill-opacity="null" stroke-opacity="null" stroke-width="3" fill="none"/>
  <ellipse id="circle2" stroke="#000" ry="38" rx="37" id="svg_13" cy="198" cx="302.5" fill-opacity="null" stroke-opacity="null" stroke-width="3" fill="none"/>
  
 </g>
</svg>

<!-- CSS -->

#circle1 {
  animation-name: cirlce1;
  animation-duration: 3s;
  animation-timing-function: ease-in-out;
  animation-iteration-count: infinite;
}
#circle2 {
  animation-name: cirlce2;
  animation-duration: 3s;
  animation-timing-function: ease-in-out;
  animation-iteration-count: infinite;
}
@keyframes cirlce1 {
  from {
    cy: 0%;
    fill: none;
    stroke: grey;
  }
  to {
    cy: 50%;
    fill: #9284D9;
    stroke: white;
  }
}
@keyframes cirlce2 {
  from {
    cx: 100%;
    fill: none;
    stroke: grey;
  }
  to {
    cx: 52%;
    fill: #9284D9;
    stroke: white;
  }
}
```

### **Анімаційний тег `<animate>`**

**Увага!** Декларативна анімація в форматі SMIL за допомогою тегів `<animate>` не рекомендується до використання і, можливо, буде видалена з браузерів у майбутньому.

`<animate>` - це тег для створення анімації, вбудований в сам SVG. Він визначає, як атрибути елементів змінюються від вихідних до кінцевих значень в процесі вказаної анімації. Це використовується для анімації властивостей, які не можуть бути анімовані за допомогою CSS.

Основні елементи, які анімуюься цим тегом: колір, рух і трансформація. Цей тег вкладається всередину об'єкта, який має бути анімований.

Приклад такої анімації:

```text
<-- HTML -->
<div class="outer">
  <div class="inner">
  <svg height="500" width="500">
    <polygon points="50,5 20,99 95,39 5,39 80,99"  style="fill:#00BD9D;stroke:#00BD9D;stroke-width:1;fill-rule:nonzero;">
  <animateTransform attributeName="transform" attributeType="XML"
                        type="scale"
                        from="1" to="3"
                        begin="0s" dur="10s"
                    repeatCount="indefinite"
                        additive="sum"/>
      <animateTransform attributeName="transform" attributeType="XML"
                        type="rotate"
                        from="0 130 120"
                        to="360 130 120"
                        begin="0s" dur="10s"

                        repeatCount="indefinite"
                        additive="sum"/>
  </polygon>
  </svg>
</div>
</div>

<-- CSS -->
#star {
  position: relative;
  right: 200;
}
.outer {
  display: flex;
  align-items: center;
  justify-content: center;
}
.inner {
  max-width: 100%;
}
```

## VI. Узагальнення та систематизація знань

## VII. Домашнє завдання

