---
title: Erstellen von iOS-Anwendungen | Microsoft Docs
description: "Was Sie beim Erstellen und Bereitstellen von Apps für iOS-Geräte berücksichtigen müssen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 349fcf335e7faddbcbd2ffe0ece7e711465f28df
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Erstellen von iOS-Apps mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In einer System Center Configuration Manager-Anwendung ist mindestens ein Bereitstellungstyp enthalten, der die Installationsdateien und Informationen enthält, die zur Bereitstellung der Software für ein Gerät erforderlich sind. Bereitstellungstypen verfügen auch über Regeln, aus denen hervorgeht, wann und wie die Software bereitgestellt wird.  

 Es gibt die folgenden Möglichkeiten zum Erstellen von Anwendungen:  

-   Erstellen Sie die Anwendungen und Bereitstellungstypen durch Lesen der Installationsdateien der Anwendung automatisch.  

-   Erstellen Sie die Anwendung manuell, und fügen Sie Bereitstellungstypen später hinzu.  

-   Importieren Sie eine Anwendung aus einer Datei.  

Unter [Starten des Assistenten zum Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) finden Sie weitere Informationen zu erforderlichen Schritten zum Erstellen von Configuration Manager-Anwendungen und Bereitstellungstypen. Berücksichtigen Sie beim Erstellen und Bereitstellen von Apps für iOS-Geräte auch Folgendes.  

## <a name="general-considerations"></a>Allgemeine Aspekte  
 Configuration Manager unterstützt die Bereitstellung folgender App-Typen:  

|Gerätetyp|Unterstützte Dateien|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> In System Center Configuration Manager müssen Sie beim Importieren einer iOS-App keine Eigenschaftenliste (.plist) angeben.|  

 Die folgenden Bereitstellungsaktionen werden unterstützt:  

|Gerätetyp|Unterstützte Aktionen|  
|-----------------|-----------------------|  
|iOS|**Verfügbar**, **Erforderlich** Der Benutzer muss der Installation und Deinstallation zustimmen.

> [!IMPORTANT]  
>  Derzeit können Endbenutzer Unternehmens-Apps nicht über die Microsoft Intune-Unternehmensportal-App für iOS installieren. Der Grund sind für Apps geltende Einschränkungen, die im iOS App Store veröffentlicht werden (siehe App Store-Rezensionsrichtlinien, Abschnitt 2). Benutzer können Unternehmens-Apps (einschließlich verwalteter App Store-Apps und Branchenanwendungspakete) durch Navigieren zum Webportal von Intune auf ihrem Gerät installieren (portal.manage.microsoft.com). Weitere Informationen über die mobilen Verwaltungsfunktionen, die von der Intune-Unternehmensportal-App aktiviert werden, finden Sie unter [Verwaltungsfunktionen für registrierte Geräte in Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  
