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


1. Se rendre sur l'explorateur de fichier. Ensuite, fair un clique droit sur **PC > propriétes**

2. Ensuite cliquer sur **Paramètre System avancer > Variables d'environement**

Maintenant on doit modifier une des variables d'environement mais cela change selon la version de windows:

Windows 10: Path dans **variables utilisateur**
Windows server 2012 R2: Path dans **variables systeme**

3. Choisir la variable et cliquer sur Modifier.

4. Ajouter le chemin du dossier **bin** dans le dossier OpenVPN

pour l'ajouter sur Windows server 2012 R2, ajouter un **;** à la fin d'un chemin

5. Exécuter le commande dans **les points 2 à 5**

Si le cmd affiche une bare de chargement tel que celle ci cela veut dire que tout est en ordre:

Pour verifier que tout est opération, rendez vous dans **C:\Program Files\OpenVPN\easy-rsa\keys"**. Si ces trois fichier sont présent c'est bon:

6. Dans le cmd en administrateur, entrer **build-ca**.

Vous devrez entrez des présision tel que la pays, la ville, ...

7. Ensuite, entrer la commande **build-key-server lenomdusrv**. validez les question par défaut meme pour le mdp. Quand il demande de signer le cerfificat, faire **y** ainsi que pour le commit

Il faut mnt crée la clef pour le client

1. Entrer **build-key nomdonneclient** dans le cmd

2. les même questions vous être posé (Voir img ...), le plus important est d'attribuer un nom dans **Common Name**. Valider par défaut le reste comme dans le point 7.

3. Entrer **OpenVPN --genkey --secret keys/ta.key** pour générer la clef **ta**.

Passon mnt à la configuration du serveur

1. Se rendre dans le dossier **OpenVPN > config** et crée un fichier **.ovpn** nommée comme le serveur. Ici c'est ServeurVPN.

Voici la configuration de notre serveur:

```
dev-node "ServerVPN"
mode server
port 12345

proto tcp4-server
dev tun

tls-server
tls-auth "C:\\Program Files\\OpenVPN\\easy-rsa\\keys\\ta.key" 0

tun-mtu 1500
tun-mtu-extra 32
mssfix 1450

ca "C:\\Program Files\\OpenVPN\\easy-rsa\\keys\\ca.crt"
cert "C:\\Program Files\\OpenVPN\\easy-rsa\\keys\\ServerVPN.crt"
key "C:\\Program Files\\OpenVPN\\easy-rsa\\keys\\ServerVPN.key"
dh "C:\\Program Files\\OpenVPN\\easy-rsa\\keys\\dh2048.pem"

server 10.10.10.0 255.255.255.0

client-to-client
keepalive 10 120
cipher AES-128-CBC
comp-lzo

persist-key
persist-tun

client-config-dir "C:\\Program Files\\OpenVPN\\config"

verb 3

route-delay 5
route-method exe

push "route 192.168.163.0 255.255.255.0"
route 192.168.163.0 255.255.255.0

```

Ensuite pour verifier si la connection s'établie il faut se rendre dans la bare des taches et cliquer sur l'icone d'openvpn et cliquer sur connecter. si l'icone de l'ordinateur à un ecrant vert cest que c'est opérationel

## configuration client

Pour commencer il faut installer openVPN sur le pc client. Faites simplement l'instalation avec les paramètres par défaut.

Ensuite il faut se rendre dans le dossier **config** d'openvpn et ajouté 5 fichiers qui se situe dans **easy-rsa/key** sur le serveur.

- ca.crt
- ClientVPN.crt
- ClientVPN.csr
- ClientVPN.key
- ta.key

1. Créer un fichier **ClientVPN.ovpn** et entrez la configuration shouaité.

voici la configuration du Client

```
remote 192.168.163.128
client
port 12345

proto tcp4-client
dev tun

tls-client
tls-auth "C:\\Program Files\\OpenVPN\\config\\ta.key" 1
remote-cert-tls server

tun-mtu 1500
tun-mtu-extra 32
mssfix 1450

ca "C:\\Program Files\\OpenVPN\\config\\ca.crt"
cert "C:\\Program Files\\OpenVPN\\config\\ClientVPN.crt"
key "C:\\Program Files\\OpenVPN\\config\\ClientVPN.key"

cipher AES-128-CBC
comp-lzo

persist-key
persist-tun

verb 3
mute 20
```

## Finalisation de la configuration

Il reste une derrnière chose à faire afin de pouvoir echanger des paquets entre le serveur et le client.

Il faut excuter le programme **regedit** et se rendre dans **HKEY_LOCAL_MACHINES\System\CurrentControlSet\Services\TcpIP\Parameters** et changer la valeur de **PEnableRouter** à 1. Il faut faire ca pour le client ET le serveur. Quand ce sera fait redémarer les machines.

Maintenant sur le pc client. cliqué sur connecter et pinger l'addresse ip du serveur. Si vous parvenez a ping le serveur et vice-versa c'est que le VPN est en place.
