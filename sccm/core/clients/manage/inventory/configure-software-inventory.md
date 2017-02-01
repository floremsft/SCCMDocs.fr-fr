---
title: "Configurer l’inventaire logiciel | Microsoft Docs"
description: "Configurez l’inventaire logiciel, et excluez des dossiers de l’inventaire logiciel dans Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
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
ms.sourcegitcommit: dacfdf02f04c6bd731ca0fc11e5af371b409c8b4
ms.openlocfilehash: 1cee12d6f9c406e2438a3ed76674c3498fe9abbd


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Guide pratique pour configurer l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Cette procédure configure les paramètres par défaut du client pour l'inventaire logiciel et s'applique à tous les ordinateurs de votre hiérarchie. Si vous voulez appliquer ces paramètres à certains ordinateurs seulement, créez un paramètre de client d’appareil personnalisé et affectez-le à un regroupement qui contient les ordinateurs qui doivent utiliser l’inventaire logiciel. Pour plus d’informations sur la création de paramètres d’appareil personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

## <a name="to-configure-software-inventory"></a>Pour configurer l'inventaire logiciel  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client**  **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres par défaut**, choisissez **Inventaire logiciel**.  

6.  Dans la liste **Paramètres de périphérique** , configurez les valeurs suivantes :  

    -   **Activer l’inventaire logiciel sur les clients** : dans la liste déroulante, sélectionnez **Vrai**.  

    -   **Planifier l’inventaire logiciel et le regroupement de fichiers** : définit la fréquence de collecte de l’inventaire logiciel et des fichiers par les clients.   

7.  Configurez les paramètres client dont vous avez besoin. Pour obtenir la liste des paramètres client de l’inventaire logiciel que vous pouvez configurer, consultez la section [Inventaire logiciel](../../../../core/clients/deploy/about-client-settings.md#software-inventory) de la rubrique [À propos des paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

 Les ordinateurs clients sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour lancer la récupération de stratégie pour un client unique, consultez [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  


## <a name="to-exclude-folders-from-software-inventory"></a>Pour exclure des dossiers d'un inventaire logiciel  

1.  Dans Notepad.exe, créez un fichier vide intitulé **Skpswi.dat**.  

2.  Cliquez avec le bouton droit sur le fichier **Skpswi.dat** et cliquez sur **Propriétés**. Dans les propriétés du fichier Skpswi.dat, sélectionnez l'attribut **Masqué** .  

3.  Placez le fichier **Skpswi.dat** à la racine du disque dur ou de la structure de dossiers de chaque client que vous souhaitez exclure de l'inventaire logiciel.  

> [!NOTE]  
>  L'inventaire logiciel n'effectue pas un nouvel inventaire du lecteur de client à moins que le fichier ne soit supprimé du lecteur sur l'ordinateur client.


<!--HONumber=Jan17_HO1-->


