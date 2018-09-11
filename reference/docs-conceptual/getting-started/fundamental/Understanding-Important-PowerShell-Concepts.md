---
ms.date: 08/23/2018
keywords: powershell,командлет
title: Основные сведения о важных концепциях PowerShell
ms.assetid: 3e601e38-4520-4578-a48d-b6779f1d35ee
ms.openlocfilehash: 577ea0764a172e1821bc492417d8b4e546e31b0b
ms.sourcegitcommit: c170a1608d20d3c925d79c35fa208f650d014146
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2018
ms.locfileid: "43353200"
---
# <a name="understanding-important-powershell-concepts"></a><span data-ttu-id="4452f-103">Основные сведения о важных концепциях PowerShell</span><span class="sxs-lookup"><span data-stu-id="4452f-103">Understanding important PowerShell concepts</span></span>

<span data-ttu-id="4452f-104">Структура PowerShell вобрала в себя концепции из разных сред.</span><span class="sxs-lookup"><span data-stu-id="4452f-104">The PowerShell design integrates concepts from many different environments.</span></span> <span data-ttu-id="4452f-105">Некоторые из них знакомы пользователям с опытом работы в определенных оболочках или средах программирования.</span><span class="sxs-lookup"><span data-stu-id="4452f-105">Several of the concepts will be familiar to people with experience in shells or programming environments.</span></span> <span data-ttu-id="4452f-106">Но мало кто знает их все.</span><span class="sxs-lookup"><span data-stu-id="4452f-106">However, few people will know about all of them.</span></span> <span data-ttu-id="4452f-107">Обзор некоторых из этих концепций поможет лучше разобраться в работе оболочки.</span><span class="sxs-lookup"><span data-stu-id="4452f-107">Looking at some of these concepts provides a useful overview of the shell.</span></span>

## <a name="output-is-object-based"></a><span data-ttu-id="4452f-108">Выходные данные являются объектно-ориентированными</span><span class="sxs-lookup"><span data-stu-id="4452f-108">Output is object-based</span></span>

<span data-ttu-id="4452f-109">В отличие от средств распространенных интерфейсов командной строки командлеты PowerShell предназначены для работы с объектами.</span><span class="sxs-lookup"><span data-stu-id="4452f-109">Unlike traditional command-line interfaces, PowerShell cmdlets are designed to deal with objects.</span></span>
<span data-ttu-id="4452f-110">Объект — это не просто набор отображаемых на экране символов, а структурированные данные.</span><span class="sxs-lookup"><span data-stu-id="4452f-110">An object is structured information that is more than just the string of characters appearing on the screen.</span></span> <span data-ttu-id="4452f-111">Выходные данные команды всегда содержат дополнительную информацию, которую при необходимости можно использовать.</span><span class="sxs-lookup"><span data-stu-id="4452f-111">Command output always carries extra information that you can use if you need it.</span></span>

<span data-ttu-id="4452f-112">Если раньше вы использовали средства обработки текста для работы с данными, вы поймете, что в PowerShell они применяются иначе.</span><span class="sxs-lookup"><span data-stu-id="4452f-112">If you've used text-processing tools to process data in the past, you'll find that they behave differently when used in PowerShell.</span></span> <span data-ttu-id="4452f-113">В большинстве случаев для получения определенных сведений средства обработки текста не нужны.</span><span class="sxs-lookup"><span data-stu-id="4452f-113">In most cases, you don't need text-processing tools to extract specific information.</span></span> <span data-ttu-id="4452f-114">Стандартный синтаксис объекта PowerShell позволяет получить прямой доступ к фрагментам данных.</span><span class="sxs-lookup"><span data-stu-id="4452f-114">You directly access portions of the data using standard PowerShell object syntax.</span></span>

## <a name="the-command-family-is-extensible"></a><span data-ttu-id="4452f-115">Семейство команд является расширяемым</span><span class="sxs-lookup"><span data-stu-id="4452f-115">The command family is extensible</span></span>

<span data-ttu-id="4452f-116">Такие интерфейсы, как **cmd.exe**, не позволяют расширить набор встроенных команд напрямую.</span><span class="sxs-lookup"><span data-stu-id="4452f-116">Interfaces such as **cmd.exe**don't provide a way for you to directly extend the built-in command set.</span></span> <span data-ttu-id="4452f-117">Можно создать внешние программы командной строки, которые выполняются в **cmd.exe**.</span><span class="sxs-lookup"><span data-stu-id="4452f-117">You can create external command-line tools that run in **cmd.exe**.</span></span> <span data-ttu-id="4452f-118">Но у этих внешних программ нет служб, таких как интеграция справки.</span><span class="sxs-lookup"><span data-stu-id="4452f-118">But these external tools don't have services, such as Help integration.</span></span> <span data-ttu-id="4452f-119">**Cmd.exe** не может автоматически определить, что такие средства являются допустимыми командами.</span><span class="sxs-lookup"><span data-stu-id="4452f-119">**cmd.exe**doesn't automatically know that these external tools are valid commands.</span></span>

<span data-ttu-id="4452f-120">Собственные команды PowerShell называются *командлетами*.</span><span class="sxs-lookup"><span data-stu-id="4452f-120">The native commands in PowerShell are known as *cmdlets* (pronounced command-lets).</span></span> <span data-ttu-id="4452f-121">Можно самостоятельно создавать командлеты, модули и функции, используя скомпилированный код или скрипты.</span><span class="sxs-lookup"><span data-stu-id="4452f-121">You can create your own cmdlets modules and functions using compiled code or scripts.</span></span> <span data-ttu-id="4452f-122">Модули могут добавлять командлеты и поставщики в оболочку.</span><span class="sxs-lookup"><span data-stu-id="4452f-122">Modules can add cmdlets and providers to the shell.</span></span> <span data-ttu-id="4452f-123">PowerShell также поддерживает скрипты, которые аналогичны скриптам оболочки UNIX и пакетным файлам **cmd.exe**.</span><span class="sxs-lookup"><span data-stu-id="4452f-123">PowerShell also supports scripts that are analogous to UNIX shell scripts and **cmd.exe** batch files.</span></span>

