---
title: "Évaluer System Center Configuration Manager en créant votre propre environnement lab | Microsoft Docs"
description: "Créez un environnement lab pour évaluer System Center Configuration Manager pour une utilisation dans votre organisation."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: 25
caps.handback.revision: 0
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: e72acbe0a2f5592b5bdf9a3612db62bfb066fadf


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Évaluer System Center Configuration Manager en créant votre propre environnement lab

*S’applique à : System Center Configuration Manager (Current Branch)*

Découvrez comment créer un environnement lab pour évaluer System Center Configuration Manager pour une utilisation dans votre organisation.  

## <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Évaluer System Center Configuration Manager en créant votre propre environnement lab  
 System Center Configuration Manager est un outil complexe et puissant pour gérer vos utilisateurs, logiciels et appareils. Nous vous recommandons de procéder à une évaluation approfondie de System Center Configuration Manager avant de procéder à un déploiement complet de façon à combiner vos connaissances conceptuelles à des exercices pratiques.  

 Ce guide s’adresse principalement aux administrateurs qui évaluent l’utilisation de Configuration Manager dans des environnements d’entreprise.  

-   Administrateurs à la recherche d’une solution de gestion complète de PC, serveurs et appareils mobiles  

-   Administrateurs dans les secteurs de haute sécurité qui exigent la sécurité liée à la gestion locale des appareils et la souplesse liée à la gestion des appareils basée sur le cloud  

-   Administrateurs souhaitant gérer la montée en puissance de leur architecture de serveurs locale  

### <a name="what-this-lab-does"></a>Ce que fait ce lab  
 L’objectif principal de la création de cet environnement est de vous fournir les connaissances générales pour vous permettre de commencer à travailler avec Configuration Manager et d’améliorer vos connaissances de cet outil. Nous allons pour cela décrire pas à pas un assembly expédié de la version actuelle de Configuration Manager en utilisant deux serveurs :  

-   L’un hébergeant Active Directory, le contrôleur de domaine et le serveur DNS.  

-   Un autre hébergeant Configuration Manager et tous les composants SQL Server associés.  

-   Les ordinateurs clients sont installés sur Hyper-V. Le lab proprement dit peut aussi être exécuté en tant que système entièrement virtualisé sur un seul serveur.  

### <a name="what-this-lab-does-not-do"></a>Ce que ne fait pas ce lab  
 Ce lab ne décrit pas tous les scénarios Configuration Manager et n’est pas destiné à être migré immédiatement dans un environnement actif.  

 Une fois ce lab généré, vous disposerez d’un environnement de travail opérationnel. Toutefois, cet environnement ne sera pas optimisé pour les performances du système, la gestion de l’espace disque dur, le stockage SQL Server, et ainsi de suite.  

###  <a name="a-namebkmkevalreca-recommended-reading-prior-to-beginning-the-lab"></a><a name="BKMK_EvalRec"></a> Lecture recommandée avant de commencer le lab  
 La [documentation de System Center Configuration Manager](http://docs.microsoft.com/sccm/) propose un contenu très riche. Une sélection de rubriques tirées de cette bibliothèque ont été incluses ci-dessous. Nous conseillons à tous les administrateurs travaillant sur des labs de les lire avant de commencer ces exercices.  

-   Découvrez les concepts de base concernant la console Configuration Manager, les portails d’utilisateurs finaux, ainsi que des exemples de scénarios dans la [présentation de System Center Configuration Manager](../../core/understand/introduction.md).  

-   Découvrez les principales fonctionnalités de gestion de Configuration Manager dans [Fonctions et fonctionnalités de System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Approfondissez vos connaissances avec le document [Principes de base de System Center Configuration Manager](../../core/understand/fundamentals.md).  

-   Découvrez l’importance des rôles de sécurité dans [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   [Concepts de la gestion de contenu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) décrit certains concepts spécifiques relatifs à la gestion de contenu.  

-   [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) peut vous aider à prendre correctement en charge les opérations quotidiennes tout au long de votre déploiement.  



<!--HONumber=Dec16_HO3-->


