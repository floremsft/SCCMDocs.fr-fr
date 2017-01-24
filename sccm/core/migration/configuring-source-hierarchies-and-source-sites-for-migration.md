---
title: "Hiérarchies sources de migration | Microsoft Docs"
description: "Configurez une hiérarchie source et des sites sources pour permettre la migration de données vers votre environnement System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 1ecac05cb7aba822047bbc519d8a0ca316c600a5


---
# <a name="configuring-source-hierarchies-and-source-sites-for-migration-to-system-center-configuration-manager"></a>Configuration des hiérarchies sources et des sites sources pour la migration vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour permettre la migration de données vers votre environnement System Center Configuration Manager, vous devez configurer une hiérarchie source Configuration Manager prise en charge et, dans cette hiérarchie, configurer un ou plusieurs sites sources contenant les données à migrer.  

> [!NOTE]  
>  Les opérations de migration sont exécutées sur le site de niveau supérieur de la hiérarchie de destination. Si vous configurez la migration à partir d’une console Configuration Manager connectée à un site enfant principal, vous devez donner le temps à la configuration de se répliquer vers le site d’administration centrale, de démarrer, puis de répliquer l’état vers le site principal auquel vous êtes connecté.  

 Pour définir la hiérarchie source et ajouter d'autres sites source, aidez-vous des informations et des procédures figurant dans les sections suivantes. Après avoir exécuté ces procédures, vous pouvez créer des tâches de migration et commencer à migrer les données de la hiérarchie source vers la hiérarchie de destination.  

