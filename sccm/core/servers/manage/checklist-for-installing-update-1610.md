---
title: "Checkliste für 1610 | System Center Configuration Manager"
description: "Erfahren Sie mehr über Aktionen, die Sie durchführen müssen, bevor Sie eine Aktualisierung auf System Center Configuration Manager Version 1610 ausführen."
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 54b243fd33ed13b8ccde48fa5e2525204455d96c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Checkliste für die Installation von Update 1610 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn Sie Current Branch von System Center Configuration Manager verwenden, können Sie das konsoleninterne Update für Version 1610 installieren, um Ihre Hierarchie von Version 1606 zu aktualisieren. Wenn in Ihrer Hierarchie Version 1511, 1602 oder 1606 ausgeführt wird, können Sie auf Version 1610 aktualisieren.

Um das Update auf Version 1610 zu erhalten, müssen Sie eine Dienstverbindungspunkt-Standortsystemrolle auf der obersten Ebene Ihrer Hierarchie verwenden. Dies kann im Online- oder Offlinemodus erfolgen. Nachdem Ihre Hierarchie das Updatepaket von Microsoft heruntergeladen hat, können Sie es in der Konsole unter **Verwaltung &gt; Übersicht &gt; Clouddienste &gt; Updates und Wartung** finden.

-   Wenn das Update als **Verfügbar** aufgeführt ist, ist das Update zur Installation bereit. Überprüfen Sie vor der Installation von Version 1610 die folgenden Informationen [über die Installation von Update 1610](#about-installing-update-1610) und die [Checkliste](#checklist) für Konfigurationen, die vor dem Starten der Aktualisierung durchgeführt werden sollen.

-   Wenn das Update als **Herunterladen** angezeigt wird und sich nicht ändert, überprüfen Sie **hman.log** und **dmpdownloader.log** auf Fehler.

    -   Normalerweise können Sie auch den Dienst **SMS_Executive** auf dem Standortserver neu starten, um den Download der Update-Neuverteilungsdateien neu zu starten.

    -   Ein weiteres häufiges Downloadproblem tritt auf, wenn Proxyservereinstellungen Downloads von <http://silverlight.dlservice.microsoft.com> und <http://download.microsoft.com> verhindern.

Weitere Informationen zum Installieren von Updates finden Sie unter [Konsoleninterne Updates und Wartung](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Informationen zu den Current Branch-Versionen finden Sie im Abschnitt [Basis- und Updateversionen](/sccm/core/servers/manage/updates#bkmk_Baselines) unter [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Informationen zur Installation des Updates 1610

**Standorte:**  
Update 1610 kann nur am Standort der obersten Ebene Ihrer Hierarchie installiert werden. Das bedeutet, dass Sie die Installation vom Standort der zentralen Verwaltung (falls vorhanden) oder vom eigenständigen primären Standort aus starten. Nach dem Installieren des Updates am Standort der obersten Ebene haben untergeordnete Standorte das folgende Updateverhalten:

-   An untergeordneten primären Standorten wird das Update automatisch gestartet, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Mithilfe von Dienstfenstern können Sie steuern, wann Updates an einem Standort installiert werden. Vor Version 1606 wurden Dienstfenster als Wartungsfenster bezeichnet. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](/sccm/core/servers/manage/service-windows).

-   Sie müssen sekundäre Standorte von der Configuration Manager-Konsole aus manuell aktualisieren, nachdem die Updateinstallation am primären übergeordneten Standort abgeschlossen wurde. Die automatische Aktualisierung sekundärer Standortserver wird nicht unterstützt.

**Standortsystemrollen:**  
Bei der Installation des Updates auf dem Standortserver werden Standortsystemrollen, die auf dem Standortserver und auf Remotecomputern installiert sind, automatisch aktualisiert. Stellen Sie daher vor der Installation des Updates sicher, dass jeder Standortsystemserver die neuen Voraussetzungen für den Betrieb mit der neuen Updateversion erfüllt.

**Configuration Manager-Konsolen:**   
Bei der ersten Verwendung einer Configuration Manager-Konsole nach Abschluss des Updates werden Sie aufgefordert, die Konsole zu aktualisieren. Dazu müssen Sie das Configuration Manager-Setup auf dem Computer ausführen, der die Konsole hostet, und dann die Option zum Aktualisieren der Konsole auswählen. Es wird empfohlen, die Installation des Updates auf der Konsole unverzüglich durchzuführen.



## <a name="checklist"></a>Prüfliste

**Stellen Sie sicher, dass an allen Standorten eine unterstützte Version von System Center Configuration Manager ausgeführt wird:** An jedem Standort in der Hierarchie muss die gleiche Version von Configuration Manager ausgeführt werden (entweder 1511, 1602 oder 1606), bevor Sie die Installation des Updates 1610 starten.

**Überprüfen Sie den Status Ihrer Software Assurance oder entsprechende Abonnementrechte:**   
Zur Installation von Update 1610 ist ein aktiver Software Assurance-Vertrag erforderlich. Wenn Sie Version 1610 installieren, haben Sie auf der Registerkarte **Lizenzierung** die Möglichkeit, Ihr **Software Assurance-Ablaufdatum** zu bestätigen.

Dies ist ein optionaler Wert, den Sie als bequeme Erinnerung für Ihr Lizenzablaufdatum angeben können, das bei der Installation zukünftiger Updates sichtbar ist. Wenn Sie Configuration Manager von den Baselinemedien der Version 1606 installiert haben, haben Sie diesen Wert während des Setups oder nach der Installation auf der Registerkarte **Lizenzierung** der **Hierarchieeinstellungen** festgelegt.

Weitere Informationen finden Sie unter [Lizenzierung und Branches für System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Überprüfen Sie die installierten Microsoft .NET-Versionen auf den Standortsystemservern:** Bei der Installation von Update 1610 an einem Standort installiert Configuration Manager automatisch .NET Framework 4.5.2 auf jedem Computer, auf dem eine der folgenden Standortsystemrollen gehostet wird, wenn .NET Framework 4.5 oder höher nicht bereits installiert ist:

-   Anmeldungsproxypunkt
-   Anmeldungspunkt
-   Verwaltungspunkt
-   Dienstverbindungspunkt

Diese Installation kann den Standortsystemserver in den Zustand „Ausstehender Neustart“ versetzen und Fehler an die Configuration Manager-Komponentenstatusanzeige melden. Darüber hinaus treten bei .NET-Anwendungen auf dem Server gelegentlich Fehler auf, bis der Server neu gestartet wird.

Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).

**Prüfen Sie den Standort- und Hierarchiestatus, und stellen Sie sicher, dass keine ungelösten Probleme vorliegen:** Bevor Sie das Update für einen Standort durchführen, sollten Sie alle Betriebsprobleme beheben, die den Standortserver, den Standortdatenbankserver und die auf Remotecomputern installierten Standortsystemrollen betreffen. Betriebsprobleme können die Ursache für Fehler beim Update von Standorten sein.

Weitere Informationen finden Sie unter [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Überprüfen Sie die Datei- und Datenreplikation zwischen Standorten:**   
Stellen Sie sicher, dass die Datei- und Datenreplikation zwischen Standorten betriebsbereit und aktuell ist. Verzögerungen oder Rückstände können ein reibungsloses und erfolgreiches Update verhindern.
Für die Datenbankreplikation können Sie die Replikationslinkanalyse verwenden, um Probleme vor Beginn des Updates zu lösen.

Weitere Informationen finden Sie unter [Informationen zur Replikationslinkanalyse](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) im Thema [Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure).

**Installieren Sie alle anwendbaren wichtigen Updates für Betriebssysteme auf Computern, auf denen der Standort gehostet wird, auf dem Standortdatenbankserver und auf Remote-Standortsystemrollen:** Installieren Sie vor der Installation eines Updates für Configuration Manager alle wichtigen Updates für jedes relevante Standortsystem. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Computer neu, bevor Sie mit dem Configuration Manager-Update beginnen.

**Deaktivieren Sie Datenbankreplikate für Verwaltungspunkte an primären Standorten:**   
Configuration Manager kann kein Update eines primären Standorts durchführen, wenn dort Datenbankreplikate für Verwaltungspunkte aktiviert sind. Deaktivieren Sie die Datenbankreplikation, bevor Sie ein Update für Configuration Manager installieren.

Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Legen Sie SQL Server Always On-Verfügbarkeitsgruppen auf manuelles Failover fest:**   
Vor der Installation von Updates, z.B. Version 1610, stellen Sie sicher, dass die Verfügbarkeitsgruppe auf manuelles Failover festgelegt ist. Nachdem der Standort aktualisiert wurde, können Sie wieder auf automatisches Failover umstellen. Weitere Informationen finden Sie unter [SQL Server AlwaysOn für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Führen Sie eine erneute Konfiguration der Softwareupdatepunkte durch, von denen NLBs verwendet werden:**   
Configuration Manager kann kein Update für Standorte durchführen, an denen Softwareupdatepunkte mithilfe eines NLB-Clusters gehostet werden.

Wenn Sie für Softwareupdatepunkte NLB-Cluster verwenden, entfernen Sie den NLB-Cluster mithilfe von Windows PowerShell.
Weitere Informationen finden Sie unter [Planen von Softwareupdates in System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Deaktivieren Sie alle Standortwartungstasks an jedem Standort für die Dauer der Updateinstallation an diesem Standort:**   
Bevor Sie das Update installieren, deaktivieren Sie alle Standortwartungstasks, die möglicherweise zu dem Zeitpunkt ausgeführt werden, zu dem der Updateprozess aktiv ist. Zu diesen Tasks gehören u. a. folgende:

-   Standortserver sichern
-   Veraltete Clientvorgänge löschen
-   Veraltete Ermittlungsdaten löschen

Wenn ein Standortdatenbank-Wartungstask während der Updateinstallation ausgeführt wird, kann bei der Updateinstallation ein Fehler auftreten. Bevor Sie einen Task deaktivieren, zeichnen Sie den Zeitplan des Tasks auf, sodass Sie die Konfiguration nach Abschluss des Updates wiederherstellen können.

Weitere Informationen finden Sie unter [Wartungstasks für System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) und [Referenz für Wartungstasks für System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Erstellen Sie eine Sicherung der Standortdatenbank am Standort der zentralen Verwaltung und an den primären Standorten:** Sichern Sie vor dem Update eines Standorts die Standortdatenbank, um sicherzustellen, dass Sie eine erfolgreiche Sicherung für die Notfallwiederherstellung besitzen.

Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung für System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

**Planen von Pilottests für Clients:**   
Bei der Installation eines Updates, das den Client aktualisiert, können Sie das neue Clientupdate in der Präproduktionsphase testen, bevor es bereitgestellt wird und all Ihre aktiven Clients aktualisiert.

Um diese Option zu nutzen, müssen Sie Ihren Standort für die Unterstützung automatischer Updates für die Präproduktionsphase konfigurieren, bevor Sie die Installation des Updates starten.

Weitere Informationen finden Sie unter [Aktualisieren von Clients in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) und [Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Mithilfe von Dienstfenstern können Sie planen, wann Standortserver Updates an einem Standort installieren:**   
Mithilfe von Dienstfenstern können Sie einen Zeitraum definieren, in dem Updates an einem Standortserver installiert werden können.

Damit können Sie steuern, wann das Update an Standorten in Ihrer Hierarchie installiert werden kann. Vor Version 1606 wurden Dienstfenster als Wartungsfenster bezeichnet. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](/sccm/core/servers/manage/service-windows).

**Führen Sie die Setup-Voraussetzungsprüfung aus:**   
Wenn das Update in der Konsole als **verfügbar** aufgeführt wird, können Sie die Voraussetzungsprüfung vor der Installation des Updates unabhängig ausführen. (Beim Installieren des Updates am Standort wird die Voraussetzungsprüfung erneut ausgeführt.)

Um eine Voraussetzungsprüfung von der Konsole aus durchzuführen, wechseln Sie zu **Verwaltung > Übersicht > Clouddienste > Updates und Wartung**. Klicken Sie als Nächstes mit der rechten Maustaste auf das **Updatepaket für Configuration Manager 1610**, und wählen Sie dann **Voraussetzungsprüfung ausführen**.

Weitere Informationen zum Starten und anschließenden Überwachen der Voraussetzungsprüfung finden Sie unter **Schritt 3: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates** im Thema [Installieren konsoleninterner Updates für System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Wenn die Voraussetzungsprüfung im Rahmen einer Updateinstallation oder unabhängig davon ausgeführt wird, werden vom Prozess einige Produktquelldateien aktualisiert, die für Standortwartungstasks verwendet werden. Wenn Sie daher nach Durchführung der Voraussetzungsprüfung, aber vor Installation des Updates 1610 einen Standortwartungstask durchführen müssen, führen Sie **Setupwpf.exe** (Configuration Manager-Setup) im Ordner „CD.Latest“ auf dem Standortserver aus.

**Standorte aktualisieren:**   
Sie können nun die Updateinstallation für Ihre Hierarchie starten. Weitere Informationen zum Installieren des Updates finden Sie unter [Installieren konsoleninterner Updates](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

Es wird empfohlen, die Installation des Updates für jeden Standort außerhalb der normalen Geschäftszeiten zu planen, wenn die Installation des Updates und die zugehörigen Aktionen zum Neuinstallieren von Standortkomponenten und Standortsystemrollen die geringsten Auswirkungen auf die Geschäftsvorgänge haben.

Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates).
