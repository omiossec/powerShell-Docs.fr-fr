---
ms.date: 06/12/2017
keywords: wmf,powershell,configuration
ms.openlocfilehash: 3f73b7cf0cdf033cbd561b3412734692bb7decd7
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187531"
---
# <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a>Autorisation des ressources en double identiques dans une configuration

DSC n’autorise pas et ne gère pas les définitions de ressources conflictuelles dans une configuration. Au lieu d’essayer de résoudre le conflit, il échoue tout simplement. Avec l’augmentation de la réutilisation des configurations due, entre autres, aux ressources composites, des conflits se produiront plus souvent. Quand des définitions de ressources conflictuelles sont identiques, DSC doit agir intelligemment et les autoriser. Dans cette version, l’existence de plusieurs instances de ressources ayant des définitions identiques est prise en charge :

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS         #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS      #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

Dans les versions précédentes, le résultat était un échec de compilation dû à un conflit, car les instances de WindowsFeature FE_IIS et WindowsFeature Worker_IIS essayaient de garantir l’installation du rôle « Serveur Web ». Notez que *toutes* les propriétés configurées sont identiques dans ces deux configurations. Étant donné que *toutes* les propriétés de ces deux ressources sont identiques, désormais la compilation réussit.

Si certaines propriétés des deux ressources sont différentes, elles ne sont pas considérées comme identiques et la compilation échoue :

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS
    {
        Ensure = 'Present'     # Ensure is Present here
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS
    {
        Ensure = 'Absent'      # Ensure property is Absent instead of Present
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

Cette configuration très semblable échoue, car les ressources WindowsFeature FE_IIS et WindowsFeature Worker_IIS ne sont plus identiques et sont donc en conflit.
