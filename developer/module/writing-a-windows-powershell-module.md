---
title: Написание модуля Windows PowerShell | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bfbccc5b-2b2b-432a-a971-9f8ab503cdc3
caps.latest.revision: 17
ms.openlocfilehash: 3c6d8e410427d6cfaa1c15db421b3fe935f7d322
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56857940"
---
# <a name="writing-a-windows-powershell-module"></a>Написание модуля Windows PowerShell

Этот документ был написан для администраторов, скрипт разработчикам и разработчикам командлетов, которым необходимо создание и распространение их командлеты Windows PowerShell. С помощью модулей Windows PowerShell, можно упаковать и распространить свои решения Windows PowerShell без использования скомпилированный язык.

Модули Windows PowerShell для его секции, упорядочивать и абстрагировать код Windows PowerShell в автономной и многократно используемых единиц. Эти единицы для повторного использования вы можете легко обмениваться модули непосредственно с другими пользователями. Если вы являетесь разработчиком скрипт, вы можете также переупаковать сторонних модулей, чтобы создавать пользовательские приложения на основе сценария. Модули, аналогичную модулям в других языках сценариев, таких как Perl и Python, включения решений со сценариями готовый к выпуску, использующих многократно используемых, распространяемые компоненты, с дополнительными преимуществами, поскольку позволяет не делать одну и абстрагировать несколько компонентов для Создание пользовательских решений.

В их основных Windows PowerShell будет рассматривать любой допустимый код сценария Windows PowerShell, сохраненные в файле с расширением psm1 как модуль. PowerShell также автоматически обрабатывает любую сборку двоичных командлет как модуль. Тем не менее можно также использовать модуль (или точнее, манифеста модуля), объединить всего решения. Следующие сценарии описывают типичные способы использования модулей Windows PowerShell.

### <a name="libraries"></a>Библиотеки

Модули можно использовать для упаковки и распространения связный библиотеки функций для выполнения типичных задач. Как правило имена этих функций, совместно использовать один или несколько существительных, отражающих типичную задачу, они используются для. Эти функции также может быть аналогичную классов .NET Framework, в том, что они могут иметь открытым и закрытым элементам. Например библиотеку может содержать набор функций для передачи файлов. В этом случае существительное, отражая общие задачи может быть «файл».

### <a name="configuration"></a>Конфигурация

Модули можно использовать для настройки вашей среды, добавив определенные командлеты, поставщики, функции и переменные.

### <a name="compiled-code-development-and-distribution"></a>Скомпилированный код разработки и распространения

Командлетов и поставщиков разработчики могут использовать модули для тестирования и распространения их скомпилированного кода без необходимости создания оснастки. Их можно импортировать сборку, содержащую скомпилированный код в виде модуля (двоичный модуль) без необходимости создания и регистрации оснастки.

## <a name="see-also"></a>См. также

[Основные сведения о модуле Windows PowerShell](./understanding-a-windows-powershell-module.md)

[Как написать модуль сценария PowerShell](./how-to-write-a-powershell-script-module.md)

[Как написать модуль двоичных файлов PowerShell](./how-to-write-a-powershell-binary-module.md)

[Как создать манифест модуля PowerShell](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6)

[Изменение пути установки PSModulePath](./modifying-the-psmodulepath-installation-path.md)

[Импорт модуля PowerShell](./importing-a-powershell-module.md)

[Установка модуля PowerShell](./installing-a-powershell-module.md)