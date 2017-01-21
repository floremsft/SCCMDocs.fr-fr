---
title: "Mettre à jour et mettre hors service des applications | System Center Configuration Manager"
description: "Révisez, remplacez ou désinstallez des applications déployées à l’aide de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
caps.latest.revision: 9
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5eafaca3317f22b0e0b434d9161785cc90c701b7


---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>Mettre à jour et mettre hors service des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous finirez probablement par vouloir apporter des modifications à une application, en désinstaller une ou remplacer une application déjà déployée par une nouvelle. System Center Configuration Manager inclut ces fonctions pour vous aider dans ce but :  
  
-   **Réviser des applications** : quand vous apportez des modifications à un type d’application ou de déploiement, Configuration Manager conserve un historique de ces modifications. Vous pouvez revenir à tout moment à la version révisée précédente de l’application. Vous pouvez également afficher les propriétés de chaque révision, restaurer une révision précédente d'une application ou supprimer une ancienne révision.  

     Pour plus d’informations, consultez [Révisions d’applications](/sccm/apps/deploy-use/revise-and-supersede-applications#application-revisions).  

-   **Supersede applications** : vous permet de mettre à niveau ou de remplacer des applications existantes par le biais d’une relation de remplacement. Lorsque vous remplacez une application, vous pouvez spécifier un nouveau type de déploiement qui remplacera le type de déploiement de l'application remplacée. Vous pouvez aussi indiquer si vous souhaitez mettre à niveau ou désinstaller l'application remplacée avant l'installation de l'application de remplacement.  

     Pour plus d’informations, consultez [Remplacement d’applications](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence).  

-   **Désinstaller des applications** : Configuration Manager facilite la désinstallation d’une application. La désinstallation peut s’effectuer sans assistance, c’est-à-dire sans intervention de l’utilisateur final.  
  
Pour plus d’informations, consultez [Désinstaller des applications](../../apps/deploy-use/uninstall-applications.md).  
   



<!--HONumber=Nov16_HO1-->


