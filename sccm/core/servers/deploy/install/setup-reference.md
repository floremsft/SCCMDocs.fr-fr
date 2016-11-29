---
title: "Informations de référence sur le programme d’installation | System Center Configuration Manager"
description: "Prenez connaissance de ces informations de référence pour mieux préparer l’installation d’un site ou d’une hiérarchie Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 06bab7e01fee2c0b030a2879fa67fd455bf668fe


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Informations de référence sur le programme d’installation de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le programme d’installation de System Center Configuration Manager fournit des liens vers plusieurs rubriques comportant les sections suivantes. Les informations contenues dans les sections suivantes peuvent vous aider à préparer l’installation d’un site ou d’une hiérarchie Configuration Manager et à prendre certaines décisions relatives à l’installation :  

-   [Avant de commencer](#bkmk_start)  

-   [Évaluer la préparation du serveur](#bkmk_assess)  

-   [Clients pour d’autres systèmes d’exploitation](#bkmk_Addclients)  

-   [Données d’utilisation et de diagnostic pour System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="a-namebkmkstarta-before-you-begin"></a><a name="bkmk_start"></a> Avant de commencer  
 Avant d’installer de nouveaux sites Configuration Manager, veillez à passer en revue les informations suivantes. Celles-ci peuvent vous aider à mettre en œuvre une conception de déploiement réussie :  

-   [Principes de base de System Center Configuration Manager](../../../../core/understand/fundamentals.md)  

-   [Planifier l’infrastructure System Center Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  

-   [Préparer l’installation de sites System Center Configuration Manager](prepare-to-install-sites.md)  

##  <a name="a-namebkmkassessa-assess-server-readiness"></a><a name="bkmk_assess"></a> Évaluer la préparation du serveur  
 Avant de commencer l’installation d’un nouveau site, vérifiez que le serveur de site et les serveurs de système de site distant que vous envisagez d’utiliser pour le site (comme le serveur qui héberge la base de données) respectent toutes les conditions préalables. Les rubriques suivantes de la bibliothèque de documentation peuvent vous aider :  

-   [Configurations prises en charge pour System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  

-   [Outil de vérification de la configuration requise](https://technet.microsoft.com/library/mt590813.aspx#bkmk_PreqChk)  

##  <a name="a-namebkmkaddclientsa-clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Clients pour d’autres systèmes d’exploitation  
 Vous pouvez télécharger le logiciel client pour Configuration Manager à partir du Centre de téléchargement Microsoft pour les systèmes d’exploitation suivants :  

-   Mac (Apple)  

-   UNIX  

-   Linux  

**Utilisez les liens suivants pour télécharger des clients pour la version de Configuration Manager que vous utilisez :**  

-   [System Center Configuration Manager (Current Branch)](http://www.microsoft.com/download/details.aspx?id=47719)  

-   [System Center 2012 R2 Configuration Manager SP1 et System Center 2012 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  

-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  

-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="a-namebkmkusagea-usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Paramètres et niveaux de données d’utilisation  
Quand vous installez votre premier site System Center Configuration Manager, il installe et configure automatiquement sur le serveur de site un nouveau rôle système de site appelé **point de connexion de service**, avec les paramètres par défaut suivants :  

-   Mode**En ligne** (un mode hors connexion est également pris en charge)  

-   Niveau **Étendu** de collecte de données (deux autres niveaux de collecte de données, De base et Total, sont pris en charge)  

Quand ce rôle est en ligne, il permet à Microsoft de collecter automatiquement des informations d’utilisation et de diagnostic sur Internet. Les informations collectées nous aident à effectuer les tâches suivantes :  

-   Identifier et résoudre les problèmes  

-   Améliorer nos produits et services  

-   identifier les mises à jour pour Configuration Manager applicables à la version de Configuration Manager que vous utilisez.  

Les trois niveaux de collecte de données sont les suivants :  

-   **De base** : comprend des données sur l’installation et la mise à niveau, comme le nombre de sites et les fonctionnalités de Configuration Manager qui sont activées. Aucune information personnelle n’est transmise.  

-   **Amélioré** : comprend les données du paramètre De base et transmet des données relatives à la hiérarchie, à la façon dont chaque fonctionnalité est utilisée (fréquence et durée), ainsi que des informations de diagnostics améliorées telles que l’état de la mémoire de votre serveur quand un blocage du système ou d’une application se produit. Aucune information personnelle n'est transmise.  

-   **Complet** : comprend les données des paramètres De base et Amélioré, et envoie également des informations de diagnostics avancées telles que des fichiers système et des captures instantanées de la mémoire. Cette option peut inclure des informations personnelles, mais nous n’utiliserons pas ces informations pour vous identifier, vous contacter ou vous envoyer du contenu publicitaire.  

Pour plus d’informations, notamment sur la divulgation des informations collectées par chaque niveau, consultez [Données d’utilisation et de diagnostic pour System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

[Déclaration de confidentialité de System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527)



<!--HONumber=Nov16_HO1-->


