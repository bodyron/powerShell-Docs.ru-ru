---
ms.date: 3/18/2019
title: Создание запросов Get-WinEvent с помощью FilterHashtable
ms.openlocfilehash: fae01cc8be5c1805e2aae008e1f21ed387efa325
ms.sourcegitcommit: 396509cd0d415acc306b68758b6f833406e26bf5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/21/2019
ms.locfileid: "58320459"
---
# <a name="creating-get-winevent-queries-with-filterhashtable"></a><span data-ttu-id="5216a-102">Создание запросов Get-WinEvent с помощью FilterHashtable</span><span class="sxs-lookup"><span data-stu-id="5216a-102">Creating Get-WinEvent queries with FilterHashtable</span></span>

<span data-ttu-id="5216a-103">Чтобы прочитать исходную запись блога **специалистов по сценариям** от 3 июня 2014 г., которая называется Use FilterHashTable to Filter Event Log with PowerShell (Использование FilterHashTable для фильтрации журнала событий с помощью PowerShell), перейдите [сюда](https://devblogs.microsoft.com/scripting/use-filterhashtable-to-filter-event-log-with-powershell/).</span><span class="sxs-lookup"><span data-stu-id="5216a-103">To read the original June 3, 2014 **Scripting Guy** blog post, see [Use FilterHashTable to Filter Event Log with PowerShell](https://devblogs.microsoft.com/scripting/use-filterhashtable-to-filter-event-log-with-powershell/).</span></span>

<span data-ttu-id="5216a-104">Эта статья является выдержкой из исходной записи блога. Здесь показано, как использовать параметр **FilterHashtable** командлета `Get-WinEvent` для фильтрации журналов событий.</span><span class="sxs-lookup"><span data-stu-id="5216a-104">This article is an excerpt of the original blog post and explains how to use the `Get-WinEvent` cmdlet's **FilterHashtable** parameter to filter event logs.</span></span> <span data-ttu-id="5216a-105">Использование командлета `Get-WinEvent` PowerShell представляет собой эффективный метод для фильтрации журналов событий и журналов диагностики Windows.</span><span class="sxs-lookup"><span data-stu-id="5216a-105">PowerShell's `Get-WinEvent` cmdlet is a powerful method to filter Windows event and diagnostic logs.</span></span> <span data-ttu-id="5216a-106">Если в запросе `Get-WinEvent` используется параметр **FilterHashtable**, производительность будет более высокой.</span><span class="sxs-lookup"><span data-stu-id="5216a-106">Performance improves when a `Get-WinEvent` query uses the **FilterHashtable** parameter.</span></span>

<span data-ttu-id="5216a-107">При работе с объемными журналами событий отправка объектов по конвейеру команде `Where-Object` не является эффективной.</span><span class="sxs-lookup"><span data-stu-id="5216a-107">When you work with large event logs, it's not efficient to send objects down the pipeline to a `Where-Object` command.</span></span> <span data-ttu-id="5216a-108">До выхода версии PowerShell 6 для получения данных журнала также использовался командлет `Get-EventLog`.</span><span class="sxs-lookup"><span data-stu-id="5216a-108">Prior to PowerShell 6, the `Get-EventLog` cmdlet was another option to get log data.</span></span> <span data-ttu-id="5216a-109">Например, приведенные ниже команды являются неэффективными для фильтрации журналов **Microsoft-Windows-Defrag**:</span><span class="sxs-lookup"><span data-stu-id="5216a-109">For example, the following commands are inefficient to filter the **Microsoft-Windows-Defrag** logs:</span></span>

`Get-EventLog -LogName Application | Where-Object Source -Match defrag`

`Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'defrag' }`

<span data-ttu-id="5216a-110">В следующей команде используется хэш-таблица, что повышает производительность:</span><span class="sxs-lookup"><span data-stu-id="5216a-110">The following command uses a hash table that improves the performance:</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='*defrag'
}
```

### <a name="blog-posts-about-enumeration"></a><span data-ttu-id="5216a-111">Записи блога, посвященные перечислению</span><span class="sxs-lookup"><span data-stu-id="5216a-111">Blog posts about enumeration</span></span>

<span data-ttu-id="5216a-112">В этой статье представлены сведения о том, как использовать перечисляемые значения в хэш-таблице.</span><span class="sxs-lookup"><span data-stu-id="5216a-112">This article presents information about how to use enumerated values in a hash table.</span></span> <span data-ttu-id="5216a-113">Дополнительные сведения о перечислении см. в записях блога **специалистов по сценариям**.</span><span class="sxs-lookup"><span data-stu-id="5216a-113">For more information about enumeration, read these **Scripting Guy** blog posts.</span></span> <span data-ttu-id="5216a-114">Сведения для создания функции, возвращающей перечисляемые значения, см. в [этой записи блога](https://devblogs.microsoft.com/scripting/hey-scripting-guy-weekend-scripter-enumerations-and-values).</span><span class="sxs-lookup"><span data-stu-id="5216a-114">To create a function that returns the enumerated values, see [Enumerations and Values](https://devblogs.microsoft.com/scripting/hey-scripting-guy-weekend-scripter-enumerations-and-values).</span></span>
<span data-ttu-id="5216a-115">Дополнительные сведения см. в [ряде записей блога специалистов по сценариям, посвященных перечислению](https://devblogs.microsoft.com/scripting/?s=about+enumeration).</span><span class="sxs-lookup"><span data-stu-id="5216a-115">For more information, see the [Scripting Guy series of blog posts about enumeration](https://devblogs.microsoft.com/scripting/?s=about+enumeration).</span></span>

### <a name="hash-table-keyvalue-pairs"></a><span data-ttu-id="5216a-116">Пары "ключ — значение" в хэш-таблице</span><span class="sxs-lookup"><span data-stu-id="5216a-116">Hash table key/value pairs</span></span>

<span data-ttu-id="5216a-117">Для создания эффективных запросов используйте командлет `Get-WinEvent` с параметром **FilterHashtable**.</span><span class="sxs-lookup"><span data-stu-id="5216a-117">To build efficient queries, use the `Get-WinEvent` cmdlet with the **FilterHashtable** parameter.</span></span>
<span data-ttu-id="5216a-118">**FilterHashtable** принимает хэш-таблицу в качестве фильтра для получения конкретных сведений из журналов событий Windows.</span><span class="sxs-lookup"><span data-stu-id="5216a-118">**FilterHashtable** accepts a hash table as a filter to get specific information from Windows event logs.</span></span> <span data-ttu-id="5216a-119">Хэш-таблица использует пары **ключ — значение**.</span><span class="sxs-lookup"><span data-stu-id="5216a-119">A hash table uses **key/value** pairs.</span></span> <span data-ttu-id="5216a-120">Дополнительные сведения о хэш-таблицах см. [здесь](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span><span class="sxs-lookup"><span data-stu-id="5216a-120">For more information about hash tables, see [about_Hash_Tables](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span></span>

<span data-ttu-id="5216a-121">Если пары **ключ — значение** находятся в одной строке, они должны быть разделены точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="5216a-121">If the **key/value** pairs are on the same line, they must be separated by a semicolon.</span></span> <span data-ttu-id="5216a-122">Если пара **ключ — значение** находится в отдельной строке, точка с запятой не требуется.</span><span class="sxs-lookup"><span data-stu-id="5216a-122">If each **key/value** pair is on a separate line, the semicolon isn't needed.</span></span> <span data-ttu-id="5216a-123">Например, в этой статье пары **ключ — значение** помещаются в отдельных строках и не содержат точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="5216a-123">For example, this article places **key/value** pairs on separate lines and doesn't use semicolons.</span></span>

<span data-ttu-id="5216a-124">В этом примере используется несколько пар **ключ — значение** для параметра **FilterHashtable**.</span><span class="sxs-lookup"><span data-stu-id="5216a-124">This sample uses several of the **FilterHashtable** parameter's **key/value** pairs.</span></span> <span data-ttu-id="5216a-125">Готовый запрос включает в себя значения **LogName**, **ProviderName**, **Keywords**, **ID** и **Level**.</span><span class="sxs-lookup"><span data-stu-id="5216a-125">The completed query includes **LogName**, **ProviderName**, **Keywords**, **ID**, and **Level**.</span></span>

<span data-ttu-id="5216a-126">Допустимые пары **ключ — значение** показаны в следующей таблице и включены в документацию для параметра **FilterHashtable**
командлета [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent).</span><span class="sxs-lookup"><span data-stu-id="5216a-126">The accepted **key/value** pairs are shown in the following table and are included in the documentation for the [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent)
**FilterHashtable** parameter.</span></span>

<span data-ttu-id="5216a-127">В следующей таблице приведены имена ключей, типы данных и сведения о том, принимаются ли подстановочные знаки для значения данных.</span><span class="sxs-lookup"><span data-stu-id="5216a-127">The following table displays the key names, data types, and whether wildcard characters are accepted for a data value.</span></span>

| <span data-ttu-id="5216a-128">Имя ключа</span><span class="sxs-lookup"><span data-stu-id="5216a-128">Key name</span></span>     | <span data-ttu-id="5216a-129">Тип данных значения</span><span class="sxs-lookup"><span data-stu-id="5216a-129">Value data type</span></span>    | <span data-ttu-id="5216a-130">Принимает ли подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5216a-130">Accepts wildcard characters?</span></span> |
|------------- | ------------------ | ---------------------------- |
| <span data-ttu-id="5216a-131">LogName</span><span class="sxs-lookup"><span data-stu-id="5216a-131">LogName</span></span>      | `<String[]>`       | <span data-ttu-id="5216a-132">Да</span><span class="sxs-lookup"><span data-stu-id="5216a-132">Yes</span></span> |
| <span data-ttu-id="5216a-133">ProviderName</span><span class="sxs-lookup"><span data-stu-id="5216a-133">ProviderName</span></span> | `<String[]>`       | <span data-ttu-id="5216a-134">Да</span><span class="sxs-lookup"><span data-stu-id="5216a-134">Yes</span></span> |
| <span data-ttu-id="5216a-135">путь</span><span class="sxs-lookup"><span data-stu-id="5216a-135">Path</span></span>         | `<String[]>`       | <span data-ttu-id="5216a-136">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-136">No</span></span>  |
| <span data-ttu-id="5216a-137">Ключевые слова</span><span class="sxs-lookup"><span data-stu-id="5216a-137">Keywords</span></span>     | `<Long[]>`         | <span data-ttu-id="5216a-138">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-138">No</span></span>  |
| <span data-ttu-id="5216a-139">Код</span><span class="sxs-lookup"><span data-stu-id="5216a-139">ID</span></span>           | `<Int32[]>`        | <span data-ttu-id="5216a-140">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-140">No</span></span>  |
| <span data-ttu-id="5216a-141">Уровень</span><span class="sxs-lookup"><span data-stu-id="5216a-141">Level</span></span>        | `<Int32[]>`        | <span data-ttu-id="5216a-142">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-142">No</span></span>  |
| <span data-ttu-id="5216a-143">StartTime</span><span class="sxs-lookup"><span data-stu-id="5216a-143">StartTime</span></span>    | `<DateTime>`       | <span data-ttu-id="5216a-144">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-144">No</span></span>  |
| <span data-ttu-id="5216a-145">EndTime</span><span class="sxs-lookup"><span data-stu-id="5216a-145">EndTime</span></span>      | `<DateTime>`       | <span data-ttu-id="5216a-146">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-146">No</span></span>  |
| <span data-ttu-id="5216a-147">UserID</span><span class="sxs-lookup"><span data-stu-id="5216a-147">UserID</span></span>       | `<SID>`            | <span data-ttu-id="5216a-148">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-148">No</span></span>  |
| <span data-ttu-id="5216a-149">Данные</span><span class="sxs-lookup"><span data-stu-id="5216a-149">Data</span></span>         | `<String[]>`       | <span data-ttu-id="5216a-150">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-150">No</span></span>  |
| *            | `<String[]>`       | <span data-ttu-id="5216a-151">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-151">No</span></span>  |

### <a name="building-a-query-with-a-hash-table"></a><span data-ttu-id="5216a-152">Создание запроса с использованием хэш-таблицы</span><span class="sxs-lookup"><span data-stu-id="5216a-152">Building a query with a hash table</span></span>

<span data-ttu-id="5216a-153">Для проверки результатов и устранения проблем полезно создавать одну пару **ключ — значение** для хэш-таблицы за раз.</span><span class="sxs-lookup"><span data-stu-id="5216a-153">To verify results and troubleshoot problems, it helps to build the hash table one **key/value** pair at a time.</span></span> <span data-ttu-id="5216a-154">Запрос получает данные из журнала **Application**.</span><span class="sxs-lookup"><span data-stu-id="5216a-154">The query gets data from the **Application** log.</span></span> <span data-ttu-id="5216a-155">Хэш-таблица создается в результате запроса `Get-WinEvent –LogName Application`.</span><span class="sxs-lookup"><span data-stu-id="5216a-155">The hash table is equivalent to `Get-WinEvent –LogName Application`.</span></span>

<span data-ttu-id="5216a-156">Для начала создайте запрос `Get-WinEvent`.</span><span class="sxs-lookup"><span data-stu-id="5216a-156">To begin, create the `Get-WinEvent` query.</span></span> <span data-ttu-id="5216a-157">Используйте пару **ключ — значение** параметра **FilterHashtable** с ключом **LogName** и его значением — **Application**.</span><span class="sxs-lookup"><span data-stu-id="5216a-157">Use the **FilterHashtable** parameter's **key/value** pair with the key, **LogName**, and the value, **Application**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
}
```

