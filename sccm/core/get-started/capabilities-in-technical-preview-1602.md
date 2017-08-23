---
title: "Funktionen in Technical Preview 1602 für Configuration Manager"
description: "Erfahren Sie mehr zu Funktionen, die in System Center Configuration Manager Technical Preview 1602 zur Verfügung stehen."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 2354f885aaf69683004ad78f0e1978e78fee9145
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1602-for-system-center-configuration-manager"></a>Funktionen in Technical Preview 1602 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

In diesem Artikel werden die Funktionen erläutert, die in der Technical Preview 1602 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen, und zu erfahren, wie Sie Updates zwischen Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.  

 Im Folgenden werden neue Funktionen aufgelistet, die Sie mit dieser Version ausprobieren können.  

##  <a name="BKMK_MDM"></a> Verbesserungen für die Verwaltung mobiler Geräte  

### <a name="ios-activation-lock"></a>iOS-Aktivierungssperre  
 System Center Configuration Manager kann Sie beim Verwalten der iOS-Aktivierungssperre unterstützen, einem Feature der App „Mein iPhone suchen“ für iOS 7.1 und höher. Die Aktivierungssperre wird automatisch aktiviert, wenn die iPhone-App „Mein iPhone suchen“ auf einem Gerät verwendet wird. Nach der Aktivierung müssen die Apple-ID und das Kennwort des Benutzers eingegeben werden, bevor folgende Vorgänge möglich sind:  

-   Deaktivieren von „Mein iPhone suchen“  

-   Löschen des Geräts  

-   Reaktivieren des Geräts  

 Configuration Manager kann den Status der Aktivierungssperre von überwachten und nicht überwachten Geräten anfordern, die iOS 7.1 und höher ausführen. Für überwachte Geräte kann Intune den Umgehungscode der Aktivierungssperre abrufen und ihn direkt auf das Gerät anwenden.  

 Weitere Informationen finden Sie unter [Unterstützen des Schutzes von iOS-Geräten durch Umgehung der Aktivierungssperre für Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock)  

##  <a name="BKMK_SC1601"></a> Verbesserungen an Software Center in Version 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Aktualisieren von Computer- und Benutzerrichtlinien eines PCs über Software Center  
 Eine neue Option, **Richtlinie synchronisieren**, wurde in Software Center zur Seite **Optionen** > **Computerwartung** hinzugefügt. Mit dieser Option können die Configuration Manager-Computer- und -Benutzerrichtlinien auf dem PC aktualisiert werden.  

##  <a name="BKMK_Win10Servicing"></a> Verbesserungen für die Wartung von Windows 10  
 Die folgenden Verbesserungen für die Wartung von Windows 10 wurden zur Technical Preview 1602 hinzugefügt:  

-   Neue Filteroptionen für Wartungpläne.  Sie können jetzt nach **Sprache**, **Erforderlich** und **Titel** filtern. Nur Upgrades, die die angegebenen Kriterien erfüllen, werden der entsprechenden Bereitstellung hinzugefügt.  

-   Bei der Auswahl der Klassifizierung **Upgrades** für die Synchronisierung von Softwareupdates wird ein Warnungsdialogfeld angezeigt, um Sie zu informieren,dass [Hotfix 3095113](https://support.microsoft.com/kb/3095113) von WSUS erforderlich ist, um Softwareupdates erfolgreich synchronisieren zu können und damit die Windows 10-Wartung ordnungsgemäß funktioniert.  Vom Dialogfeld aus gelangen Sie zum Knowledge Base-Artikel für den Hotfix.  

-   Verfügbare Windows 10-Upgrades werden jetzt nur im Knoten **Windows 10-Wartung** \ **Alle Windows 10-Updates** der Configuration Manager-Konsole angezeigt. Diese Updates werden nicht mehr im Knoten **Softwareupdates** \ **Alle Softwareupdates** angezeigt.  

-   Endbenutzern, die ein Windows 10-Upgradepaket starten, wird ein Dialogfeld angezeigt, in dem sie informiert werden, dass sie im Begriff sind, ihr Betriebssystem zu aktualisieren.  
