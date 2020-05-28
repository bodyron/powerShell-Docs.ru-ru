---
ms.date: 04/19/2019
keywords: wmf,powershell,установка
title: Windows Management Framework (WMF)
ms.openlocfilehash: d581370fd602e03c86aa549eb8b273ff4d01b4e5
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2020
ms.locfileid: "83808690"
---
# <a name="windows-management-framework"></a><span data-ttu-id="92b28-103">Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="92b28-103">Windows Management Framework</span></span>

<span data-ttu-id="92b28-104">Windows Management Framework (WMF) — это согласованный интерфейс управления для Windows.</span><span class="sxs-lookup"><span data-stu-id="92b28-104">Windows Management Framework (WMF) provides a consistent management interface for Windows.</span></span> <span data-ttu-id="92b28-105">WMF обеспечивает удобный способ управления несколькими версиями клиента Windows и Windows Server.</span><span class="sxs-lookup"><span data-stu-id="92b28-105">WMF provides a seamless way to manage various versions of Windows client and Windows Server.</span></span> <span data-ttu-id="92b28-106">Пакеты установщика WMF содержат обновления для функций управления и доступны для более старых версий Windows.</span><span class="sxs-lookup"><span data-stu-id="92b28-106">WMF installer packages contain updates to management functionality and are available for older versions of Windows.</span></span>

<span data-ttu-id="92b28-107">При установке WMF добавляются или обновляются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="92b28-107">WMF installation adds and/or updates the following features:</span></span>

- <span data-ttu-id="92b28-108">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="92b28-108">Windows PowerShell</span></span>
- <span data-ttu-id="92b28-109">Windows PowerShell Desired State Configuration (DSC)</span><span class="sxs-lookup"><span data-stu-id="92b28-109">Windows PowerShell Desired State Configuration (DSC)</span></span>
- <span data-ttu-id="92b28-110">Интегрированная среда сценариев Windows PowerShell (ISE)</span><span class="sxs-lookup"><span data-stu-id="92b28-110">Windows PowerShell Integrated Script Environment (ISE)</span></span>
- <span data-ttu-id="92b28-111">Удаленное управление Windows (WinRM)</span><span class="sxs-lookup"><span data-stu-id="92b28-111">Windows Remote Management (WinRM)</span></span>
- <span data-ttu-id="92b28-112">Инструментарий управления Windows (WMI)</span><span class="sxs-lookup"><span data-stu-id="92b28-112">Windows Management Instrumentation (WMI)</span></span>
- <span data-ttu-id="92b28-113">Веб-службы Windows PowerShell (расширение IIS OData для управления)</span><span class="sxs-lookup"><span data-stu-id="92b28-113">Windows PowerShell Web Services (Management OData IIS Extension)</span></span>
- <span data-ttu-id="92b28-114">Инвентаризация программного обеспечения (SIL)</span><span class="sxs-lookup"><span data-stu-id="92b28-114">Software Inventory Logging (SIL)</span></span>
- <span data-ttu-id="92b28-115">Поставщик CIM диспетчера сервера</span><span class="sxs-lookup"><span data-stu-id="92b28-115">Server Manager CIM Provider</span></span>

## <a name="wmf-release-notes"></a><span data-ttu-id="92b28-116">Заметки о выпуске WMF</span><span class="sxs-lookup"><span data-stu-id="92b28-116">WMF Release Notes</span></span>

<span data-ttu-id="92b28-117">Сведения о различных улучшениях в PowerShell и других компонентах определенной версии WMF см. по следующим ссылкам на заметки о выпусках:</span><span class="sxs-lookup"><span data-stu-id="92b28-117">To learn about various enhancements in PowerShell and other components of a given WMF, please refer to the links below to review the release notes:</span></span>