## <a name="powershell-handles-console-input-and-display"></a><span data-ttu-id="4452f-124">PowerShell обрабатывает ввод и отображение данных в консоли</span><span class="sxs-lookup"><span data-stu-id="4452f-124">PowerShell handles console input and display</span></span>

<span data-ttu-id="4452f-125">Когда вы вводите команду, PowerShell всегда обрабатывает входные данные командной строки напрямую.</span><span class="sxs-lookup"><span data-stu-id="4452f-125">When you type a command, PowerShell always processes the command-line input directly.</span></span> <span data-ttu-id="4452f-126">PowerShell также форматирует выходные данные, отображаемые на экране.</span><span class="sxs-lookup"><span data-stu-id="4452f-126">PowerShell also formats the output that you see on the screen.</span></span> <span data-ttu-id="4452f-127">Это важно, так как нагрузка, требуемая для обработки каждого командлета, сокращается,</span><span class="sxs-lookup"><span data-stu-id="4452f-127">This difference is significant because it reduces the work required of each cmdlet.</span></span> <span data-ttu-id="4452f-128">и действия выполняются аналогичным образом независимо от используемого командлета.</span><span class="sxs-lookup"><span data-stu-id="4452f-128">It ensures that you can always do things the same way with any cmdlet.</span></span> <span data-ttu-id="4452f-129">Разработчикам командлетов не нужно писать код для синтаксического анализа аргументов командной строки или форматирования выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4452f-129">Cmdlet developers don't need to write code to parse the command-line arguments or format the output.</span></span>

<span data-ttu-id="4452f-130">Традиционные программы командной строки используют собственные схемы для запроса и отображения справки.</span><span class="sxs-lookup"><span data-stu-id="4452f-130">Traditional command-line tools have their own schemes for requesting and displaying Help.</span></span> <span data-ttu-id="4452f-131">Некоторые программы используют **/?**</span><span class="sxs-lookup"><span data-stu-id="4452f-131">Some command-line tools use **/?**</span></span> <span data-ttu-id="4452f-132">для отображения справки. Другие используют **-?**, **/H** или даже **//**.</span><span class="sxs-lookup"><span data-stu-id="4452f-132">to trigger the Help display; others use **-?**, **/H**, or even **//**.</span></span> <span data-ttu-id="4452f-133">Некоторые отображают справку в окне графического пользовательского интерфейса, а не в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="4452f-133">Some will display Help in a GUI window, rather than in the console display.</span></span> <span data-ttu-id="4452f-134">Если введен неправильный параметр, средство может проигнорировать ошибку и автоматически начать выполнение задачи.</span><span class="sxs-lookup"><span data-stu-id="4452f-134">If you use the wrong parameter, the tool might ignore what you typed and begin executing a task automatically.</span></span>
<span data-ttu-id="4452f-135">PowerShell автоматически анализирует и обрабатывает все вводимые данные. Поэтому указание параметра **-?**</span><span class="sxs-lookup"><span data-stu-id="4452f-135">Since PowerShell automatically parses and processes the command line, the **-?**</span></span> <span data-ttu-id="4452f-136">всегда означает запрос на вывод справки об этой команде.</span><span class="sxs-lookup"><span data-stu-id="4452f-136">parameter always means "show me Help for this command".</span></span>

> [!NOTE]
> <span data-ttu-id="4452f-137">Когда вы запускаете в PowerShell графическое приложение, для него открывается окно.</span><span class="sxs-lookup"><span data-stu-id="4452f-137">If you run a graphic application in PowerShell, the window for the application opens.</span></span>
> <span data-ttu-id="4452f-138">PowerShell вмешивается в процесс только при обработке заданных вами в командной строке входных данных или при возврате выходных данных приложения в окно консоли.</span><span class="sxs-lookup"><span data-stu-id="4452f-138">PowerShell intervenes only when processing the command-line input you supply or the application output returned to the console window.</span></span> <span data-ttu-id="4452f-139">На внутреннюю работу приложения система не влияет.</span><span class="sxs-lookup"><span data-stu-id="4452f-139">It does not affect how the application works internally.</span></span>

## <a name="powershell-uses-some-c-syntax"></a><span data-ttu-id="4452f-140">PowerShell использует некоторую часть синтаксиса C#</span><span class="sxs-lookup"><span data-stu-id="4452f-140">PowerShell uses some C# syntax</span></span>

<span data-ttu-id="4452f-141">В основе PowerShell лежит .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4452f-141">PowerShell is built on the .NET Framework.</span></span> <span data-ttu-id="4452f-142">Также PowerShell содержит некоторые функции и ключевые слова синтаксиса языка программирования C#.</span><span class="sxs-lookup"><span data-stu-id="4452f-142">It shares some syntax features and keywords with the C# programming language.</span></span> <span data-ttu-id="4452f-143">Изучение PowerShell может значительно упростить освоение C#.</span><span class="sxs-lookup"><span data-stu-id="4452f-143">Learning PowerShell can make it much easier to learn C#.</span></span> <span data-ttu-id="4452f-144">Если же вы знакомы с C#, вам также будет проще изучать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4452f-144">If you're already familiar with C#, these similarities can make learning PowerShell easier.</span></span>