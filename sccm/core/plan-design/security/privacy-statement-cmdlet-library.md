---
title: "System Center Configuration Manager-Datenschutzbestimmungen – Configuration Manager-Cmdlet-Bibliothek | Microsoft-Dokumentation"
description: "Erfahren Sie mehr darüber, wie Microsoft Daten zur System Center Configuration Manager-Cmdlet-Bibliothek sammelt und verwendet."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3936075555cc0bb370ea6e42c7e720b864d565f7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager-Datenschutzbestimmungen – Configuration Manager-Cmdlet-Bibliothek

*Gilt für: System Center Configuration Manager (Current Branch)*

Diese Datenschutzbestimmungen gelten für die Features der System Center Configuration Manager-Cmdlet-Bibliothek.  

## <a name="usage-data"></a>Nutzungsdaten  
 **Funktionsweise dieses Features:**   
Mit der System Center Configuration Manager-Cmdlet-Bibliothek können Sie eine Configuration Manager-Hierarchie mithilfe von Windows PowerShell-Cmdlets und -Skripts verwalten. Von der Cmdlet-Bibliothek werden Informationen darüber gesammelt, wie Sie die Cmdlets in der Bibliothek verwenden, um Trends und Verwendungsmuster zu ermitteln. Von der Cmdlet-Bibliothek werden auch Art und Anzahl der Fehler ermittelt, die beim Verwenden der Cmdlets auftreten.  

 **Erfasste, verarbeitete oder übertragene Informationen:**   
Zu den gesammelten Nutzungsdaten gehören das Starten, Anhalten und Beenden von Cmdlets und das Ausführen von veralteten Cmdlets und Aktivitätsmetriken für Vorgänge im Zusammenhang mit Cmdlets, die mit SMS-Anbietern (Systems Management Server) verknüpft sind. Diese Informationen sind nicht personenbezogen.  Zu den gesammelten Informationen gehören u.a. die von Cmdlets zurückgegebenen Fehler sowie Details zu Ausnahmefehlern. Einige Detailberichte zu Fehlern enthalten möglicherweise unbeabsichtigt personenbezogene Daten, z.B. Seriennummern von Geräten, die mit dem Computer verbunden sind. Diese Informationen in den Fehlerberichten werden von der Cmdlet-Bibliothek gefiltert und anonymisiert, um etwaige persönliche Informationen vor der Übertragung an Microsoft zu entfernen.  

 **Verwendung der Informationen:**   
Wir verwenden diese Informationen zur Verbesserung der Qualität, der Sicherheit und der Integrität der von uns angebotenen Produkte und Dienste.  

 **Auswahl/Kontrolle:**   
Das Feature zur Erfassung von Nutzungsdaten ist standardmäßig aktiviert. Die System Center Configuration Manager-Cmdlet-Bibliothek umfasst zwei Registrierungsschlüssel zur Steuerung dieser Funktionalität.  

 Zur vollständigen Deaktivierung müssen Sie die Werte dieser beiden Registrierungsschlüssel festlegen – jeweils einen für jeden der Anbieter zur Ereignisnachverfolgung für Windows (Event Tracing for Windows, ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (beendet die Erfassung von Nutzungsdaten für den Laufwerksanbieter)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (beendet die Erfassung von Nutzungsdaten für die Cmdlets)  

 Die Einstellungen für Nutzungsdaten gelten nur für den betreffenden Computer, auf dem sie festgelegt wurden.  

 Weitere Informationen zum Konfigurieren von Nutzungsdaten (Sammlung) finden Sie in der [Dokumentation zur System Center Configuration Manager-Cmdlets-Bibliothek](https://technet.microsoft.com/en-us/library/dn958404.aspx).   
