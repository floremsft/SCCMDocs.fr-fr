---
title: "Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune"
titleSuffix: Configuration Manager
description: "Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: "18"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c0a583de1a0b24bd31c0d55c1acb54f480bb4230
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
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
