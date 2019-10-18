---
title: Объявление атрибута параметра | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, Parameter
- Parameter attribute, described
- Parameter attribute
ms.assetid: 08433d0b-169b-42c8-9335-2881d9034698
caps.latest.revision: 13
ms.openlocfilehash: 81b1ed95669f51ba554f6f99031d098e239f02e0
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72365363"
---
# <a name="parameter-attribute-declaration"></a>Объявление атрибута параметра

Атрибут Parameter определяет открытое свойство класса командлета в качестве параметра командлета.

## <a name="syntax"></a>Синтаксис

```csharp
[Parameter()]
[Parameter(Named Parameters...)]
```

#### <a name="parameters"></a>Параметры

`Mandatory` ([System. Boolean](/dotnet/api/System.Boolean)) необязательный именованный параметр. значение `True` указывает, что параметр командлета является обязательным. Если требуемый параметр не указан при вызове командлета, Windows PowerShell предлагает пользователю указать значение параметра. Значение по умолчанию — `false`.

`ParameterSetName` ([System. String](/dotnet/api/System.String)) необязательный именованный параметр. Задает набор параметров, к которому относится этот параметр командлета. Если набор параметров не задан, параметр относится ко всем наборам параметров.

`Position` ([System. Int32](/dotnet/api/System.Int32)) необязательный именованный параметр. Задает расположение параметра в команде Windows PowerShell.

`ValueFromPipeline` ([System. Boolean](/dotnet/api/System.Boolean)) необязательный именованный параметр. `True` указывает, что параметр командлета принимает значение из объекта конвейера. Укажите это ключевое слово, если командлет обращается к полному объекту, а не только к свойству объекта. Значение по умолчанию — `false`.

`ValueFromPipelineByPropertyName` ([System. Boolean](/dotnet/api/System.Boolean)) необязательный именованный параметр. `True` указывает, что параметр командлета принимает свое значение из свойства объекта конвейера с тем же именем или псевдонимом, что и у этого параметра. Например, если командлет имеет параметр `Name`, а у объекта конвейера также есть свойство `Name`, то значение свойства `Name` присваивается параметру `Name` командлета. Значение по умолчанию — `false`.

`ValueFromRemainingArguments` ([System. Boolean](/dotnet/api/System.Boolean)) необязательный именованный параметр. `True` указывает, что параметр командлета принимает все оставшиеся аргументы, переданные в командлет. Значение по умолчанию — `false`.

`HelpMessage` необязательный именованный параметр. Задает краткое описание параметра. Windows PowerShell отображает это сообщение при выполнении командлета, а обязательный параметр не указан.

`HelpMessageBaseName` необязательный именованный параметр. Указывает расположение, в котором находятся идентификаторы ресурсов. Например, этот параметр может указывать сборку ресурсов, содержащую справочные сообщения, которые требуется локализовать.

`HelpMessageResourceId` необязательный именованный параметр. Указывает идентификатор ресурса для сообщения справки.

## <a name="remarks"></a>Замечания

- Дополнительные сведения об объявлении этого атрибута см. в разделе [как объявлять параметры командлета](./how-to-declare-cmdlet-parameters.md).

- Командлет может иметь любое количество параметров. Однако для повышения удобства работы пользователей Ограничьте количество параметров.

- Параметры должны быть объявлены для открытых нестатических полей или свойств. Параметры должны быть объявлены в свойствах. Свойство должно иметь открытый метод доступа set, и если указано ключевое слово `ValueFromPipeline` или `ValueFromPipelineByPropertyName`, свойство должно иметь открытый метод доступа get.

- При указании позиционированных параметров Ограничьте число параметров, заданных в параметре, равным меньше пяти. И параметры позиционирования не должны быть непрерывными. Позиции 5, 100 и 250 работают так же, как позиции 0, 1 и 2.

- Если ключевое слово `Position` не указано, на параметр командлета должно ссылаться имя.

- При использовании наборов параметров Обратите внимание на следующее:

    - Каждый набор параметров должен иметь по крайней мере один уникальный параметр. Хорошая структура командлетов указывает, что этот уникальный параметр также должен быть обязательным, если это возможно. Если командлет предназначен для выполнения без параметров, то уникальный параметр не может быть обязательным.

    - Ни один из наборов параметров не должен содержать более одного позиционированного параметра с одинаковой позицией.

    - Только один параметр в наборе параметров должен объявлять `ValueFromPipeline = true`. Несколько параметров могут определять `ValueFromPipelineByPropertyName = true`.

    - Несколько параметров могут определять `ValueFromPipelineByPropertyName = true`.

- Дополнительные сведения о рекомендациях по именам параметров см. в разделе [имена параметров командлета](standard-cmdlet-parameter-names-and-types.md).

- Атрибут параметра определяется классом [System. Management. Automation. параметераттрибуте](/dotnet/api/System.Management.Automation.ParameterAttribute) .

## <a name="see-also"></a>См. также:

[System. Management. Automation. Параметераттрибуте](/dotnet/api/System.Management.Automation.ParameterAttribute)

[Имена параметров командлета](standard-cmdlet-parameter-names-and-types.md)

[Запись командлета Windows PowerShell](./writing-a-windows-powershell-cmdlet.md)