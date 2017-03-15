---
title: "Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune | Microsoft Docs"
description: "Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.lasthandoff: 03/06/2017

---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez collecter un inventaire des applications installées sur des appareils mobiles. La liste des applications inventoriées varie selon que l'appareil appartient à l'entreprise ou à l'utilisateur. Pour les appareils personnels, les seules applications inventoriées sont celles qui sont gérées par Microsoft Intune.  

> [!NOTE]  
>  L’inventaire sur les applications installées sur les appareils mobiles est collecté dans le cadre du processus d’[inventaire matériel](mobile-device-hardware-inventory-hybrid.md).  

 Voici les applications inventoriées pour les appareils personnels ou d’entreprise.  

|Plate-forme|Pour les appareils personnels|Pour les appareils d’entreprise|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sans client Configuration Manager)|Uniquement les applications gérées|Uniquement les applications gérées|
|Windows 8.1 (sans client Configuration Manager)|Uniquement les applications gérées|Uniquement les applications gérées|  
|Windows Phone 8|Uniquement les applications gérées|Uniquement les applications gérées|  
|Windows RT|Uniquement les applications gérées|Uniquement les applications gérées|  
|iOS|Uniquement les applications gérées|Toutes les applications installées sur l’appareil|  
|Android|Uniquement les applications gérées|Toutes les applications installées sur l’appareil|  

Pour en savoir plus sur l’utilisation de l’inventaire logiciel pour collecter des informations sur les fichiers se trouvant sur les appareils des clients, voir [Présentation de l’inventaire logiciel](../../core/clients/manage/inventory/introduction-to-software-inventory.md) et [Comment configurer l’inventaire logiciel](../../core/clients/manage/inventory/configure-software-inventory.md).

