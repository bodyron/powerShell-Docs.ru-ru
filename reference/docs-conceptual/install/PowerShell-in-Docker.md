---
title: Использование PowerShell в Docker
description: Использование среды PowerShell, предварительно установленной в образе Docker.
ms.devlang: powershell
ms.topic: conceptual
ms.date: 03/03/2020
ms.openlocfilehash: 771214c719ef01fe2c8bc56a4b26c629fcad3856
ms.sourcegitcommit: 01c60c0c97542dbad48ae34339cddbd813f1353b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279661"
---
# <a name="using-powershell-in-docker"></a><span data-ttu-id="2cc64-103">Использование PowerShell в Docker</span><span class="sxs-lookup"><span data-stu-id="2cc64-103">Using PowerShell in Docker</span></span>

<span data-ttu-id="2cc64-104">Корпорация Майкрософт публикует образы Docker с предварительной установкой PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cc64-104">We publish Docker images with PowerShell preinstalled.</span></span> <span data-ttu-id="2cc64-105">В этой статье описывается, как приступить к работе с PowerShell в контейнере Docker.</span><span class="sxs-lookup"><span data-stu-id="2cc64-105">This article shows you how to get started using PowerShell in the Docker container.</span></span>

## <a name="finding-available-images"></a><span data-ttu-id="2cc64-106">Поиск доступных образов</span><span class="sxs-lookup"><span data-stu-id="2cc64-106">Finding available images</span></span>

<span data-ttu-id="2cc64-107">Для выпущенных образов требуется Docker 17.05 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2cc64-107">The released images require Docker 17.05 or newer.</span></span> <span data-ttu-id="2cc64-108">Также предполагается, что Docker можно запускать без `sudo` или прав локального администратора.</span><span class="sxs-lookup"><span data-stu-id="2cc64-108">It is also expected that you are able to run Docker without `sudo` or local administrative rights.</span></span> <span data-ttu-id="2cc64-109">Чтобы правильно установить `docker`, следуйте официальным [инструкциям][install] Docker.</span><span class="sxs-lookup"><span data-stu-id="2cc64-109">Please follow Docker's official [instructions][install] to install `docker` correctly.</span></span>

<span data-ttu-id="2cc64-110">Контейнеры выпуска извлекают содержимое из официального распространяемого образа, например `centos:7`, затем устанавливают зависимости и, наконец, устанавливают пакет PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cc64-110">The release containers derive from the official distribution image, such as `centos:7`, then install dependencies, and finally install the PowerShell package.</span></span>

<span data-ttu-id="2cc64-111">Контейнеры находятся по адресу [hub.docker.com/r/microsoft/powershell][docker-release].</span><span class="sxs-lookup"><span data-stu-id="2cc64-111">These containers live at [hub.docker.com/r/microsoft/powershell][docker-release].</span></span>

<span data-ttu-id="2cc64-112">Чтобы получить дополнительные сведения об этих образах Docker, перейдите в репозиторий [PowerShell-Docker][PowerShell-Docker] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="2cc64-112">For more information about these Docker images, visit the [PowerShell-Docker][PowerShell-Docker] repository on GitHub.</span></span>

## <a name="using-powershell-in-a-container"></a><span data-ttu-id="2cc64-113">Использование PowerShell в контейнере</span><span class="sxs-lookup"><span data-stu-id="2cc64-113">Using PowerShell in a container</span></span>

<span data-ttu-id="2cc64-114">Ниже представлены команды Docker, необходимые для скачивания образа и запуска интерактивного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cc64-114">The following steps show the Docker commands required to download the image and start an interactive PowerShell session.</span></span>

```console
docker run -it mcr.microsoft.com/powershell
```

### <a name="remove-the-image-when-no-longer-needed"></a><span data-ttu-id="2cc64-115">Удаление ненужного образа</span><span class="sxs-lookup"><span data-stu-id="2cc64-115">Remove the image when no longer needed</span></span>

