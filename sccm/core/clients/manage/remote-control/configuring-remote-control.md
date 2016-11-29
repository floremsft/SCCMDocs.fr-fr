---
title: "Configurer le contrôle à distance | System Center Configuration Manager"
description: "Configurez le contrôle à distance dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aea35afe970e20bc2b22f9ae3f413a3c735caae1


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configuration du contrôle à distance dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de pouvoir utiliser le contrôle à distance dans System Center Configuration Manager, vous devez effectuer les étapes de configuration suivantes.  

## <a name="how-to-enable-remote-control-and-configure-client-settings"></a>Comment activer le contrôle à distance et configurer les paramètres client  
 Cette procédure décrit la configuration des paramètres client par défaut pour le contrôle à distance et s’applique à tous les ordinateurs de votre hiérarchie. Si vous voulez que ces paramètres s’appliquent uniquement à certains ordinateurs, créez un paramètre client de périphérique personnalisé et affectez-le à un regroupement contenant les ordinateurs à utiliser dans une session de contrôle à distance. Pour plus d’informations sur la création de paramètres d’appareil personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Pour activer le contrôle à distance et configurer les paramètres client  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Cliquez sur **Paramètres client par défaut**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Par défaut**  , cliquez sur **Outils de contrôle à distance**.  

6.  Configurez les paramètres client de contrôle à distance, d’Assistance à distance et de Bureau à distance dont vous avez besoin. Pour obtenir la liste des paramètres client configurables dans les outils de contrôle à distance, consultez la section [Outils de contrôle à distance](../../../../core/clients/deploy/about-client-settings.md#BKMK_RemoteToolsDeviceSettings) dans la rubrique [À propos des paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

    > [!NOTE]  
    >  Vous pouvez modifier le nom de l'entreprise qui apparaît dans la boîte de dialogue **Contrôle à distance ConfigMgr** en configurant une valeur pour **Nom d'organisation affiché dans le Centre logiciel** dans les paramètres client **Agent ordinateur** .  

    > [!IMPORTANT]  
    >  Pour utiliser l’Assistance à distance ou le Bureau à distance, vous devez les installer et les configurer sur l’ordinateur qui exécute la console Configuration Manager. Pour plus d’informations sur la procédure d’installation et de configuration de l’Assistance à distance ou du Bureau à distance, consultez votre documentation Windows.  

7.  Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres par défaut** .  

 Les ordinateurs clients sont configurés avec ces paramètres la prochaine fois qu’ils téléchargent la stratégie client. Pour lancer la récupération de stratégie pour un client unique, consultez [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Nov16_HO1-->


