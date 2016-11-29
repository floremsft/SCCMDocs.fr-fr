---
title: "Utilisation des données de diagnostic | System Center Configuration Manager"
description: "Découvrez comment Microsoft utilise les données de diagnostic et d’utilisation collectées par System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 68e2a6b5baeaf9ab9e74e771bbc3d755d1388779


---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Utilisation des données d’utilisation et de diagnostic pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les données d’utilisation et de diagnostic collectées pour System Center Configuration Manager fournissent à Microsoft un retour d’expérience quasi immédiat sur la manière dont le produit fonctionne (ou ne fonctionne pas), et permettent d’améliorer les mises à jour ultérieures. Nous pouvons également voir des données de configuration qui nous aident à concevoir et tester les configurations qui sont en production. Exemple :  

-   Versions de Windows Server utilisées par les serveurs de site  

-   Modules linguistiques installés  

-   Différentiel du schéma SQL par rapport aux paramètres par défaut du produit  

Ces données aident l’équipe de conception à planifier les prochains tests visant à garantir la meilleure expérience possible pour les configurations les plus courantes. Les mises à jour de Configuration Manager étant publiées à un rythme plus soutenu (pour mieux prendre en charge les technologies qui évoluent rapidement, telles que Windows 10 et Microsoft Intune), ces données sont cruciales pour une adaptation rapide.  

Il est également important de savoir comment les données d’utilisation et de diagnostic ne sont pas utilisées. Microsoft n’utilise pas ces données pour ce qui suit :  

-   Audits de licence (par exemple, comparer l’utilisation des clients avec les contrats de licence)  

-   Audit de produits non pris en charge  

-   Publicité basée sur des données disponibles, telles que l’utilisation de fonctionnalités ou la géolocalisation (fuseau horaire)  

##  <a name="a-namebkmkimprovea-examples-of-how-diagnostics-and-usage-data-is-improving-the-product"></a><a name="bkmk_improve"></a> Exemples de la façon dont les données de diagnostic et d’utilisation contribuent à l’amélioration du produit  
Microsoft utilise les données disponibles pour améliorer le produit. Voici quelques exemples de la manière de procéder :  

-   **Prise en charge révisée pour les systèmes d’exploitation serveur plus anciens :**  

     La prise en charge initiale offerte par System Center Configuration Manager (Current Branch) comprenait une limite quant à la période de prise en charge de Windows Server 2008 R2. Après examen des données d’utilisation de clients qui avaient effectué une mise à niveau vers la version Current Branch de Configuration Manager, nous avons jugé utile de modifier et d’étendre cette période pour prendre en charge les nombreux clients qui continuaient d’utiliser ce système d’exploitation serveur pour héberger des serveurs de site et des rôles de système de site.  

-   **Vérifications de configuration requise améliorées :**  

     Sur la base des données d’utilisation, nous avons amélioré les vérifications des conditions requises pour l’installation d’une mise à jour, afin de supprimer des règles obsolètes, de tenir compte de cas supplémentaires et, dans certains cas, de remédier automatiquement à certains problèmes.  



<!--HONumber=Nov16_HO1-->


