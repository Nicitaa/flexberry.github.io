---
title: Связывание LookUp'ов в AjaxGroupEdit с внешним LookUp'ом
sidebar: flexberry-aspnet_sidebar
keywords: FAQ, Flexberry ASP-NET, How to (page)
toc: true
permalink: en/fa_change-lcs-lookup-age.html
lang: en

---

**Цель связывания LookUp'ов в AGE с внешним LookUp'ом:** [Функция ограничения](fo_limit-function.html) [LookUp'ов](fa_master-editor-ajax-lookup.html) внутри [AjaxGroupEdit](fa_ajax-group-edit.html) должна зависеть от значения во внешнем LookUp'е.

Модель:

![](/images/pages/products/flexberry-aspnet/controls/groupedit/model.png)

Код:

```csharp
/// <summary>
/// Метод изменяющий LCS в лукапах, находящихся в AGE.
/// </summary>
/// <param name="territoryKey">Ключ значения с "главного" лукапа.</param>
/// <param name="lfKey">Ключ сессии.</param>
/// <returns>Ключ сессии.</returns>
[WebMethod]
public static string CreateLf(string territoryKey, string lfKey)
{
    if (string.IsNullOrEmpty(lfKey))
    {
        lfKey = Guid.NewGuid().ToString("B");
    }

    var langdef = ExternalLangDef.LanguageDef;

    var lf = langdef.GetFunction(langdef.funcEQ,
        new VariableDef(langdef.GuidType, Information.ExtractPropertyName<Company>(x => x.Territory)),
        territoryKey);

    LimitFunctionsHolder.PersistLimitFunction(lfKey, lf);

    return lfKey;
}
```

```javascript
<script type="text/javascript">
        $(document).ready(function() {
            var lfName = '';
            var territoryKey = $('#<%=ctrlTerritory.ClientID%>').val();
            var changeLf = function() {
                $.ajax({
                    type: "POST",
                    url: window.location.pathname + "/CreateLf",
                    dataType: "json",
                    contentType: "application/json; charset=utf-8",
                    data: JSON.stringify({ territoryKey: territoryKey, lfKey: lfName }),
                    async: false, cache: false,
                    success: function(data) {
                        lfName = data.d;
                    }
                });
            }
            /**
             * Перебираем в АГЕ ctrlCompanyEmployee все лукапы ctrlCompany и проставляем им измененный limit function.
             */
            if (territoryKey) {
                changeLf();
                $('[id$=ctrlCompany]', '#<%=ctrlCompanyEmployee.ClientID%>').each(
                    function() {
                        $(this).icsMasterEditorAjaxLookup('updateOptions', { lookup: { LFName: lfName } });
                    });
            }
            /**
             * Если в "главном" лукапе ctrlTerritory поменяли значение - то переопределяем все лукапы ctrlCompany в АГЕ ctrlCompanyEmployee.
             */
            $('#<%=ctrlTerritory.ClientID%>').on('change',
                function() {
                    territoryKey = $('#<%=ctrlTerritory.ClientID%>').val();
                    changeLf();
                    $('[id$=ctrlCompany]', '#<%=ctrlCompanyEmployee.ClientID%>').each(
                        function() {
                            $(this).icsMasterEditorAjaxLookup('updateOptions', { lookup: { LFName: lfName } });
                        });
                });
            /**
             * Если добавлена новая строка в АГЕ, сразу назначим limit function.
             * @param {int} row Номер добавленной строки.
             */
            $('#<%=ctrlCompanyEmployee.ClientID%>').on('rowadded.ajaxgroupedit', function(e, d) {
                $('[id$=ctrlCompany]', d).icsMasterEditorAjaxLookup('updateOptions', { lookup: { LFName: lfName } });
            });
        });
    </script>
```
