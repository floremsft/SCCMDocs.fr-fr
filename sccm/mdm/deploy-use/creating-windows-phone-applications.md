---
title: Erstellen von Windows Phone-Anwendungen | Microsoft Docs
description: "Erfahren Sie, was Sie beim Erstellen und Bereitstellen von Anwendungen für Windows Phone-Geräte berücksichtigen müssen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6cbf2389a72c0c384ef8e84a1755ac77b64bfc6d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Erstellen von Windows Phone-Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In einer System Center Configuration Manager-Anwendung ist mindestens ein Bereitstellungstyp enthalten, der die Installationsdateien und Informationen enthält, die zur Bereitstellung der Software für ein Gerät erforderlich sind. Bereitstellungstypen verfügen auch über Regeln, aus denen hervorgeht, wann und wie die Software bereitgestellt wird.  

 Es gibt die folgenden Möglichkeiten zum Erstellen von Anwendungen:  

-   Erstellen Sie die Anwendungen und Bereitstellungstypen durch Lesen der Installationsdateien der Anwendung automatisch.  

-   Erstellen Sie die Anwendung manuell, und fügen Sie Bereitstellungstypen später hinzu.  

-   Importieren Sie eine Anwendung aus einer Datei.  

Unter [Starten des Assistenten zum Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) finden Sie weitere Informationen zu erforderlichen Schritten zum Erstellen von Configuration Manager-Anwendungen und Bereitstellungstypen. Berücksichtigen Sie beim Erstellen und Bereitstellen von Apps für Windows Phone-Geräte auch Folgendes.  

## <a name="general-considerations"></a>Allgemeine Aspekte  
 Configuration Manager unterstützt die Bereitstellung folgender App-Dateitypen:  

|Gerätetyp|Unterstützte Dateitypen|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|
|Windows 10 Mobile|.xap, .appx, .appxbundle|

 Die folgenden Bereitstellungsaktionen werden unterstützt:  

|Gerätetyp|Unterstützte Aktionen|  
|-----------------|-----------------------|  
|Windows Phone 8, Windows Phone 8.1 und Windows 10 Mobile|Verfügbar, Erforderlich, Deinstallieren|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>Schritte zur Bereitstellung der neuesten Windows Phone-Unternehmensportal-App mit Ablösung  
 In der folgenden Tabelle finden Sie Schritte, Details und weitere Informationen zum Erstellen und Bereitstellen der aktuellen Windows Phone 8-Unternehmensportal-App.  

|Schritt|Weitere Informationen|  
|----------|----------------------|  
|**Schritt 1:** Beschaffen Sie sich die aktuelle Unternehmensportal-App.|Laden Sie die [Unternehmensportal-App von Windows Phone 8](http://go.microsoft.com/fwlink/?LinkId=268440)herunter.|  
|**Schritt 2:** Signieren Sie die Unternehmensportal-App mit Ihrem Symantec-Zertifikat.|Weitere Informationen zum Signieren der Unternehmensportal-App finden Sie unter [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune (Einrichten einer hybriden Geräteverwaltung für Windows Phone und Windows 10 Mobile mit System Center Configuration Manager und Microsoft Intune)](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Schritt 3:** Erstellen Sie eine neue Anwendung mit der aktuellen Version der Unternehmensportal-App, und geben Sie eine Ablösungsbeziehung an.|Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md) und [Überarbeiten und Ablösen von Anwendungen](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Schritt 4:** Fügen Sie die Anwendung dem Assistenten für Microsoft Intune-Abonnements hinzu.|Weitere Informationen finden Sie unter [Set up Windows Phone and Windows 10 Mobile hybrid device management with System Center Configuration Manager and Microsoft Intune (Einrichten einer hybriden Geräteverwaltung für Windows Phone und Windows 10 Mobile mit System Center Configuration Manager und Microsoft Intune)](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Schritt 5:** Löschen Sie die beim Hinzufügen der Unternehmensportal-App zum Assistenten für Microsoft Intune-Abonnements automatisch erstellte Bereitstellung.|Eine automatische Bereitstellung dieser App wurde durch das Microsoft Intune-Abonnement erstellt, da eine Ablösung von dieser Bereitstellung nicht unterstützt wird.|  
|**Schritt 6:** Erstellen Sie eine neue Bereitstellung der Anwendung. Aktivieren Sie im **Assistenten zum Bereitstellen von Software** auf der Seite **Bereitstellungseinstellungen** die Option **Automatically upgrade any superceded versions of this application** (Abgelöste Versionen dieser Anwendung automatisch upgraden).|Erstellen Sie mithilfe der Anwendung, die Sie mit der Ablösungsbeziehung erstellt haben, eine neue Bereitstellung mit Ablösung.|  
|**Schritt 7 (optional):** Die ablösenden Apps würden standardmäßig nach 7 Tagen auf den Geräten installiert werden. Wenn Sie die Unternehmensportal-App auf zuvor bereits angemeldeten Geräten schneller bereitstellen möchten, können Sie für die Einstellung **Erneute Auswertung für Bereitstellungen planen** einen niedrigeren Wert festlegen.<br /><br /> Wenn Sie einen Wert festlegen, der niedriger als die Standardeinstellung ist, kann dies jedoch die Leistung von Netzwerk und Clientcomputern beeinträchtigen.|keine zusätzlichen Informationen|  
