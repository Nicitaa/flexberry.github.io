---
title: Вариант 6 - «Пропускная система в офисе»
keywords: Tasks
sidebar: guide-tasks_sidebar
toc: true
permalink: ru/gt_flexberry-ember-case-06.html
lang: ru
summary: Вариант сквозного задания на проектирование и разработку с использованием фреймворка Flexberry Ember
---

## Задание

В рамках выполнения практической части курса вами будет разработан сквозной пример: приложение «Пропускная система в офисе» (ИС для автоматизации учета перемещения сотрудников офиса).

Первая часть практического задания будет посвящена освоению базовых технологий, таких как C#, базы данных, клиентские технологии и т.п., вторая часть будет включать изучение возможностей платформы Flexberry для эффективного создания приложений.

## Общее описание предметной области

В офисе компании Х вводится пропускная система на основе персональных пропускных карт. При помощи карты сотрудник может попасть на любой этаж в офисе, в общественные места (кухня, переговорка и т.п.) и только в свой кабинет. Требуется разработать информационную систему, в которой будет вестись информация как о выданных персональных пропускных картах, так и информация о перемещениях сотрудников. Все двери кабинетов, в которых работают сотрудники могут находиться в 2-х состояниях: `замок открыт` и `замок закрыт`. Во время рабочего дня, если в кабинете находятся сотрудники, как правило дверь находится в состоянии `замок открыт`. Таким образом, при перемещении между кабинетами офиса сотрудники не всегда используют карты. На входе и выходе из здания офиса все сотрудники обязаны использовать карту в индивидуальном порядке, это позволяет зафиксировать время прихода сотрудника в офис и время его ухода.

Технические требования:

