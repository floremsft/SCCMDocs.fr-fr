---
title: "Mettre à niveau l’infrastructure locale | Microsoft Docs"
description: "Découvrez comment mettre à niveau l’infrastructure, telles que SQL Server et le système d’exploitation de site des systèmes de site."
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8b4c80aa092369ec251757d82a1b4bb2863aa96a
ms.openlocfilehash: f3742dcb930444bab7eb02374fd77ebd0e455734


---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Mettre à niveau l’infrastructure locale qui prend en charge System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations suivantes pour mettre à niveau l’infrastructure qui exécute System Center Configuration Manager.  

##  <a name="a-namebkmksupconfigupgradesitesrva-upgrade-site-operating-system-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Mettre à niveau le système d’exploitation de site des systèmes de site  
 Configuration Manager prend en charge la mise à niveau sur place du système d’exploitation de serveurs qui hébergent un serveur de site et des serveurs distants hébergeant un rôle de système de site, dans les situations suivantes :  

-   Mise à niveau sur place vers un Service Pack Windows Server ultérieur si le niveau du Service Pack de Windows qui en résulte est pris en charge par Configuration Manager.  
-   Mise à niveau sur place à partir de :
    - Windows Server 2012 R2 vers Windows Server 2016 ([afficher des informations supplémentaires](#upgrade-windows-server-2012-r2-to-2016))
    - Windows Server 2012 vers Windows Server 2012 R2 ([afficher des informations supplémentaires](#upgrade-windows-server-2012-to-windows-server-2012-r2))
    - Quand vous utilisez Configuration Manager version 1602 ou version ultérieure, la mise à niveau de Windows Server 2008 R2 vers Windows Server 2012 R2 est également pris en charge ([afficher des informations supplémentaires](#upgrade-windows-server-2008-r2-to-windows-server-2012-r2))

    > [!WARNING]  
    >  Avant de mettre à niveau vers Windows Server 2012 R2, **vous devez désinstaller WSUS 3.2** du serveur.  
    >   
    >  Pour plus d’informations sur cette étape critique, consultez la section Fonctionnalités nouvelles et modifiées de [Vue d’ensemble des services WSUS (Windows Server Update Services)](https://technet.microsoft.com/library/hh852345.aspx) dans la documentation de Windows Server.  

Pour mettre à niveau un serveur, utilisez les procédures de mise à niveau fournies par le système d’exploitation vers lequel vous effectuez la mise à niveau.  Consultez les rubriques suivantes :
  -  [Options de mise à niveau pour Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) dans la documentation de Windows Server.  
  - [Options de mise à niveau et de conversion pour Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths) dans la documentation de Windows Server.

### <a name="upgrade-windows-server-2012-r2-to-2016"></a>Mise à niveau de Windows Server 2012 R2 vers 2016  
Ce scénario de mise à niveau du système d’exploitation a les conditions suivantes :

**Avant la mise à niveau :**  
-   Supprimez le client SCEP (System Center Endpoint Protection). Windows Defender, qui remplace le client SCEP, est intégré à Windows Server 2016. La présence du client SCEP peut empêcher la mise à niveau vers Windows Server 2016.

**Après la mise à niveau :**
-   Vérifiez que Windows Defender est activé, configuré pour démarrer automatiquement et en cours d’exécution.
-   Vérifiez que les services Configuration Manager suivants sont en cours d’exécution :
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Vérifiez que le **service d’activation des processus Windows** et le **service WWW/W3SVC** sont activés, configurés pour démarrer automatiquement et en cours d’exécution pour les rôles de système de site suivants (ces services sont désactivés pendant la mise à niveau) :
  -     Serveur de site
  -     Point de gestion
  -     Point de service Web du catalogue des applications
  -     Point du site web du catalogue des applications


-   Vérifiez que chaque serveur qui héberge un rôle de système de site respecte l’ensemble de la [configuration requise pour les rôles de système de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) qui s’exécutent sur ce serveur. Par exemple, il se peut que vous deviez réinstaller le service BITS ou le service WSUS, ou de configurer des paramètres spécifiques pour IIS.

  Après avoir restauré les composants requis manquants, redémarrez le serveur une fois de plus pour garantir que les services sont démarrés et opérationnels.

**Problème connu lié aux consoles Configuration Manager distantes :**  
Une fois la mise à niveau du serveur de site ou d’un serveur qui héberge une instance de SMS_Provider vers Windows Server 2016 effectuée, il se peut que les utilisateurs administratifs ne puissent pas connecter une console Configuration Manager au site. Pour contourner ce problème, vous devez restaurer manuellement les autorisations pour le groupe Administrateurs SMS dans WMI. Les autorisations doivent être définies sur le serveur de site, ainsi que sur chaque serveur distant qui héberge une instance du fournisseur SMS :

1. Sur les serveurs applicables, ouvrez la console MMC (Microsoft Management Console) et ajoutez le composant logiciel enfichable pour le **Contrôle WMI**, puis sélectionnez **Ordinateur local**.
2. Dans la console MMC, ouvrez les **Propriétés** du **Contrôle WMI (local)**, puis sélectionnez l’onglet **Sécurité**.
3. Développez l’arborescence sous la racine, sélectionnez le nœud **SMS**, puis cliquez sur **Sécurité**.  Vérifiez que le groupe **Administrateurs SMS** dispose des autorisations suivantes :
  -     Activer le compte
  -     Appel à distance autorisé
4. Ensuite, sous l’**onglet Sécurité**, sous le nœud SMS, sélectionnez le nœud **site_&lt;code_de_site>**, puis cliquez sur **Sécurité**. Vérifiez que le groupe **Administrateurs SMS** dispose de l’autorisation suivante :
  -   Méthodes d’exécution
  -   Écriture fournisseur
  -   Activer le compte
  -   Appel à distance autorisé
5. Enregistrez les autorisations pour restaurer l’accès à la console Configuration Manager.

### <a name="windows-server-2012-to-windows-server-2012-r2"></a>Windows Server 2012 vers Windows Server 2012 R2

**Avant la mise à niveau :**
-  Contrairement aux autres scénarios pris en charge, ce scénario ne nécessite pas de considérations supplémentaires avant la mise à niveau.

**Après la mise à niveau :**
  - Vérifiez que le service de déploiement Windows est démarré et en cours d’exécution pour les rôles de système de site suivants (ce service est arrêté pendant la mise à niveau) :
    - Serveur de site
    - Point de gestion
    - Point de service Web du catalogue des applications
    - Point du site web du catalogue des applications


  -     Vérifiez que le **service d’activation des processus Windows** et le **service WWW/W3SVC** sont activés, configurés pour démarrer automatiquement et en cours d’exécution pour les rôles de système de site suivants (ces services sont désactivés pendant la mise à niveau) :
    -   Serveur de site
    -   Point de gestion
    -   Point de service Web du catalogue des applications
    -   Point du site web du catalogue des applications


  -     Vérifiez que chaque serveur qui héberge un rôle de système de site respecte l’ensemble de la [configuration requise pour les rôles de système de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) qui s’exécutent sur ce serveur. Par exemple, il se peut que vous deviez réinstaller le service BITS ou le service WSUS, ou de configurer des paramètres spécifiques pour IIS.

  Après avoir restauré les composants requis manquants, redémarrez le serveur une fois de plus pour garantir que les services sont démarrés et opérationnels.

### <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Mise à niveau de Windows Server 2008 R2 vers Windows Server 2012 R2
Ce scénario de mise à niveau du système d’exploitation a les conditions suivantes :  

**Avant la mise à niveau :**
-   Désinstallez WSUS 3.2.  
    Avant de mettre à niveau le système d’exploitation d’un serveur vers Windows Server 2012 R2, vous devez désinstaller WSUS 3.2 du serveur. Pour plus d’informations sur cette étape critique, consultez la section Fonctionnalités nouvelles et modifiées de la rubrique Vue d’ensemble des services WSUS (Windows Server Update Services) dans la documentation de Windows Server.

**Après la mise à niveau :**
  - Vérifiez que le service de déploiement Windows est démarré et en cours d’exécution pour les rôles de système de site suivants (ce service est arrêté pendant la mise à niveau) :
    - Serveur de site
    - Point de gestion
    - Point de service Web du catalogue des applications
    - Point du site web du catalogue des applications


  -     Vérifiez que le **service d’activation des processus Windows** et le **service WWW/W3SVC** sont activés, configurés pour démarrer automatiquement et en cours d’exécution pour les rôles de système de site suivants (ces services sont désactivés pendant la mise à niveau) :
    -   Serveur de site
    -   Point de gestion
    -   Point de service Web du catalogue des applications
    -   Point du site web du catalogue des applications


  -     Vérifiez que chaque serveur qui héberge un rôle de système de site respecte l’ensemble de la [configuration requise pour les rôles de système de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) qui s’exécutent sur ce serveur. Par exemple, il se peut que vous deviez réinstaller le service BITS ou le service WSUS, ou de configurer des paramètres spécifiques pour IIS.

  Après avoir restauré les composants requis manquants, redémarrez le serveur une fois de plus pour garantir que les services sont démarrés et opérationnels.


### <a name="unsupported-upgrade-scenarios"></a>Scénarios de mise à niveau non pris en charge
Les scénarios de mise à niveau de Windows Server suivants font souvent l’objet de questions, mais ils ne sont pas pris en charge par Configuration Manager :  

-   Windows Server 2008 vers Windows Server 2012 ou version ultérieure  
-   Windows Server 2008 R2 vers Windows Server 2012



##  <a name="a-namebkmksupconfigupgradeclienta-upgrade-the-operating-system-of-configuration-manager-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Mettre à niveau le système d’exploitation de clients Configuration Manager  
 Configuration Manager prend en charge une mise à niveau sur place du système d’exploitation pour les clients Configuration Manager dans les situations suivantes :  

-   La mise à niveau sur place vers un Service Pack Windows ultérieur si le niveau du Service Pack qui en résulte est pris en charge par Configuration Manager.  

-   Mise à niveau sur place de Windows à partir d’une version prise en charge vers Windows 10. Pour plus d’informations, consultez [Mettre à niveau Windows vers la dernière version avec System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Mises à niveau de la maintenance de build à build de Windows 10.  Pour plus d’informations, consultez [Gérer Windows as a Service (WaaS) à l’aide de System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

##  <a name="a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> Mettre à niveau SQL Server sur le serveur de base de données de site  
  Configuration Manager prend en charge une mise à niveau sur place de SQL Server à partir d’une version prise en charge de SQL sur le serveur de base de données de site. Vous trouverez ci-après des détails sur les scénarios de mise à niveau de SQL Server pris en charge par Configuration Manager et la configuration requise pour chaque scénario.

 Pour plus d’informations sur les versions de SQL Server prises en charge par Configuration Manager, consultez [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 **Mettre à niveau la version du Service Pack de SQL Server**    
 Configuration Manager prend en charge la mise à niveau sur place de SQL Server vers un Service Pack ultérieur si le niveau du Service Pack SQL Server qui en résulte est pris en charge par Configuration Manager.

 Quand une hiérarchie comprend plusieurs sites Configuration Manager, chaque site peut exécuter une version différente du Service Pack de SQL Server, et il n’existe pas de limitation quant à l’ordre dans lequel les sites mettent à niveau la version du Service Pack de SQL Server qui est utilisé pour la base de données du site.

 **Mise à niveau vers une nouvelle version de SQL Server :**   
 Configuration Manager prend en charge la mise à niveau sur place de SQL Server vers les versions suivantes :

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

Quand vous mettez à niveau la version de SQL Server qui héberge la base de données du site, vous devez mettre à niveau la version de SQL Server qui est utilisée sur les sites dans l’ordre suivant :

 1. Mettez d'abord à niveau SQL Server sur le site administration centrale.
 2. Mettez à niveau les sites secondaires avant de mettre à niveau le site principal parent d’un site secondaire.
 3. Mettez à niveau les sites principaux parents en dernier. Ceci inclut les sites principaux enfants qui dépendent d'un site d'administration centrale et les sites principaux autonomes qui constituent les sites de plus haut niveau d'une hiérarchie.

**Niveau Estimation de cardinalité SQL Server et base de données de site :**   
Quand une base de données de site est mise à niveau à partir d’une version antérieure de SQL Server, la base de données conserve son niveau Estimation de cardinalité SQL Server (SQL Server CE) existant s’il est au minimum autorisé pour cette instance de SQL Server. En mettant à niveau SQL Server avec une base de données à un niveau de compatibilité inférieur que celui autorisé automatiquement, vous définissez la base de données sur le niveau de compatibilité le plus bas autorisé par SQL.

Le tableau suivant identifie les niveaux de compatibilité recommandés pour les bases de données de site Configuration Manager :

|Version SQL Server | Niveaux de compatibilité pris en charge |Niveau conseillé|
|----------------|--------------------|--------|
| SQL Server 2016| 130, 120, 110, 100 | 130|
| SQL Server 2014| 120, 110, 100      | 110|

Pour identifier le niveau de compatibilité SQL Server CE en cours d’utilisation pour votre base de données de site, exécutez la requête SQL suivante sur le serveur de base de données de site : **SELECT name, compatibility_level FROM sys.databases**

 Pour plus d’informations sur les niveaux de compatibilité SQL CE et comment les définir, consultez [Niveau de compatibilité ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx).


**Pour plus d’informations sur SQL Server, consultez la documentation de SQL Server sur TechNet :**  
-   [Mise à niveau vers SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [Mise à niveau vers SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [Mise à niveau vers SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Pour mettre à niveau SQL Server sur le serveur de base de données de site  

1.  Arrêtez tous les services de Configuration Manager sur le site.  
2.  Mettez à niveau SQL Server vers une version prise en charge.  
3.  Redémarrez les services de Configuration Manager.  

> [!NOTE]  
>  Quand vous changez l'édition de SQL Server utilisée sur le site d'administration centrale d'une édition Standard en une édition Enterprise ou Datacenter, la partition de base de données qui limite le nombre de clients que la hiérarchie prend en charge ne change pas.



<!--HONumber=Dec16_HO3-->


