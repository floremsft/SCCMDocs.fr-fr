---
title: "Checkliste für 1602 | Microsoft-Dokumentation"
description: "Erhalten Sie mehr über Aktionen, die Sie durchführen müssen, bevor Sie eine Aktualisierung von System Center Configuration Manager Version 1511 auf Version 1602 ausführen."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
caps.latest.revision: "13"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 3e0de56b7a592b105e6a61b3d6654b1d0142584d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="checklist-for-installing-update-1602-for-system-center-configuration-manager"></a>Checkliste für die Installation von Update 1602 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Lesen Sie vor dem Aktualisieren von System Center Configuration Manager Version 1511 auf Version 1602 die folgenden Informationen und die Checkliste mit Aktionen, die vor Beginn des Updates durchgeführt werden müssen.  

 **Informationen über die Installation des Updates 1602:**  

 Update 1602 kann nur am Standort der obersten Ebene Ihrer Hierarchie installiert werden. Das bedeutet, dass Sie die Installation vom Standort der zentralen Verwaltung (falls vorhanden) oder vom eigenständigen primären Standort aus starten.  

-   An untergeordneten primären Standorten wird das Update automatisch installiert, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Mithilfe von Wartungsfenstern können Sie steuern, wann Updates an einem Standort installiert werden. Mit der Veröffentlichung des Updates 1602 werden Wartungsfenster in *Dienstfenster* umbenannt. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](/sccm/core/servers/manage/service-windows).  

-   Sie müssen sekundäre Standorte von der Configuration Manager-Konsole aus manuell aktualisieren, nachdem die Installation des Updates am primären übergeordneten Standort abgeschlossen wurde. Automatische Aktualisierungen sekundärer Standortserver werden nicht unterstützt.  

Bei der Installation des Updates auf dem Standortserver werden Standortsystemrollen, die auf dem Standortserver und auf Remotecomputern installiert sind, automatisch aktualisiert. Stellen Sie daher vor der Installation des Updates sicher, dass jeder Standortsystemserver die neuen Voraussetzungen für den Betrieb mit der neuen Updateversion erfüllt.  

Bei der ersten Verwendung einer Configuration Manager-Konsole nach Abschluss des Updates werden Sie aufgefordert, die Konsole zu aktualisieren. Dazu müssen Sie das Configuration Manager-Setup auf dem Computer ausführen, der die Konsole hostet, und die Option zum Aktualisieren der Konsole auswählen. Es wird empfohlen, die Installation des Updates auf der Konsole unverzüglich durchzuführen.  

 **Checkliste:**  

 **Stellen Sie sicher, dass an allen Standorten eine unterstützte Version von System Center Configuration Manager ausgeführt wird:** Auf jedem Standortserver in der Hierarchie muss Configuration Manager Version 1511 ausgeführt werden, damit Sie die Installation des Updates 1602 starten können.  

 **Überprüfen Sie die installierten Microsoft .NET-Versionen auf den Standortsystemservern:** Bei der Installation von Update 1602 an einem Standort installiert Configuration Manager automatisch .NET Framework 4.5.2 auf jedem Computer, auf dem eine der folgenden Standortsystemrollen gehostet wird (wenn .NET Framework 4.5 oder höher nicht bereits installiert ist):  

-   Anmeldungsproxypunkt  

-   Anmeldungspunkt  

-   Verwaltungspunkt  

-   Dienstverbindungspunkt  

Diese Installation kann den Standortsystemserver in den Zustand „Ausstehender Neustart“ versetzen und Fehler an die Configuration Manager-Komponentenstatusanzeige melden. Darüber hinaus treten bei .NET-Anwendungen auf dem Server gelegentlich Fehler auf, bis der Server neu gestartet wird.  

 Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  

 **Prüfen Sie den Standort- und Hierarchiestatus, und stellen Sie sicher, dass keine ungelösten Probleme vorliegen:** Bevor Sie das Update für einen Standort durchführen, sollten Sie alle Betriebsprobleme beheben, die den Standortserver, den Standortdatenbankserver und die auf Remotecomputern installierten Standortsystemrollen betreffen. Betriebsprobleme können die Ursache für Fehler beim Update von Standorten sein.  

