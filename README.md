Для построения сайта используется генератор страниц [zola](https://www.getzola.org).

## Структура папок
 - content -- папка с основным контентом )
 - docs -- сюда складываются финальные странички, которые потом раздаются с github
 - sass -- папка со стилями, скопировал со старой темы "как есть"
 - static -- папка со всякими общими скриптами/картинками и т.п., копируется при генерации сайта в docs
 - templates -- папка с шаблонами страниц


### Templates
Шаблоны используют движок [Tera](https://tera.netlify.app/docs).
В файлах идет html-разметка и вставки некоторых данных из метаданных страничек.

В partials лежат составные блоки, из которых собираются шаблоны страниц:
 - base -- основной шаблон базовой страницы, в нем подключаются стили/скрипты, сделан каркас страницы
 - favicon -- подключение иконки сайта для разных платформ
 - footer -- блок футера
 - metadata -- описание для соц. сетей
 - navigation -- строка навигации в шапке
 - sidebar -- боковой блок, отдельные элементы можно скрывать через настройки конкретной страницы

Шаблоны страниц есть такие:
 - index -- главная страница (блоки с услугами, уникальными предложениями и ценами)
 - section/section_paginated -- разделы со списками страниц
 - service_page -- странцы с описанием услуг и отзывы, вместо кнопок Вперед/Назад там Записаться
 - blog_page -- страница блога
 - single -- раздел без подстраниц, используется в about и галерее

### Content
Контент лежит в текстовых файлах с markdown-разметкой. Каждый раздел сайта в отдельной папке.

В шапке контена обязательно должен быть блок, обрамленный `---`. В этом блоке задаются настройки 
отдельной страниц. Можно указать следующие вещи:
 - title -- заголовок страницы, попадает в название вкладки в браузере
 - template -- название шаблона, который применять при генерации html-страницы для раздела
 - page_template -- название шаблона, который применять при генерации html-страницы для страниц раздела
 - weight -- вес страницы, используется для сортировки. Чем меньше вес, тем выше страница в списках.
 - date -- дата написания в формате ГГГГ-ММ-ДД

Блоги услуг и цены на главной лежат в `content/_index.md`

Для сервисов/отзывов/статей внутри папки раздела создаются папки для отдельных страниц.
Внутри папки страницы нужно создать файл `index.md` с параметрами и текстом. В папку страницы
можно закинуть картинки. По умолчанию для основной картинки используется первая по алфавиту.
Это можно поменять, см. описание услуг

Чтобы сделать галерею, нужно ее включить в настройках страницы (пример `about/_index.md`):
```
extra:
  gallery: true
```
Картинки в галерее тоже идут по алфавиту

Для разделов можно указать настройки пагинации и сортировки. Сейчас пагинация включена в блоге и отзывах,
по 5 статей на одной странице. Сортировка блога идет по дате в статье, сортировка услуг и отзывов -- по весу.

По умолчанию путь к странице в строке браузера берется из названий папки раздела и папки страницы. 
Для статей в блоге папки пронумерованы, чтобы понимать порядок, поэтому там в каждой странице прописан параметр
```
slug: 'путь до странице в браузере`
```
Для новых статей можно не делать, тогда просто в браузере будет еще номер статьи добавлен.
Для старых пришлось добавить, чтобы сохранить ссылки прежними.

Короткая выжимка для боковой панели задается через:
```
extra:
  abstract: 'тут текст
```

### Работа со статьями
Подготовительные шаги:
1. Скачать [GitHub Desktop](https://desktop.github.com/)
2. Подключить репозиторий https://github.com/9planets-ru/9planets-ru.github.io
3. Скачасть [zola](https://github.com/getzola/zola/releases/download/v0.15.3/zola-v0.15.3-x86_64-pc-windows-msvc.zip). Положить `zola.exe` в папку с сайтом рядом с `zola_server.cmd`

Создание новой статьи
1. Добавить новую папку в `content/blog`. В ней создать файл `index.md`
2. Прописать параметры страницы: title, date, extra:abstract, slug
3. Написать текст. Часть, которая пойдет в список статей отделяется `<!-- more -->`
4. Запустить `zola_server.cmd` и зайти на http://127.0.0.1:1111 -- должен открыться сайт локально. Можно править текст статьи, оно должно автоматом обновляться в браузере.
5. Когда получили локально желаемый результат, запускаем `zola_build.cmd`. Это должно сгенерировать в папке `docs`
новую версию сайта.
6. После этого идем в GitHub Desktop, коммитим все изменения, и пушим их на github.
7. Через минут 5-10 сайт обновляется.





  
 

