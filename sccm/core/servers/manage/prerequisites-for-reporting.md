---
title: "Prérequis pour la création de rapports | Microsoft Docs"
description: "Comprenez les diverses dépendances qui ont un impact sur l’utilisation des rapports dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 5
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: ae750188b0258122d8561b163a5ecd85c4179f18


---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Configuration requise pour la création de rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La création de rapports dans System Center Configuration Manager comporte des dépendances externes et des dépendances au sein du produit.  

## <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  
 Le tableau suivant répertorie les dépendances externes pour la création de rapports.  

|Configuration requise|Plus d'informations|  
|------------------|----------------------|  
|SQL Server Reporting Services|Pour pouvoir utiliser des rapports dans Configuration Manager, vous devez installer et configurer SQL Server Reporting Services.<br /><br /> Pour plus d'informations sur la planification et le déploiement de Reporting Services dans votre environnement, reportez-vous à la section [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) de la documentation en ligne de SQL Server 2008.|  
|Dépendances de rôle de système de site pour les ordinateurs qui exécutent le point de Reporting Services.|[Configurations prises en charge pour System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dépendances internes à Configuration Manager  
 Le tableau suivant répertorie les dépendances pour la création de rapports dans Configuration Manager.  

|Configuration requise|Plus d'informations|  
|------------------|----------------------|  
|Point de Reporting Services|Vous devez configurer le rôle système de site du point de Reporting Services pour pouvoir utiliser la création de rapports dans Configuration Manager. Pour plus d’informations sur l’installation et la configuration d’un point Reporting Services, consultez [Configuration de la création de rapports dans Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versions de SQL Server prises en charge par le point de Reporting Services  
 La base de données Reporting Services peut être installée sur l'instance par défaut ou sur une instance nommée d'une installation 64 bits de SQL Server. L'instance SQL Server peut se trouver au même emplacement que le serveur du système de site ou sur un ordinateur distant.  

 Le tableau ci-dessous indique quelles versions de SQL Server sont prises en charge par le point de Reporting Services.  

|Version SQL Server|Point de Reporting Services|  
|------------------------|------------------------------|  
|SQL Server 2008 SP2 avec au minimum la mise à jour cumulative 9<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|?|  
|SQL Server 2008 SP3 avec au minimum la mise à jour cumulative 4<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|?|  
|SQL Server 2008 R2 avec SP1 et au minimum la mise à jour cumulative 6<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|?|  
|SQL Server 2008 R2 avec SP2<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|?|  
|SQL Server Express 2008 R2 avec SP1 et au minimum la mise à jour cumulative 4|Non pris en charge|  
|SQL Server Express 2008 R2 avec SP2|Non pris en charge|  
|SQL Server 2012 avec au minimum la mise à jour cumulative 2<br /><br /> -   Standard<br />-   Enterprise|?|  
|SQL Server 2012 avec SP1 et aucune mise à jour cumulative minimum<br /><br /> -   Standard<br />-   Enterprise|?|  
|SQL Server 2014<br /><br /> -   Standard<br />-   Enterprise|?|  

## <a name="next-steps"></a>Étapes suivantes
[Opérations et maintenance pour les rapports](operations-and-maintenance-for-reporting.md)



<!--HONumber=Dec16_HO3-->


