# POC Active directory

# Installation

1. Nouvelle forêt : **Prjs.local**

2. Niveau fonctionnalités : **Windows Server 2012 R2**

  - ajout d'un **DNS**
  - DSRM: **Pa$$w0rd**


3. Nom de domaine NetBIOS: **PRJS**

4. Emplacement de la BD, Fichier journeau et SYSVOL:

  - BD: C:\Windows\NTDS
  - Fichier journeaux: C:\Windows\NTDS
  - SYSVOL: C:\Windows\SYSVOL

Script de création:

```
#
# Script Windows PowerShell pour le déploiement d’AD DS
#

Import-Module ADDSDeployment
Install-ADDSForest `
-CreateDnsDelegation:$false `
-DatabasePath "C:\Windows\NTDS" `
-DomainMode "Win2012R2" `
-DomainName "Prjs.local" `
-DomainNetbiosName "PRJS" `
-ForestMode "Win2012R2" `
-InstallDns:$true `
-LogPath "C:\Windows\NTDS" `
-NoRebootOnCompletion:$false `
-SysvolPath "C:\Windows\SYSVOL" `
-Force:$true
```

Mot de passe admin: **StrongPa$$w0rd**

# Installation de OpenVPN

Pour commencer, telecharger l'installeur sur le site d'OpenVPN

1. Cocher RA2

2. Installer l'adaptateur réseau

voila, nous avons installer OpenVPN. Passon mnt a la configuration.

1. Ouvrir un CMD en tant qu'admin

2. Se rendre dans **"C:\Program Files\OpenVPN\easy-rsa"** avec un **cd**

3. Executer la commande **init-config.bat**

4. Executer la commande **vars** et ensuite **clean-all**

5. Ensuite, exectuer la commande **build-dh**.


si le résultat est:
```
'openssl' n'est pas reconnu en tant que commande interne
ou externe, un programme exécutable ou un fichier de commandes.
```

c'est tout a fait normal. nous allons voir comment régler ce probleme.
