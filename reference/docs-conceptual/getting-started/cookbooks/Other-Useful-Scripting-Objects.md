---
ms.date: 06/05/2017
keywords: powershell,applet de commande
title: Autres objets de script utiles
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 04e94f858b568928b3910dd0ee85a912a6afc264
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268498"
---
# <a name="other-useful-scripting-objects"></a>Autres objets de script utiles

Les objets suivants fournissent des fonctionnalités de script supplémentaires dans Windows PowerShell ISE. Ils ne sont pas inclus dans la hiérarchie **$psISE**.

## <a name="useful-scripting-objects"></a>Objets de script utiles

### <a name="psunsupportedconsoleapplications"></a>$psUnsupportedConsoleApplications

Il existe certaines restrictions sur la façon dont Windows PowerShell ISE interagit avec les applications de console. Une commande ou un script d’automatisation qui nécessite l’intervention de l’utilisateur peut ne pas fonctionner de la même façon qu’à partir de la console Windows PowerShell. Vous pouvez empêcher l’exécution de ces commandes ou scripts dans le volet Commande de Windows PowerShell ISE. L’objet **$psUnsupportedConsoleApplications** conserve la liste de ces commandes. Si vous essayez d’exécuter les commandes de cette liste, vous obtenez un message indiquant qu’elles ne sont pas prises en charge. Le script suivant ajoute une entrée à la liste.

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a>$psLocalHelp

Il s’agit d’un objet de dictionnaire qui gère un mappage sensible au contexte entre des rubriques d’aide et leurs liens correspondants dans le fichier d’aide HTML compilé local. Il est utilisé pour localiser l’aide locale d’une rubrique particulière. Vous pouvez ajouter ou supprimer des rubriques dans cette liste. L’exemple de code suivant illustre certaines paires clé-valeur contenues dans `$psLocalHelp`.

```powershell
# See the local help map
$psLocalHelp | Format-List
```

```output
Key   : Add-Computer
Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm

Key   : Add-Content
Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm
```

Le script suivant ajoute une entrée à la liste.

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a>$psOnlineHelp

Il s’agit d’un objet de dictionnaire qui gère un mappage sensible au contexte entre des titres de rubriques d’aide et leurs URL externes correspondantes. Il est utilisé pour localiser l’aide d’une rubrique particulière sur le web. Vous pouvez ajouter ou supprimer des rubriques dans cette liste.

```powershell
$psOnlineHelp | Format-List
```

```output
Key   : Add-Computer
Value : http://go.microsoft.com/fwlink/p/?LinkID=135194

Key   : Add-Content
Value : http://go.microsoft.com/fwlink/p/?LinkID=113278
```

Le script suivant ajoute une entrée à la liste.

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a>Voir aussi

[Objectif du modèle objet de script Windows PowerShell ISE](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)