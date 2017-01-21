---
title: Package Transfer Manager | System Center Configuration Manager
description: "Découvrez comment le composant Package Transfer Manager de System Center Configuration Manager transfère le contenu d’un serveur de site vers des points de distribution distants."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e77925ce15f20afe463860a22bf670108bbee344

---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Package Transfer Manager dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans un site System Center Configuration Manager, Package Transfer Manager est un composant du service SMS_Executive qui est chargé de gérer le transfert de contenu d’un ordinateur serveur de site vers les points de distribution distants d’un site. (Un point de distribution est dit distant s’il ne se trouve pas sur l’ordinateur serveur de site.) Le composant Package Transfer Manager ne prend pas en charge les configurations effectuées par l’administrateur, mais le fait de comprendre comment il fonctionne peut vous aider à planifier votre infrastructure de gestion de contenu et à résoudre les problèmes de distribution de contenu.


Quand vous distribuez du contenu vers un ou plusieurs points de distribution distants d’un site, le **Gestionnaire de distribution** crée une tâche de transfert de contenu et indique à Package Transfer Manager, sur les serveurs de site principal et secondaire, de transférer le contenu vers des points de distribution distants.

 Package Transfer Manager consigne ses actions dans le fichier **pkgxfermgr.log** sur le serveur de site. Le fichier journal est le seul emplacement où vous pouvez voir les activités du Package Transfer Manager.  

> [!NOTE]  
>  Dans les versions précédentes de Configuration Manager, le gestionnaire de distribution gère le transfert de contenu à destination d’un point de distribution distant. Le gestionnaire de distribution gère également le transfert de contenu entre sites. Avec System Center Configuration Manager, le gestionnaire de distribution continue de gérer le transfert de contenu entre deux sites. Cependant, Package Transfer Manager permet à Configuration Manager de décharger depuis le gestionnaire de distribution les opérations nécessaires pour transférer du contenu vers un grand nombre de points de distribution. Par rapport aux versions précédentes du produit, cela permet d'améliorer les performances générales de déploiement de contenu à la fois entre les sites et vers les points de distribution au sein d'un site.  

 Pour transférer du contenu vers un point de distribution standard, Package Transfer Manager fonctionne de la même façon que le gestionnaire de distribution des versions précédentes de Configuration Manager. En d'autres termes, il gère activement le transfert de fichiers pour chaque point de distribution distant. Cependant, pour distribuer du contenu vers un point de distribution d'extraction, Package Transfer Manager informe le point de distribution d'extraction que du contenu est disponible et transmet le processus de transfert de ce contenu au point de distribution d'extraction.  

Les informations suivantes expliquent comment Package Transfer Manager gère le transfert de contenu vers les points de distribution standard et les points de distribution configurés en tant que points de distribution d’extraction :
1.  **L’utilisateur administrateur déploie le contenu vers un ou plusieurs points de distribution sur un site**  

    -   **Point de distribution standard** : le gestionnaire de distribution crée un travail de transfert de contenu pour ce contenu.  

    -   **Point de distribution d’extraction** : le gestionnaire de distribution crée un travail de transfert de contenu pour ce contenu.  

2.  **Le gestionnaire de distribution exécute des vérifications préliminaires**  

    -   **Point de distribution standard** : le gestionnaire de distribution exécute une vérification de base pour s’assurer que chaque point de distribution est prêt à recevoir le contenu. Après cette vérification, le gestionnaire de distribution instruit Package Transfer Manager de démarrer le transfert de contenu vers le point de distribution.  

    -   **Point de distribution d’extraction** : le gestionnaire de distribution démarre Package Transfer Manager, qui informe le point de distribution d’extraction qu’il existe un nouveau travail de transfert de contenu pour le point de distribution. Le gestionnaire de distribution ne vérifie pas l'état des points de distribution distants qui sont des points de distribution d'extraction, car chaque point de distribution d'extraction gère ses propres transferts de contenu.  

