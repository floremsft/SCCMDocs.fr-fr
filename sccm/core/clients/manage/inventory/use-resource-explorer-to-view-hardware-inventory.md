---
title: "Afficher l’inventaire matériel | Microsoft Docs | Explorateur de ressources"
description: "Utilisez l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 2cd138b3bbb437d84f0ff7c2aeef869518bd817d


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Comment utiliser l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’Explorateur de ressources de System Center Configuration Manager pour afficher des informations sur l’inventaire matériel collecté à partir de clients de votre hiérarchie.  

> [!NOTE]  
>  L'Explorateur de ressources n'affichera pas de données d'inventaire avant qu'un cycle d'inventaire matériel ait été exécuté sur le client auquel vous êtes connecté.  

 L'Explorateur de ressources de Configuration Manager contient les sections suivantes relatives à l'inventaire matériel :  

-   **Matériel** : contient l’inventaire matériel le plus récent collecté à partir de l’appareil client Configuration Manager spécifié. Vous pouvez consulter l'article en stock **état de la station de travail** pour découvrir l'heure et la date lorsque le périphérique de la dernière exécution de l'inventaire matériel.  

-   **Historique du matériel** : contient un historique des éléments d'inventaire qui ont été modifiés depuis le dernier inventaire matériel. Chaque élément de la liste contient un nœud **En cours** et un ou plusieurs nœuds de *<date\>*. Vous pouvez comparer les informations du nœud en cours à l'un des nœuds historiques pour découvrir les éléments qui ont été modifiés dans l'inventaire de matériel des ordinateurs client.  

    > [!NOTE]  
    >  Configuration Manager conserve l'historique de l'inventaire matériel pendant le nombre de jours que vous spécifiez dans la tâche de maintenance du site **Supprimer les historiques d'inventaire anciens**.  

> [!NOTE]  
>  Pour plus d’informations sur la façon d’afficher l’inventaire matériel des clients qui exécutent Linux et UNIX, consultez [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Comment exécuter l’Explorateur de ressources à partir de la console Configuration Manager  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Périphériques** ou ouvrez un regroupement qui affiche des périphériques.  

3.  Cliquez sur l'ordinateur contenant l'inventaire que vous souhaitez afficher, puis, dans l'onglet **Accueil** , dans le groupe **Périphériques** , cliquez sur **Démarrer** , puis sur **Explorateur de ressources**. La fenêtre **Explorateur de ressources** s'ouvre.  

4.  Vous pouvez cliquer avec le bouton droit sur un élément dans le volet droit de la fenêtre **Explorateur de ressources**, puis cliquer sur **Propriétés** pour ouvrir la boîte de dialogue **Propriétés** de *<nom_élément\>* pour visualiser les informations d’inventaire recueillies dans un format plus lisible.  

5.  Lorsque vous avez terminé, fermez la fenêtre **Explorateur de ressources** .  



<!--HONumber=Dec16_HO3-->


