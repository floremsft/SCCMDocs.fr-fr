---
title: "Collecte des données de diagnostic | System Center Configuration Manager"
description: "Découvrez comment System Center Configuration Manager collecte les données de diagnostic et d’utilisation y afférentes."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 89292a11d003edd9e3a0eeb7fd367265a6b150b6


---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Comment les données d’utilisation et de diagnostic sont collectées pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour collecter les données de diagnostic et d’utilisation pour System Center Configuration Manager, chaque site principal exécute des requêtes SQL Server à une fréquence hebdomadaire. Dans une hiérarchie multisite, les données sont répliquées vers le site d’administration centrale.  

Sur le site de niveau supérieur d’une hiérarchie, le rôle système de site de point de connexion de service soumet ces informations quand il recherche des mises à jour. Le fonctionnement des transferts de données varie selon le mode du point de connexion de service :  

-   **En mode en ligne :** les données d’utilisation et de diagnostic sont envoyées automatiquement une fois par semaine du point de connexion de service au service cloud.  

-   **En mode hors connexion :** les données d’utilisation et de diagnostic sont transférées manuellement à l’aide de l’outil de connexion de service. Pour plus d'informations, voir [Utiliser l’outil de connexion de service pour System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Pour plus d’informations, voir [À propos du point de connexion de service dans System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  



<!--HONumber=Nov16_HO1-->


