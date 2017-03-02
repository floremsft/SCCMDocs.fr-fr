---
title: "Prise en charge de Windows 10 | Microsoft Docs"
description: "Découvrez les versions de Windows 10 qui sont prises en charge pour exécuter le client System Center Configuration Manager."
ms.custom: na
ms.date: 2/10/2017
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
ms.sourcegitcommit: 3702993d6cf9644d5aebaadd168749668fbcb62c
ms.openlocfilehash: 4b90384621dd20475ab9ea33ea062c24f5ecf5fa
ms.lasthandoff: 02/22/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>Prise en charge de Windows 10 comme client de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Cette rubrique identifie les versions de Windows 10 que vous pouvez utiliser comme client avec les différentes versions de System Center Configuration Manager Current Branch.

- Elle complète [Systèmes d’exploitation pris en charge pour les clients et appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
- Si vous utilisez LTSB (Long Term Servicing Branch) de Configuration Manager, consultez [Configurations prises en charge pour Long Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).

Configuration Manager tente d’assurer la prise en charge de chaque nouvelle version de Windows 10 dès que possible après la publication de cette version de Windows. Étant donné que les produits ont des calendriers de développement et de publication distincts, la prise en charge assurée par Configuration Manager dépend du moment où les versions et les branches de chaque produit sont publiées.  



|Versions de Windows 10 |Configuration Manager 1602|Configuration Manager 1606|Configuration Manager 1610|
|---------------------|-----|-----|-----|
|Entreprise 2015 LTSB |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|1507 <br />Entreprise, Professionnel | ![Pris en charge](media/green_check.png)| ![Pris en charge](media/green_check.png)|![Pris en charge](media/green_check.png) |
|1511 <br />Entreprise, Professionnel <br />(CB), (CBB) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |![Pris en charge](media/green_check.png) |
|Entreprise 2016 LTSB    |![Non pris en charge](media/Red_X.png) |![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png)|
|1607 <br />Entreprise, Professionnel<br /> (CB)    |![Non pris en charge](media/Red_X.png) |![Compatibilité descendante](media/blue_compat.png) |![Pris en charge](media/green_check.png) |
|1607 <br />Entreprise, Professionnel <br />(CBB)    |![Non pris en charge](media/Red_X.png) |![Compatibilité descendante](media/Red_X.png) |![Pris en charge](media/green_check.png) |


|Clé|
|--|
|![Prise en charge](media/green_check.png) = **Prise en charge**  |
|![Pas de prise en charge](media/blue_compat.png)  = **Compatibilité descendante** : cela signifie que les fonctionnalités de gestion du client existantes (inventaire matériel, inventaire logiciel, mises à jour logicielles, etc.) doivent fonctionner avec la nouvelle build de Windows 10 Current Branch. Les mises en garde ou problèmes connus seront documentés. <br><br>Cette approche vous offre la possibilité de déployer et gérer de nouvelles builds de Windows 10 Current Branch dès le premier jour avec une prise en charge de la compatibilité des applications sans nécessiter une nouvelle version de mise à jour de Configuration Manager. |
|![Prise en charge](media/Red_X.png) = **Pas de prise en charge**|

