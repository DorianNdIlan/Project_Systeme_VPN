# Documentation Projet système
## - Accès externe aux ressources d’entreprises -

## 1. Introduction

Ce projet consiste à faire une étude concernant un principe de fonctionnement d&#39;un outils/applications lié aux réseaux. Un exemple concret d&#39;application au sein du CPNV doit être présenté. Des travaux pratiques seront mis en place pour appuyer et illustrer le fonctionnement de ces outils.

Notre sujet porte sur l&#39;accès externe aux ressources d&#39;entreprise, avec comme outils : SSTP et OpenVPN. Une analyse complète de chaque outil sera effectuée, une comparaison de ces deux outils sera ensuite faite pour en tirer des avantages/désavantages de l&#39;un comparé à l&#39;autre.

## 2. Analyse du contexte

Le contexte est de mettre en place un système utile pour le CPNV. Notre sujet portant sur l&#39;accès externe aux ressources d&#39;une entreprise, le but étant de pouvoir accéder à certaines ressources de l&#39;entreprise via un VPN.

Cas utile pour le CPNV : l&#39;accès aux documents présent sur les différents partages (Commun, Perso, etc…) depuis l&#39;extérieur (ex. depuis chez soi), via un client VPN.

## 3. Analyse des outils

Analyse des deux outils utilisés


### 3.1 OpenVPN

 ![](images\Layer-3-routing-diagram-1024x606.png)

### 3.2 SSTP

### 3.2.1 Description

SSTP (Secure Socket Tunneling Protocol) est un protocole de VPN créé par Microsoft, il est cependant uniquement disponible sur Windows. Il est reconnu comme l&#39;un des protocoles les plus sécurisés.

Il utilise le canal sécurisé SSL (port 443), ce qui lui permet de passer plus facilement entre les pare-feu, du fait que les pare-feu autorisent le trafic SSL via le port 443.

### 3.2.2 Avantages et inconvénients

|Avantages|Inconvénients|
|---------|-------------|
|- Très sécurisé<br> - Disponible nativement sur Windows|- Disponible uniquement sur Windows|

## 4 Critères de comparaisons
