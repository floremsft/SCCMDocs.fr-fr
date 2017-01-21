---
title: Planifier la migration | Microsoft Docs
description: "Informez-vous sur les sites et les hiérarchies avant de migrer des données vers une hiérarchie de destination System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: ccc9973c07da9eca4bfacfb3bc7d1228a976c78b


---
# <a name="planning-for-migration-to-system-center-configuration-manager"></a>Planification de la migration vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de migrer des données vers une hiérarchie de destination System Center Configuration Manager, familiarisez-vous avec les sites et les hiérarchies dans Configuration Manager. Pour plus d’informations sur les sites et les hiérarchies, consultez [Principes de base de System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Pour pouvoir migrer des données à partir d’une hiérarchie source prise en charge, vous devez au préalable installer une hiérarchie System Center Configuration Manager, qui constituera votre hiérarchie de destination.  

 Une fois la hiérarchie de destination installée, avant de commencer à migrer les données, configurez les fonctionnalités de gestion et les fonctions que vous souhaitez utiliser dans votre hiérarchie de destination.  

 En outre, vous devrez peut-être anticiper un éventuel chevauchement entre la hiérarchie source et votre hiérarchie de destination. Supposons par exemple qu'une hiérarchie source est configurée pour utiliser les mêmes emplacements réseau ou les mêmes limites que votre hiérarchie de destination et que vous installez ensuite de nouveaux clients sur votre hiérarchie de destination et utilisez l'affectation de site automatique. Dans ce scénario, comme un client Configuration Manager nouvellement installé peut sélectionner un site à rejoindre dans n’importe quelle hiérarchie, le client risque d’être attribué de façon incorrecte à votre hiérarchie source. Par conséquent, au lieu d'utiliser la fonctionnalité d'attribution de site automatique, envisagez plutôt d'attribuer chaque nouveau client de la hiérarchie de destination à un site spécifique de cette hiérarchie.  

 Pour plus d’informations sur les attributions de site, consultez la section [Considérations sur l’attribution de sites aux clients](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) dans la rubrique [Interopérabilité entre les différentes versions de System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="planning-topics"></a>Rubriques relatives à la planification  
 Utilisez les rubriques suivantes pour planifier la migration d’une hiérarchie source prise en charge vers une hiérarchie de destination System Center Configuration Manager :  

-   [Prérequis de la migration dans System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Listes de vérification de l’administrateur pour la planification de la migration dans System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Déterminer s’il faut migrer des données vers System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planification d’une stratégie de hiérarchie source dans System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Listes de vérification de l’administrateur pour la planification de la migration dans System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planification d’une stratégie de migration de clients dans System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planification d’une stratégie de migration de déploiement de contenu dans System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planification de la migration d’objets Configuration Manager vers System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planification de la surveillance de l’activité de migration dans System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planification de la fin de la migration dans System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  



<!--HONumber=Dec16_HO3-->


