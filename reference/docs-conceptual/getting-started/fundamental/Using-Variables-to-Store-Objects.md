---
ms.date: 08/27/2018
keywords: powershell,applet de commande
title: Utilisation de variables pour stocker des objets
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: f4254199facb914c68a487b281b30070c35550a1
ms.sourcegitcommit: c170a1608d20d3c925d79c35fa208f650d014146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43353216"
---
# <a name="using-variables-to-store-objects"></a>Utilisation de variables pour stocker des objets

PowerShell fonctionne avec des objets. PowerShell vous permet de créer des objets nommés reconnus comme des variables.
Les noms des variables peuvent inclure le trait de soulignement et tout caractère alphanumérique. Lorsqu’elle est utilisée dans PowerShell, une variable est toujours spécifiée à l’aide du caractère \$ suivi par le nom de la variable.

## <a name="creating-a-variable"></a>Création d’une variable

Vous pouvez créer une variable en tapant un nom de variable valide :

```
PS> $loc
PS>
```

Cet exemple ne retourne aucun résultat, car `$loc` n’a pas de valeur. Vous pouvez créer une variable et lui attribuer une valeur au cours de la même étape. PowerShell ne crée la variable que si elle n’existe pas.
Sinon, il attribue la valeur spécifiée à la variable existante. L’exemple suivant stocke l’emplacement actuel dans la variable `$loc` :

```powershell
$loc = Get-Location
```

PowerShell n’affiche aucune sortie lorsque vous tapez cette commande. PowerShell envoie la sortie de « Get-Location » à `$loc`. Dans PowerShell, les données qui ne sont pas attribuées ou redirigées sont envoyées à l’écran. Tapez `$loc` pour afficher votre emplacement actuel :

```
PS> $loc

Path
----
C:\temp
```

Vous pouvez utiliser `Get-Member` pour afficher des informations sur le contenu de variables. `Get-Member` indique que `$loc` est un objet **PathInfo**, tout comme la sortie de `Get-Location` :

```powershell
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

## <a name="manipulating-variables"></a>Manipulation de variables

PowerShell fournit plusieurs commandes pour manipuler des variables. Vous pouvez afficher leur liste complète sous forme lisible en tapant ce qui suit :

```powershell
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

PowerShell crée également plusieurs variables définies par le système. Vous pouvez utiliser la cmdlet `Remove-Variable` pour effacer toutes les variables non contrôlées par PowerShell de la session actuelle. Pour effacer toutes les variables, tapez la commande suivante :

```powershell
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

Après avoir exécuté la commande précédente, la cmdlet `Get-Variable` affiche les variables système PowerShell.

PowerShell crée également un lecteur de variable. Pour afficher toutes les variables PowerShell à l’aide du lecteur de variable, utilisez l’exemple suivant :

```powershell
Get-ChildItem variable:
```

## <a name="using-cmdexe-variables"></a>Utilisation de variables cmd.exe

PowerShell peut utiliser les mêmes variables d’environnement que celles disponibles pour n’importe quel processus Windows, notamment **cmd.exe**. Ces variables sont exposées via un lecteur nommé `env:`. Vous pouvez consulter ces variables en tapant la commande suivante :

```powershell
Get-ChildItem env:
```

Les cmdlets `*-Variable` standard ne sont pas conçues pour fonctionner avec les variables d’environnement. Les variables d’environnement sont accessibles à l’aide du préfixe du lecteur `env:`. Par exemple, la variable **%SystemRoot%** dans **cmd.exe** contient le nom du répertoire racine du système d’exploitation. Dans PowerShell, vous utilisez `$env:SystemRoot` pour accéder à la même valeur.

```
PS> $env:SystemRoot
C:\WINDOWS
```

Vous pouvez également créer et modifier des variables d’environnement à partir de PowerShell. Les variables d’environnement dans PowerShell suivent les mêmes règles que les variables d’environnement utilisées ailleurs dans le système d’exploitation. L’exemple suivant crée une variable d’environnement :

```powershell
$env:LIB_PATH='/usr/local/lib'
```

Bien que cela ne soit pas obligatoire, il est courant que les noms des variables d’environnement utilisent uniquement des lettres majuscules.