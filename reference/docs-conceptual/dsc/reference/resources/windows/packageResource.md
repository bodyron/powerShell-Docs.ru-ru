---
ms.date: 09/20/2019
keywords: dsc,powershell,конфигурация,установка
title: Ресурс Package в DSC
ms.openlocfilehash: ff2eae712b4117da9bca915f52e18caed7c4885d
ms.sourcegitcommit: 173556307d45d88de31086ce776770547eece64c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83559936"
---
# <a name="dsc-package-resource"></a>Ресурс Package в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.x

Ресурс **Package** в DSC Windows PowerShell предоставляет механизм установки или удаления пакетов, таких как пакеты установщика Windows и setup.exe, на целевом узле.

## <a name="syntax"></a>Синтаксис

```Syntax
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ ReturnCode = [UInt32[]] ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Свойства

|Свойство |Description |
|---|---|
|Имя |Указывает имя пакета, для которого требуется обеспечить определенное состояние. |
|путь |Указывает путь к файлу пакета. |
|ProductId |Указывает уникальный идентификатор пакета. |
|Аргументы |Указывает строку аргументов, которая будет передана в пакет в указанном виде. |
|Учетные данные |Предоставляет доступ к пакету в удаленном источнике. Это свойство не используется для установки пакета. Пакет всегда устанавливается в локальной системе. |
|LogPath |Указывает полный путь к папке, где нужно сохранить файл журнала для установки или удаления пакета. |
|ReturnCode |Указывает ожидаемый код возврата. Если фактический код возврата не соответствует указанному здесь значению, настройка вернет ошибку. |

## <a name="common-properties"></a>Общие свойства

|Свойство |Description |
|---|---|
|DependsOn |Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — ResourceName, а его тип — ResourceType, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`. |
|Ensure |Указывает, установлен ли пакет. Если это свойство имеет значение **Absent**, пакет не устанавливается (а если он уже установлен, то удаляется). Если это свойство имеет значение **Present**, пакет устанавливается. Значение по умолчанию — **Present**. |
|PsDscRunAsCredential |Задает учетные данные для выполнения всего ресурса от другого имени. |

> [!NOTE]
> В WMF 5.0 было добавлено общее свойство **PsDscRunAsCredential**, разрешающее запуск любого ресурса DSC в контексте других учетных данных. Дополнительные сведения см. в разделе [Использование учетных данных с ресурсами DSC](../../../configurations/runasuser.md).

## <a name="example"></a>Пример

В этом примере выполняется установщик MSI, который находится по указанному пути и имеет указанный идентификатор.

```powershell
Configuration PackageTest
{
    Package PackageExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Path        = "$Env:SystemDrive\TestFolder\TestProject.msi"
        Name        = "TestPackage"
        ProductId   = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
    }
}
```
