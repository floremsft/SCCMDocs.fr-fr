---
title: "Gérer la bande passante du réseau pour le contenu | Microsoft Docs"
description: "Découvrez comment configurer la planification, la limitation de bande passante et le contenu préparé pour System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 14ce376f385ec19d224e8b1a2918eed5379a64e5


---

##  <a name="a-namebkmkplanningforthrottlingascheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Planification et limitation de bande passante  
 Pour mieux gérer la bande passante réseau utilisée pour la gestion du contenu, vous pouvez utiliser les commandes Configuration Manager intégrées de planification et de limitation de bande passante, ou préparer du contenu.  

 Lorsque vous créez un package, modifiez le chemin source du contenu ou mettez à jour le contenu sur le point de distribution, les fichiers sont copiés depuis le chemin source vers la bibliothèque de contenu sur le serveur de site. Ensuite, le contenu est copié depuis la bibliothèque de contenu sur le serveur de site vers la bibliothèque de contenu sur les points de distribution. Si des fichiers sources de contenu sont mis à jour et que ces fichiers ont déjà été distribués, Configuration Manager récupère uniquement les fichiers nouveaux ou mis à jour, puis il les envoie au point de distribution. Les commandes de planification et de limitation peuvent être configurées pour la communication entre sites et pour la communication entre un serveur de site et un point de distribution distant. Si la bande passante réseau entre le serveur de site et le point de distribution distant est limitée même après que vous avez configuré le calendrier et les paramètres de limitation, vous pouvez envisager de préparer le contenu sur le point de distribution.  

 Dans Configuration Manager, vous pouvez configurer un calendrier et définir des paramètres de limitation de bande passante spécifiques sur des points de distribution distants qui déterminent quand et comment s’effectue la distribution du contenu. Chaque point de distribution distant peut avoir différentes configurations qui permettent de répondre aux limitations de la bande passante réseau à partir du serveur de site pour le point de distribution distant. Les commandes utilisées pour la planification et la limitation vers le point de distribution distant sont similaires aux paramètres pour une adresse d'expéditeur standard, mais dans ce cas, les paramètres sont utilisés par un nouveau composant appelé Package Transfer Manager. Package Transfer Manager distribue le contenu à partir d'un serveur de site, site principal ou secondaire, vers un point de distribution qui est installé sur un système de site. Les paramètres de limitation sont configurés sur l'onglet **Limites du taux de transfert** et les paramètres de planification sont configurés sur l'onglet **Calendrier** pour un point de distribution qui ne se trouve pas sur un serveur de site. Les paramètres d'heure sont basés sur le fuseau horaire du site émetteur, et non sur le point de distribution.  

> [!WARNING]  
>  Les onglets **Limites du taux de transfert** et **Calendrier** sont affichés uniquement dans les propriétés des points de distribution qui ne sont pas installés sur un serveur de site.  

