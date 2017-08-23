---
title: Einrichten des Intune-Abonnements | Microsoft-Dokumentation
description: "Richten Sie ein Intune-Abonnement ein, um die Lizenzierung für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager zu verfolgen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 5a81ec06e16992ae1c41b0fc98ebcd07386c5381
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Einrichten eines Microsoft Intune-Abonnements in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die lokale Verwaltung mobiler Geräte in System Center Configuration Manager setzt ein Microsoft Intune-Abonnement voraus, damit die Lizenzierung verfolgt werden kann. Der Intune-Dienst wird nicht zum Verwalten von Geräten oder zum Speichern von Verwaltungsinformationen verwendet. Für die lokale Verwaltung mobiler Geräte erfolgt die gesamte Geräteverwaltung über die Configuration Manager-Infrastruktur.  

> [!NOTE]  
> Ab Version 1610 unterstützt Configuration Manager die gleichzeitige Verwendung von Microsoft Intune und der lokalen Configuration Management-Infrastruktur zur gleichzeitigen Verwaltung mobiler Geräte.   

> [!TIP]  
>  Es wird empfohlen, dass Sie das Intune-Abonnement für die lokale Verwaltung mobiler Geräte einrichten, bevor Sie die erforderlichen Standortsystemrollen installieren, um die erforderliche Zeit zu minimieren, bis die neu installierten Standortsystemrollen funktionsfähig sind.  

##  <a name="sign-up-for-microsoft-intune"></a>Registrieren für Microsoft Intune  
 Intune ist erforderlich, damit die lokale Verwaltung mobiler Geräte funktionsfähig ist. [Registrieren](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) Sie sich einfach für ein Test- oder ein kostenpflichtiges Abonnement, und wechseln Sie dann zum nächsten Schritt, um das Abonnement Configuration Manager hinzuzufügen.  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Hinzufügen des Intune-Abonnements zu Configuration Manager  
 Damit das Abonnement Configuration Manager hinzugefügt wird, befolgen Sie einfach die gleichen grundlegenden Schritte wie beim Hinzufügen des Abonnements für die Verwaltung mobiler Geräte mit Intune. Lesen Sie die nachfolgenden Hinweise zu bestimmten Unterschieden, und verwenden Sie dann die Anleitungen unter [Konfigurieren Ihres Intune-Abonnements mit System Center Configuration Manager und Microsoft Intune](../deploy-use/configure-intune-subscription.md).  

> [!NOTE]  
>  Bedenken Sie beim Hinzufügen des Intune-Abonnements Folgendes:  
>   
>  -   Die im Assistenten zum Hinzufügen eines Microsoft Intune\-Abonnements angegebene Sammlung wird nicht für die Benutzerrechtdelegierung der lokalen Verwaltung mobiler Geräte verwendet. Sie dient lediglich der Verwaltung mobiler Geräte mit Intune. Allerdings müssen Sie an eine Sammlung angeben, damit der Assistent fortgesetzt werden kann.  
> -   Die im Assistenten angegebene Standortcodeeinstellung wird für die lokale Verwaltung mobiler Geräte ignoriert. Der verwendete Standortcode ist der Code, den Sie im Registrierungsprofil angeben, das den Benutzern die Berechtigung zum Registrieren von Geräten erteilt.  
> -   Aktivieren Sie nicht die Multi-Factor Authentication. Sie wird in der lokalen Verwaltung mobiler Geräte nicht unterstützt.  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>Konfigurieren des Intune-Abonnements zur lokalen Verwaltung mobiler Geräte  

1.  Klicken Sie in der Configuration Manager-Konsole mit der rechten Maustaste auf **Microsoft Intune-Abonnement**, und klicken Sie dann auf **Eigenschaften**.  

2.  Wählen Sie im Feld „On Premises Mobile Device Management“ (Lokale Verwaltung mobiler Geräte) eine der folgenden Aktionen aus:

  - Wenn Sie nur lokal verwaltete Geräte haben möchten, aktivieren Sie das Kontrollkästchen neben **Only manage devices on-premises** (Geräte nur lokal verwalten). Klicken Sie dann auf **OK**.  

      > [!NOTE]  
      >  Durch Aktivieren dieses Kontrollkästchens konfigurieren Sie das Intune-Abonnement so, dass alle Verwaltungsinformationen lokal vorgehalten und Daten nicht in der Cloud repliziert werden.  

    - Wenn Sie Geräte sowohl mit Intune als auch mit Configuration Manager lokal verwalten möchten, aktivieren Sie das Kontrollkästchen nicht.

3.  Wenn Sie beabsichtigen, Geräte mit Windows 10 Mobile zu verwalten, klicken Sie mit der rechten Maustaste auf **Microsoft Intune-Abonnement**, klicken Sie dann auf **Plattformen konfigurieren**, und klicken Sie anschließend auf  **Windows Phone**.  

4.  Aktivieren Sie das Kontrollkästchen neben **Windows Phone 8.1 und Windows 10 Mobile**, und klicken Sie dann auf **OK**.  

5.  Wenn Sie beabsichtigen, Desktopcomputer mit Windows 10 zu verwalten, klicken Sie mit der rechten Maustaste auf **Microsoft Intune-Abonnement**, klicken Sie dann auf **Plattformen konfigurieren**, und klicken Sie anschließend auf **Windows-Registrierung aktivieren**.  

6.  Aktivieren Sie das Kontrollkästchen neben **Windows-Registrierung aktivieren**, und klicken Sie dann auf **OK**.  