<span data-ttu-id="5216a-158">Продолжайте выполнять сборку хэш-таблицы с использованием ключа **ProviderName**.</span><span class="sxs-lookup"><span data-stu-id="5216a-158">Continue to build the hash table with the **ProviderName** key.</span></span> <span data-ttu-id="5216a-159">**ProviderName** — это имя, отображаемое в поле **источника** в средстве **Просмотра событий Windows**.</span><span class="sxs-lookup"><span data-stu-id="5216a-159">The **ProviderName** is the name that appears in the **Source** field in the **Windows Event Viewer**.</span></span> <span data-ttu-id="5216a-160">Например, **среда выполнения .NET** на следующем снимке экрана:</span><span class="sxs-lookup"><span data-stu-id="5216a-160">For example, **.NET Runtime** in the following screenshot:</span></span>

![Изображение источников в средстве "Просмотр событий Windows".](./media/creating-get-winEvent-queries-with-filterhashtable/providername.png)

<span data-ttu-id="5216a-162">Обновите хэш-таблицу и добавьте пару **ключ — значение** с ключом \*\*ProviderName и его значением — **.NET Runtime**.</span><span class="sxs-lookup"><span data-stu-id="5216a-162">Update the hash table and include the **key/value** pair with the key, \*\*ProviderName, and the value, **.NET Runtime**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
}
```

<span data-ttu-id="5216a-163">Если запрос должен получить данные из архивных журналов событий, используйте ключ **Path**.</span><span class="sxs-lookup"><span data-stu-id="5216a-163">If your query needs to get data from archived event logs, use the **Path** key.</span></span> <span data-ttu-id="5216a-164">Значение **Path** указывает полный путь к файлу журнала.</span><span class="sxs-lookup"><span data-stu-id="5216a-164">The **Path** value specifies the full path to the log file.</span></span> <span data-ttu-id="5216a-165">Дополнительные сведения см. в записи блога **специалистов по сценариям** [Use PowerShell to Parse Saved Event Logs for Errors](https://devblogs.microsoft.com/scripting/use-powershell-to-parse-saved-event-logs-for-errors) (Анализ сохраненных журналов событий на наличие ошибок с помощью PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5216a-165">For more information, see the **Scripting Guy** blog post, [Use PowerShell to Parse Saved Event Logs for Errors](https://devblogs.microsoft.com/scripting/use-powershell-to-parse-saved-event-logs-for-errors).</span></span>

### <a name="using-enumerated-values-in-a-hash-table"></a><span data-ttu-id="5216a-166">Использование перечисляемых значений в хэш-таблице</span><span class="sxs-lookup"><span data-stu-id="5216a-166">Using enumerated values in a hash table</span></span>

<span data-ttu-id="5216a-167">**Keywords** — следующий ключ в хэш-таблице.</span><span class="sxs-lookup"><span data-stu-id="5216a-167">**Keywords** is the next key in the hash table.</span></span> <span data-ttu-id="5216a-168">Тип данных **Keywords** представляет собой массив типа значения `[long]`, который содержит большое число.</span><span class="sxs-lookup"><span data-stu-id="5216a-168">The **Keywords** data type is an array of the `[long]` value type that holds a large number.</span></span> <span data-ttu-id="5216a-169">Используйте следующую команду, чтобы найти максимальное значение `[long]`:</span><span class="sxs-lookup"><span data-stu-id="5216a-169">Use the following command to find the maximum value of `[long]`:</span></span>

```powershell
[long]::MaxValue
```

```Output
9223372036854775807
```

<span data-ttu-id="5216a-170">Для ключа **Keywords** PowerShell использует число, а не строку, такую как **Security**.</span><span class="sxs-lookup"><span data-stu-id="5216a-170">For the **Keywords** key, PowerShell uses a number, not a string such as **Security**.</span></span> <span data-ttu-id="5216a-171">В средстве **Просмотр событий Windows** значения **Keywords** отображаются в виде строк, но они являются перечисляемыми значениями.</span><span class="sxs-lookup"><span data-stu-id="5216a-171">**Windows Event Viewer** displays the **Keywords** as strings, but they are enumerated values.</span></span> <span data-ttu-id="5216a-172">Если вы используете ключ **Keywords** со строковым значением, в хэш-таблице отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5216a-172">In the hash table, if you use the **Keywords** key with a string value, an error message is displayed.</span></span>

<span data-ttu-id="5216a-173">Откройте средство **Просмотр событий Windows** и в окне **Действия** щелкните **Фильтровать текущий журнал**.</span><span class="sxs-lookup"><span data-stu-id="5216a-173">Open the **Windows Event Viewer** and from the **Actions** pane, click on **Filter current log**.</span></span>
<span data-ttu-id="5216a-174">В раскрывающемся меню **Ключевые слова** отображаются доступные ключевые слова, как показано на следующем снимке экрана:</span><span class="sxs-lookup"><span data-stu-id="5216a-174">The **Keywords** drop-down menu displays the available keywords, as shown in the following screenshot:</span></span>

![Изображение ключевых слов средства "Просмотр событий Windows".](./media/creating-get-winEvent-queries-with-filterhashtable/keywords.png)

<span data-ttu-id="5216a-176">Используйте следующую команду для отображения имен свойств `StandardEventKeywords`.</span><span class="sxs-lookup"><span data-stu-id="5216a-176">Use the following command to display the `StandardEventKeywords` property names.</span></span>

```powershell
[System.Diagnostics.Eventing.Reader.StandardEventKeywords] | Get-Member -Static -MemberType Property
```

```Output
   TypeName: System.Diagnostics.Eventing.Reader.StandardEventKeywords
