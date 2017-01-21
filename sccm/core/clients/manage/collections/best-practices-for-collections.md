---
title: Bonnes pratiques pour les regroupements | System Center Configuration Manager
description: Obtenir les bonnes pratiques pour les regroupements dans System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8e22f353ba0803a3b1b4d387a8c00fdb98186bf5


---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Pratiques recommandées pour les regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les bonnes pratiques suivantes pour les regroupements dans System Center Configuration Manager.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>N'utilisez pas de mises à jour incrémentielles pour un grand nombre de regroupements.  
 Lorsque vous activez l'option **Utiliser des mises à jour incrémentielles pour ce regroupement** , cette configuration peut entraîner des retards d'évaluation si vous l'activez pour de nombreux regroupements. Le seuil s’élève à environ 200 regroupements dans votre hiérarchie. Le nombre exact dépend des facteurs suivants :  

-   Nombre total de regroupements  

-   Fréquence d'ajout et de modification de ressources dans la hiérarchie  

-   Nombre de clients dans la hiérarchie  

-   Complexité des règles d'appartenance de regroupement dans la hiérarchie  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Assurez-vous que les fenêtres de maintenance sont assez grandes pour déployer des mises à jour logicielles critiques  
 Vous pouvez configurer des fenêtres de maintenance pour les regroupements d'appareils afin de limiter les périodes où Configuration Manager peut installer des logiciels sur ces appareils. Si vous configurez une fenêtre de maintenance trop petite, le client peut ne pas installer les mises à jour logicielles critiques et se retrouver vulnérable à l'attaque qui aurait été contrée par la mise à jour logicielle.  



<!--HONumber=Nov16_HO1-->


