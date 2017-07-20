---
title: "Configurer des groupes de disponibilité | Microsoft Docs"
description: "Configurez et gérez des groupes de disponibilité SQL Server Always On avec SCCM."
ms.custom: na
ms.date: 5/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 138834b6cc64332202256961ad1d2f5ab6d176db
ms.contentlocale: fr-fr
ms.lasthandoff: 06/01/2017


---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configurer des groupes de disponibilité SQL Server Always On pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations de cette rubrique pour configurer et gérer des groupes de disponibilité avec Configuration Manager.

Avant de commencer :  
-   Familiarisez-vous avec les informations de la rubrique [Se préparer à l’utilisation de groupes de disponibilité SQL Server Always On avec Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).
-   Familiarisez-vous avec la documentation de SQL Server qui traite de l’utilisation des groupes de disponibilité et des procédures nécessaires pour exécuter les scénarios suivants.

> [!TIP]  
>  Les liens de cette rubrique pour SQL Server pointent vers le contenu pour SQL Server 2016. Si vous n’utilisez pas cette version de SQL Server, consultez la documentation de votre version.

## <a name="create-and-configure-an-availability-group"></a>Créer et configurer un groupe de disponibilité
Utilisez la procédure suivante pour créer un groupe de disponibilité, puis déplacez une copie de la base de données de site vers ce groupe de disponibilité.

Pour effectuer cette procédure, le compte que vous utilisez doit être :
-   membre du groupe **Administrateurs locaux** sur chaque ordinateur qui figurera dans le groupe de disponibilité.
-   **sysadmin** sur chaque instance SQL Server qui hébergera la base de données du site.

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>Pour créer et configurer un groupe de disponibilité pour Configuration Manager  
1.    Utilisez la commande suivante pour arrêter le site Configuration Manager : **Preinst.exe /stopsite**. Pour plus d'informations sur l’utilisation de PreInst.exe, consultez [Utilitaire Maintenance de la hiérarchie](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.    Remplacez le mode de sauvegarde **SIMPLE** de la base de données du site par **COMPLÈTE**.
Consultez [Afficher ou modifier le mode de récupération d’une base de données (SQL Server)](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) dans la documentation de SQL Server. (Les groupes de disponibilité prennent en charge uniquement le mode de récupération COMPLÈTE).

3.    Utilisez SQL Server pour créer une sauvegarde complète de votre base de données de site, puis effectuez l’une des opérations suivantes, selon que le serveur qui héberge votre base de données de site sera ou non un membre réplica du nouveau groupe de disponibilité :
    -   **Sera membre de votre groupe de disponibilité :**  
        Si vous utilisez ce serveur en tant que membre réplica principal initial du groupe de disponibilité, il est inutile de restaurer une copie de la base de données de site sur ce serveur ou sur un autre serveur du groupe. La base de données sera déjà en place sur le réplica principal, et SQL Server répliquera la base de données sur les réplicas secondaires à une étape ultérieure.  

      -    **Ne sera pas membre du groupe de disponibilité :**   
    Vous devez restaurer une copie de la base de données de site sur le serveur qui hébergera le réplica principal du groupe.

    Pour plus d’informations sur la façon de procéder, consultez [Créer une sauvegarde complète de base de données](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) et [Restaurer une sauvegarde de base de données à l’aide de SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) dans la documentation de SQL Server.

4.    Sur le serveur qui hébergera le réplica principal initial du groupe, utilisez [l’Assistant Nouveau groupe de disponibilité](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) pour créer le groupe de disponibilité. Dans l’Assistant :
      -    Dans la page **Sélectionner une base de données**, sélectionnez la base de données pour votre site Configuration Manager.  

      -    Dans la page **Spécifier les réplicas** , configurez ce qui suit :
          -    **Réplicas :** spécifiez les serveurs qui hébergeront les réplicas secondaires.

          -    **Écouteur :** spécifiez le **nom d’écouteur DNS** en tant que nom DNS complet, par exemple **&lt;Serveur_écouteur>.fabrikam.com**. Ce nom est utilisé quand vous configurez Configuration Manager pour utiliser la base de données située dans le groupe de disponibilité.

      -    Dans la page **Sélectionner la synchronisation de données initiale** , sélectionnez **Complète**. Après avoir créé le groupe de disponibilité, l’Assistant sauvegarde la base de données primaire et le journal des transactions, puis les restaure sur chaque serveur hébergeant un réplica secondaire. (Si vous ne suivez pas cette étape, vous devez restaurer une copie de la base de données du site sur chaque serveur hébergeant un réplica secondaire, et joindre manuellement cette base de données au groupe.)   

