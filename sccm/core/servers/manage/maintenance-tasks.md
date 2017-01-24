---
title: "Tâches de maintenance | Microsoft Docs"
description: "Comprenez quelles tâches de maintenance effectuer les sites et les hiérarchies Configuration Manager, et à quel moment les effectuer."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 46a24145d28111d7611f393f5806d0d7cc47ed71


---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Tâches de maintenance pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les sites et hiérarchies System Center Configuration Manager exigent une maintenance et une surveillance régulières pour fournir en permanence des services efficaces. Une maintenance régulière garantit que le matériel, les logiciels et la base de données Configuration Manager fonctionnent toujours correctement et efficacement. Lorsque les performances sont optimales, les risques de défaillance sont considérablement réduits.  

 Pour configurer des alertes et utiliser le système d’état pour surveiller l’intégrité de Configuration Manager, consultez [Utiliser des alertes et le système d’état pour System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Tâches de maintenance](#bkmk_MTs)  

##  <a name="a-namebkmkmtsa-maintenance-tasks"></a><a name="bkmk_MTs"></a> Tâches de maintenance  
 Une maintenance régulière est essentielle pour assurer le bon fonctionnement du site. Un journal des tâches de maintenance doit être tenu à jour pour y documenter les dates, les auteurs et tout commentaire de maintenance sur la tâche exécutée.  

### <a name="when-to-perform-common-maintenance-tasks"></a>À quel moment effectuer les tâches de maintenance courantes  
 Pour maintenir votre site, envisagez une maintenance régulière sur un plan quotidien, hebdomadaire, et pour certaines tâches, plus souvent. Une maintenance courante peut inclure les tâches de maintenance prédéfinies, ainsi que d'autres tâches, telles que la gestion des comptes pour conserver la conformité aux politiques de votre société.  

 Utilisez les informations suivantes comme guide pour planifier à quel moment effectuer les tâches de maintenance. Utilisez ces listes comme point de départ et ajoutez les tâches supplémentaires pouvant être nécessaires.  

**Tâches quotidiennes**   
Tâches de maintenance que vous pouvez envisager d'effectuer quotidiennement :  

-   Vérifier que les tâches de maintenance prédéfinies devant être exécutées quotidiennement s’exécutent correctement.  

-   Vérifier l’état de la base de données Configuration Manager  

-   Vérifier l’état du serveur de site.  

-   Vérifier les boîtes de réception de système de site Configuration Manager pour des backlogs de fichiers  

-   Vérifier l’état des systèmes de site.  

-   Vérifier les journaux d’événements du système d’exploitation sur les systèmes de site.  

-   Vérifier le journal des erreurs de SQL Server sur l’ordinateur de la base de données de site.  

-   Vérifier les performances du système.  

-   Vérifier les alertes Configuration Manager  

**Tâches hebdomadaires**   
Tâches de maintenance que vous pouvez envisager d'effectuer sur une base hebdomadaire :  

-   Vérifier que les tâches de maintenance prédéfinies devant être exécutées chaque semaine s’exécutent correctement.  

-   Supprimer les fichiers inutiles des systèmes de site.  

-   Créer et distribuer des rapports destinés aux utilisateurs finaux, si nécessaire.  

-   Sauvegarder les journaux des événements d’application, de sécurité et système, et supprimer les journaux inutiles.  

-   Vérifier la taille de la base de données du site et s’assurer que l’espace disque disponible sur le serveur de bases de données du site est suffisant pour contenir la base de données lorsque sa taille augmentera.  

-   Effectuer la maintenance de la base de données du site, conformément à votre plan de maintenance de base de données SQL Server.  

-   Vérifier l’espace disque disponible sur tous les systèmes de site.  

-   Exécuter les outils de défragmentation de disque sur tous les systèmes de site.  

**Tâches périodiques**   
Certaines tâches ne doivent pas nécessairement être exécutées selon un programme de maintenance quotidien ou hebdomadaire, mais elles sont importantes pour garantir l'intégrité générale des sites et la mise à jour des plans de sécurité et de récupération d'urgence. Les tâches de maintenance que vous pouvez envisager d'effectuer plus régulièrement que les tâches quotidiennes ou hebdomadaires sont les suivantes :  

-   Modifier les comptes et les mots de passe, si nécessaire, en fonction de votre plan de sécurité.  

-   Passer en revue le plan de maintenance pour vérifier si les tâches de maintenance prévues sont planifiées correctement et efficacement en fonction des paramètres de site configurés.  

-   Passer en revue la conception de la hiérarchie Configuration Manager et apporter toute modification nécessaire.  

-   Vérifier les performances du réseau pour vous assurer que les modifications effectuées n’affectent pas le fonctionnement des sites.  

-   Vérifier que les paramètres Active Directory affectant le fonctionnement des sites n’ont pas été modifiés. Par exemple, vérifiez que les sous-réseaux attribués aux sites Active Directory qui sont utilisés comme limites du site Configuration Manager n’ont pas changé.  

-   Examiner votre plan de récupération d’urgence et apporter toute modification nécessaire.  

-   Récupérer un site selon le plan de récupération d’urgence dans un environnement de test lab en utilisant une copie de sauvegarde de la dernière sauvegarde créée par la tâche de maintenance Serveur de site de sauvegarde.  

-   Examiner les erreurs liées au matériel ou vérifier si des mises à jour matérielles sont disponibles.  

-   Vérifier l’état d’intégrité global du site.  

###  <a name="a-namebkmkusemtsa-maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a> Garantir l’intégrité opérationnelle de votre base de données de site  
 Quand votre site et hiérarchie Configuration Manager effectuent les tâches que vous planifiez et configurez, les composants de site ajoutent continuellement des données à la base de données Configuration Manager. Les performances de la base de données et l'espace de stockage disponible dans la base de données diminuent au fur et à mesure que la quantité de données augmente. Vous pouvez configurer des tâches de maintenance de site pour supprimer les données anciennes dont vous n'avez plus besoin.  

 Configuration Manager propose des tâches de maintenance prédéfinies que vous pouvez utiliser pour garantir l’intégrité de la base de données Configuration Manager. Les tâches de maintenance ne sont pas toutes disponibles sur chaque site ; par défaut, certaines sont activées alors que d'autres ne le sont pas, et toutes prennent en charge une planification que vous pouvez configurer pour l'exécution.  

 La plupart des tâches de maintenance prédéfinies suppriment régulièrement les données périmées de la base de données Configuration Manager. La réduction de la taille de la base de données obtenue en supprimant les données inutiles permet d'améliorer les performances et l'intégrité de la base de données, ce qui améliore l'efficacité du site et de la hiérarchie. D'autres tâches, telles que **Reconstruire les index**, permettent de maintenir l'efficacité de la base de données, alors que d'autres encore, telles que **Serveur de site de sauvegarde** vous aident à préparer la reprise après sinistre.  

> [!IMPORTANT]  
>  Lorsque vous planifiez l'exécution d'une tâche qui supprime des données, examinez l'utilisation de ces données dans la hiérarchie. Quand une tâche qui supprime des données s’exécute sur un site, les informations sont supprimées de la base de données Configuration Manager, et cette modification est répliquée sur tous les sites dans la hiérarchie. Cela peut affecter d'autres tâches reposant sur ces données. Par exemple, sur le site d’administration centrale, vous pouvez configurer l’exécution de la détection une fois par mois pour identifier les ordinateurs sur lesquels le client n’est pas installé, et planifier l’installation du client Configuration Manager sur ces ordinateurs deux semaines, au plus tard, après leur détection. Cependant, sur un site de la hiérarchie, un administrateur configure l’exécution tous les sept jours de la tâche Supprimer les données de découverte anciennes, de sorte que sept jours après leur détection, ces ordinateurs sont supprimés de la base de données Configuration Manager. De retour sur le site d’administration centrale, vous préparez l’installation push du client Configuration Manager sur ces nouveaux ordinateurs au bout du dixième jour. Toutefois, étant donné que la tâche Supprimer les données de découverte anciennes a récemment été exécutée pour supprimer les données de sept jours ou plus, les ordinateurs récemment découverts ne sont plus disponibles dans la base de données.  

Après l’installation d’un site Configuration Manager, passez en revue les tâches de maintenance disponibles et activez celles nécessaire pour vos opérations. Vérifiez la planification par défaut de chaque tâche et, le cas échéant, modifiez-la pour configurer la tâche de maintenance selon votre hiérarchie et votre environnement. Bien que la planification par défaut de chaque tâche s’adapte à la plupart des environnements, surveillez les performances de vos sites et de votre base de données, et envisagez de reconfigurer ces tâches afin d’optimiser l’efficacité de vos déploiements. Envisagez d'examiner les performances du site et de la base de données, ainsi que de reconfigurer les tâches de maintenance et leur planification afin de maintenir l'efficacité.  

#### <a name="configure-maintenance-tasks"></a>Configurer les tâches de maintenance  
 Chaque site Configuration Manager prend en charge des tâches de maintenance qui contribuent à garantir le fonctionnement optimal de la base de données du site. Par défaut, plusieurs tâches de maintenance sont activées pour chaque site, et toutes les tâches prennent en charge des planifications indépendantes. Les tâches de maintenance sont configurées individuellement pour chaque site et s'appliquent à la base de données de ce site. Cependant, certaines tâches telles que **Supprimer les données de découverte anciennes**affectent les informations disponibles dans tous les sites de la hiérarchie.  

 La console Configuration Manager affiche uniquement les tâches de maintenance que vous pouvez configurer sur un site. Pour obtenir la liste complète des tâches de maintenance par type de site, consultez [Référence des tâches de maintenance pour System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Utilisez la procédure suivante pour vous aider à configurer les paramètres courants des tâches de maintenance.  

###### <a name="to-configure-maintenance-tasks-for-configuration-manager"></a>Pour configurer des tâches de maintenance pour Configuration Manager  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Site Configuration** >**Sites**.  

2.  Sélectionnez le site qui contient la tâche de maintenance que vous souhaitez configurer.  

3.  Sous l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Maintenance de site**, puis sélectionnez la tâche de maintenance que vous souhaitez configurer.  

    > [!TIP]  
    >  Seules les tâches disponibles sur le site sélectionné sont affichées.  

4.  Pour configurer la tâche, cliquez sur **Modifier**, assurez-vous que la case **Activer cette tâche** est cochée et planifiez l'exécution de la tâche. Si la tâche supprime également les données anciennes, configurez l'ancienneté des données qui seront supprimées de la base de données lors de l'exécution de la tâche. Cliquez sur **OK** pour fermer les **Propriétés**de la tâche.  

    > [!NOTE]  
    >  Pour **Supprimer les messages d'état anciens**, vous devez configurer l'ancienneté des données à supprimer lorsque vous configurez des règles de filtre d'état.  

5.  Pour activer ou désactiver la tâche sans modifier les propriétés de tâche, cliquez sur le bouton **Activer** ou **Désactiver** . L'étiquette du bouton change en fonction de la configuration actuelle de la tâche.  

6.  Lorsque vous avez terminé de configurer les tâches de maintenance, cliquez sur **OK** pour terminer la procédure.



<!--HONumber=Dec16_HO3-->


