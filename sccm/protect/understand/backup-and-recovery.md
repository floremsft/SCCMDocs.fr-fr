---
title: Sauvegarde et restauration | Microsoft Docs
description: "Découvrez comment sauvegarder et récupérer vos sites en cas de défaillance ou de perte de données dans System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3aa9f2e4d3f7210981b5b84942485de11fe15cb2
ms.openlocfilehash: a7e052bc0e1c354b75a7f95afdd266ed742ce689

---

# <a name="backup-and-recovery"></a>Sauvegarde et récupération

*S’applique à : System Center Configuration Manager (Current Branch)*

Préparez les approches de sauvegarde et de récupération pour éviter la perte de données. Pour les sites Configuration Manager, une approche de sauvegarde et de récupération peut permettre de récupérer des sites et des hiérarchies plus rapidement avec une moindre perte de données. Utilisez les sections de cette rubrique pour vous aider à sauvegarder vos sites et à récupérer un site en cas de défaillance ou de perte de données.  



- [Sauvegarde d'un site Configuration Manager](#BKMK_SiteBackup)   

  - [Tâche de maintenance de sauvegarde](#BKMK_BackupMaintenanceTask)   

  - [Utilisation de Data Protection Manager pour sauvegarder votre base de données de site](#BKMK_DPMBackup)   

  -  [Archivage de l'instantané de sauvegarde](#BKMK_ArchivingBackupSnapshot)   

  -  [Utilisation du fichier AfterBackup.bat](#BKMK_UsingAfterBackup)   

  -  [Tâches de sauvegarde supplémentaires](#BKMK_SupplementalBackup)   

-  [Récupération d'un site Configuration Manager](#BKMK_RecoverSite)   

  -   [Détermination de vos options de récupération](#BKMK_DetermineRecoveryOptions)   

         -   [Options de récupération de serveur de site](#BKMK_SiteServerRecoveryOptions)   

         -   [Options de récupération de base de données de site](#BKMK_SiteDatabaseRecoveryOption)   

         -   [Période de rétention du suivi des modifications SQL Server](#bkmk_SQLretention)   

         -   [Processus de réinitialisation de site ou de données globales](#bkmk_reinit)   

         -   [Scénarios de récupération de base de données de site](#BKMK_SiteDBRecoveryScenarios)  

  -   [Clés du fichier de script de récupération de site sans assistance](#BKMK_UnattendedSiteRecoveryKeys)  

  -   [Tâches postérieures à la récupération](#BKMK_PostRecovery)  

  -   [Récupération d'un site secondaire](#BKMK_RecoverSecondarySite)  

-   [Service Enregistreur SMS](#BKMK_SMSWriterService)  

> [!NOTE]  
>  Si vous utilisez un groupe de disponibilité SQL Server AlwaysOn pour héberger la base de données du site, modifiez vos plans de sauvegarde et de récupération comme décrit dans la section [Modifications de la sauvegarde et de la récupération lorsque vous utilisez un groupe de disponibilité AlwaysOn SQL Server](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR) section de la rubrique [SQL Server AlwaysOn pour une base de données de site à haut niveau de disponibilité pour System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

##  <a name="a-namebkmksitebackupa-back-up-a-configuration-manager-site"></a><a name="BKMK_SiteBackup"></a> Sauvegarde d'un site Configuration Manager  
 Configuration Manager possède une tâche de maintenance de sauvegarde qui :  

-   s’exécute selon un calendrier ;  

-   sauvegarde la base de données du site ;  

-   sauvegarde des clés de Registre spécifiques ;  

-   sauvegarde des dossiers et fichiers spécifiques ;  

-   sauvegarde le dossier **CD.Latest**. (Voir [Dossier CD.Latest pour System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

 Planifiez l’exécution de la tâche de sauvegarde de site par défaut au minimum tous les cinq jours. La raison en est que Configuration Manager utilise une période de 5 jours comme [Période de rétention du suivi des modifications SQL Server](#bkmk_SQLretention).  

 Pour simplifier le processus de sauvegarde, vous pouvez créer un fichier **AfterBackup.bat** pour accomplir automatiquement des actions postérieures à la sauvegarde une fois la tâche de maintenance de sauvegarde correctement exécutée. Le fichier AfterBackup.bat est généralement utilisé pour archiver l'instantané de sauvegarde à un emplacement sécurisé. Vous pouvez également utiliser le fichier AfterBackup.bat pour copier des fichiers vers votre dossier de sauvegarde et démarrer d'autres tâches de sauvegarde supplémentaires.

Utilisez les sections suivantes pour créer votre stratégie de sauvegarde Configuration Manager.  

> [!NOTE]  
>  Configuration Manager peut récupérer la base de données de site à partir de la tâche de maintenance de sauvegarde Configuration Manager ou à partir d'une sauvegarde de base de données de site que vous avez créée avec un autre processus. Par exemple, vous pouvez restaurer la base de données de site à partir d'une sauvegarde créée dans le cadre du plan de maintenance de Microsoft SQL Server. Vous pouvez restaurer la base de données de site à partir d’une sauvegarde créée à l’aide de System Center 2012 Data Protection Manager (DPM). Pour plus d’informations, consultez [Utilisation de Data Protection Manager pour sauvegarder votre base de données de site](#BKMK_DPMBackup).  

###  <a name="a-namebkmkbackupmaintenancetaska-backup-maintenance-task"></a><a name="BKMK_BackupMaintenanceTask"></a> Tâche de maintenance de sauvegarde  
 Il est possible d'automatiser la sauvegarde des sites Configuration Manager en planifiant une tâche de maintenance de sauvegarde du serveur de site prédéfinie. Vous pouvez sauvegarder un site d'administration centrale et un site principal, mais il n'existe pas de prise en charge de la sauvegarde des sites secondaires ou des serveurs de système de site. Quand le service de sauvegarde de Configuration Manager est en cours d’exécution, il suit les instructions définies dans le fichier de contrôle de sauvegarde (**&lt;dossier_installation_ConfigMgr\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). Vous pouvez apporter des modifications à ce fichier de contrôle de la sauvegarde afin de changer le comportement du service de sauvegarde. Les informations sur l’état de la sauvegarde du site sont enregistrées dans le fichier **Smsbkup.log** . Ce fichier est créé dans le dossier de destination spécifié dans les propriétés de la tâche de maintenance de sauvegarde du serveur de site.  


##### <a name="to-enable-the-site-backup-maintenance-task"></a>Pour activer la tâche de maintenance de sauvegarde de site  

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Configuration de site**.  

     \> **Sites**.  

2.  Sélectionnez le site dans lequel vous souhaitez activer la tâche de maintenance de sauvegarde de site.  

3.  Dans l'onglet **Accueil**, dans le groupe **Paramètres**, cliquez sur **Tâches de maintenance de site**.  

4.  Choisissez **Serveur de site de sauvegarde**  >  **Modifier**.  

5.  Choisissez **Activer cette tâche** > **Définir les chemins** pour spécifier la destination de la sauvegarde. Les options suivantes sont disponibles :  

    > [!IMPORTANT]  
    >  Pour empêcher la falsification des fichiers de sauvegarde, stockez les fichiers dans un emplacement sécurisé. Le chemin de sauvegarde vers un lecteur local est le plus sûr pour pouvoir définir des autorisations de système de fichiers NTFS sur le dossier. Quelle que soit l'option que vous sélectionnez, Configuration Manager ne chiffre pas les données de sauvegarde stockées dans le chemin de sauvegarde.  

    -   **Lecteur local sur le serveur de site pour les données de site et la base de données**: spécifie que les fichiers de sauvegarde pour le site et la base de données de site sont stockés dans le chemin spécifié sur le disque local du serveur de site. Vous devez créer le dossier local avant d'exécuter la tâche de sauvegarde.   Le compte système local sur le serveur de site doit disposer des autorisations de système de fichiers NTFS en **écriture** sur le dossier local pour la sauvegarde de serveur de site. Le compte système local sur l'ordinateur qui exécute SQL Server doit disposer des autorisations NTFS en **écriture** sur le dossier pour la sauvegarde de base de données de site.  

    -   **Chemin d’accès réseau (nom UNC) aux données de site et à la base de données**: spécifie que les fichiers de sauvegarde pour le site et la base de données de site sont stockés dans le chemin UNC spécifié. Vous devez créer le partage avant d'exécuter la tâche de sauvegarde. Le compte d'ordinateur du serveur de site et le compte d'ordinateur de SQL Server (si SQL server est installé sur un autre ordinateur) doivent disposer des autorisations NTFS en **écriture** et de partage sur le dossier réseau partagé.  

    -   **Lecteurs locaux sur le serveur de site et SQL Server**: spécifie que les fichiers de sauvegarde pour le site sont stockés dans le chemin spécifié sur le disque local du serveur de site, et les fichiers de sauvegarde pour la base de données de site sont stockés sur le chemin spécifié sur le disque local du serveur de base de données de site. Vous devez créer les dossiers locaux avant d'exécuter la tâche de sauvegarde. Le compte d'ordinateur du serveur de site doit disposer des autorisations NTFS en **écriture** sur le dossier créé sur le serveur de site. Le compte d'ordinateur de SQL Server doit disposer des autorisations NTFS en **écriture** sur le dossier créé sur le serveur de base de données de site. Cette option est disponible uniquement lorsque la base de données de site n'est pas installée sur le serveur de site.  

    > [!NOTE]  
    >    - L'option d'accès à la destination de sauvegarde n'est disponible que lorsque vous spécifiez le chemin UNC de la destination de sauvegarde.

    > - Le nom de dossier ou le nom de partage utilisé pour la destination de sauvegarde ne prend pas en charge les caractères Unicode.  


6.  Configurez une planification pour la tâche de sauvegarde de site. Comme bonne pratique, considérez une planification de sauvegarde en dehors des heures de travail. Si vous disposez d'une hiérarchie, pensez à une planification qui s'exécute au moins deux fois par semaine pour assurer une conservation maximale des données en cas de défaillance du site.  

    Lorsque vous exécutez la console Configuration Manager sur le même serveur de site que vous configurez pour la sauvegarde, la tâche de maintenance de sauvegarde du serveur de site utilise l'heure locale pour la planification. Lorsque vous exécutez la console Configuration Manager à partir d'un ordinateur distant du site que vous configurez pour la sauvegarde, la tâche de maintenance de sauvegarde du serveur de site utilise le temps universel coordonné (UTC) pour la planification.  

7.  Indiquez si vous souhaitez créer une alerte en cas d'échec de la tâche de sauvegarde de site, cliquez sur **OK**, puis cliquez de nouveau sur **OK**. Lorsqu'il est sélectionné, Configuration Manager crée une alerte critique pour l'échec de sauvegarde, que vous pouvez consulter dans le nœud **Alertes** de l'espace de travail **Surveillance**.  

 Ensuite, vérifiez que la tâche de maintenance de sauvegarde du serveur de site est en cours d’exécution afin de vous assurer que les sauvegardes sont créées.  

##### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Pour vérifier que la tâche de maintenance de sauvegarde du serveur de site est en cours d’exécution  

-   Vérifiez que la tâche de maintenance de sauvegarde de site est en cours d’exécution en examinant les éléments suivants :  

    -   Vérifiez l'horodatage sur les fichiers dans le dossier de destination de sauvegarde qui a été créé par la tâche. Vérifiez que l'horodatage a été mis à jour avec l'heure de la dernière exécution de la tâche.  

    -   Dans le nœud **État du composant** de l'espace de travail **Surveillance** , consultez les messages d'état pour SMS_SITE_BACKUP. Lorsque la sauvegarde de site est terminée, le message ID 5035 s'affiche, indiquant que la sauvegarde de site a été effectuée sans erreurs.  

    -   Lorsque la tâche de maintenance de sauvegarde du serveur de site est configurée pour créer une alerte en cas d'échec de la sauvegarde, vous pouvez vérifier les échecs de sauvegarde dans le nœud **Alertes** de l'espace de travail **Surveillance** .  

    -   Dans &lt;*dossier_installation_ConfigMgr*>\Logs, recherchez les avertissements et les erreurs dans le fichier smsbkup.log. Une fois la sauvegarde de site terminée, `Backup completed` s'affiche avec un horodateur et un ID de message `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Lorsque la tâche de maintenance de la sauvegarde échoue, vous pouvez redémarrer la tâche de sauvegarde en arrêtant, puis en redémarrant le service SMS_SITE_BACKUP.  

###  <a name="a-namebkmkdpmbackupa-using-data-protection-manager-to-back-up-your-site-database"></a><a name="BKMK_DPMBackup"></a> Utilisation de Data Protection Manager pour sauvegarder votre base de données de site  
 Vous pouvez utiliser System Center 2012 Data Protection Manager (DPM) pour sauvegarder votre base de données de site. Vous devez créer un nouveau groupe de protection dans DPM pour l'ordinateur de base de données de site. Sur la page **Sélectionner les membres du groupe** de l'Assistant Création d'un nouveau groupe de protection, sélectionnez le service Enregistreur SMS dans la liste des sources de données, puis sélectionnez la base de données de site comme membre approprié. Pour plus d'informations sur l'utilisation de DPM pour sauvegarder votre base de données de site, voir [Bibliothèque de documentation de Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) sur TechNet.  

> [!IMPORTANT]  
>  Configuration Manager ne prend pas en charge la sauvegarde DPM pour un cluster SQL Server qui utilise une instance nommée, mais il prend en charge la sauvegarde DPM sur un cluster SQL Server qui utilise l'instance par défaut de SQL Server.  

 Après la restauration de la base de données de site, suivez les étapes décrites dans le processus d'installation pour récupérer le site. Sélectionnez l'option de récupération **Utiliser une base de données de site qui a été récupérée manuellement** pour utiliser la base de données de site que vous avez récupérée avec Data Protection Manager.  

###  <a name="a-namebkmkarchivingbackupsnapshota-archiving-the-backup-snapshot"></a><a name="BKMK_ArchivingBackupSnapshot"></a> Archivage de l'instantané de sauvegarde  
 La première fois que la tâche de maintenance de sauvegarde du serveur de site est exécutée, elle génère un instantané de sauvegarde que vous pouvez utiliser pour récupérer votre serveur de site en cas de défaillance. Lorsque la tâche de sauvegarde est réexécutée au cours des cycles suivants, un nouvel instantané de sauvegarde est créé et remplace l'instantané précédent. Ainsi, le site n'a qu'un seul instantané de sauvegarde, et vous n'avez aucun moyen de récupérer un instantané de sauvegarde antérieur.  

 Il est également recommandé d'effectuer plusieurs archives d'instantanés de sauvegarde pour les raisons suivantes :  

-   Il arrive souvent que le média de sauvegarde soit défectueux, égaré ou ne contienne qu'une partie de la sauvegarde. La récupération d'un site principal autonome défaillant à partir d'une sauvegarde ancienne est un moindre mal. Pour un serveur de site dans une hiérarchie, la sauvegarde doit être dans la période de rétention des modifications de suivi de SQL Server, ou bien la sauvegarde n'est pas requise.  

-   La corruption des données sur un site peut passer inaperçue pendant plusieurs cycles de sauvegarde. Vous devrez peut-être utiliser un instantané de sauvegarde antérieur à la corruption du site. Cela s'applique à un site primaire autonome et aux sites dans une hiérarchie où la sauvegarde se trouve dans la période de rétention des modifications de suivi de SQL Server.  

-   Le site ne dispose peut-être d'aucun instantané de sauvegarde si, par exemple, la tâche de maintenance de sauvegarde du serveur de site échoue. Comme la tâche de sauvegarde supprime l'instantané de sauvegarde précédent avant de démarrer la sauvegarde des données en cours, aucun instantané de sauvegarde valide ne sera disponible.  

###  <a name="a-namebkmkusingafterbackupa-using-the-afterbackupbat-file"></a><a name="BKMK_UsingAfterBackup"></a> Utilisation du fichier AfterBackup.bat  
 Après avoir sauvegardé le site, la tâche de sauvegarde du serveur de site tente automatiquement d'exécuter un fichier nommé AfterBackup.bat. Vous devez créer manuellement le fichier AfterBackup.bat dans &lt;*dossier_installation_ConfigMgr*>\Inboxes\Smsbkup. Si un fichier AfterBackup.bat existe et est stocké dans le dossier approprié, il est exécuté automatiquement à l'issue de l'exécution de la tâche de sauvegarde. Le fichier AfterBackup.bat permet d'archiver l'instantané de sauvegarde à la fin de chaque opération de sauvegarde, et d'effectuer automatiquement d'autres tâches postérieures à la sauvegarde, qui ne font pas partie de la tâche de maintenance de sauvegarde du serveur de site. Le fichier AfterBackup.bat intègre les opérations d'archivage et de sauvegarde, permettant ainsi d'archiver chaque nouvel instantané de sauvegarde. Lorsque le fichier AfterBackup.bat n'est pas présent, la tâche de sauvegarde l'ignore sans effet sur l'opération de sauvegarde. Pour vérifier que la tâche de sauvegarde de site a exécuté avec succès le fichier AfterBackup.bat, consultez le nœud **État du composant** dans l'espace de travail **Surveillance** et vérifiez les messages d'état pour SMS_SITE_BACKUP. Lorsque la tâche démarre avec succès le fichier de commande AfterBackup.bat, le message ID 5040 s'affiche.  

> [!TIP]  
>  Pour créer le fichier AfterBackup.bat afin d'archiver vos fichiers de sauvegarde de serveur de site, vous devez utiliser un outil de commande de copie, tel que Robocopy, dans le fichier de commandes. Par exemple, vous pouvez créer le fichier AfterBackup.bat et, sur la première ligne, ajouter une instruction similaire à la suivante : `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`. Pour plus d'informations sur Robocopy, consultez la page web de référence de ligne de commande [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) .  

 Même si le but premier du fichier AfterBackup.bat est d'archiver des instantanés de sauvegarde, vous pouvez créer un fichier AfterBackup.bat pour exécuter d'autres tâches à la fin de chaque opération de sauvegarde.  

###  <a name="a-namebkmksupplementalbackupa-supplemental-backup-tasks"></a><a name="BKMK_SupplementalBackup"></a> Tâches de sauvegarde supplémentaires  
 La tâche de maintenance de sauvegarde du serveur de site fournit un instantané de sauvegarde pour les fichiers de serveur de site et la base de données de site, mais il existe certains autres éléments non sauvegardés que vous devez considérer lorsque vous créez votre stratégie de sauvegarde. Utilisez les sections suivantes pour définir votre stratégie de sauvegarde Configuration Manager.  

#### <a name="back-up-custom-reporting-services-reports"></a>Sauvegarde des rapports Reporting Services personnalisés  
 Lorsque vous avez modifié des rapports Reporting Services personnalisés prédéfinis ou créés, la création d'une sauvegarde pour les fichiers de base de données de serveur du rapport est une partie importante de votre stratégie de sauvegarde. La sauvegarde du serveur de rapports doit inclure une sauvegarde des fichiers sources pour les rapports et les modèles, des clés de cryptage, des assemblys ou des extensions personnalisés, des fichiers de configuration, des vues SQL Server personnalisées, des procédures stockées personnalisées, etc.  

> [!IMPORTANT]  
>  Quand Configuration Manager est mis à niveau vers une version plus récente, les rapports prédéfinis peuvent être remplacés par de nouveaux rapports. Si vous modifiez un rapport prédéfini, sauvegardez le rapport avant d’effectuer la mise à jour, puis restaurez-le dans Reporting Services.  

 Pour plus d’informations sur la sauvegarde de vos rapports personnalisés dans Reporting Services, consultez [Opérations de sauvegarde et de restauration pour Reporting Services](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) dans la documentation en ligne de SQL Server 2014.  

#### <a name="backup-content-files"></a>Sauvegarde des fichiers de contenu  
 La bibliothèque de contenu dans Configuration Manager correspond à l'emplacement dans lequel sont enregistrés tous les fichiers de contenu pour le déploiement des mises à jour logicielles, des applications, du système d'exploitation, etc. La bibliothèque de contenu se trouve sur le serveur de site et sur chaque point de distribution. La tâche de maintenance de sauvegarde du serveur de site n'inclut pas une sauvegarde de la bibliothèque de contenu ou des fichiers sources du package. Lors de la défaillance d'un serveur de site, les informations sur les fichiers de la bibliothèque de contenu sont restaurées vers la base de données de site, mais vous devez restaurer la bibliothèque de contenu et les fichiers sources des packages sur le serveur de site.  

-   **Bibliothèque de contenu**: la bibliothèque de contenu doit être restaurée avant que vous puissiez redistribuer le contenu vers des points de distribution. Lorsque vous démarrez la redistribution du contenu, Configuration Manager copie les fichiers depuis la bibliothèque de contenu sur le serveur de site vers les points de distribution. La bibliothèque de contenu pour le serveur de site se trouve dans le dossier SCCMContentLib, qui est généralement situé sur le lecteur qui dispose de la plus grande quantité d'espace libre au moment de l'installation du site.  

-   **Fichiers sources d’un package**: les fichiers sources d’un package doivent être restaurés avant que vous puissiez mettre à jour le contenu sur des points de distribution. Lorsque vous démarrez la mise à jour d'un contenu, Configuration Manager copie les fichiers nouveaux ou modifiés depuis la source du package vers la bibliothèque de contenu, qui à son tour copie les fichiers vers des points de distribution associés. Vous pouvez exécuter la requête suivante dans SQL Server pour trouver l'emplacement source du package pour tous les packages et applications : `SELECT * FROM v_Package`. Vous pouvez identifier le site source du package en examinant les trois premiers caractères de l'ID de package. Par exemple, si l'ID de package est CEN00001, le code de site pour le site source est CEN. Lorsque vous restaurez les fichiers sources du package, ceux-ci doivent être restaurés vers le même emplacement que celui dans lequel ils se trouvaient avant la défaillance.  

 Vérifiez que vous incluez à la fois la bibliothèque de contenu et les emplacements sources du package dans la sauvegarde de votre système de fichiers pour le serveur de site.  

#### <a name="back-up-custom-software-updates"></a>Sauvegarder les mises à jour logicielles personnalisées  
 System Center Updates Publisher 2011 est un outil autonome qui vous permet de publier des mises à jour logicielles personnalisées vers Windows Server Update Services (WSUS), de synchroniser les mises à jour logicielles vers Configuration Manager, d’évaluer la compatibilité des mises à jour logicielles et de déployer des mises à jour logicielles personnalisées sur des clients. L’éditeur de mise à jour utilise une base de données locale pour son espace de stockage des mises à jour logicielles. Quand vous utilisez l’éditeur de mise à jour pour gérer les mises à jour logicielles personnalisées, déterminez si vous devez inclure la base de données de l’éditeur de mise à jour dans votre plan de sauvegarde. Pour plus d'informations sur l'éditeur de mise à jour, voir [Éditeur de mise à jour System Center 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) dans la bibliothèque TechCenter de System Center.  

 Utilisez la procédure suivante pour sauvegarder la base de données de l'éditeur de mise à jour.  

###### <a name="to-back-up-the-updates-publisher-2011-database"></a>Pour sauvegarder la base de données de l'éditeur de mise à jour 2011  

1.  Sur l’ordinateur qui exécute l’éditeur de mise à jour, accédez au fichier de base de données de l’éditeur de mise à jour (Scupdb.sdf) dans %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\\. Il existe un fichier de base de données différent pour chaque utilisateur qui exécute l’éditeur de mise à jour.  

2.  Copiez le fichier de base de données vers votre destination de sauvegarde. Par exemple, si votre destination de sauvegarde est E:\ConfigMgr_Backup, vous pouvez copier le fichier de base de données de l’éditeur de mise à jour vers E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  Lorsqu'il existe plusieurs fichiers de base de données sur un ordinateur, envisagez de stocker le fichier dans un sous-dossier qui indique le profil utilisateur associé au fichier de base de données. Par exemple, vous pourriez avoir un seul fichier de base de données dans E:\ConfigMgr_Backup\SCUP2011\User1 et un autre fichier de base de données dans E:\ConfigMgr_Backup\SCUP2011\User2.  

### <a name="user-state-migration-data"></a>Données de migration de l'état utilisateur  
 Vous pouvez utiliser des séquences de tâches Configuration Manager pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation où vous souhaitez conserver l’état utilisateur du système d’exploitation actuel. Les dossiers qui stockent les données d'état utilisateur sont répertoriés dans les propriétés du point de migration d'état. Ces données de migration d'état utilisateur ne sont pas sauvegardées dans le cadre de la tâche de maintenance de sauvegarde du serveur de site. Dans le cadre de votre plan de sauvegarde, vous devez sauvegarder manuellement les dossiers que vous spécifiez pour stocker les données de migration d'état utilisateur.   

#### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Pour déterminer les dossiers utilisés pour stocker les données de migration d'état utilisateur  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis choisissez **Serveurs et rôles de système de site**.  

3.  Sélectionnez le système de site qui héberge le rôle de migration d'état, puis choisissez **Point de migration de l'état** dans **Rôles de système de site**.  


4.  Dans l'onglet **Rôle du site** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  
5.  Les dossiers qui stockent les données de migration d'état utilisateur sont répertoriés dans la section **Détails du dossier** de l'onglet **Général** .  

## <a name="recover-a-configuration-manager-site"></a>Récupération d'un site Configuration Manager
 La récupération d'un site Configuration Manager est nécessaire à chaque défaillance d'un site Configuration Manager ou perte de données dans la base de données d'un site. La réparation et la resynchronisation des données constituent les principales tâches de récupération d'un site et elles sont nécessaires pour éviter l'interruption des opérations.  

> [!IMPORTANT]  
>  Quand vous récupérez la base de données pour un site :  

>  -   Vous devez utiliser la même version et la même édition de SQL Server. Par exemple, la restauration d’une base de données qui s’exécutait sur SQL Server 2012 vers SQL Server 2014 n’est pas prise en charge. De la même manière, il n’est pas possible de restaurer une base de données de site qui s’exécutait sur une édition Standard de SQL Server 2014 vers une édition Enterprise de SQL Server 2014.  
> -   SQL Server ne doit pas être configuré en **mode mono-utilisateur**.  
> -   Vérifiez que les fichiers .MDF et .LDF sont valides. Quand vous récupérez un site, l’état des fichiers que vous restaurez n’est pas vérifié.  


 La récupération du site est lancée en exécutant l’Assistant Installation de Configuration Manager à partir du dossier CD.Latest.  Vous pouvez également configurer le script d’installation sans assistance, puis utiliser l’option **/script** de la commande d’installation pour exécuter le programme d’installation à partir de ce même dossier CD.Latest. Vos options de récupération varient selon que vous disposez ou non d'une sauvegarde de la base de données du site Configuration Manager. Pour plus d’informations, voir [Dossier CD.Latest pour System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).  

> [!IMPORTANT]  
>  Si vous exécutez le programme d'installation de Configuration Manager à partir du menu **Démarrer** sur le serveur de site, l'option **Récupérer un site** n'est pas disponible.  

>  Si vous avez installé des mises à jour à partir de la console Configuration Manager avant d’effectuer votre sauvegarde, vous ne pouvez pas réinstaller correctement le site en utilisant le programme d’installation à partir du support d’installation ou du chemin d’installation de Configuration Manager.  

> [!NOTE]  
>  Après avoir restauré une base de données de site configurée pour des réplicas de base de données et avant de pouvoir utiliser les réplicas de base de données, vous devez reconfigurer chaque réplica de base de données en recréant les publications et les abonnements.  

###  <a name="a-namebkmkdeterminerecoveryoptionsa-determine-your-recovery-options"></a><a name="BKMK_DetermineRecoveryOptions"></a> Détermination de vos options de récupération  
 Il existe deux zones principales que vous devez prendre en compte pour la récupération d'un site principal Configuration Manager et d'un site d'administration centrale : le serveur de site et la base de données de site. Utilisez les sections suivantes pour vous aider à déterminer les options que vous devez sélectionner pour votre scénario de récupération.  

> [!NOTE]  

####  <a name="a-namebkmksiteserverrecoveryoptionsa-site-server-recovery-options"></a><a name="BKMK_SiteServerRecoveryOptions"></a> Options de récupération de serveur de site  
 Vous devez démarrer le programme d’installation à partir d’une copie du dossier CD.Latest que vous créez en dehors du dossier d’installation de Configuration Manager. Vous sélectionnez ensuite l’option **Récupérer un site** . Lorsque vous exécutez le programme d'installation, vous disposez des options de récupération suivantes pour le serveur de site défaillant :  

-   **Récupérer le serveur de site à l’aide d’une sauvegarde existante** : utilisez cette option si vous disposez d’une sauvegarde du serveur de site Configuration Manager qui a été créée sur le serveur de site dans le cadre de la tâche de maintenance de **sauvegarde du serveur de site** avant la défaillance du site. Le site est réinstallé et les paramètres du site sont configurés en fonction du site qui a été sauvegardé.  

-   **Réinstaller le serveur de site**: utilisez cette option si vous ne possédez pas de sauvegarde du serveur du site. Le serveur de site est réinstallé et vous devez spécifier les paramètres du site, comme vous le feriez lors d'une installation initiale. Vous devez utiliser les mêmes code de site et nom de base de données de site que ceux que vous avez utilisés lors de l'installation initiale du site défaillant afin de récupérer correctement le site.  

> [!NOTE]  
>  Lorsque le programme d'installation détecte un site Configuration Manager existant sur le serveur, vous pouvez démarrer une récupération de site, mais les options de récupération pour le serveur de site sont limitées. Par exemple, si vous exécutez le programme d'installation sur un serveur de site existant, lorsque vous choisissez la récupération, vous pouvez récupérer le serveur de base de données de site mais l'option de récupération du serveur de site est désactivée.  

####  <a name="a-namebkmksitedatabaserecoveryoptiona-site-database-recovery-options"></a><a name="BKMK_SiteDatabaseRecoveryOption"></a> Options de récupération de base de données de site  
 Lorsque vous exécutez le programme d'installation, vous disposez des options de récupération suivantes pour la base de données de site :  

-   **Récupérer la base de données de site à l’aide d’un jeu de sauvegarde** : utilisez cette option si vous disposez d’une sauvegarde de la base de données de site Configuration Manager qui a été créée dans le cadre de la tâche de maintenance de **sauvegarde du serveur de site** exécutée sur le site avant la défaillance de la base de données de site. Lorsque vous possédez une hiérarchie, les modifications qui ont été effectuées au niveau de la base de données de site après la dernière sauvegarde de la base de données de site sont récupérées à partir du site d'administration centrale pour un site principal ou à partir d'un site principal de référence pour un site d'administration centrale. Lorsque vous récupérez la base de données de site pour un site principal autonome, vous perdez les modifications effectuées au niveau du site après la dernière sauvegarde.  

     Lorsque vous récupérez la base de données de site pour un site d'une hiérarchie, le comportement de récupération est différent pour un site d'administration centrale et un site principal et lorsque la dernière sauvegarde se situe pendant ou en dehors de la période de rétention du suivi des modifications SQL Server. Pour plus d’informations, voir la section [Scénarios de récupération de base de données de site](#BKMK_SiteDBRecoveryScenarios) de cette rubrique.  

    > [!NOTE]  
    >  La récupération échoue si vous choisissez de restaurer la base de données de site à l'aide d'un jeu de sauvegarde, alors que la base de données de site existe déjà.  

-   **Créer une nouvelle base de données pour ce site** : utilisez cette option si vous ne possédez pas de sauvegarde de la base de données de site Configuration Manager. Lorsque vous possédez une hiérarchie, une nouvelle base de données de site est créée et les données sont récupérées à l'aide des données répliquées depuis le site d'administration centrale pour un site principal ou depuis un site principal de référence pour un site d'administration centrale. Cette option n'est pas disponible lorsque vous récupérez un site principal autonome ou un site d'administration centrale qui ne possède pas de sites principaux.  

-   **Utiliser une base de données de site qui a été récupérée manuellement** : utilisez cette option quand vous avez déjà récupéré la base de données de site Configuration Manager mais que vous devez effectuer le processus de récupération. Configuration Manager peut récupérer la base de données de site à partir de la tâche de maintenance de sauvegarde Configuration Manager ou à partir d'une sauvegarde de base de données de site que vous effectuez à l’aide de DPM ou d’autre processus. Après avoir restauré la base de données de site à l'aide d'une méthode en dehors de Configuration Manager, vous devez exécuter le programme d'installation et sélectionner cette option pour effectuer la récupération de la base de données de site. Lorsque vous possédez une hiérarchie, les modifications qui ont été effectuées au niveau de la base de données de site après la dernière sauvegarde de la base de données de site sont récupérées à partir du site d'administration centrale pour un site principal ou à partir d'un site principal de référence pour un site d'administration centrale. Lorsque vous récupérez la base de données de site pour un site principal autonome, vous perdez les modifications effectuées au niveau du site après la dernière sauvegarde.  

    > [!NOTE]  
    >  Lorsque vous utilisez DPM pour sauvegarder votre base de données de site, appliquez les procédures DPM pour restaurer la base de données de site sur un emplacement défini avant de continuer le processus de restauration dans Configuration Manager. Pour plus d'informations sur DPM, voir [Bibliothèque de documentation de Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) sur TechNet.  

-   **Ignorer la récupération de base de données** : utilisez cette option quand aucune perte de données ne s’est produite sur le serveur de base de données de site Configuration Manager. Cette option est valide uniquement lorsque la base de données de site se trouve sur un ordinateur différent du serveur de site que vous récupérez.  

####  <a name="a-namebkmksqlretentiona-sql-server-change-tracking-retention-period"></a><a name="bkmk_SQLretention"></a> Période de rétention du suivi des modifications SQL Server  
 Le suivi des modifications est activé pour la base de données de site dans SQL Server. Le suivi des modifications permet à Configuration Manager de demander des informations sur les modifications qui ont été apportées aux tables de base de données après un moment précis. La période de rétention spécifie la durée de conservation des informations de suivi des modifications. Par défaut, la période de rétention de la base de données de site est définie sur 5 jours. Lorsque vous récupérez une base de données de site, le processus de récupération se déroule différemment si votre sauvegarde a lieu pendant ou en dehors de la période de rétention. Par exemple, en cas d'échec de votre serveur de base de données de site, si votre dernière sauvegarde remonte à 7 jours, elle se situe en dehors de la période de rétention.

 Pour plus d’informations sur les éléments internes du suivi des modifications SQL Server, consultez les blogs de l’équipe SQL Server suivants : [Nettoyage du suivi des modifications - partie 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1) et [Nettoyage du suivi des modifications - partie 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).



####  <a name="a-namebkmkreinita-process-to-reinitialize-site-or-global-data"></a><a name="bkmk_reinit"></a> Processus de réinitialisation de site ou de données globales  
 Le processus de réinitialisation de site ou de données globales remplace les données existantes dans la base de données de site par les données d'une autre base de données de site. Par exemple, lorsque le site ABC réinitialise les données du site XYZ, les étapes suivantes se produisent :  

-   Les données sont copiées du site XYZ au site ABC.  

-   Les données existantes pour le site XYZ sont supprimées de la base de données de site sur le site ABC.  

-   Les données copiées à partir du site XYZ sont insérées dans la base de données de site du site ABC.  

##### <a name="example-scenario-1"></a>Exemple de scénario 1  
 **Le site principal réinitialise les données globales à partir du site d’administration centrale**: le processus de récupération supprime les données globales existantes pour le site principal dans la base de données du site principal et remplace les données par les données globales copiées à partir du site d’administration centrale.  

##### <a name="example-scenario-2"></a>Exemple de scénario 2  
 **Le site d’administration centrale réinitialise les données du site à partir d’un site principal**: le processus de récupération supprime les données de site existantes pour ce site principal dans la base de données du site d’administration centrale et remplace les données par les données de site copiées à partir du site principal. Les données de site d'autres sites principaux ne sont pas affectées.  

####  <a name="a-namebkmksitedbrecoveryscenariosa-site-database-recovery-scenarios"></a><a name="BKMK_SiteDBRecoveryScenarios"></a> Scénarios de récupération de base de données de site  
 Suite à la restauration d'une base de données de site à partir d'une sauvegarde, Configuration Manager tente de restaurer les modifications effectuées au niveau du site et des données globales après la dernière sauvegarde de la base de données. Voici une description des actions que Configuration Manager démarre après la restauration d’une base de données de site à partir d’une sauvegarde.  

 **Le site récupéré est un site d’administration centrale :**  

-   **Sauvegarde de base de données pendant la période de rétention du suivi des modifications**  

    -   **Données globales :** les modifications des données globales après la sauvegarde sont répliquées à partir de tous les sites principaux.  

    -   **Données de site :** les modifications des données du site après la sauvegarde sont répliquées à partir de tous les sites principaux.  

-   **Sauvegarde de base de données antérieure à la période de rétention du suivi des modifications**  

    -   **Données globales :** le site d’administration centrale réinitialise les données globales à partir du site principal de référence, si vous le spécifiez. Ensuite, tous les autres sites principaux réinitialisent les données globales à partir du site d'administration centrale. Si aucun site de référence n'est spécifié, tous les sites principaux réinitialisent les données globales à partir du site d'administration centrale (les données qui ont été restaurées à partir de la sauvegarde).  

    -   **Données de site :** le site d’administration centrale réinitialise les données de site à partir de chaque site principal.  

 **Le site récupéré est un site principal :**  

-   **Sauvegarde de base de données pendant la période de rétention du suivi des modifications**  

    -   **Données globales :** les modifications apportées aux données globales après la sauvegarde sont répliquées à partir du site d’administration centrale.  

    -   **Données de site :** le site d’administration centrale réinitialise les données de site à partir du site principal. Les modifications après la sauvegarde sont perdues, mais la plupart des données sont régénérées par les clients qui envoient des informations au site principal.  

-   **Sauvegarde de base de données antérieure à la période de rétention du suivi des modifications**  

    -   **Données globales :** le site principal réinitialise les données globales à partir du site d’administration centrale.  

    -   **Données de site :** le site d’administration centrale réinitialise les données de site à partir du site principal. Les modifications après la sauvegarde sont perdues, mais la plupart des données sont régénérées par les clients qui envoient des informations au site principal.  

### <a name="site-recovery-procedures"></a>Procédures de récupération de site  
 Appliquez l'une des procédures suivantes pour récupérer votre serveur de site ainsi que la base de données du site.  

##### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Pour démarrer une récupération de site avec l'Assistant Installation  

1.  Copiez le dossier CD.Latest à un emplacement en dehors du dossier d’installation de Configuration Manager. (Voir [Dossier CD.Latest pour System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).)  

     À partir de la copie du dossier CD.Latest, exécutez l’Assistant Installation de Configuration Manager.  

2.  Sur la page **Mise en route** , sélectionnez **Récupérer un site**, puis cliquez sur **Suivant**.  

3.  Terminez l'Assistant en utilisant les options qui conviennent à la récupération de votre site.  

    > [!IMPORTANT]  
    >  Pendant la récupération, le programme d'installation identifie le port de SQL Server Service Broker (SSB) utilisé par SQL Server. Ne modifiez pas ce paramètre de port lors de la récupération, sinon, la réplication de données ne fonctionnera pas correctement une fois la récupération terminée.  

    > [!NOTE]  
    >  Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager dans l’Assistant Installation.  

##### <a name="to-start-an-unattended-site-recovery"></a>Pour démarrer une récupération de site en mode sans assistance  

1.  Préparez le script d'installation sans assistance pour les options dont vous avez besoin pour la récupération du site.  

2.  Exécutez le programme d’installation de Configuration Manager en utilisant l’option de commande **/script**. Par exemple, si vous avez nommé le fichier d’initialisation de l’installation ConfigMgrUnattend.ini et que vous l’avez enregistré dans le répertoire C:\Temp de l’ordinateur sur lequel vous exécutez le programme d’installation, la commande est la suivante : **Setup /script C:\temp\ConfigMgrUnattend.ini**  

> [!NOTE]  
>  Après la récupération d’un site d’administration centrale, l’établissement de la réplication de certaines données de site à partir des sites enfants peut échouer. Cela peut inclure l’inventaire matériel, l’inventaire logiciel et les messages d’état.  
>   
>  Si cela se produit, vous devez réinitialiser **ConfigMgrDRSSiteQueue** pour la réplication de base de données.  Pour ce faire, utilisez **SQL Server Manager** pour exécuter la requête suivante sur la base de données de site Configuration Manager sur le site d’administration centrale :  
>   
>  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = ’ConfigMgrDRSSiteQueue’ AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="a-namebkmkunattendedsiterecoverykeysa-unattended-site-recovery-script-file-keys"></a><a name="BKMK_UnattendedSiteRecoveryKeys"></a> Clés du fichier de script de récupération de site sans assistance  
 Pour effectuer une récupération en mode sans assistance d'un site d'administration centrale Configuration Manager ou d'un site principal, vous pouvez créer un script d'installation sans assistance et utiliser le programme d'installation avec l'option de commande /script. Le script fournit le même type d'informations que les invites de l'Assistant Installation ; la seule différence est qu'il n'existe pas de paramètres par défaut. Toutes les valeurs doivent être indiquées pour les clés d'installation qui s'appliquent au type de récupération choisi.  

 Vous pouvez exécuter le programme d'installation de Configuration Manager sans assistance en utilisant un fichier d'initialisation avec l'option de ligne de commande d'installation /script. L'installation sans assistance est prise en charge pour la récupération d'un site d'administration centrale Configuration Manager et d'un site primaire. Pour utiliser l'option de ligne de commande d'installation /script, vous devez créer un fichier d'initialisation et en spécifier le nom après l'option de ligne de commande d'installation /script. Le nom du fichier n'a pas importance tant qu'il est suivi de l'extension de fichier .ini. Lorsque vous référencez le fichier d'initialisation d'installation à partir de la ligne de commande, vous devez fournir le chemin d'accès complet au fichier. Par exemple, si votre fichier d'initialisation d'installation s'appelle setup.ini et qu'il est stocké dans le dossier C:\setup, votre ligne de commande serait :  

 **setup /script c:\setup\setup.ini**.  

> [!IMPORTANT]  
>  Vous devez disposer de droits d'administrateur pour exécuter le programme d'installation. Lorsque vous exécutez le programme d'installation avec le script sans assistance, démarrez l'invite de commande dans un contexte d'administrateur à l'aide de l'option **Exécuter en tant qu'administrateur**.  

 Le script contient les noms de section, les noms de clé et les valeurs. Les noms des clés de section requis varient en fonction du type de récupération faisant l'objet du script. L’ordre des clés dans les sections et l’ordre des sections dans le fichier n’ont pas d’importance. Les clés ne tiennent pas compte de la casse. Lorsque vous attribuez des valeurs aux clés, le nom de la clé doit être suivi du signe égal (=) et de la valeur de la clé.  

 Utilisez les sections suivantes pour créer votre script de récupération de site en mode sans assistance. Les tableaux répertorient les clés de script d'installation disponibles ainsi que leurs valeurs correspondantes, indiquent si elles sont obligatoires ou non, le type d'installation pour lequel elles sont utilisées, ainsi qu'une brève description de la clé.  

#### <a name="recover-a-central-administration-site-unattended"></a>Récupérer un site d’administration centrale sans assistance  
 Utilisez les informations suivantes pour configurer un fichier de script d’installation sans assistance afin de récupérer un site d’administration centrale.  

 **Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** RecoverCCAR  

    -   **Détails :** récupère un site d’administration centrale  

**RecoveryOptions**  

-   **Nom de clé :** ServerRecoveryOptions  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 1, 2 ou 4  

         1 = Serveur de site de récupération et SQL Server.  

         2 = Récupérer le serveur de site uniquement.  

         4 = Récupérer SQL Server uniquement.  

    -   **Détails :** spécifie si le programme d’installation doit récupérer le serveur de site, SQL Server ou les deux. Les clés associées sont requises lorsque vous définissez la valeur suivante pour le paramètre ServerRecoveryOptions :  

        -   **Valeur = 1** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

             la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.  

        -   **Valeur = 2** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   **Valeur = 4** la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.  

-   **Nom de clé :** DatabaseRecoveryOptions  

    -   **Obligatoire :** peut-être  

    -   **Valeurs :** 10, 20, 40, 80  

         10 = Restaurer la base de données du site à partir d'une sauvegarde.  

         20 = Utiliser une base de données de site qui a été récupérée manuellement à l'aide d'une autre méthode.  

         40 = Créer une nouvelle base de données de site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  

         80 = Ignorer la récupération de base de données.  

    -   **Détails :** spécifie comment le programme d’installation va récupérer la base de données de site dans SQL Server. Cette clé est requise lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **4**.  

-   **Nom de clé :** ReferenceSite  

    -   **Obligatoire :** peut-être  

    -   **Valeurs :** &lt;nom_domaine_complet_site_référence\>  

    -   **Détails :** spécifie le site principal de référence que le site d’administration centrale utilise pour récupérer des données globales si la sauvegarde de la base de données est antérieure à la période de rétention du suivi des modifications ou quand vous récupérez le site sans sauvegarde.  

         Lorsque vous ne spécifiez pas de site de référence et que la sauvegarde est antérieure à la période de rétention du suivi des modifications, tous les sites principaux sont réinitialisés avec les données restaurées à partir du site d'administration centrale.  

         Lorsque vous ne spécifiez pas de site de référence, et que la sauvegarde est comprise dans la période de rétention du suivi des modifications, seules les modifications apportées depuis la dernière sauvegarde sont répliquées à partir des sites principaux. Lorsqu'il existe des conflits entre des modifications issues de différents sites principaux, le site d'administration centrale utilise la première modification reçue.  

         Cette clé est requise lorsque le paramètre **DatabaseRecoveryOptions** a la valeur **40**.  

-   **Nom de clé :** SiteServerBackupLocation  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;chemin_vers_jeu_sauvegarde_serveur_site\>  

    -   **Détails :** spécifie le chemin vers le jeu de sauvegarde du serveur de site. Cette clé est optionnelle lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

-   **Nom de clé :** BackupLocation  

    -   **Obligatoire :** peut-être  

    -   **Valeurs :** &lt;chemin_vers_jeu_sauvegarde_base_de_données_site\>  

    -   **Détails :** spécifie le chemin d’accès au jeu de sauvegarde de la base de données du site. La clé **BackupLocation** est requise lorsque vous configurez une valeur de **1** ou **4** pour la clé **ServerRecoveryOptions** , et une valeur de **10** pour la clé **DatabaseRecoveryOptions** .  

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Eval  

    -   **Détails :** clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;code_de_site\>  

    -   **Détails :** trois caractères alphanumériques identifiant le site de façon univoque dans votre hiérarchie. Vous devez définir le code de site utilisé par le site avant la défaillance.  

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** nom_site  

    -   **Détails :** description de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*CheminInstallationConfigMgr*>  

    -   **Détails :** spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

        > [!NOTE]  
        >  Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** spécifie le FQDN du serveur qui héberge le fournisseur SMS. Vous devez spécifier le serveur qui hébergeait le fournisseur SMS avant la défaillance.  

         Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = téléchargement  

         1 = déjà téléchargé  

    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d'installation va télécharger les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>  

    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur **PrerequisiteComp** , le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou pour localiser des fichiers précédemment téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** peut-être  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si la console Configuration Manager doit ou non être installée. Cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.  

-   **Nom de clé :** JoinCEIP  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas joindre  

         1 = joindre  

    -   **Détails :** spécifie si vous voulez vous joindre au programme d’amélioration de l’expérience utilisateur.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *&lt;nom_SQLServer\>*  

    -   **Détails :** nom du serveur ou nom de l’instance en cluster exécutant SQL Server, et devant héberger la base de données de site. Vous devez spécifier le serveur qui a hébergé la base de données de site avant la défaillance.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :**  

         *&lt;nom_base_de_données_site\>*  

         ou  

         *&lt;nom_instance\>*\\*&lt;nom_base_de_données_site\>*  

    -   **Détails :** nom de la base de données SQL Server à créer ou à utiliser pour installer la base de données du site d’administration centrale. Vous devez spécifier le nom de base de données qui était utilisé avant la défaillance.  

        > [!IMPORTANT]  
        >  Si vous n'utilisez pas l'instance par défaut, vous devez spécifier le nom d'instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*numéro_port_SSB*>  

    -   **Détails :** spécifiez le port SQL Server Service Broker (SSB) utilisé par SQL Server. Généralement, SSB est configuré pour utiliser le port TCP 4022, mais d'autres ports sont pris en charge. Vous devez définir le même port SSB utilisé avant la défaillance.  

#### <a name="recover-a-primary-site-unattended"></a>Récupérer un site principal en mode sans assistance  
 Utilisez les informations suivantes pour configurer un fichier de script d’installation sans assistance afin de récupérer un site d’administration centrale.  

 **Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** site_principal_à_récupérer  

    -   **Détails :** récupère un site principal  

**RecoveryOptions**  

-   **Nom de clé :** ServerRecoveryOptions  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 1, 2 ou 4  

         1 = Serveur de site de récupération et SQL Server.  

         2 = Récupérer le serveur de site uniquement.  

         4 = Récupérer SQL Server uniquement.  

    -   **Détails :** spécifie si le programme d’installation doit récupérer le serveur de site, SQL Server ou les deux. Les clés associées sont requises lorsque vous définissez la valeur suivante pour le paramètre ServerRecoveryOptions :  

        -   **Valeur = 1** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

             la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.  

        -   **Valeur = 2** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   **Valeur = 4** la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.  

-   **Nom de clé :** DatabaseRecoveryOptions  

    -   **Obligatoire :** peut-être  

    -   **Valeurs :** 10, 20, 40, 80  

         10 = Restaurer la base de données du site à partir d'une sauvegarde.  

         20 = Utiliser une base de données de site qui a été récupérée manuellement à l'aide d'une autre méthode.  

         40 = Créer une nouvelle base de données de site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  

         80 = Ignorer la récupération de base de données.  

    -   **Détails :** spécifie comment le programme d’installation va récupérer la base de données de site dans SQL Server. Cette clé est requise lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **4**.  

-   **Nom de clé :** SiteServerBackupLocation  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;chemin_vers_jeu_sauvegarde_serveur_site\>  

    -   **Détails :** spécifie le chemin vers le jeu de sauvegarde du serveur de site. Cette clé est optionnelle lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

-   **Nom de clé :** BackupLocation  

    -   **Obligatoire :** peut-être  

    -   **Valeurs :** &lt;chemin_vers_jeu_sauvegarde_base_de_données_site\>  

    -   **Détails :** spécifie le chemin d’accès au jeu de sauvegarde de la base de données du site. La clé **BackupLocation** est requise lorsque vous configurez une valeur de **1** ou **4** pour la clé **ServerRecoveryOptions** , et une valeur de **10** pour la clé **DatabaseRecoveryOptions** .  

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Eval  

    -   **Détails :** clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;code_de_site\>  

    -   **Détails :** trois caractères alphanumériques identifiant le site de façon univoque dans votre hiérarchie. Vous devez définir le code de site utilisé par le site avant la défaillance.  

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** nom_site  

    -   **Détails :** description de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*CheminInstallationConfigMgr*>  

    -   **Détails :** spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

        > [!NOTE]  
        >  Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** spécifie le FQDN du serveur qui héberge le fournisseur SMS. Vous devez spécifier le serveur qui hébergeait le fournisseur SMS avant la défaillance.  

         Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = téléchargement  

         1 = déjà téléchargé  

    -   **Détails :** spécifie si les fichiers d’installation prérequis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d'installation va télécharger les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** &lt;*chemin_fichiers_requis_programme_installation*>  

    -   **Détails :** spécifie le chemin vers les fichiers d’installation prérequis. Selon la valeur **PrerequisiteComp** , le programme d'installation utilise ce chemin d'accès pour stocker les fichiers téléchargés ou pour localiser des fichiers précédemment téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** peut-être  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas installer  

         1 = installer  

    -   **Détails :** spécifie si la console Configuration Manager doit ou non être installée. Cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.  

-   **Nom de clé :** JoinCEIP  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = ne pas joindre  

         1 = joindre  

    -   **Détails :** spécifie si vous voulez vous joindre au programme d’amélioration de l’expérience utilisateur.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *&lt;nom_SQLServer\>*  

    -   **Détails :** nom du serveur ou nom de l’instance en cluster exécutant SQL Server, et devant héberger la base de données de site. Vous devez spécifier le serveur qui a hébergé la base de données de site avant la défaillance.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :**  

         *&lt;nom_base_de_données_site\>*  

         ou  

         *&lt;nom_instance\>*\\*&lt;nom_base_de_données_site\>*  

    -   **Détails :** nom de la base de données SQL Server à créer ou à utiliser pour installer la base de données du site d’administration centrale. Vous devez spécifier le nom de base de données qui était utilisé avant la défaillance.  

        > [!IMPORTANT]  
        >  Si vous n'utilisez pas l'instance par défaut, vous devez spécifier le nom d'instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*numéro_port_SSB*>  

    -   **Détails :** spécifiez le port SQL Server Service Broker (SSB) utilisé par SQL Server. Généralement, SSB est configuré pour utiliser le port TCP 4022, mais d'autres ports sont pris en charge. Vous devez définir le même port SSB utilisé avant la défaillance.  

**Option d’extension de hiérarchie**  

-   **Nom de clé :** CCARSiteServer  

    -   **Obligatoire :** peut-être  

    -   **Valeurs :** &lt;*code_site_pour_site_administration_centrale*>  

    -   **Détails :** spécifie le site d’administration centrale auquel un site principal s’attache quand il rejoint la hiérarchie Configuration Manager. Ce paramètre est requis si le site principal était attaché à un site d'administration centrale avant la défaillance. Vous devez spécifier le code de site qui était utilisé pour le site d'administration centrale avant la défaillance.  

-   **Nom de clé :** CASRetryInterval  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*intervalle*>  

    -   **Détails :** spécifie l’intervalle (en minutes) avant une nouvelle tentative de connexion au site d’administration centrale après un échec de connexion. Par exemple, en cas d'échec de la connexion au site d'administration centrale, le site principal attend le nombre de minutes que vous avez spécifié pour CASRetryInterval et essaie de nouveau d'établir une connexion.  

-   **Nom de clé :** WaitForCASTimeout  

    -   **Obligatoire :** non  

    -   **Valeurs :** &lt;*délai d’attente*>  

    -   **Détails :** spécifie la valeur maximale du délai d’attente (en minutes) pour qu’un site principal se connecte au site d’administration centrale. Par exemple, si un site principal ne parvient pas à se connecter à un site d'administration centrale, le site principal essaie de nouveau d'établir une connexion selon la valeur de CASRetryInterval jusqu'à ce que le délai WaitForCASTimeout soit atteint. Vous pouvez spécifier une valeur de 0 à 100.  

###  <a name="a-namebkmkpostrecoverya-post-recovery-tasks"></a><a name="BKMK_PostRecovery"></a> Tâches postérieures à la récupération  
 Après avoir récupéré votre site, il existe plusieurs tâches à effectuer après la récupération, pour que celle-ci soit complète. Utilisez les sections suivantes pour vous aider à terminer le processus de récupération de site.  

#### <a name="re-enter-user-account-passwords"></a>Entrer de nouveau des mots de passe du compte d'utilisateur  
 Après une récupération de serveur de site, les mots de passe des comptes d'utilisateur spécifiés pour le site doivent être entrés de nouveau car ils sont réinitialisés par la restauration du site. Les comptes sont répertoriés sur la page **Terminé** de l'Assistant Installation après la récupération du site, et enregistrés dans C:\ConfigMgrPostRecoveryActions.html sur le serveur de site récupéré.  

###### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Pour entrer de nouveau les mots de passe du compte d'utilisateur après la récupération du site  

1.  Ouvrez la console Configuration Manager et connectez-vous au site récupéré.  

2.  Dans la console Configuration Manager, cliquez sur **Administration**.  

3.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Comptes**.  

4.  Pour chaque compte pour lequel vous devez entrer de nouveau le mot de passe, effectuez les opérations suivantes :  

    1.  Sélectionnez le compte dans la liste des comptes identifiés après la récupération du site. Vous trouverez cette liste dans C:\ConfigMgrPostRecoveryActions.html sur le serveur de site récupéré.  

    2.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés** pour ouvrir les propriétés du compte.  

    3.  Dans l'onglet **Général** , cliquez sur **Définir**et entrez de nouveau les mots de passe du compte.  

    4.  Cliquez sur **Vérifier**, sélectionnez la source de données appropriée pour le compte d'utilisateur sélectionné, puis cliquez sur **Tester la connexion** pour vérifier que le compte d'utilisateur peut se connecter à la source de données.  

    5.  Cliquez sur **OK** pour enregistrer les modifications du mot de passe, puis cliquez sur **OK**.  

#### <a name="re-enter-sideloading-keys"></a>Entrer de nouveau les clés de chargement de version test  
 Après une récupération de serveur de site, vous devez saisir à nouveau les clés de chargement de version test Windows spécifiées pour le site, car elles sont réinitialisées lors de la récupération de site. Une fois que vous avez de nouveau entré les clés de chargement de version test, la valeur de la colonne **Activations utilisées** pour les clés de chargement de version test Windows est réinitialisée dans la console Configuration Manager. Par exemple, avant la défaillance du site, la valeur du champ **Total activations** est définie sur **100** et **Activations utilisées** sur **90** pour le nombre de clés qui ont été utilisées par les appareils. Après la récupération du site, la colonne **Total activations** affiche toujours **100**, mais la colonne **Activations utilisées** affiche la valeur erronée de **0**. Cependant, une fois que 10 nouveaux appareils auront utilisé une clé de chargement de version test, il ne restera aucune clé de chargement de version test et l'appareil suivant ne parviendra pas à appliquer une clé de chargement de version test.  

#### <a name="recreate-the-microsoft-intune-subscription"></a>Recréer l’abonnement Microsoft Intune  
 Si vous récupérez un serveur de site Configuration Manager après que l’ordinateur serveur de site a été ré-imagé, l’abonnement Microsoft Intune n’est pas restauré. Vous devez reconnecter l’abonnement après avoir récupéré le site.  Ne créez pas de demande APN. À la place, chargez le fichier .pem valide actuel qui a été chargé la dernière fois que la gestion iOS a été configurée ou renouvelée. Pour plus d’informations, consultez [Configuration de l’abonnement Microsoft Intune](../../mdm/deploy-use/setup-hybrid-mdm.md#step-3-configure-intune-subscription).  

#### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurer SSL pour les rôles de système de site qui utilisent IIS  
 Lorsque vous récupérez des systèmes de site qui exécutent IIS et qui ont été configurés pour le protocole HTTPS avant la panne, vous devez reconfigurer IIS pour utiliser le certificat de serveur Web.  

#### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Réinstaller les correctifs sur le serveur de site récupéré  
 Après la récupération d'un site, vous devez réinstaller tous les correctifs qui étaient appliqués au serveur de site. Les correctifs logiciels précédemment installés sont répertoriés dans la page **Terminé** de l’Assistant Installation après la récupération du site et ils sont enregistrés dans **C:\ConfigMgrPostRecoveryActions.html** sur le serveur de site récupéré.  

#### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Récupérer des rapports personnalisés sur l'ordinateur qui exécute Reporting Services  
 Si vous avez créé des rapports de Reporting Services personnalisés, en cas de défaillance de Reporting Services, vous pouvez récupérer les rapports lorsque le serveur de rapports a été sauvegardé. Pour plus d'informations sur la restauration de vos rapports personnalisés dans Reporting Services, voir [Opérations de sauvegarde et de restauration pour une installation Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) dans la documentation en ligne de SQL Server 2008.  

#### <a name="recover-content-files"></a>Récupérer des fichiers de contenu  
 La base de données du site contient des informations sur l'emplacement des fichiers de contenu sur le serveur de site, mais les fichiers de contenu ne sont pas sauvegardés ou restaurés lors du processus de sauvegarde et de récupération. Pour récupérer complètement les fichiers de contenu, vous devez restaurer la bibliothèque de contenu et les fichiers sources du package vers leur emplacement d'origine. Il existe plusieurs méthodes pour récupérer vos fichiers de contenu, mais la méthode la plus simple consiste à récupérer les fichiers à partir d'une sauvegarde du système de fichiers du serveur de site.  

 Si vous ne disposez pas de sauvegarde du système de fichiers pour les fichiers sources du package, vous devez les copier ou les télécharger manuellement, comme vous l'avez fait lors de la création initiale du package. Vous pouvez exécuter la requête suivante dans SQL Server pour trouver l'emplacement source du package pour tous les packages et applications : `SELECT * FROM v_Package`. Vous pouvez identifier le site source du package en examinant les trois premiers caractères de l'ID de package. Par exemple, si l'ID de package est CEN00001, le code de site pour le site source est CEN. Lorsque vous restaurez les fichiers sources du package, ceux-ci doivent être restaurés vers le même emplacement que celui dans lequel ils se trouvaient avant la défaillance.  

 Si vous ne disposez pas d'une sauvegarde des systèmes de fichiers qui contient la bibliothèque de contenu, vous pouvez utiliser les options de restauration suivantes :  

-   **Importer un fichier de contenu préparé** : quand vous disposez d’une hiérarchie Configuration Manager, vous pouvez créer un fichier de contenu préparé avec tous les packages et applications d’un autre emplacement, puis importer le fichier de contenu préparé pour récupérer la bibliothèque de contenu sur le serveur de site.  

-   **Mettre à jour le contenu**: quand vous démarrez l’action de mise à jour de contenu pour un type de déploiement d’application ou de package, le contenu est copié de la source du package vers la bibliothèque de contenu. Les fichiers sources du package doivent être disponibles sur l'emplacement d'origine pour que cette action soit effectuée avec succès. Vous devez effectuer cette action pour chaque package et chaque application.  

#### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Récupérer les mises à jour logicielles personnalisées sur l'ordinateur qui exécute l'éditeur de mise à jour  
 Lorsque vous avez inclus les fichiers de base de données de l’éditeur de mise à jour dans votre plan de sauvegarde, vous pouvez récupérer les bases de données en cas de panne de l'ordinateur sur lequel l’éditeur de mise à jour s'exécute. Pour plus d'informations sur l'éditeur de mise à jour, voir [Éditeur de mise à jour System Center 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) dans la bibliothèque TechCenter de System Center.  

 Utilisez la procédure suivante pour restaurer la base de données de l'éditeur de mise à jour.  

###### <a name="to-restore-the-updates-publisher-2011-database"></a>Pour restaurer la base de données de l'éditeur de mise à jour 2011  

1.  Réinstallez l’éditeur de mise à jour sur l’ordinateur récupéré.  

2.  Copiez le fichier de base de données (Scupdb.sdf) depuis la destination de sauvegarde vers %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ sur l'ordinateur qui exécute l’éditeur de mise à jour.  

3.  Lorsque plusieurs utilisateurs exécutent l’éditeur de mise à jour sur l'ordinateur, vous devez copier chaque fichier de base de données vers l'emplacement du profil de l'utilisateur approprié.  

#### <a name="user-state-migration-data"></a>Données de migration de l'état utilisateur  
 Dans le cadre des propriétés du système de site du point de migration d'état, vous pouvez spécifier les dossiers qui conservent les données de migration de l'état utilisateur. Après avoir récupéré un serveur disposant d'un dossier qui conserve les données de migration d'état utilisateur, vous devez restaurer manuellement les données de migration d'état utilisateur vers les emplacements qu'elles occupaient avant la panne.  

#### <a name="regenerate-the-certificates-for-distribution-points"></a>Régénérer les certificats pour les points de distribution  
 Après la restauration d’un site, le fichier journal distmgr.log peut contenir l’entrée suivante pour un ou plusieurs points de distribution : **Échec de déchiffrage des données PFX du certificat**. Cette entrée indique le site ne peut pas déchiffrer les données de certificat du point de distribution. Pour résoudre ce problème, vous devez régénérer ou réimporter le certificat pour les points de distribution concernés. Ceci peut se faire en utilisant l’applet de commande PowerShell [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx).  

#### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Mettre à jour les certificats utilisés pour les points de distribution cloud  
 Configuration Manager requiert un certificat de gestion pour la communication entre le serveur de site et le point de distribution cloud. Suite à la récupération d'un site, vous devez mettre à jour les certificats des points de distribution cloud.  

####  <a name="a-namebkmkrecoversecondarysitea-recover-a-secondary-site"></a><a name="BKMK_RecoverSecondarySite"></a> Récupération d'un site secondaire  
 Configuration Manager ne prend pas en charge la sauvegarde de la base de données sur un site secondaire, mais prend en charge la récupération en réinstallant le site secondaire. La récupération de site secondaire est requise dans le cas de défaillance d'un site secondaire Configuration Manager. Vous pouvez récupérer un site secondaire à l'aide de l'action **Récupérer le site secondaire** à partir du nœud **Site** dans la console Configuration Manager. Contrairement à la récupération d'un site d'administration centrale ou d'un site principal, la récupération d'un site secondaire n'utilise pas de fichier de sauvegarde, mais réinstalle plutôt les fichiers du site secondaire sur l'ordinateur du site secondaire ayant échoué. Ensuite, les données du site secondaire sont réinitialisées avec les données du site principal parent. Pendant le processus de récupération, Configuration Manager vérifie si la bibliothèque de contenu existe bien sur l'ordinateur du site secondaire et si le contenu approprié est disponible. Le site secondaire utilisera la bibliothèque de contenu existante, si elle contient le contenu approprié. Sinon, pour récupérer la bibliothèque de contenu d'un site secondaire récupéré, vous devez redistribuer ou prédéfinir le contenu sur ce site récupéré. Lorsque vous disposez d'un point de distribution qui ne se trouve pas sur le site secondaire, vous n'avez pas à réinstaller le point de distribution lors d'une restauration du site secondaire. Après la restauration du site secondaire, le site se synchronise automatiquement avec le point de distribution.  

 Vous pouvez vérifier l'état de la récupération du site secondaire à l'aide de l'action **Afficher l'état d'installation** dans le nœud **Sites** de la console Configuration Manager.  

> [!IMPORTANT]  
>  Vous devez utiliser un ordinateur avec la même configuration que l'ordinateur en échec, par exemple, son nom de domaine complet, pour récupérer correctement le site secondaire. L'ordinateur doit également respecter toutes les conditions préalables de site secondaire et disposer des droits de sécurité appropriés configurés. Vous devez également utiliser le même chemin d'installation qui a été utilisé pour le site en échec.  

> [!IMPORTANT]  
>  Lors d'une restauration de site secondaire, Configuration Manager n'installe pas SQL Server Express s'il n'est pas installé sur l'ordinateur. Par conséquent, avant de récupérer un site secondaire, vous devez installer manuellement SQL Server Express ou SQL Server. Vous devez utiliser la même version de SQL Server et la même instance de SQL Server que vous avez utilisées pour la base de données de site secondaire avant la défaillance.  

##  <a name="a-namebkmksmswriterservicea-sms-writer-service"></a><a name="BKMK_SMSWriterService"></a> Service Enregistreur SMS  
 L'Enregistreur SMS est un service qui interagit avec le service de cliché instantané du volume (VSS, Volume Shadow copy Service) pendant le processus de sauvegarde. Le service Enregistreur SMS doit être en cours d'exécution pour mener à bien la sauvegarde de site Configuration Manager.  

### <a name="purpose"></a>Fonction  
 L'Enregistreur SMS s'enregistre auprès du service VSS et établit une liaison à ses interfaces et événements. Lorsque le service VSS diffuse des événements, ou s'il envoie une notification spécifique à l'Enregistreur SMS, ce dernier répond à la notification et entreprend les mesures appropriées. L’Enregistreur SMS lit le fichier de contrôle de sauvegarde (smsbkup.ctl), situé dans &lt;*chemin_installation_ConfigMgr*>\inboxes\smsbkup.box, puis détermine les fichiers et les données à sauvegarder. L'Enregistreur SMS génère des métadonnées, consistant de différents composants, en se basant sur ces informations ainsi que sur des données spécifiques à partir de la clé de Registre SMS et des sous-clés. Il envoie les métadonnées vers le service VSS lorsqu'elles sont demandées. Le service VSS envoie ensuite les métadonnées à l'application faisant la demande ; le Gestionnaire de sauvegarde Configuration Manager. sélectionne les données à sauvegarder et les envoie à l'Enregistreur SMS via le service VSS. L'Enregistreur SMS prend les mesures appropriées pour préparer la sauvegarde. Plus tard, lorsque le service VSS est prêt à prendre l'instantané, il envoie un événement ; l'Enregistreur SMS arrête tous les services Configuration Manager et s'assure que toutes les activités Configuration Manager sont figées pendant la création de l'instantané. Une fois le processus d'instantané terminé, l'Enregistreur SMS redémarre les services et les activités.  

 Le service Enregistreur SMS est installé automatiquement. Il doit être en cours d'exécution lorsque l'application VSS demande une sauvegarde ou une restauration.  

### <a name="writer-id"></a>ID du rédacteur  
 L’ID d’enregistreur pour l’Enregistreur SMS est le suivant : 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Autorisations  
 Le service Enregistreur SMS doit s'exécuter sous le compte système local.  

### <a name="volume-shadow-copy-service"></a>Service de cliché instantané du volume  
 Le service de cliché instantané du volume (VSS) est un ensemble d'API COM qui implémente une structure permettant de réaliser des sauvegardes de volumes en même temps que les applications sur un système continuent d'écrire dans les volumes. Le service VSS fournit une interface cohérente pour la coordination entre les applications de l'utilisateur qui mettent à jour des données sur le disque (le service Enregistreur SMS) et celles qui sauvegardent des applications (le service Gestionnaire de sauvegarde). Pour plus d'informations sur le service VSS, voir la rubrique [Volume Shadow Copy Service (Service de cliché instantané du volume)](http://go.microsoft.com/fwlink/p/?LinkId=241968) dans Windows Server TechCenter.  



<!--HONumber=Feb17_HO2-->


