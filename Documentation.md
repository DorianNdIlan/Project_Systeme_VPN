# Documentation Projet système
## - Accès externe aux ressources d’entreprises -

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Documentation Projet système](#documentation-projet-systme)
	- [- Accès externe aux ressources d’entreprises -](#-accs-externe-aux-ressources-dentreprises-)
	- [1. Introduction](#1-introduction)
	- [2. Analyse du contexte](#2-analyse-du-contexte)
	- [3. Définition des critères](#3-dfinition-des-critres)
	- [4. Analyse des outils](#4-analyse-des-outils)
		- [4.1 OpenVPN](#41-openvpn)
		- [4.2 SSTP](#42-sstp)
			- [4.2.1 Description](#421-description)
			- [4.2.2 Avantages et inconvénients](#422-avantages-et-inconvnients)
		- [4.3 Centrify](#43-centrify)
			- [4.3.1 Description](#431-description)
			- [4.3.2 Avantages et Inconvénients](#432-avantages-et-inconvnients)

<!-- /TOC -->


## 1. Introduction

Ce projet consiste à faire une étude concernant un principe de fonctionnement d&#39;un outils/applications lié aux réseaux. Un exemple concret d&#39;application au sein du CPNV doit être présenté. Des travaux pratiques seront mis en place pour appuyer et illustrer le fonctionnement de ces outils.

Notre sujet porte sur l&#39;accès externe aux ressources d&#39;entreprise, avec comme outils : SSTP (gratuit), OpenVPN (gratuit), Centrify (payant) et Akamai (payant). Une analyse complète de chaque outil sera effectuée, une comparaison de ces outils sera ensuite faite pour en tirer des avantages/désavantage.

## 2. Analyse du contexte

Le contexte est de mettre en place un système utile pour le CPNV. Notre sujet portant sur l&#39;accès externe aux ressources d&#39;une entreprise, le but étant de pouvoir accéder à certaines ressources de l&#39;entreprise via un VPN.

Cas utile pour le CPNV : l&#39;accès aux documents présent sur les différents partages (Commun, Perso, etc…) depuis l&#39;extérieur (ex. depuis chez soi), via un client VPN.

## 3. Définition des critères

|Critère|Définition|
|-------|----------|
|Sécurité|La sécurité de l'outil (connexion sécurisée)|
|Prix|Prix de la solution|
|Rapidité de mise en place|La solution est-t-elle rapidement et facilement mise en place dans l'infrastructure ? Facile à utilisé pour les clients ?|
|Fonctionnalités|Les fonctionnalités mises à disposition sont-elles suffisantes ? Trop chargées ?|
|Compatibilité|L'outil est-il compatible avec toutes les plateformes, versions de l'OS ?|

## 4. Analyse des outils

Analyse des deux outils utilisés

### 4.1 OpenVPN

 ![](images\Layer-3-routing-diagram-1024x606.png)

### 4.2 SSTP

#### 4.2.1 Description

SSTP (Secure Socket Tunneling Protocol) est un protocole de VPN créé par Microsoft, il est cependant uniquement disponible sur Windows. Il est reconnu comme l&#39;un des protocoles les plus sécurisés.

Il utilise le canal sécurisé SSL (port 443), ce qui lui permet de passer plus facilement entre les pare-feu, du fait que les pare-feu autorisent le trafic SSL via le port 443.

#### 4.2.2 Avantages et inconvénients

|Avantages|Inconvénients|
|---------|-------------|
|- Très sécurisé<br> - Disponible nativement sur Windows|- Disponible uniquement sur Windows <br> - Mise en place peut être un peu plus difficile|

### 4.3 Centrify

#### 4.3.1 Description

Centrify propose plusieurs solutions dans la gestion des ressources et des utilisateurs d'une entreprise ainsi que dans sa sécurité.

#### 4.3.2 Avantages et Inconvénients

|Avantages|Inconvénients|
|---------|-------------|
|- Offre beaucoup de fonctionnalité <br> - Hautement sécurisé|- Payant <br> - Trop de fonctionnalités par rapport aux besoins|
