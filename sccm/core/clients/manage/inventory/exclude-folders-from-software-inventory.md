---
title: "Exclure des dossiers de l’inventaire logiciel | Documents Microsoft"
description: "Excluez des dossiers de l’inventaire logiciel dans System Center Configuration Manager."
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6d1aabbde576f01de920468fd3ef372bd23be9df
ms.openlocfilehash: 7850b69cdccb0e897ee71b75255004bdc8d0ae97


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>Comment exclure des dossiers de l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Cette procédure configure les paramètres par défaut du client pour l'inventaire logiciel et s'applique à tous les ordinateurs de votre hiérarchie. Si vous voulez appliquer ces paramètres à certains ordinateurs seulement, créez un paramètre de client d’appareil personnalisé et affectez-le à un regroupement qui contient les ordinateurs qui doivent utiliser l’inventaire logiciel. Pour plus d’informations sur la création de paramètres d’appareil personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

### <a name="to-configure-software-inventory"></a>Pour configurer l'inventaire logiciel  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client**  **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres par défaut**, choisissez **Inventaire logiciel**.  

6.  Dans la liste **Paramètres de périphérique** , configurez les valeurs suivantes :  

    -   **Activer l’inventaire logiciel sur les clients** : dans la liste déroulante, sélectionnez **Vrai**.  

    -   **Planifier l’inventaire logiciel et le regroupement de fichiers** : définit la fréquence de collecte de l’inventaire logiciel et des fichiers par les clients.   

7.  Configurez les paramètres client dont vous avez besoin. Pour obtenir la liste des paramètres client de l’inventaire logiciel que vous pouvez configurer, consultez la section [Inventaire logiciel](../../../../core/clients/deploy/about-client-settings.md#software-inventory) de la rubrique [À propos des paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

 Les ordinateurs clients sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour lancer la récupération de stratégie pour un client unique, consultez [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO3-->


