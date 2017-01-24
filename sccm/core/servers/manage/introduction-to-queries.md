---
title: "Présentation des requêtes | Microsoft Docs"
description: "Créez et exécutez des requêtes pour rechercher les objets dans une hiérarchie System Center Configuration Manager qui correspondent à vos critères de requête."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f84d518670c0ece3c08c890d2293335518f7f8e9


---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Présentation des requêtes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez créer et exécuter des requêtes pour rechercher les objets dans une hiérarchie System Center Configuration Manager qui correspondent à vos critères de requête. Ces objets incluent des éléments tels que des types spécifiques d'ordinateurs ou de groupes d'utilisateurs. Les requêtes peuvent renvoyer la plupart des types d’objets Configuration Manager, à savoir des sites, des regroupements, des applications et des données d’inventaire.  

 Quand vous créez une requête, vous devez spécifier au moins deux paramètres : où effectuer la recherche et ce que vous souhaitez rechercher. Par exemple, pour rechercher la quantité d’espace disponible sur le disque dur de tous les ordinateurs dans un site Configuration Manager, vous pouvez créer une requête pour rechercher la classe **Disque logique** et l’attribut **Espace libre (Mo)** pour déterminer l’espace disque disponible.  

 Après avoir créé une requête initiale, vous pouvez spécifier d'autres critères. Par exemple, vous pouvez spécifier que les résultats de la requête incluent uniquement les ordinateurs affectés à un site spécifié. Vous pouvez aussi modifier l'affichage des résultats pour visualiser les résultats dans un ordre qui est significatif pour vous. Par exemple, vous pouvez spécifier que les résultats doivent être classés par quantité d'espace disponible sur les disques durs en ordre croissant ou décroissant.  

 Lorsque vous créez une requête, elle est stockée par Configuration Manager et affichée dans le nœud **Requêtes** de l’espace de travail **Surveillance**. Dans cet emplacement, vous pouvez créer une requête et exécuter, mettre à jour ou gérer une requête existante.  

 Vous pouvez également importer une requête dans une règle de requête dans un regroupement Configuration Manager. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="see-also"></a>Voir aussi  
 [Informations techniques de référence sur les requêtes pour System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)



<!--HONumber=Dec16_HO3-->


