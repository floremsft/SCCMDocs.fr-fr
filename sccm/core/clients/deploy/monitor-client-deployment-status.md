---
title: "Surveiller l’état de déploiement des clients | Microsoft Docs"
description: "Surveillez l’état de déploiement des clients dans System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
caps.latest.revision: "11"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3d9d02d8c56aea17e563112f92173c2b56781da6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-client-deployment-status-in-system-center-configuration-manager"></a>Guide pratique pour surveiller l’état de déploiement des clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le déploiement de clients sur votre site prend du temps et certaines installations ne réussissent pas dès la première fois. La console System Center Configuration Manager permet de garder un œil sur les déploiements de clients au sein d’un regroupement en signalant l’état de déploiement des clients en temps réel.  

> [!NOTE]  
>  Le moyen le plus efficace et le plus fiable de surveiller le déploiement des clients est d’utiliser la console Configuration Manager (comme décrit dans cet article). La section **État du client** de l’espace de travail **Analyse** dans la console indique l’état du déploiement des clients avec précision et en temps réel. Vous pouvez surveiller les déploiements de client avec d’autres outils, tels le Gestionnaire de serveur dans Windows Server ou System Center Operations Manager, mais vous risquez de recevoir des alarmes en relation avec l’activité normale d’installation de clients. En raison de la façon dont le programme d’installation client (CCMSetup.exe) s’exécute dans différents environnements, ces autres outils peuvent générer de faux avertissements ou alarmes ne reflétant pas fidèlement l’état de déploiement des clients.  

 Dans l’espace de travail **Analyse** de la console, vous pouvez surveiller les états suivants des déploiements de clients se produisant à l’intérieur d’un regroupement que vous spécifiez :  

-   conformité  

-   En cours  

-   Non conforme  

-   Échec  

-   Inconnu  

 Configuration Manager génère des rapports sur les déploiements de clients en production ou en pré-production. La console Configuration Manager fournit également un graphique illustrant les déploiements de clients ayant échoué au cours d’une période donnée, pour vous aider à déterminer si les actions que vous exécutez pour résoudre les problèmes de déploiements améliorent le taux de réussite des déploiements au fil du temps.  

## <a name="to-monitor-client-deployments"></a>Pour analyser les déploiements de clients  

-   Dans la console Configuration Manager, cliquez sur **Surveillance** > **État du client**.  

-   Cliquez sur **Déploiement des clients en production** ou **Déploiement des clients en préproduction**, selon la version du client que vous souhaitez analyser.  

-   Consulter les graphiques d’état du déploiement des clients et d’échec de déploiement des clients.  

-   Si vous souhaitez modifier l’étendue du rapport, cliquez sur **Parcourir...**, puis choisissez un autre regroupement.  

 Pour en savoir plus sur les déploiements de clients en préproduction, consultez [Comment tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).

 > [!NOTE]
 > L’état du déploiement sur les ordinateurs hébergeant des rôles de système de site dans un regroupement de préproduction peut être signalé comme **Non conforme**, même quand le client a été correctement déployé. Lors de la promotion du client en production, l’état du déploiement est correctement signalé.   

 Pour analyser l’état des clients déployés, consultez [Comment surveiller les clients dans System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md)  

 Vous pouvez utiliser des rapports Configuration Manager pour obtenir un complément d’informations sur l’état des clients de votre site. Pour plus d’informations sur la façon d’exécuter des rapports, consultez [Génération de rapports dans System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
