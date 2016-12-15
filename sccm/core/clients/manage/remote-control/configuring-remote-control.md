---
title: "Configurer le contrôle à distance | Documents Microsoft"
description: "Configurez le contrôle à distance dans System Center Configuration Manager."
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: dudeso
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
ms.sourcegitcommit: 88828e68bc4aff216e83807ea8288c7d42c60cbd
ms.openlocfilehash: cbfa9dc6cb37518c0a561700272cc882b0041350


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configuration du contrôle à distance dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Cette procédure décrit la configuration des paramètres client par défaut pour le contrôle à distance et s’applique à tous les ordinateurs de votre hiérarchie. Si vous voulez que ces paramètres s’appliquent uniquement à certains ordinateurs, créez un paramètre client de périphérique personnalisé et affectez-le à un regroupement contenant les ordinateurs à utiliser dans une session de contrôle à distance. Pour plus d’informations, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Pour utiliser l’Assistance à distance ou le Bureau à distance, vous devez les installer et les configurer sur l’ordinateur qui exécute la console Configuration Manager. Pour plus d’informations sur la procédure d’installation et de configuration de l’Assistance à distance ou du Bureau à distance, consultez votre documentation Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Pour activer le contrôle à distance et configurer les paramètres client  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client** > **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Dans la boîte de dialogue **Par défaut**, choisissez **Outils de contrôle à distance**.  

6.  Configurez les paramètres client du contrôle à distance, de l’Assistance à distance et du Bureau à distance. Pour obtenir la liste des paramètres client des outils de contrôle à distance que vous pouvez configurer, consultez [Outils de contrôle à distance](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Vous pouvez modifier le nom de l'entreprise qui apparaît dans la boîte de dialogue **Contrôle à distance ConfigMgr** en configurant une valeur pour **Nom d'organisation affiché dans le Centre logiciel** dans les paramètres client **Agent ordinateur** .  

 Les ordinateurs clients sont configurés avec ces paramètres la prochaine fois qu’ils téléchargent la stratégie du client. Pour lancer la récupération de stratégie pour un client unique, consultez [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO1-->


