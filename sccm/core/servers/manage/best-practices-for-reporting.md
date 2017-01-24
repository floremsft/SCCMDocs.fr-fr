---
title: "Bonnes pratiques pour la création de rapports | Microsoft Docs"
description: "Lire des conseils utiles sur l’utilisation de la fonction de rapport de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 759258999f3eaa810803a6a7f856f00fe7771a9e


---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Pratiques recommandées pour la création de rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les bonnes pratiques suivantes pour les rapports dans System Center Configuration Manager :  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Pour des performances optimales, installez le point de Reporting Services sur un serveur de système de site distant  
 Même si vous pouvez installer le point de Reporting Services sur le serveur de site ou sur un système de site distant, la performance est meilleure lorsque vous installez le point de Reporting Services sur un serveur de système de site distant.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Optimiser les requêtes de SQL Server Reporting Services  
 En règle générale, les délais de création de rapports sont liés à la durée nécessaire à l'exécution des requêtes et à la récupération des résultats. Si vous utilisez Microsoft SQL Server, les outils tels que l'analyseur de requêtes et le générateur de profils peuvent vous aider à optimiser des requêtes.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Planifier l'exécution du traitement des abonnements aux rapports en dehors des heures de bureau habituelles  
 Dès que possible, planifiez le traitement des abonnements aux rapports en dehors des heures de bureau habituelles pour minimiser le traitement par le processeur sur le serveur de base de données du site Configuration Manager. Cette pratique améliore également la disponibilité pour les demandes de rapport imprévues.  

## <a name="next-steps"></a>Étapes suivantes
[Configurer les rapports](configuring-reporting.md)



<!--HONumber=Dec16_HO3-->