- [<span data-ttu-id="92b28-118">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="92b28-118">WMF 5.1</span></span>](whats-new/release-notes.md#wmf-51-changes)
- [<span data-ttu-id="92b28-119">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="92b28-119">WMF 5.0</span></span>](whats-new/release-notes.md#wmf-50-changes)
- [<span data-ttu-id="92b28-120">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="92b28-120">WMF 4.0</span></span>](https://download.microsoft.com/download/3/D/6/3D61D262-8549-4769-A660-230B67E15B25/Windows%20Management%20Framework%204%200%20Release%20Notes.docx)
- [<span data-ttu-id="92b28-121">WMF 3.0</span><span class="sxs-lookup"><span data-stu-id="92b28-121">WMF 3.0</span></span>](https://download.microsoft.com/download/E/7/6/E76850B8-DA6E-4FF5-8CCE-A24FC513FD16/WMF%203%20Release%20Notes.docx)

## <a name="wmf-availability-across-windows-operating-systems"></a><span data-ttu-id="92b28-122">Доступность WMF в различных операционных системах Windows</span><span class="sxs-lookup"><span data-stu-id="92b28-122">WMF Availability Across Windows Operating Systems</span></span>

|        <span data-ttu-id="92b28-123">Версия операционной системы</span><span class="sxs-lookup"><span data-stu-id="92b28-123">Operating System Version</span></span>         | <span data-ttu-id="92b28-124">[WMF 5.1][]</span><span class="sxs-lookup"><span data-stu-id="92b28-124">[WMF 5.1][]</span></span>  | <span data-ttu-id="92b28-125">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="92b28-125">WMF 5.0</span></span><br><span data-ttu-id="92b28-126">*Не поддерживается*</span><span class="sxs-lookup"><span data-stu-id="92b28-126">*Out of support*</span></span> | <span data-ttu-id="92b28-127">[WMF 4.0][]</span><span class="sxs-lookup"><span data-stu-id="92b28-127">[WMF 4.0][]</span></span>  | <span data-ttu-id="92b28-128">[WMF 3.0][]</span><span class="sxs-lookup"><span data-stu-id="92b28-128">[WMF 3.0][]</span></span>  | <span data-ttu-id="92b28-129">[WMF 2.0][]</span><span class="sxs-lookup"><span data-stu-id="92b28-129">[WMF 2.0][]</span></span>  |
| --------------------------------------- | ------------ | --------------------------- | ------------ | ------------ | ------------ |
| <span data-ttu-id="92b28-130">Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="92b28-130">Windows Server 2019</span></span>                     | <span data-ttu-id="92b28-131">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-131">Ships in-box</span></span> |                             |              |              |              |
| <span data-ttu-id="92b28-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="92b28-132">Windows Server 2016</span></span>                     | <span data-ttu-id="92b28-133">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-133">Ships in-box</span></span> |                             |              |              |              |
| <span data-ttu-id="92b28-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="92b28-134">Windows 10</span></span>                              | <span data-ttu-id="92b28-135">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-135">Ships in-box</span></span> | <span data-ttu-id="92b28-136">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-136">Ships in-box</span></span>                |              |              |              |
| <span data-ttu-id="92b28-137">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="92b28-137">Windows Server 2012 R2</span></span>                  | <span data-ttu-id="92b28-138">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-138">Yes</span></span>          | <span data-ttu-id="92b28-139">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-139">Yes</span></span>                         | <span data-ttu-id="92b28-140">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-140">Ships in-box</span></span> |              |              |
| <span data-ttu-id="92b28-141">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="92b28-141">Windows 8.1</span></span>                             | <span data-ttu-id="92b28-142">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-142">Yes</span></span>          | <span data-ttu-id="92b28-143">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-143">Yes</span></span>                         | <span data-ttu-id="92b28-144">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-144">Ships in-box</span></span> |              |              |
| <span data-ttu-id="92b28-145">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="92b28-145">Windows Server 2012</span></span>                     | <span data-ttu-id="92b28-146">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-146">Yes</span></span>          | <span data-ttu-id="92b28-147">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-147">Yes</span></span>                         | <span data-ttu-id="92b28-148">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-148">Yes</span></span>          | <span data-ttu-id="92b28-149">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-149">Ships in-box</span></span> |              |
| <span data-ttu-id="92b28-150">Windows 8</span><span class="sxs-lookup"><span data-stu-id="92b28-150">Windows 8</span></span><br><span data-ttu-id="92b28-151">*Не поддерживается*</span><span class="sxs-lookup"><span data-stu-id="92b28-151">*Out of support*</span></span>           |              |                             |              | <span data-ttu-id="92b28-152">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-152">Ships in-box</span></span> |              |
| <span data-ttu-id="92b28-153">Windows Server 2008 R2 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="92b28-153">Windows Server 2008 R2 SP1</span></span>              | <span data-ttu-id="92b28-154">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-154">Yes</span></span>          | <span data-ttu-id="92b28-155">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-155">Yes</span></span>                         | <span data-ttu-id="92b28-156">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-156">Yes</span></span>          | <span data-ttu-id="92b28-157">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-157">Yes</span></span>          | <span data-ttu-id="92b28-158">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-158">Ships in-box</span></span> |
| <span data-ttu-id="92b28-159">Windows 7 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="92b28-159">Windows 7 SP1</span></span>                           | <span data-ttu-id="92b28-160">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-160">Yes</span></span>          | <span data-ttu-id="92b28-161">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-161">Yes</span></span>                         | <span data-ttu-id="92b28-162">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-162">Yes</span></span>          | <span data-ttu-id="92b28-163">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-163">Yes</span></span>          | <span data-ttu-id="92b28-164">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="92b28-164">Ships in-box</span></span> |
| <span data-ttu-id="92b28-165">Windows Server 2008 с пакетом обновления 2 (SP2)</span><span class="sxs-lookup"><span data-stu-id="92b28-165">Windows Server 2008 SP2</span></span>                 |              |                             |              | <span data-ttu-id="92b28-166">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-166">Yes</span></span>          | <span data-ttu-id="92b28-167">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-167">Yes</span></span>          |
| <span data-ttu-id="92b28-168">Windows Vista</span><span class="sxs-lookup"><span data-stu-id="92b28-168">Windows Vista</span></span><br><span data-ttu-id="92b28-169">*Не поддерживается*</span><span class="sxs-lookup"><span data-stu-id="92b28-169">*Out of support*</span></span>       |              |                             |              |              | <span data-ttu-id="92b28-170">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-170">Yes</span></span>          |
| <span data-ttu-id="92b28-171">Windows Server 2003</span><span class="sxs-lookup"><span data-stu-id="92b28-171">Windows Server 2003</span></span><br><span data-ttu-id="92b28-172">*Не поддерживается*</span><span class="sxs-lookup"><span data-stu-id="92b28-172">*Out of support*</span></span> |              |                             |              |              | <span data-ttu-id="92b28-173">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-173">Yes</span></span>          |
| <span data-ttu-id="92b28-174">Windows XP</span><span class="sxs-lookup"><span data-stu-id="92b28-174">Windows XP</span></span><br><span data-ttu-id="92b28-175">*Не поддерживается*</span><span class="sxs-lookup"><span data-stu-id="92b28-175">*Out of support*</span></span>          |              |                             |              | <span data-ttu-id="92b28-176">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-176">Yes</span></span>          | <span data-ttu-id="92b28-177">Да</span><span class="sxs-lookup"><span data-stu-id="92b28-177">Yes</span></span>          |

- <span data-ttu-id="92b28-178">**Входит в комплект поставки**: функции указанной версии WMF были включены в указанную версию клиента Windows или Windows Server.</span><span class="sxs-lookup"><span data-stu-id="92b28-178">**Ships in-box**: The features of the specified version of WMF were shipped in the indicated version of Windows client or Windows Server.</span></span>
- <span data-ttu-id="92b28-179">**Не поддерживается**: эти продукты больше не поддерживаются корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="92b28-179">**Out of support**: These products are no longer supported by Microsoft.</span></span> <span data-ttu-id="92b28-180">Необходимо обновить продукт до новой поддерживаемой версии.</span><span class="sxs-lookup"><span data-stu-id="92b28-180">You must upgrade to a new version that is supported.</span></span> <span data-ttu-id="92b28-181">Дополнительные сведения см. на странице [Политика жизненного цикла поддержки Майкрософт][].</span><span class="sxs-lookup"><span data-stu-id="92b28-181">For more information, see the [Microsoft Lifecycle Policy][] page.</span></span>

> [!NOTE]
> <span data-ttu-id="92b28-182">Установщик WMF 5.0 больше недоступен или не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="92b28-182">The installer for WMF 5.0 is no longer available or supported.</span></span> <span data-ttu-id="92b28-183">Он заменен на WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="92b28-183">It has been replaced by WMF 5.1.</span></span>

[Политика жизненного цикла поддержки Майкрософт]: https://support.microsoft.com/lifecycle
[Microsoft Lifecycle Policy]: https://support.microsoft.com/lifecycle
[WMF 5.1]: https://aka.ms/wmf51download
[WMF 5.1]: https://aka.ms/wmf51download
[WMF 4.0]: https://aka.ms/wmf4download
[WMF 4.0]: https://aka.ms/wmf4download
[WMF 3.0]: https://aka.ms/wmf3download
[WMF 3.0]: https://aka.ms/wmf3download
[WMF 2.0]: https://aka.ms/wmf2download
[WMF 2.0]: https://aka.ms/wmf2download