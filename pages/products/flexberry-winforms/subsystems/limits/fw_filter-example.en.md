---
title: Пример использования AdvLimit и создания FilterSettings
sidebar: flexberry-winforms_sidebar
keywords: Ограничения
summary: Описание формы задания пользовательских ограничений, и указание как настроить её для обеспечения возможности накладывать ограничения по детейлам
toc: true
permalink: en/fw_filter-example.html
folder: products/flexberry-winforms/
lang: en
---

## Форма редактирования пользовательских ограничений (AdvLimit)

В сгенерированных формах приложения существует возможность наложения пользовательских ограничений на списки. Пользовательские ограничения позволяют настроить правила, по которым отфильтровываются объекты, попадающие в список. Рассмотрим на примере:

''Примечание: предполагается, что приложение уже сгенерировано''

### Диаграмма классов

![](/images/pages/products/flexberry-winforms/subsystems/limits/filter-ex-diagram.png)

### Форма задания пользовательских ограничений

Допустим, что у нас есть список из 5 клиентов, заполненный следующим образом, и мы хотим выделить всех клиентов, прописанных в Перми:

![](/images/pages/products/flexberry-winforms/subsystems/limits/filter-ex-list1.png)

Чтобы это сделать, необходимо открыть форму редактирования пользовательских ограничений и ввести соответствующее ограничение на поле `Прописка`. Проверка весьма примитивна - проверяем строку на наличие в ней подстроки "Пермь".

![](/images/pages/products/flexberry-winforms/subsystems/limits/filter-ex-list2.png)

После того, как ограничение заполнено, необходимо нажать кнопку "`Сохранить и применить`", после возвращения на форму необходимо обновить список, чтобы к нему применилось ограничение.

![](/images/pages/products/flexberry-winforms/subsystems/limits/filter-ex-list3.png)

Как можно заметить, количество Клиентов сократилось до 3х человек: остались только те, у кого в поле `Прописка` была подстрока Пермь.

Чтобы вернуть список в исходное состояние, необходимо сбросить текущее ограничение, нажав кнопку "`Сбросить ограничения`"

![](/images/pages/products/flexberry-winforms/subsystems/limits/filter-ex-list4.png)


## Пример настройки FilterSettings

FilterSettings позволяют настроить доступные для наложения пользовательских ограничений поля объекта. Рассмотрим пример:

![](/images/pages/products/flexberry-winforms/subsystems/limits/filtersettings-ex0.png)

Так выглядит форма настройки списка Кредитов. Предположим, что мы хотим отфильтровать список и вывести те кредиты, в которых было хотя бы одно погашение на сумму, превышающую 100 000.

Откроем форму создания пользовательских ограничений:

![](/images/pages/products/flexberry-winforms/subsystems/limits/filtersettings-ex1.png)

В дереве полей объекта Кредит есть все его мастера, а также собственные поля, но нет его детейлов. Чтобы в нем появились детейлы, необходимо создать FilterSetting через AdmConsole.

1. Скачиваем AdmConsole 
2. Правим `AdmConsole.exe.cofig`, необходимо прописать путь к базе данных нашего приложения в ключ CustomizationString 

```
 <add key="CustomizationStrings" value="SERVER=localhost;Trusted_connection=yes;DATABASE=credits;" /> 
```

3. При первом запуске приложения выберем папку с кешем сборок, можно указать путь к папке, куда собирается проект с Объектами, но предпочтительнее создать отдельную папку.
4. В папку с кешем надо скопировать:
    1. DLL с объектами `<ИмяПроекта>(Objects).dll`
    2. DLL с Формами `<ИмяПроекта>(Forms).dll`
    3. IIS.WinUI.AdvancedFSCtrl.dll - находится в папке с AdmConsole.exe
5. Откроем `Специальные формы настройки` -> `Настройки фильтров`
6. Создадим новую настройку, нажав на кнопку `Создать`, откроется форма создания настроки.
7. На форме: ![](/images/pages/products/flexberry-winforms/subsystems/limits/filtersettings-ex2.png)
    1. Введем `Наименование` настройки
    2. Выберем сборку из выпадающего списка
    3. Выберем тип `Кредит`
    4. Выберем представление `КредитL`
    ![](/images/pages/products/flexberry-winforms/subsystems/limits/filtersettings-ex3.png)
    6. Перейдем на вкладку `Детейлы` и нажмем кнопку `Заполнить`.
''__Примечание__: если при нажатии на кнопку `Заполнить` появляется сообщение "Нет измененных детейлов", необходимо сохранить настройку и попробовать снова''
8. Сохраним настройку и выйдем из AdmConsole

Теперь необходимо указать приложению, что на списковой форме `Кредитов` должна быть применена эта настройка фильтров. Варианты:
* [Настройка в дизайнере VS](fw_filter-settings.html)
* [Настройка через код](fw_filter-settings.html). ''__Примечание__: если нет возможности открыть проект в Visual Studio, но есть желание все-таки применить эту настройку, необходимо сделать следующее:
    * Открыть папку с проектами форм
    * Найти файл КредитL.cs и открыть его любым текстовым редактором (например Блокнотом)
    * Найти метод GetDpdForm()
    * Записать в [скобки программиста](fd_change-model.html) `КредитL.GetDpdForm() end` следующую строчку кода:

```csharp 
form.FilterSettingName = "Кредиты"; 
```

* Сохранить файл''

Теперь после сборки приложения зайдем на форму кредитов и откроем форму создания пользовательских ограничений:

![](/images/pages/products/flexberry-winforms/subsystems/limits/filtersettings-ex4.png)

Как видите, появилась возможность наложения ограничений на детейл Кредита. Создадим условие, фильтрующее все кредиты с погашениям свыше 100000. Нажмем `Сохранить и применить` и обновим список на форме, получим:

![](/images/pages/products/flexberry-winforms/subsystems/limits/filtersettings-ex5.png)




