---
title: SQL Server AlwaysOn | Microsoft Docs
ms.custom: na
ms.date: 1/4/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: aaaab003ddd22f18160d4be63cfeab3a7e7f6b03
ms.lasthandoff: 03/27/2017


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>SQL Server AlwaysOn pour une base de données de site à haut niveau de disponibilité pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 À partir de System Center Configuration Manager version 1602, vous pouvez utiliser des [groupes de disponibilité AlwaysOn](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx) SQL Server pour héberger la base de données du site sur les sites principaux, et le site d’administration centrale en tant que solution de récupération d’urgence à haute disponibilité. Le groupe de disponibilité peut être hébergé localement ou dans Microsoft Azure.  

 Quand vous utilisez Microsoft Azure pour héberger le groupe de disponibilité, vous pouvez encore augmenter la disponibilité de la base de données de votre site en utilisant des groupes de disponibilité AlwaysOn SQL Server avec des groupes à haute disponibilité Azure. Pour plus d’informations sur les groupes à haute disponibilité Azure, consultez [Gestion de la disponibilité des machines virtuelles](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).  

 Configuration Manager prend en charge l’hébergement de la base de données de site sur un groupe de disponibilité SQL qui se trouve derrière un équilibreur de charge interne ou externe. En plus de configurer des exceptions de pare-feu sur chaque réplica, vous devez ajouter des règles d’équilibrage de charge pour les ports suivants :
  - SQL sur TCP : TCP 1433
  - SQL Server Service Broker : TCP 4022
  - Server Message Block (SMB) : TCP 445
  - Mappeur de point de terminaison RPC : TCP 135


Voici des scénarios pris en charge avec les groupes de disponibilité :  

-   Vous pouvez déplacer votre base de données de site vers l’instance par défaut d’un groupe de disponibilité  

-   Vous pouvez ajouter ou supprimer des membres réplicas dans un groupe de disponibilité qui héberge une base de données de site  

-   Vous pouvez déplacer votre base de données de site à partir d’un groupe de disponibilité vers une instance par défaut ou nommée d’un serveur SQL Server autonome  

> [!Important]  
> Lorsque vous utilisez Microsoft Intune avec Configuration Manager dans une configuration hybride, le déplacement de la base de données de site vers ou depuis un groupe de disponibilité déclenche une resynchronisation des données avec le cloud. Cette opération est inévitable. 



> [!NOTE]  
>  Pour pouvoir configurer et utiliser des groupes de disponibilité, vous devez savoir comment configurer SQL Server et les groupes de disponibilité SQL Server. Les procédures relatives à System Center Configuration Manager décrites dans cette rubrique s’appuient sur une documentation et des procédures supplémentaires figurant dans la bibliothèque de documentation SQL Server.  

 **Problèmes connus liés à l’utilisation de groupes de disponibilité AlwaysOn avec Configuration Manager :**  

-   **Tous les serveurs de réplication doivent avoir un chemin de fichier identique au moment où vous paramétrez Configuration Manager pour utiliser le groupe de disponibilité :**  

    -   Quand vous exécutez le programme d’installation de Configuration Manager pour rediriger le site afin d’utiliser la base de données dans un groupe de disponibilité, chaque serveur réplica secondaire de ce groupe doit avoir un chemin de fichier identique à celui utilisé pour héberger les fichiers de base de données du site sur le réplica principal actuel. À défaut de chemin identique sur les réplicas secondaires, le programme d’installation ne peut pas ajouter l’instance de groupes de disponibilité comme nouvel emplacement de la base de données du site.  

         En outre, sur chaque serveur de réplication secondaire, le compte de service SQL Server local doit avoir une autorisation **Contrôle total** sur ce dossier.  

         Les serveurs de réplication secondaires doivent avoir ce chemin de fichier uniquement pendant que vous utilisez le programme d’installation pour spécifier l’instance de base de données dans le groupe de disponibilité.  Une fois que le programme d’installation a apporté la modification permettant d’utiliser la base de données du site dans le groupe de disponibilité, vous pouvez supprimer le chemin inutilisé des serveurs de réplication secondaires.  

         Par exemple, examinez le scénario suivant :  

        -   Vous créez un groupe de disponibilité qui utilise trois serveurs SQL Server  

        -   Votre serveur de réplication principal est une nouvelle installation de SQL Server 2014.  Par défaut, les fichiers .MDF et .LDF de la base de données sont stockés dans C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA  

        -   Vos deux serveurs de réplication secondaires ont été mis à niveau vers SQL Server 2014 à partir de versions antérieures et conservent le chemin de fichier d’origine pour stocker les fichiers de base de données, à savoir C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA  

        -   Avant de tenter de déplacer la base de données du site vers ce groupe de disponibilité, sur chaque serveur de réplication secondaire, vous devez créer le prochain chemin de fichier, même si les réplicas secondaires n’utilisent pas cet emplacement de fichier, à savoir  C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (il s’agit du même chemin que celui en cours d’utilisation sur le réplica principal)  

        -   Vous accordez ensuite au compte de service SQL Server sur chaque réplica secondaire un accès en contrôle total à l’emplacement du fichier qui vient d’être créé sur ce serveur  

        -   Vous pouvez désormais exécuter correctement le programme d’installation de Configuration Manager pour indiquer au site d’utiliser la base de données du site figurant dans le groupe de disponibilité  

