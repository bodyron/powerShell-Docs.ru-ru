---
title: Написание модуля скрипта PowerShell | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ed7645ea-5e52-4a45-81a7-aa3c2d605cde
caps.latest.revision: 16
ms.openlocfilehash: b2a929a1724f77f0516ad24cfd90f6d6053ed19e
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72360693"
---
# <a name="how-to-write-a-powershell-script-module"></a>Как написать модуль сценария PowerShell

По сути, модуль скрипта — это любой допустимый сценарий PowerShell, сохраненный в расширении. PSM1. Это расширение позволяет подсистеме PowerShell использовать ряд правил и командлетов в файле. Большая часть этих возможностей заключается в том, чтобы помочь вам установить код в других системах, а также управлять областями. Можно также использовать файл манифеста модуля, который может описывать еще более сложные установки и решения.

## <a name="writing-a-powershell-script-module"></a>Написание модуля скрипта PowerShell

Создайте модуль скрипта, сохранив в PSM1-файле допустимый скрипт PowerShell, а затем сохранив этот файл в каталоге, где PowerShell может его найти. В этой папке можно также разместить все ресурсы, необходимые для выполнения скрипта, а также файл манифеста, который описывает, как работает ваш модуль PowerShell.

#### <a name="to-create-a-basic-powershell-module"></a>Создание базового модуля PowerShell

1. Возьмите существующий сценарий PowerShell и сохраните скрипт с расширением PSM1.

   Сохранение скрипта с расширением PSM1 означает, что на нем можно использовать командлеты модуля, такие как [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module). Эти командлеты в основном существуют, чтобы вы могли легко импортировать и экспортировать код в системы других пользователей. (Альтернативное решение — загрузить код в другие системы, а затем передать его в активную память, что не является особенно масштабируемым решением.) Дополнительные сведения см. в разделе **командлеты и переменные модуля** в [модулях Windows PowerShell](./understanding-a-windows-powershell-module.md) Обратите внимание, что по умолчанию все функции в скрипте доступны пользователям, которые импортируют файл PSM1, но свойства не являются.

   Пример скрипта PowerShell, имеющий `Show-Calendar`, доступен в конце этого раздела.

   ```powershell
   function Show-Calendar {
   param(
       [DateTime] $start = [DateTime]::Today,
       [DateTime] $end = $start,
       $firstDayOfWeek,
       [int[]] $highlightDay,
       [string[]] $highlightDate = [DateTime]::Today.ToString()
       )

       #actual code for the function goes here see the end of the topic for the complete code sample
   }
   ```

2. Чтобы управлять доступом пользователей к определенным функциям или свойствам, вызовите [Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) в конце скрипта.

   В примере кода в нижней части страницы имеется только одна функция, которая по умолчанию будет предоставляться. Однако рекомендуется явно вызывать функции, которые необходимо предоставить, как описано в следующем коде:

   ```powershell
   function Show-Calendar {
         }
   Export-ModuleMember -Function Show-Calendar
   ```

   Вы также можете ограничить импортируемые объекты с помощью манифеста модуля. Дополнительные сведения см. в статьях [Импорт модуля PowerShell](./importing-a-powershell-module.md) и [написание манифеста модуля PowerShell](./how-to-write-a-powershell-module-manifest.md).

3. Если у вас есть модули, которые должен загрузить ваш собственный модуль, их можно использовать с вызовом `Import-Module` в верхней части вашего модуля.

   `Import-Module` — это командлет, который импортирует целевой модуль на систему. Таким образом, он также используется позже в процедуре установки собственного модуля. В примере кода в нижней части этой страницы не используются модули импорта. Тем не менее, они будут перечислены в верхней части файла, как описано в следующем коде:

   ```powershell
   Import-Module GenericModule
   ```

4. Чтобы описать модуль в справочной системе PowerShell, можно либо использовать стандартные комментарии в файле справки, либо создать дополнительный файл справки.

   Пример кода в нижней части этого раздела содержит справочную информацию в комментариях. Можно также написать развернутые XML-файлы, содержащие дополнительное содержимое справки. Дополнительные сведения см. в разделе [Создание справки для модулей Windows PowerShell](./writing-help-for-windows-powershell-modules.md).

5. Если у вас есть дополнительные модули, файлы XML или другое содержимое, которое вы хотите упаковать с модулем, это можно сделать с помощью манифеста модуля.

   Манифест модуля — это файл, содержащий имена других модулей, макетов каталогов, Номера версий, данные автора и другие сведения. PowerShell использует файл манифеста модуля для Организации и развертывания решения. Однако из-за относительно простой природы этого примера файл манифеста не требовался. Дополнительные сведения см. в разделе [манифесты модулей](./how-to-write-a-powershell-module-manifest.md).

6. Чтобы установить и запустить модуль, сохраните модуль в один из соответствующих путей PowerShell и выполните вызов `Import-Module`.

   Пути, по которым можно установить модуль, находятся в глобальной переменной `$env:PSModulePath`. Например, общий путь для сохранения модуля в системе будет `%SystemRoot%/users/<user>/Documents/WindowsPowerShell/Modules/<moduleName>`. Не забудьте создать папку, в которой будет существовать модуль, даже если он является единственным PSM1-файлом. Если вы не сохранили модуль по одному из этих путей, необходимо передать расположение модуля в вызове `Import-Module`. (В противном случае PowerShell не сможет найти его.) Начиная с PowerShell 3,0, если модуль помещен в один из путей модуля PowerShell, вам не нужно явно импортировать его. Модуль автоматически загружается, когда пользователь вызывает функцию.
   Дополнительные сведения о пути к модулю см. в разделе [Импорт модуля PowerShell](./importing-a-powershell-module.md) и [переменной среды PSModulePath](./modifying-the-psmodulepath-installation-path.md).