Name             MemberType Definition
—-             ———- ———-
AuditFailure     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
AuditSuccess     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
CorrelationHint  Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
CorrelationHint2 Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
EventLogClassic  Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
None             Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
ResponseTime     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
Sqm              Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
WdiContext       Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
WdiDiagnostic    Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
```

<span data-ttu-id="5216a-177">Перечисляемые значения описаны в **.NET Framework**.</span><span class="sxs-lookup"><span data-stu-id="5216a-177">The enumerated values are documented in the **.NET Framework**.</span></span> <span data-ttu-id="5216a-178">Дополнительные сведения см. в разделе о команде перечисления [StandardEventKeywords](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventkeywords?redirectedfrom=MSDN&view=netframework-4.7.2).</span><span class="sxs-lookup"><span data-stu-id="5216a-178">For more information, see [StandardEventKeywords Enumeration](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventkeywords?redirectedfrom=MSDN&view=netframework-4.7.2).</span></span>

<span data-ttu-id="5216a-179">Имена **ключевых слов** и перечисляемые значения выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5216a-179">The **Keywords** names and enumerated values are as follows:</span></span>

| <span data-ttu-id="5216a-180">Name</span><span class="sxs-lookup"><span data-stu-id="5216a-180">Name</span></span>             |  <span data-ttu-id="5216a-181">Значение</span><span class="sxs-lookup"><span data-stu-id="5216a-181">Value</span></span>            |
| ---------------- | ------------------|
| <span data-ttu-id="5216a-182">AuditFailure</span><span class="sxs-lookup"><span data-stu-id="5216a-182">AuditFailure</span></span>     | <span data-ttu-id="5216a-183">4503599627370496</span><span class="sxs-lookup"><span data-stu-id="5216a-183">4503599627370496</span></span>  |
| <span data-ttu-id="5216a-184">AuditSuccess</span><span class="sxs-lookup"><span data-stu-id="5216a-184">AuditSuccess</span></span>     | <span data-ttu-id="5216a-185">9007199254740992</span><span class="sxs-lookup"><span data-stu-id="5216a-185">9007199254740992</span></span>  |
| <span data-ttu-id="5216a-186">CorrelationHint2</span><span class="sxs-lookup"><span data-stu-id="5216a-186">CorrelationHint2</span></span> | <span data-ttu-id="5216a-187">18014398509481984</span><span class="sxs-lookup"><span data-stu-id="5216a-187">18014398509481984</span></span> |
| <span data-ttu-id="5216a-188">EventLogClassic</span><span class="sxs-lookup"><span data-stu-id="5216a-188">EventLogClassic</span></span>  | <span data-ttu-id="5216a-189">36028797018963968</span><span class="sxs-lookup"><span data-stu-id="5216a-189">36028797018963968</span></span> |
| <span data-ttu-id="5216a-190">Sqm</span><span class="sxs-lookup"><span data-stu-id="5216a-190">Sqm</span></span>              | <span data-ttu-id="5216a-191">2251799813685248</span><span class="sxs-lookup"><span data-stu-id="5216a-191">2251799813685248</span></span>  |
| <span data-ttu-id="5216a-192">WdiDiagnostic</span><span class="sxs-lookup"><span data-stu-id="5216a-192">WdiDiagnostic</span></span>    | <span data-ttu-id="5216a-193">1125899906842624</span><span class="sxs-lookup"><span data-stu-id="5216a-193">1125899906842624</span></span>  |
| <span data-ttu-id="5216a-194">WdiContext</span><span class="sxs-lookup"><span data-stu-id="5216a-194">WdiContext</span></span>       | <span data-ttu-id="5216a-195">562949953421312</span><span class="sxs-lookup"><span data-stu-id="5216a-195">562949953421312</span></span>   |
| <span data-ttu-id="5216a-196">ResponseTime</span><span class="sxs-lookup"><span data-stu-id="5216a-196">ResponseTime</span></span>     | <span data-ttu-id="5216a-197">281474976710656</span><span class="sxs-lookup"><span data-stu-id="5216a-197">281474976710656</span></span>   |
| <span data-ttu-id="5216a-198">Нет</span><span class="sxs-lookup"><span data-stu-id="5216a-198">None</span></span>             | <span data-ttu-id="5216a-199">0</span><span class="sxs-lookup"><span data-stu-id="5216a-199">0</span></span>                 |

<span data-ttu-id="5216a-200">Обновите хэш-таблицу и добавьте пару **ключ — значение** с ключом **Keywords** и значением перечисления **EventLogClassic** — **36028797018963968** .</span><span class="sxs-lookup"><span data-stu-id="5216a-200">Update the hash table and include the **key/value** pair with the key, **Keywords**, and the **EventLogClassic** enumeration value, **36028797018963968**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
}
```

#### <a name="keywords-static-property-value-optional"></a><span data-ttu-id="5216a-201">Значение статического свойства Keywords (необязательно)</span><span class="sxs-lookup"><span data-stu-id="5216a-201">Keywords static property value (optional)</span></span>

<span data-ttu-id="5216a-202">Значение ключа **Keywords** перечисляется, но имя статического свойства можно использовать в запросе с хэш-таблицей.</span><span class="sxs-lookup"><span data-stu-id="5216a-202">The **Keywords** key is enumerated, but you can use a static property name in the hash table query.</span></span>
<span data-ttu-id="5216a-203">Вместо того чтобы использовать возвращаемую строку, имя свойства должно преобразовываться в значение с применением свойства **Value__**.</span><span class="sxs-lookup"><span data-stu-id="5216a-203">Rather than using the returned string, the property name must be converted to a value with the **Value__** property.</span></span>

<span data-ttu-id="5216a-204">Например, следующий скрипт использует свойство **Value__**.</span><span class="sxs-lookup"><span data-stu-id="5216a-204">For example, the following script uses the **Value__** property.</span></span>

```powershell
$C = [System.Diagnostics.Eventing.Reader.StandardEventKeywords]::EventLogClassic
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=$C.Value__
}
```

### <a name="filtering-by-event-id"></a><span data-ttu-id="5216a-205">Фильтрация по идентификатору события</span><span class="sxs-lookup"><span data-stu-id="5216a-205">Filtering by Event Id</span></span>

