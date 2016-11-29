---
title: "Opérations de migration | System Center Configuration Manager"
description: "Créez et exécutez des tâches pour migrer les données et les clients vers System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9289dd8983846c27a3f5bd3ae999eed018ae4ccb


---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>Opérations de migration vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour la migration dans System Center Configuration Manager, une fois que vous avez correctement recueilli des données à partir d’un site source dans une hiérarchie source prise en charge, vous pouvez commencer à migrer les données et les clients. Utilisez les informations des sections suivantes pour créer et exécuter des tâches de migration afin de migrer des données, des clients, puis terminer le processus de migration.  

-   [Créer et modifier des tâches de migration](#Create_Edit_migration_Jobs)  

-   [Exécuter des tâches de migration](#Run_Migration_Jobs)  

-   [Mettre à niveau ou réattribuer un point de distribution partagé](#BKMK_ProcUpgrdSS)  

-   [Surveiller l’activité de migration dans l’espace de travail Migration](#Monitor_MIgration)  

-   [Migrer des clients](#BKMK_MigrateClients)  

-   [Terminer la migration](#Complete_Migration)  

##  <a name="a-namecreateeditmigrationjobsa-create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Créer et modifier des tâches de migration  
 Procédez comme suit pour créer des tâches de migration de données, modifier la liste d'exclusions pour les tâches de migration basée sur un regroupement, configurer des points de distribution partagés et modifier des planifications de tâches de migration.  

> [!NOTE]  
>  La procédure ci-dessous, qui permet de créer une tâche de migration basée sur des regroupements, s’applique uniquement aux hiérarchies sources qui exécutent une version prise en charge de Configuration Manager 2007. Le type de tâche de migration basée sur les regroupements n’est pas disponible lorsque vous migrez à partir d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager.  

#### <a name="to-create-a-migration-job-to-migrate-by-collections"></a>Pour créer une tâche de migration par regroupements  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Tâches de migration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une tâche de migration**.  

4.  Sur la page **Général** de l'Assistant Création de tâche de migration, configurez les éléments suivants, puis cliquez sur **OK**:  

    -   Spécifiez un nom pour la tâche de migration.  

    -   Dans la liste déroulante **Type de tâche** , sélectionnez **Migration du regroupement**.  

5.  Sur la page **Sélectionner des regroupements** , configurez les éléments suivants, puis cliquez sur **Suivant**:  

    -   Sélectionnez les regroupements que vous souhaitez migrer.  

    -   Si vous souhaitez migrer uniquement les regroupements et non les objets associés à ces regroupements, désactivez l'option **Migrer les objets qui sont associés aux regroupements spécifiés** . Si vous désactivez cette option, aucun objet associé n'est migré au cours de cette tâche et vous pouvez ignorer les étapes 6 et 7.  

6.  Sur la page **Sélectionner des objets** , désactivez tous les types d'objet ou les objets disponibles spécifiques que vous ne souhaitez pas migrer. Par défaut, tous les types d'objet associés et les objets disponibles sont sélectionnés. Cliquez ensuite sur **Suivant**.  

7.  Sur la page **Propriété du contenu** , attribuez la propriété du contenu de chacun des sites source de la liste à un site de la hiérarchie de destination, puis cliquez sur **Suivant**.  

8.  Sur la page **Étendue de sécurité** , sélectionnez une ou plusieurs étendues de sécurité d'administration basée sur un rôle à affecter aux objets à migrer dans cette tâche de migration, puis cliquez sur **Suivant**.  

9. Sur la page **Limitation au regroupement** , configurez un regroupement appartenant à la hiérarchie de destination, afin de limiter l'étendue de chacun des regroupements de la liste, puis cliquez sur **Suivant**. Si aucun regroupement ne figure dans la liste, cliquez sur **Suivant**.  

10. Dans la page **Remplacement d’un code de site**, affectez un code de site appartenant à la hiérarchie de destination, afin de remplacer le code de site Configuration Manager 2007 de chaque regroupement répertorié, puis cliquez sur **Suivant**. Si aucun regroupement ne figure dans la liste, cliquez sur **Suivant**.  

11. Sur la page **Consulter les informations** , cliquez sur **Enregistrer dans un fichier** pour enregistrer les informations affichées afin de les consulter ultérieurement. Lorsque vous êtes prêt à continuer, cliquez sur **Suivant**.  

12. Sur la page **Paramètres** , configurez la période d'exécution de la tâche de migration et tous les autres paramètres nécessaires à cette tâche de migration, puis cliquez sur **Suivant**.  

13. Confirmez les paramètres et mettez fin à l'Assistant.  

#### <a name="to-create-a-migration-job-to-migrate-by-objects"></a>Pour créer une tâche de migration par objets  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Tâches de migration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une tâche de migration**.  

4.  Sur la page **Général** de l'Assistant Création de tâche de migration, configurez les éléments suivants, puis cliquez sur **Suivant**:  

    -   Spécifiez un nom pour la tâche de migration.  

    -   Dans la liste déroulante **Type de tâche** , sélectionnez **Migration d'objet**.  

5.  Sur la page **Sélectionner des objets** , sélectionnez les types d'objet que vous souhaitez migrer. Par défaut, tous les objets disponibles sont sélectionnés pour chaque type d'objet que vous sélectionnez.  

6.  Sur la page **Propriété du contenu** , attribuez la propriété du contenu de chacun des sites source de la liste à un site de la hiérarchie de destination, puis cliquez sur **Suivant**. Si aucun site source ne figure dans la liste, cliquez sur **Suivant**.  

7.  Sur la page **Étendue de sécurité** , sélectionnez une ou plusieurs étendues de sécurité d'administration basée sur un rôle à affecter aux objets de cette tâche de migration, puis cliquez sur **Suivant**.  

8.  Sur la page **Consulter les informations** , cliquez sur **Enregistrer dans un fichier** pour enregistrer les informations affichées afin de les consulter ultérieurement. Lorsque vous êtes prêt à continuer, cliquez sur **Suivant**.  

9. Sur la page **Paramètres** , configurez la période d'exécution de la tâche de migration et tous les autres paramètres nécessaires à cette tâche de migration. Cliquez ensuite sur **Suivant**.  

10. Confirmez les paramètres et mettez fin à l'Assistant.  

#### <a name="to-create-a-migration-job-to-migrate-changed-objects"></a>Pour créer une tâche de migration pour migrer des objets modifiés  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Tâches de migration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une tâche de migration**.  

4.  Sur la page **Général** de l'Assistant Création de tâche de migration, configurez les éléments suivants, puis cliquez sur **Suivant**:  

    -   Spécifiez un nom pour la tâche de migration.  

    -   Dans la liste déroulante **Type de tâche** , sélectionnez **Objets modifiés après la migration**.  

5.  Sur la page **Sélectionner des objets** , sélectionnez les types d'objet que vous souhaitez migrer. Par défaut, tous les objets disponibles sont sélectionnés pour chaque type d'objet que vous sélectionnez.  

6.  Sur la page **Propriété du contenu** , attribuez la propriété du contenu de chacun des sites source de la liste à un site de la hiérarchie de destination, puis cliquez sur **Suivant**. Si aucun site source ne figure dans la liste, cliquez sur **Suivant**.  

7.  Sur la page **Étendue de sécurité** , sélectionnez une ou plusieurs étendues de sécurité d'administration basée sur un rôle à affecter aux objets de cette tâche de migration, puis cliquez sur **Suivant**.  

8.  Sur la page **Consulter les informations** , cliquez sur **Enregistrer dans un fichier** pour enregistrer les informations affichées afin de les consulter ultérieurement. Lorsque vous êtes prêt à continuer, cliquez sur **Suivant**.  

9. Sur la page **Paramètres** , configurez la période d'exécution de la tâche de migration et tous les autres paramètres nécessaires à cette tâche de migration. À la différence des autres types de tâches de migration, cette tâche de migration doit remplacer les objets migrés précédemment dans la base de données System Center Configuration Manager. Cliquez sur **Suivant**.  

10. Confirmez les paramètres, puis mettez fin à l'Assistant.  

###  <a name="a-namebkmkmodifyexclusionlista-to-modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a> Pour modifier la liste d’exclusions pour la migration  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Migration** pour accéder à la liste d'exclusions. Vous pouvez également accéder à la liste des exclusions à partir du nœud **Hiérarchie source** ou **Tâches de migration** .  

3.  Dans l'onglet **Accueil** , dans le groupe **Migration** , cliquez sur **Modifier la liste d'exclusion**.  

4.  Dans la boîte de dialogue **Modifier la liste d'exclusion** , sélectionnez l'objet exclu que vous souhaitez retirer de la liste d'exclusions, puis cliquez sur **Supprimer**.  

5.  Cliquez sur **OK** pour enregistrer les modifications et mettre fin à l'édition. Pour annuler les modifications en cours et restaurer tous les objets que vous avez supprimés, cliquez sur **Annuler**, puis sur **Non**. La suppression des objets est annulée et la boîte de dialogue **Modifier la liste d'exclusion** se ferme.  

#### <a name="to-share-distribution-points-from-the-source-hierarchy"></a>Pour partager des points de distribution à partir de la hiérarchie source  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, cliquez sur **Hiérarchie source**, puis sélectionnez le site source que vous souhaitez configurer.  

3.  Dans l' onglet **Accueil** , dans le groupe **Site source** , cliquez sur **Configurer**.  

4.  Dans la boîte de dialogue **Informations d'identification du site source** , sélectionnez **Activer le partage du point de distribution pour ce serveur de site source**, puis cliquez sur **OK**.  

5.  Une fois la collecte des données terminée, cliquez sur **Fermer**.  

#### <a name="to-change-the-schedule-of-a-migration-job"></a>Pour modifier la planification d'une tâche de migration  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Tâches de migration**.  

3.  Cliquez sur la tâche de migration que vous souhaitez modifier. Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Dans les propriétés de la tâche de migration, sélectionnez l'onglet **Paramètres** , modifiez l'heure d'exécution pour la tâche de migration, puis cliquez sur **OK**.  

##  <a name="a-namerunmigrationjobsa-run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Exécuter des tâches de migration  
 Pour exécuter une tâche de migration n'a pas encore commencé, suivez la procédure ci-dessous.  

#### <a name="to-run-migration-jobs"></a>Pour exécuter des tâches de migration  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Tâches de migration**.  

3.  Cliquez sur la tâche de migration que vous souhaitez exécuter. Dans l'onglet **Accueil** , dans le groupe **Tâche de migration** , cliquez sur **Démarrer**.  

4.  Cliquez sur **Oui** pour démarrer la tâche de migration maintenant.  

##  <a name="a-namebkmkprocupgrdssa-upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a> Mettre à niveau ou réattribuer un point de distribution partagé  
 Vous pouvez mettre à niveau un point de distribution pris en charge partagé à partir d’un site source Configuration Manager 2007 ou réaffecter un point de distribution pris en charge partagé à partir d’un site source System Center Configuration Manager, pour qu’ils deviennent des points de distribution dans la hiérarchie de destination.  

> [!IMPORTANT]  
>  Avant de mettre à niveau un point de distribution de branche Configuration Manager 2007, vous devez désinstaller le logiciel client Configuration Manager 2007 de l’ordinateur du point de distribution de branche. Si le logiciel client Configuration Manager 2007 est installé lorsque vous essayez de mettre à niveau le point de distribution, la mise à niveau échoue et le contenu précédemment déployé sur le point de distribution de branche est supprimé de l’ordinateur.  

> [!CAUTION]  
>  Lorsque vous mettez à niveau ou réaffectez un point de distribution partagé, le rôle de système de site et l'ordinateur du système de site du point de distribution sont supprimés du site source et ajoutés comme un point de distribution au site sélectionné dans la hiérarchie de destination.  

#### <a name="to-upgrade-or-reassign-a-shared-distribution-point"></a>Pour mettre à niveau ou réattribuer un point de distribution partagé  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Hiérarchie source**.  

3.  Sélectionnez le site propriétaire du point de distribution que vous souhaitez mettre à niveau, cliquez sur l'onglet **Points de distribution partagés** , puis sélectionnez le point de distribution éligible que vous souhaitez mettre à niveau ou réattribuer.  

4.  Sous l’onglet **Point de distribution** , dans le groupe **Point de distribution** , cliquez sur **Réaffecter**.  

5.  Dans l'Assistant Réaffectation du point de distribution partagé, spécifiez les paramètres comme si vous installiez un nouveau point de distribution pour la hiérarchie de destination, en ajoutant les configurations suivantes :  

    -   Dans la page **Conversion du contenu** , prenez connaissance des conseils relatifs à l'espace requis pour convertir le contenu existant. Puis, sur la page **Paramètres du lecteur** de l'Assistant, vérifiez que le lecteur de l'ordinateur du point de distribution sélectionné contient la quantité requise d'espace disque disponible.  

6.  Confirmez les paramètres, puis mettez fin à l'Assistant.  

##  <a name="a-namemonitormigrationa-monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Surveiller l’activité de migration dans l’espace de travail Migration  
 Pour surveiller la migration à l’aide de la console Configuration Manager, suivez la procédure ci-dessous.  

#### <a name="to-monitor-migration-activity-in-the-migration-workspace"></a>Pour surveiller l'activité de migration dans l'espace de travail Migration  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Tâches de migration**.  

3.  Cliquez sur la tâche de migration que vous souhaitez surveiller.  

4.  Affichez les détails et l'état de la tâche de migration sélectionnée sur les onglets **Synthèse** et **Objets de la tâche**.  

##  <a name="a-namebkmkmigrateclientsa-migrate-clients"></a><a name="BKMK_MigrateClients"></a> Migrer des clients  
 Après avoir migré des données pour des clients entre des hiérarchies, mais avant d'avoir terminé la migration, envisagez de migrer des clients vers la hiérarchie de destination. La migration de clients entre les hiérarchies implique la désinstallation du logiciel client Configuration Manager des ordinateurs qui sont affectés à la hiérarchie source, puis l’installation du logiciel client Configuration Manager à partir de la hiérarchie de destination. Lorsque vous installez le client à partir de la hiérarchie de destination, vous affectez également le client à un site principal de cette hiérarchie. Pour plus d’informations sur la migration de clients, consultez [Planification d’une stratégie de migration de clients dans System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="a-namecompletemigrationa-complete-migration"></a><a name="Complete_Migration"></a> Terminer la migration  
 Procédez comme suit pour terminer la migration à partir de la hiérarchie source.  

#### <a name="to-complete-migration"></a>Pour terminer la migration  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Migration**, puis cliquez sur **Hiérarchie source**.  

3.  Dans le cas d’une hiérarchie source Configuration Manager 2007, sélectionnez un site source qui se trouve au niveau inférieur de la hiérarchie source. Dans le cas d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, sélectionnez le site source disponible.  

4.  Dans l'onglet **Accueil** , dans le groupe **Nettoyer** , cliquez sur **Arrêter la collecte de données**.  

5.  Cliquez sur **Oui** pour confirmer l'action.  

6.  Pour une hiérarchie source Configuration Manager 2007, avant de passer à l’étape suivante, répétez les étapes 3, 4 et 5. Répétez ces étapes au niveau de chaque site de la hiérarchie, du bas vers le haut. Dans le cas d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, passez à l’étape suivante.  

7.  Dans l'onglet **Accueil** , dans le groupe **Nettoyer** , cliquez sur **Nettoyer les données de migration**.  

8.  Dans la boîte de dialogue **Nettoyer les données de migration** , dans la liste déroulante **Hiérarchie source** , sélectionnez le code de site et le serveur de site du site de niveau supérieur de la hiérarchie source, puis cliquez sur **OK**.  

9. Cliquez sur **Oui** pour terminer le processus de migration pour la hiérarchie source.  



<!--HONumber=Nov16_HO1-->


