---
title: Inventaire logiciel | System Center Configuration Manager
description: "Obtenez une présentation de l’inventaire logiciel dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8d664616e222119f7821a70a7c8f9cdbfca38538


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Présentation de l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’inventaire logiciel dans System Center Configuration Manager pour collecter des informations sur les fichiers qui figurent sur les appareils clients de votre organisation. En outre, l'inventaire logiciel peut regrouper les fichiers des appareils client et stocker ces derniers sur le serveur de site. L'inventaire logiciel est collecté quand le paramètre **Activer l'inventaire logiciel sur les clients** est activé dans les paramètres du client.  

 Une fois que l’inventaire logiciel est activé et que les clients exécutent un cycle d’inventaire logiciel, le client envoie les informations d’inventaire à un point de gestion dans le site du client. Le point de gestion transfère ensuite les informations d'inventaire au serveur de site Configuration Manager, qui les stocke dans la base de données du site. L'inventaire logiciel s'exécute sur les clients en fonction de la planification que vous spécifiez dans les paramètres du client.  

 Vous pouvez utiliser un certain nombre de méthodes pour afficher les données d’inventaire logiciel que Configuration Manager collecte. Ces référentiels sont notamment les suivants :  

-   Créer des requêtes qui retournent les appareils en fonction des fichiers que vous spécifiez qui sont détectés sur les appareils. Pour plus d’informations, consultez [Informations techniques de référence sur les requêtes pour System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

-   Créer des regroupements basés sur une requête et sur les fichiers que vous spécifiez qui sont détectés sur les appareils. Les appartenances à un regroupement basé sur une requête sont mises à jour automatiquement selon un calendrier. Vous pouvez utiliser des regroupements pour un certain nombre de tâches, telles que le déploiement de logiciels. Pour plus d’informations, consultez [Informations techniques de référence sur les regroupements pour System Center Configuration Manager](../../../../core/clients/manage/collections/collections-technical-reference.md).  

-   Exécuter des rapports qui affichent des détails spécifiques sur les fichiers sur les appareils de votre organisation. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

-   Utiliser l'Explorateur de ressources pour examiner les informations détaillées sur les fichiers qui ont été inventoriés et collectés sur les appareils client. Pour plus d’informations, consultez [Comment utiliser l’Explorateur de ressources pour afficher l’inventaire logiciel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

 Lorsqu'un inventaire logiciel s'exécute sur un appareil client, le premier rapport d'inventaire renvoyé est toujours un inventaire complet. Les rapports d'inventaire suivants contiennent uniquement les informations d'inventaire différentielles. Le serveur de site traite les informations d'inventaire différentielles selon l'ordre dans lequel il les reçoit. Si des informations d'inventaire différentielles d'un client manquent, le serveur de site rejette les autres informations d'inventaire différentielles et indique au client d'exécuter un cycle d'inventaire complet.  

 Configuration Manager assure une prise en charge limitée des ordinateurs à double démarrage. Configuration Manager peut détecter les ordinateurs à double démarrage, mais retourne uniquement les informations d’inventaire du système d’exploitation qui était actif au moment de l’inventaire.  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune  
 Vous pouvez collecter l’inventaire sur les applications installées sur des appareils mobiles. La liste des applications inventoriées varie selon que l'appareil appartient à l'entreprise ou à l'utilisateur. Pour les appareils personnels, les seules applications inventoriées sont celles qui sont gérées par Microsoft Intune.  

> [!NOTE]  
>  L’inventaire sur les applications installées sur les appareils mobiles est collecté dans le cadre du processus d’inventaire matériel dans Configuration Manager. Pour plus d’informations, consultez [Comment configurer l’inventaire matériel pour les appareils mobiles inscrits par Microsoft Intune et System Center Configuration Manager](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md).  

 Le tableau ci-dessous répertorie les applications inventoriées pour les appareils personnels ou d’entreprise.  

|Plate-forme|Pour les appareils personnels|Pour les appareils d’entreprise|  
|--------------|---------------------------------|--------------------------------|  
|Windows 8.1 (sans client Configuration Manager)|Uniquement les applications gérées|Uniquement les applications gérées|  
|Windows Phone 8|Uniquement les applications gérées|Uniquement les applications gérées|  
|Windows RT|Uniquement les applications gérées|Uniquement les applications gérées|  
|iOS|Uniquement les applications gérées|Toutes les applications installées sur l’appareil|  
|Android|Uniquement les applications gérées|Toutes les applications installées sur l’appareil|  



<!--HONumber=Nov16_HO1-->