Weitere Informationen finden Sie unter [Verwenden von Benachrichtigungen und des Statussystems für System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Überprüfen Sie die Datei- und Datenreplikation zwischen Standorten:**  Stellen Sie sicher, dass die Datei- und Datenreplikation zwischen Standorten betriebsbereit und aktuell ist. Verzögerungen oder Rückstände können ein reibungsloses und erfolgreiches Update verhindern.    

Für die Datenbankreplikation können Sie die Replikationslinkanalyse verwenden, um Probleme vor Beginn des Updates zu lösen.    

 Weitere Informationen finden Sie unter [Informationen zur Replikationslinkanalyse](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) im Thema [Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Installieren Sie alle anwendbaren wichtigen Updates für Betriebssysteme auf Computern, auf denen der Standort gehostet wird, auf dem Standortdatenbankserver und auf Remote-Standortsystemrollen:** Installieren Sie vor der Installation eines Updates für Configuration Manager alle wichtigen Updates für jedes relevante Standortsystem. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Computer neu, bevor Sie mit dem Upgrade beginnen.  

 **Deaktivieren Sie Datenbankreplikate für Verwaltungspunkte an primären Standorten:** Configuration Manager kann einen primären Standort, an dem ein Datenbankreplikat für Verwaltungspunkte aktiviert ist, nicht erfolgreich aktualisieren. Deaktivieren Sie die Datenbankreplikation, bevor Sie folgende Schritte ausführen:  

-   Erstellen einer Sicherung der Standortdatenbank zum Testen des Datenbankupgrades.  

-   Installieren eines Updates für Configuration Manager.  

Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Konfigurieren Sie Softwareupdatepunkte mit NLBs neu:** Configuration Manager kann kein Update für Standorte durchführen, an denen Softwareupdatepunkte mithilfe eines Netzwerklastenausgleich-Clusters (Network Load Balancing, NLB) gehostet werden.  Wenn Sie für Softwareupdatepunkte NLB-Cluster verwenden, entfernen Sie den NLB-Cluster mithilfe von Windows PowerShell.    

 Weitere Informationen finden Sie unter [Planen von Softwareupdates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Deaktivieren Sie alle Standortwartungstasks an jedem Standort für die Dauer der Updateinstallation am jeweiligen Standort:** Deaktivieren Sie vor der Updateinstallation alle Standortwartungstasks, die möglicherweise während des Zeitraums ausgeführt werden, für den der Updatevorgang aktiv ist. Zu diesen Aufgaben gehören u.a. folgende:  

-   Standortserver sichern  

-   Veraltete Clientvorgänge löschen  

-   Veraltete Ermittlungsdaten löschen  

Wenn ein Standortdatenbank-Wartungstask während der Updateinstallation ausgeführt wird, kann bei der Updateinstallation ein Fehler auftreten. Bevor Sie einen Task deaktivieren, zeichnen Sie den Zeitplan des Tasks auf, sodass Sie die Konfiguration nach Abschluss des Updates wiederherstellen können.  

 Weitere Informationen finden Sie unter [Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) und [Referenz für Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Erstellen Sie eine Sicherung der Standortdatenbank am Standort der zentralen Verwaltung und an den primären Standorten:** Sichern Sie vor dem Update eines Standorts die Standortdatenbank, um sicherzustellen, dass Sie eine erfolgreiche Sicherung für die Notfallwiederherstellung besitzen.   

Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung für System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Sichern Sie eine benutzerdefinierte Datei „Configuration.mof“:** Wenn Sie eine benutzerdefinierte Datei „Configuration.mof“ verwenden, um die bei der Hardwareinventur verwendeten Datenklassen zu definieren, müssen Sie vor dem Update des Standorts eine Sicherung dieser Datei erstellen. Nach dem Update stellen Sie diese Datei am Standort der Version 1602 wieder her. Beim Update eines Standorts wird die aktuelle Datei durch die Originalversion (Standard) der Datei überschrieben. Weitere Informationen zur Verwendung dieser Datei finden Sie unter [Erweitern der Hardwareinventur in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Testen Sie das Datenbankupgrade mit einer Kopie der letzten Sicherung der Standortdatenbank:** Bevor Sie ein Update für einen Standort der zentralen Verwaltung oder einen primären Standort von System Center Configuration Manager durchführen, sollten Sie den Datenbankupgradeprozess mit einer Kopie der letzten Sicherung der Standortdatenbank testen.  

-   Sie sollten den Standortdatenbank-Upgradeprozess testen, da die Standortdatenbank während der Aktualisierung eines Standorts geändert werden kann.  

-   Ein Testdatenbankupgrade ist zwar nicht erforderlich, doch können dadurch Probleme beim Upgrade ermittelt werden, bevor die Produktionsdatenbank betroffen ist.  

-   Wenn beim Upgrade einer Standortdatenbank Fehler auftreten, ist die Datenbank möglicherweise nicht mehr betriebsfähig, und es müsste eine Standortwiederherstellung erfolgen.  

-   Obwohl die Standortdatenbank von allen Standorten in einer Hierarchie gemeinsam genutzt wird, sollten Sie die Datenbank an jedem relevanten Standort testen, bevor Sie das Upgrade für diesen Standort durchführen.  

-   Wenn Sie an einem primären Standort Datenbankreplikate für Verwaltungspunkte verwenden, deaktivieren Sie die Replikation, bevor Sie die Sicherung der Standortdatenbank erstellen.  

Configuration Manager unterstützt weder die Sicherung sekundärer Standorte noch das Testupgrade einer sekundären Standortdatenbank.   
Führen Sie kein Testdatenbankupgrade für die Datenbank des Produktionsstandorts aus. Dadurch würde ein Update der Standortdatenbank durchgeführt, und Ihr Standort wäre möglicherweise nicht mehr betriebsfähig. Weitere Informationen finden Sie unter **Vor der Installation eines konsoleninternen Updates** und dann im [Schritt 2: Testen des Datenbankupgrades vor der Installation eines Updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2).  

 **Planen Sie Pilottests für Clients:** Wenn Sie ein Update zum Aktualisieren des Clients installieren, können Sie dieses neue Clientupdate in der Präproduktionsphase testen, bevor es bereitgestellt und das Upgrade für all Ihre aktiven Clients durchgeführt wird.   

 Um diese Option zu nutzen, müssen Sie Ihren Standort für die Unterstützung automatischer Updates für die Präproduktionsphase konfigurieren, bevor Sie die Installation des Updates starten. Weitere Informationen finden Sie unter [Aktualisieren von Clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) und   
[Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planen Sie die Verwendung von Wartungsfenstern, um den Zeitpunkt der Updateinstallation auf den Standortservern zu steuern:** Mithilfe der Wartungsfenster können Sie einen Zeitraum definieren, in dem Updates am Standortserver installiert werden können. Damit können Sie steuern, wann das Update an Standorten in Ihrer Hierarchie installiert werden kann.   

Mit der Veröffentlichung des Updates 1602 werden Wartungsfenster in *Dienstfenster* umbenannt. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](/sccm/core/servers/manage/service-windows).  

 **Führen Sie die Setup-Voraussetzungsprüfung aus:** Vor der Installation des Updates 1602 können Sie die Voraussetzungsprüfung unabhängig von der Updateinstallation ausführen. Beim Installieren des Updates am Standort wird die Voraussetzungsprüfung erneut ausgeführt.  

Weitere Informationen finden Sie unter **Schritt 3: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates** im Thema [Updates für System Center Configuration Manager](../../../core/servers/manage/updates.md).  

> [!IMPORTANT]  
>  Wenn die Voraussetzungsprüfung im Rahmen einer Updateinstallation oder unabhängig davon ausgeführt wird, werden vom Prozess einige Produktquelldateien aktualisiert, die für Standortwartungstasks verwendet werden. Wenn Sie daher nach Durchführung der Voraussetzungsprüfung, aber vor Installation des Updates 1602 einen Standortwartungstask durchführen müssen, führen Sie **Setupwfe.exe** (Configuration Manager-Setup) im Ordner „CD.Latest“ auf dem Standortserver aus.  

 **Aktualisieren Sie Standorte:** Sie können nun die Updateinstallation für Ihre Hierarchie starten. Es wird empfohlen, die Installation des Updates für jeden Standort außerhalb der normalen Geschäftszeiten zu planen, wenn die Installation des Updates und die zugehörigen Aktionen zum Neuinstallieren von Standortkomponenten und Standortsystemrollen die geringsten Auswirkungen auf die Geschäftsvorgänge haben.

Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Weitere Informationen:  
 [Updates for System Center Configuration Manager (Updates für System Center Configuration Manager)](../../../core/servers/manage/updates.md)
