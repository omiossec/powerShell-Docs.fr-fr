---
ms.date: 2017-08-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: Notes de publication de WMF 5.1
ms.openlocfilehash: 3a6b7fb84d679d9bbe7a89e30c8c769e26f7381a
ms.sourcegitcommit: 3f49bd2e0b786e69c71393c00ad85d05a8466753
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/04/2017
---
# <a name="windows-management-framework-wmf-51"></a><span data-ttu-id="99166-103">Windows Management Framework (WMF) 5.1</span><span class="sxs-lookup"><span data-stu-id="99166-103">Windows Management Framework (WMF) 5.1</span></span> #

<span data-ttu-id="99166-104">WMF offre aux utilisateurs la possibilité de mettre à jour les systèmes Windows existants avec les versions des composants PowerShell, WMI, WinRM et SIL (Journalisation de l’inventaire logiciel) qui ont été publiées avec Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="99166-104">WMF provides users with the ability to update existing Windows systems to the versions of PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span> 

<span data-ttu-id="99166-105">WMF 5.1 peut être installé sur Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 et 2012 R2, et fournit plusieurs améliorations par rapport à WMF 5.0 RTM, notamment :</span><span class="sxs-lookup"><span data-stu-id="99166-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="99166-106">Nouvelles applets de commande : groupes et utilisateurs locaux ; Get-ComputerInfo</span><span class="sxs-lookup"><span data-stu-id="99166-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="99166-107">Améliorations de PowerShellGet avec l’utilisation imposée de modules signés et l’installation de modules JEA</span><span class="sxs-lookup"><span data-stu-id="99166-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="99166-108">Ajout de la prise en charge de PackageManagement pour les conteneurs, l’installation de CBS, l’installation basée sur des fichiers .exe et les packages CAB</span><span class="sxs-lookup"><span data-stu-id="99166-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="99166-109">Améliorations du débogage pour les classes DSC et PowerShell</span><span class="sxs-lookup"><span data-stu-id="99166-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="99166-110">Améliorations de la sécurité, notamment l’utilisation imposée de modules signés par le catalogue provenant du serveur collecteur et lors de l’utilisation des applets de commande PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="99166-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="99166-111">Réponses à plusieurs demandes et problèmes des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="99166-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="99166-112">Pour connaître les nouveautés de cette version, parcourez les rubriques listées sous [Nouveaux scénarios et fonctionnalités](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features).</span><span class="sxs-lookup"><span data-stu-id="99166-112">To learn about what is new in this release, browse the topics listed under [New Scenarios and Features](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features).</span></span> 

<span data-ttu-id="99166-113">La rubrique [Installer et configurer](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) décrit la configuration requise et fournit les instructions d’installation de WMF.</span><span class="sxs-lookup"><span data-stu-id="99166-113">The [Install and Configure](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) topic lists the requirements and provides installation instructions for WMF.</span></span> 

<span data-ttu-id="99166-114">La rubrique [Compatibilité](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) liste quelles versions de WMF peuvent être installées sur quelles versions Windows.</span><span class="sxs-lookup"><span data-stu-id="99166-114">The [Compatibility](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) topic lists which versions of WMF may be installed on which Windows releases.</span></span> 

<span data-ttu-id="99166-115">La rubrique [Compatibilité des produits](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) liste les applications Microsoft qui n’ont pas approuvé WMF 5.1 pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="99166-115">[Product Compatibility](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) lists the Microsoft applications that have not approved WMF 5.1 for use at this time.</span></span> 

<span data-ttu-id="99166-116">Les détails des composants de WMF se trouvent dans la documentation MSDN :</span><span class="sxs-lookup"><span data-stu-id="99166-116">Details for the components of WMF will be found in MSDN documentation:</span></span>

- [<span data-ttu-id="99166-117">PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="99166-117">PowerShell 5.1</span></span>](https://docs.microsoft.com/en-us/powershell/) 
- [<span data-ttu-id="99166-118">WMI</span><span class="sxs-lookup"><span data-stu-id="99166-118">WMI</span></span>](https://msdn.microsoft.com/en-us/library/jj152383(v=vs.85).aspx)
- [<span data-ttu-id="99166-119">WinRM</span><span class="sxs-lookup"><span data-stu-id="99166-119">WinRM</span></span>](https://msdn.microsoft.com/en-us/library/aa384426(v=vs.85).aspx)
- [<span data-ttu-id="99166-120">Journalisation de l’inventaire logiciel</span><span class="sxs-lookup"><span data-stu-id="99166-120">Software Inventory Logging</span></span>](https://technet.microsoft.com/en-us/library/dn383584(v=ws.11).aspx)
