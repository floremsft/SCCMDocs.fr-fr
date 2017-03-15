---
title: "Nouvelle version 1702 | Microsoft Docs"
description: "Obtenez des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1702 de System Center Configuration Manager."
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 473ba742bea74cbfdf8cab550244ccd522523718
ms.lasthandoff: 03/04/2017

---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>Nouveautés de la version 1702 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1702 de la version Current Branch de System Center Configuration Manager est une mise à jour dans la console des sites déjà installés qui exécutent la version 1606 ou 1610. Elle est également disponible sous la forme d’une version de ligne de base, que vous pouvez utiliser lors de l’installation d’un nouveau déploiement.

> [!TIP]  
> Pour installer un nouveau site, vous devez utiliser une version de base de Configuration Manager.  
>  Informations supplémentaires :    
>  -   [Installation de nouveaux sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Installation de mises à jour sur les sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Les sections suivantes fournissent des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1702 de Configuration Manager.  


## <a name="data-warehouse-service-point"></a>Point de service de l’entrepôt de données
Utilisez le point de service de l’entrepôt de données pour stocker des données d’historique à long terme et créer des rapports sur celles-ci pour votre déploiement de Configuration Manager.

L’entrepôt de données prend en charge jusqu’à 2 To de données, avec des horodatages pour le suivi des modifications. Pour stocker des données, vous utilisez des synchronisations automatisées entre la base de données du site Configuration Manager et la base de données de l’entrepôt de données. Ces informations sont ensuite accessibles à partir de votre point de Reporting Services.



Pour en savoir plus, consultez la section relative au [point de service de l’entrepôt de données](/sccm/core/servers/manage/data-warehouse).

