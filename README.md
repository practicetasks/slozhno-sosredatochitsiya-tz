# Проектная задача

В этом проекте перед вами амбициозная задача: сверстать адаптивный сайт в светлой и тёмной темах. Вы не будете начинать
с чистого листа. В заготовке проекта уже есть нужная структура со всеми файлами, шрифтами, картинками и скриптом
переключения темы.

Вам нужно написать разметку, перенести контент из макета и всё это стилизовать при помощи CSS.

[Шаблон](https://github.com/practicetasks/slozhno-sosredatochitsiya-template)

## Шаг 1. Определение подхода и изучение стартового кода

Внимательно
изучите [макет](https://www.figma.com/design/QieNXCaxpKp07zN55ufi7J/%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%BD%D0%B0%D1%8F-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-(no-focus)?node-id=1-96&t=7YWVlqv3R4iwywEE-0).

В начале работы над проектом вам нужно принять решение, какие подходы применять при вёрстке:

1. **Mobile first** или **Desktop first**. В этой работе вы будете использовать Mobile first.
2. **Чёрное** или **белое**. Решите, какую тему верстать как основную. Это не повлияет на то, какая тема будет включена
   у пользователя при входе на сайт. Наша рекомендация — начинать с тёмной темы. Можете ориентироваться на тему в вашей
   операционной системе.

Изучите стартовый код. Стили нужно писать в разных файлах, поэтому посмотрите на имена файлов и почитайте комментарии
внутри. Так будет понятно, где какие стили писать.

В HTML уже есть блок с кнопками, которые переключают тему принудительно, вне зависимости от того, какая тема выбрана на
компьютере пользователя. Оставьте разметку этого блока как есть, не меняйте классы. Иначе JavaScript-код сломается, и
темы не будут переключаться.

В файле `globals.css` сброшены стандартные отступы элементов и задано несколько важных свойств. Вы можете дополнять или
менять эти стили по необходимости.

## Общие рекомендации перед стартом

* Стили для основной темы и основной ширины экрана пишите в файле `style.css`. Ниже в этом же файле вы напишете
  медиавыражения для адаптива под разные экраны.
* При вёрстке старайтесь использовать логические свойства там, где это возможно. Например, `margin-block-start` вместо
  `margin-top` или `border-inline-end` вместо `border-right`.
* Практически во всей работе для расстановки элементов подойдут гриды. С их помощью можно адаптировать сайт под разные
  экраны, практически не меняя стили. Советуем использовать их максимально.
* Обязательно убедитесь, что сайт совпадает с макетом на основных разрешениях, а в промежуточных состояниях не ломается
  и блоки выглядят хорошо. Вспомните про «резиновую» вёрстку.
* Отдельно обратите внимание на горизонтальный скролл. Он не должен появляться ни на каких разрешениях и ни при каких
  условиях.
* Держите инструменты разработчика открытыми. В них удобно переключать автоматические темы.

![img1.png](img1.png)

## Шаг 2. Подключение файлов и мета страницы

Подключите все нужные файлы стилей в HTML-разметке. Внимательно выбирайте порядок подключения.

Помните про каскадную сущность CSS: чем ниже в коде, тем приоритетнее. Поэтому важно, чтобы более общие стили были
подключены раньше менее общих.

Например, при подключении файлов для цветовых тем советуем такой порядок:

```html

<link rel="stylesheet" href="./styles/variables.css">
<link rel="stylesheet" href="./styles/style.css">
<link rel="stylesheet" href="./styles/dark.css">
<link rel="stylesheet" href="./styles/light.css">
```

Для остальных файлов стилей выберите порядок самостоятельно.

Чтобы браузер понял, что у нашего сайта есть тёмная и светлая темы внутри `<head>`, важно прописать строку с метатегом
для `color-scheme`. На первом месте укажите ту тему, которую верстаете как основную. Если это тёмная тема, то запись
будет такой:

После этих действий браузер научится отображать страницу в той теме, которая выбрана в операционной системе. Например,
на скринкасте видно, что страница не белая, как обычно, а с тёмным фоном.

VIDEO

## Шаг 3. Создание статичной версии

Поработайте над шапкой, основным контентом, галереей и футером.

### Работа над шапкой

Для расположения элементов в шапке сайта отлично подходят гриды и свойства индивидуального выравнивания грид-элементов.

Если присмотреться к макетам в разных темах, то можно заметить, что в тёмной теме в правом верхнем углу есть небольшая
надпись REC. В светлой теме этого декоративного элемента нет. Пожалуй, это единственный пустой тег в разметке и
единственный элемент, к которому уместно применить абсолютное позиционирование.

Точку справа от надписи реализуйте через псевдоэлемент — одного пустого тега в HTML достаточно.

Не забудьте о скринридерах. Поскольку это декоративный элемент, его нужно скрыть при помощи aria-атрибута от читалок.

В правом верхнем и нижнем левом углах есть декоративные уголки. Их можно реализовать при помощи псевдоэлементов и
указания границ для двух сторон.

Чтобы заголовок в шапке красиво адаптировался и при этом хорошо выглядел на больших и маленьких экранах, используйте
`clamp()`. Ниже вы найдёте формулы расчёта размера текста. Подумайте, почему используются именно такие значения и для
какого разрешения применить формулу:

```
/* Для мобильных */
clamp(7.25rem, 7.0115rem + 1.0178vw, 7.5rem)

/* Для планшета и десктопа */
clamp(7.5rem, 0.5625rem + 14.4531vw, 9.8125rem)
```

Формулы сгенерированы с помощью
сайта [Font-size Clamp Generator](https://clamp.font-size.app/?config=eyJyb290IjoiMTYiLCJtaW5XaWR0aCI6IjMyMHB4IiwibWF4V2lkdGgiOiIxNDU2cHgiLCJtaW5Gb250U2l6ZSI6IjE0cHgiLCJtYXhGb250U2l6ZSI6IjIwcHgifQ%3D%3D).
Он пригодится вам, чтобы адаптировать текст на других
разрешениях.

У текста в заголовке задана тень. Вот стили для неё: `text-shadow: 4px 4px 0 var(--accent-color);`.

Параграфу в шапке задан фоновый цвет. Такой же декоративный приём встречается в основном блоке сайта. Используйте
отдельный класс `title-decor`, чтобы удобно задавать фон и цвет текста всем схожим элементам.

### Работа над основным контентом

Перед тем как верстать основной контент страницы:

1. Задайте для `.page` фоновое изображение. Путь до фоновой картинки так же можно вынести в переменную, которая будет
   переопределяться в зависимости от выбранной темы — светлой или тёмной.
2. Расположите фоновое изображение по центру. Пусть оно закрывает собой всего родителя.
3. После этого пропишите `background-attachment: fixed;`, чтобы фон оставался на месте при прокрутке страницы.

В основном контенте встречается обычный текст и заголовки разных уровней:

1. Разбейте весь текст на секции, определите, какого уровня нужны заголовки.
2. Просмотрите макеты для всех разрешений и примерно прикиньте, какие обёртки вам понадобятся для удобного адаптива этих
   блоков.
3. Переиспользуйте класс `title-decor` там, где текст находится на цветном фоне.
4. Старайтесь задавать похожим элементам одинаковые классы, чтобы писать стили только один раз. Повторений и так
   хватает.

В тексте встречаются ссылки. Им тоже задана тень. Возьмите значения для свойства text-shadow из макета и реализуйте этот
стиль по аналогии с заголовком в шапке. Не забудьте про состояния ховера и фокуса для ссылок.

Расставьте цвета, согласно выбранной схеме. Для этого используйте CSS-переменные.

### Работа над переменными

Большинство цветов, шрифт, размеры текста и отступы удобно хранить в переменных, потому что они часто используются в
разных местах кода. А ещё так можно быстро менять темы простым переопределением переменных.

Все переменные должны храниться только в файле `variables.css`.

Задавая значения для переменных цветов, пишите только нужные для той темы, которую вы выбрали основной. Цвета для второй
темы вы добавите позже.

Выбирайте для переменных имена, которые будут иметь смысл в обеих темах. Старайтесь без особой надобности не плодить
сущности. Не нужно создавать для одного цвета две переменные — для светлой и тёмной темы. Создайте одну переменную, а
потом, если нужно, поменяйте её значение.

Не надо так:

```css
:root {
    --accent-color-dark-theme: #ff0070;
    --accent-color-light-theme: #ff8dcb;
}
```

Лучше так:

```css
/* Файл variables.css */
:root {
    --accent-color: #ff0070;
}

/* Файл light.css */
:root {
    --accent-color: #ff8dcb;
}
```

### Работа над галереей

В галерее всем картинкам должен быть задан атрибут `alt` с описанием изображения. Поскольку галерея находится сильно
ниже первого экрана, который увидит пользователь, вы можете сократить время загрузки страницы и задать для `<img>`
атрибут `loading` со значением `lazy`, отвечающим за «ленивую» загрузку.

Сложная разметка здесь не понадобится — дополнительные обертки изображениям не нужны, адаптировать галерею под разные
устройства удобно при помощи свойств гридов.

### Работа над футером

1. Используйте гриды и установите отступы.
2. Расставьте цвета, согласно выбранной схеме. Для этого примените CSS-переменные.

Футер во многом повторяет шапку сайта. Тот же размер, те же декоративные элементы и стили заголовка. Но есть маленький
подвох: стили заголовка отличаются от стилей в шапке, пусть и совсем немного. Будьте внимательны.

Помните, что хотя заголовки и выглядят одинаково, они не могут быть одного уровня. На странице должен быть только один
заголовок `<h1>`, и его место в шапке, а не в подвале.

Декоративные уголки можно переиспользовать из шапки. Для этого пропишите стили отдельному, независимому от положения в
документе классу.

## Шаг 4. Добавление адаптивности

### Реализуем адаптивность

1. Создайте медиазапрос для расширения больше 768 пикселей. Он будет определять стили для экранов с шириной больше 768
   пикселей.
2. Создайте медиазапрос для расширения больше 1024 пикселей. Он будет определять стили для экранов с шириной больше 1024
   пикселей.
3. Скорректируйте правила для нужных элементов согласно макету.

### Добавляем вторую цветовую схему

4. В файле второй цветовой схемы установите CSS-переменные и цвета.
5. Скорректируйте отображение элементов, которые меняются в этой теме:
    - фоновую картинку страницы;
    - изображение блока «Запись»;
    - стиль кнопки в шапке.

## Шаг 5. Работа над кнопками переключения тем

Разметка этого блока уже готова. При нажатии кнопок запускается JavaScript-код, который принудительно меняет темы сайта.
Как это работает?

### Кнопка «День»

При нажатии на кнопку для корневого тега `<html>` добавляется класс `theme-light`. При этом должна отобразиться светлая
тема.

### Кнопка «Неон»

При нажатии на кнопку для корневого тега `<html>` добавляется класс `theme-dark`. При этом должна отобразиться тёмная
тема.

### Кнопка «Авто»

При нажатии на кнопку для корневого тега `<html>` добавляется класс `theme-auto`. При этом должна отобразиться та тема,
которая выбрана у пользователя в системе. Сработает медиафича `prefers-color-scheme`.

Для нажатой кнопки устанавливается класс `.header__theme-menu-button_active`. Кнопка должна стать недоступна для клика.
Поможет свойство `pointer-events: none`.

Нужно стилизовать состояния кнопок по ховеру и по фокусу. Для стилизации фокуса используйте `:focus-visible`. Стили всех
состояний можно найти в макете.

Из-за того, что темы на сайте будут переключаться не только в зависимости от настроек пользователя, но и принудительно,
по классу, при написании стилей придётся дублировать стили тем. Один раз для класса, а второй раз для медиафичи
`prefers-color-scheme`.

Предположим, вы выбрали основной тёмную тему. Опишем структуру кода внутри файлов стилей.

Файл `variables.css`:

```css
:root {
    /* Переменные тёмной темы */
}
```

Файл `dark.css`:

```css
:root.theme-dark {
    /* Дублируем переменные для тёмной темы */
}

/* Остальные стили, только при необходимости */
```

Файл `light.css`:

```css
:root.theme-light {
    /* Переменные светлой темы */
}

/* Остальные стили, только при необходимости */

@media (prefers-color-scheme: light) {
    :root {
        /* Дублируем переменные светлой темы */
    }
}

/* Остальные стили, только при необходимости */
```

Для тёмной темы не нужно использовать правило `@media (prefers-color-scheme: dark) {}`, поскольку она выставлена по
умолчанию, и её переменные уже заданы в `variables.css`. Они будут применены автоматически.

### Помните о рефакторинге

Запланируйте время на рефакторинг. После того, как закончите, отложите код хотя бы на один день. Затем вернитесь и
посмотрите, можно ли где-то сделать проще и изящнее. Может быть, вы увидите, что использовали лишние обёртки или слишком
длинные записи для стилей.

Такой подход поможет выработать критический взгляд на свою работу — и сделать её лучше.