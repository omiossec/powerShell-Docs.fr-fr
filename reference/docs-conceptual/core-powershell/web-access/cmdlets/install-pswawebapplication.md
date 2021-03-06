---
ms.topic: reference
keywords: powershell,applet de commande
ms.date: 12/12/2016
title: Install-PswaWebApplication
ms.openlocfilehash: 29e074b75eeb387640831229c63142e6dd5e991a
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268297"
---
# <a name="install-pswawebapplication"></a>Install-PswaWebApplication

## <a name="synopsis"></a>SYNOPSIS

Configure l’application web Accès Web Windows PowerShell dans IIS.

## <a name="syntax"></a>SYNTAXE

### <a name="default"></a>Par défaut
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>DESCRIPTION

L’applet de commande **Install-PswaWebApplication** configure l’application web Accès Web Windows PowerShell.
Cette applet de commande installe l’application web, l’associe à un site web et crée éventuellement un certificat de test SSL à l’aide du paramètre **useTestCertificate**. Pour des raisons de sécurité, les administrateurs web ne doivent pas utiliser un certificat de test pour les environnements de production.

## <a name="parameters"></a>PARAMÈTRES

### <a name="-usetestcertificate"></a>-UseTestCertificate

Spécifie qu’un certificat de test est créé. Si ce paramètre est défini sur true, cette applet de commande crée un certificat de test et configure l’application web Accès Web Windows PowerShell pour qu’elle utilise le certificat pour les requêtes HTTPS. Si ce paramètre est défini sur false, aucun certificat ni aucune liaison ne sont créés. Définissez cette valeur sur false si un autre certificat est utilisé pour Accès Web Windows PowerShell.

|||
|-|-|
| Alias                              | none                                 |
| Obligatoire ?                            | false                                |
| Position ?                            | nommé                                |
| Valeur par défaut                        | true                                 |
| Accepter l’entrée de pipeline ?               | false                                |
| Accepter les caractères génériques ?          | false                                |

### <a name="-webapplicationname"></a>-WebApplicationName

Spécifie le nom de votre application web. Il constitue la dernière partie de l’URL d’Accès Web Windows PowerShell.

|||
|-|-|
| Alias                              | none                                 |
| Obligatoire ?                            | false                                |
| Position ?                            | 1                                    |
| Valeur par défaut                        | pswa                                 |
| Accepter l’entrée de pipeline ?               | false                                |
| Accepter les caractères génériques ?          | false                                |

### <a name="-websitename"></a>-WebSiteName

Spécifie le nom du site web du serveur Web IIS sur lequel installer cette application web Accès Web Windows PowerShell.

|||
|-|-|
| Alias                              | none                                 |
| Obligatoire ?                            | false                                |
| Position ?                            | nommé                                |
| Valeur par défaut                        | Default Web Site                     |
| Accepter l’entrée de pipeline ?               | false                                |
| Accepter les caractères génériques ?          | false                                |

### <a name="-confirm"></a>-Confirm

Votre confirmation sera requise avant l’exécution de l’applet de commande.

|||
|-|-|
| Obligatoire ?                            | false                                |
| Position ?                            | nommé                                |
| Valeur par défaut                        | false                                |
| Accepter l’entrée de pipeline ?               | false                                |
| Accepter les caractères génériques ?          | false                                |

### <a name="-whatif"></a>-WhatIf

Présente les conséquences éventuelles de l’exécution de l’applet de commande.
L’applet de commande n’est pas exécutée.

|||
|-|-|
| Obligatoire ?                            | false                                |
| Position ?                            | nommé                                |
| Valeur par défaut                        | false                                |
| Accepter l’entrée de pipeline ?               | false                                |
| Accepter les caractères génériques ?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Cette applet de commande prend en charge les paramètres courants : -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer et -OutVariable. Pour plus d’informations, consultez [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>ENTRÉES

Cette applet de commande ne prend pas d’entrée.

## <a name="outputs"></a>SORTIES

Cette applet de commande ne produit pas de sortie.

## <a name="examples"></a>EXEMPLES

### <a name="example-1"></a>EXEMPLE 1

Cet exemple installe l’application web PSWA en utilisant les valeurs par défaut pour les paramètres **WebApplicationName** (*pswa*) et **WebSiteName** (*Default Web Site*).

```
Install-PswaWebApplication
```

### <a name="example-2"></a>EXAMPLE 2

Cet exemple installe l’application web PSWA avec un certificat de test, en utilisant les valeurs par défaut pour les paramètres **WebApplicationName** et **WebSiteName**.

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a>Rubriques connexes

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)