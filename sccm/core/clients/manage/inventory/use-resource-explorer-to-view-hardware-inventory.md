---
title: "Afficher l’inventaire matériel | Microsoft Docs | Explorateur de ressources"
description: "Utilisez l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 05c27c7aa36e0b4236867766dab36125c31467b3
ms.openlocfilehash: 6265ee70b70a715862b1651d2f3760bef096ee8a
ms.contentlocale: fr-fr
ms.lasthandoff: 01/03/2017


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Comment utiliser l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’Explorateur de ressources de System Center Configuration Manager pour afficher des informations sur l’inventaire matériel collecté à partir de clients de votre hiérarchie.  

> [!NOTE]  
>  L'Explorateur de ressources n'affichera pas de données d'inventaire avant qu'un cycle d'inventaire matériel ait été exécuté sur le client auquel vous êtes connecté.  

 L’Explorateur de ressources contient les sections suivantes relatives à l’inventaire matériel :  

-   **Matériel** : contient l’inventaire matériel le plus récent collecté à partir de l’appareil client indiqué.  **État de la station de travail** : indique l’heure et la date du dernier inventaire matériel effectué par l’appareil.  

-   **Historique du matériel** : contient un historique des éléments d’inventaire qui ont été modifiés depuis le dernier inventaire matériel. Chaque élément contient un nœud **En cours** et un ou plusieurs nœuds *<date\>*. Vous pouvez comparer les informations du nœud en cours à l’un des nœuds historiques pour découvrir les éléments qui ont été modifiés.  

    > [!NOTE]  
    >  Configuration Manager conserve l'historique de l'inventaire matériel pendant le nombre de jours que vous spécifiez dans la tâche de maintenance du site **Supprimer les historiques d'inventaire anciens**.  

> [!NOTE]  
>  Pour plus d’informations sur la façon d’afficher l’inventaire matériel des clients qui exécutent Linux et UNIX, consultez [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Comment exécuter l’Explorateur de ressources à partir de la console Configuration Manager  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Appareils**, ou ouvrez un regroupement qui affiche des appareils.  

3.  Choisissez l’ordinateur contenant l’inventaire que vous souhaitez afficher puis, dans l’onglet **Accueil**, dans le groupe **Appareils**, choisissez **Démarrer** >  **Explorateur de ressources**.   

4.  Cliquez avec le bouton droit sur un élément dans le volet droit de la fenêtre **Explorateur de ressources**, puis choisissez **Propriétés** pour ouvrir la boîte de dialogue **Propriétés de** *<nom_élément\>* et visualiser les informations d’inventaire recueillies sous un format plus lisible.  


