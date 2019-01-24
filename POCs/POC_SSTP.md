# POC - SSTP

## 1. introduction

Installation de l'infrastructure avec un VPN SSTP afin de pouvoir accèder aux ressources du serveur depuis un autre réseau.

Machines utilisées : **PRJS_CLI1** et **PRJS_SRV1**. cf. [Documentation - point 5](../Documentation.pdf#5)

## 2. Installation du serveur VPN
Sur PRJS_SRV1

1. Ajouter le rôle "Accès à distance"
2. Services de rôle : DirectAccess et VPN
3. Laisser le reste par défaut (installer le service IIS)
4. Configurer le Service
5. Sélectionner Déployer VPN uniquement

## 3.
