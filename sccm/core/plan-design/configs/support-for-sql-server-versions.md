---
title: Prise en charge de SQL Server | System Center Configuration Manager
description: "Découvrez les exigences en matière de version et de configuration de SQL Server pour l’hébergement d’une base de données du site System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b17720021f797d404a89933939427696dfafd7dc


---
# <a name="support-for-sql-server-versions-for-system-center-configuration-manager"></a>Prise en charge des versions de SQL Server pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Chaque site System Center Configuration Manager a besoin d’une version et d’une configuration de SQL Server prises en charge pour héberger la base de données du site.  

##  <a name="a-namebkmkinstancesa-sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> Emplacements et instances de SQL Server  
 **Site d’administration centrale et sites principaux :**  

La base de données du site doit utiliser une installation complète de SQL Server.  

 L’emplacement de SQL Server peut être sur :  

-   L’ordinateur serveur de site  
-   Un ordinateur distant du serveur de site  

Les instances suivantes sont prises en charge :  

-   Instance par défaut ou nommée de SQL Server  
-   Configuration d’instances multiples  
-   Cluster SQL Server - Consultez [Utiliser un cluster SQL Server pour héberger la base de données de site](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)
-   Groupe de disponibilité SQL Server AlwaysOn - Cette option nécessite Configuration Manager 1602 ou version ultérieure. Pour plus d’informations, consultez [SQL Server AlwaysOn pour une base de données de site à haut niveau de disponibilité pour System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)  

> [!NOTE]  
>  Un cluster SQL Server dans une configuration de cluster d'équilibrage de la charge réseau (NLB) n'est pas pris en charge. En outre, la technologie de mise en miroir de base de données SQL Server et la réplication d'égal à égal ne sont pas prises en charge. La réplication transactionnelle standard de SQL Server est prise en charge uniquement pour répliquer des objets sur des points de gestion configurés pour utiliser des [réplicas de base de données](https://technet.microsoft.com/library/mt608546.aspx).  


 **Sites secondaires :**  

 La base de données du site peut utiliser l’instance par défaut d’une installation complète de SQL Server ou de SQL Server Express.  

 L’emplacement de SQL Server doit se trouver sur l’ordinateur serveur de site.  

##  <a name="a-namebkmksqlversionsa-supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Versions de SQL Server prises en charge  
 Dans une hiérarchie comprenant plusieurs sites, chaque site peut utiliser différentes versions de SQL Server pour héberger la base de données du site, dès lors que les versions de SQL Server que vous utilisez sont prises en charge par Configuration Manager.  

 Les versions suivantes de SQL Server sont prises en charge avec System Center Configuration Manager 1511 et versions ultérieures.  

> [!IMPORTANT]  
>  L’utilisation de SQL Server Standard pour la base de données du site d’administration centrale limite le nombre total de clients qu’une hiérarchie peut prendre en charge. Consultez [Taille et échelle en chiffres](../../../core/plan-design/configs/size-and-scale-numbers.md).

### <a name="sql-server-2016---standard-enterprise"></a>SQL Server 2016 - Standard, Enterprise  

Prise en charge avec utilisation de la version 1606.   
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site d'administration centrale  
-   Site principal  
-   Site secondaire  


### <a name="sql-server-2014-sp2---standard-enterprise"></a>SQL Server 2014 SP2 - Standard, Enterprise  

Prise en charge pour les versions 1511 et ultérieures.  
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site d'administration centrale  
-   Site principal  
-   Site secondaire  



### <a name="sql-server-2014-sp1---standard-enterprise"></a>SQL Server 2014 SP1 - Standard, Enterprise  

Prise en charge pour les versions 1511 et ultérieures.  
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site d'administration centrale  
-   Site principal  
-   Site secondaire  


### <a name="sql-server-2012-sp3---standard-enterprise"></a>SQL Server 2012 SP3 – Standard, Enterprise  