*	Приложение реализуется в виде [SPA-приложения](https://ru.wikipedia.org/wiki/%D0%9E%D0%B4%D0%BD%D0%BE%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%87%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5) с бакендом на C# и фронтендом на EmberJS.
*	Данные хранятся в БД Postgres.

## Практическое задание №1 - Серверная разработка (C#, .NET, ASP.NET)

Для реализации потребуется:

* Microsoft Visual Studio 2017
* Git for Windows

### Задание

Требуется реализовать алгоритм вычисления дружеских связей сотрудников на основе информации о совместном обеде или приходе и уходе из офиса. Если несколько сотрудников в течение недели выходили на обед с разницей не более 5 минут и возвращались с обеда с такой же небольшой разницей не менее 3-х раз, то они считаются друзьями. Если сотрудники приходят в офис утром и уходят вечером в одно и то же время с разницей не более 5-ти минут не менее 3-х раз, то тоже считаются друзьями.  
На вход алгоритму подаётся массив структур, которые содержат:

* ФИО сотрудника и его id
* Массив кортежей: дата-время прихода в офис и дата-время ухода из офиса

На выходе должен быть массив кортежей, каждый из которых содержит информацию о дружеских отношениях между сотрудниками.  
Реализацию следует сделать в виде .net-библиотеки и подготовить модульные тесты для неё (xUnit), продемонстрировать процент покрытия кода модульными тестами (чем больше, тем лучше).

### Предоставление результатов выполнения работы на проверку

Реализованное решение (Visual Studio Solution) полностью разместить в репозитории на GitHub (решение должно компилироваться и запускаться). Ссылку на репозиторий предоставить преподавателям курса.

## Практическое задание №2 - Клиентская разработка (HTML, CSS, JS, jQuery)

Для реализации потребуется:

* Редактор кода для клиентской разработки: Visual Studio Code
* Git for Windows

### Задание

С использованием возможностей HTML, CSS, JS, jQuery сверстать форму, на которой пользователь может указать ФИО сотрудника, год, месяц и получить информацию о его посещениях офиса с детализацией до каждого дня. Форма должна напоминать месячный календарь, т.е. в таблице должно быть 7 столбцов (пн, вт, ср, чт, пт, сб, вс) и недели в строках. В каждой ячейке таблицы должно быть указано число и время прихода-ухода в офис (сотрудник может несколько раз посещать офис).

### Предоставление результатов

Реализованный проект разместить в репозитории на GitHub в виде встроенных страниц GitHub Pages, позволяющих просматривать готовый результат. Ссылку на репозиторий и опубликованный таким образом проект предоставить преподавателям курса.

## Практическое задание №3 - Клиентская разработка с использованием SPA-фреймфорка (EmberJS)

Для реализации потребуется:

* Редактор кода для клиентской разработки: Visual Studio Code
* Git for Windows

### Задание

Требуется реализовать EmberJS приложение, в котором будет реализована форма, на которой пользователь может указать ФИО сотрудника, год, месяц и получить информацию о его посещениях офиса с детализацией до каждого дня. Форма должна напоминать месячный календарь, т.е. в таблице должно быть 7 столбцов (пн, вт, ср, чт, пт, сб, вс) и недели в строках. В каждой ячейке таблицы должно быть указано число и время прихода-ухода в офис (сотрудник может несколько раз посещать офис). Под календарём должен выводить список вероятных друзей данного сотрудника (EmberJS-компонент).  

В виде EmberJS-утилиты требуется реализовать алгоритм вычисления дружеских связей сотрудников на основе информации о совместном обеде или приходе и уходе из офиса (см. задание №1).

Требуется реализовать компонент, в который передаётся id сотрудника, год и месяц, а он отображает список сотрудников, которые могут являться друзьями данного сотрудника. Использовать в компоненте EmberJS-утилиту с алгоритмом вычисления дружеских связей.  

### Предоставление результатов

Реализованный проект разместить в репозитории на GitHub в виде проекта EmberJS и опубликованного приложения в GitHub Pages, которые позволяют просматривать готовый результат. Ссылку на репозиторий и опубликованный таким образом проект предоставить преподавателям курса.

## Практическое задание №4 - Базы данных

Для реализации потребуется:

*	Postgres
*	pgAdmin
*	Git for Windows

### Задание

Для указанной предметной области реализовать базу данных, заполнить базу скриптами (минимум по 5 записей на таблицу). Реализовать скрипты по созданию ограничений, индексов. 

Подготовить SQL-скрипты для получения следующей информации:

1. Вывести топ-5 сотрудников, которые проводят в офисе больше всего времени
2. Вывести информацию о количестве открываний-закрываний двери на каждом из этажей в порядке убывания
3. Вывести информацию о рабочих днях максимальном, среднем и минимальном количестве сотрудников, посетивших офис
4. Вывести информацию об общем времени работы всех сотрудников в офисе по месяцам
5. Вывести топ-5 кабинетов, которые больше всего простаивают (чаше других закрыты на ключ)

### Предоставление результатов

Реализованные скрипты создания БД и заполнения, бекап БД закоммитить в GitHub-репозиторий. Ссылку на репозиторий предоставить преподавателям курса.

## Практическое задание №5 - Проектирование ИС

Для реализации потребуется:

*	Flexberry Designer

### Задание

Нарисовать UML-диаграммы для обозначенной предметной области. Состав диаграмм определяется самим слушателем курсов, но должен обеспечивать полноценное описание предметной области.

### Предоставление результатов

Результатом работы является выгруженная в формате CRP стадия из Flexberry Designer. Стадию (файл с расширением *.CRP) следует закоммитить в репозиторий на GitHub, ссылку предоставить преподавателям курса.

## Практическое задание №6 - Объектный дизайн и генерация приложений

Для реализации потребуется:

*	Flexberry Designer
*	Microsoft Visual Studio 2017
*	Postgres
*	Git for Windows

### Задание

Выполнить объектный дизайн и генерацию Ember-приложения для описанной предметной области. В качестве основы использовать реализованные ранее UML-модели. Генерация приложения и БД должна быть выполнена средствами Flexberry Designer приложение должно соответствовать требованиям и быть полностью работоспособным. Представления должны быть качественно настроены, подписи к классам и атрибутам на формах должны быть адекватными. Перечень форм и атрибутивный состав должны соответствовать предметной области и покрывать все требуемые бизнес-функции.

### Предоставление результатов

Сгенерированное приложение и скрипты создания БД следует выложить в репозиторий на GitHub. Предоставить преподавателям ссылку на репозиторий.

## Практическое задание №7 - Разработка бизнес-логики приложений

Для реализации потребуется:

* Flexberry Designer
* Microsoft Visual Studio 2017
* Postgres
* Git for Windows

### Задание

В сгенерированном при помощи Flexberry Designer приложении требуется реализовать следующую бизнес-логику.

1. Реализовать бизнес-сервер, который будет контролировать, что сотрудник не выходит из здания, если он не входил в него и наоборот - не входит, если не выходил. Должно быть сгенерировано событие, которое свидетельствует о неисправности оборудования.
2. Реализовать бизнес-сервер, который будет запрещать удаление объектов с информацией о проходе по карте (чтобы нельзя было скрыть преступление).
3. Реализовать бизнес-сервер, который будет контролировать закрыли ли сотрудники дверь кабинета перед уходом. Если сотрудник кабинета выходит последним из здания, а дверь кабинета находится в состоянии `замок открыт`, то нужно сгенерировать событие с информацией о сотруднике и номере кабинета.
4. Добавить не хранимое поле в класс Сотрудник, которое будет представлять ФИО одной строкой из Фамилии Имени и Отчества.
5. Добавить не хранимое поле ВОфисе в класс сотдудник, которое будет сигнализировать о том в офисе находится сотрудник или нет.

### Предоставление результатов

Доработанная бизнес-логика должна быть включена в разрабатываемое приложение и закоммичена в соответствующий репозиторий. Ссылка на репозиторий предоставляется для проверки преподавателям курса.

## Практическое задание №8 - Разработка UI-логики приложения

Для реализации потребуется:

*	Microsoft Visual Studio 2017
*	Postgres
*	Редактор кода для клиентской разработки: Visual Studio Code
*	Git for Windows

### Задание

Привязать реализованные ранее EmberJS дополнительные формы и компоненты к данным из БД.  
Перенести в сгенерированное приложение и реализовать интеграцию формы из задания №3 с бизнес-логикой приложения. 
На форме для элементов управления с выбором - данные должны браться из БД (через ORM и Lookup). Заполнение данных также должно работать с сохранением в БД. 
Требуется настроить красивый внешний вид для всех форм приложения. Улучшить визуальную тему оформления. Реализовать ярлыки на рабочем столе приложения для быстрого доступа к часто используемым функциям.  
Реализовать дополнительные формы, которые будут выводить результаты выполнения запросов из задания по БД.

### Предоставление результатов

Доработанная UI-логика должна быть включена в разрабатываемое приложение и закоммичена в соответствующий репозиторий. Ссылка на репозиторий предоставляется для проверки преподавателям курса.

## Практическое задание №9 - Функциональные подсистемы Flexberry

Для реализации потребуется:

*	Flexberry Designer
*	Microsoft Visual Studio 2017
*	Редактор кода для клиентской разработки: Visual Studio Code
*	Postgres
*	Git for Windows

### Задание

Для реализованного приложения настроить подсистему полномочий. Сотрудники и карты должны заводиться администратором приложения. Авторизация на основе форм. Создать иерархию ролей, добавить операции на просмотр сведений и выдать права только администраторам. Настроить несколько ролей и назначить эти роли пользователям.  
Настроить подсистему аудита. В разрабатываемом приложении все изменения объектов данных должно фиксироваться в подсистеме аудита. В навигационное меню следует добавить формы аудита, которые должны показываться только администраторам.

### Предоставление результатов

Доработанное приложение должно быть закоммичено в соответствующий репозиторий. Дополнительно в репозиторий должны быть добавлены SQL-скрипты, которые нужно выполнить для функционирования приложения с подсистемой полномочий и аудита. Ссылка на репозиторий предоставляется для проверки преподавателям курса.
