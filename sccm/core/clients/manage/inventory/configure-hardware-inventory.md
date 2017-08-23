---
title: Hardwareinventur konfigurieren | Microsoft-Dokumentation
description: "Richten Sie die Hardwareinventur für alle Clients oder für eine Sammlung in System Center Configuration Manager ein."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0baadb95ec8dbb945f1a611ebb95a03cec3199bd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für die Hardwareinventur konfiguriert. Sie gilt für alle Clients in der Hierarchie. Wenn Sie diese Einstellungen nur auf manche Clients anwenden möchten, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung und weisen diese einer Sammlung mit den Geräten zu, auf denen Sie die Hardwareinventur verwenden möchten. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Wenn ein Clientgerät Hardwareinventureinstellungen von mehreren Clienteinstellungssätzen erhält, werden die Hardwareinventurklassen aus jedem Einstellungssatz zusammengeführt, sobald vom Client eine Hardwareinventur gemeldet wird.  

### <a name="to-configure-hardware-inventory"></a>So konfigurieren Sie die Hardwareinventur  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Standardeinstellungen** die Option **Hardwareinventur** aus.  

6.  Konfigurieren Sie in der Liste **Geräteeinstellungen** die folgenden Optionen:  

    -   **Hardwareinventur auf Clients aktivieren**: Wählen Sie **Wahr** aus.  

    -   **Hardwareinventur-Zeitplan**: Klicken Sie auf **Zeitplan**, um das Intervall anzugeben, in dem Clients eine Hardwareinventur sammeln.  

7.  Konfigurieren Sie andere [Hardwareinventurclient-Einstellungen](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory), die Sie benötigen.  

Die Clientgeräte werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Abrufens von Richtlinien für einen einzelnen Client finden Sie unter [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
