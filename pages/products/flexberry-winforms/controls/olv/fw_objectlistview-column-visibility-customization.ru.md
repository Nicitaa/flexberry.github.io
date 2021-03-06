---
title: Настройка видимости колонок ObjectListView
sidebar: flexberry-winforms_sidebar
keywords: Windows UI (Контролы), Windows UI (формы), Ограничения
summary: Описан вариант как устанавить видимость некоторой колонки в ObjectListView
toc: true
permalink: ru/fw_objectlistview-column-visibility-customization.html
folder: products/flexberry-winforms/
lang: ru
---
Пусть необходимо, например, в зависимости от полномочий пользователя устанавливать видимость некоторой колонки в [ObjectListView](fw_objectlistview.html).

Изменять objectListView1.Columns во время работы приложения нельзя.

Одним из решений поставленной задачи может быть использование `ObjectListView.View.Properties`.

```csharp
public class WinformC__ПользовательПриложенияL : ICSSoft.STORMNET.UI.BaseWinListStandard, IIS.TryAccessSystem.DPDIC__ПользовательПриложенияL
{
	public WinformC__ПользовательПриложенияL() //конструктор формы
	{
		this.InitializeComponent();
		this.prv_TuneAdditionalObjectListViews();
		// *** Start programmer edit section *** (Form Constructor)
		//...
		if (!ICSSoft.STORMNET.RightManager.AccessObjectCheck(curObject, "Update", false)) //проверяем полномочия пользователя
		{
			var columnInfoList = (from ICSSoft.STORMNET.PropertyInView mi in objectListView1.View.Properties
								  where mi.Name == "ЛогинПользователя"
								  select mi).ToList(); //ищем нужное свойство
			if (columnInfoList.Count == 1) //проверяем, что нужное свойство найдено
			{
				ICSSoft.STORMNET.PropertyInView columnInfo = columnInfoList[0];
				int cINumber = objectListView1.View.Properties.ToList().IndexOf(columnInfo);
				objectListView1.View.Properties[cINumber].Visible = false; //устанавливаем Visible в false
			}
		}
		//...
		// *** End programmer edit section *** (Form Constructor)
	}
	//...
}
```


{% include note.html content="Специфика работы с массивом `ObjectListView.View.Properties` объясняется тем, что `PropertyInView` - это [не класс, а структура](http://generally.wordpress.com/2007/06/21/c-list-of-struct/)." %}


{% include important.html content="Обратите внимание, что настройка видимости колонки происходит в конструкторе формы." %}