-   [Spécifier une hiérarchie source pour la migration](#BKBM_ConfigSrcHierarchy)  

-   [Identifier des sites sources supplémentaires dans la hiérarchie source](#BKBM_ConfigSrcSites)  

##  <a name="a-namebkbmconfigsrchierarchya-specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a> Spécifier une hiérarchie source pour la migration  
 Pour migrer les données vers votre hiérarchie de destination, vous devez spécifier une hiérarchie source prise en charge qui contient les données à migrer. Par défaut, le site de niveau supérieur de cette hiérarchie devient un site source de la hiérarchie source. Si vous effectuez la migration à partir d’une hiérarchie Configuration Manager 2007, après avoir collecté les données du site source initial, vous pouvez configurer des sites sources supplémentaires à utiliser pour la migration. Si vous effectuez la migration à partir d’une hiérarchie System Center 2012 Configuration Manager ou System Center Configuration Manager, vous n’avez pas besoin de configurer des sites sources supplémentaires pour migrer les données de la hiérarchie source. Ceci est dû au fait que ces versions de Configuration Manager utilisent une base de données partagée qui est disponible sur le site de niveau supérieur dans la hiérarchie source. La base de données partagée contient toutes les informations que vous pouvez migrer.  

 Utilisez les procédures suivantes pour spécifier une hiérarchie source pour la migration et pour identifier des sites sources supplémentaires dans une hiérarchie Configuration Manager 2007.  

 Effectuez cette procédure dans une console Configuration Manager qui est connectée à la hiérarchie de destination.  

#### <a name="to-configure-a-source-hierarchy"></a>Pour configurer une hiérarchie source  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Hiérarchie source**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Migration** , cliquez sur **Spécifier la hiérarchie source**.  

4.  Dans la boîte de dialogue **Spécifier une hiérarchie source** , pour **Hiérarchie source**, sélectionnez **Nouvelle hiérarchie source**.  

5.  Dans **Serveur de site Configuration Manager de niveau supérieur**, entrez le nom ou l’adresse IP du site de niveau supérieur d’une hiérarchie source prise en charge.  

6.  Spécifiez les comptes d'accès au site source qui disposent des autorisations suivantes :  

    -   Compte du site source : Autorisation **Lecture** pour le fournisseur SMS du site de niveau supérieur spécifié dans la hiérarchie source.  

    -   Compte de base de données du site source : Autorisation **Lecture** et **Exécution** sur la base de données SQL Server du site de niveau supérieur spécifié dans la hiérarchie source.  

     Si vous spécifiez l’utilisation du compte d’ordinateur, Configuration Manager utilise le compte d’ordinateur du site de niveau supérieur de la hiérarchie de destination. Pour cette option, assurez-vous que ce compte est membre du groupe de sécurité **Utilisateurs du modèle COM distribué** dans le domaine où réside le site de niveau supérieur de la hiérarchie source.  

7.  Pour partager des points de distribution entre des hiérarchies source et de destination, activez la case à cocher **Activer le partage du point de distribution pour ce serveur de site source** . Si vous n'activez pas le partage des points de distribution maintenant, vous pouvez le faire en modifiant les informations d'identification du site source après la collecte de données.  

8.  Cliquez sur **OK** pour enregistrer la configuration. La boîte de dialogue **État de la collecte de données** s'ouvre, et la collecte de données démarre automatiquement.  

9. À la fin de la collecte des données, cliquez sur **Fermer** pour fermer la boîte de dialogue **État de la collecte de données** et terminer la configuration.  

##  <a name="a-namebkbmconfigsrcsitesa-identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a> Identifier des sites sources supplémentaires dans la hiérarchie source  
 Lorsque vous configurez une hiérarchie source prise en charge, le site de niveau supérieur de cette hiérarchie est automatiquement configuré comme un site source, et les données sont collectées à partir de celui-ci. L’action suivante à effectuer dépend de la version de Configuration Manager qui est exécutée par la hiérarchie source :  

-   S’il s’agit d’une hiérarchie source Configuration Manager 2007, à la fin de la collecte des données du site source initial, vous pouvez soit commencer la migration uniquement à partir de ce site source initial, soit configurer des sites sources supplémentaires dans la hiérarchie source. Configurez des sites sources supplémentaires dans une hiérarchie Configuration Manager 2007 si vous devez migrer des données qui sont disponibles uniquement sur un site enfant. Par exemple, vous pouvez configurer des sites sources supplémentaires pour recueillir des données relatives au contenu que vous souhaitez migrer lorsque ce contenu a été créé sur un site enfant de la hiérarchie source et qu'il n'est pas disponible sur le site supérieur de la hiérarchie source.  

-   Dans le cas d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, vous n’avez pas besoin de configurer de sites sources supplémentaires. Ceci est dû au fait que ces versions de Configuration Manager utilisent une base de données partagée qui est disponible sur le site de niveau supérieur dans la hiérarchie source. La base de données partagée contient toutes les informations que vous pouvez migrer à partir de tous les sites dans cette hiérarchie source. Par conséquent, les données que vous pouvez migrer sont disponibles à partir du site de niveau supérieur de la hiérarchie source.  

Quand vous configurez des sites sources supplémentaires dans une hiérarchie source Configuration Manager 2007, vous devez les configurer du haut de la hiérarchie source vers le bas. Vous devez configurer un site parent comme site source pour pouvoir configurer ses sites enfant comme sites source.  

Effectuez la procédure suivante pour configurer des sites sources supplémentaires dans une hiérarchie source Configuration Manager 2007.  

#### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Pour identifier des sites sources supplémentaires dans la hiérarchie source  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Hiérarchie source**.  

3.  Cliquez sur le site à configurer comme site source.  

4.  Dans l'onglet **Accueil** , dans le groupe **Site source** , cliquez sur **Configurer**.  

5.  Dans la boîte de dialogue **Informations d'identification du site source** , pour des comptes d'accès de site source, définissez les comptes qui disposent des autorisations suivantes :  

    -   Compte du site source : Autorisation **Lecture** pour le fournisseur SMS du site de niveau supérieur spécifié dans la hiérarchie source.  

    -   Compte de base de données du site source : Autorisation **Lecture** et **Exécution** sur la base de données SQL Server du site de niveau supérieur spécifié dans la hiérarchie source.  

    Si vous spécifiez l’utilisation du compte d’ordinateur, Configuration Manager utilise le compte d’ordinateur du site de niveau supérieur de la hiérarchie de destination. Pour cette option, assurez-vous que ce compte est membre du groupe de sécurité **Utilisateurs du modèle COM distribué** dans le domaine où réside le site de niveau supérieur de la hiérarchie source.  

6.  Pour partager des points de distribution entre des hiérarchies source et de destination, activez la case à cocher **Activer le partage du point de distribution pour ce serveur de site source** . Si vous n'activez pas le partage des points de distribution maintenant, vous pouvez le faire en modifiant les informations d'identification du site source après la collecte de données.  

7.  Cliquez sur **OK** pour enregistrer la configuration. La boîte de dialogue **État de la collecte de données** s'ouvre, et la collecte de données démarre automatiquement.  

8.  À la fin de la collecte des données, cliquez sur **Fermer** pour terminer la configuration.  



<!--HONumber=Dec16_HO3-->


