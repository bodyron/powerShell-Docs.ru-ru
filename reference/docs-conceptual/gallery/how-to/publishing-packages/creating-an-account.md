---
ms.date: 09/11/2018
contributor: JKeithB
keywords: коллекции,powershell,командлет,psgallery
title: Создание учетной записи коллекции PowerShell
ms.openlocfilehash: f43d7e65bb8bf9a9bbdda9790cc622786377fa38
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "78278792"
---
# <a name="creating-a-powershell-gallery-account"></a>Создание учетной записи коллекции PowerShell

Перед публикацией чего-либо в коллекцию PowerShell необходимо создать учетную запись коллекции PowerShell.
Учетные записи коллекции PowerShell должны быть связаны с учетной записью входа с поддержкой электронной почты. Эта учетная запись может быть учетной записью Azure Active Directory или идентификатором Майкрософт, таким как учетная запись электронной почты outlook.com или hotmail.com.

Чтобы создать учетную запись коллекции PowerShell, перейдите на веб-сайт по адресу [https://PowerShellGallery.com](https://PowerShellGallery.com) и выберите пункт **Войти**, как показано на следующем рисунке.

![Регистрация новой учетной записи](media/creating-an-account/CreateAccount-Register.png)

Чтобы использовать учетную запись Azure Active Directory, щелкните **Рабочая или учебная учетная запись** и выполните вход с помощью своей учетной записи. Чтобы использовать идентификатор Майкрософт, выберите **Личная учетная запись** и выполните вход.

Затем вам будет предложено создать имя пользователя для коллекции PowerShell. Ознакомьтесь с условиями использования и политикой конфиденциальности, введите имя пользователя и щелкните **Зарегистрировать**.

> [!NOTE]
> Имя учетной записи нельзя изменить после ее создания. См. дополнительные сведения об [управлении владельцами пакетов](managing-package-owners.md).

## <a name="recommended-practices-for-powershell-gallery-accounts"></a>Рекомендации по использованию учетных записей коллекции PowerShell

Важно постоянно отслеживать учетную запись электронной почты, используемую с вашей учетной записью коллекции PowerShell. Общение с владельцами пакетов коллекции PowerShell осуществляется через этот адрес электронной почты. Если группе эксплуатации не удается связаться с владельцем пакета, может потребоваться удалить пакет.

Организации, которые публикуют в коллекцию PowerShell, часто создают для этого уникальные внешние учетные записи. Для пересылки уведомлений на адрес организации рекомендуется использовать функцию пересылки электронной почты.

Если с пакетом связаны несколько владельцев, все уведомления коллекции PowerShell отправляются всем владельцам. См. дополнительные сведения об [управлении владельцами пакетов](managing-package-owners.md).