5.    Vérifiez la configuration sur chaque réplica :   
  1.    Vérifiez que le compte d’ordinateur du serveur de site est un membre du groupe **Administrateurs locaux** sur chaque ordinateur membre du groupe de disponibilité.  

  2.  Exécutez le [script de vérification](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) indiqué dans la configuration requise pour confirmer que la base de données de site est correctement configurée sur chaque réplica.

  3.    S’il est nécessaire de définir des configurations sur les réplicas secondaires, vous devez basculer manuellement le réplica principal vers le réplica secondaire avant de continuer car vous ne pouvez pas configurer la base de données d’un réplica principal. Pour plus d’informations, consultez [Effectuer un basculement manuel planifié d’un groupe de disponibilité (SQL Server)](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) dans la documentation de SQL Server.

6.    Une fois que tous les réplicas répondent aux conditions requises, le groupe de disponibilité est prêt à être utilisé avec le Configuration Manager.

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>Configurer un site pour utiliser la base de données dans le groupe de disponibilité
Après avoir [créé et configuré le groupe de disponibilité](#create-and-configure-an-availability-group), utilisez la maintenance de site Configuration Manager pour configurer le site afin d’utiliser la base de données hébergée par le groupe de disponibilité.

L’installation d’un nouveau site avec sa base de données dans un groupe de disponibilité n’est pas prise en charge. Par exemple, si vous utilisez le support 1702 de référence, vous devez installer le site à l’aide d’une seule instance SQL Server. Une fois le site installé, vous pouvez déplacer la base de données de site vers le groupe de disponibilité.

Pour effectuer cette procédure, le compte que vous utilisez pour exécuter le programme d’installation Configuration Manager doit être :
-   membre du groupe **Administrateurs locaux** sur chaque ordinateur membre du groupe de disponibilité.
-   **sysadmin** sur chaque instance SQL Server qui héberge la base de données du site.

> [!IMPORTANT]
> Lorsque vous utilisez Microsoft Intune avec Configuration Manager dans une configuration hybride, le déplacement de la base de données de site vers ou depuis un groupe de disponibilité déclenche une resynchronisation des données avec le cloud. Cette opération est inévitable.

### <a name="to-configure-a-site-to-use-the-availability-group"></a>Pour configurer un site afin d’utiliser le groupe de disponibilité
1.    Exécutez le **programme d’installation de Configuration Manager** à partir du **&lt;*dossier d’installation du site Configuration Manager*>\BIN\X64\setup.exe**.

2.    Sur la page **Mise en route** , sélectionnez **Effectuer une maintenance de site ou réinitialiser ce site**, puis cliquez sur **Suivant**.

3.    Sélectionnez l’option **Modifier la configuration de SQL Server** , puis cliquez sur **Suivant**.

4.    Reconfigurez ce qui suit pour la base de données du site :
    -   **Nom du serveur SQL Server :** entrez le nom virtuel de l’**écouteur** de groupe de disponibilité que vous avez configuré lors de la création du groupe de disponibilité. Le nom virtuel doit être un nom DNS complet, par exemple **&lt;*endpointServer*>.fabrikam.com**.  

    -   **Instance :** cette valeur doit être vide pour spécifier l’instance par défaut pour l’*écouteur* du groupe de disponibilité. Si la base de données du site actuel est installée sur une instance nommée, celle-ci est répertoriée et doit être désactivée.

    -   **Base de données :** laissez le nom tel qu’il s’affiche. Il s’agit du nom de la base de données du site actuel.

5.    Après avoir fourni les informations relatives au nouvel emplacement de la base de données, exécutez le programme d’installation avec vos processus et configurations normaux.



## <a name="add-and-remove-replica-members"></a>Ajouter et supprimer des membres réplicas  
Si votre base de données de site est hébergée dans un groupe de disponibilité, utilisez les procédures suivantes pour ajouter ou supprimer des membres réplicas. Configuration Manager prend en charge un seul nœud principal et jusqu'à deux nœuds secondaires.

Pour effectuer les procédures suivante, le compte doit que vous utilisez doit être :
-   membre du groupe **Administrateurs locaux** sur chaque ordinateur membre du groupe de disponibilité.
-   **sysadmin** sur chaque instance SQL Server qui héberge ou hébergera la base de données du site.


### <a name="to-add-a-new-replica-member"></a>Pour ajouter un nouveau membre réplica
1.    Ajoutez le nouveau serveur en tant que réplica secondaire au groupe de disponibilité. Consultez [Ajouter un réplica secondaire à un groupe de disponibilité (SQL Server)](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)dans la bibliothèque de documentation de SQL Server.

2.    Arrêtez le site Configuration Manager en exécutant **Preinst.exe /stopsite**. Consultez [Outil Maintenance de la hiérarchie](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

3.    Utilisez SQL Server pour créer une sauvegarde de la base de données du site à partir du réplica principal, puis restaurez cette sauvegarde sur le nouveau serveur réplica secondaire. Consultez [Créer une sauvegarde complète de base de données](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) et [Restaurer une sauvegarde de base de données à l’aide de SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) dans la documentation de SQL Server.

4.    Configurez chaque réplica secondaire. Pour chaque réplica secondaire dans le groupe de disponibilité, effectuez les opérations suivantes :

    1.    Vérifiez que le compte d’ordinateur du serveur de site est un membre du groupe **Administrateurs locaux** sur chaque ordinateur membre du groupe de disponibilité.

    2.    Exécutez le [script de vérification](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) indiqué dans la configuration requise pour confirmer que la base de données de site est correctement configurée sur chaque réplica.

    3.    S’il est nécessaire de configurer le nouveau réplica, basculez manuellement le réplica principal vers le nouveau réplica secondaire, puis modifiez les paramètres requis. Consultez [Effectuer un basculement manuel planifié d’un groupe de disponibilité (SQL Server)](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) dans la documentation de SQL Server.

5.    Redémarrez le site en démarrant le Gestionnaire de composant de site (**sitecomp**) et les services **SMS_Executive** .

### <a name="to-remove-a-replica-member"></a>Pour supprimer un membre réplica
Pour cette procédure, utilisez les informations de [Supprimer un réplica secondaire d’un groupe de disponibilité (SQL Server)](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) dans la documentation de SQL Server.

## <a name="stop-using-an-availability-group"></a>Cesser d’utiliser un groupe de disponibilité
Lorsque vous ne souhaitez plus héberger la base de données de votre site dans un groupe de disponibilité, procédez comme suit. Cela implique de déplacer la base de données de site vers une seule instance SQL Server.

Pour effectuer cette procédure, le compte que vous utilisez doit être :
-   membre du groupe **Administrateurs locaux** sur chaque ordinateur membre du groupe de disponibilité
-   **sysadmin** sur chaque instance SQL Server qui héberge la base de données du site.

> [!IMPORTANT]  
> Lorsque vous utilisez Microsoft Intune avec Configuration Manager dans une configuration hybride, le déplacement de la base de données de site vers ou depuis un groupe de disponibilité déclenche une resynchronisation des données avec le cloud. Cette opération est inévitable.

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Pour replacer la base de données du site à partir d’un groupe de disponibilité dans une instance SQL Server unique
1.    Arrêtez le site Configuration Manager à l’aide de la commande suivante : **Preinst.exe /stopsite**. Pour plus d'informations, consultez [Outil Maintenance de la hiérarchie](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.    Utilisez SQL Server pour créer une sauvegarde complète de la base de données de votre site à partir du réplica principal. Pour plus d’informations sur la façon de procéder, consultez [Créer une sauvegarde complète de base de données (SQL Server)](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) dans la documentation de SQL Server.

3.    Si le serveur représentant le réplica principal pour le groupe de disponibilité hébergera l’instance unique de la base de données du site, vous pouvez ignorer cette étape :  

    -   Utilisez SQL Server pour restaurer la sauvegarde de la base de données du site sur le serveur qui hébergera la base de données du site. Consultez [Restaurer une sauvegarde de base de données à l’aide de SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) dans la documentation de SQL Server.   <br />  <br />

4.    Sur le serveur qui hébergera la base de données de site (le réplica principal ou le serveur sur lequel vous avez restauré la base de données de site), remplacez le modèle de sauvegarde **Complète** de la base de données par **SIMPLE**. Consultez [Afficher ou modifier le mode de récupération d’une base de données (SQL Server)](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) dans la documentation de SQL Server.  

5.    Exécutez le **programme d’installation de Configuration Manager** à partir du **&lt;*dossier d’installation du site Configuration Manager>*\BIN\X64\setup.exe**.

6.    Sur la page **Mise en route** , sélectionnez **Effectuer une maintenance de site ou réinitialiser ce site**, puis cliquez sur **Suivant**.  

7.    Sélectionnez l’option **Modifier la configuration de SQL Server** , puis cliquez sur **Suivant**.  

8.    Reconfigurez ce qui suit pour la base de données du site :
    -   **Nom du serveur SQL Server :** entrez le nom du serveur hébergeant actuellement la base de données du site.

    -   **Instance :** spécifiez l’instance nommée hébergeant la base de données du site, ou laissez ce champ vide si la base de données se trouve sur l’instance par défaut.

    -   **Base de données :** laissez le nom tel qu’il s’affiche. Il s’agit du nom de la base de données du site actuel.    

9.    Après avoir fourni les informations relatives au nouvel emplacement de la base de données, exécutez le programme d’installation avec vos processus et configurations normaux. Une fois l’exécution du programme d’installation terminée, le site redémarre et commence à utiliser le nouvel emplacement de la base de données.    

10.    Pour nettoyer les serveurs qui étaient membres du groupe de disponibilité, suivez les instructions de [Supprimer un groupe de disponibilité (SQL Server)](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) dans la documentation de SQL Server.