Pour plus d’informations sur la configuration des paramètres de planification et de limitation de bande passante pour un point de distribution distant, consultez [Installer et configurer des points de distribution pour System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

##  <a name="a-namebkmkprestagingcontentaprestaged-content"></a><a name="BKMK_PrestagingContent"></a>Contenu préparé  
 Vous pouvez préparer du contenu pour ajouter les fichiers de contenu à la bibliothèque de contenu sur un serveur de site ou sur un point de distribution avant de distribuer le contenu.  

-   Comme les fichiers de contenu sont déjà dans la bibliothèque de contenu, ils ne sont pas transférés via le réseau quand vous distribuez le contenu.  

-   Vous pouvez préparer des fichiers de contenu pour les applications et les packages.  

Dans la console Configuration Manager, sélectionnez le contenu à préparer, puis utilisez l’**Assistant Création du fichier de contenu préparé** pour créer un fichier de contenu préparé compressé qui contient les fichiers et les métadonnées associées pour le contenu. Vous pouvez ensuite importer manuellement le contenu au niveau d'un serveur de site ou d'un point de distribution.  

-   Quand vous importez le fichier de contenu préparé sur un serveur de site, les fichiers de contenu sont ajoutés à la bibliothèque de contenu sur le serveur de site, puis enregistrés dans la base de données du serveur de site.  

-   Quand vous importez le fichier de contenu préparé sur un point de distribution, les fichiers de contenu sont ajoutés à la bibliothèque de contenu sur le point de distribution, et un message d’état est envoyé au serveur de site qui informe le site que le contenu est disponible sur le point de distribution.  

Vous pouvez éventuellement configurer le point de distribution comme **préparé** pour faciliter la gestion de la distribution de contenu. Ensuite, quand vous distribuez le contenu, choisissez l’option souhaitée :  

-   Toujours préparer le contenu sur le point de distribution  

-   Préparer le contenu initial pour le package, puis utiliser le processus de distribution de contenu standard lorsque des mises à jour du contenu sont disponibles  

-   Toujours utiliser le processus de distribution de contenu standard pour le contenu du package  

###  <a name="a-namebkmkdeterminetoprestagecontentadetermine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Déterminer si vous devez préparer du contenu  
 Envisagez de préparer du contenu pour les applications et les packages dans les cas suivants :  

-   **Bande passante réseau limitée depuis le serveur de site vers le point de distribution** : si la planification et la limitation ne répondent pas à vos besoins en matière de distribution de contenu sur le réseau vers un point de distribution distant, envisagez de préparer le contenu sur le point de distribution. Chaque point de distribution est associé au paramètre **Activer ce point de distribution pour le contenu préparé** que vous pouvez configurer dans les propriétés du point de distribution. Lorsque vous activez cette option, le point de distribution est identifié comme un point de distribution préparé et vous pouvez choisir comment gérer le contenu pour chaque package.  

     Les paramètres suivants sont disponibles dans les propriétés d'une application, d'un package, d'un package de pilotes, d'une image de démarrage, du programme d'installation d'un système d'exploitation et d'une image et ils vous permettent de configurer la manière dont la distribution du contenu est gérée sur des points de distribution distants qui sont identifiés comme préparés :  

    -   **Télécharger automatiquement le contenu lorsque des packages sont attribués à des points de distribution**: utilisez cette option lorsque vous disposez de packages plus petits pour lesquels les paramètres de planification et de limitation offrent suffisamment de contrôle pour la distribution de contenu.  

    -   **Télécharger uniquement les modifications de contenu vers le point de distribution**: utilisez cette option si vous disposez d’un package initial qui est éventuellement volumineux et si vous prévoyez que les futures mises à jour du contenu du package seront normalement plus petites. Par exemple, vous pouvez préparer une application telle que Microsoft Office, car la taille du package initial est supérieure à 700 Mo et trop volumineuse pour être envoyée via le réseau. Toutefois, les mises à jour du contenu pour ce package peuvent être inférieures à 10 Mo et distribuables sur le réseau. Un autre exemple pourrait être des packages de pilotes dont la taille initiale est importante, mais des ajouts de pilotes incrémentiels au package petits.  

    -   **Copier manuellement le contenu de ce package vers le point de distribution**: Utilisez cette option pour les cas où vous disposez de packages volumineux, avec du contenu tel qu'un système d'exploitation et n'utilisez jamais le réseau pour distribuer le contenu vers le point de distribution. Lorsque vous sélectionnez cette option, vous devez préparer le contenu sur le point de distribution.  

    > [!WARNING]  
    >  Les options précédentes sont applicables pour chaque package et ne sont utilisées que lorsqu'un point de distribution est identifié comme préparé. Les points de distribution qui n'ont pas été identifiés comme préparés ignorent ces paramètres. Dans ce cas, le contenu est toujours distribué via le réseau à partir du serveur de site vers les points de distribution.  

-   **Restaurer la bibliothèque de contenu sur un serveur de site**: lors de la défaillance d'un serveur de site, les informations sur les packages et applications inclus dans la bibliothèque de contenu sont restaurées vers la base de données de site dans le cadre du processus de restauration, mais les fichiers de la bibliothèque de contenu ne sont pas restaurés dans le cadre du processus. Si vous ne disposez pas d'une sauvegarde du système de fichiers pour restaurer la bibliothèque de contenu, vous pouvez créer un fichier de contenu préparé à partir d'un autre site contenant les packages et applications que vous devez avoir, puis extraire le fichier de contenu préparé sur le serveur de site récupéré. Pour plus d’informations sur la sauvegarde et la récupération du serveur de site, consultez [Sauvegarder et récupérer dans System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery)  



<!--HONumber=Dec16_HO3-->


