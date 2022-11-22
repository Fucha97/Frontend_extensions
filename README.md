# Lesson 1.

## Contents

1. [Chapter I](#chapter-i) \
   1.1.[Что такое расширение](#что-такое-расширение) \
   1.2 [Как расширения работают](#как-расширения-работают) \
   1.3 [Canvas](#canvas) \
   1.3 [СORS](#cors)

## Chapter I

Перед началом изучения ознакомтесь с инструкцией и убедитесь что у вас установлены все необходимые инструменты для выполнения заданий.

В данной главне мы рассмотрим браузерные расширения, изучим как они работают, а также познакомимся с тегом canvas.

### Что такое расширение

Наверняка вы знаете, что такое расширение для браузера – большинство людей используют их в повседневной жизни для более комфортного времяпрепровождения в браузере, такие как AdBlock или Vpn. Давайте определим, что такое расширение и что оно из себя представляет. Расширения является программой, которую можно подключить к браузеру и главное задачей которой является расширение возможностей этого браузера.

### Как расширения работают

Расширения построены на основе веб-технологий, таких как HTML, JavaScript и CSS. Они запускаются в отдельной, "песочнице", среде выполнения и взаимодействуют с браузером Chrome.
Расширения работают с помощью пользовательского интерфейса конечного пользователя и API разработчика.
Чтобы создать расширение, вы собираете некоторые ресурсы - манифест, файлы JavaScript и HTML, изображения и другие - которые составляют расширение.
И так, по подробнее - в каждом расширении для Chrome должен быть файл manifest.json. В нем содержатся описание метаданных вашего расширения: \
`-` Название. \
`-` Версия

Также в нем могут быть описаны аспекты функциональности вашего расширения: \
`-` Фон. \
`-` Сценарий контента. \
И др.

Пример простого manifest.json от разработчиков Chrome:

```
{
  "name": "Hello Extensions",
  "description": "Base Level Extension",
  "version": "1.0",
  "manifest_version": 3,
  "action": {
    "default_popup": "hello.html",
    "default_icon": "hello_extensions.png"
  }
}
```

[Полный список ключей manifest.json](https://developer.mozilla.org/en-US/docs/Web/Manifest) можно найти в mdn web docs.
Для разработки и тестирования вашего расширения вы можете загрузить его в Chrome, используя режим разработчика расширений.

### Canvas

Давайте немного поговорим о таком тэге как Canvas. Canvas является тегом HTML5, который предназначен для создания растрового изображения с помощью Javascript. Забегая немного вперед, данный тэг вам понадобится для выполнения одного из заданий, поэтому будьте внимательны.
Сам <canvas> представляет из себя контейнер для графики, для того чтобы что-то произошло необходимо использовать Javascript.

Для начала работы с canvas нам потребуются следующие строчки:
const canvas = document.getElementById(‘çanvas’);
const ctx = canvas.getContext('2d');

getContext – метод, принимающий 1 аргумент (тип контекста) и позволяющй нам получить контект виизуализации и функциии рисования. В данном случае тип контекта 2D. Далее мы готовы начать рисовать

Пример кода прямой линии:

```
context.moveTo(10,10);
context.lineTo(400,40);
context.stroke();
```

С базовым принципом работы разобрались, также хотелось бы затронуть тему использования изображений в canvas.
Изображения в canvas могут быть использованы для отображения фона в играх или графиках, для динамической композиции фото и так далее.
Чтобы импортировать изображение в canvas для дальнейшей манипуляции нам необходимо: \
`-` Получить ссылку на HTMLImageElement или Url изображения. \
`-` Использовать метод drawImage().

CanvasRenderingContext2D предоставляет нам один занятный метод, который называется **getImageData()** - он возвращает объект ImageData, представляющий базовые пиксельные данные для указанной части холста.

Для тех, кто заинтересовался данным элементом(canvas) и негодует почему предоставлено так мало информации, не волнуйтесь, основная цель в данной главе — это ознакомление, в последующих уроках у вас будет возможность изучить больше возможностей canvas.

### CORS

В двух словах о CORS и CORS в canvas.

Cross-origin resource sharing (CORS) – это механизм, основанный на HTTP протоколе, который позволяет серверу распознать любые источники (домен, порт и т.д.) отличные от своего собственного, с которых браузер должен разрешить загрузку ресурсов. CORS также опирается на механизм, при котором перед отправкой фактического запроса, браузер шлет запрос с заголовками, которые будут использоваться при фактическом запросе на сервер, на котором находится cross-origin resource, для проверки возможна ли отправка фактического запроса.

В целях безопасности браузеры ограничивают cross-origin запросы, инициируемые скриптами. Например, Fetch следуют same-origin-policy. Политика одинакового источника предотвращает cross-origin атаки, блокируя доступ для прочтения загружаемых ресурсов из другого источника.

Следует отметить проблему безопасности в canvas, пиксели в растровом изображении при их загрузке из различных источников, в том числе с других хостов, являются уязвимым местом.

Как только вы рисуете на холсте любые данные, которые были загружены из другого источника без одобрения CORS, холст становится испорченным. Испорченный холст — это тот, который больше не считается безопасным, и любые попытки получить данные изображения с холста вызовут исключение.

Для избежания этого, можно воспользоваться HTML атрибутом crossorigin, который в сочетании с соответствующими заголовками CORS дает возможность использовать различные изображения, полученные из сторонних источников в canvas, также как если бы они были загружены из одного источника.

### Project_01

Вам предстоит реализовать два довольно полезных для frontend разработчика расширения:

- ColorPicker (установлено по дефолту при открытие расширения). С помощью этого расширения юзер может узнать цвет любого пикселя на активной вкладке браузера. В момент работы этого расширения юзер может двигать мышкой и видеть цвет каждого пикселя, на котором в текущий момент установлен курсор. В месте расположения курсора виден [label](./materials/label.png) в котором указан цвет в форматах HEX и RGB
- PixelRuler. С помощью этого расширения юзер может измерить интересующую его высоту/длину. При клике мышкой по любому месту страницы он устанавливает точку отсчета, по следующему клику устанавливается финишная точка, между этими точками строится отрезок и указывается его длина. В момент работы данного режима курсор пользователя [изменяется](materials/cursor.png). По клику на мышь устнавливаются начальная и конечная точки отрезка. После чего юзер может видеть прямую линию построенную по этим точках. Над линией указана ее длина в пикселях

Если, вдруг, вы очень долгое время не можете придумать как реализовать проект, то мы оставили небольшие подсказки в [этом файле](./Spoiler.md)
