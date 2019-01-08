---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Параметры учетных данных в данных конфигурации
ms.openlocfilehash: 10cf3456fcc7104b7dd779db30aebace54ba087a
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046647"
---
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="10b1d-103">Параметры учетных данных в данных конфигурации</span><span class="sxs-lookup"><span data-stu-id="10b1d-103">Credentials Options in Configuration Data</span></span>
><span data-ttu-id="10b1d-104">Область применения. Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="10b1d-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="10b1d-105">Пароли в виде простого текста и пользователи домена</span><span class="sxs-lookup"><span data-stu-id="10b1d-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="10b1d-106">При использовании конфигураций DSC, содержащих незашифрованные учетные данные, выдается сообщение об ошибке из-за указания паролей в виде простого текста.</span><span class="sxs-lookup"><span data-stu-id="10b1d-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="10b1d-107">Кроме того, DSC выдает предупреждение при использовании учетных данных домена.</span><span class="sxs-lookup"><span data-stu-id="10b1d-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="10b1d-108">Чтобы не получать такие ошибки и предупреждения, используйте следующие ключевые слова в данных конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="10b1d-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>
* <span data-ttu-id="10b1d-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="10b1d-109">**PsDscAllowPlainTextPassword**</span></span>
* <span data-ttu-id="10b1d-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="10b1d-110">**PsDscAllowDomainUser**</span></span>

