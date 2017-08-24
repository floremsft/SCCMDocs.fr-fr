---
title: Surveiller la migration | Microsoft Docs
description: "Apprenez à surveiller l’avancement et la réussite des tâches de migration à l’aide de la console Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 896807ec2c4be2835094a27add59d4cc09e93add
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>Planification de la surveillance de la migration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager vous permet de surveiller la migration dans la console Configuration Manager qui se connecte à la hiérarchie de destination. Dans la console Configuration Manager, dans l’espace de travail **Administration**, vous pouvez utiliser le nœud **Migration** pour surveiller l’avancement et la réussite des tâches de migration. Vous pouvez consulter les informations récapitulatives de chaque tâche de migration qui identifie les objets qui ont été migrés, ceux qui n'ont pas encore été migrés et le nombre d'objets qui ont été exclus de la migration. Elles contiennent également des informations sur les problèmes éventuels de migration.  

## <a name="view-migration-progress"></a>Afficher l'avancement de la migration  
 Pour afficher l'avancement d'une tâche de migration, optez pour l'une des actions suivantes :  

-   Dans l’espace de travail **Administration** de la console Configuration Manager, développez le nœud **Tâches de migration**, sélectionnez une tâche de migration, puis sélectionnez l’onglet **Objets dans la tâche**.  

-   Utilisez les fichiers journaux Configuration Manager pour vérifier l’avancement de la migration ou pour identifier les problèmes. Le gestionnaire de migration est le processus de Configuration Manager qui suit les actions de migration et les enregistre dans le fichier migmctrl.log dans le dossier **\&lt;Chemin_Installation\>\\LOGS** sur le serveur de site.  

    > [!NOTE]  
    >  Si une tâche de migration échoue, examinez les informations dans ce fichier dès que possible. Les entrées du journal de migration sont continuellement ajoutées au fichier et remplacent les anciennes. Si les entrées sont remplacées, vous risquez de ne pas pouvoir déterminer si les problèmes qui peuvent apparaître avec les objets migrés sont liés à la migration. L’activité de migration est consignée sur le site de niveau supérieur de la hiérarchie, quel que soit le site auquel la console Configuration Manager se connecte au moment où vous configurez la migration.  

-   Utilisez les rapports Configuration Manager. Configuration Manager propose plusieurs rapports intégrés pour la migration, que vous pouvez aussi modifier en fonction de vos besoins. Pour plus d’informations sur les rapports Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  