-   **Quand le programme d’installation s’exécute pour indiquer à la base de données du site d’utiliser le groupe de disponibilité, des erreurs similaires à la suivante peuvent être consignées dans ConfigMgrSetup.log :**  

    -   ERREUR : erreur SQL Server : [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Échec de la mise à jour de la base de données « CM_AAA », car celle-ci est en lecture seule.   Installation de Configuration Manager 21/1/2016 16:54:59 7344 (0x1CB0)  

     Ces erreurs sont journalisées quand le programme d’installation tente de traiter des rôles de base de données sur des réplicas secondaires du groupe de disponibilité. Vous pouvez ignorer ces erreurs sans risque.
- **Serveurs SQL qui hébergent des groupes de disponibilité supplémentaires :**

  Avant d’installer la version 1610, quand vous utilisez un groupe de disponibilité, et que vous exécutez ensuite le programme d’installation de Configuration Manager ou que vous installez une mise à jour pour Configuration Manager, chaque réplica de chaque groupe de disponibilité supplémentaire sur le serveur SQL Server hébergeant le groupe de disponibilité Configuration Manager doit disposer des configurations suivantes :
    - **basculement manuel**
    - **autoriser toute connexion en lecture seule**


##  <a name="bkmk_BnR"></a> Modifications de la sauvegarde et de la récupération lorsque vous utilisez un groupe de disponibilité AlwaysOn SQL Server  
 **Sauvegarde :**  

 Quand une base de données du site s’exécute dans un groupe de disponibilité, vous devez continuer à exécuter la tâche intégrée de maintenance de serveur **Sauvegarder le site** pour sauvegarder les paramètres et fichiers Configuration Manager courants. Toutefois, évitez d’utiliser les fichiers .MDF ou .LDF créés par cette sauvegarde. Au lieu de cela, envisagez d’effectuer des sauvegardes directes de la base de données du site à l’aide de SQL Server.  

 De plus, étant donné que le mode de récupération de la base de données a trait à une récupération complète, vous devez planifier d’analyser et de gérer la taille du journal des transactions de base de données du site.  Dans le mode de récupération complète, les transactions ne sont pas renforcées tant qu’une sauvegarde complète de la base de données ou du journal des transactions n’a pas été effectuée. Le mode de récupération complète est une exigence liée à l’utilisation de la base de données du site dans un groupe de disponibilité. Il est défini quand vous configurez le groupe pour être utilisé avec Configuration Manager. Pour plus d’informations sur la sauvegarde et la restauration de SQL Server, consultez [Sauvegarde et restauration des bases de données SQL Server](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) dans la documentation de SQL Server.  

 **Récupération :**  

 Durant la récupération d’un site, aussi longtemps qu’un nœud du groupe de disponibilité reste fonctionnel, vous pouvez utiliser l’option de récupération de site **Ignorer la récupération de base de données (Utiliser cette option si la base de données de site n’était pas affectée)**.  

 Toutefois, si tous les nœuds d’un groupe de disponibilité ont été perdus, avant de pouvoir récupérer le site, vous devez recréer le groupe de disponibilité (System Center Configuration Manager ne peut pas régénérer, ni restaurer le nœud de disponibilité.)  Une fois le groupe recréé avec une sauvegarde restaurée et reconfigurée, vous pouvez utiliser l’option de récupération de site **Ignorer la récupération de base de données (Utiliser cette option si la base de données de site n’était pas affectée)**.  

 Pour plus d’informations sur la sauvegarde et la récupération, consultez [Sauvegarde et récupération pour System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

##  <a name="bkmk_create"></a> Configuration d’un groupe de disponibilité pour une utilisation avec Configuration Manager  
 Avant de débuter la procédure suivante, prenez connaissance des procédures SQL Server nécessaires pour effectuer cette configuration, ainsi que des détails suivants applicables aux groupes de disponibilité que vous configurez pour une utilisation avec Configuration Manager.  

 **Configuration requise pour les groupes de disponibilité AlwaysOn utilisés avec System Center Configuration Manager :**  

-  *Version* : Chaque nœud (ou réplica) du groupe de disponibilité doit exécuter une version de SQL Server prise en charge par System Center Configuration Manager. Si elle sont prises en charge par SQL Server, les différents nœuds du groupe de disponibilité peuvent exécuter des versions différentes de SQL Server.   

- *Édition* : Vous devez utiliser une édition Enterprise de SQL Server.  L’édition Standard de SQL Server 2016 introduit les groupes de disponibilité de base, qui ne sont pas pris en charge par Configuration Manager.


-   Le groupe de disponibilité doit avoir un réplica principal et peut avoir jusqu’à deux réplicas secondaires synchrones.  

-  Après avoir ajouté une base de données à un groupe de disponibilité, vous devez basculer le réplica principal vers un réplica secondaire (ce qui fait de celui-ci le nouveau réplica principal), puis configurer la base de données avec les éléments suivants :
    - Activer la propriété Trustworthy : True
    - Activer Service Broker : True
    - Valeur de dbowner : SA

    Vous pouvez exécuter le script suivant pour configurer ces paramètres, où cm_ABC est le nom de votre base de données de site :  

    >     USE master  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', 2147483647 reconfigure



-   Le groupe de disponibilité doit avoir au moins un **écouteur de groupe de disponibilité**.  Le nom virtuel de cet écouteur est utilisé quand vous configurez Configuration Manager pour utiliser la base de données du site dans le groupe de disponibilité. Bien qu’un groupe de disponibilité puisse contenir plusieurs écouteurs, Configuration Manager ne peut en utiliser qu’un seul  

-   Chaque réplica principal et secondaire doit :  
    - être configuré pour **autoriser toute connexion en lecture seule**;
    - utiliser **l’instance par défaut**;
    - être configuré pour le **basculement manuel**.  

        > [!TIP]  
        >  System Center Configuration Manager prend en charge l’utilisation de réplicas de groupe de disponibilité quand il est configuré pour le basculement automatique. Toutefois, un basculement manuel doit être défini quand vous exécutez le programme d’installation pour spécifier l’utilisation de la base de données du site dans le groupe de disponibilité, ainsi qu’au moment où vous installez des mises à jour de Configuration Manager (et pas seulement des mises à jour qui s’appliquent à la base de données du site).  

  **Restrictions pour les groupes de disponibilité**
   - Les groupes de disponibilité de base (introduits avec l’édition Standard de SQL Server 2016) ne sont pas pris en charge. La raison en est que les groupes de disponibilité de base ne prennent pas en charge les accès en lecture aux réplicas secondaires, ce qui est obligatoire pour une utilisation avec Configuration Manager. Pour plus d’informations, consultez [Groupes de disponibilité de base (Groupes de disponibilité AlwaysOn)](https://msdn.microsoft.com/en-us/library/mt614935.aspx).

   - Les groupes de disponibilité sont pris en charge uniquement pour la base de données du site, mais pas pour la base de données de mises à jour logicielles ni pour la base de données de création de rapports.   
   - Quand vous utilisez un groupe de disponibilité, vous devez configurer manuellement votre point de rapport pour utiliser le réplica principal actuel et pas l’écouteur de groupe de disponibilité. Si le réplica principal bascule sur un autre réplica, vous devez ensuite reconfigurer le point de rapport pour utiliser le nouveau réplica principal.  
   - Avant d’installer les mises à jour, telles que la version 1606, vérifiez que le groupe de disponibilité est défini pour un basculement manuel. Une fois le site mis à jour, vous pouvez restaurer le basculement automatique.



 **Autorisations requises pour configurer et utiliser des groupes de disponibilité :**  

-   Le compte d’ordinateur du serveur de site doit être membre du groupe **Administrateurs locaux** sur chaque ordinateur membre du groupe de disponibilité.  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>Pour configurer un groupe de disponibilité pour héberger une base de données de site  

1.  Utilisez la commande suivante pour arrêter le site Configuration Manager :  
     **Preinst.exe /stopsite**  

     Pour plus d’informations sur l’utilisation de Preinst.exe, consultez [Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Remplacez le mode de sauvegarde **SIMPLE** de la base de données du site par **COMPLÈTE**.  

     Consultez [Afficher ou modifier le mode de récupération d’une base de données (SQL Server)](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) dans la documentation de SQL Server. (Les groupes de disponibilité prennent en charge uniquement le mode de récupération COMPLÈTE).  

3.  Sur le serveur qui hébergera le réplica principal du groupe, utilisez **l’Assistant Nouveau groupe de disponibilité** pour créer le groupe de disponibilité. Dans l’Assistant :  

    -   Dans la page **Sélectionner une base de données**, sélectionnez la base de données pour votre site Configuration Manager  

    -   Dans la page **Spécifier les réplicas** , configurez ce qui suit :  

        -   **Réplicas**: spécifiez les serveurs qui hébergeront les réplicas secondaires  

        -   **Écouteur** : spécifiez le **nom d’écouteur DNS** en tant que nom DNS complet, par exemple **&lt;Serveur_écouteur>.fabrikam.com**. Ce nom est utilisé quand vous configurez Configuration Manager pour utiliser la base de données située dans le groupe de disponibilité.

    -   Dans la page **Sélectionner la synchronisation de données initiale** , sélectionnez **Complète**. Après avoir créé le groupe de disponibilité, l’Assistant sauvegarde la base de données primaire et le journal des transactions, puis les restaure sur chaque serveur hébergeant un réplica secondaire. Si vous ne suivez pas cette étape, vous devez restaurer une copie de la base de données du site sur chaque serveur hébergeant un réplica secondaire, et joindre manuellement cette base de données au groupe.  

    Pour plus d’informations, consultez [Utiliser l’Assistant Groupe de disponibilité (SQL Server Management Studio)](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) dans la documentation de SQL Server.  

4.  Une fois le groupe de disponibilité configuré, configurez la base de données du site sur le réplica principal avec la propriété **TRUSTWORTHY** , puis **activez l’intégration du CLR**. Pour plus d’informations sur la façon d’effectuer ces configurations, consultez [Propriété de base de données TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) et  [Activation de l’intégration du CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) dans la documentation de SQL Server.  

5.  Pour configurer chaque réplica secondaire dans le groupe de disponibilité, procédez comme suit :  

    1.  Basculez manuellement le réplica principal actuel vers un réplica secondaire. Consultez [Effectuer un basculement manuel planifié d’un groupe de disponibilité (SQL Server)](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) dans la documentation de SQL Server.  

    2.  Configurez la base de données sur le nouveau réplica principal avec la propriété **TRUSTWORTHY** , puis **activez l’intégration du CLR**.  

6.  Une fois tous les réplicas promus en réplicas principaux et les bases de données configurées, le groupe de disponibilité est prêt à être utilisé avec Configuration Manager.  





##  <a name="bkmk_direct"></a> Déplacer une base de données de site vers un groupe de disponibilité  
 Vous pouvez déplacer une base de données pour un site précédemment installé vers un groupe de disponibilité. Vous devez tout d’abord créer le groupe de disponibilité, puis configurer la base de données pour fonctionner dans le groupe de disponibilité.  

 Pour effectuer cette procédure, le compte d’utilisateur exécutant le programme d’installation de Configuration Manager doit être membre du groupe **Administrateurs locaux** sur chaque ordinateur membre du groupe de disponibilité.  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>Pour déplacer une base de données de site vers un groupe de disponibilité  

1.  Exécutez le **programme d’installation de Configuration Manager** à partir du **&lt;dossier d’installation du site Configuration Manager\>\BIN\X64\setup.exe**.  

2.  Sur la page **Mise en route** , sélectionnez **Effectuer une maintenance de site ou réinitialiser ce site**, puis cliquez sur **Suivant**.  

3.  Sélectionnez l’option **Modifier la configuration de SQL Server** , puis cliquez sur **Suivant**.  

4.  Reconfigurez ce qui suit pour la base de données du site :  

    -   **Nom du serveur SQL Server :** entrez le nom virtuel de l’écouteur de groupe de disponibilité que vous avez configuré lors de la création du groupe de disponibilité. Le nom virtuel doit être un nom DNS complet, par exemple **&lt;serveur_point_de_terminaison\>.fabrikam.com**  

    -   **Instance :** cette valeur doit être vide pour spécifier l’instance par défaut pour l’écouteur du groupe de disponibilité.  Si la base de données du site actuel est installée sur une instance nommée, celle-ci est répertoriée et doit être désactivée.  

    -   **Base de données :** laissez le nom tel qu’il s’affiche. Il s’agit du nom de la base de données du site actuel.  

5.  Après avoir fourni les informations relatives au nouvel emplacement de la base de données, exécutez le programme d’installation avec vos processus et configurations normaux.  

##  <a name="bkmk_change"></a> Ajout ou suppression de membres d’un groupe de disponibilité actif  
 Une fois que Configuration Manager utilise une base de données de site hébergée dans un groupe de disponibilité, vous pouvez supprimer ou ajouter un membre réplica (sans dépasser un nœud principal et deux nœuds secondaires).  

#### <a name="to-add-a-new-replica-member"></a>Pour ajouter un nouveau membre réplica  

1.  Ajoutez le nouveau serveur en tant que réplica secondaire au groupe de disponibilité. Consultez  [Ajouter un réplica secondaire à un groupe de disponibilité (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)dans la bibliothèque de documentation de SQL Server.  

2.  Arrêtez le site Configuration Manager en exécutant **Preinst.exe /stopsite**. Consultez [Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

3.  Configurez chaque réplica secondaire. Pour chaque réplica secondaire dans le groupe de disponibilité, effectuez les opérations suivantes :  

    1.  Basculez manuellement le réplica principal vers le nouveau réplica secondaire. Consultez [Effectuer un basculement manuel planifié d’un groupe de disponibilité (SQL Server)](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) dans la documentation de SQL Server.  

    2.  Configurez la base de données sur le nouveau serveur sur Digne de confiance, puis activez l’intégration du CLR. Consultez [Propriété de base de données TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) et  [Activation de l’intégration du CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)dans la documentation de SQL Server.  

4.  Redémarrez le site en démarrant le Gestionnaire de composant de site (**sitecomp**) et les services **SMS_Executive** .  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>Pour supprimer un membre réplica du groupe de disponibilité  

-   Utilisez les informations de [Supprimer un réplica secondaire d’un groupe de disponibilité (SQL Server)](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) dans la documentation de SQL Server.  

##  <a name="bkmk_remove"></a> Replacement de la base de données du site à partir d’un groupe de disponibilité dans une instance SQL Server unique  
 Lorsque vous ne souhaitez plus héberger la base de données de votre site dans un groupe de disponibilité, procédez comme suit.  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Pour replacer la base de données du site à partir d’un groupe de disponibilité dans une instance SQL Server unique  

1.  Arrêtez le site Configuration Manager à l’aide de la commande suivante :  
     **Preinst.exe /stopsite**.  Pour plus d’informations, consultez [Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Utilisez SQL Server pour créer une sauvegarde complète de la base de données de votre site à partir du réplica principal. Pour plus d’informations sur la façon de procéder, consultez [Créer une sauvegarde complète de base de données (SQL Server)](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) dans la documentation de SQL Server.  

3.  Si le serveur hébergeant le réplica principal pour le groupe de disponibilité n’hébergea l’instance unique de la base de données du site, vous pouvez ignorer cette étape :  

    -   Utilisez SQL Server pour restaurer la sauvegarde de la base de données du site sur le serveur qui hébergera la base de données du site.  Consultez [Restaurer une sauvegarde de base de données (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) dans la documentation de SQL Server.  

4.  Sur la base de données de site restaurée, remplacez le mode de sauvegarde **COMPLÈTE** de la base de données du site par **SIMPLE**.  Consultez [Afficher ou modifier le mode de récupération d’une base de données (SQL Server)](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) dans la documentation de SQL Server.  

5.  Exécutez le **programme d’installation de Configuration Manager** à partir du **&lt;dossier d’installation du site Configuration Manager\>\BIN\X64\setup.exe**.  

6.  Sur la page **Mise en route** , sélectionnez **Effectuer une maintenance de site ou réinitialiser ce site**, puis cliquez sur **Suivant**.  

7.  Sélectionnez l’option **Modifier la configuration de SQL Server** , puis cliquez sur **Suivant**.  

8.  Reconfigurez ce qui suit pour la base de données du site :  

    -   **Nom du serveur SQL Server :** entrez le nom du serveur hébergeant actuellement la base de données du site.  

    -   **Instance :** spécifiez l’instance nommée hébergeant la base de données du site, ou laissez ce champ vide si la base de données se trouve sur l’instance par défaut.  

    -   **Base de données :** laissez le nom tel qu’il s’affiche. Il s’agit du nom de la base de données du site actuel.  

9. Après avoir fourni les informations relatives au nouvel emplacement de la base de données, exécutez le programme d’installation avec vos processus et configurations normaux. Une fois l’exécution du programme d’installation terminée, le site redémarre et commence à utiliser le nouvel emplacement de la base de données.  

10. Pour nettoyer les serveurs qui étaient membres du groupe de disponibilité, suivez les instructions de [Supprimer un groupe de disponibilité (SQL Server)](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) dans la documentation de SQL Server.

