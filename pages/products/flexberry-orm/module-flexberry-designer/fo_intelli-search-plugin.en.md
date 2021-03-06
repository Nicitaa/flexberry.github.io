---
title: Search function
sidebar: flexberry-orm_sidebar
keywords: Flexberry Designer, Flexberry ORM, plugins
summary: Features of using the search for fragments of diagrams for selected projects
toc: true
permalink: en/fo_intelli-search-plugin.html
lang: en
---

Модуль расширения [Flexberry Designer](fd_landing_page.html): `IntelliSearch` разработан для поиска фрагментов диаграмм по выбранным проектам репозитория.

## Подключение

Подключение осуществляется по следующему алгоритму:

* Зарегистрировать плагин в CASEBERRY
    * Открыть меню `Полезности` - `Модули`
    * Нажать `Создать`
    * Указать путь к библиотеке `IntelliSearch.dll`

* Добавить плагин к репозиторию
    * Открыть свойства репозитория, выбрав пункт меню `Репозитарий` - `Редактировать свойства`
    * В разделе `Модули` нажать `Создать`, в добавившейся строке в колонке `Модуль` выбрать `IntelliSearchPlugin`
    * Сохранить изменения

{% include note.html content="Подробнее о модулях и их подключении можно посмотреть в статье [Модули расширения функциональности](fd_flexberry-plugins.html)." %}

После этого появится пункт меню Стадии `IntelliSearchPlugin`, позволяющий переформировать индекс для конкретной Стадии, а также кнопка `Искать в других стадия` на диаграмме классов.

## Использование поиска

Чтобы воспользоваться поиском, необходимо:

* Создать пустую диаграмму классов в любой стадии
* Нарисовать объекты (классы, связи и пр.), которые необходимо найти
* Нажать кнопку `Искать в других стадиях` 

![](/images/pages/products/flexberry-orm/module-flexberry-designer/search-example.png)

* В открывшемся окне "Стадии для поиска" выбрать интересующие стадии 

![](/images/pages/products/flexberry-orm/module-flexberry-designer/search-studys.png)

* При необходимости настроить параметры поиска (порог релевантности и важность совпадения имен\типов данных\значений по умолчанию\кардинальностей) нажав на кнопку `Параметры поиска`

![](/images/pages/products/flexberry-orm/module-flexberry-designer/search-params.png)

* Нажать кнопку `Поиск`.

{% include note.html content="Поиск требует индексации стадий, если будет выбрано большое количество непроиндексированных стадий, то процесс индексации может занять длительное время." %}

Результат представляется в виде дерева стадий со скриншотами диаграмм, на которых найдены схожие фрагменты. Скриншот диаграммы можно открыть в натуральную величину.

![](/images/pages/products/flexberry-orm/module-flexberry-designer/search-results.png)
