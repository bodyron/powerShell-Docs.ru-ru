---
ms.date: 09/05/2018
contributor: JKeithB
keywords: коллекции,powershell,командлет,psgallery
title: Параметры учетной записи коллекции PowerShell
ms.openlocfilehash: 7f67311b42123f247a00a9c7a5bf775685b64d48
ms.sourcegitcommit: 173556307d45d88de31086ce776770547eece64c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83560463"
---
# <a name="powershell-gallery-account-settings"></a>Параметры учетной записи коллекции PowerShell

Учетная запись коллекции PowerShell представляет собой видимое для обычных пользователей имя, связанное с удостоверением. Этим удостоверением является либо идентификатор Майкрософт, такой как `user@hotmail.com` или `user@outlook.com`, либо учетная запись Azure Active Directory (AAD).

Коллекция PowerShell предоставляет следующие параметры учетной записи:

- учетная запись электронной почты, связанная с вашей учетной записью коллекции PowerShell;
- параметры для уведомлений по электронной почте, отправляемых из коллекции PowerShell;
- учетная запись пользователя, связанная с вашей учетной записью коллекции PowerShell;
- изображение, связанное с вашей учетной записью коллекции PowerShell.

## <a name="email-address"></a>Адрес электронной почты

Адрес электронной почты является назначением для уведомлений коллекции PowerShell. Он не должен совпадать с учетной записью входа. Можно использовать любую доступную учетную запись электронной почты. Коллекция PowerShell никогда напрямую не предоставляет ваш адрес электронной почты другим пользователям.

![Изменение адреса электронной почты](media/managing-account/PSGallery_AcccountEmailAddress.png)

Когда вы вводите новый адрес электронной почты, коллекция PowerShell отправляет на него проверочное сообщение. В этом сообщении содержится ссылка на коллекцию PowerShell для завершения процесса изменения. Пока вы не завершите процесс проверки, все уведомления отправляются на предыдущий адрес.

## <a name="email-notifications"></a>Уведомления по электронной почте

Коллекция PowerShell предоставляет следующие параметры уведомлений.

- Users can contact me through the PowerShell Gallery (Пользователи могут связываться со мной с помощью коллекции PowerShell)
- Notify me when an item is pushed to the PowerShell Gallery using my account (Уведомлять об отправке пакета в коллекцию PowerShell с помощью моей учетной записи)

![Изменение адреса электронной почты](media/managing-account/PSGallery_AccountEmailOptions.png)

Как указано на странице, критически важные уведомления из коллекции PowerShell отключить невозможно.
К ним относятся следующие объекты.

- уведомления безопасности;
- уведомления об управлении учетными записями от администраторов коллекции PowerShell;
- уведомления о тестах, запускаемых коллекцией PowerShell, для выполненной отправки.

## <a name="change-your-login-account"></a>Изменение учетной записи входа

Чтобы изменить учетную запись входа, необходимо выполнить вход с помощью текущей учетной записи. Выполните следующие действия для изменения учетной записи.

![Параметры учетной записи](media/managing-account/PSGallery_LoginAccountSettings.png)

1. Щелкните **Изменить учетную запись**. Появится всплывающее окно объясняющее, что изменение учетной записи входа применяется ко всем случаям использования этой учетной записи в коллекции PowerShell. Ознакомьтесь с информацией и нажмите кнопку **ОК**, чтобы продолжить.

   ![Параметры учетной записи](media/managing-account/PSGallery_LoginAccountChange-1.png)

2. Затем вам будет предложено выполнить вход с помощью _новой учетной записи_.

   ![Параметры учетной записи](media/managing-account/PSGallery_LoginAccountChange-2.png)

3. После нажатия кнопки **Далее** появится сообщение, информирующее о входе с использованием текущей учетной записи.
   Щелкните **Выйти и выполнить вход с использованием другой учетной записи**.

   ![Параметры учетной записи](media/managing-account/PSGallery_LoginAccountChange-3.png)

4. Введите пароль новой учетной записи. После ввода пароля вы вернетесь на страницу параметров учетной записи, где отображается обновленная учетная запись.

## <a name="enable-two-factor-authentication-2fa"></a>Включение двухфакторной проверки подлинности

Двухфакторную проверку подлинности рекомендуется проходить всем пользователям, которые вручную публикуют данные в коллекцию PowerShell. Чтобы включить двухфакторную проверку подлинности, для учетной записи входа должны быть зарегистрированы по крайней мере две формы проверки подлинности. Одной является использование пароля, а другими могут быть:

- номер телефона с поддержкой приема текстовых сообщений;
- зарегистрированное приложение для проверки подлинности, например Microsoft Authenticator, для мобильного телефона.

Эти формы проверки подлинности должны быть настроены в разделе сведений об учетной записи AAD или в параметрах безопасности учетной записи ИД Майкрософт.

После включения двухфакторной проверки подлинности вам требуется проходить проверку подлинности с помощью настроенных форм при каждом входе в коллекцию PowerShell.

> [!IMPORTANT]
> При включении двухфакторной проверки подлинности для сайта коллекции PowerShell не нужно включать двухфакторную проверку подлинности для всех случаев использования учетной записи входа. Дополнительные сведения см. в статье [Сведения о двухфакторной проверке подлинности](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="change-your-profile-picture"></a>Изменение изображения в профиле

Для хранения и отображения изображения, связанного с профилем, коллекция PowerShell использует Gravatar. Чтобы обновить изображение в профиле, посетите веб-сайт [Gravatar.com](http://www.gravatar.com/).
