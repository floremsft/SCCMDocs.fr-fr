---
title: "Checkliste für 1606 | Microsoft-Dokumentation"
description: "Erhalten Sie mehr über Aktionen, die Sie durchführen müssen, bevor Sie eine Aktualisierung von System Center Configuration Manager Version 1511 oder 1602 auf Version 1606 ausführen."
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a6bda116499845fedff0126e2890755931de85bb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>Checkliste für die Installation von Update 1606 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Version 1606 für System Center Configuration Manager (Current Branch) ist ein Update, das Sie für das Aktualisieren von Version 1511 oder 1602 verwenden können.

Lesen Sie vor der Installation von Version 1606 als Update die folgenden Informationen und die Checkliste mit Aktionen, die vor Beginn des Updates durchgeführt werden müssen.

Informationen zu Basisversionen finden Sie unter [Updates für System Center Configuration Manager](../../../core/servers/manage/updates.md) im Abschnitt [Baseline- und Updateversionen](../../../core/servers/manage/updates.md#bkmk_Baselines).

 ## <a name="about-installing-update-1606"></a>Informationen zur Installation des Updates 1606

Als *Update* kann 1606 nur am Standort der obersten Ebene Ihrer Hierarchie installiert werden. Das bedeutet, dass Sie die Installation vom Standort der zentralen Verwaltung (falls vorhanden) oder vom eigenständigen primären Standort aus starten.  

-   An untergeordneten primären Standorten wird das Update automatisch installiert, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Mithilfe von Dienstfenstern können Sie steuern, wann Updates an einem Standort installiert werden. Vor Version 1606 wurden Dienstfenster als Wartungsfenster bezeichnet. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](/sccm/core/servers/manage/service-windows).  

-   Sie müssen sekundäre Standorte von der Configuration Manager-Konsole aus manuell aktualisieren, nachdem die Installation des Updates am primären übergeordneten Standort abgeschlossen wurde. Die automatische Aktualisierung sekundärer Standortserver wird nicht unterstützt.  

Bei der Installation des Updates auf dem Standortserver werden Standortsystemrollen, die auf dem Standortserver und auf Remotecomputern installiert sind, automatisch aktualisiert. Stellen Sie daher vor der Installation des Updates sicher, dass jeder Standortsystemserver die neuen Voraussetzungen für den Betrieb mit der neuen Updateversion erfüllt.  

Bei der ersten Verwendung einer Configuration Manager-Konsole nach Installation des Updates werden Sie aufgefordert, die Konsole zu aktualisieren.  Dazu müssen Sie das Configuration Manager-Setup auf dem Computer ausführen, der die Konsole hostet, und dann die Option zum Aktualisieren der Konsole auswählen. Es wird empfohlen, die Installation des Updates auf der Konsole unverzüglich durchzuführen.

 **Bekannte Probleme dieses Updates**   
  Die folgenden Probleme betreffen Sie, wenn Sie den Installationsstatus des Updatepakets anzeigen:
  - Beim Aktualisieren von Version 1602 auf 1606 zeigt der Schritt **Updatepaket-Nutzlast extrahieren** den Status **Nicht gestartet** an, auch wenn der Download abgeschlossen ist.
  - Beim Aktualisieren von Version 1511 auf 1606 zeigen einige Schritte den Status **Abgeschlossen**, jedoch keinen Wert für **Zeitpunkt der letzten Aktualisierung** an.


## <a name="checklist"></a>Prüfliste  

 **Stellen Sie sicher, dass an allen Standorten eine unterstützte Version von System Center Configuration Manager ausgeführt wird:** Auf jedem Standortserver in der Hierarchie muss die gleiche Version von Configuration Manager ausgeführt werden (entweder 1511 oder 1602), bevor Sie die Installation des Updates 1606 starten.

 **Überprüfen Sie die installierten Microsoft .NET-Versionen auf den Standortsystemservern:** Bei der Installation von Update 1606 an einem Standort installiert Configuration Manager automatisch .NET Framework 4.5.2 auf jedem Computer, auf dem eine der folgenden Standortsystemrollen gehostet wird (wenn .NET Framework 4.5 oder höher nicht bereits installiert ist):  