7. Чтобы удалить модуль из активной службы, выполните вызов [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module).

   Обратите внимание, что [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) удаляет модуль из активной памяти. фактически он не удаляется из места сохранения файлов модулей.

### <a name="show-calendar-code-example"></a>Пример кода для показа календаря

В следующем примере показан простой модуль скрипта, содержащий одну функцию с именем `Show-Calendar`.
Эта функция отображает визуальное представление календаря. Кроме того, образец содержит строки справки PowerShell для кратких сведений, описания, значений параметров и, например,. Обратите внимание, что последняя строка кода гарантирует, что функция `Show-Calendar` экспортируется как элемент модуля при импорте модуля.

```powershell
<#
 .Synopsis
  Displays a visual representation of a calendar.

 .Description
  Displays a visual representation of a calendar. This function supports multiple months
  and lets you highlight specific date ranges or days.

 .Parameter Start
  The first month to display.

 .Parameter End
  The last month to display.

 .Parameter FirstDayOfWeek
  The day of the month on which the week begins.

 .Parameter HighlightDay
  Specific days (numbered) to highlight. Used for date ranges like (25..31).
  Date ranges are specified by the Windows PowerShell range syntax. These dates are
  enclosed in square brackets.

 .Parameter HighlightDate
  Specific days (named) to highlight. These dates are surrounded by asterisks.

 .Example
   # Show a default display of this month.
   Show-Calendar

 .Example
   # Display a date range.
   Show-Calendar -Start "March, 2010" -End "May, 2010"

 .Example
   # Highlight a range of days.
   Show-Calendar -HighlightDay (1..10 + 22) -HighlightDate "December 25, 2008"
#>
function Show-Calendar {
param(
    [DateTime] $start = [DateTime]::Today,
    [DateTime] $end = $start,
    $firstDayOfWeek,
    [int[]] $highlightDay,
    [string[]] $highlightDate = [DateTime]::Today.ToString()
    )

## Determine the first day of the start and end months.
$start = New-Object DateTime $start.Year,$start.Month,1
$end = New-Object DateTime $end.Year,$end.Month,1

## Convert the highlighted dates into real dates.
[DateTime[]] $highlightDate = [DateTime[]] $highlightDate

## Retrieve the DateTimeFormat information so that the
## calendar can be manipulated.
$dateTimeFormat  = (Get-Culture).DateTimeFormat
if($firstDayOfWeek)
{
    $dateTimeFormat.FirstDayOfWeek = $firstDayOfWeek
}

$currentDay = $start

## Process the requested months.
while($start -le $end)
{
    ## Return to an earlier point in the function if the first day of the month
    ## is in the middle of the week.
    while($currentDay.DayOfWeek -ne $dateTimeFormat.FirstDayOfWeek)
    {
        $currentDay = $currentDay.AddDays(-1)
    }

    ## Prepare to store information about this date range.
    $currentWeek = New-Object PsObject
    $dayNames = @()
    $weeks = @()

    ## Continue processing dates until the function reaches the end of the month.
    ## The function continues until the week is completed with
    ## days from the next month.
    while(($currentDay -lt $start.AddMonths(1)) -or
        ($currentDay.DayOfWeek -ne $dateTimeFormat.FirstDayOfWeek))
    {
        ## Determine the day names to use to label the columns.
        $dayName = "{0:ddd}" -f $currentDay
        if($dayNames -notcontains $dayName)
        {
            $dayNames += $dayName
        }

        ## Pad the day number for display, highlighting if necessary.
        $displayDay = " {0,2} " -f $currentDay.Day

        ## Determine whether to highlight a specific date.
        if($highlightDate)
        {
            $compareDate = New-Object DateTime $currentDay.Year,
                $currentDay.Month,$currentDay.Day
            if($highlightDate -contains $compareDate)
            {
                $displayDay = "*" + ("{0,2}" -f $currentDay.Day) + "*"
            }
        }

        ## Otherwise, highlight as part of a date range.
        if($highlightDay -and ($highlightDay[0] -eq $currentDay.Day))
        {
            $displayDay = "[" + ("{0,2}" -f $currentDay.Day) + "]"
            $null,$highlightDay = $highlightDay
        }

        ## Add the day of the week and the day of the month as note properties.
        $currentWeek | Add-Member NoteProperty $dayName $displayDay

        ## Move to the next day of the month.
        $currentDay = $currentDay.AddDays(1)

        ## If the function reaches the next week, store the current week
        ## in the week list and continue.
        if($currentDay.DayOfWeek -eq $dateTimeFormat.FirstDayOfWeek)
        {
            $weeks += $currentWeek
            $currentWeek = New-Object PsObject
        }
    }

    ## Format the weeks as a table.
    $calendar = $weeks | Format-Table $dayNames -AutoSize | Out-String

    ## Add a centered header.
    $width = ($calendar.Split("`n") | Measure-Object -Maximum Length).Maximum
    $header = "{0:MMMM yyyy}" -f $start
    $padding = " " * (($width - $header.Length) / 2)
    $displayCalendar = " `n" + $padding + $header + "`n " + $calendar
    $displayCalendar.TrimEnd()

    ## Move to the next month.
    $start = $start.AddMonths(1)

}
}
Export-ModuleMember -Function Show-Calendar
```