---
title: Accès distant à PowerShell via SSH
description: Accès distant dans PowerShell Core à l’aide de SSH
ms.date: 08/14/2018
ms.openlocfilehash: 1de034d667aa9a377e5460e7eb474402c690cb42
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133156"
---
# <a name="powershell-remoting-over-ssh"></a>Accès distant à PowerShell via SSH

## <a name="overview"></a>Vue d’ensemble

L’accès distant PowerShell utilise normalement WinRM pour la négociation de la connexion et le transport des données. SSH est désormais disponible pour les plateformes Linux et Windows, et permet une réelle communication à distance PowerShell multiplateforme.

WinRM fournit un modèle d’hébergement robuste pour les sessions distantes PowerShell. Cette implémentation de la communication à distance basée sur SSH ne prend actuellement pas en charge la configuration d’un point de terminaison distant et JEA (Just Enough Administration).

La communication à distance SSH vous permet d’établir la communication à distance pour une session PowerShell de base entre des ordinateurs Windows et Linux. La communication à distance SSH crée un processus hôte PowerShell sur l’ordinateur cible en tant que sous-système SSH.
Nous implémenterons prochainement un modèle d’hébergement général, similaire à WinRM, pour prendre en charge la configuration de point de terminaison et JEA.

Les cmdlets `New-PSSession` `Enter-PSSession` et `Invoke-Command` ont maintenant un nouvel ensemble de paramètres pour prendre en charge cette nouvelle connexion de communication à distance.

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Pour créer une session distante, vous spécifiez l’ordinateur cible avec le paramètre `HostName` et vous fournissez le nom d’utilisateur avec `UserName`. Lors de l’exécution des cmdlets de manière interactive, vous êtes invité à entrer un mot de passe. Vous pouvez également utiliser l’authentification par clé SSH à l’aide d’un fichier de clé privée avec le paramètre `KeyFilePath`.

## <a name="general-setup-information"></a>Informations générales sur l’installation

SSH doit être installé sur tous les ordinateurs. Installez le client SSH (`ssh.exe`) et le serveur (`sshd.exe`) pour pouvoir communiquer à distance vers et depuis les ordinateurs. Pour Windows, installez [OpenSSH Win32 à partir de GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).
Pour Linux, installez SSH (y compris le serveur sshd) approprié pour votre plateforme. Vous devez également installer PowerShell Core à partir de GitHub pour obtenir la fonctionnalité de communication à distance SSH. Le serveur SSH doit être configuré pour créer un sous-système SSH afin d’héberger un processus PowerShell sur l’ordinateur distant. Vous devez également configurer l’activation de l’authentification par mot de passe ou clé.

## <a name="set-up-on-windows-machine"></a>Configuration sur un ordinateur Windows

