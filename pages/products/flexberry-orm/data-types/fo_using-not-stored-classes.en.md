---
title: The use of not-stored classes
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, data types, DataObject
summary:  Features of launching forms using not-stored classes
toc: true
permalink: en/fo_using-not-stored-classes.html
lang: en
---

Генерируемые [Flexberry ORM](fo_flexberry-orm.html) формы для нехранимых классов удобно использовать для выбора некого текущего объекта, проведении авторизации пользователей.

Для того чтобы сделать класс нехранимым, необходимо при работе с диаграммой классов убрать галочку у параметра `Stored` в его свойствах (либо добавить символ "/" перед его названием).

Для того чтобы подавить сообщения с вопросом о необходимости сохранения данных формы, можно переопределить метод формы `OnClosing`, где запретить вызов базового метода.

```csharp
protected override void OnClosing(CancelEventArgs e)
{
	//base.OnClosing(e);
}
```

## Запуск немодальной формы

Для запуска полученной формы немодально можно воспользоваться [инструкцией](fw_force-call-editing-form.html).

{% include note.html content="При создании формы используется независимая форма, которая вызовет зависимую форму." %}

{% include note.html content="Описаный способ хорош только для запуска немодальной формы. При использовании данного способа для запуска модальной формы необходимо переопределение метода [Edit](fa_form-interaction.html), однако простой заменой в соответствующем коде вызова `Show` на `ShowDialog` не добиться решения проблемы, поскольку этот вариант не учитывает, что для корректной работы формы должна пройти определённая последовательность вызовов." %}

## Запуск модальной формы

Для запуска формы в модальном режиме можно подключить сборку `IIS.WinUI` к проекту, а далее в коде осуществить с помощью неё запуск формы (пример запуска формы представлен в статье [Установка текущего объекта при запуске приложения](fo_define-default-object.html)).