> [!NOTE]
> <span data-ttu-id="10b1d-111">Хранение и передача незашифрованных паролей с простым текстом обычно являются небезопасными.</span><span class="sxs-lookup"><span data-stu-id="10b1d-111">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="10b1d-112">Рекомендуется использовать методы защиты учетных данных, описанные далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="10b1d-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>
> <span data-ttu-id="10b1d-113">Служба Azure Automation DSC позволяет вам централизованно управлять учетными данными, включать их в конфигурации и обеспечивать безопасное хранение.</span><span class="sxs-lookup"><span data-stu-id="10b1d-113">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>
> <span data-ttu-id="10b1d-114">Подробнее: [Компиляция конфигураций DSC / ресурсы учетных данных](/azure/automation/automation-dsc-compile#credential-assets)</span><span class="sxs-lookup"><span data-stu-id="10b1d-114">For information, see: [Compiling DSC Configurations / Credential Assets](/azure/automation/automation-dsc-compile#credential-assets)</span></span>

<span data-ttu-id="10b1d-115">Ниже приведен пример передачи учетных данных в виде открытого текста:</span><span class="sxs-lookup"><span data-stu-id="10b1d-115">The following is an example of passing plain text credentials:</span></span>

```powershell
#Prompt user for their credentials
#credentials will be unencrypted in the MOF
$promptedCreds = get-credential -Message "Please enter your credentials to generate a DSC MOF:"

# Store passwords in plaintext, in the document itself
# will also be stored in plaintext in the mof
$password = "ThisIsAPlaintextPassword" | ConvertTo-SecureString -asPlainText -Force
$username = "User1"
[PSCredential] $credential = New-Object System.Management.Automation.PSCredential($username,$password)

# DSC requires explicit confirmation before storing passwords insecurely
$ConfigurationData = @{
    AllNodes = @(
            @{
                # The "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves
                NodeName="*"
                PSDscAllowPlainTextPassword = $true
            },
            #however, each node still needs to be explicitly defined for "*" to have meaning
            @{
                NodeName = "TestMachine1"
            },
            #we can also use a property to define node-specific passwords, although this is no more secure
            @{
                NodeName = "TestMachine2";
                UserName = "User2"
                LocalPassword = "ThisIsYetAnotherPlaintextPassword"
            }
        )
}

configuration unencryptedPasswordDemo
{
    Node "TestMachine1"
    {
        # We use the plaintext password to generate a new account
        User User1
        {
            UserName = $username
            Password = $credential
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }
        # We use the prompted password to add this account to the local admins group
        Group addToAdmin
        {
            # Ensure the user exists before we add the user to a group
            DependsOn = "[User]User1"
            Credential = $promptedCreds
            GroupName = "Administrators"
            Ensure = "Present"
            MembersToInclude = "User1"
        }
    }

    Node "TestMachine2"
    {
        # Now we'll use a node-specific password to this machine
        $password = $Node.LocalPassword | ConvertTo-SecureString -asPlainText -Force
        $username = $node.UserName
        [PSCredential] $nodeCred = New-Object System.Management.Automation.PSCredential($username,$password)

        User User2
        {
            UserName = $username
            Password = $nodeCred
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }

        Group addToAdmin
        {
            Credential = $promptedCreds
            GroupName = "Administrators"
            DependsOn = "[User]User2"
            Ensure = "Present"
            MembersToInclude = "User2"
        }
    }
}

# We declared the ConfigurationData in a local variable, but we need to pass it
# in to our configuration function
# We need to invoke the configuration function we created to generate a MOF
unencryptedPasswordDemo -ConfigurationData $ConfigurationData

# We need to pass the MOF to the machines we named.
#-wait: doesn't use jobs so we get blocked at the prompt until the configuration is done
#-verbose: so we can see what's going on and catch any errors
#-force: for testing purposes, I run start-dscconfiguration frequently + want to make sure i'm
#        not blocked by previous configurations that are still running
Start-DscConfiguration ./unencryptedPasswordDemo -verbose -wait -force
```

<span data-ttu-id="10b1d-116">Это выдержка из файла «.mof», создаваемая конфигурацией для «TestMachine1».</span><span class="sxs-lookup"><span data-stu-id="10b1d-116">This is an excerpt from the ".mof" file generated by the configuration for "TestMachine1".</span></span> <span data-ttu-id="10b1d-117">`System.Security.SecureString` Используется в конфигурации было преобразованию в неформатированный текст и сохранено в файле «.mof» в качестве `MSF_Credential`.</span><span class="sxs-lookup"><span data-stu-id="10b1d-117">The `System.Security.SecureString` used in the configuration was converted to plain text and stored in the ".mof" file as a `MSF_Credential`.</span></span> <span data-ttu-id="10b1d-118">Объект `SecureString` шифруется с использованием текущего профиля пользователей.</span><span class="sxs-lookup"><span data-stu-id="10b1d-118">A `SecureString` is encrypted with the current users profile.</span></span> <span data-ttu-id="10b1d-119">Это подходит для всех форм удаленное управление PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10b1d-119">This works well with all forms of PowerShell remote management.</span></span> <span data-ttu-id="10b1d-120">Механизм только конфигурации, автономный предназначен MOF «-» файла.</span><span class="sxs-lookup"><span data-stu-id="10b1d-120">A ".mof" file is designed to be a stand alone configuration mechanism.</span></span> <span data-ttu-id="10b1d-121">Начиная с PowerShell 5.0, MOF-файлы на узле, шифруются при хранении, но не в пути к узлу.</span><span class="sxs-lookup"><span data-stu-id="10b1d-121">Beginning in PowerShell 5.0, ".mof" files on a Node are encrypted at rest, but not in transit to the Node.</span></span> <span data-ttu-id="10b1d-122">Это означает, что пароли в файле «.mof» представляются как открытым текстом, при их применении к узлу.</span><span class="sxs-lookup"><span data-stu-id="10b1d-122">This means that passwords in a ".mof" file are exposed as clear text when you apply them to a Node.</span></span> <span data-ttu-id="10b1d-123">Чтобы зашифровать учетные данные, необходимо использовать **опрашивающего сервера**.</span><span class="sxs-lookup"><span data-stu-id="10b1d-123">To encrypt credentials, you need to use a **Pull Server**.</span></span> <span data-ttu-id="10b1d-124">Дополнительные сведения см. в разделе [защита MOF-файлов с помощью сертификатов](../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="10b1d-124">For more information, see [Securing MOF files with Certificates](../pull-server/secureMOF.md).</span></span>

```syntax
instance of MSFT_Credential as $MSFT_Credential1ref
{
Password = "ThisIsYetAnotherPlaintextPassword";
 UserName = "User2";

};

instance of MSFT_UserResource as $MSFT_UserResource1ref
{
ResourceID = "[User]User2";
 Description = "local account";
 UserName = "User2";
 Ensure = "Present";
 Password = $MSFT_Credential1ref;
 Disabled = False;
 SourceInfo = "::66::9::User";
 PasswordNeverExpires = True;
 ModuleName = "PsDesiredStateConfiguration";
 PasswordChangeRequired = False;

ModuleVersion = "1.0";

 ConfigurationName = "unencryptedPasswordDemo";

};
```

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="10b1d-125">Обработка учетных данных в DSC</span><span class="sxs-lookup"><span data-stu-id="10b1d-125">Handling Credentials in DSC</span></span>

<span data-ttu-id="10b1d-126">По умолчанию ресурсы DSC запускаются от имени `Local System`.</span><span class="sxs-lookup"><span data-stu-id="10b1d-126">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="10b1d-127">При этом некоторые ресурсы требуют учетных данных, например, если ресурсу `Package` необходимо установить программное обеспечение с помощью учетной записи определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="10b1d-127">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="10b1d-128">В более ранних ресурсах для этого использовалось прописываемое в коде свойство `Credential`.</span><span class="sxs-lookup"><span data-stu-id="10b1d-128">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="10b1d-129">В WMF 5.0 для всех ресурсов было добавлено автоматическое свойство `PsDscRunAsCredential`.</span><span class="sxs-lookup"><span data-stu-id="10b1d-129">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="10b1d-130">Дополнительные сведения об использовании `PsDscRunAsCredential` см. в разделе [Запуск DSC с учетными данными пользователя](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="10b1d-130">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="10b1d-131">Новые и настраиваемые ресурсы позволяют использовать это автоматическое свойство вместо создания отдельного свойства для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="10b1d-131">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="10b1d-132">Некоторые виды ресурсов используют множество учетных данных для определенной цели. Такие ресурсы имеют собственные свойства учетных данных.</span><span class="sxs-lookup"><span data-stu-id="10b1d-132">The design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="10b1d-133">Чтобы найти доступные свойства учетных данных ресурса, используйте `Get-DscResource -Name ResourceName -Syntax` или Intellisense в интегрированной среде сценариев (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="10b1d-133">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

```powershell
PS C:\> Get-DscResource -Name Group -Syntax
Group [String] #ResourceName
{
    GroupName = [string]
    [Credential = [PSCredential]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Members = [string[]]]
    [MembersToExclude = [string[]]]
    [MembersToInclude = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

<span data-ttu-id="10b1d-134">В этом примере используется ресурс [Group](../resources/resources.md) из встроенного модуля ресурсов DSC `PSDesiredStateConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="10b1d-134">This example uses a [Group](../resources/resources.md) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="10b1d-135">Он может создавать локальные группы, а также добавлять и удалять члены.</span><span class="sxs-lookup"><span data-stu-id="10b1d-135">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="10b1d-136">Этот ресурс принимает как свойство `Credential`, так и автоматическое свойство `PsDscRunAsCredential`,</span><span class="sxs-lookup"><span data-stu-id="10b1d-136">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="10b1d-137">но использует только свойство `Credential`.</span><span class="sxs-lookup"><span data-stu-id="10b1d-137">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="10b1d-138">См. дополнительные сведения о свойстве `PsDscRunAsCredential` и [запуске DSC с учетными данными пользователя](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="10b1d-138">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="10b1d-139">Пример: Ресурс группы свойство учетных данных</span><span class="sxs-lookup"><span data-stu-id="10b1d-139">Example: The Group resource Credential property</span></span>

<span data-ttu-id="10b1d-140">DSC выполняется в качестве `Local System`, поэтому уже имеет разрешения на изменение локальных пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="10b1d-140">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="10b1d-141">Если в локальную учетную группу добавляется новый пользователь, учетные данные не требуются.</span><span class="sxs-lookup"><span data-stu-id="10b1d-141">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="10b1d-142">Но если ресурс `Group` добавляет учетную запись домена в локальную группу, учетные данные необходимы.</span><span class="sxs-lookup"><span data-stu-id="10b1d-142">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="10b1d-143">Анонимные запросы к Active Directory не допускаются.</span><span class="sxs-lookup"><span data-stu-id="10b1d-143">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="10b1d-144">Свойство `Credential` ресурса `Group` — это учетная запись домена, которая используется для запросов к Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10b1d-144">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="10b1d-145">В большинстве случаев это может быть универсальная учетная запись пользователя, поскольку пользователи по умолчанию могут *читать* большинство объектов в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10b1d-145">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="10b1d-146">Пример конфигурации</span><span class="sxs-lookup"><span data-stu-id="10b1d-146">Example Configuration</span></span>

<span data-ttu-id="10b1d-147">В следующем примере кода DSC используется для добавления пользователя домена в локальную группу:</span><span class="sxs-lookup"><span data-stu-id="10b1d-147">The following example code uses DSC to populate a local group with a domain user:</span></span>

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred
```

<span data-ttu-id="10b1d-148">Этот код вызывает ошибку и предупреждение:</span><span class="sxs-lookup"><span data-stu-id="10b1d-148">This code generates both an error and warning message:</span></span>

```
ConvertTo-MOFInstance : System.InvalidOperationException error processing
property 'Credential' OF TYPE 'Group': Converting and storing encrypted
passwords as plain text is not recommended. For more information on securing
credentials in MOF file, please refer to MSDN blog:
http://go.microsoft.com/fwlink/?LinkId=393729

At line:11 char:9
+   Group
At line:297 char:16
+     $aliasId = ConvertTo-MOFInstance $keywordName $canonicalizedValue
+                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessProperty,ConvertTo-MOFInstance

WARNING: It is not recommended to use domain credential for node 'localhost'.
In order to suppress the warning, you can add a property named
'PSDscAllowDomainUser' with a value of $true to your DSC configuration data
for node 'localhost'.
```

<span data-ttu-id="10b1d-149">В этом примере есть две проблемы:</span><span class="sxs-lookup"><span data-stu-id="10b1d-149">This example has two issues:</span></span>
1. <span data-ttu-id="10b1d-150">Ошибка с указанием на то, что использовать пароли в виде простого текста не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="10b1d-150">An error explains that plain text passwords are not recommended</span></span>
2. <span data-ttu-id="10b1d-151">Предупреждение с рекомендацией не использовать доменные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="10b1d-151">A warning advises against using a domain credential</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="10b1d-152">PsDscAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="10b1d-152">PsDscAllowPlainTextPassword</span></span>

<span data-ttu-id="10b1d-153">В первом сообщении об ошибке находится URL-адрес документации.</span><span class="sxs-lookup"><span data-stu-id="10b1d-153">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="10b1d-154">Он содержит инструкции по шифрованию паролей с использованием структуры [ConfigurationData](./configData.md) и сертификата.</span><span class="sxs-lookup"><span data-stu-id="10b1d-154">This link explains how to encrypt passwords using a [ConfigurationData](./configData.md) structure and a certificate.</span></span>
<span data-ttu-id="10b1d-155">Дополнительные сведения о сертификатах в DSC см. в [этой записи](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="10b1d-155">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="10b1d-156">Чтобы принудительно использовать пароль в виде простого текста, необходимо добавить в раздел данных конфигурации ресурса ключ `PsDscAllowPlainTextPassword` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="10b1d-156">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowPlainTextPassword = $true
        }
    )
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred -ConfigurationData $cd
```

> [!NOTE]
> <span data-ttu-id="10b1d-157">`NodeName` не может равняться звездочке. Обязательно укажите имя конкретного узла.</span><span class="sxs-lookup"><span data-stu-id="10b1d-157">`NodeName` cannot equal asterisk, a specific node name is mandatory.</span></span>

<span data-ttu-id="10b1d-158">**Корпорация Майкрософт не рекомендует использовать пароли в виде простого текста из-за серьезной угрозы безопасности.**</span><span class="sxs-lookup"><span data-stu-id="10b1d-158">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="10b1d-159">Доменные учетные данные</span><span class="sxs-lookup"><span data-stu-id="10b1d-159">Domain Credentials</span></span>

<span data-ttu-id="10b1d-160">Выполнив сценарий конфигурации из примера еще раз (с шифрованием или без), вы снова получите предупреждение о том, что использовать доменную учетную запись в качестве учетных данных не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="10b1d-160">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="10b1d-161">Пользуясь для этой цели локальной учетной записью, вы защитите от риска доменные учетные данные, которые можно использовать на других серверах.</span><span class="sxs-lookup"><span data-stu-id="10b1d-161">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="10b1d-162">**Используя учетные данные с ресурсами DSC, по возможности отдавайте предпочтение локальной учетной записи, а не доменной.**</span><span class="sxs-lookup"><span data-stu-id="10b1d-162">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="10b1d-163">Если свойство `Username` учетных данных содержит \' или @, DSC будет рассматривать их как доменную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="10b1d-163">If there is a '\' or '@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="10b1d-164">Исключение составляют значения localhost, 127.0.0.1 и ::1 в доменной части имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="10b1d-164">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="10b1d-165">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="10b1d-165">PSDscAllowDomainUser</span></span>

<span data-ttu-id="10b1d-166">В приведенном выше примере ресурса `Group` DSC для запроса к домену Active Directory *требуется* доменная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="10b1d-166">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="10b1d-167">В этом случае добавьте свойство `PSDscAllowDomainUser` в блок `ConfigurationData` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="10b1d-167">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

```powershell
$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowDomainUser = $true
            # PSDscAllowPlainTextPassword = $true
            CertificateFile = "C:\PublicKeys\server1.cer"
        }
    )
}
```

<span data-ttu-id="10b1d-168">После этого сценарий конфигурации создаст MOF-файл без ошибок или предупреждений.</span><span class="sxs-lookup"><span data-stu-id="10b1d-168">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>