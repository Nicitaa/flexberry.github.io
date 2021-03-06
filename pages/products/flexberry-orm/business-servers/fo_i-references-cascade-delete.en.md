---
title: IReferencesCascadeDelete
sidebar: flexberry-orm_sidebar
keywords: DataObject, Flexberry ORM, business-servers, сascading deletion of objects
summary: Features of cascading deletion of objects
toc: true
permalink: en/fo_i-references-cascade-delete.html
lang: en
---

Интерфейс `IReferencesCascadeDelete` позволяет осуществлять каскадное удаление объектов (при удалении самого объекта все ссылающиеся на него объекты также удаляются).

## Как работает IReferencesCascadeDelete

Логика по каскадному удалению прописана в [бизнес-сервере](fo_bs-wrapper.html) интерфейса `IReferencesCascadeDelete`, собственных свойств и методов данный интерфейс не предоставляет. Таким образом, чтобы вместе с некоторым объектом удалить все объекты, которые на него ссылаются, достаточно, чтобы класс объекта был наследником от `IReferencesCascadeDelete`.
Поиск классов, которые ссылаются на искомый, осуществляется следующим образом:

1. Определяется директория, где располагается сборка с классом, ссылки на который мы ищем.
2. В директории выбираются все сборки, имя которых заканчивается на «(Objects).dll».
3. В сборках ищутся типы, наследующие от [DataObject](fo_data-object.html).
4. В найденных типах определяются свойства, которые содержат ссылку на искомый класс или его прародителей. 

## Пример

Пусть у есть диаграмма вида:

![](/images/pages/products/flexberry-orm/i-references-cascade-delete/i-references-cascade-delete.png)

На диаграмму добавлен `IReferencesCascadeDelete` со стереотипом [externalinterface](fd_external-interface.html) , от которого наследуется класс `Territory2` и `Country2`. При удалении экземпляров этого класса будут удаляться также все объекты, которые ссылаются на них.
При указанном расположении классов с учётом [наследования](fd_inheritance.html):
1. При удалении экземпляра класса `Territory2` будут проверяться ссылки среди экземпляров классов `Human2` и `Place2`.
2. При удалении экземпляра класса `Country2` будут проверяться ссылки среди экземпляров классов `Human2`, `Place2`, `Adress2`, `Apparatus2` (экземпляры класса `Region` являются детейлами и будут удаляться даже без использования соответствующего интерфейса).