-   Anmeldungsproxypunkt  

-   Anmeldungspunkt  

-   Verwaltungspunkt  

-   Dienstverbindungspunkt  

Diese Installation kann den Standortsystemserver in den Zustand „Ausstehender Neustart“ versetzen und Fehler an die Configuration Manager-Komponentenstatusanzeige melden. Darüber hinaus treten bei .NET-Anwendungen auf dem Server gelegentlich Fehler auf, bis der Server neu gestartet wird.  

 Weitere Informationen finden Sie unter [Standort- und Standortsystemanforderungen](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Prüfen Sie den Standort- und Hierarchiestatus, und stellen Sie sicher, dass keine ungelösten Probleme vorliegen:** Bevor Sie das Update für einen Standort durchführen, sollten Sie alle Betriebsprobleme beheben, die den Standortserver, den Standortdatenbankserver und die auf Remotecomputern installierten Standortsystemrollen betreffen. Betriebsprobleme können die Ursache für Fehler beim Update von Standorten sein.

 Weitere Informationen finden Sie unter [Verwenden von Benachrichtigungen und des Statussystems für System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Überprüfen Sie die Datei- und Datenreplikation zwischen Standorten:**  Stellen Sie sicher, dass die Datei- und Datenreplikation zwischen Standorten betriebsbereit und aktuell ist. Verzögerungen oder Rückstände können ein reibungsloses und erfolgreiches Update verhindern.    

Für die Datenbankreplikation können Sie die Replikationslinkanalyse verwenden, um Probleme vor Beginn des Updates zu lösen. Weitere Informationen finden Sie unter [Informationen zur Replikationslinkanalyse](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) im Thema [Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Installieren Sie alle anwendbaren wichtigen Updates für Betriebssysteme auf Computern, auf denen der Standort gehostet wird, auf dem Standortdatenbankserver und auf Remote-Standortsystemrollen:** Installieren Sie vor der Installation eines Updates für Configuration Manager alle wichtigen Updates für jedes relevante Standortsystem. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Computer neu, bevor Sie mit dem Upgrade beginnen.  

 **Deaktivieren Sie Datenbankreplikate für Verwaltungspunkte an primären Standorten:** Configuration Manager kann einen primären Standort, an dem ein Datenbankreplikat für Verwaltungspunkte aktiviert ist, nicht erfolgreich aktualisieren. Deaktivieren Sie die Datenbankreplikation, bevor Sie ein Update für Configuration Manager installieren.  

Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Legen Sie SQL Server Always On-Verfügbarkeitsgruppen auf manuelles Failover fest:**  
 Vor der Installation von Updates, z.B. Version 1606, stellen Sie sicher, dass die Verfügbarkeitsgruppe auf manuelles Failover festgelegt ist. Nachdem der Standort aktualisiert wurde, können Sie wieder auf automatisches Failover umstellen. Weitere Informationen finden Sie unter [SQL Server AlwaysOn für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

 **Konfigurieren Sie Softwareupdatepunkte mit NLBs neu:** Configuration Manager kann kein Update für Standorte durchführen, an denen Softwareupdatepunkte mithilfe eines Netzwerklastenausgleich-Clusters (Network Load Balancing, NLB) gehostet werden.  

Wenn Sie für Softwareupdatepunkte NLB-Cluster verwenden, entfernen Sie den NLB-Cluster mithilfe von Windows PowerShell.    

 Weitere Informationen finden Sie unter [Planen von Softwareupdates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Deaktivieren Sie alle Standortwartungstasks an jedem Standort für die Dauer der Updateinstallation am jeweiligen Standort:** Deaktivieren Sie vor der Updateinstallation alle Standortwartungstasks, die möglicherweise während des Zeitraums ausgeführt werden, für den der Updatevorgang aktiv ist. Zu diesen Tasks gehören u. a. folgende:  

-   Standortserver sichern  

-   Veraltete Clientvorgänge löschen  

-   Veraltete Ermittlungsdaten löschen  

Wenn ein Standortdatenbank-Wartungstask während der Updateinstallation ausgeführt wird, kann bei der Updateinstallation ein Fehler auftreten. Bevor Sie einen Task deaktivieren, zeichnen Sie den Zeitplan des Tasks auf, sodass Sie die Konfiguration nach Abschluss des Updates wiederherstellen können.  

Weitere Informationen finden Sie unter [Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) und [Referenz für Wartungstasks für System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Erstellen Sie eine Sicherung der Standortdatenbank am Standort der zentralen Verwaltung und an den primären Standorten:** Sichern Sie vor dem Update eines Standorts die Standortdatenbank, um sicherzustellen, dass Sie eine erfolgreiche Sicherung für die Notfallwiederherstellung besitzen.   

Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung für System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

<!-- Removed from update guidance 6/6/2017
 **Test the database upgrade on a copy of the most recent site database backup:** Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

-   You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

 **Planen Sie Pilottests für Clients:** Wenn Sie ein Update zum Aktualisieren des Clients installieren, können Sie dieses neue Clientupdate in der Präproduktionsphase testen, bevor es bereitgestellt und das Upgrade für all Ihre aktiven Clients durchgeführt wird.   

 Um diese Option vor der Installation des Updates zu nutzen, müssen Sie Ihren Standort für die Unterstützung automatischer Updates für die Präproduktionsphase konfigurieren. Weitere Informationen finden Sie unter [Aktualisieren von Clients in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) und   
[Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planen Sie die Verwendung von Dienstfenstern, um den Zeitpunkt der Updateinstallation auf den Standortservern zu steuern:** Mithilfe der Dienstfenster können Sie einen Zeitraum definieren, in dem Updates an einem Standortserver installiert werden können.

Damit können Sie steuern, wann das Update an Standorten in Ihrer Hierarchie installiert werden kann.
Vor Version 1606 wurden Dienstfenster als Wartungsfenster bezeichnet. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](/sccm/core/servers/manage/service-windows).  

 **Führen Sie die Setup-Voraussetzungsprüfung aus:** Vor der Installation des Updates 1606 können Sie die Voraussetzungsprüfung unabhängig von der Updateinstallation ausführen. Beim Installieren des Updates am Standort wird die Voraussetzungsprüfung erneut ausgeführt.  

Weitere Informationen finden Sie unter **Schritt 3: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates** im Thema [Updates für System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

> [!IMPORTANT]  
>  Wenn die Voraussetzungsprüfung im Rahmen einer Updateinstallation oder unabhängig davon ausgeführt wird, werden vom Prozess einige Produktquelldateien aktualisiert, die für Standortwartungstasks verwendet werden. Wenn Sie daher nach Durchführung der Voraussetzungsprüfung, aber vor Installation des Updates 1606 einen Standortwartungstask durchführen müssen, führen Sie **Setupwpf.exe** (Configuration Manager-Setup) im Ordner „CD.Latest“ auf dem Standortserver aus.  

 **Aktualisieren Sie Standorte:** Sie können nun die Updateinstallation für Ihre Hierarchie starten.  
  Es wird empfohlen, die Installation des Updates für jeden Standort außerhalb der normalen Geschäftszeiten zu planen, wenn die Installation des Updates und die zugehörigen Aktionen zum Neuinstallieren von Standortkomponenten und Standortsystemrollen die geringsten Auswirkungen auf die Geschäftsvorgänge haben.

Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](../../../core/servers/manage/updates.md).  