3.  **Package Transfer Manager prépare le transfert du contenu**  

    -   **Point de distribution standard** : Package Transfer Manager examine le magasin de contenu à instance unique de chaque point de distribution distant spécifié pour identifier les fichiers qui se trouvent déjà sur ce point de distribution. Ensuite, Package Transfer Manager met en file d'attente le transfert uniquement des fichiers qui ne sont pas déjà présents.  

        > [!NOTE]  
        >  Lorsque vous utilisez l'action **Redistribuer** pour le contenu, Package Transfer Manager copie chaque fichier à distribuer vers le point de distribution, même si les fichiers sont déjà présents dans le magasin d'instances uniques du point de distribution.  

    -   **Point de distribution d’extraction** : pour chaque point de distribution d’extraction de la distribution, Package Transfer Manager vérifie les points de distribution source des points de distribution d’extraction pour s’assurer que le contenu est disponible :  

        -   Lorsque le contenu est disponible sur au moins un point de distribution source, Package Transfer Manager envoie une notification à ce point de distribution d'extraction pour lui indiquer de commencer le processus de transfert de contenu. La notification inclut les noms de fichiers et les tailles, les attributs et les valeurs de hachage.  

        -   Lorsque le contenu n'est pas encore disponible, Package Transfer Manager n'envoie pas de notification au point de distribution. Il répète la vérification toutes les 20 minutes jusqu'à ce que le contenu soit disponible. Puis, lorsque le contenu est disponible, Package Transfer Manager envoie la notification à ce point de distribution d'extraction.  

        > [!NOTE]  
        >  Lorsque vous utilisez l'action **Redistribuer** pour le contenu, le point de distribution d'extraction copie chaque fichier à distribuer vers le point de distribution, même si les fichiers sont déjà présents dans le magasin d'instances uniques du point de distribution d'extraction.  

4.  **Le transfert du contenu commence**  

    -   **Point de distribution standard** : Package Transfer Manager copie les fichiers sur chaque point de distribution distant. Lors du transfert vers un point de distribution standard :  

        -   Par défaut, Package Transfer Manager peut traiter simultanément trois packages uniques et les distribuer à cinq points de distribution en parallèle. Ce sont les **Paramètres de distribution simultanée** , qui sont configurés sur l'onglet **Général** dans **Propriétés du composant de distribution de logiciels** pour chaque site.  

        -   Package Transfer Manager utilise les configurations de la bande passante réseau et de la planification de chaque point de distribution lors du transfert de contenu vers ce point de distribution. Ces paramètres sont configurés dans les onglets **Planification** et **Limites du taux de transfert** des **Propriétés** de chaque point de distribution distant. Pour plus d’informations, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Point de distribution d’extraction** : quand un point de distribution d’extraction reçoit un fichier de notification, le point de distribution commence le processus de transfert du contenu. Le processus de transfert s'exécute indépendamment sur chaque point de distribution d'extraction :  

        -   La distribution d'extraction identifie les fichiers dans la distribution de contenu qui ne se trouvent pas déjà dans son magasin d'instances uniques et prépare le téléchargement de ce contenu depuis un de ses points de distribution source.  

        -   Ensuite, le point de distribution d'extraction vérifie chacun de ses points de distribution source, dans l'ordre, jusqu'à ce qu'il trouve un point de distribution source disposant du contenu. Lorsque le point de distribution d'extraction identifie un point de distribution source avec le contenu, il commence le téléchargement de ce contenu.  

        > [!NOTE]  
        >  Le processus de téléchargement de contenu du point de distribution d’extraction est le même que celui des clients Configuration Manager. Pour le transfert de contenu par le point de distribution d'extraction, ni les paramètres de transfert simultané, ni les options de planification et de limitation que vous configurez pour les points de distribution standard ne sont utilisés.  

5.  **Fin du transfert de contenu**  

    -   **Point de distribution standard** : une fois que Package Transfer Manager a terminé le transfert de fichiers vers chaque point de distribution distant désigné, il vérifie le hachage du contenu sur le point de distribution et informe le gestionnaire de distribution que la distribution est terminée.  

    -   **Point de distribution d’extraction** : une fois que le point de distribution d’extraction a terminé le téléchargement du contenu, le point de distribution vérifie le hachage du contenu et envoie un message d’état au point de gestion des sites pour indiquer que l’opération a abouti. Toutefois, si l'état n'est pas reçu après 60 minutes, Package Transfer Manager sort de veille et vérifie auprès du point de distribution d'extraction pour confirmer si le contenu a été téléchargé. Si le téléchargement du contenu est en cours, Package Transfer Manager se met en veille pendant 60 minutes avant de vérifier de nouveau auprès du point de distribution d'extraction. Ce cycle se répète jusqu'à ce que le point de distribution d'extraction termine le transfert du contenu.  



<!--HONumber=Nov16_HO1-->


