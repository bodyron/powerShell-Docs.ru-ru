---
ms.date: 12/31/2019
keywords: powershell,командлет
title: Объект ISEMenuItem
ms.openlocfilehash: c3ffe6e8f0b28987543fe0a873c552292dc5158a
ms.sourcegitcommit: 2aec310ad0c0b048400cb56f6fa64c1e554c812a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2020
ms.locfileid: "83809320"
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="0746b-103">Объект ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="0746b-103">The ISEMenuItem Object</span></span>

<span data-ttu-id="0746b-104">Объект **ISEMenuItem** является экземпляром класса **Microsoft.PowerShell.Host.ISE.ISEMenuItem**.</span><span class="sxs-lookup"><span data-stu-id="0746b-104">An **ISEMenuItem** object is an instance of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>
<span data-ttu-id="0746b-105">Все объекты в меню **Надстройки** являются экземплярами класса **Microsoft.PowerShell.Host.ISE.ISEMenuItem**.</span><span class="sxs-lookup"><span data-stu-id="0746b-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="0746b-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="0746b-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="0746b-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="0746b-107">DisplayName</span></span>

<span data-ttu-id="0746b-108">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="0746b-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0746b-109">Свойство только для чтения, которое получает отображаемое имя пункта меню.</span><span class="sxs-lookup"><span data-stu-id="0746b-109">The read-only property that gets the display name of the menu item.</span></span>

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a><span data-ttu-id="0746b-110">Действие</span><span class="sxs-lookup"><span data-stu-id="0746b-110">Action</span></span>

<span data-ttu-id="0746b-111">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="0746b-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0746b-112">Свойство только для чтения, которое получает блок сценария.</span><span class="sxs-lookup"><span data-stu-id="0746b-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="0746b-113">Оно вызывает действие при щелчке по элементу меню.</span><span class="sxs-lookup"><span data-stu-id="0746b-113">It invokes the action when you click the menu item.</span></span>

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="0746b-114">Клавиша</span><span class="sxs-lookup"><span data-stu-id="0746b-114">Shortcut</span></span>

<span data-ttu-id="0746b-115">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="0746b-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0746b-116">Свойство только для чтения, которое получает сочетания клавиш Windows для пункта меню.</span><span class="sxs-lookup"><span data-stu-id="0746b-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="0746b-117">Подменю</span><span class="sxs-lookup"><span data-stu-id="0746b-117">Submenus</span></span>

<span data-ttu-id="0746b-118">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="0746b-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0746b-119">Свойство только для чтения, которое получает [список подменю](The-ISEMenuItemCollection-Object.md) для пункта меню.</span><span class="sxs-lookup"><span data-stu-id="0746b-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="0746b-120">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="0746b-120">Scripting example</span></span>

<span data-ttu-id="0746b-121">Чтобы лучше понять, как пользоваться меню надстроек и его свойствами с поддержкой сценариев, прочтите следующий пример сценария.</span><span class="sxs-lookup"><span data-stu-id="0746b-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

```powershell
# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu - a parent and a child submenu item.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
```

## <a name="see-also"></a><span data-ttu-id="0746b-122">См. также:</span><span class="sxs-lookup"><span data-stu-id="0746b-122">See Also</span></span>

- [<span data-ttu-id="0746b-123">Объект ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="0746b-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md)
- [<span data-ttu-id="0746b-124">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0746b-124">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="0746b-125">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="0746b-125">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)