---
title: "FAQ sur les données de diagnostic | Microsoft Docs"
description: "Consultez les questions fréquemment posées sur les données de diagnostic et d’utilisation pour System Center Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 6cf291d79c1c5d9540f809fcb00e7ab48e0c3d3b
ms.openlocfilehash: 177a30a30f6b8579fa1956d28581d4f9d3a11838
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017


---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Questions fréquemment posées sur les données d’utilisation et de diagnostic pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Retrouvez ci-dessous les questions fréquemment posées sur les données de diagnostic et d’utilisation pour System Center Configuration Manager :  

###  <a name="bkmk_off"></a> Comment désactiver la télémétrie ?  
La télémétrie ne peut pas être désactivée. Toutefois, vous pouvez choisir le niveau des données de télémétrie collectées. Vous pouvez également utiliser un point de connexion de service en mode hors connexion pour gérer à quel moment les données de télémétrie sont envoyées.

La version Current Branch de Configuration Manager doit être mise à jour régulièrement pour pouvoir prendre en charge les nouvelles versions de Windows 10 et de Microsoft Intune. Microsoft exige au moins le niveau De base des données d’utilisation et de diagnostic pour pouvoir maintenir à jour le produit, améliorer l’expérience de mise à jour, ainsi qu’améliorer la qualité et la sécurité du produit.

###  <a name="bkmk_retention"></a> Quelle est la période de rétention des données ?  
 Les données d’utilisation et de diagnostic sont conservées un an.  

###  <a name="bkmk_update"></a> Des données d’utilisation et de diagnostic sont-elles envoyées lors de l’installation ou de la mise à jour du produit ?  
 Non. Des données d’utilisation et de diagnostic sont envoyées uniquement une fois le site installé et opérationnel.  

###  <a name="bkmk_frequency"></a> À quelle fréquence les données sont-elles envoyées ?  
 Les procédures stockées SQL s’exécutent tous les sept jours (à partir de la date d’installation du site). En mode en ligne, le point de connexion de service est configuré pour charger les données après l’exécution de requêtes. En mode hors connexion, l’administrateur utilise l’outil de connexion de service pour charger les données. (Notez que les données ne sont initialement pas disponibles pour une utilisation hors connexion avant sept jours après l’installation du site.)  

###  <a name="bkmk_network"></a> Les données peuvent-elles être utilisées pour former un mappage réseau ?  
 Comme indiqué dans la description des niveaux de collecte de données d’utilisation et de diagnostic pour System Center Configuration Manager, les détails du site incluent les informations de fuseau horaire de chaque site. Celles-ci peuvent fournir des insights concernant la géolocalisation large et la dispersion globale des sites dans une hiérarchie. Toutefois, aucun détail relatif au réseau, comme des adresses IP ou des informations géographiques plus détaillées, n’est collecté.
 - [Données de diagnostic pour 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Données de diagnostic pour 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Données de diagnostic pour 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Données de diagnostic pour 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> Pouvez-vous voir les données figurant dans des tables personnalisées ?  
 Non. Les données d’utilisation et de diagnostic sont collectées via des procédures stockées SQL appliquées à des tables de produit par défaut dans la base de données (précédées de **TEL_**). Dans le cadre de la requête de détection de schéma SQL, tous les noms de tables sont hachés à des fins de comparaison avec les valeurs par défaut connues. Cela peut permettre de déterminer l’existence de tables personnalisées dans la base de données (le schéma de base de données est étendu par rapport à la valeur par défaut), mais pas les données contenues dans ces tables.  

###  <a name="bkmk_databases"></a> Pouvez-vous voir les noms d’autres bases de données, ou des données dans d’autres bases de données ?  
 Non. Les procédures stockées pour la collecte des données sont limités à la base de données du site.  

## <a name="see-also"></a>Voir aussi  
 [Données d’utilisation et de diagnostic pour System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