Prise en charge pour les versions 1511 et ultérieures.  
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site d'administration centrale  
-   Site principal  
-   Site secondaire  


### <a name="sql-server-2012-sp2---standard-enterprise"></a>SQL Server 2012 SP2 – Standard, Enterprise  

Prise en charge pour les versions 1511 et ultérieures.  
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site d'administration centrale  
-   Site principal  
-   Site secondaire  


### <a name="sql-server-2008-r2-sp3---standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3 – Standard, Enterprise, Datacenter  

Prise en charge pour les versions 1511 et ultérieures.    
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site d'administration centrale  
-   Site principal  
-   Site secondaire  

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Prise en charge avec utilisation de la version 1606.  
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :
-   Site secondaire

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2  
Prise en charge avec utilisation des versions 1511 et ultérieures.  
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site secondaire  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1  
 Prise en charge avec utilisation des versions 1511 et ultérieures.   
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site secondaire  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Prise en charge avec utilisation des versions 1511 et ultérieures.   
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site secondaire  

### <a name="sql-server-2012-express-sp2"></a>SQL Server 2012 Express SP2  
 Prise en charge avec utilisation des versions 1511 et ultérieures.  
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Site secondaire  

##  <a name="a-namebkmksqlconfiga-required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Configurations requises pour SQL Server  
 Les éléments suivants sont requis par toutes les installations de SQL Server que vous utilisez pour une base de données de site (dont SQL Server Express). Quand Configuration Manager installe SQL Server Express dans le cadre d’une installation de site secondaire, ces configurations sont effectuées automatiquement.  

 **Version d’architecture de SQL Server :**  
 Configuration Manager requiert une version 64 bits de SQL Server pour héberger la base de données de site.  

 **Classement de la base de données**  
 Sur chaque site, à la fois l'instance de SQL Server qui est utilisée pour le site et la base de données de site doivent utiliser le classement suivant : **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager prend en charge deux exceptions à ce classement pour satisfaire aux normes définies dans GB18030 pour une utilisation en Chine. Pour plus d’informations, consultez [Prise en charge internationale dans System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **Fonctionnalités SQL Server :**  
 Seule la fonctionnalité **Services Moteur de base de données** est requise pour chaque serveur de site.  

 La réplication de la base de données Configuration Manager ne nécessite pas la fonctionnalité **Réplication SQL Server**. Toutefois, cette configuration de SQL Server est requise si vous utilisez [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Authentification Windows :**  
 Configuration Manager nécessite l’**authentification Windows** pour valider les connexions à la base de données.  

 **Instance SQL Server :**  
 Vous devez utiliser une instance dédiée de SQL Server pour chaque site. Il peut s’agir d’une **instance nommée** ou de l’ **instance par défaut**.  

 **Mémoire de SQL Server :**  
 Réservez de la mémoire pour SQL Server en utilisant SQL Server Management Studio et en définissant le paramètre **Mémoire minimale du serveur** sous **Options mémoire du serveur**. Pour plus d’informations sur la manière de définir une quantité fixe de mémoire, consultez [Procédure : définir une quantité fixe de mémoire (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Serveur de base de données installé sur le même ordinateur que le serveur du site :** Limitez la mémoire pour SQL Server à 50-80 % de la mémoire système adressable disponible.  

-   **Serveur de base de données dédié (distant du serveur de site) :** Limitez la mémoire pour SQL Server à 80-90 % de la mémoire système adressable disponible.  

-   **Réserve de mémoire pour le pool de mémoires tampons de chaque instance SQL Server en cours d’utilisation :**  

    -   Site d’administration centrale : minimum 8 gigaoctets (Go)  
    -   Site principal : minimum 8 gigaoctets (Go)  
    -   Site secondaire : minimum 4 gigaoctets (Go)  

 **Déclencheurs imbriqué SQL :**  

 Les[déclencheurs imbriqués SQL](http://go.microsoft.com/fwlink/?LinkId=528802) doivent être activés.  

 **Intégration du CLR SQL Server**  

  La base de données du site nécessite que le CLR (Common Language Runtime) SQL Server soit activé. Cette option est activée automatiquement lors de l’installation de Configuration Manager. Pour plus d’informations sur le CLR, consultez [Présentation de l’intégration de CLR dans SQL Server](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx)  

##  <a name="a-namebkmkoptionala-optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Configurations facultatives pour SQL Server  
 Les configurations suivantes sont facultatives pour chaque base de données utilisant une installation complète de SQL Server.  

 **Service SQL Server :**  
 Vous pouvez configurer le service SQL Server pour s’exécuter avec les ressources suivantes :  

-   Compte d’**utilisateur local de domaine** :  

    -   Il s’agit d’une bonne pratique qui peut exiger que vous enregistriez manuellement le nom de principal du service (SPN) pour le compte.  

-   Compte**système local** de l’ordinateur exécutant SQL Server :  

    -   Utilisez le compte système local pour simplifier le processus de configuration.  
    -   Quand vous utilisez le compte système local, Configuration Manager inscrit automatiquement le SPN pour le service SQL Server.  
    -   Notez que l’utilisation du compte système local pour le service SQL Server n’est pas une meilleure pratique pour SQL Server.  

Si le serveur SQL Server n’utilise pas ce compte système local d’ordinateur pour exécuter les services SQL Server, vous devez configurer le nom de principal du service (SPN) du compte qui exécute les services SQL Server dans des services de domaine Active Directory. (Quand le compte système est utilisé, le SPN est inscrit automatiquement.)

Pour plus d’informations sur les SPN pour la base de données du site, consultez  [Gérer le SPN pour le serveur de base de données du site](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) dans la rubrique [Modifier votre infrastructure System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  

Pour plus d’informations sur la façon de modifier le compte utilisé par le service SQL Server, consultez [Modifier le compte de démarrage du service pour SQL Server (Gestionnaire de configuration SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services :**  
Requis pour installer un point de Reporting Services permettant de générer des rapports.  

**Ports SQL Server :**  
Pour la communication vers le moteur de base de données SQL Server et pour la réplication intersite, vous pouvez utiliser les configurations du port SQL Server par défaut ou spécifier des ports personnalisés :  

-   Les**communications intersites** utilisent SQL Server Service Broker qui, par défaut, utilise le port TCP 4022.  
-   Les **communications intrasites** entre le moteur de base de données SQL Server et divers rôles système de site Configuration Manager utilisent par défaut le port TCP 1433. Les rôles de système de site suivants communiquent directement avec la base de données SQL Server :  

    -   Point de gestion  
    -   Ordinateur du fournisseur SMS  
    -   Point de Reporting Services  
    -   Serveur de site  

Quand un serveur SQL Server héberge une base de données provenant de plusieurs sites, chaque base de données doit utiliser une instance distincte de SQL Server, et chaque instance doit être configurée pour utiliser un ensemble de ports unique.  

> [!WARNING]  
>  Configuration Manager ne prend pas en charge les ports dynamiques. Étant donné que les instances nommées de SQL Server utilisent par défaut des ports dynamiques pour les connexions au moteur de base de données, lorsque vous utilisez une instance nommée, vous devez configurer manuellement le port statique que vous souhaitez utiliser pour la communication intrasite.  

Si un pare-feu est activé sur l'ordinateur exécutant SQL Server, assurez-vous qu'il est configuré pour autoriser les ports utilisés par votre déploiement et, à tous les emplacements du réseau, entre les ordinateurs qui communiquent avec SQL Server.  

Pour obtenir un exemple montrant comment configurer SQL Server pour utiliser un port spécifique, consultez [Configurer un serveur pour écouter un port TCP spécifique (Gestionnaire de configuration SQL Server)](http://go.microsoft.com/fwlink/p/?LinkID=226349) dans la bibliothèque TechNet relative à SQL Server.  



<!--HONumber=Nov16_HO1-->


