---
ms.date: 06/12/2017
contributor: JKeithB
keywords: коллекции,powershell,командлет,psgallery
title: Фильтрация результатов поиска
ms.openlocfilehash: 13270a310613a974e1588a9f56d443a936cfebb8
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50003939"
---
# <a name="filtering-search-results"></a><span data-ttu-id="ddedb-103">Фильтрация результатов поиска</span><span class="sxs-lookup"><span data-stu-id="ddedb-103">Filtering search results</span></span>

<span data-ttu-id="ddedb-104">На [вкладке "Пакеты"](https://www.powershellgallery.com/packages) отображаются все доступные пакеты в коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddedb-104">The [Packages tab](https://www.powershellgallery.com/packages) displays all available packages in the PowerShell Gallery.</span></span>

<span data-ttu-id="ddedb-105">Есть несколько способов фильтрации, сортировки и поиска пакетов.</span><span class="sxs-lookup"><span data-stu-id="ddedb-105">There are several ways to filter, sort, and search the packages.</span></span>
<span data-ttu-id="ddedb-106">Чтобы узнать больше об определенном пакете, щелкните его.</span><span class="sxs-lookup"><span data-stu-id="ddedb-106">To see more details about a particular package, click the package.</span></span>

## <a name="filter-by"></a><span data-ttu-id="ddedb-107">Фильтровать по</span><span class="sxs-lookup"><span data-stu-id="ddedb-107">Filter By</span></span>

<span data-ttu-id="ddedb-108">В раскрывающемся списке в разделе "Фильтровать по" можно отфильтровать результаты по следующим параметрам:</span><span class="sxs-lookup"><span data-stu-id="ddedb-108">The drop-down under "Filter By" allows users to filter the results by:</span></span>
- <span data-ttu-id="ddedb-109">"Включить предварительные выпуски";</span><span class="sxs-lookup"><span data-stu-id="ddedb-109">Include Prerelease</span></span>
- <span data-ttu-id="ddedb-110">"Только стабильные".</span><span class="sxs-lookup"><span data-stu-id="ddedb-110">Stable Only</span></span>

<span data-ttu-id="ddedb-111">Сведения о параметрах "Предварительный выпуск" и "Стабильный" см. в статье о [добавленной функции управления предварительными выпусками в PowerShellGet и коллекции PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) в блоге команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddedb-111">For information about "Prerelease" and "Stable", see [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) in the PowerShell Team Blog.</span></span>

<span data-ttu-id="ddedb-112">Установив флажки в раскрывающемся списке, можно отфильтровать результаты по:</span><span class="sxs-lookup"><span data-stu-id="ddedb-112">The checkboxes under the drop-down allow users to filter the results by:</span></span>
- <span data-ttu-id="ddedb-113">Типы пакетов</span><span class="sxs-lookup"><span data-stu-id="ddedb-113">Package Types</span></span>
  - <span data-ttu-id="ddedb-114">Модуль</span><span class="sxs-lookup"><span data-stu-id="ddedb-114">Module</span></span>
  - <span data-ttu-id="ddedb-115">Скрипт</span><span class="sxs-lookup"><span data-stu-id="ddedb-115">Script</span></span>
- <span data-ttu-id="ddedb-116">Категории</span><span class="sxs-lookup"><span data-stu-id="ddedb-116">Categories</span></span>
  - <span data-ttu-id="ddedb-117">Командлет</span><span class="sxs-lookup"><span data-stu-id="ddedb-117">Cmdlet</span></span>
  - <span data-ttu-id="ddedb-118">Ресурс DSC</span><span class="sxs-lookup"><span data-stu-id="ddedb-118">DSC Resource</span></span>
  - <span data-ttu-id="ddedb-119">Функция</span><span class="sxs-lookup"><span data-stu-id="ddedb-119">Function</span></span>
  - <span data-ttu-id="ddedb-120">Возможность роли</span><span class="sxs-lookup"><span data-stu-id="ddedb-120">Role Capability</span></span>
  - <span data-ttu-id="ddedb-121">Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="ddedb-121">Workflow</span></span>

<span data-ttu-id="ddedb-122">Чтобы просмотреть только модули в коллекции PowerShell, щелкните "Модуль" в списке типов пакетов.</span><span class="sxs-lookup"><span data-stu-id="ddedb-122">To see only modules in the PowerShell Gallery, check Module in the Package Types.</span></span>
<span data-ttu-id="ddedb-123">Аналогичным образом, чтобы просмотреть только скрипты в коллекции PowerShell, щелкните "Скрипт" в списке с типами пакетов.</span><span class="sxs-lookup"><span data-stu-id="ddedb-123">Similarly, to see only scripts in the PowerShell Gallery, check Script in the Package Types.</span></span>

> [!NOTE]
> <span data-ttu-id="ddedb-124">При обработке фильтрами используется инклюзивный подход.</span><span class="sxs-lookup"><span data-stu-id="ddedb-124">Filters are inclusive.</span></span>
> <span data-ttu-id="ddedb-125">Пример. Пакет, содержащий командлеты и функции, будет отображаться при выборе категорий "Командлет" или "Функция" (как по-отдельности, так и вместе).</span><span class="sxs-lookup"><span data-stu-id="ddedb-125">Example: A package containing both cmdlets and functions will appear if either Cmdlet or Function (or both) are checked.</span></span>
> <span data-ttu-id="ddedb-126">Если ни одна из этих категорий не выбрана, пакет не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="ddedb-126">If neither are selected, the package will not appear.</span></span>
> <span data-ttu-id="ddedb-127">Аналогично, если выбираются все категории, будут отображаться только пакеты, содержащие хотя бы одну из этих категорий.</span><span class="sxs-lookup"><span data-stu-id="ddedb-127">Similarly, if all categories are selected, only packages containing one of those categories will appear.</span></span>
> <span data-ttu-id="ddedb-128">**Пакеты, которые не принадлежат ни к одной из этих категорий, отображаться не будут.**</span><span class="sxs-lookup"><span data-stu-id="ddedb-128">**Packages that do not belong to any of those categories will not appear.**</span></span>

## <a name="sort-by"></a><span data-ttu-id="ddedb-129">Сортировать по</span><span class="sxs-lookup"><span data-stu-id="ddedb-129">Sort By</span></span>

<span data-ttu-id="ddedb-130">Раскрывающийся список "Сортировать по" позволяет сортировать результаты по следующим параметрам:</span><span class="sxs-lookup"><span data-stu-id="ddedb-130">The Sort By drop-down allows users to sort the results by:</span></span>
- <span data-ttu-id="ddedb-131">"Популярность" — определяется по числу скачиваний;</span><span class="sxs-lookup"><span data-stu-id="ddedb-131">Popularity - Popularity is determined by Download Count</span></span>
- <span data-ttu-id="ddedb-132">A–Z — в алфавитном порядке по имени пакета;</span><span class="sxs-lookup"><span data-stu-id="ddedb-132">A-Z - Alphabetically by package name</span></span>
- <span data-ttu-id="ddedb-133">"Последние" — пакеты располагаются по дате их публикации.</span><span class="sxs-lookup"><span data-stu-id="ddedb-133">Recent - Packages appear in order of publish date</span></span>

## <a name="search-box"></a><span data-ttu-id="ddedb-134">Поле поиска</span><span class="sxs-lookup"><span data-stu-id="ddedb-134">Search Box</span></span>

<span data-ttu-id="ddedb-135">Поле поиска позволяет искать пакеты по ключевым словам.</span><span class="sxs-lookup"><span data-stu-id="ddedb-135">The Search Box allows users to search the packages on keywords.</span></span>
<span data-ttu-id="ddedb-136">Дополнительные сведения см. в статье [Синтаксис поиска по коллекции](search-syntax.md).</span><span class="sxs-lookup"><span data-stu-id="ddedb-136">For more information, see [Gallery Search Syntax](search-syntax.md).</span></span>