---
title: "Utiliser des fenêtres de maintenance | Microsoft Docs"
description: "Utilisez les regroupements et les fenêtres de maintenance pour gérer efficacement les clients dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: e59953f41422ee8f79ca054b5ccaccf41bb4e7af


---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Comment utiliser les fenêtres de maintenance dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les fenêtres de maintenance dans System Center Configuration Manager permettent aux utilisateurs administratifs de définir une période pendant laquelle diverses opérations Configuration Manager peuvent être effectuées sur les membres d’un regroupement d’appareils. Vous pouvez utiliser les fenêtres de maintenance afin de vous assurer que les modifications apportées à la configuration client seront effectuées pendant des périodes qui n'affectent pas la productivité de l'organisation.  

 Les opérations Configuration Manager suivantes prennent en charge les fenêtres de maintenance :  

-   Déploiements de logiciels  

-   Déploiements de mises à jour logicielles  

-   Déploiement et évaluation des paramètres de compatibilité  

-   Déploiements de système d'exploitation  

-   Déploiements de séquences de tâches  

 Les fenêtres de maintenance sont configurées pour un regroupement comportant une date de début, une heure de début et de fin et une périodicité. Chaque fenêtre de maintenance doit posséder une durée inférieure à 24 heures. Par défaut, les redémarrages de l'ordinateur dus à un déploiement ne sont pas autorisés à l'extérieur d'une fenêtre de maintenance, mais vous pouvez remplacer la valeur par défaut dans les paramètres pour chaque déploiement. Les fenêtres de maintenance affectent uniquement l’heure d’exécution du programme de déploiement ; les applications configurées pour un téléchargement et une exécution en local peuvent télécharger du contenu en dehors de la fenêtre de maintenance.  

 Quand un ordinateur client est membre d’un regroupement de périphériques pour lequel une fenêtre de maintenance est configurée, un programme de déploiement est exécuté uniquement si la durée d’exécution maximale autorisée ne dépasse pas la durée configurée pour la fenêtre de maintenance. Si le programme ne peut pas être exécuté, une alerte est générée et le déploiement est de nouveau exécuté lors de la fenêtre de maintenance planifiée suivante qui dispose de suffisamment de temps.  

## <a name="using-multiple-maintenance-windows"></a>Utilisation de fenêtres de maintenance multiples  
 Lorsqu'un ordinateur client est membre de plusieurs regroupements de périphériques pour lesquels des fenêtres de maintenance sont configurées, les règles suivantes s'appliquent :  

-   Si les fenêtres de maintenance ne se chevauchent pas, elles sont traitées comme deux fenêtres de maintenance indépendantes.  

-   Si les fenêtres de maintenance se chevauchent, elles sont traitées comme une seule fenêtre de maintenance englobant la période couverte par les deux fenêtres de maintenance. Par exemple, si deux fenêtres de maintenance d'une heure chacune se chevauchent de 30 minutes, la durée effective de la fenêtre de maintenance est de 90 minutes.  

 Quand un utilisateur lance l’installation d’une application à partir du Centre logiciel, l’application est installée immédiatement, quelle que soit la maintenance configurée.  

 Si le déploiement d’une application avec un objectif **Obligatoire** atteint son échéance d’installation pendant les heures creuses configurées par un utilisateur dans le Centre logiciel, l’application est installée.  

### <a name="how-to-configure-maintenance-windows"></a>Comment configurer les fenêtres de maintenance  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements d’appareils**.  

3.  Dans la liste **Regroupements de périphériques** , sélectionnez le regroupement pour lequel vous souhaitez configurer une fenêtre de maintenance.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans l’onglet **Fenêtres de maintenance** de la boîte de dialogue **Propriétés de &lt;nom_regroupement\>**, cliquez sur l’icône **Nouveau**.  

    > [!NOTE]  
    >  Vous ne pouvez pas créer de fenêtres de maintenance pour le regroupement **Tous les systèmes** .  

6.  Dans la boîte de dialogue **Calendrier &lt;nouveau\>**, spécifiez un nom, un calendrier et une périodicité pour la fenêtre de maintenance. Vous pouvez également activer l’option permettant d’appliquer la planification aux séquences de tâches uniquement.  

7.  À partir de la liste déroulante **Appliquer cette planification à** , indiquez si cette fenêtre de maintenance s’applique à tous les déploiements, uniquement aux mises à jour logicielles ou uniquement aux séquences de tâches.  

8.  Cliquez sur **OK** pour fermer la boîte de dialogue **Calendrier &lt;nouveau\>** et créer la fenêtre de maintenance.  

9. Fermez la boîte de dialogue **Propriétés de &lt;nom_regroupement\>**.  



<!--HONumber=Dec16_HO3-->


