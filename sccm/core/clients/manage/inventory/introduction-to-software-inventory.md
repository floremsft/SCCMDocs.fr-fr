---
title: "Inventaire logiciel | Microsoft Docs"
description: "Obtenez une présentation de l’inventaire logiciel dans System Center Configuration Manager."
ms.custom: na
ms.date: 12/26/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: c9956dd4ef94a1b109d761e44e42f512c42eb8d2


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Présentation de l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’inventaire logiciel pour collecter des informations sur les fichiers présents sur les appareils clients. L’inventaire logiciel peut aussi collecter des fichiers auprès des appareils clients et les stocker sur le serveur de site. L’inventaire logiciel est collecté quand vous choisissez le paramètre **Activer l’inventaire logiciel sur les clients** dans les paramètres du client, où vous pouvez aussi planifier l’opération.  

Une fois que l’inventaire logiciel est activé et que les clients exécutent un cycle d’inventaire logiciel, le client envoie les informations à un point de gestion dans le site du client. Le point de gestion transfère ensuite les informations d’inventaire au serveur de site Configuration Manager, qui les stocke dans la base de données du site.   

 Voici comment afficher les données de l’inventaire logiciel :  

-   [Créez des requêtes](../../../../core/servers/manage/queries-technical-reference.md) qui retournent les appareils avec des fichiers spécifiés.   

-   Créez des [regroupements basés sur une requête](../../../../core/clients/manage/collections/introduction-to-collections.md) qui incluent les appareils avec des fichiers spécifiés.   

-   [Exécutez des rapports](../../../../core/servers/manage/reporting.md) qui fournissent des détails sur les fichiers présents sur les appareils. 

-   Utiliser l’[Explorateur de ressources](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) pour examiner les informations détaillées sur les fichiers qui ont été inventoriés et collectés sur les appareils clients.   

 Quand un inventaire logiciel s’exécute sur un appareil client, le premier rapport d’inventaire est un inventaire complet. Les rapports d’inventaire suivants contiennent seulement des informations d’inventaire différentielles. Le serveur de site traite les informations différentielles selon l’ordre dans lequel il les reçoit. S’il manque des informations différentielles pour un client, le serveur de site rejette les informations différentielles suivantes et indique au client d’exécuter un inventaire complet.  

 Configuration Manager peut détecter les ordinateurs à double démarrage, mais retourne uniquement les informations d’inventaire du système d’exploitation qui était actif au moment de l’inventaire.  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune  
 Vous pouvez collecter un inventaire des applications installées sur des appareils mobiles. La liste des applications inventoriées varie selon que l'appareil appartient à l'entreprise ou à l'utilisateur. Pour les appareils personnels, les seules applications inventoriées sont celles qui sont gérées par Microsoft Intune.  

> [!NOTE]  
>  L’inventaire sur les applications installées sur les appareils mobiles est collecté dans le cadre du processus d’[inventaire matériel](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md).  

 Voici les applications inventoriées pour les appareils personnels ou d’entreprise.  

|Plate-forme|Pour les appareils personnels|Pour les appareils d’entreprise|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sans client Configuration Manager)|Uniquement les applications gérées|Uniquement les applications gérées| 
|Windows 8.1 (sans client Configuration Manager)|Uniquement les applications gérées|Uniquement les applications gérées|  
|Windows Phone 8|Uniquement les applications gérées|Uniquement les applications gérées|  
|Windows RT|Uniquement les applications gérées|Uniquement les applications gérées|  
|iOS|Uniquement les applications gérées|Toutes les applications installées sur l’appareil|  
|Android|Uniquement les applications gérées|Toutes les applications installées sur l’appareil|  





<!--HONumber=Dec16_HO5-->


