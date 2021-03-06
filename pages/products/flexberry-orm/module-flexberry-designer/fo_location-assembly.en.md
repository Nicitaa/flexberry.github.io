---
title: Location of assemblies after code generation
sidebar: flexberry-orm_sidebar
keywords:  Flexberry Designer, Flexberry ORM
summary: The concept of a package, the structure, name and location of the catalogs of the generated application
toc: true
permalink: en/fo_location-assembly.html
lang: en
---

## Понятие пакета

__Пакетом__ называется некоторое логическое объединение генерируемых исходных кодов сборок. После генерации исходники, объединённые в пакет, располагаются в отдельном подкаталоге.

### Структура каталогов после генерации кода выглядит следующим образом

* Каталог, указанный в "Каталога для исходного кода" настроек стадии 
* Приложение 1 
* Приложение 2 
* ... 
* Приложение N 
* Пакет 1 
* Пакет 2 
* ... 
* Пакет N 

Если имя пакета не указано внутри какого-либо класса, то в качестве имени пакета используется [свойство "Название продукта"](fd_project-customization.html) из настроек стадии.

Внутри каждого пакета могут находиться следующие исходные коды сборок(в отдельных каталогах, с указанными именами):

* `BusinessServers` - сборка классов со стереотипами [businessserver](fd_business-servers.html);
* `BusinessServersComPlus` - сборка [обёртки для обращения к бизнес-серверу](fo_bs-wrapper.html) через COM+ для бизнес-серверов, у которых установлена галочка `GenerateComPlusServer`; 
* `BusinessServersHttp` - сборка обёртки для обращения к бизнес-серверуfo_bs-wrapper.html через веб-сервис для серверов, у которых установлена галочка `GenerateHTTPRemoteServer`; 
* `Catchers` - для классов со стереотипом [eventarg](fd_eventarg.html), у которых установлена галочка `GenerateCatcher` в эту сборку генерируются классы-перехватчики событий; 
* `Objects` - классы со стереотипами: [implementation](fd_data-classes.html), `type`, [enumeration](fd_enumerations.html), `eventarg`. 
* `Scripts` - сценарии, определённые диаграммным методом `EBSD`. 

Дополнительно (при наличии специальных генераторов) могут генерироваться:

* `DesktopCustomizers` - сборка классов - настройщиков классов со стереотипом [application](fd_additional-stereotypes.html); 
* `Forms` - классы со стереотипами: [editform, listform, printform, userform](fd_additional-stereotypes.html); 

Если нет в стадии классов, попадающих в соответствующую категорию, то исходные коды не генерируются и каталог не создаётся.

### Пространства имён

Внутри сборок определяются пространства имен. Разработчик может управлять пространствами имен, для чего имеются следующие возможности:

* каждый класс имеет свойство `NamespacePostfix`; 
* стадия имеет свойство [Namespace](fd_project-customization.html). 

Пространства имён формируются следующим образом (слитно приписывается, точка между ними не ставится):

``` csharp
<Namespace стадии> + <NamespacePostfix класса>
```
Если NamespacePostfix класса не указан, то остаётся только "<Namespace стадии>".

Если <Namespace стадии> не указан, то он формируется как "<Название компании>.<Название продукта>" из настроек стадии. [Подробнее...](fd_project-customization.html).
