---
title: Terminer la migration | System Center Configuration Manager
description: "Apprenez à terminer la migration vers une hiérarchie de destination System Center Configuration Manager une fois qu’une hiérarchie source ne contient plus de données."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 862a039ada302c9432fc86d68f5ba9aad360f69b


---
# <a name="planning-to-complete-migration-in-system-center-configuration-manager"></a>Planification de la fin de la migration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec System Center Configuration Manager, quand une hiérarchie source ne contient plus de données à migrer vers votre hiérarchie de destination, vous pouvez terminer le processus de migration. Pour cela, suivez les étapes ci-dessous :  

-   Vérifiez que les données dont vous avez besoin ont bien été migrées. Avant de terminer la migration à partir d'une hiérarchie source, vérifiez que vous avez bien migré toutes les ressources de la hiérarchie source dont vous pouvez avoir besoin dans la hiérarchie de destination. Pensez notamment aux données et aux clients.  

-   Arrêtez la collecte des données des sites source. Pour pouvoir terminer la migration à partir d'une hiérarchie source, vous devez au préalable arrêter la collecte des données des sites source.  

-   Nettoyez les données de migration. Après avoir arrêté la collecte des données des sites source d'une hiérarchie source, vous pouvez supprimer de la base de données de la hiérarchie de destination les données relatives au processus de migration et à la hiérarchie source.  

-   Retirez la hiérarchie source. Une fois que la migration à partir d'une hiérarchie source est terminée et que cette hiérarchie ne contient plus de ressources que vous gérez, vous pouvez retirer les sites de la hiérarchie source et supprimer l'infrastructure concernée de votre environnement. Pour plus d’informations sur le retrait de sites et de hiérarchies sources, consultez la documentation de cette version de Configuration Manager.  

Pour planifier l'achèvement d'une migration à partir d'une hiérarchie source par l'arrêt de la collecte de données et le nettoyage des données de migration, aidez-vous des sections ci-dessous :  

-   [Planifier l’arrêt de la collecte de données](#Plan_to_Stop_Data_Gath)  

-   [Planifier le nettoyage des données de migration](#Plan_to_clean_up)  

##  <a name="a-nameplantostopdatagatha-plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a> Planifier l’arrêt de la collecte de données  
 Avant de terminer la migration et de nettoyer les données de migration, vous devez arrêter la collecte des données de chaque site source dans la hiérarchie source. Pour arrêter la collecte de données de chaque site source, vous devez exécuter la commande **Arrêter la collecte de données** sur les sites source de niveau inférieur, puis répéter le processus au niveau de chaque site parent. Le site de niveau supérieur de la hiérarchie source doit être le dernier site sur lequel vous arrêtez la collecte des données. Vous devez arrêter la collecte de données sur chaque site enfant avant d'exécuter cette commande sur un site parent. En règle générale, vous arrêtez la collecte de données uniquement lorsque vous êtes prêt à exécuter le processus de migration.  

 Lorsque vous arrêtez la collecte des données d'un site source, les points de distribution partagés de ce site ne sont plus disponibles en tant qu'emplacements de contenu pour les clients de la hiérarchie de destination. Par conséquent, vérifiez que le contenu migré dont les clients ont besoin dans la hiérarchie de destination reste bien disponible. Pour cela, utilisez l'une des méthodes suivantes :  

-   Dans la hiérarchie de destination, distribuez le contenu à un point de distribution au moins.  

-   Avant d'arrêter la collecte de données à partir d'un site source, mettez à niveau ou réaffectez les points de distribution partagés ayant le contenu requis. Pour plus d’informations sur la mise à niveau ou la réaffectation de points de distribution partagés, consultez les sections correspondantes dans la rubrique [Planification d’une stratégie de migration de déploiement de contenu dans System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Après avoir arrêté la collecte de données à partir de chaque site source de la hiérarchie source, vous pouvez nettoyer les données de migration. Dans la console Configuration Manager, vous pouvez accéder à chaque tâche de migration qui a été exécutée ou qui est planifiée pour être exécutée, tant que vous n’avez pas nettoyé les données de migration.  

Pour plus d’informations sur les sites source et la collecte de données, consultez [Planification d’une stratégie de hiérarchie source dans System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="a-nameplantocleanupa-plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a> Planifier le nettoyage des données de migration  
 La dernière étape requise pour terminer la migration consiste à nettoyer les données de migration. Vous pouvez utiliser la commande **Nettoyer les données de migration** après avoir arrêté la collecte des données pour chaque site source de la hiérarchie source. Cette action facultative supprime de la base de données de la hiérarchie de destination l'ensemble des données relatives à la hiérarchie source actuelle.  

 Lors du nettoyage des données de migration, la plupart des données relatives à la migration sont supprimées de la base de données de la hiérarchie de destination. Cependant, les détails sur les objets migrés sont conservés. Grâce à ces détails, vous pouvez utiliser l'espace de travail **Migration** pour reconfigurer la hiérarchie source contenant les données migrées, soit pour reprendre la migration à partir de cette hiérarchie source, soit pour vérifier les objets et la propriété de site des objets précédemment migrés.  



<!--HONumber=Nov16_HO1-->


