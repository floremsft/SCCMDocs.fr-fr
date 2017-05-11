---
title: "Versions SQL Server prises en charge | Microsoft Docs"
description: "Découvrez les exigences en matière de version et de configuration de SQL Server pour l’hébergement d’une base de données du site System Center Configuration Manager."
ms.custom: na
ms.date: 05/01/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: d5a6fdc9a526c4fc3a9027dcedf1dd66a6fff5a7
ms.openlocfilehash: fa7f232fd385f742bb11c6596c954d87c2da87a8
ms.contentlocale: fr-fr
ms.lasthandoff: 05/01/2017


---
# <a name="supported-sql-server-versions-for-system-center-configuration-manager"></a>Versions SQL Server prises en charge pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Chaque site System Center Configuration Manager a besoin d’une version et d’une configuration de SQL Server prises en charge pour héberger la base de données du site.  

##  <a name="bkmk_Instances"></a> Emplacements et instances SQL Server  
 **Site d’administration centrale et sites principaux :**  
La base de données du site doit utiliser une installation complète de SQL Server.  

 SQL Server peut être à l’un de ces emplacements :  

-   L’ordinateur de serveur de site.  
-   Un ordinateur distant du serveur de site.  

Les instances suivantes sont prises en charge :  

-   L’instance par défaut ou nommée de SQL Server.  
-   Des configurations d’instances multiples.  
-   Un cluster SQL Server. Consultez [Utiliser un cluster SQL Server pour héberger la base de données de site](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
-   Un groupe de disponibilité SQL Server AlwaysOn. Cette option nécessite Configuration Manager version 1602 ou ultérieure. Pour plus d’informations, consultez [SQL Server AlwaysOn pour une base de données de site à haut niveau de disponibilité pour System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

> [!NOTE]  
>  L’utilisation d’un cluster SQL Server dans une configuration de cluster d’équilibrage de la charge réseau (NLB) n’est pas prise en charge. La technologie de mise en miroir de base de données SQL Server et la réplication d’égal à égal ne sont pas prises en charge non plus. La réplication transactionnelle standard de SQL Server est prise en charge uniquement pour répliquer des objets sur des points de gestion configurés pour utiliser des [réplicas de base de données](https://technet.microsoft.com/library/mt608546.aspx).  


 **Sites secondaires :**  
 La base de données du site peut utiliser l’instance par défaut d’une installation complète de SQL Server ou de SQL Server Express.  

 SQL Server doit se trouver sur l’ordinateur du serveur de site.  

##  <a name="bkmk_SQLVersions"></a> Versions SQL Server prises en charge  
 Dans une hiérarchie comprenant plusieurs sites, chaque site peut utiliser différentes versions de SQL Server pour héberger la base de données du site, dès lors que les conditions suivantes sont réunies :
 -  Configuration Manager prend en charge les versions de SQL Server que vous utilisez.
 -  Les versions SQL Server que vous utilisez restent prises en charge par Microsoft.
 -  SQL Server prend en charge la réplication entre les deux versions de SQL Server.  Par exemple, [SQL Server ne prend pas en charge la réplication entre SQL Server 2008 R2 et SQL Server 2016](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication).



 Sauf indication contraire, les versions suivantes de SQL Server sont prises en charge avec toutes les versions System Center Configuration Manager actives. Si vous ajoutez la prise en charge d’une nouvelle version de SQL Server ou un Service Pack, la version de Configuration Manager qui ajoute cette prise en charge sera indiquée. De même, si la prise en charge est déconseillée, recherchez plus d’informations sur les versions Configuration Manager concernées.   

La prise en charge d’un Service Pack de SQL Server spécifique inclut des mises à jour cumulatives pour ce Service Pack, sauf si une mise à jour cumulative interrompt la compatibilité descendante vers cette version du Service Pack de base. Si aucune version du Service Pack n’est indiquée, la prise en charge s’applique à cette version de SQL Server sans Service Pack. À l’avenir, si un Service Pack est fourni pour cette version, une instruction de prise en charge dinstincte sera déclarée avant que cette version du Service Pack ne soit prise en charge.


> [!IMPORTANT]  
>  Si vous utilisez SQL Server Standard pour la base de données du site d’administration centrale, vous limitez le nombre total de clients qu’une hiérarchie peut prendre en charge. Consultez [Taille et échelle en chiffres](../../../core/plan-design/configs/size-and-scale-numbers.md).

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1 : Standard, Enterprise  
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site d’administration centrale  
-   Un serveur de site principal  
-   Un site secondaire  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016 :- Standard, Enterprise  
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site d’administration centrale  
-   Un serveur de site principal  
-   Un site secondaire  


### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2 : Standard, Enterprise  
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site d’administration centrale  
-   Un serveur de site principal  
-   Un site secondaire



### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1 : Standard, Enterprise  
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site d’administration centrale  
-   Un serveur de site principal  
-   Un site secondaire


### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3 : Standard, Enterprise  
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site d’administration centrale  
-   Un serveur de site principal  
-   Un site secondaire  


### <a name="sql-server-2012-sp2-standard-enterprise"></a>SQL Server 2012 SP2 : Standard, Enterprise   
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site d’administration centrale  
-   Un serveur de site principal  
-   Un site secondaire  


### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3 : Standard, Enterprise, Datacenter     
  Cette version de SQL Server n’est pas prise en charge [depuis la version 1702](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-support-for-sql-server-versions-as-a-site-database).  
 Cette version de SQL Server reste prise en charge si vous utilisez une version de Configuration Manager antérieure à la version 1702.

Si elle est prise en charge par votre version de Configuration Manager, vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site d’administration centrale  
-   Un serveur de site principal
-   Un site secondaire



### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :
-   Un site secondaire

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :
-   Un site secondaire


### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site secondaire  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site secondaire  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site secondaire  

### <a name="sql-server-2012-express-sp2"></a>SQL Server 2012 Express SP2   
 Vous pouvez utiliser cette version de SQL Server sans version de mise à jour cumulative minimale pour les éléments suivants :  

-   Un site secondaire  

##  <a name="bkmk_SQLConfig"></a> Configurations requises pour SQL Server  
 Les éléments suivants sont nécessaires pour toutes les installations de SQL Server que vous utilisez pour une base de données de site (y compris SQL Server Express). Quand Configuration Manager installe SQL Server Express dans le cadre d’une installation de site secondaire, ces configurations sont créées automatiquement.  

 **Version d’architecture de SQL Server :**  
 Configuration Manager requiert une version 64 bits de SQL Server pour héberger la base de données de site.  

 **Classement de la base de données**  
 Sur chaque site, à la fois l'instance de SQL Server qui est utilisée pour le site et la base de données de site doivent utiliser le classement suivant : **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager prend en charge deux exceptions à ce classement pour satisfaire aux normes définies dans GB18030 pour une utilisation en Chine. Pour plus d’informations, consultez [Prise en charge internationale dans System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **Fonctionnalités SQL Server :**  
 Seule la fonctionnalité **Services Moteur de base de données** est requise pour chaque serveur de site.  

 La réplication de la base de données Configuration Manager ne nécessite pas la fonctionnalité **Réplication SQL Server**. Toutefois, cette configuration de SQL Server est requise si vous utilisez des [réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Authentification Windows :**  
 Configuration Manager nécessite l’**authentification Windows** pour valider les connexions à la base de données.  

 **Instance SQL Server :**  
 Vous devez utiliser une instance dédiée de SQL Server pour chaque site. Il peut s’agir d’une **instance nommée** ou de l’ **instance par défaut**.  

 **Mémoire de SQL Server :**  
 Réservez de la mémoire pour SQL Server en utilisant SQL Server Management Studio et en définissant le paramètre **Mémoire minimale du serveur** sous **Options mémoire du serveur**. Pour plus d’informations sur la manière de définir une quantité fixe de mémoire, consultez [Procédure : définir une quantité fixe de mémoire (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Pour un serveur de base de données installé sur le même ordinateur que le serveur du site :** limitez la mémoire pour SQL Server à 50-80 % de la mémoire système adressable disponible.  

-   **Pour un serveur de base de données dédié (distant du serveur de site) :** limitez la mémoire pour SQL Server à 80-90 % de la mémoire système adressable disponible.  

-   **Pour une réserve de mémoire pour le pool de mémoires tampons de chaque instance SQL Server en cours d’utilisation :**  

    -   Pour un site d’administration centrale, définissez un minimum de 8 gigaoctets (Go).  
    -   Pour un site principal, définissez un minimum de 8 gigaoctets (Go).  
    -   Pour un site secondaire, définissez un minimum de 4 gigaoctets (Go).  

**Déclencheurs imbriqué SQL :**  
Les [déclencheurs imbriqués SQL](http://go.microsoft.com/fwlink/?LinkId=528802) doivent être activés.  

 **Intégration du CLR SQL Server**  
  La base de données du site nécessite que le CLR (Common Language Runtime) SQL Server soit activé. Cette option est activée automatiquement lors de l’installation de Configuration Manager. Pour plus d’informations sur le CLR, consultez [Présentation de l’intégration de CLR dans SQL Server](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx).  

##  <a name="bkmk_optional"></a> Configurations facultatives pour SQL Server  
 Les configurations suivantes sont facultatives pour chaque base de données utilisant une installation complète de SQL Server.  

 **Service SQL Server :**  
 Vous pouvez configurer le service SQL Server pour s’exécuter avec les ressources suivantes :  

-   Le compte d’**utilisateur local de domaine** :  

    -   Il s’agit d’une bonne pratique qui peut exiger que vous enregistriez manuellement le nom de principal du service (SPN) pour le compte.  

-   Le compte **système local** de l’ordinateur exécutant SQL Server :  

    -   Utilisez le compte système local pour simplifier le processus de configuration.  
    -   Quand vous utilisez le compte système local, Configuration Manager inscrit automatiquement le SPN pour le service SQL Server.  
    -   Notez que l’utilisation du compte système local pour le service SQL Server n’est pas une bonne pratique pour SQL Server.  

Si l’ordinateur qui exécute SQL Server n’utilise pas son compte système local pour exécuter le service SQL Server, vous devez configurer le SPN du compte qui exécute le service SQL Server dans Active Directory Domain Services. (Quand le compte système est utilisé, le SPN est inscrit automatiquement.)

Pour plus d’informations sur les SPN pour la base de données du site, consultez [Gérer le SPN pour le serveur de base de données du site](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) dans la rubrique [Modifier votre infrastructure System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  

Pour plus d’informations sur la façon de modifier le compte utilisé par le service SQL Server, consultez [Modifier le compte de démarrage du service pour SQL Server (Gestionnaire de configuration SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services :**  
SQL Server Reporting Services est nécessaire pour installer un point de Reporting Services permettant de générer des rapports.  

> [!IMPORTANT]  
> Une fois SQL Server mis à niveau à partir d’une version précédente, l’erreur suivante peut s’afficher : *Le Générateur de rapports n’existe pas*.    
> Pour corriger cette erreur, vous devez réinstaller le rôle de système de site du point de Reporting Services.

**Ports SQL Server :**  
Pour la communication vers le moteur de base de données SQL Server et pour la réplication intersites, vous pouvez utiliser les configurations de port SQL Server par défaut ou spécifier des ports personnalisés :  

-   Les **communications intersites** font appel à SQL Server Service Broker, qui utilise le port TCP 4022 par défaut.  
-   Les **communications intrasite** entre le moteur de base de données SQL Server et les divers rôles de système de site Configuration Manager utilisent le port TCP 1433 par défaut. Les rôles de système de site suivants communiquent directement avec la base de données SQL Server :  

    -   Point de gestion  
    -   Ordinateur du fournisseur SMS  
    -   Point de Reporting Services  
    -   Serveur de site  

Quand un ordinateur exécutant SQL Server héberge une base de données de plusieurs sites, chaque base de données doit utiliser une instance distincte de SQL Server. De plus, chaque instance doit être configurée pour utiliser un ensemble de ports unique.  

> [!WARNING]  
>  Configuration Manager ne prend pas en charge les ports dynamiques. Étant donné que les instances nommées de SQL Server utilisent par défaut des ports dynamiques pour les connexions au moteur de base de données, lorsque vous utilisez une instance nommée, vous devez configurer manuellement le port statique que vous souhaitez utiliser pour la communication intrasite.  

Si un pare-feu est activé sur l'ordinateur exécutant SQL Server, assurez-vous qu'il est configuré pour autoriser les ports utilisés par votre déploiement et, à tous les emplacements du réseau, entre les ordinateurs qui communiquent avec SQL Server.  

Pour obtenir un exemple montrant comment configurer SQL Server pour utiliser un port spécifique, consultez [Configurer un serveur pour écouter un port TCP spécifique (Gestionnaire de configuration SQL Server)](http://go.microsoft.com/fwlink/p/?LinkID=226349) dans la bibliothèque TechNet relative à SQL Server.  

## <a name="upgrade-options-for-sql-server"></a>Options de mise à niveau pour SQL Server
Si vous devez mettre à niveau votre version de SQL Server, nous vous recommandons les méthodes suivantes, de la plus simple à la plus complexe.
1. [Mise à niveau de SQL Server sur place](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recommandé).
2. Installez une nouvelle version de SQL Server sur un nouvel ordinateur, puis [utilisez l’option de déplacement de la base de données](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) du programme d’installation de Configuration Manager pour pointer votre serveur de site vers la nouvelle version de SQL Server.
3. Utilisez la [sauvegarde et la récupération](/sccm/protect/understand/backup-and-recovery).