<span data-ttu-id="2cc64-116">Приведенная ниже команда служит для удаления контейнера Docker, если он больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="2cc64-116">The following command is used to delete the Docker container when you no longer need it.</span></span>

```console
docker rmi mcr.microsoft.com/powershell
```

## <a name="legal-and-licensing"></a><span data-ttu-id="2cc64-117">Правовая информация и лицензирование</span><span class="sxs-lookup"><span data-stu-id="2cc64-117">Legal and Licensing</span></span>

<span data-ttu-id="2cc64-118">PowerShell лицензируется на условиях [Лицензия MIT][].</span><span class="sxs-lookup"><span data-stu-id="2cc64-118">PowerShell is licensed under the [MIT license][].</span></span>

### <a name="windows-docker-file-and-image-licenses"></a><span data-ttu-id="2cc64-119">Файл Windows Docker и лицензии на образы</span><span class="sxs-lookup"><span data-stu-id="2cc64-119">Windows Docker File and Image Licenses</span></span>

<span data-ttu-id="2cc64-120">Запрашивая и используя образ ОС контейнера для контейнеров Windows, вы признаете, что ознакомлены с Дополнительными условиями лицензионного соглашения, доступными в Docker Hub, и соглашаетесь с ними:</span><span class="sxs-lookup"><span data-stu-id="2cc64-120">By requesting and using the Container OS Image for Windows containers, you acknowledge, understand, and consent to the Supplemental License Terms available on Docker hub:</span></span>

- <span data-ttu-id="2cc64-121">[Window Server Core][Window Server Core]</span><span class="sxs-lookup"><span data-stu-id="2cc64-121">[Window Server Core][Window Server Core]</span></span>
- <span data-ttu-id="2cc64-122">[Nano Server][Nano Server]</span><span class="sxs-lookup"><span data-stu-id="2cc64-122">[Nano Server][Nano Server]</span></span>

### <a name="telemetry"></a><span data-ttu-id="2cc64-123">Телеметрия</span><span class="sxs-lookup"><span data-stu-id="2cc64-123">Telemetry</span></span>

<span data-ttu-id="2cc64-124">По умолчанию PowerShell собирает ограниченные данные телеметрии без личных сведений, которые могут помочь в разработке будущих версий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cc64-124">By default, PowerShell collects limited telemetry without personally identifiable information to help aid development of future versions of PowerShell.</span></span> <span data-ttu-id="2cc64-125">Чтобы отказаться от отправки данных телеметрии, создайте переменную среды `POWERSHELL_TELEMETRY_OPTOUT` и присвойте ей значение `1` перед запуском PowerShell из места установки.</span><span class="sxs-lookup"><span data-stu-id="2cc64-125">To opt-out of sending telemetry, create an environment variable called `POWERSHELL_TELEMETRY_OPTOUT` set to a value of `1` before starting PowerShell from the installed location.</span></span> <span data-ttu-id="2cc64-126">На собираемые нами данные телеметрии распространяется [Заявление о конфиденциальности корпорации Майкрософт][privacy].</span><span class="sxs-lookup"><span data-stu-id="2cc64-126">The telemetry we collect falls under the [Microsoft Privacy Statement][privacy].</span></span>

<!-- link references -->
[install]: https://docs.docker.com/engine/installation/
[docker-release]: https://hub.docker.com/r/microsoft/powershell/
[appinsights]: https://azure.microsoft.com/services/application-insights/
[Лицензия MIT]: https://github.com/PowerShell/PowerShell/tree/master/LICENSE.txt
[MIT license]: https://github.com/PowerShell/PowerShell/tree/master/LICENSE.txt
[PowerShell-Docker]: https://github.com/PowerShell/PowerShell-Docker
[Window Server Core]: https://hub.docker.com/r/microsoft/windowsservercore/
[Nano Server]: https://hub.docker.com/r/microsoft/nanoserver/
[privacy]: https://privacy.microsoft.com/privacystatement/