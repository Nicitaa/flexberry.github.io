---
title: Example of using a business server
sidebar: flexberry-orm_sidebar
keywords: Flexberry Designer, Flexberry ORM, business servers, example
summary: Example of a business server implementation
toc: true
permalink: en/fo_bs-example.html
lang: en
---

В данном примере будет рассмотрено введение ограничений на создание новых объектов на примере следующей [диаграммы классов](fd_class-diagram.html):

![](/images/pages/products/flexberry-orm/business-servers/filter-ex-diagram.png)

`Задача.` При попытке создания нового кредита необходимо проверить, существуют ли непогашенные кредиты для этого Клиента.

## Реализация

Прежде всего необходимо создать класс со стереотипом [businessserver](fd_business-servers.html) на диаграмме классов с наименованием, например, `КредитБС`.

{% include note.html content="Чтобы класс не занимал много места, его можно свернуть, выбрав контекстное меню `Свернуть`." %}

![](/images/pages/products/flexberry-orm/business-servers/bs-example.PNG)

Сохранть диаграмму, чтобы бизнес-сервер попал в список доступных классов.

В свойствах класса `Кредит` в поле [BSClass](fd_data-classes.html) выбирать из выпадающего списка созданный бизнес-сервер.

![](/images/pages/products/flexberry-orm/business-servers/bs-example1.PNG)

Сохранить и закроем окно, а затем - диаграмму классов. Теперь появилась возможность генерации бизнес-серверов. Сгенерировать проект бизнес-серверов.

{% include important.html content="Объекты также нужно перегенерировать, чтобы ссылки объектов и бизнес-серверов были актуализированы." %}

Добавить в проект Visual Studio сгенерированный проект бизнес-серверов.

В классе `Кредит` появилась ссылка в виде атрибута класса на новый бизнес-сервер:

``` csharp
[BusinessServer("IIS.Кредиты.КредитБС, Кредиты(BusinessServers)", ICSSoft.STORMNET.Business.DataServiceObjectEvents.OnAllEvents))
```

Открыть файл бизнес-сервера `КредитБС.cs`.

Код метода `OnUpdateКредит`, принимающий в качестве параметра объект типа `Кредит` и возвращающий объект типа `DataObject[)`

``` csharp
public virtual ICSSoft.STORMNET.DataObject[) OnUpdateКредит(IIS.Кредиты.Кредит UpdatedObject)
{
	// *** Start programmer edit section *** (OnUpdateКредит)

	return new ICSSoft.STORMNET.DataObject[0);
	// *** End programmer edit section *** (OnUpdateКредит)
}
```

Как можно заметить, в этом методе ничего не происходит. В него следует добавить логику по проверке вводимого значения суммы кредита: она должна быть неотрицательной.

``` csharp
public virtual ICSSoft.STORMNET.DataObject[) OnUpdateКредит(IIS.Кредиты.Кредит UpdatedObject)
{
	// *** Start programmer edit section *** (OnUpdateКредит)
	if (UpdatedObject.СуммаКредита < 0)
		throw new Exception("Сумма кредита не может быть отрицательной");

	return new ICSSoft.STORMNET.DataObject[0);
	// *** End programmer edit section *** (OnUpdateКредит)
}
```

Теперь при попытке ввода отрицательного числа в поле `Сумма кредита` будет выдаваться исключение.

Аналогично можно поставить проверки на `СрокКредита` и на `ДатуВыдачи`.

По условиям задачи необходимо проверить, нет ли у данного клиента незакрытых кредитов:

* Данная проверка имеет место только при создании `Кредита`.
* Необходимо найти все кредиты `Клиента`, для которого создается `Кредит` (потребуется наложение [ограничения](fo_limitation.html)).
* Проверить сколько из них не закрыты.
* Вывести сообщение об ошибке если обнаружен незакрытый Кредит.

``` csharp
// Учтем, что данная проверка имеет место только при создании кредита
if (UpdatedObject.GetStatus() == ObjectStatus.Created)
{
     // Найдем все кредиты Клиента, для которого создается Кредит
     var кредиты = LoadAllByКлиент(UpdatedObject.Клиент);
     foreach (Кредит кредит in кредиты)
     {
         // Проверим, сколько из них не закрыты
         decimal sum = кредит.СтрокаПланаПогашения.Cast<СтрокаПланаПогашения>().Sum(stroke => stroke.Сумма);
         if (sum <= кредит.СуммаКредита)
         {
             // Выдадим сообщение об ошибке если обнаружим незакрытый Кредит
             throw new Exception("У данного клиента есть незакрытые кредиты.");
         }
     }
}
```

{% include note.html content="Первая проверка [UpdatedObject.GetStatus() == ObjectStatus.Created](fo_object-status.html), она позволяет отсечь случаи обновления или удаления объекта." %}

Теперь при попытке создания нового `Кредита` будет происходить проверка, описанная выше.

[Бизнес-сервер](fo_bs-wrapper.html) можно создать для каждого класса и вводить необходимую логику, которая будет выполняться в момент сохранения изменений в объект, будь то создание, удаление или изменение состояния объекта.