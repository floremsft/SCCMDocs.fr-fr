---
title: "Tester les mises à niveau du client dans un regroupement de préproduction | Documents Microsoft"
description: "Testez les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager."
ms.custom: na
ms.date: 12/04/2016
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
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 17b36eae97272c408fce20e1f88812dafc984773
ms.openlocfilehash: bfc53760572e71814ebf0e38ea24c5c4684619ee


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez tester une nouvelle version du client Configuration Manager dans un regroupement de préproduction avant de mettre à niveau le reste du site vers cette version.  Quand vous procédez ainsi, seuls les appareils qui font partie du regroupement de test sont mis à niveau. Une fois que vous avez pu tester le client, vous pouvez le promouvoir, ce qui rend la nouvelle version du logiciel client disponible pour le reste du site.

> [!NOTE]
> Pour promouvoir un client de test en production, vous devez être connecté tant qu’utilisateur avec le rôle de sécurité **Administrateur complet** et une étendue de sécurité de **Tout**. Pour plus d’informations, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration). Vous devez également être connecté à un serveur connecté au site d’administration centrale ou à un site principal autonome du plus haut niveau.

 Il existe 3 étapes de base pour tester des clients en préproduction.  

1.  [Pour configurer des mises à jour automatiques du client pour utiliser un regroupement de préproduction](#BKMK_config) pour utiliser un regroupement de préproduction.  

2.  [Pour installer une mise à jour de Configuration Manager qui inclut une nouvelle version du client](#BKMK_install) qui inclut une nouvelle version du client. Lors de l’installation, vous spécifiez un regroupement de préproduction pour le nouveau logiciel client.  

3.  [Pour promouvoir le nouveau client en production](#BKMK_promote) après des tests réussis.  

> [!TIP]  
>  Si vous mettez à niveau votre infrastructure de serveurs à partir d’une version précédente de Configuration Manager \(comme Configuration Manager 2007 ou System Center 2012 Configuration Manager\), nous vous recommandons d’effectuer les mises à niveau des serveurs en incluant l’installation de toutes les mises à jour Current Branch. Ceci garantit que vous avez la dernière version du logiciel client avant la mise à niveau des clients Configuration Manager.  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> Pour configurer des mises à jour automatiques du client pour utiliser un regroupement de préproduction  

1. Configurez un regroupement contenant les ordinateurs sur lesquels vous voulez déployer le client de préproduction. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements](..\collections\create-collections.md).

> [!NOTE]
> N’incluez pas d’ordinateurs de groupe de travail dans les regroupements de préproduction. Les ordinateurs de groupe de travail ne peuvent pas utiliser l’authentification nécessaire pour permettre au point de distribution d’accéder au package du client de préproduction.   

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Configuration du site** > **Sites**, puis choisissez **Paramètres de hiérarchie**.  

     Sous l’onglet **Mise à niveau des clients** des **Propriétés des paramètres de hiérarchie**:  

    -   Sélectionnez **Mettre à niveau automatiquement tous les clients du regroupement de préproduction en utilisant un client de préproduction**.  

    -   Entrez le nom d’un regroupement à utiliser comme regroupement de préproduction.  


##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> Pour installer une mise à jour de Configuration Manager qui inclut une nouvelle version du client  

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Services cloud** > **Mises à jour et services**, sélectionnez une mise à jour avec l’indication **Disponible**, puis choisissez **Installer le pack de mise à jour**.  

     Pour plus d’informations sur l’installation des mises à jour, consultez [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Lors de l’installation de la mise à jour, dans la page **Options du client** de l’Assistant, sélectionnez **Tester dans le regroupement de préproduction**.  

3.  Déroulez le reste de l’Assistant et installez le pack de mise à jour.  

     Une fois l’Assistant terminé, les clients inclus dans le regroupement de préproduction commencent à déployer le client mis à jour. Vous pouvez surveiller le déploiement de clients mis à niveau en accédant à **Surveillance** > **État du client** > **Déploiement des clients en préproduction**. Pour plus d’informations, consultez [Comment surveiller l’état du déploiement des clients dans System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > L’état du déploiement sur les ordinateurs hébergeant des rôles de système de site dans un regroupement de préproduction peut être signalé comme **Non conforme**, même quand le client a été correctement déployé. Lors de la promotion du client en production, l’état du déploiement est correctement signalé.

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> Pour promouvoir le nouveau client en production  

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Services cloud** > **Mises à jour et maintenance**, puis choisissez **Promouvoir le client de préproduction**.

    > [!TIP]
    > Le bouton **Promouvoir le client de préproduction** est également disponible quand vous surveillez les déploiements de clients dans la console en utilisant **Surveillance** > **État du client** > **Déploiement des clients en préproduction**.

2.  Dans la boîte de dialogue, examinez les versions du client en production et préproduction, vérifiez que le regroupement de préproduction approprié est spécifié, puis cliquez sur **Promouvoir**. Dans la zone de confirmation, cliquez sur **Oui**.  

3.  Une fois la boîte de dialogue fermée, la version du client mise à jour remplace la version du client actuellement en cours d’utilisation dans votre hiérarchie. Vous pouvez ensuite mettre à niveau les clients pour l’ensemble du site. Pour plus d’informations, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  



<!--HONumber=Dec16_HO1-->


