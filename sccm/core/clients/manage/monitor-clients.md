---
title: "Überwachen von Clients – Configuration Manager | Microsoft-Dokumentation"
description: "Ausführliche Anleitungen zur Überwachung von Clients in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
caps.latest.revision: "23"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 08a4d9b29871b49e3118aef949572cef64940f96
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-clients-in-system-center-configuration-manager"></a>Überwachen von Clients in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


 Nachdem die System Center Configuration Manager-Clientanwendung auf den Windows-Computern und -Geräten an Ihrem Standort installiert wurde, können Sie deren Status und Aktivität in der Configuration Manager-Konsole überwachen.  

##  <a name="bkmk_about"></a> Informationen zum Clientstatus  
 Configuration Manager stellt die folgenden Informationstypen als Clientstatus bereit:  

-   **Onlinestatus von Clients:** Ab Version 1602 gibt dieser Status an, ob der Computer online ist oder nicht. Ein Computer gilt als online, wenn er mit dem ihm zugewiesenen Verwaltungspunkt verbunden ist.  Um anzugeben, dass der Client online ist, sendet er Ping-ähnliche Nachrichten an den Verwaltungspunkt. Wenn der Verwaltungspunkt nach ca. fünf Minuten keine Nachricht erhält, gilt der Client als offline.  

-   **Clientaktivität:** Dieser Status gibt an, ob der Client in den letzten 7 Tagen aktiv mit Configuration Manager interagiert hat. Wenn der Client keine Richtlinienaktualisierung angefordert, keine Taktnachricht gesendet oder in den letzten 7 Tagen keine Hardwareinventur gesendet hat, gilt der Client als inaktiv.  