1. Installez la dernière version de [PowerShell Core pour Windows]

   - Vous pouvez savoir si elle dispose de la prise en charge de l’accès distant SSH en examinant les ensembles de paramètres pour `New-PSSession`

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. Installez la dernière version de [OpenSSH Win32] depuis GitHub en utilisant les instructions [d’installation]
3. Ouvrez le fichier sshd_config à l’emplacement où vous avez installé OpenSSH Win32

   - Vérifiez que l’authentification par mot de passe est activée

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.4/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > OpenSSH pour Windows présente un bogue qui empêche les espaces de fonctionner dans les chemins exécutables du sous-système. Pour plus d’informations, consultez [ce problème GitHub](https://github.com/PowerShell/Win32-OpenSSH/issues/784).

     Une solution consiste à créer un lien symbolique vers le répertoire d’installation de Powershell sans espaces :

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.4"
     ```

     puis de l’entrer dans le sous-système :

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - Vous pouvez éventuellement activer l’authentification par clé

     ```
     PubkeyAuthentication yes
     ```

4. Redémarrez le service sshd

   ```powershell
   Restart-Service sshd
   ```

5. Ajoutez le chemin où OpenSSH est installé à votre variable d’environnement Path. Par exemple, `C:\Program Files\OpenSSH\`. Cette entrée permet au système de trouver ssh.exe.

## <a name="set-up-on-linux-ubuntu-1404-machine"></a>Configuration sur un ordinateur Linux (Ubuntu 14.04)

1. Installez la dernière version [PowerShell Core pour Linux] à partir de GitHub
2. Installez [Ubuntu SSH] si nécessaire

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. Ouvrez le fichier sshd_config à l’emplacement /etc/ssh

   - Vérifiez que l’authentification par mot de passe est activée

   ```
   PasswordAuthentication yes
   ```

   - Ajoutez une entrée de sous-système PowerShell

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - Vous pouvez éventuellement activer l’authentification par clé

   ```
   PubkeyAuthentication yes
   ```

4. Redémarrez le service sshd

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a>Configuration sur un ordinateur MacOS

1. Installez la dernière version de [PowerShell Core pour MacOS]

   - Vérifiez que l’accès distant SSH est activé en suivant ces étapes :
     - Ouvrez `System Preferences`
     - Cliquez sur `Sharing`
     - Vérifiez `Remote Login`, qui doit être `Remote Login: On`
     - Autorisez l’accès aux utilisateurs appropriés

2. Ouvrez le fichier `sshd_config` à l’emplacement `/private/etc/ssh/sshd_config`

   - Utiliser votre éditeur préféré ou

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - Vérifiez que l’authentification par mot de passe est activée

     ```
     PasswordAuthentication yes
     ```

   - Ajoutez une entrée de sous-système PowerShell

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - Vous pouvez éventuellement activer l’authentification par clé

     ```
     PubkeyAuthentication yes
     ```

3. Redémarrez le service sshd

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="powershell-remoting-example"></a>Exemple d’accès distant PowerShell

Le moyen le plus simple de tester la communication à distance est de l’essayer sur un seul ordinateur. Dans cet exemple, nous créons une session distante avec le même ordinateur Linux. Nous utilisons des cmdlets PowerShell de manière interactive, afin de voir les invites SSH demandant de vérifier l’ordinateur hôte ainsi que des demandes de mot de passe. Vous pouvez faire la même chose sur un ordinateur Windows pour vérifier que la communication à distance fonctionne. Puis, établissez la communication à distance entre les ordinateurs en modifiant le nom d’hôte.

```powershell
#
# Linux to Linux
#
$session = New-PSSession -HostName UbuntuVM1 -UserName TestUser
```

```output
The authenticity of host 'UbuntuVM1 (9.129.17.107)' cannot be established.
ECDSA key fingerprint is SHA256:2kCbnhT2dUE6WCGgVJ8Hyfu1z2wE4lifaJXLO7QJy0Y.
Are you sure you want to continue connecting (yes/no)?
TestUser@UbuntuVM1s password:
```

```powershell
$session
```

```output
 Id Name   ComputerName    ComputerType    State    ConfigurationName     Availability
 -- ----   ------------    ------------    -----    -----------------     ------------
  1 SSH1   UbuntuVM1       RemoteMachine   Opened   DefaultShell             Available
```

```powershell
Enter-PSSession $session
```

```output
[UbuntuVM1]: PS /home/TestUser> uname -a
Linux TestUser-UbuntuVM1 4.2.0-42-generic 49~14.04.1-Ubuntu SMP Wed Jun 29 20:22:11 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

[UbuntuVM1]: PS /home/TestUser> Exit-PSSession
```

```powershell
Invoke-Command $session -ScriptBlock { Get-Process powershell }
```

```output
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName                    PSComputerName
-------  ------    -----      -----     ------     --  -- -----------                    --------------
      0       0        0         19       3.23  10635 635 powershell                     UbuntuVM1
      0       0        0         21       4.92  11033 017 powershell                     UbuntuVM1
      0       0        0         20       3.07  11076 076 powershell                     UbuntuVM1
```

```powershell
#
# Linux to Windows
#
Enter-PSSession -HostName WinVM1 -UserName PTestName
```

```output
PTestName@WinVM1s password:
```

```powershell
[WinVM1]: PS C:\Users\PTestName\Documents> cmd /c ver
```

```output
Microsoft Windows [Version 10.0.10586]
```

```powershell
#
# Windows to Windows
#
C:\Users\PSUser\Documents>pwsh.exe
```

```output
PowerShell
Copyright (c) Microsoft Corporation. All rights reserved.
```

```powershell
$session = New-PSSession -HostName WinVM2 -UserName PSRemoteUser
```

```output
The authenticity of host 'WinVM2 (10.13.37.3)' can't be established.
ECDSA key fingerprint is SHA256:kSU6slAROyQVMEynVIXAdxSiZpwDBigpAF/TXjjWjmw.
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'WinVM2,10.13.37.3' (ECDSA) to the list of known hosts.
PSRemoteUser@WinVM2's password:
```

```powershell
$session
```

```output
 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            WinVM2          RemoteMachine   Opened        DefaultShell             Available
```

```powershell
Enter-PSSession -Session $session
```

```output
[WinVM2]: PS C:\Users\PSRemoteUser\Documents> $PSVersionTable

Name                           Value
----                           -----
PSEdition                      Core
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
SerializationVersion           1.1.0.1
BuildVersion                   3.0.0.0
CLRVersion
PSVersion                      6.0.0-alpha
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
GitCommitId                    v6.0.0-alpha.17


[WinVM2]: PS C:\Users\PSRemoteUser\Documents>
```

### <a name="known-issues"></a>Problèmes connus

La commande sudo ne fonctionne pas dans une session distante sur un ordinateur Linux.

## <a name="see-also"></a>Voir aussi

[PowerShell Core pour Windows](../setup/installing-powershell-core-on-windows.md#msi)

[PowerShell Core pour Linux](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[PowerShell Core pour MacOS](../setup/installing-powershell-core-on-macos.md)

[OpenSSH Win32](https://github.com/PowerShell/Win32-OpenSSH/releases)

[Installation](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

[Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
