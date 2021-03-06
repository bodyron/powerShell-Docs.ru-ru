---
title: Примеры настраиваемого узла | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 55aee25b-bbcb-4d41-a4c0-fb8e30c4cdc1
caps.latest.revision: 11
ms.openlocfilehash: 1e58b74cf1c37c70ebfb0f4970cfbf8a8263ec5c
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "72367513"
---
# <a name="custom-host-samples"></a>Примеры пользовательских узлов

В этом разделе содержится пример кода для написания пользовательского узла. С помощью Microsoft Visual Studio можно создать консольное приложение, а затем скопировать код из разделов этого раздела в ведущее приложение.

## <a name="in-this-section"></a>Содержание

 [Пример Host01](./host01-sample.md) В этом примере показано, как реализовать ведущее приложение, которое использует базовый пользовательский узел.

 [Пример Host02](./host02-sample.md) В этом примере показано, как создать ведущее приложение, которое использует среду выполнения Windows PowerShell вместе с реализацией пользовательского узла. Ведущее приложение устанавливает немецкий язык и региональные параметры, запускает командлет [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) и отображает результаты, как это можно увидеть с помощью пврш. exe, а затем выводит текущие данные и время на немецком языке.

 [Пример Host03](./host03-sample.md) В этом примере показано, как создать консольное приложение на основе консоли, которое считывает команды из командной строки, выполняет команды и выводит результаты на консоль.

 [Пример Host04](./host04-sample.md) В этом примере показано, как создать консольное приложение на основе консоли, которое считывает команды из командной строки, выполняет команды и выводит результаты на консоль. Это приложение также поддерживает отображение запросов, позволяющих пользователю выбрать несколько вариантов.

 [Пример Host05](./host05-sample.md) В этом примере показано, как создать консольное приложение на основе консоли, которое считывает команды из командной строки, выполняет команды и выводит результаты на консоль. Это ведущее приложение также поддерживает вызовы удаленных компьютеров с помощью командлетов [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) и [Exit-PSSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) .

 [Пример Host06](./host06-sample.md) В этом примере показано, как создать консольное приложение на основе консоли, которое считывает команды из командной строки, выполняет команды и выводит результаты на консоль. Кроме того, в этом примере используются интерфейсы API создателя токенов для указания цвета текста, вводимого пользователем.

## <a name="see-also"></a>См. также:
