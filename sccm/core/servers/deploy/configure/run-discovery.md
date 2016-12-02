---
title: "Exécuter la découverte | System Center Configuration Manager"
description: "Lire une vue d’ensemble du processus de découverte et des enregistrements de données de découverte."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: 20
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d73b493318b0a1938d42265ec03369015365addb


---
# <a name="run-discovery-for-system-center-configuration-manager"></a>Exécuter la découverte pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser une ou plusieurs des méthodes de découverte proposées dans    
      System Center Configuration Manager pour trouver les appareils et les utilisateurs que vous pouvez gérer. Vous pouvez également utiliser la découverte pour identifier l’infrastructure réseau de votre environnement.  Vous disposez de diverses méthodes de découverte permettant de découvrir différents éléments. Chaque méthode a ses propres configurations et limitations.  

## <a name="overview-of-discovery"></a>Vue d’ensemble de la découverte  
 La découverte est le processus par lequel Configuration Manager apprend quels élément vous pouvez gérer. Les méthodes de découverte disponibles sont les suivantes :  

-   Découverte de forêts Active Directory  

-   Découverte de groupes Active Directory  

-   Découverte de systèmes Active Directory  

-   Découverte d’utilisateurs Active Directory  

-   Découverte par pulsations d'inventaire  

-   Découverte du réseau  

-   Découverte de serveurs  

> [!TIP]  
>  Vous pouvez en savoir plus sur chaque méthode de découverte dans [About discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md) (À propos des méthodes de découverte pour System Center Configuration Manager).  
>   
>  Pour savoir quelle méthode privilégier et quel site de votre hiérarchie choisir, consultez [Select discovery methods to use for System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md) (Déterminer quelles méthodes de découverte utiliser pour System Center Configuration Manager).  

 Pour utiliser la plupart des méthodes de découverte, vous devez les activer sur un site et les configurer pour qu’elles effectuent une recherche sur un réseau ou à des emplacements Active Directory spécifiques. Lorsqu’une méthode de découverte est exécutée, elle interroge l’emplacement spécifié afin de recueillir des informations sur les appareils ou utilisateurs que Configuration Manager peut gérer.  Quand une méthode de découverte trouve des informations sur une ressource, elle place celles-ci dans un fichier appelé enregistrement de données de découverte (DDR, Discovery Data Record), qui est traité par un site principal ou un site d’administration centrale. Le traitement d’un fichier DDR génère un nouvel enregistrement dans la base de données du site pour les nouvelles ressources découvertes, ou met à jour des enregistrements existants avec les nouvelles informations.  

 Certaines méthodes de découverte peuvent générer un volume important de trafic réseau, et les fichiers DDR obtenus peuvent entraîner une utilisation intensive des ressources du processeur au cours du traitement. Par conséquent, prévoyez d’utiliser uniquement les méthodes de découverte dont vous avez besoin pour atteindre vos objectifs. Vous pouvez commencer par n’utiliser qu’une ou deux méthodes de découverte, avant d’éventuellement en activer d’autres de manière contrôlée par la suite pour étendre le niveau de découverte dans votre environnement.  

 Une fois les informations de découverte ajoutées à la base de données du site, elles sont répliquées vers chaque site dans la hiérarchie, indépendamment du site sur lequel les informations ont été découvertes ou traitées. Par conséquent, si vous pouvez configurer des planifications et des paramètres différents pour les méthodes de découverte sur différents sites, vous ne pouvez exécuter une méthode de découverte spécifique que sur un seul site afin de réduire l’utilisation de la bande passante réseau par le biais d’actions de détection de doublons, et de réduire le traitement de données de découverte redondantes sur plusieurs sites.  

 Vous pouvez utiliser les données de découverte pour créer des regroupements et requêtes personnalisés qui regroupent logiquement des ressources pour les tâches de gestion suivantes, par exemple :  

-   effectuer une installation Push du client ou une mise à niveau ;  

-   déployer du contenu vers des utilisateurs ou appareils ;  

-   déployer des paramètres client et les configurations associées.  

##  <a name="a-namebkmkddrsa-about-discovery-data-records"></a><a name="BKMK_DDRs"></a> À propos des enregistrements de données de découverte  
 Les enregistrements de données de découverte (DDR) sont des fichiers créés par une méthode de découverte ; ils contiennent des informations sur une ressource que vous pouvez gérer dans Configuration Manager. Les DDR contiennent des informations sur les ordinateurs, les utilisateurs et, dans certains cas, l'infrastructure du réseau. Ils sont traités au niveau des sites principaux ou des sites d'administration centrale. Une fois que les informations sur la ressource contenues dans le DDR ont été entrées dans la base de données, le DDR est supprimé et cette information est répliquée sous forme de données globales vers tous les sites de la hiérarchie.  

 Le site où un DDR est traité dépend des informations qu'il contient :  

-   Les DDR des ressources nouvellement découvertes, qui ne sont pas dans la base de données, sont traités sur le site de niveau supérieur de la hiérarchie. Le site de niveau supérieur crée un nouvel enregistrement de ressource dans la base de données et lui attribue un identifiant unique. Les DDR sont transférés par réplication basée sur les fichiers, jusqu'à ce qu'ils atteignent le site de niveau supérieur.  

-   Les DDR d'objets précédemment découverts sont traités au niveau des sites principaux. Les sites enfants principaux ne transfèrent pas de DDR au site d'administration centrale lorsque le DDR contient des informations sur une ressource qui est déjà dans la base de données.  

-   Les sites secondaires ne traitent pas les enregistrements de données de découverte, mais les transfèrent toujours par une réplication basée sur les fichiers vers leur site principal parent.  

Les fichiers DDR sont identifiés par l'extension .ddr et ont généralement une taille standard d'environ 1 Ko.  

## <a name="get-started-with-discovery"></a>Prise en main de la découverte :  
 Avant d’utiliser la console Configuration Manager pour configurer la découverte, vous devez comprendre les différences entre les méthodes, les opérations possibles et, pour certaines d’entre elles, leurs limites.  
Les rubriques suivantes peuvent vous aider à utiliser correctement les méthodes de découverte :  

-   [À propos des méthodes de découverte pour System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Sélectionner les méthodes de découverte à utiliser pour System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Dès lors que vous avez déterminé quelles méthodes utiliser, vous pouvez les configurer en vous aidant des conseils fournis dans [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md) (Configurer les méthodes de découverte pour System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