<span data-ttu-id="5216a-206">Для получения более конкретных данных результаты запроса можно отфильтровать по **идентификатору события**. **Идентификатор события** указывается в хэш-таблице как ключ **ID**, а значение соответствует конкретному **идентификатору события**. В средстве **Просмотр событий Windows** отображается **идентификатор события**. В этом примере используется **идентификатор события 1023**.</span><span class="sxs-lookup"><span data-stu-id="5216a-206">To get more specific data, the query's results are filtered by **Event Id**. The **Event Id** is referenced in the hash table as the key **ID** and the value is a specific **Event Id**. The **Windows Event Viewer** displays the **Event Id**. This example uses **Event Id 1023**.</span></span>

<span data-ttu-id="5216a-207">Обновите хэш-таблицу и добавьте пару **ключ — значение** с ключом **ID** и его значением — **1023**.</span><span class="sxs-lookup"><span data-stu-id="5216a-207">Update the hash table and include the **key/value** pair with the key, **ID** and the value, **1023**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
}
```

### <a name="filtering-by-level"></a><span data-ttu-id="5216a-208">Фильтрация по уровню</span><span class="sxs-lookup"><span data-stu-id="5216a-208">Filtering by Level</span></span>

<span data-ttu-id="5216a-209">Чтобы дополнительно уточнить результаты и включить только события, которые являются ошибками, используйте ключ **Level**.</span><span class="sxs-lookup"><span data-stu-id="5216a-209">To further refine the results and include only events that are errors, use the **Level** key.</span></span>
<span data-ttu-id="5216a-210">В средстве **Просмотр событий Windows** значения **Level** отображаются в виде строковых значений, но они являются перечисляемыми значениями.</span><span class="sxs-lookup"><span data-stu-id="5216a-210">**Windows Event Viewer** displays the **Level** as string values, but they are enumerated values.</span></span> <span data-ttu-id="5216a-211">Если вы используете ключ **Level** со строковым значением, в хэш-таблице отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="5216a-211">In the hash table, if you use the **Level** key with a string value, an error message is displayed.</span></span>

<span data-ttu-id="5216a-212">У ключа **Level** есть такие значения, как **Error** (Ошибка), **Warning** (Предупреждение) или **Informational** (Информация).</span><span class="sxs-lookup"><span data-stu-id="5216a-212">**Level** has values such as **Error**, **Warning**, or **Informational**.</span></span> <span data-ttu-id="5216a-213">Используйте следующую команду для отображения имен свойств `StandardEventLevel`.</span><span class="sxs-lookup"><span data-stu-id="5216a-213">Use the following command to display the `StandardEventLevel` property names.</span></span>

```powershell
[System.Diagnostics.Eventing.Reader.StandardEventLevel] | Get-Member -Static -MemberType Property
```

```Output
   TypeName: System.Diagnostics.Eventing.Reader.StandardEventLevel

