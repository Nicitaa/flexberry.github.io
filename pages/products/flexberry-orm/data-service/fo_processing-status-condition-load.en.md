---
title: Processing of the status and status of object loading
sidebar: flexberry-orm_sidebar
keywords: Flexberry ORM, data service
summary: Processing of the status and state of loading an object by data services
toc: true
permalink: en/fo_processing-status-condition-load.html
lang: en
---

При обновлении в хранилище объекта данных, любой сервис данных учитывает статусы следующим образом:

| **ObjectStatus**| **Хранилище**| **Объект данных**|
|:----------------|:----------------|:----------------|
| UnAltered| Не изменяет данные| Не меняется (остаётся Loaded/LightLoaded и UnAltered)|
| Created| Создаёт данные в хранилище| Меняется статус на Loaded и UnAltered|
| Altered| Изменяет данные в хранилище| Меняется статус на Loaded/LightLoaded и UnAltered|
| Deleted| Удаляет данные из хранилища| Объект удаляется из массива обрабатываемых объектов (возвращается null в случае одного объекта)|