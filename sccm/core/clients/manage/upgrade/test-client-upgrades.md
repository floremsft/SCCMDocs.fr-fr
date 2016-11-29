---
title: "Tester les mises à niveau du client dans un regroupement de préproduction | System Center Configuration Manager"
description: "Testez les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e648b94a475bda2b35d69ff0a8863d2e0d248fb


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour mettre à niveau le client Configuration Manager sur les ordinateurs et appareils Windows, vous pouvez tester une nouvelle version du client dans un regroupement de préproduction avant de mettre à niveau le reste du site.  Ce faisant, seuls les appareils qui font partie du regroupement de préproduction sont mis à niveau vers le nouveau client. Une fois que vous avez eu l’occasion de tester le client dans ce regroupement de préproduction, vous pouvez promouvoir le client, ce qui rend la nouvelle version du logiciel client disponible pour le reste du site.  

 Il existe 3 étapes de base pour tester des clients en préproduction  

1.  [Pour configurer des mises à jour automatiques du client pour utiliser un regroupement de préproduction](#BKMK_config) pour utiliser un regroupement de préproduction.  

2.  [Pour installer une mise à jour de Configuration Manager qui inclut une nouvelle version du client](#BKMK_install) qui inclut une nouvelle version du client. Pendant l’installation, vous spécifiez d’utiliser un regroupement de préproduction pour que le nouveau logiciel client.  

3.  [Pour promouvoir le nouveau client en production](#BKMK_promote) une fois que vous l’avez testé suffisamment en préproduction.  

> [!TIP]  
>  Si vous mettez à niveau votre infrastructure de serveur à partir d’une version précédente de Configuration Manager \(comme Configuration Manager 2007 ou System Center 2012 Configuration Manager\), nous vous recommandons d’effectuer les mises à niveau du serveur, dont l’installation de toutes les mises à jour de la version Current Branch, avant la mise à niveau des clients.   La dernière mise à jour de la version Current Branch contenant la dernière version du client, il est préférable d’effectuer les mises à niveau des clients après avoir installé toutes les mises à jour de Configuration Manager que vous souhaitez utiliser.  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> Pour configurer les mises à jour automatiques du client pour utiliser un regroupement de préproduction  

1. Configurez un regroupement contenant les ordinateurs sur lesquels vous voulez déployer le client de préproduction. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements](..\collections\create-collections.md).

> [!NOTE]
> N’incluez pas d’ordinateurs de groupe de travail dans les regroupements de préproduction. Les ordinateurs de groupe de travail ne peuvent pas utiliser l’authentification nécessaire pour permettre au point de distribution d’accéder au package du client de préproduction.   

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Configuration du site** > **Sites**, puis cliquez sur **Paramètres de hiérarchie**.  

     Sous l’onglet **Mise à niveau des clients** des **Propriétés des paramètres de hiérarchie**:  

    -   Sélectionnez **Mettre à niveau automatiquement tous les clients du regroupement de préproduction en utilisant un client de préproduction**.  

    -   Entrez le nom d’un regroupement à utiliser comme regroupement de préproduction.  

2.  Cliquez sur **OK** pour enregistrer les paramètres de mise à niveau du client.  

##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> Pour installer une mise à jour de Configuration Manager comprenant une nouvelle version du client  

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Services cloud** > **Mises à jour et services**, sélectionnez une mise à jour avec l’indication **Disponible**, puis cliquez sur **Installer le pack de mise à jour**.  

     Pour plus d’informations sur l’installation des mises à jour, consultez [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Pendant l’installation de la mise à jour, dans la page **Options du client** de l’Assistant, sélectionnez **Tester dans le regroupement de préproduction**, puis cliquez sur **Suivant**.  

3.  Déroulez le reste de l’Assistant et installez le pack de mise à jour.  

     Une fois l’Assistant terminé, les clients inclus dans le regroupement de préproduction commencent à déployer le client mis à jour. Vous pouvez surveiller le déploiement de clients mis à niveau en accédant à **Surveillance** > **État du client** > **Déploiement des clients en préproduction**. Pour plus d’informations, consultez [Comment surveiller l’état du déploiement des clients dans System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > L’état du déploiement sur les ordinateurs hébergeant des rôles de système de site dans un regroupement de préproduction peut être signalé comme **Non démarré** même quand le client a été correctement déployé. Lors de la promotion du client en production, l’état du déploiement est correctement signalé.

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> Pour promouvoir le nouveau client en production  

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Services cloud** > **Mises à jour et maintenance**, puis cliquez sur **Promouvoir le client de préproduction**.

    > [!TIP]
    > Le bouton **Promouvoir le client de préproduction** est également disponible quand vous surveillez les déploiements de clients dans la console en utilisant **Surveillance** > **État du client** > **Déploiement des clients en préproduction**.

2.  Dans la boîte de dialogue, examinez les versions du client en production et préproduction, vérifiez que le regroupement de préproduction approprié est spécifié, puis cliquez sur **Promouvoir**. Dans la zone de confirmation, cliquez sur **Oui**.  

3.  Une fois la boîte de dialogue fermée, la version du client mise à jour remplace la version du client actuellement en cours d’utilisation dans votre hiérarchie. Vous pouvez ensuite mettre à niveau les clients pour l’ensemble du site. Pour plus d’informations, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  



<!--HONumber=Nov16_HO1-->


