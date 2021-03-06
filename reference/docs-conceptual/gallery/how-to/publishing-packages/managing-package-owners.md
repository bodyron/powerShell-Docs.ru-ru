---
ms.date: 06/12/2017
contributor: JKeithB
keywords: коллекции,powershell,командлет,psgallery
title: Управление владельцами пакетов
ms.openlocfilehash: 72a3ff72818c5461c74d46de5689e2d6c59b19bf
ms.sourcegitcommit: 173556307d45d88de31086ce776770547eece64c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2020
ms.locfileid: "83564675"
---
# <a name="managing-package-owners"></a>Управление владельцами пакетов

Право собственности на пакет в коллекции PowerShell определяется тем, кто опубликовал пакет в коллекции.
Иногда этими метаданными необходимо управлять после первоначальной публикации пакета, а значит метаданные о владельцах пакета должны быть изменяемыми, даже если сам пакет таковым не является.

Все владельцы пакета имеют равные права.
Это значит, что любой владелец пакета может опубликовать его новую версию. Это также означает, что любой владелец пакета может удалить любого другого владельца этого пакета.
Ни один владелец не имеет больше полномочий, чем другие.

## <a name="setting-a-packages-initial-owner"></a>Установка первоначального владельца пакета

При публикации пакета в коллекции PowerShell статус первоначального владельца получает пользователь, опубликовавший пакет. Он определяется по ключу интерфейса API, который использовался в командлете Publish-Module.

## <a name="adding-owners"></a>Добавление владельцев

После публикации пакета в коллекции PowerShell можно пригласить других пользователей стать его владельцами.

1. [Войдите](https://powershellgallery.com/users/account/LogOn) в коллекцию PowerShell с помощью учетной записи текущего владельца пакета.
2. Перейдите на страницу пакета, открыв вкладку "Пакеты", выполнив поиск или щелкнув свое имя пользователя, и выберите пункт [**Управление моими пакетами**](https://www.powershellgallery.com/account/Packages).
3. Если вход в систему выполнен владельцем пакета, слева будет доступна ссылка "Управление владельцами".
4. Введите имя пользователя, которого нужно добавить в качестве владельца, и нажмите кнопку "Добавить".
5. После этого новому совладельцу будет отправлено электронное письмо с приглашением стать владельцем пакета.
6. Щелкнув ссылку в этом письме, пользователь станет совладельцем пакета со всеми правами, включая возможность удалять других владельцев пакета.

**Примечание**. Пока новый владелец не подтвердит свой статус владельца, он *не будет* указан как владелец пакета.
В списке текущих владельцев на странице **Управление владельцами** для него будет отображаться запись "Ожидает подтверждения".
Приглашение, как и других владельцев, можно удалить.
Процедура приглашения защищает пользователей от ошибочного добавления других пользователей в число владельцев пакета.

Обратите внимание, что метаданные "Авторы" заполняются произвольно, контролируются только "Владельцы".

## <a name="removing-owners"></a>Удаление владельцев

Если у пакета несколько владельцев и одного из них нужно удалить, это делается очень просто:

1. [Войдите](https://powershellgallery.com/users/account/LogOn) в коллекцию PowerShell по учетной записи текущего владельца пакета.
2. Перейдите на страницу пакета, открыв вкладку "Пакеты", выполнив поиск или щелкнув свое имя пользователя, и выберите пункт [**Управление моими пакетами**](https://www.powershellgallery.com/account/Packages).
3. Если вход в систему выполнен владельцем пакета, слева будет доступна ссылка "Управление владельцами".
4. Щелкните ссылку "Удалить" рядом с удаляемым владельцем.

## <a name="transferring-package-ownership"></a>Передача права собственности на пакет

В службу поддержки периодически поступают запросы о передаче права собственности на пакет от одного пользователя к другому, но почти всегда вы можете сделать это сами.
Передача владения от одного пользователя другому представляет собой простую комбинацию двух описанных выше функций.

1. Текущий владелец приглашает нового пользователя в качестве совладельца, а новый пользователь принимает приглашение.
2. Новый пользователь удаляет старого пользователя из списка владельцев.

Это действие может потребоваться по ряду причин, но процедура всегда одна и та же.

- Право собственности на пакет переходит от одного разработчика к другому.
- Пакет был ошибочно опубликован с помощью другой учетной записи.

## <a name="orphaned-packages"></a>У пакетов нет владельца.

Возможна и еще одна ситуация, но встречается она нечасто.
Пакет остается без владельца, а учетную запись единственного владельца пакета нельзя использовать, чтобы добавить новых владельцев.
Приведем несколько примеров такой ситуации.

- Учетная запись владельца связана с адресом электронной почты, который больше не существует, либо пользователь забыл пароль.
- Зарегистрированный владелец уволился из компании, в которой был создан пакет, и с ним не удается связаться, чтобы передать право собственности на пакет.
- Из-за ошибки, затронувшей небольшое количество пакетов, пакет остался в коллекции без владельца.

Администраторы коллекции PowerShell имеют доступ к ссылке "Управление владельцами" любого пакета.
Если вы являетесь действительным владельцем пакета и не можете связаться с текущим владельцем, чтобы получить право собственности, щелкните ссылку "Сообщить о нарушении" в коллекции, чтобы связаться с администраторами коллекции PowerShell.
Мы проверим ваше право собственности на этот пакет.
Если подтвердится, что владельцем пакета должны быть вы, мы воспользуемся ссылкой "Управление владельцами" и отправим вам приглашение стать владельцем.
Мы сделаем это только после того, как убедимся, что вы должны быть владельцем; дальнейший порядок действий зависит от ситуации.
Как правило, мы пытаемся связаться с владельцем проекта, используя URL-адрес проекта этого пакета, но можем также искать его в социальных сетях, с помощью электронной почты или других средств.
