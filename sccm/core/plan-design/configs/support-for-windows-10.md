---
title: "Prise en charge de Windows 10 | Microsoft Docs"
description: "Découvrez les versions de Windows 10 qui sont prises en charge pour exécuter le client System Center Configuration Manager."
ms.custom: na
ms.date: 3/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: db258a09ce21627ffba37eb1f3d521c1ea0341ed
ms.openlocfilehash: 7df4bde6970b63262eee9e785d983addbeac0908
ms.lasthandoff: 04/13/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>Prise en charge de Windows 10 comme client de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Cette rubrique identifie les versions de Windows 10 que vous pouvez utiliser comme client avec les différentes versions de System Center Configuration Manager Current Branch.

- Elle complète [Systèmes d’exploitation pris en charge pour les clients et appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
- Si vous utilisez LTSB (Long Term Servicing Branch) de Configuration Manager, consultez [Configurations prises en charge pour Long Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).

Configuration Manager tente d’assurer la prise en charge de chaque nouvelle version de Windows 10 dès que possible après la publication de cette version de Windows. Étant donné que les produits ont des calendriers de développement et de publication distincts, la prise en charge assurée par Configuration Manager dépend du moment où les versions et les branches de chaque produit sont publiées.

Par exemple, une version de Configuration Manager sera supprimée de la matrice lorsque la [prise en charge de cette version](/sccm/core/servers/manage/current-branch-versions-supported) se termine. De même, la prise en charge de versions Windows 10 comme Enterprise 2015 LTSB or 1607 (CBB) sera supprimée de la matrice lorsque ces versions seront supprimées de la liste des configurations Configuration Manager prises en charge. Pour plus d’informations, consultez [Systèmes d’exploitation déconseillés](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems).



|Versions de Windows 10                    |Configuration Manager 1606          |Configuration Manager 1610          |    Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|Entreprise 2015 LTSB                   |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|1507 <br />(*voir éditions*)            |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|1511 (CB), (CBB)<br />(*voir éditions*) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|Entreprise 2016 LTSB                   |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|1607 (CB)    <br />Mise à jour anniversaire<br />(*voir éditions*)      |![Compatibilité descendante](media/blue_compat.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|1607 (CBB)    <br />Mise à jour anniversaire<br />(*voir éditions*)      |![Non pris en charge](media/Red_X.png)   |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|1703 (CB)    <br />Creators Update<br />(*voir éditions*)      |![Non pris en charge](media/Red_X.png)   |![Non pris en charge](media/Red_X.png) |![Compatibilité descendante](media/blue_compat.png) |



**Éditions :** Entreprise, Professionnel, Éducation, Professionnel Éducation   

|Clé|
|--|
|![Prise en charge](media/green_check.png) = **Prise en charge**  |
|![Pas de prise en charge](media/blue_compat.png)  = **Compatibilité descendante** : cela signifie que les fonctionnalités de gestion du client existantes (inventaire matériel, inventaire logiciel, mises à jour logicielles, etc.) doivent fonctionner avec la nouvelle build de Windows 10 Current Branch. Les mises en garde ou problèmes connus seront documentés. <br><br>Cette approche vous offre la possibilité de déployer et gérer de nouvelles builds de Windows 10 Current Branch dès le premier jour avec une prise en charge de la compatibilité des applications sans nécessiter une nouvelle version de mise à jour de Configuration Manager. |
|![Prise en charge](media/Red_X.png) = **Pas de prise en charge**|