Name          MemberType Definition
----          ---------- ----------
Critical      Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Critical {get;}
Error         Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Error {get;}
Informational Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Informational {get;}
LogAlways     Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel LogAlways {get;}
Verbose       Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Verbose {get;}
Warning       Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Warning {get;}
```

<span data-ttu-id="5216a-214">Перечисляемые значения описаны в **.NET Framework**.</span><span class="sxs-lookup"><span data-stu-id="5216a-214">The enumerated values are documented in the **.NET Framework**.</span></span> <span data-ttu-id="5216a-215">Дополнительные сведения см. в разделе о команде перечисления [StandardEventLevel](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventlevel?redirectedfrom=MSDN&view=netframework-4.7.2).</span><span class="sxs-lookup"><span data-stu-id="5216a-215">For more information, see [StandardEventLevel Enumeration](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventlevel?redirectedfrom=MSDN&view=netframework-4.7.2).</span></span>

<span data-ttu-id="5216a-216">Имена ключа **Level** и перечисляемые значения выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5216a-216">The **Level** key's names and enumerated values are as follows:</span></span>

| <span data-ttu-id="5216a-217">Name</span><span class="sxs-lookup"><span data-stu-id="5216a-217">Name</span></span>           | <span data-ttu-id="5216a-218">Значение</span><span class="sxs-lookup"><span data-stu-id="5216a-218">Value</span></span> |
| -------------- | ----- |
| <span data-ttu-id="5216a-219">Verbose</span><span class="sxs-lookup"><span data-stu-id="5216a-219">Verbose</span></span>        |   <span data-ttu-id="5216a-220">5</span><span class="sxs-lookup"><span data-stu-id="5216a-220">5</span></span>   |
| <span data-ttu-id="5216a-221">Сведения</span><span class="sxs-lookup"><span data-stu-id="5216a-221">Informational</span></span>  |   <span data-ttu-id="5216a-222">4</span><span class="sxs-lookup"><span data-stu-id="5216a-222">4</span></span>   |
| <span data-ttu-id="5216a-223">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="5216a-223">Warning</span></span>        |   <span data-ttu-id="5216a-224">3</span><span class="sxs-lookup"><span data-stu-id="5216a-224">3</span></span>   |
| <span data-ttu-id="5216a-225">Ошибка</span><span class="sxs-lookup"><span data-stu-id="5216a-225">Error</span></span>          |   <span data-ttu-id="5216a-226">2</span><span class="sxs-lookup"><span data-stu-id="5216a-226">2</span></span>   |
| <span data-ttu-id="5216a-227">Критическое</span><span class="sxs-lookup"><span data-stu-id="5216a-227">Critical</span></span>       |   <span data-ttu-id="5216a-228">1</span><span class="sxs-lookup"><span data-stu-id="5216a-228">1</span></span>   |
| <span data-ttu-id="5216a-229">LogAlways</span><span class="sxs-lookup"><span data-stu-id="5216a-229">LogAlways</span></span>      |   <span data-ttu-id="5216a-230">0</span><span class="sxs-lookup"><span data-stu-id="5216a-230">0</span></span>   |

<span data-ttu-id="5216a-231">Хэш-таблица для готового запроса содержит ключ **Level** и его значение — **2**.</span><span class="sxs-lookup"><span data-stu-id="5216a-231">The hash table for the completed query includes the key, **Level**, and the value, **2**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
   Level=2
}
```

#### <a name="level-static-property-in-enumeration-optional"></a><span data-ttu-id="5216a-232">Статическое свойство уровня в перечислении (необязательно)</span><span class="sxs-lookup"><span data-stu-id="5216a-232">Level static property in enumeration (optional)</span></span>

<span data-ttu-id="5216a-233">Значение ключа **Level** перечисляется, но имя статического свойства можно использовать в запросе к хэш-таблице.</span><span class="sxs-lookup"><span data-stu-id="5216a-233">The **Level** key is enumerated, but you can use a static property name in the hash table query.</span></span>
<span data-ttu-id="5216a-234">Вместо того чтобы использовать возвращаемую строку, имя свойства должно преобразовываться в значение с применением свойства **Value__**.</span><span class="sxs-lookup"><span data-stu-id="5216a-234">Rather than using the returned string, the property name must be converted to a value with the **Value__** property.</span></span>

<span data-ttu-id="5216a-235">Например, следующий скрипт использует свойство **Value__**.</span><span class="sxs-lookup"><span data-stu-id="5216a-235">For example, the following script uses the **Value__** property.</span></span>

```powershell
$C = [System.Diagnostics.Eventing.Reader.StandardEventLevel]::Informational
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
   Level=$C.Value__
}
```