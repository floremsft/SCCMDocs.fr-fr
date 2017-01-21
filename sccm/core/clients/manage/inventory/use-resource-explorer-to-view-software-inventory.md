---
title: "Afficher l’inventaire logiciel | Explorateur de ressources | System Center Configuration Manager"
description: "Utilisez l’Explorateur de ressources pour afficher l’inventaire logiciel dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b4ecb27cfb119ae80d1ed7d90d84c61a87b183c8


---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Comment utiliser l’Explorateur de ressources pour afficher l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’Explorateur de ressources de System Center Configuration Manager pour afficher des informations sur l’inventaire logiciel collecté auprès des ordinateurs de votre hiérarchie.  

> [!NOTE]  
>  L'Explorateur de ressources n'affiche pas de données d'inventaire tant qu'aucun cycle d'inventaire logiciel n'a été exécuté sur le client auquel vous vous connectez.  

 L’Explorateur de ressources de Configuration Manager contient les sections suivantes relatives à l’inventaire logiciel :  

-   **Logiciels** : cette section de l’Explorateur de ressources contient quatre sections :  

    -   **Fichiers collectés** : affiche des informations sur les fichiers collectés lors de l’inventaire logiciel.  

    -   **Détails du fichier** : affiche des informations sur les fichiers qui ont été inventoriés pendant l’inventaire logiciel et qui ne sont pas associés à un produit ou un fabricant.  

    -   **Dernière analyse logicielle** : affiche la date et l’heure de la dernière collecte d’inventaire logiciel et de fichiers exécutée sur l’ordinateur client.  

    -   **Détails du produit** : affiche des informations sur les produits logiciels qui ont été inventoriés par l’inventaire logiciel, regroupés par fabricant.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Pour exécuter l'Explorateur de ressources à partir de la console Configuration Manager  
 Procédez comme suit pour exécuter l’Explorateur de ressources dans Configuration Manager.  

#### <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Pour exécuter l'Explorateur de ressources à partir de la console Configuration Manager  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Périphériques** ou ouvrez un regroupement qui affiche des périphériques.  

3.  Cliquez sur l'ordinateur contenant l'inventaire que vous souhaitez afficher, puis, dans l'onglet **Accueil** , dans le groupe **Périphériques** , cliquez sur **Démarrer** , puis sur **Explorateur de ressources**. La fenêtre **Explorateur de ressources** s'ouvre.  

4.  Vous pouvez cliquer avec le bouton droit sur un élément dans le volet droit de la fenêtre Explorateur de ressources, puis cliquer sur **Propriétés** pour ouvrir la boîte de dialogue *Propriétés de ***<nom_élément\>** pour visualiser les informations d’inventaire recueillies dans un format plus lisible.  

5.  Lorsque vous avez terminé, fermez la fenêtre **Explorateur de ressources** .  



<!--HONumber=Nov16_HO1-->


