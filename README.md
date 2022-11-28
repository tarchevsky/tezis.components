# UI-pack

![License](https://img.shields.io/badge/licence-GPL--3.0-yellowgreen)

## <a name="target">Назначение репозитория / библиотеки</a>

### Если просто

Нужна сетка, кнопки, выпадающие меню, табы, аккордеон, слайдеры, модальное окно, но не нужен громоздкий Bootstrap?

Инклюд компонента в любом файле pug, подключение стилей этого компонента, замена кода цвета в переменных sass - и ваш блок готов.

### Если подробнее

#### Переиспользование, универсальность

В работе верстальщика рано или поздно встаёт вопрос реюза стилей / сеток / JS - решений.

Выпадающие списки, табы, меню, слайдеры - стандартные элементы, которые можно написать сотнями разных способов, учитывая или не учитывая множество переменных, таких как доступность и реюзабельность, лаконичность кода. Вместе с normalize.css и отменой браузерных стилей, мы часто переписываем одно и то же с нуля, либо используем решения других разработчиков, берём из codepen и других хороших ресурсов. Но вопрос более локальной стандартизации наверняка волнует большое количество разработчиков.

Кастомные решения особенно важны в небольших проектах или наоборот, проектах с длинным циклом разработки, когда избыточность библиотек, типа bootstrap, нам не нужна.

В данной библиотеке будет просто как использовать то, что есть, чтобы создать что-то быстро и без дополнительных гуглений, либо переписать все неудобные стили / переменные / функции и избавиться от лишнего, не нагромождая свой код.

### Доступность

Библиотека UI-pack про семантическую верстку и за доступность. И если на первых этапах это может быть неочевидным, то когда основные компоненты будут дописаны и усовершенствованы, вы сможете писать проект почти не задумываясь о доступности и концентрируясь на более сложных и важных задачах.

> Например, на данный момент вместо старых свойства отступов и позиционирования используются логические свойства, которые часто можно увидеть в браузере до сброса стилей. Например, вместо ```margin-top: $ind``` можно увидеть ```margin-block-start: $ind```. А вместо ```right: 50%``` - ```inset-inline-end```. На первый взгляд это сложнее, но эти логические свойства перекликаются c flex и grid layout, отчего учатся очень быстро. Также стоит использовать в text-align вместо старых свойств start и end. Не все логические свойства учитываются в силу того, что пока они не везде работают и не всегда делают смысл. Например, max-inline-(start, end) не работает с медиазапросами. А свойства из разряда border-inline-start-block-end-radius больно нелепо выглядят в верстке, хоть и нечасто встречются. Поэтому в стандартных стилях используется классический border-(top, bottom, left, right).

Если хотите более детально почитать о логических свойствах, вот неплохая [статья](https://medium.com/web-standards/logical-css-props-c5046c563640).

Из-за того, что большинство уроков, гайдов и документации в интернете на поверхности не затрагивают тему доступности, проекты получаются более поверхностными и как следствие, менее долгоиграющими.

Нам всем важно, чтобы когда мы сдавали сайт на wordpress, любой новый параграф, вставленный клиентом и не предусмотренный кастомными полями и без специализированных классов, – выглядел хорошо, не нуждался в паддингах и вашей поддержке :smiley:, и эта библиотека решает эту задачу.

[Демо](#demo)

[Базовые стили и разметка](#styles)
- [Переменные SCSS](#scss-variables)
- [Сетка:](#grid)
  * [container (для проектов с фиксированной шириной контейнера)](#container)
  * [layout (для сайтов с элементами, выходящими за границы контентной части)](#layout)
  * [content (контейнер контента после header и до footer)](#content)
  * [sidebar](#sidebar)
  * [col](#col)
  * [row](#row)

[SVG-спрайты](#svg-sprites)

[Компоненты](#components)
- [Подключение компонентов](#import-component)
- [Вендорские стили и скрипты:](#scripts-vendor)
- [Список компонентов](#components-list)
  - [Картинки](#img)
  - [Кнопки](#button)
  - [Формы](#form)
  - [Таблицы](#table)
  - [Бургер](#burger)
  - [Модальное окно](#modal)
  - [Бесконечная прокрутка контента](#infinite-scroll)
  - [Флекс-галерея](#flex-gallery)
  - [Раскрывающееся меню - список](#dropdown)
  - [Мультиязыковое меню + мини-плагин локализации для небольших сайтов](#dropdown-lang)
  - [Слайдер Swiper c базовыми стилями и настройками](#slider)
  - [Слайдер Swiper с контентом, заходящим за край страницы и со скроллбаром](#slide-beyond)
  - [Вертикальный слайдер (vertical-slider)](#vertical-slider) - самописный вертикальный простой слайдер без использования библиотеки swiper
  - [Табы](#tabs)
  - [Табы в виде тегов](#tabs-tags)
  - [Хлебные крошки](#breadcrumbs)
  - [Квиз](#quiz)
  - [Текст с анимированным движением по кругу](#circle)
  - [Контейнер, выходящий за границы основной ширины макета](#container-beyond)
  - [Аккордеон](#accordion)
  - [Галерея](#gallery)

[Рекомендации и напоминания о возможных способах реализации блоков с помощью семантических тегов](#semantics)

[README gulp-pug-starter с основами работы сборщика](#gulp-pug-starter)
- [Особенности](#features)
- [Установка](#installation)
- [Файловая структура](#structure)
- [Команды](#commands)
- [Рекомендации по использованию](#recommendations)
- [Компоненты](#components)
- [Страницы проекта](#pages)
- [Шрифты](#fonts)
- [Изображения](#images)
- [SVG-спрайты](#sprites)
- [Сторонние библиотеки](#vendors)
- [Нужен SCSS без Pug?](#withoutpug)
- [Нравится проект gulp-pug-starter?](#donate)
- [Контакты создателя gulp-pug-starter](#contacts)

## <a name="demo">Демо</a>

Прежде чем вникать в преимущества библиотеки, читать весь этот документ, сделайте несколько несложных действий.

Скачайте [архив](https://github.com/tarchevsky/ui-pack/archive/refs/heads/master.zip).

Установите глобально:

* Yarn: ```npm i -g yarn```
* Gulp: ```npm i -g gulp```
* Bem Tools: ```npm i -g bem-tools-core```

Откройте папку, где распаковали файлы архива в редакаторе кода, на котором работаете и введите:

```yarn set version berry```, затем ```yarn``` для установки всех зависимостей.

После этого процесса запустите локальный сервер с помощью команды ```yarn run dev``` и пустой сайт откроется в Вашем браузере по умолчанию.

Сейчас на сайте лишь шапка и подвал.

Для того, чтобы увидеть демо-контент, зайдите в файловую систему библиотеку, а именно папку ```src``` - именно с ней вы будете работать, но чуть позже.

Сейчас просто перейдите по написанному путю: ```./src/views/index.pug``` и откройте файл index.pug.

Найдите строчку ```include ../blocks/modules/main/main``` и ниже вставьте ```
include ../blocks/modules/demo/demo```.

Также раскомментируйте все строки в файлах:

```./src/blocks/components/components.scss```,
```./src/js/import/components.js```

# <a name="styles">Базовые стили и разметка</a>
### <a name="scss-variables">Переменные SCSS</a>

Все цвета и отступы определяются с помощью переменных в ```./src/styles/helpers/_variables.scss```.

Все значения в верстке заданы переменными, так что настройка проекта начинается с них.

1. ```$container``` - переменная для ширины контейнера контентной части сайта.
2. ```$layout-margin``` - переменная дли отступов контейнера layout контентной части сайта.
3. ```$layout-margin-mob``` - переменная дли отступов мобильной версии контейнера layout контентной части сайта.
4. ``$base-color`` - цвет, используемый в шрифтах и бордерах, а также псевдоэлементов (если в макете цвет шрифта и псевдоэлементов совпадает)
5. ``$accent-color`` - цвет кнопок и ссылок (подчеркивания) и псевдоэлементов, если цвет псевдоэлементов не совпадает с base-color. Также может быть фоновым цветом, если фоновый цвет не отличается от него.
6. ``$hover-color`` - цвет состояния, цвет при наведении
7. ``$active-color`` - цвет состояния, цвет в активном состоянии
8. ``$disabled`` - цвет состояния, цвет элемента в отключенном состоянии, иногда цвет пассивного бордера, можно использовать в бордерах, неакцентное состояние
9. ``$bg-color`` - фоновый цвет
10. ``$contrast-color`` - цвет контраста. Чаще всего белый цвет. Пример использования: белый цвет шрифта при наведении на кнопку, когда для читабельности темный цвет шрифта сменяется на светлый.
11. ``$border`` - настройка бордера, в качестве цвета используется переменная disabled
12. ``$brr`` - основной border-radius. brrmin и brrmax - минимальное (меньшее) и максимальное (большее) значение
13. ``$ind`` - сокр. от indentation, отступ. Универсальное и наиболее часто встречающееся значение отступа. Введено вместо большого количества переменных и миксинов по margin и padding. Коротко и удобно. Также, как и border-radius, присутствуют минимальное и максимальное значение ``$indmin`` ``$indmax``.
14. ```$gap``` а также ```$gapmin``` и ```$gapmax``` - по сути аналогичны ```$ind```. Но нужны там, где в проекте отступы gap отличаются от отступов между элементами и блоками. В данном случае закомментированы.
15. ```$transition``` - стандартные длительность и тип анимации.

#### Дополнительные переменные цвета

Также есть цветовые переменные для тех случаев, когда на сайте необходимы блоки с цветным содержимым, не заимствующим стандартные цвета.

По умолчанию цвета стоят пастельных тонов, замените, если нужны будут другие. Цвета будут дополняться.

```scss
// Colors

$aquamarine: #66CCC7;
$lightblue: #98BBDD;
$lightpurple: #E2A7C2;
$darkblue: #211F5C;
$green: #6C7E2A;
$lightgreen: #E6E4B3;
$black: #1F150A;
$orange: #FFB02E;
$lightorange: #FFB841;
$lightyellow: #F5FF66;
$lightbrown: #9F8170;
$darkgrey: #4C514A;
```

Стилей с этими цветами нигде нет, но такие решения часто используются для фоновых цветов, в таких случаях копируйте код отсюда:

```scss
.aquamarine {
  background-color: $aquamarine;
}

.lightblue {
  background-color: $lightblue;
}

.lightpurple {
  background-color: $lightpurple;
}
.darkblue {
  background-color: $darkblue;
}
.green {
  background-color: $green;
}
.lightgreen {
  background-color: $lightgreen;
}
.black {
  background-color: $black;
}
.orange {
  background-color: $orange;
}
.lightyellow {
  background-color: $lightyellow;
}
.lightbrown {
  background-color: $lightbrown;
}
.darkgrey {
  background-color: $darkgrey;
}
```
# <a name="grid">Сетка (container, layout, content, sidebar, col, row)</a>

Сетка библиотеки построена на нескольких базовых принципах: скорость, легкость, доступность, унификация самых распространенных элементов на сайтах, адаптивность из коробки. На последнем остановимся.

Контейнерам container, layout, content и row - прописаны grid-правила, позволяющие начинать работу без базовой настройки сетки.

> CSS - правила сетки описаны в файле ```./src/styles/base/_general.scss```, адаптация там же.

### <a name="container">container (для проектов с фиксированной шириной контейнера)</a>

! В сборке стоит по умолчанию в файле default.pug

Подключается в default.pug, над block header

#### Ширина контентной части

Нужен в случаях, когда необходим контейнер фиксированной ширины. Пример:
ширина контентной части макета - ```max-width: 1300px```.

> Ширину контейнера container определяет переменная ``$container`` в ``./src/styles/helpers/_variables.scss``

#### Высота контентной части

Контейнер разделяет страницу на три части: шапку, контент и подвал. С помощью ```grid-template-rows: 80px minmax(75vh, 1fr) 80px;```. В базовой верстке контейнера высота всех трех частей фиксированная. Это нужно для большей привлекательности и удобства верстки.

Но на боевой верстке самое удобное - поставить высоту шапки и подвала с помощью директивы auto. Таким образом контент будет принимать высоту содержимого.

#### адаптация container

В container прописано базовое свойство ```grid-template-columns: minmax(250px, $container);```

При ширине экрана / окна меньше $container (по умолчанию 1300px), вступает в силу медиа-запрос на 1300px, добавляющий фиксированные ```padding: 0 $ind```. Значение переменной $ind берется из _variables.scss

Таким образом реализуется адаптивность контейнера и контентной части сайта.

### <a name="layout">layout (для сайтов с элементами, выходящими за границы контентной части)</a>

Тоже контейнер контентной части, но задаёт его не фиксированной шириной, а с помощью высчитывания ширины полей.

Подключается в default.pug, над block header

#### Ширина контентной части

> Смысл этого контейнера в использовании в сочетании с классом layout-none. Если у вас в проекте присутствуют блоки, растягивающиеся на полную ширину окна, вроде фонов или слайдеров, layout поможет вам работать, не разбивая сайт на большое количество контейнеров. У вас будет один адаптируемый layout. А если нужно будет получить блок на всю ширину экрана, используйте какой-нибудь семантический тег в связке с layout-none, например: ```article.layout-none```. **Но очень важно, чтобы родительским элементом был именно layout**.

Про расчет ширины контентной части. Формула такая:

Берем ширину контентной части из макета. Например, 1300px. 
- Вычисляем, сколько процентов эта ширина занимает от общей ширины, например от 1440px. 
- Полученный процент отнимаем от 100%. Результат - это сумма двух полей по бокам от макета. 
- Делим на два и вставляем получившееся значение в свойство ```margin-inline``` класс layout в _general.scss.

Более краткая формула

> ширина контента / ширина сайта * 100% = результат - 100% (получается совокупная ширина полей)  
ширина полей / 2 = margin-inline

Ширину отступов определяет переменная $layout-margin в _variables.scss. В качестве единицы измерения используем vw вместо %, чтобы ширина высчитывалась не из ширины контента, а из ширины окна.

Да, вы можете использовать абсолютные значения. Но vw гораздо удобнее.

#### Высота контентной части

Контейнер, как разделяет страницу на три части: шапку, контент и подвал. С помощью ```grid-template-rows: 80px minmax(75vh, 1fr) 80px;```. В базовой верстке контейнера высота всех трех частей фиксированная. Это нужно для большей привлекательности и удобства верстки.

Но на боевой верстке самое удобное - поставить высоту шапки и подвала с помощью директивы auto. Таким образом контент будет принимать высоту содержимого.

#### адаптация layout

Для адаптации ширины layout стоит использовать прописанное медиа-выражение, начинающееся с 1300px. По умолчанию в layout написан ```margin-inline: $layout-margin-mob```. Это переменная из _variables.scss со значением по умолчанию 2vw.

### <a name="content">content (контейнер контента после header и до footer)</a>

Вспомогательный класс, содержащий ```grid-template-columns: minmax(200px, 2fr)``` и базовый gap. Нужен для того, чтобы обозначить контентную часть. Идёт после header.

> Для напоминания структура общей колонки сайта grid-template-columns - .header / .content / .footer.

Он служит оберткой для всех семантических блоков контентной части сайта.

### <a name="sidebar">sidebar</a>

Сперва подключим стили блока sidebar в ```_modules.scss```: ```@import 'sidebar/sidebar';```.

Контейнер сайдбара активируется в default.pug, над block content. Для того, чтобы сайдбар заработал, добавьте  ```content``` родительский класс ```content-sidebar```.

Выглядеть это будет так:
```
block header
.content-sidebar
    .content
        block content
```

Затем надо добавить сам сайдбар в сетку, для этого добавьте выше или ниже ```content``` импорт БЭМ-блока ```include ../../blocks/modules/sidebar/sidebar```. 

```
block header
.content-sidebar
    include ../../blocks/modules/sidebar/sidebar
    .content
        block content
```

Нужен липкий контент в сайдбаре или просто контейнер для добавления контента? - предусмотрен
класс ```sidebar__inner```.

#### Сайдбар без отступа слева

Во многих проектах, вроде SPA-сайтов, сайдбар реализован без отступа слева, чтобы придать вид более цельного интерфейса. Для таких случаев реализована совместимость с layout-none.

Естественно, чтобы способ работал, надо, чтобы в default.pug основным контейнером был ```layout```. А block content был обёрнут в тег с классом layout-none.

Активируется, если вы поместите элемент с классом content-sidebar внутрь layout-none. А стандартный вспомогательный класс content внутрь content-sidebar.

Теперь экран делится на две части. Сайдбар и контентную часть, которые тоже надо прописать. Вот так:

```
.layout-none
        .content-sidebar
            .sidebar
                .sidebar__inner
                    Some content in sidebar, maybe nav menu
            .content
                h1 Some content
```

#### адаптация sidebar

На данный момент есть базовая адаптация с отступами.

Но элемент sidebar имеет css-свойство height: 100%. А это значит, что растягивается он по максимальной ширине контента.

А поскольку в разных макетах сайдбары адаптируют по-разному, в первом коммите с сайдбаром никакой более продуманной адаптации пока не выполнено.

### <a name="col">col</a>

#### адаптация col

### <a name="row">row</a>

Если нужно сделать колонки с автоматической адаптацией - вставьте класс ```.row```. Этот класс адаптирует до минимального размера экрана 320px.

Кстати, про количество колонок. Если колонки больше 320, они автоматически подстроятся под ширину экрана и ширину контента в колонках.

> ***Руководство по стилю исполнения***. Если намереваетесь использовать в одном из блоков row, добавляйте к названию блока ```__row``` по БЭМ.

## <a name="svgsprites">SVG-спрайты</a>

Для легкости работы с svg-спрайтами в ```./src/views/helpers/mixins.pug``` существует миксин
```mixin sprite```.

Использование в коде выглядит так:

```
  +sprite("class", "img/sprites/sprite.svg#svgname", width="value", height="value")
```

# <a name="components">Компоненты</a>

## <a name="import-component">Подключение компонентов</a>

Для того, чтобы на сайте заработал тот или иной компонент, нужно:

1. Подключить его стили через ``./src/blocks/components/_components.scss``
2. Подключить скрипты, если блок их предусматривает через ``./src/js/import/components.js``

> Компонент можно использовать, как подключив через include в pug, так и скопировав pug необходимые теги c css-классами. Иной раз важна иерархия классов, будьте внимательны при написании с нуля.

**Дополнительное описание работы каждого компонента находится в папке компонента с одноименным .md файлом.**

## <a name="scripts-vendor">Вендорские стили и скрипты</a>

В библиотеке есть два вендорских скрипта со стилями, реализованные через импорт:

1. Swiper Slider (component slider)
2. Fancybox (component gallery)
3. Gsap

Чтобы подключить скачанные вендорские скрипты, нужно вставить ```script(src="js/vendor.js")```

в index.pug, в раздел ```block scripts```.

#### Где находятся эти импорты и как подключать самостоятельно новые библиотеки

#### Установка

```yarn add <library>```

#### Подключение

* Импортировать библиотеку в js файле компонента ```./src/blocks/components/component/component.js``` строчками вида
  ```import { name } from "path";``` или
  ```import name { plugins } from "path";```
* Сохранить файл стилей подключаемой библиотеки в ```./src/styles/vendor/import/...``` с названием вида
  ```_swiper.scss```
* Подключить файл стилей библиотеки в ```./src/styles/vendor/_libs.scss```

## Список компонентов

### <a name="img">Картинки (img)</a>

##### Верстка

Подключение в index.pug: ```include ../blocks/components/img/img```

Хоть pug-файл компонента существует, использовать его рекомендуется без импорта в pug, а используя "живую" верстку.

Эталонный вариант использования:

```pug
.img
  img(src="img/img.jpg" alt="Какая-то картинка")
```

или

```pug
.img
    img(data-src="img/img.webp" data-alt="Название картинки")
```

этот отрезок кода стоит по умолчанию для работы Intersection observer API - lazy loading. А об этом дальше

> Если хотите, чтобы картинка была без отступов сверху и снизу, добавьте контейнеру класс ```.img__empty```

Также по умолчанию компонент поддерживает ленивую загрузку через Intersection observer API.

#### Как работать с ленивой загрузкой Intersection observer API.

Проследите, что в components.js подключен js-файл компонента img:

```js
import "%components%/img/img";
```

Если хотите ленивую загрузку, не используйте src, а вставляйте адрес картинки в атрибут ```data-src="./img/img.jpg"```.

Также не вставляйте атрибут alt, а вместо него атрибут ```data-alt="Название картинки"```.

Все эти атрибуты Intersection observer вытащит значения data-src и data-alt, и заменит их и создаст src и alt с этими значениями.

data-alt создан для того, чтобы при загрузке страницы не возникал значок недостающего изображения на месте изображения, которое пока не подгрузилось.

##### CSS

Подключение в ```_components.scss```: раскомментировать ```@import 'img/img';```

### <a name="button">Кнопки (button)</a>

##### Верстка

Кнопка сама по себе - элемент формы. Поэтому если хотите сделать из кнопки ссылку, оберните ```button``` в тег ```form``` с атрибутом ```action="ссылка"```

##### CSS

По умолчанию у кнопки есть ```margin-block``` с отступами ```$ind``` (_variables.scss). Но если кнопка находится в ```form```, отступы аннулируются, так как у тега ```form``` по умолчанию есть свои ```margin-block: $ind```.

### <a name="form">Формы (form)</a>

### <a name="table">Таблицы (table)</a>

### <a name="burger">Бургер (burger)</a>

> Важно! В js-файле компонента есть уже включенный пункт меню с dropdown - компонентом. Для избежания ошибок в консоли все функции, связанные с компонентом закомментированы.

### <a name="modal">Модальное окно (modal)</a>

##### Верстка

Для подключения добавьте в default.pug ниже ```block footer``` - ```block modal```. Затем в код страницы, например *index.pug*:

```jade
block footer
    include ../blocks/modules/footer/footer
      
block modal
    include ../blocks/components/modal/modal

block scripts...
```

Для того, чтобы **добавить кнопку активации** модального окна, поместите атрибут ```data-modal``` к любой ссылке или кнопке на странице

##### CSS

Подключение в ```_components.scss```: добавить строчку ```@import 'modal/modal';```

###### JS

Подключение в ```components.js```: добавить```import "%components%/modal/modal";```.

### <a name="infinite-scroll">Бесконечная прокрутка контента (infinite-scroll)</a>

Для того, чтобы встроить плагин в проект:

1. Подключите файлы стилей и скриптов, как на [примере](#import-component)

Подключение в index.pug: ```include ../blocks/components/infinite-scroll/infinite-scroll```

### <a name="flex-gallery">Флекс-галерея</a>

##### Верстка

Подключение в любом блоке, типа main.pug: ```include ../../components/flex-gallery/flex-gallery```

##### CSS

Подключение в ```_components.scss```: раскомментировать ```@import 'flex-gallery/flex-gallery';```

###### JS

Подключение в ```components.js```: раскомментировать```import "%components%/flex-gallery/flex-gallery";```.

### <a name="dropdown">Раскрывающееся меню - список (dropdown)</a>

### <a name="dropdown-lang">Мультиязычное меню + мини-плагин локализации для небольших сайтов (dropdown-lang)</a>

##### Верстка

Подключение в header.pug: ```include ../../components/dropdown-lang/dropdown-lang```

##### CSS

Подключение в ```_components.scss```: раскомментировать ```@import 'dropdown-lang/dropdown-lang';```

###### JS

Подключение в ```components.js```: раскомментировать```import "%components%/dropdown-lang/dropdown-lang";```.

### <a name="slider">Слайдер Swiper c базовыми стилями и настройками (slider)</a>

> Внимание! Не помещайте слайдер в grid и flex-контейнеры, либо дорабатывайте слайдер под свои задачи

### <a name="slide-beyond">Слайдер Swiper с контентом, заходящим за край страницы и со скроллбаром (slide-beyond)</a>

##### Верстка

Подключение в index.pug: ```include ../blocks/components/slider/slide-beyond```

> Внимание! Не помещайте слайдер в grid и flex-контейнеры, либо дорабатывайте слайдер под свои задачи

##### CSS

Подключение в ```_components.scss```: раскомментировать ```@import 'slider/slider';```

###### JS

Подключение в ```components.js```: раскомментировать```import "%components%/slider/slider";```.

### <a name="vertical-slider">Вертикальный слайдер (vertical-slider)</a> - самописный вертикальный простой слайдер без использования библиотеки swiper

##### Верстка

Подключение в любом блоке, типа main.pug: ```include ../../components/vertical-slider/vertical-slider```

##### CSS

Подключение в ```_components.scss```: раскомментировать ```@import 'vertical-slider/vertical-slider';```

###### JS

Подключение в ```components.js```: раскомментировать```import "%components%/vertical-slider/vertical-slider";```.

### Табы в виде тегов (tabs-tags)

### Хлебные крошки (breadcrumbs)

### Квиз (quiz)

### Текст с анимированным движением по кругу (circle)

### Контейнер, выходящий за границы основной ширины макета (container-beyond)

### Аккордеон (accordion)

### Галерея (gallery)

Lightbox в галерее реализован через fancybox.

##### Верстка

Подключение в index.pug: ```include ../blocks/components/gallery/gallery```

Для того, чтобы активировать работу fancybox, напишите верстку такого вида:
```
a(data-fancybox="gallery" href="img/img.webp")
    img(src="img/img.webp")
```

##### CSS

Подключение в ```_components.scss```: раскомментировать ```@import 'gallery/gallery';```

###### JS

Подключение в ```components.js```: раскомментировать```import "%components%/gallery/gallery";```.

Базовые настройки fancybox будут внутри.

## <a name="semantics">Рекомендации и напоминания о возможных способах реализации блоков с помощью семантических тегов</a>

### Семантические теги и за что они отвечают

dl - список описаний - не забывать использовать, дабы не множить *диватоз*
```
<dl>
  <dt>Питание</dt>
  <dd>от сети</dd>

  <dt>Тип патрона</dt>
  <dd>SDS-Plus</dd>

  <dt>Количество скоростей работы</dt>
  <dd>1</dd>

  <dt>Потребляемая мощность</dt>
  <dd>880 Вт</dd>
  …
</dl>
   ```

Таблицы - пример находится в `components` в `table`. Не забывайте, что таблица может не выглядеть как таблица, а размечать связанные значения
```
<figure>
  <figcaption>Подпись к картинке</figcaption>
  <img src="https://randart.ru/art/classics20s/mountains/" alt="Атрибут для картинки">
  <img src="https://randart.ru/art/classics20s/kartinki/" alt="Атрибут названия">
</figure>
```

``form`` - используется не только для **форм**, но и для фильтров

`button` - не забывать указывать по умолчанию type="button", если кнопка не относится к форме

# <a name="gulp-pug-starter">README изначального репозитория gulp-pug-starter, на основе которого был создана библиотека UI-pack.</a>

![License](https://img.shields.io/github/license/andreyalexeich/gulp-pug-starter)
![GitHub stars](https://img.shields.io/github/stars/andreyalexeich/gulp-pug-starter.svg?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/andreyalexeich/gulp-pug-starter.svg?style=social)`<br><a href="https://qiwi.com/n/ANDREYALEXEICH">``<img src="https://img.shields.io/badge/%D0%97%D0%B0%D0%B4%D0%BE%D0%BD%D0%B0%D1%82%D1%8C%20%D0%BD%D0%B0%20%D0%BF%D0%B8%D0%B2%D0%BE-Qiwi-orange?style=for-the-badge&logo=qiwi"></a>`

## 🔥 <a name="features">Особенности</a>

* именование классов по [БЭМ](https://ru.bem.info/)
* используется БЭМ-структура
* используются препроцессоры [Pug](https://pugjs.org/) и [SCSS](https://sass-lang.com/)
* используется транспайлер [Babel](https://babeljs.io/) для поддержки современного JavaScript (ES6) в браузерах
* используется [Webpack](https://webpack.js.org/) для сборки JavaScript-модулей
* используется жёсткий кодгайд
* используется проверка кода на ошибки перед коммитом

## 🛠 <a name="installation">Установка</a>

* установите [NodeJS](https://nodejs.org/en/)
* установите глобально:
  * [Yarn](https://yarnpkg.com/getting-started): ``npm i -g yarn``
  * [Gulp](https://gulpjs.com/): ``npm i -g gulp``
  * [Bem Tools](https://www.npmjs.com/package/bem-tools-core): ``npm i -g bem-tools-core``
* скачайте сборку с помощью [Git](https://git-scm.com/downloads): ``git clone https://github.com/andreyalexeich/gulp-pug-starter.git``
* перейдите в скачанную папку со сборкой: ``cd gulp-pug-starter``
* введите ``yarn set version berry``
* скачайте необходимые зависимости: ``yarn``
* чтобы начать работу, введите команду: ``yarn run dev`` (режим разработки)
* чтобы собрать проект, введите команду ``yarn run build`` (режим сборки)

Если вы всё сделали правильно, у вас должен открыться браузер с локальным сервером.
Режим сборки предполагает оптимизацию проекта: сжатие изображений, минифицирование CSS и JS-файлов для загрузки на сервер.

## 📂 <a name="structure">Файловая структура</a>

```
gulp-pug-starter
├── dist
├── gulp-tasks
├── src
│   ├── blocks
│   ├── fonts
│   ├── img
│   ├── js
│   ├── styles
│   ├── views
│   └── .htaccess
├── gulpfile.babel.js
├── webpack.config.js
├── package.json
├── .yarnrc.yml
├── .babelrc.js
├── .bemrc.js
├── .eslintrc.json
├── .stylelintrc
├── .stylelintignore
└── .gitignore
```

* Корень папки:
  * ``.babelrc.js`` — настройки Babel
  * ``.bemrc.js`` — настройки БЭМ
  * ``.eslintrc.json`` — настройки ESLint
  * ``.gitignore`` – запрет на отслеживание файлов Git'ом
  * ``.stylelintrc`` — настройки Stylelint
  * ``.stylelintignore`` – запрет на отслеживание файлов Stylelint'ом
  * ``.yarnrc.yml`` – настройка Yarn
  * ``gulpfile.babel.js`` — настройки Gulp
  * ``webpack.config.js`` — настройки Webpack
  * ``package.json`` — список зависимостей
* Папка ``src`` - используется во время разработки:
  * БЭМ-блоки и компоненты: ``src/blocks``
  * шрифты: ``src/fonts``
  * изображения: ``src/img``
  * JS-файлы: ``src/js``
  * страницы сайта: ``src/views/pages``
  * SCSS-файлы: ``src/styles``
  * служебные Pug-файлы: ``src/views``
  * конфигурационный файл веб-сервера Apache с настройками [gzip](https://habr.com/ru/post/221849/) (сжатие без потерь): ``src/.htaccess``
* Папка ``dist`` - папка, из которой запускается локальный сервер для разработки (при запуске ``yarn run dev``)
* Папка ``gulp-tasks`` - папка с Gulp-тасками

## ⌨️ <a name="commands">Команды</a>

* ``yarn run lint:styles`` - проверить SCSS-файлы. Для VSCode необходимо установить [плагин](https://marketplace.visualstudio.com/items?itemName=shinnn.stylelint). Для WebStorm
  или PHPStorm необходимо включить Stylelint в ``Languages & Frameworks - Style Sheets - Stylelint`` (ошибки будут исправлены автоматически при сохранении файла)
* ``yarn run dev`` - запуск сервера для разработки проекта
* ``yarn run build`` - собрать проект с оптимизацией без запуска сервера
* ``yarn run build:views`` - скомпилировать Pug-файлы
* ``yarn run build:styles`` - скомпилировать SCSS-файлы
* ``yarn run build:scripts`` - собрать JS-файлы
* ``yarn run build:images`` - собрать изображения
* ``yarn run build:webp`` - сконвертировать изображения в формат ``.webp``
* ``yarn run build:sprites``- собрать спрайты
* ``yarn run build:fonts`` - собрать шрифты
* ``yarn run build:favicons`` - собрать фавиконки
* ``yarn run build:gzip`` - собрать конфигурацию Apache
* ``yarn run bem-m`` - добавить БЭМ-блок
* ``yarn run bem-c`` - добавить компонент
* ``yarn run lint:styles --fix`` - исправить ошибки в SCSS-файлах согласно настройкам Stylelint
* ``yarn run lint:scripts`` - проверить JS-файлы
* ``yarn run lint:scripts --fix`` - исправить ошибки в JS-файлах согласно настройкам ESLint.

## 💡 <a name="recommendations">Рекомендации по использованию</a>

### Компонентный подход к разработке сайтов

* каждый БЭМ-блок имеет свою папку внутри ``src/blocks/modules``
* папка одного БЭМ-блока содержит в себе один Pug-файл, один SCSS-файл и один JS-файл (если у блока используется скрипт)
  * Pug-файл блока импортируется в файл ``src/views/index.pug`` (или в необходимый файл страницы, откуда будет вызываться блок)
  * SCSS-файл блока импортируется в файл ``src/blocks/modules/_modules.scss``
  * JS-файл блока импортируется в ``src/js/import/modules.js``

Пример структуры папки с БЭМ-блоком:

```
blocks
├── modules
│   ├── header
│   │   ├── header.pug
│   │   ├── header.js
│   │   ├── header.scss
```

Чтобы вручную не создавать соответствующие папку и файлы, достаточно в консоли прописать следующие команды:

* ``yarn run bem-m my-block`` - для создания БЭМ-блока в ``src/block/modules`` (для основных БЭМ-блоков), где ``my-block`` - имя БЭМ-блока (после создания нужно удалить содержимое js-файла БЭМ-блока);
* ``yarn run bem-с my-component`` - для создания компонента в ``src/blocks/components`` (для компонентов), где ``my-component`` - имя компонента (после создания нужно удалить содержимое js-файла БЭМ-компонента);

### <a name="components">Компоненты</a>

* компоненты (например, иконки, кнопки) оформляются в Pug с помощью примесей
* каждый компонент имеет свою папку внутри ``src/blocks/components``
* папка одного компонента содержит в себе один Pug-файл, один SCSS-файл и один JS-файл (если у компонента используется скрипт)
  * Pug-файл компонента импортируется в файл главной страницы ``src/views/index.pug`` (или в необходимый файл страницы, откуда будет вызываться компонент)
  * SCSS-файл компонента импортируется в файл ``src/blocks/components/_components.scss``
  * JS-файл компонента импортируется в файл ``src/js/import/components.js``

### <a name="pages">Страницы проекта</a>

* страницы проекта находятся в папке ``src/views/pages``
  * каждая страница (в том числе главная) наследует шаблон ``src/views/layouts/default.pug``
  * главная страница: ``src/views/index.pug``

### <a name="fonts">Шрифты</a>

* шрифты находятся в папке ``src/fonts``
  * используйте [форматы](https://caniuse.com/#search=woff) ``.woff`` и ``.woff2``
  * шрифты подключаются в файл ``src/styles/base/_fonts.scss``
  * сконвертировать локальные шрифты можно с помощью [данного сервиса](https://onlinefontconverter.com/)

## Адаптация

Если по проекту и макету нет четкого гайдлайна, в body стоит адаптивный шрифт. За основу берется браузерный стандарт 16px. Минимальный шрифт 0.9rem (14.4px), максимальный - 1rem (ну, собственно, 16px). Ширина экрана, на которой меняется шрифт - от 768px до 1024px.

Если вам нужны аналогичные вычисления для своих значений, рекомендую воспользоваться этим [калькулятором](https://nekocalc.com/px-to-rem-converter).


Шрифты лучше перераспределять с 16px в html {} на 14px на брейкпоинте, означающем переход на размер мобильных устройств

### <a name="images">Изображения</a>

* изображения находятся в папке ``src/img``
  * изображения автоматически конвертируются в формат ``.webp``. Подробная информация по использованию [тут](https://vk.com/@vk_it-webp)
  * изображение для генерации фавиконок должно находиться в папке ``src/img/favicon`` и иметь размер не менее ``1024px x 1024px``

### <a name="sprites">SVG-спрайты</a>

Для создания спрайтов изображения ``.svg`` должны находиться в папке ``src/img/sprites``. Например, у нас есть файлы ``icon-1.svg``, ``icon-2.svg`` и ``icon-3.svg``, и мы должны обратиться к ``icon-2.svg``. Для этого в HTML нужно воспользоваться тегом ``use``:

```pug
svg
    use(xlink:href="img/sprites/sprite.svg#logo")
```

Изменить стили svg-иконки из спрайта в CSS:

```css
svg use {
  fill: red;
}
```

Бывает такая ситуация, когда стили иконки поменять не получается. Это связано с тем, что при экспорте из Figma в svg добавляется лишний код. Например:

```html
<svg width="18" height="19" viewBox="0 0 18 19" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M4.90918 4.04542L13.091 9.54088L4.90918 14.9545L4.90918 4.04542Z" fill="#1B1B1D"/>
</svg>
```

Нужно удалить ``fill="none"`` и ``fill="#1B1B1D"``. Должно получиться так:

```html
<svg width="18" height="19" viewBox="0 0 18 19" xmlns="http://www.w3.org/2000/svg">
  <path d="M4.90918 4.04542L13.091 9.54088L4.90918 14.9545L4.90918 4.04542Z"/>
</svg>
```

### <a name="vendors">Cторонние библиотеки</a>

* все сторонние библиотеки устанавливаются в папку ``node_modules``

  * для их загрузки воспользуйтеcь командой ``yarn add package_name``
  * для подключения JS-файлов библиотек импортируйте их в самом начале JS-файла БЭМ-блока (то есть тот БЭМ-блок, который использует скрипт), например:

  ```javascript
  import $ from "jquery";
  ```

  * для подключения стилевых файлов библиотек импортируйте их в файл ``src/styles/vendor/_libs.scss``
  * JS-файлы и стилевые файлы библиотек самостоятельно изменять нельзя

## 👉 <a name="withoutpug">Нужен SCSS без Pug?</a>

Используйте [эту](https://github.com/andreyalexeich/gulp-scss-starter/) сборку.

## 💛 <a name="donate">Нравится проект?</a>

Сообщайте мне о [багах](https://github.com/andreyalexeich/gulp-pug-starter/issues), ставьте звёздочку в правом верхнем углу, [задонатьте](https://qiwi.com/n/ANDREYALEXEICH) мне на пиво 🍺

## ✉️ <a name="contacts">Контакты</a>

По всем вопросам пишите в [Telegram](https://t.me/andreyalexeich)
