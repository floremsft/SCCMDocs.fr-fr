---
title: "Configurer l’inventaire matériel | Microsoft Docs"
description: "Configurez l’inventaire matériel pour l’ensemble des clients ou pour un regroupement dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: f39714e53e1b38c162e2c0418356d223432fdd87


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>Comment configurer l’inventaire matériel dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Exécutez les étapes suivantes pour configurer l’inventaire matériel System Center Configuration Manager pour votre site.  

 Cette procédure configure les paramètres client par défaut pour l’inventaire matériel et s’applique à tous les clients de votre hiérarchie. Si vous voulez que ces paramètres s’appliquent uniquement à certains clients, créez un paramètre client de périphérique personnalisé et affectez-le à un regroupement contenant les périphériques pour lesquels utiliser l’inventaire matériel. Pour plus d’informations sur la création de paramètres de d’appareil personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Si un périphérique client reçoit des paramètres d’inventaire matériel de la part de plusieurs ensembles de paramètres client, les classes d’inventaire matériel de chaque ensemble de paramètres sont alors fusionnées lors de l’inventaire matériel.  

### <a name="to-configure-hardware-inventory"></a>Pour configurer l'inventaire matériel  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Cliquez sur **Paramètres client par défaut**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres par défaut** , cliquez sur **Inventaire matériel**.  

6.  Dans la liste **Paramètres de périphérique** , configurez les éléments suivants :  

    -   **Activer l'inventaire matériel sur les clients** : dans la liste déroulante, sélectionnez **Vrai**.  

    -   **Calendrier de l’inventaire matériel** : indiquez l’intervalle auquel les clients collectent l’inventaire matériel. Utilisez la valeur par défaut, à savoir **7 jours** , ou cliquez sur **Calendrier** pour configurer un intervalle personnalisé.  

7.  Configurez tous les autres paramètres client dont vous avez besoin. Pour obtenir la liste des paramètres client d’inventaire matériel que vous pouvez configurer, consultez la section [Inventaire matériel](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) dans la rubrique [À propos des paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres par défaut** .  

 Les périphériques client sont configurés en utilisant ces paramètres lors du prochain téléchargement de stratégie client. Pour lancer la récupération de stratégie pour un client unique, consultez [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO3-->


