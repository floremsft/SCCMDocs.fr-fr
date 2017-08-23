---
title: "Softwareinventur für mobile Geräte, die bei Microsoft Intune registriert sind | Microsoft-Dokumentation"
description: "Softwareinventur für mobile Geräte, die bei Microsoft Intune registriert sind."
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
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Softwareinventur für mobile Geräte, die bei Microsoft Intune registriert sind

*Gilt für: System Center Configuration Manager (Current Branch)*

 Sie können Inventurdaten zu Apps sammeln, die auf mobilen Geräten installiert sind. Welche Apps inventarisiert werden, hängt davon ab, ob es sich um ein firmeneigenes Gerät handelt, oder ob das Gerät dem Benutzer gehört. Für persönliche Geräte werden nur von Microsoft Intune verwaltete Apps inventarisiert.  

> [!NOTE]  
>  Inventurdaten zu auf mobilen Geräten installierten Apps werden bei der [Hardwareinventur](mobile-device-hardware-inventory-hybrid.md) gesammelt.  

 Die folgende Liste umfasst die inventarisierten Apps für Geräte, die einem Benutzer gehören, und für Geräte, die dem Unternehmen gehören.  

|Plattform|Geräte, die einem Benutzer gehören|Geräte, die dem Unternehmen gehören|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (ohne Configuration Manager-Client)|Nur verwaltete Apps|Nur verwaltete Apps|
|Windows 8.1 (ohne Configuration Manager-Client)|Nur verwaltete Apps|Nur verwaltete Apps|  
|Windows Phone 8|Nur verwaltete Apps|Nur verwaltete Apps|  
|Windows RT|Nur verwaltete Apps|Nur verwaltete Apps|  
|iOS|Nur verwaltete Apps|Alle auf dem Gerät installierten Apps|  
|Android|Nur verwaltete Apps|Alle auf dem Gerät installierten Apps|  

Finden Sie unter [Einführung in die Softwareinventur](../../core/clients/manage/inventory/introduction-to-software-inventory.md) und [Konfigurieren der Softwareinventur ](../../core/clients/manage/inventory/configure-software-inventory.md) ausführliche Informationen zur Verwendung der Softwareinventur, um Dateiinformationen auf Clientgeräten zu sammeln.
