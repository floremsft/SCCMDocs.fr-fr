---
title: "Inventaire matériel | System Center Configuration Manager"
description: "Obtenez une présentation de l’inventaire matériel dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6a0addd31f6e8cd7ef91303cc664d9242c22e0f2


---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Présentation de l’inventaire matériel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’inventaire matériel dans System Center Configuration Manager pour recueillir des informations sur la configuration matérielle des appareils clients de votre organisation. Pour recueillir l'inventaire matériel, le paramètre **Activer l'inventaire matériel sur les clients** doit être activé dans les paramètres client.  

 Une fois l’inventaire matériel activé et un cycle d’inventaire matériel exécuté par le client, ce dernier envoie les informations d’inventaire qu’il a recueillies à un point de gestion du site du client. Le point de gestion transfère ensuite les informations d’inventaire au serveur de site Configuration Manager, qui les stocke dans la base de données du site. L'inventaire matériel s'exécute sur les clients en fonction de la planification que vous spécifiez dans les paramètres du client.  

 Vous pouvez utiliser plusieurs méthodes pour afficher les données d’inventaire matériel que Configuration Manager recueille. Ces référentiels sont notamment les suivants :  

-   Créer des requêtes qui retournent des appareils basés sur une configuration matérielle spécifique. Pour plus d’informations, consultez [Informations techniques de référence sur les requêtes pour System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

-   Créer des regroupements basés sur des requêtes qui reposent sur une configuration matérielle spécifique. Les appartenances à un regroupement basé sur une requête sont mises à jour automatiquement selon un calendrier. Vous pouvez utiliser des regroupements pour plusieurs tâches, notamment le déploiement de logiciel. Pour plus d’informations, consultez [Informations techniques de référence sur les regroupements pour System Center Configuration Manager](../../../../core/clients/manage/collections/collections-technical-reference.md).  

-   Exécuter des rapports qui affichent des détails spécifiques sur les configurations matérielles de votre organisation. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

-   Utilisez l'Explorateur de ressources pour afficher des informations détaillées sur l'inventaire matériel collecté à partir d’appareils clients. Pour plus d’informations, consultez [Guide pratique pour utiliser l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

 Lorsque l'inventaire matériel s'exécute sur un appareil client, les premières données d'inventaire renvoyées par le client sont toujours un inventaire complet. Les informations d'inventaire suivantes contiennent uniquement des informations d'inventaire différentielles. Le serveur de site traite les informations d'inventaire différentielles selon l'ordre dans lequel il les reçoit. S'il manque des informations d'inventaire différentielles pour un client, le serveur de site rejette les informations d'inventaire différentielles supplémentaires et indique au client d'exécuter un cycle d'inventaire complet.  

 Configuration Manager assure une prise en charge limitée des ordinateurs à double démarrage. Configuration Manager peut détecter les ordinateurs à double démarrage, mais retourne uniquement les informations d’inventaire du système d’exploitation qui était actif au moment de l’inventaire.  

> [!NOTE]  
>  Pour plus d’informations sur l’utilisation de l’inventaire matériel avec des clients qui exécutent Linux et UNIX, consultez [Inventaire matériel pour Linux et UNIX dans System Center Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Extension de l’inventaire matériel Configuration Manager  
 En plus de l’inventaire matériel intégré dans Configuration Manager, vous pouvez également utiliser une des méthodes suivantes pour étendre l’inventaire matériel en vue de collecter des informations supplémentaires :  

|Méthode|Description|  
|------------|-----------------|  
|Ajouter et supprimer des classes d’inventaire à partir de la console Configuration Manager|Dans Configuration Manager, vous pouvez activer, désactiver, ajouter et supprimer des classes d’inventaire pour l’inventaire matériel à partir de la console Configuration Manager.|  
|Fichiers NOIDMIF|Utilisez des fichiers NOIDMIF pour collecter des informations sur les appareils clients qui ne peuvent pas être inventoriés par Configuration Manager. Par exemple, vous pouvez souhaiter recueillir des informations numéros de périphérique actif qui existe uniquement en tant qu'étiquette sur le périphérique. L’inventaire NOIDMIF est automatiquement associé à l’appareil client à partir duquel il a été recueilli.|  
|Fichiers IDMIF|Utilisez des fichiers IDMIF pour collecter des informations sur les ressources de votre organisation qui ne sont pas associées à un client Configuration Manager, par exemple, les projecteurs, les photocopieurs et les imprimantes réseau.|  

 Pour plus d’informations sur l’utilisation de ces méthodes pour étendre l’inventaire matériel de Configuration Manager, consultez [Guide pratique pour configurer l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  



<!--HONumber=Nov16_HO1-->


