---
title: "Prérequis des profils Wi-Fi et VPN | System Center Configuration Manager"
description: "Découvrez les autorisations de sécurité nécessaires pour gérer des profils de certificat, des profils Wi-Fi et des profils VPN dans System Center Configuration Manager."
ms.custom: na
ms.date: 0201-03-31
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5c6cf3c1697b49708aa5192b67b08b700da7dc72
ms.openlocfilehash: c103735a0f5fab6b800a7e9fb808221aebb102cb


---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Prérequis des profils Wi-Fi et VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les profils Wi-Fi et VPN dans System Center Configuration Manager ont uniquement des dépendances au sein du produit.  

 Vous devez disposer des autorisations de sécurité suivantes pour gérer les paramètres d'accès aux ressources de l'entreprise, par exemple, les profils de certificat, les profils Wi-Fi et les profils VPN :  

-   Pour afficher et gérer les alertes et les rapports pour les profils Wi-Fi : autorisations **Créer**, **Supprimer**, **Modifier**, **Modifier le rapport**, **Lecture** et **Exécuter le rapport** sur l’objet **Alertes**.  

-   Pour créer et gérer des profils de certificat : **Créer une stratégie**, **Modifier le rapport**, **Lecture**et **Exécuter le rapport** pour l’objet **Profil de certificat** .  

-   Pour gérer les déploiements de profil Wi-Fi, VPN et de certificat : **Déployer des stratégies de configuration**, **Modifier l’alerte relative à l’état du client**, **Lecture**et **Lire la ressource** pour l’objet **Regroupement** .  

-   Pour gérer toutes les stratégies de configuration : **Créer**, **Supprimer**, **Modifier**, **Lecture**et **Définir l’étendue de sécurité** pour l’objet **Stratégie de configuration** .  

-   Pour exécuter des requêtes liées aux profils Wi-Fi et VPN : autorisation **Lecture** sur l’objet **Requête**.  

-   Pour afficher les informations sur les profils Wi-Fi et VPN dans la console System Center Configuration Manager : autorisation **Lecture** sur l’objet **Site**.  

-   Pour afficher des messages d’état pour les profils Wi-Fi et VPN : autorisation **Lecture** sur l’objet **Messages d’état** .  

-   Pour créer et modifier le profil de certificat d’Autorité de certification approuvé : **Créer une stratégie**, **Modifier le rapport**, **Lecture**et **Exécuter le rapport** pour l’objet **Profil de certificat d’Autorité de certification approuvé** .  

-   Pour créer et gérer les profils VPN : **Créer une stratégie**, **Modifier le rapport**, **Lecture**et **Exécuter le rapport** pour l’objet **Profil VPN** .  

-   Pour créer et gérer les profils Wi-Fi : **Créer une stratégie**, **Modifier le rapport**, **Lecture**et **Exécuter le rapport** pour l’objet **Profil Wi-Fi** .  

 Le rôle de sécurité **Gestionnaire d’accès aux ressources de l’entreprise** intègre les autorisations permettant de gérer les profils Wi-Fi dans System Center Configuration Manager. Pour plus d’informations, consultez [Configurer la sécurité dans System Center Configuration Manager](../../core/plan-design/security/configure-security.md).



<!--HONumber=Nov16_HO1-->