-   **Clientprüfung:** Dieser Status gibt den Erfolg der regelmäßigen Überprüfung an, ob der Configuration Manager-Client auf dem Computer ausgeführt wird.  Bei dieser Prüfung gefundene Probleme können teilweise behoben werden. Weitere Informationen finden Sie unter [Prüfungen und Behebungsmaßnahmen durch Clientprüfung](#BKMK_ClientHealth).  

     Auf Computern mit Windows 7 wird die Clientüberprüfung als geplante Aufgabe ausgeführt. Bei nachfolgenden Betriebssystemen wird die Clientüberprüfung während des Windows-Wartungsfensters automatisch ausgeführt.  

     Sie können die Wiederherstellung so konfigurieren, dass sie auf bestimmten Computern, beispielsweise geschäftskritischen Servern, nicht ausgeführt wird. Wenn es außerdem noch zusätzliche Objekte gibt, die Sie auswerten möchten, können Sie die Kompatibilitätseinstellungen in Configuration Manager verwenden, um eine umfassende Lösung zur Überwachung der allgemeinen Integrität, Aktivität und Kompatibilität von Computern in Ihrer Organisation zu erstellen. Weitere Informationen zu Kompatibilitätseinstellungen finden Sie unter [Planen und Konfigurieren von Kompatibilitätseinstellungen in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

##  <a name="bkmk_indStatus"></a> Überwachen des Status einzelner Clients  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Geräte**, oder wählen Sie unter **Gerätesammlungen** eine Sammlung.  

     Ab Version 1602 geben die Symbole am Anfang jeder Zeile den Onlinestatus des Geräts an:  

    |||  
    |-|-|  
    |![Symbol für den Onlinestatus des Clients](../../../core/clients/manage/media/online-status-icon.png)|Gerät ist online.|  
    |![Symbol für den Offlinestatus des Clients](../../../core/clients/manage/media/offline-status-icon.png)|Gerät ist offline.|  
    |![Symbol für den unbekannten Status des Clients](../../../core/clients/manage/media/unknown-status-icon.png)|Onlinestatus ist unbekannt.|  
    |![Client ist nicht installiert](../../../core/clients/manage/media/client-not-installed.png)|Client ist nicht auf dem Gerät installiert.|  

2.  Um detaillierte Informationen zum Onlinestatus des Clients zu erhalten, fügen Sie diese Informationen der Geräteansicht hinzu, indem Sie mit der rechten Maustaste auf die Spaltenüberschrift klicken und dann auf die Onlinestatusfelder klicken, die Sie hinzufügen möchten. Die folgenden Spalten können Sie hinzufügen:  

    -   Der**Onlinestatus des Geräts** gibt an, ob der Client derzeit online oder offline ist. (Dies entspricht den von den Symbolen angezeigten Informationen).  

    -   Die Spalte**Zuletzt online** gibt an, wann sich der Status des Clients zuletzt in „online“ geändert hat.  

    -   Die Spalte**Zuletzt offline** gibt an, wann sich der Status des Clients zuletzt in „offline“ geändert hat.  

3.  Klicken Sie im Listenbereich auf einen einzelnen Client , um im Detailbereich weitere Statusinformationen anzuzeigen, z. B. zu Clientaktivität und Clientprüfungen.  

##  <a name="bkmk_allStatus"></a> Überwachen des Status aller Clients  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung** > **Clientstatus**. Auf dieser Seite der Konsole können Sie die Gesamtstatistik für die Clientaktivität und Clientprüfungen am gesamten Standort überprüfen.  Sie können auch den Umfang der Informationen ändern, indem Sie eine andere Sammlung auswählen.  

2.  Klicken Sie für Details zu den gemeldeten Statistiken auf den Namen der gemeldeten Informationen, z.B. **Active clients that have passed client check or no results (Aktive Clients, die die Clientprüfung bestanden haben oder für die keine Ergebnisse vorliegen)**, und überprüfen Sie die Informationen zu den einzelnen Clients.  

3.  Klicken Sie auf **Clientaktivität**, um Diagramme mit den Clientaktivitäten an Ihrem Configuration Manager-Standort einzublenden.  

4.  Klicken Sie auf **Clientprüfung**, um Diagramme zum Status von Clientprüfungen an Ihrem Configuration Manager-Standort einzublenden.  

 Sie können Warnungen konfigurieren, um benachrichtigt zu werden, wenn die Ergebnisse der Clientprüfung oder die Aktivität der Clients unter einen angegebenen Prozentsatz der Clients in einer Sammlung sinken oder wenn die Wiederherstellung bei einem angegebenen Prozentsatz der Clients nicht ausgeführt werden kann. Informationen zum Konfigurieren des Clientstatus finden Sie unter [Konfigurieren des Clientstatus in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

##  <a name="BKMK_ClientHealth"></a> Prüfungen und Behebungsmaßnahmen durch Clientprüfung  
 Die folgenden Prüfungen und Wiederherstellungsmaßnahmen können mithilfe der Clientprüfung ausgeführt werden.  

|Clientprüfung|Wiederherstellungsmaßnahme|Weitere Informationen|  
|------------------|------------------------|----------------------|  
|Überprüfen Sie, ob die Clientprüfung vor Kurzem ausgeführt wurde|Führen Sie die Clientprüfung aus|Es wird überprüft, ob die Clientprüfung mindestens einmal innerhalb der letzten drei Tage ausgeführt wurde.|  
|Überprüfen Sie, ob die erforderlichen Clientkomponenten installiert sind|Installieren Sie die erforderlichen Clientkomponenten|Es wird überprüft, ob die erforderlichen Clientkomponenten installiert sind. Es wird die Datei ccmsetup.xml im Installationsordner des Clients ausgelesen, um die erforderlichen Komponenten herauszufinden.|  
|WMI-Repository-Integritätstest|Installieren Sie den Configuration Manager-Client erneut.|Überprüft, ob Configuration Manager-Clienteinträge in WMI vorhanden sind|  
|Überprüfen Sie, ob der Clientdienst ausgeführt wird|Starten Sie den Clientdienst (SMS-Agent-Host)|keine zusätzlichen Informationen|  
|WMI-Ereignissenkentest.|Starten Sie den Clientdienst neu|Überprüfen Sie, ob die Configuration Manager-bezogene WMI-Ereignissenke verloren gegangen ist|  
|Überprüfen Sie, ob der WMI-Dienst (Windows-Verwaltungsinstrumentation) vorhanden ist|Keine Behebung|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Client ordnungsgemäß installiert wurde|Installieren Sie den Client erneut|keine zusätzlichen Informationen|  
|Lese- und Schreibtest für WMI-Repository|Setzen Sie das WMI-Repository zurück, und installieren Sie den Configuration Manager-Client erneut.|Eine Behebung dieser Clientprüfung wird nur auf Computern mit Windows Server 2003, Windows XP (64-Bit) oder früher durchgeführt.|  
|Überprüfen Sie, ob der Antischadsoftware-Dienststarttyp auf Automatisch eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|keine zusätzlichen Informationen|  
|Stellen Sie sicher, dass der Antischadsoftwaredienst ausgeführt wird.|Starten Sie den Antischadsoftwaredienst|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp für Windows Update auf Automatisch oder Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Starttyp des Clientdienstes (SMS-Agent-Host) auf Automatisch eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der WMI-Dienst (Windows-Verwaltungsinstrumentation) ausgeführt wird.|Starten Sie den Dienst Windows-Verwaltungsinstrumentation (WMI)|keine zusätzlichen Informationen|  
|Überprüfen Sie die Integrität der Microsoft SQL CE-Datenbank|Installieren Sie den Configuration Manager-Client erneut.|Keine zusätzlichen Informationen|  
|WMI-Integritätstest der Microsoft Policy Platform|Reparieren der Microsoft Policy Platform|keine zusätzlichen Informationen|  
|Stellen Sie sicher, dass der Microsoft Policy Platform-Dienst vorhanden ist|Reparieren der Microsoft Policy Platform|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp der Microsoft Policy Platform auf Manuell eingestellt ist.|Setzen Sie den Dienststarttyp zurück auf Manuell|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der intelligente Hintergrundübertragungsdienst (BITS) vorhanden ist|Keine Behebung|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Starttyp für den intelligenten Hintergrundübertragungsdienst auf Automatisch oder Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Starttyp für den Netzwerkinspektionsdienst auf Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Manuell, falls er installiert ist|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp für Windows-Verwaltungsinstrumentation (WMI) auf Automatisch eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp für Windows Update auf Windows 8-Computern auf Automatisch oder Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Manuell|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Clientdienst (SMS-Agent-Host) vorhanden ist.|Keine Behebung|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienststarttyp für die Remotesteuerung in Configuration Manager auf Automatisch oder Manuell eingestellt ist|Setzen Sie den Dienststarttyp zurück auf Automatisch|keine zusätzlichen Informationen|  
|Überprüfen Sie, ob der Dienst „Remotesteuerung in Configuration Manager“ ausgeführt wird|Starten Sie den Remotesteuerungsdienst|keine zusätzlichen Informationen|  
|Überprüfen Sie die Integrität des Client-WMI-Anbieters|Starten Sie den Dienst Windows-Verwaltungsinstrumentation (WMI) neu|Eine Behebung dieser Clientprüfung wird nur auf Computern mit Windows Server 2003, Windows XP (64-Bit) oder früher durchgeführt.|  
|Überprüfen Sie, ob der Aktivierungsproxydienst (ConfigMgr-Aktivierungsproxy) ausgeführt wird|Starten Sie den ConfigMgr-Aktivierungsproxydienst|Diese Clientprüfung wird nur vorgenommen, wenn die Clienteinstellung unter **Energieverwaltung**: **Aktivierungsproxy zulassen** auf unterstützten Clientbetriebssystemen auf **Ja** eingestellt ist.|  
|Überprüfen Sie, ob der Starttyp für den Aktivierungsproxydienst (ConfigMgr-Aktivierungsproxy) auf Automatisch eingestellt ist|Setzen Sie den Dienststarttyp für den ConfigMgr-Aktivierungsproxy zurück auf Automatisch|Diese Clientprüfung wird nur vorgenommen, wenn die Clienteinstellung unter **Energieverwaltung**: **Aktivierungsproxy zulassen** auf unterstützten Clientbetriebssystemen auf **Ja** eingestellt ist.|  

## <a name="client-deployment-log-files"></a>Clientbereitstellungs-Protokolldateien
Informationen zu den Protokolldateien, die von Clientbereitstellungs- und Verwaltungsvorgängen verwendet werden, finden Sie unter [Protokolldateien in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).
