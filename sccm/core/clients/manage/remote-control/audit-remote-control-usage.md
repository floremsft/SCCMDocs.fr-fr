---
title: "Auditer l’utilisation du contrôle à distance | System Center Configuration Manager"
description: "Auditer l’utilisation du contrôle à distance dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1a23f37cfc67edb6ed097adb7e58342c9929a8fc


---
# <a name="how-to-audit-remote-control-usage-in-system-center-configuration-manager"></a>Comment auditer l’utilisation du contrôle à distance dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser les rapports System Center Configuration Manager pour afficher les informations d’audit du contrôle à distance.  

 Pour plus d’informations sur la configuration des rapports dans Configuration Manager, consultez [Rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

 Les deux rapports suivants sont disponibles avec la catégorie **Messages d'état - Audit**:  

-   **Contrôle à distance - Tous les ordinateurs contrôlés à distance par un utilisateur spécifique** : affiche un résumé de l’activité de contrôle à distance initiée par un utilisateur spécifique.  

-   **Contrôle à distance - Toutes les informations de contrôle à distance** : affiche un résumé des messages d'état concernant le contrôle à distance des ordinateurs clients.  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>Pour exécuter le rapport Contrôle à distance - Tous les ordinateurs contrôlés à distance par un utilisateur spécifique  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports**, puis cliquez sur **Rapports**.  

3.  Dans le nœud **Rapports** , cliquez sur la colonne **Catégorie** pour trier les rapports, ce qui vous permettra de trouver plus rapidement les rapports dans la catégorie **Messages d'état - Audit**.  

4.  Sélectionnez le rapport **Contrôle à distance - Tous les ordinateurs contrôlés à distance par un utilisateur spécifique**, puis, sous l’onglet **Accueil** , dans **Groupe de rapports**, cliquez sur **Exécuter**.  

5.  Dans la liste **Nom d’utilisateur** de **Contrôle à distance - Tous les ordinateurs contrôlés à distance par un utilisateur spécifique**, indiquez l’utilisateur pour lequel vous voulez afficher des informations d’audit, puis cliquez sur **Afficher le rapport**.  

6.  Une fois que vous avez terminé de consulter les données du rapport, fermez la fenêtre du rapport.  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>Pour exécuter le rapport Contrôle à distance - Toutes les informations de contrôle à distance  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports**, puis cliquez sur **Rapports**.  

3.  Dans le nœud **Rapports** , cliquez sur la colonne **Catégorie** pour trier les rapports, ce qui vous permettra de trouver plus rapidement les rapports dans la catégorie **Messages d'état - Audit**.  

4.  Sélectionnez le rapport **Contrôle à distance - Toutes les informations de contrôle à distance**, puis, sous l’onglet **Accueil** , dans **Groupe de rapports**, cliquez sur **Exécuter** pour ouvrir la fenêtre **Contrôle à distance - Toutes les informations de contrôle à distance** .  

5.  Une fois que vous avez terminé de consulter les données du rapport, fermez la fenêtre du rapport.  



<!--HONumber=Nov16_HO1-->


