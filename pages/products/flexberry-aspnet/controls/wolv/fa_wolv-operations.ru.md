---
title: Операции WebObjectListView
sidebar: flexberry-aspnet_sidebar
keywords: Flexberry ASP-NET
toc: true
permalink: ru/fa_wolv-operations.html
lang: ru
---

При помощи Операций можно настроить поведение WebObjectListView.

Получить доступ к Операциям можно через свойство `Operations` контрола.

Чтобы включить отображение кнопки печати списка, необходимо выполнить следующий код при загрузке страницы:

```csharp
webObjectListView1.Operations.Print = true;
```

## Операции по умолчанию

Настроить операции по умолчанию для всего приложения сразу можно через файл конфигурации `web.config`

Для этого необходимо добавить ключ `WOLVDefaultOperations`, в качестве значения указать список операций через запятую.
Ключ добавляется в секцию `configuration` - `appSettings`:

```xml
<configuration>
  <appSettings>
    <!--Другие ключи-->
    <add key="WOLVDefaultOperations" value="Refresh,Filter,Search,New,Delete,ShowMarks,EditInRow,ConfigureColumns,NewByExampleInRow,ExportToExcel,AllowColumnResizing,LimitEdit,EditOnClickInRow,FixTableHeader,HighlightObject" />
    <!--Другие ключи-->
  </appSettings>
</configuration>
```

## Список операций

| Операция | Описание |
| -------- | -------- |
| AdjustListHeight | Отображать WOLV на всю высоту страницы |
| AllowColumnResizing | Дать пользователю возможность изменять ширину столбцов списка
| CheckChanges | Включать ли проверку изменений на форме редактирования при переходе с неё, инициированным данным списком (по умолчанию true). Подробнее см. ниже. |
| ConfigureColumns  | Кнопка на тулбаре для редактирования отображения столбцов |
| Delete  | Кнопка "Удалить" |
| DeleteInRow  | Кнопка "Удалить" в строке |
| Edit  | Кнопка "Редактировать" |
| EditInRow  | Кнопка "Редактировать" в строке |
| EditOnClickInRow  | Поднимать на редактирование по клику в строке (если форма не на лукапе) |
| ExportToExcel  | Кнопка "Экспорт в Excel" |
| ExportToXML  | Кнопка "Экспорт в XML" |
| Filter  | Кнопка "Фильтр" (простой) |
| FilterStartPercent  | Фильтровать с уже подставленными % в начале строки (по умолчанию true) |
| FilterEndPercent  | Фильтровать с уже подставленными % в конце строки (по умолчанию true) |
| FilterSubString  | Фильтровать по подстроке: % уже подставлены в начало и конец строки, все пробелы так же заменяются на % (по умолчанию false). |
| FixTableHeader | Зафиксировать заголовок таблицы. При прокрутке заголовок будет оставаться на месте. |
| FullViewSearch  | Изменить поиск на поиск по всем полям ([подробнее](fa_wolv-search.html)). |
| HighlightObject  | Подсветка объекта, pk которого был указан в URL ("PK" или WOLVSO) (по умолчанию true). Подсветка делается проставлением класса для td |
| LimitEdit | Расширенный редактор ограничений |
| MultiSelect  | Множественное выделение объектов |
| New  | Кнопка "Новый" |
| NewByExampleInRow  | Кнопка "Создать на основе" в строке (подробнее см. [здесь](fa_web-data-object-prototyping.html)) |
| OpenEditorInNewWindow | Открывать форму редактирования (при создании\редактировании\просмотре объекта) в другом окне браузера |
| OpenEditorInModalWindow  | Отображать форму редактирования (при создании\редактировании\просмотре объекта) в модальной форме. Работает только если `OpenEditorInNewWindow == true`; Кастомный заголовок модальному окну можно задать через необязательное свойство WOLV-a `EditorInModalWindowCaption` |
| Order | Кнопки перемещения строк при наличии в представлении Oreded-атрибутов |
| Print  | Печать списка |
| ReadCommittedUsage  | Отменить использование грязного чтения |
| ReturnUrlParams | Параметры, которые допишутся в `ReturnUrl`. Должны быть в формате `param1=value1&amp;param2=value2`. Если на списковой форме уже есть параметр, который передается через `ReturnUrlParams`, то приоритет будет у `ReturnUrlParams` (т.е. перезапишется параметр, находившийся на списковой форме). |
| Refresh | Кнопка "Обновить" |
| Search  | Кнопка "Поиск" |
| ShowInRow | Отображать кнопку для поднятия формы просмотра объекта. Если она не установлена, то используется форма редактирования в режиме Read-Only. |
| ShowMarks  | Показывать галки |
| SwitchNextPage | Переход на следующую страницу при редактировании последнего объекта на текущей странице |
| UseLocalizedCaptions | Использование механизма локализации заголовков колонок |
| OverflowWordEllipsis | Задает поведение содержимого ячейки при переполнении по ширине столбца. Если опция установлена в False (по умолчанию), то происходит перенос содержимого ячейки на новую строку. Если опция установлена в True, то содержимое ячейки обрезается и в конец добавляется многоточие. |
| UserColumnsSort | Включает или отключает настройку пользователем сортировки списка и восстановление пользовательских настроек сортировки. |

## CheckChanges

Данное свойство работает только в случаях, когда WOLV располагается на форме редактирования.

При попытке уйти со страницы (к примеру, нажав на кнопку "Закрыть"), включается проверка изменений, внесенных в объект. Если в объект были внесены изменения, то пользователю задастся вопрос, хочет ли он сохранить его.

Аналогичная функциональность была добавлена в список, располагающийся на форме редактирования: к примеру, если пользователь попытается добавить новый элемент (и таким образом совершить переход с формы редактирования одного объекта на форму редактирования другого), то система спросит его, хочет ли он сохранить изменения.

Операция `CheckChanges` включает или выключает данную проверку.

{% include note.html content="Eсли данная настройка выключена, то обработка сохранения изменений возлагается на прикладного программиста.  
Для этого можно использовать [события](fa_wolv-events.html) списка, или его [JS API](fa_js-api-wolv.html)." %}

По умолчанию данная настройка включена.

## Внешний вид WOLV с включенными операциями

![](/images/pages/products/flexberry-aspnet/controls/wolv/all-operations-wolv.png)