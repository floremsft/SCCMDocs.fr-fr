---
title: "Simuler des déploiements d’applications | System Center Configuration Manager"
description: "Évaluez la méthode de détection, les exigences et les dépendances d’un type de déploiement sans installer l’application."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a7d9267d35b58fdc6a01b869eb739e9c721db4a4


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simuler des déploiements d’applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les déploiements simulés si vous souhaitez tester l'applicabilité du déploiement d'une application sur des ordinateurs, sans installation ou désinstallation de l'application. Un déploiement simulé évalue la méthode de détection, les spécifications et les dépendances d'un type de déploiement, et génère un rapport contenant les résultats dans le nœud **Déploiements** de l'espace de travail **Surveillance** . Utilisez la procédure indiquée dans cette rubrique pour simuler un déploiement d’application dans System Center Configuration Manager.  

> [!NOTE]  
>  Vous ne pouvez pas utiliser les déploiements simulés pour les regroupements d'appareils mobiles.  
>   
>  Vous ne pouvez pas déployer une application dont l'objet de déploiement est **Désinstaller** si un déploiement simulé de la même application est actif.  
  
Utilisez la procédure suivante pour configurer un déploiement simulé d’application :
  
1.  Dans la console Configuration Manager, sélectionnez un des éléments suivants :  

    -   Un regroupement d'utilisateurs.  

    -   Un regroupement de périphériques.  

    -   Une application Configuration Manager.  

2.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Simuler un déploiement**.  

3.  Dans l' **Assistant Simuler un déploiement d'application**, spécifiez les informations suivantes :  

    -   **Application** : cliquez sur **Parcourir** , puis sélectionnez l’application pour laquelle vous voulez créer un déploiement simulé.  

    -   **Collection** : cliquez sur **Parcourir** , puis sélectionnez le regroupement à utiliser pour le déploiement simulé.  

    -   **Action** : dans la liste déroulante, indiquez si vous voulez simuler l’installation ou la désinstallation de l’application sélectionnée.  

    -   **Déployer automatiquement avec ou sans connexion de l’utilisateur** : si cette option est cochée, les clients évaluent le déploiement simulé, qu’ils soient connectés ou non.  

4.  Cliquez sur **Suivant**, consultez les informations figurant sur la page **Résumé** , puis terminez l'Assistant pour créer le déploiement d'application simulé.  

5.  Les applications simulées apparaissent dans le nœud **Déploiements** de l'espace de travail **Surveillance** et leur objet est **Simuler**. Pour plus d’informations sur la surveillance des déploiements d’applications, consultez [Surveiller des applications à partir de la console System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  



<!--HONumber=Nov16_HO1-->


