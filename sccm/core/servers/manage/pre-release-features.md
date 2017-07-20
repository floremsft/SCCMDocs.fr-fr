---
title: "Fonctionnalités en préversion| Microsoft Docs"
description: "Fonctionnalités en préversion dans System Center Configuration Manager"
ms.custom: na
ms.date: 6/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 988f8da0b221f8c0b470e7a0a8ed995356193f98
ms.contentlocale: fr-fr
ms.lasthandoff: 06/13/2017


---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Fonctionnalités en préversion dans System Center Configuration Manager
*S’applique à : System Center Configuration Manager (Current Branch)*

Les fonctionnalités de préversion sont des fonctions incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production. Ces fonctionnalités sont entièrement prises en charge mais sont toujours en cours de développement. Elles peuvent donc être modifiées jusqu'à ce qu’elles passent en préversion.

 Pour pouvoir sélectionner et utiliser ces fonctions, vous devez d’abord donner votre consentement via la console Configuration Manager.  

Le consentement est une action à effectuer une seule fois par hiérarchie ; elle ne peut pas être annulée. Tant que vous n’avez pas accepté de les utiliser, vous ne pouvez pas activer les fonctions en préversion incluses avec les mises à jour. Après avoir activé une fonctionnalité en préversion, vous ne pouvez pas la désactiver.

Pour donner votre consentement, accédez à la console, sélectionnez **Administration** > **Configuration du site** > **Sites**, puis choisissez **Paramètres de hiérarchie**. Sous l’onglet **Général**, choisissez **Accepter d’utiliser les fonctionnalités en préversion**.

 > [!NOTE]
 > Si vous avez activé des fonctionnalités en préversion à compter de la mise à jour 1602 avant d’installer une mise à jour ultérieure, ces fonctionnalités restent activées, même si vous ne donnez pas votre consentement pour utiliser les fonctionnalités en préversion.

Lorsque vous installez une mise à jour qui comprend des fonctionnalités de préversion, ces dernières sont affichées dans l’Assistant Maintenance et mises à jour, avec les fonctionnalités standard incluses dans la mise à jour :
  - **Si vous avez donné votre consentement :** vous pouvez activer les fonctionnalités à partir de l’Assistant Maintenance et mises à jour quand vous installez la mise à jour. Pour ce faire, sélectionnez les fonctionnalités de préversion, comme vous le feriez pour toute autre fonctionnalité.     

    Si vous le souhaitez, vous pouvez attendre pour activer une fonctionnalité en préversion par la suite à partir du nœud **Administration** > **Mises à jour et maintenance** > **Fonctionnalités** de la console. Dans le nœud **Fonctionnalités**, sélectionnez la fonctionnalité, puis choisissez **Activer**. Cette option est grisée jusqu’à ce que vous donniez votre consentement. (Avant la version 1702, les mises à jour et la maintenance s’effectuaient via le menu **Administration** > **Services cloud**.)
  -   **Si vous n’avez pas donné votre consentement :** lorsque vous installez une mise à jour, les fonctionnalités en préversion sont visibles dans l’Assistant Mises à jour et maintenance, mais elles sont grisées et ne peuvent pas être activées. Une fois la mise à jour installée, vous pouvez afficher ces fonctionnalités dans le nœud **Fonctionnalités**. Mais vous ne pouvez pas les activer tant que vous n’avez pas donné votre consentement dans **Paramètres de hiérarchie**.

Si vous avez donné votre consentement sur un site principal autonome, et si vous développez ensuite la hiérarchie en installant un nouveau site d’administration centrale, vous devez redonner votre consentement sur ce dernier.

 Quand vous activez une fonctionnalité en préversion, le Gestionnaire de hiérarchie de Configuration Manager (HMAN) doit traiter le changement avant que cette fonctionnalité ne soit disponible. Le traitement du changement est souvent immédiat, mais il peut prendre jusqu’à 30 minutes en fonction du cycle de traitement HMAN. Une fois le changement traité, vous devez redémarrer la console pour voir la nouvelle interface utilisateur associée à cette fonctionnalité.

**Les fonctionnalités en préversion disponibles sont les suivantes** :

 |Fonctionnalité          |Ajoutée en préversion | Ajoutée en version complète|  
|------------------|---------------------|---------------------|
| Gestion Device Guard avec Configuration Manager |  [Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application  |   [Version 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Point de service de l’entrepôt de données  |  [Version 1702](/sccm/core/servers/manage/data-warehouse) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Cache d’homologue pour la distribution de contenu aux clients |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Passerelle de gestion cloud |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Tableau de bord Sources de données du client |  [Version 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Connecteur Microsoft Operations Management Suite  | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Maintenance d’un regroupement prenant en charge les clusters (maintenance d’un groupe de serveurs)| [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Accès conditionnel pour les PC gérés par System Center Configuration Manager | [Version 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [Version 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |

