---
title: AccessDBProviderSample04 | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ee3a7e56-7331-4f71-9ecb-7a59b8021c68
caps.latest.revision: 10
ms.openlocfilehash: 0d3133c75d8e608967f15ffb7345fc0f63e1cd5c
ms.sourcegitcommit: 7f2479edd329dfdc55726afff7019d45e45f9156
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80977511"
---
# <a name="accessdbprovidersample04"></a>AccessDBProviderSample04

В этом примере показано, как перезаписать методы контейнера для поддержки вызовов командлетов `Copy-Item`, `Get-ChildItem`, `New-Item`и `Remove-Item`. Эти методы должны быть реализованы, когда хранилище данных содержит элементы, являющиеся контейнерами. Контейнер — это группа дочерних элементов в составе общего родительского элемента. Класс поставщика в этом примере является производным от класса [System. Management. Automation. Provider. контаинеркмдлетпровидер](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) .

## <a name="demonstrates"></a>Что демонстрирует

> [!IMPORTANT]
> Скорее всего, класс поставщика будет производным от класса [System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

В этом образце демонстрируется следующее.

- Объявление атрибута `CmdletProvider`.
- Определение класса поставщика, производного от класса [System. Management. Automation. Provider. контаинеркмдлетпровидер](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) .
- Перезапись метода [System. Management. Automation. Provider. контаинеркмдлетпровидер. CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) для изменения поведения командлета `Copy-Item`, позволяющего пользователю копировать элементы из одного расположения в другое. (В этом примере не показано, как добавлять динамические параметры в командлет `Copy-Item`.)
- Перезапись метода [System. Management. Automation. Provider. контаинеркмдлетпровидер. жетчилдитемс *](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) для изменения поведения командлета Get-чилдитемс, который позволяет пользователю получить дочерние элементы родительского элемента. (В этом примере не показано, как добавлять динамические параметры в командлет Get-Чилдитемс.)
- Перезапись метода [System. Management. Automation. Provider. контаинеркмдлетпровидер. жетчилднамес *](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) для изменения поведения командлета Get-чилдитемс при указании параметра `Name` командлета.
- Перезапись метода [System. Management. Automation. Provider. контаинеркмдлетпровидер. newItem *](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) для изменения поведения командлета `New-Item`, который позволяет пользователю добавлять элементы в хранилище данных. (В этом примере не показано, как добавлять динамические параметры в командлет `New-Item`.)
- Перезапись метода [System. Management. Automation. Provider. контаинеркмдлетпровидер. RemoveItem *](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) для изменения поведения командлета `Remove-Item`. (В этом примере не показано, как добавлять динамические параметры в командлет `Remove-Item`.)

## <a name="example"></a>Пример

В этом примере показано, как перезаписать методы, необходимые для копирования, создания и удаления элементов, а также методы получения дочерних элементов родительского элемента.

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs" range="11-1635":::

## <a name="see-also"></a>См. также:

[System. Management. Automation. Provider. Итемкмдлетпровидер](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[System. Management. Automation. Provider. Контаинеркмдлетпровидер](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[System. Management. Automation. Provider. Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[Разработка поставщика Windows PowerShell](./provider-types.md)
