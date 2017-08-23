---
title: "Checkliste für 1706 | System Center Configuration Manager"
description: "Erfahren Sie mehr über Aktionen, die Sie durchführen müssen, bevor Sie eine Aktualisierung auf System Center Configuration Manager Version 1706 vornehmen."
ms.custom: na
ms.date: 07/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7def067e-845c-4db3-9d56-fa1dcf2fd7c7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: dab99748902df0fad32a1e2adad0c05e0dd8bdc9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="checklist-for-installing-update-1706-for-system-center-configuration-manager"></a>Checkliste für die Installation des Updates 1706 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn Sie Current Branch von System Center Configuration Manager verwenden, können Sie das konsoleninterne Update auf Version 1706 installieren, um Ihre aus einer älteren Version stammende Hierarchie zu aktualisieren.

Um das Update auf Version 1706 zu erhalten, müssen Sie auf der obersten Ebene Ihrer Hierarchie eine Dienstverbindungspunkt-Standortsystemrolle verwenden. Dies kann im Online- oder Offlinemodus erfolgen. Nachdem Ihre Hierarchie das Updatepaket von Microsoft heruntergeladen hat, können Sie es in der Konsole unter **Verwaltung &gt; Übersicht &gt; Clouddienste &gt; Updates und Wartung** finden.

-   Wenn das Update als **Verfügbar** aufgeführt ist, ist das Update zur Installation bereit. Lesen Sie vor der Installation von Version 1706 die Informationen [zur Installation des Updates 1706](#about-installing-update-1706) und die [Checkliste](#checklist) für Konfigurationen, die vor dem Starten der Aktualisierung durchgeführt werden sollen.

-   Wenn das Update als **Herunterladen** angezeigt wird und sich nicht ändert, überprüfen Sie **hman.log** und **dmpdownloader.log** auf Fehler.

    -   Wenn „dmpdownloader.log“ angibt, dass der dmpdownloader-Prozess inaktiv ist und bis zur Prüfung auf neue Updates noch eine Zeit lang wartet, können Sie den Dienst **SMS_Executive** auf dem Standortserver erneut starten, um den Download der Update-Neuverteilungsdateien ebenfalls erneut zu starten.

    -   Ein weiteres häufiges Downloadproblem tritt auf, wenn Proxyservereinstellungen Downloads von <http://silverlight.dlservice.microsoft.com> und <http://download.microsoft.com> verhindern.

Weitere Informationen zum Installieren von Updates finden Sie unter [Konsoleninterne Updates und Wartung](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Informationen zu den Current Branch-Versionen finden Sie im Abschnitt [Basis- und Updateversionen](/sccm/core/servers/manage/updates#bkmk_Baselines) unter [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1706"></a>Informationen zur Installation des Updates 1706

**Standorte:**  
Sie installieren das Update 1706 am Standort der obersten Ebene Ihrer Hierarchie. Das bedeutet, dass Sie die Installation vom Standort der zentralen Verwaltung (falls vorhanden) oder vom eigenständigen primären Standort aus starten. Nach dem Installieren des Updates am Standort der obersten Ebene haben untergeordnete Standorte das folgende Updateverhalten:

-   An untergeordneten primären Standorten wird das Update automatisch gestartet, sobald die Installation des Updates am Standort der zentralen Verwaltung abgeschlossen ist. Mithilfe von Dienstfenstern können Sie steuern, wann das Update an einem Standort installiert wird. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](/sccm/core/servers/manage/service-windows).

-   Sie müssen jeden sekundären Standort von der Configuration Manager-Konsole aus manuell aktualisieren, nachdem die Updateinstallation am primären übergeordneten Standort abgeschlossen wurde. Die automatische Aktualisierung sekundärer Standortserver wird nicht unterstützt.

**Standortsystemrollen:**  
Bei der Installation des Updates auf dem Standortserver werden Standortsystemrollen, die auf dem Standortservercomputer und auf Remotecomputern installiert sind, automatisch aktualisiert. Stellen Sie daher vor der Installation des Updates sicher, dass jeder Standortsystemserver die Voraussetzungen für den Betrieb mit der neuen Updateversion erfüllt.

**Configuration Manager-Konsolen:**   
Bei der ersten Verwendung einer Configuration Manager-Konsole nach Abschluss des Updates werden Sie aufgefordert, die Konsole zu aktualisieren. Dazu müssen Sie das Configuration Manager-Setup auf dem Computer ausführen, der die Konsole hostet, und dann die Option zum Aktualisieren der Konsole auswählen. Es wird empfohlen, die Installation des Updates auf der Konsole unverzüglich durchzuführen.

> [!IMPORTANT]  
> Wenn Sie ein Update am Standort der zentralen Verwaltung installieren, beachten Sie folgende Einschränkungen und Verzögerungen, die bis zum Abschluss der Updateinstallation auf allen untergeordneten primären Standorten auftreten:    
> - **Clientupgrades** starten nicht. Dazu zählen auch automatische Updates für Clients und Präproduktionsclients. Sie können außerdem keine Präproduktionsclients auf die Produktionsphase höherstufen, bis die Updateinstallation auch am letzten Standort abgeschlossen ist. Wenn die Updateinstallation auch am letzten Standort abgeschlossen ist, werden die Clientupgrades basierend auf Ihren Konfigurationen durchgeführt.   
> - **Neue Funktionen**, die Sie mit dem Update aktivieren, sind nicht verfügbar. Damit können Sie verhindern, dass die Replikation von Daten, die mit dieser Funktion verknüpft sind, an einen Standort geschickt wird, der die Funktion noch nicht unterstützt. Wenn das Update an allen primären Standorten installiert wurde, können Sie die Funktion nutzen.   
> - **Replikationslinks** zwischen dem Standort der zentralen Verwaltung und untergeordneten primären Standorten werden als nicht aktualisiert angezeigt. Dies wird im Installationsstatus des Updatepakets als „Completed“ („Abgeschlossen“) mit der Warnung „Replikationsinitialisierung wird überwacht“ angezeigt. Im Knoten „Überwachung“ der Konsole wird dies als *Link wird konfiguriert* angezeigt.



## <a name="checklist"></a>Prüfliste

**Stellen Sie sicher, dass an allen Standorten eine Version von System Center Configuration Manager ausgeführt wird, die ein Update auf Version 1706 unterstützt:**   
Auf jedem Standortserver in der Hierarchie muss die gleiche Version von System Center Configuration Manager ausgeführt werden, bevor Sie die Installation des Updates 1706 starten können. Sie können die Versionen 1606, 1610 und 1702 auf 1706 aktualisieren.

**Überprüfen Sie den Status Ihrer Software Assurance oder entsprechende Abonnementrechte:**   
Zur Installation des Updates 1706 ist ein aktiver Software Assurance-Vertrag erforderlich. Wenn Sie dieses Update installieren, haben Sie auf der Registerkarte **Lizenzierung** die Möglichkeit, Ihr **Software Assurance-Ablaufdatum** zu bestätigen.

Dies ist ein optionaler Wert, den Sie als praktische Erinnerung an das Ablaufdatum Ihrer Lizenz angeben können. Dieses Datum ist sichtbar, wenn Sie künftige Updates installieren. Sie haben diesen Wert möglicherweise schon während des Setups oder nach der Installation eines Updates oder über die Registerkarte **Lizenzierung** der **Hierarchieeinstellungen** innerhalb der Configuration Manager-Konsole festgelegt.

Weitere Informationen finden Sie unter [Lizenzierung und Branches für System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Überprüfen Sie die installierten Microsoft .NET-Versionen auf den Standortsystemservern:** Bei der Installation dieses Updates an einem Standort installiert Configuration Manager automatisch .NET Framework 4.5.2 auf jedem Computer, auf dem eine der folgenden Standortsystemrollen gehostet wird, wenn .NET Framework 4.5 oder höher nicht bereits installiert ist:

-   Anmeldungsproxypunkt
-   Anmeldungspunkt
-   Verwaltungspunkt
-   Dienstverbindungspunkt

Diese Installation kann den Standortsystemserver in den Zustand „Ausstehender Neustart“ versetzen und Fehler an die Configuration Manager-Komponentenstatusanzeige melden. Darüber hinaus treten bei .NET-Anwendungen auf dem Server gelegentlich Fehler auf, bis der Server neu gestartet wird.

Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).

**Überprüfen Sie die Version des Windows Assessment and Deployment Kit (ADK) für Windows 10** Das ADK für Windows 10 sollte Version 1607 oder höher haben. Wenn Sie das ADK aktualisieren müssen, sollten Sie dies vor dem Update von Configuration Manager machen. So wird sichergestellt, dass die Standardstartabbilder automatisch auf die neueste Version der Windows PE aktualisiert werden. (Benutzerdefinierte Startabbilder müssen manuell aktualisiert werden.)

Wenn Sie den Standort vor dem Update des ADKs aktualisieren, finden Sie unter [Configuration Manager and the Windows ADK for Windows 10, version 1607 (Configuration Manager und das Windows ADK für Windows 10, Version 1607)](https://blogs.technet.microsoft.com/enterprisemobility/2016/09/09/configuration-manager-and-the-windows-adk-for-windows-10-version-1607/) ein Skript zum erneuten Generieren der Startabbilder.

**Prüfen Sie den Standort- und Hierarchiestatus, und stellen Sie sicher, dass keine ungelösten Probleme vorliegen:** Bevor Sie das Update für einen Standort durchführen, sollten Sie alle Betriebsprobleme beheben, die den Standortserver, den Standortdatenbankserver und die auf Remotecomputern installierten Standortsystemrollen betreffen. Betriebsprobleme können die Ursache für Fehler beim Update von Standorten sein.

Weitere Informationen finden Sie unter [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Überprüfen Sie die Datei- und Datenreplikation zwischen Standorten:**   
Stellen Sie sicher, dass die Datei- und Datenreplikation zwischen Standorten betriebsbereit und aktuell ist. Verzögerungen oder Rückstände können ein reibungsloses und erfolgreiches Update verhindern.
Für die Datenbankreplikation können Sie die Replikationslinkanalyse verwenden, um Probleme vor Beginn des Updates zu lösen.

Weitere Informationen finden Sie unter [Informationen zur Replikationslinkanalyse](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) im Thema [Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure).

**Installieren Sie alle anwendbaren wichtigen Updates für Betriebssysteme auf Computern, auf denen der Standort gehostet wird, auf dem Standortdatenbankserver und auf Remote-Standortsystemrollen:** Installieren Sie vor der Installation eines Updates für Configuration Manager alle wichtigen Updates für jedes relevante Standortsystem. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Computer neu, bevor Sie mit dem Upgrade beginnen.

**Deaktivieren Sie Datenbankreplikate für Verwaltungspunkte an primären Standorten:**   
Configuration Manager kann kein Update eines primären Standorts durchführen, wenn dort Datenbankreplikate für Verwaltungspunkte aktiviert sind. Deaktivieren Sie die Datenbankreplikation, bevor Sie ein Update für Configuration Manager installieren.

Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Legen Sie SQL Server Always On-Verfügbarkeitsgruppen auf manuelles Failover fest:**   
Wenn Sie eine Verfügbarkeitsgruppe verwenden, stellen Sie sicher, dass diese auf „Manuelles Failover“ festgelegt ist, bevor Sie mit der Installation des Updates beginnen. Nachdem der Standort aktualisiert wurde, können Sie wieder auf „Automatisches Failover“ umstellen. Weitere Informationen finden Sie unter [SQL Server AlwaysOn für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

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

**Planen von Pilottests für Clients:**   
Bei der Installation eines Updates, das den Client aktualisiert, können Sie das neue Clientupdate in der Präproduktionsphase testen, bevor es bereitgestellt wird und all Ihre aktiven Clients aktualisiert.

Um diese Option zu nutzen, müssen Sie Ihren Standort für die Unterstützung automatischer Updates für die Präproduktionsphase konfigurieren, bevor Sie die Installation des Updates starten.

Weitere Informationen finden Sie unter [Aktualisieren von Clients in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) und [Testen von Clientupgrades in einer Präproduktionssammlung in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Mithilfe von Dienstfenstern können Sie planen, wann Standortserver Updates an einem Standort installieren:**   
Definieren Sie mithilfe von Dienstfenstern einen Zeitraum definieren, in dem Updates an einem Standortserver installiert werden können.

Damit können Sie steuern, wann das Update an Standorten in Ihrer Hierarchie installiert werden kann. Weitere Informationen finden Sie unter [Dienstfenster für Standortserver](/sccm/core/servers/manage/service-windows).

**Führen Sie die Setup-Voraussetzungsprüfung aus:**   
Wenn das Update in der Konsole als **verfügbar** aufgeführt wird, können Sie die Voraussetzungsprüfung vor der Installation des Updates unabhängig ausführen. (Beim Installieren des Updates am Standort wird die Voraussetzungsprüfung erneut ausgeführt.)

Um eine Voraussetzungsprüfung von der Konsole aus durchzuführen, wechseln Sie zu **Verwaltung > Übersicht > Clouddienste > Updates und Wartung**. Klicken Sie als Nächstes mit der rechten Maustaste auf das **Updatepaket für Configuration Manager 1706**, und wählen Sie dann **Voraussetzungsprüfung ausführen** aus.

Weitere Informationen zum Starten und anschließenden Überwachen der Voraussetzungsprüfung finden Sie unter **Schritt 3: Ausführen der Voraussetzungsprüfung vor der Installation eines Updates** im Thema [Installieren konsoleninterner Updates für System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Wenn die Voraussetzungsprüfung im Rahmen einer Updateinstallation oder unabhängig davon ausgeführt wird, werden vom Prozess einige Produktquelldateien aktualisiert, die für Standortwartungstasks verwendet werden. Wenn Sie daher nach Durchführung der Voraussetzungsprüfung, aber vor Installation des Updates einen Standortwartungstask durchführen müssen, führen Sie **Setupwpf.exe** (Configuration Manager-Setup) im Ordner „CD.Latest“ auf dem Standortserver aus.

**Standorte aktualisieren:**   
Sie können nun die Updateinstallation für Ihre Hierarchie starten. Weitere Informationen zum Installieren des Updates finden Sie unter [Installieren konsoleninterner Updates](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

Es wird empfohlen, die Installation des Updates für jeden Standort außerhalb der normalen Geschäftszeiten zu planen, wenn die Installation des Updates und die zugehörigen Aktionen zum Neuinstallieren von Standortkomponenten und Standortsystemrollen die geringsten Auswirkungen auf die Geschäftsvorgänge haben.

Weitere Informationen finden Sie unter [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="post-update-checklist"></a>Checkliste: Was Sie nach dem Update beachten müssen
Schauen Sie sich folgende Maßnahmen an, die Sie nach dem Abschluss des Updates ergreifen müssen.
1.  Stellen Sie sicher, dass die Replikation zwischen Standorten aktiviert ist. Schauen Sie sich in der Konsole **Überwachung** > **Standorthierarchie** und **Überwachung** > **Datenbankreplikation** an, um Hinweise auf Probleme zu erkennen und sicherzugehen, dass Replikationslinks aktiviert sind.
2.  Stellen Sie sicher, dass jeder Standortserver und jede Standortsystemrolle auf Version 1706 aktualisiert wurde. Sie können in der Konsole die optionale Spalte **Version** zur Anzeige mancher Knoten, wie z.B. **Standorte** und **Verteilungspunkte**, hinzufügen.

 Wenn dies nötig ist, wird eine Standortsystemrolle automatisch erneut installiert, um sie auf die neueste Version zu aktualisieren. Ziehen Sie in Erwägung, remote Standortsysteme erneut zu starten, wenn diese nicht erfolgreich aktualisiert werden konnten.
3.  Konfigurieren Sie Datenbankreplikate für Verwaltungspunkte an primären Standorten neu, die Sie vor dem Beginn des Updates deaktiviert haben.
4.  Konfigurieren Sie Datenbankwartungsaufgaben neu, die Sie vor dem Beginn des Updates deaktiviert haben.
5.  Wenn Sie Pilottests für Client vor der Installation des Updates konfiguriert haben, aktualisieren Sie Clients anhand des Plans, den Sie erstellt haben.

## <a name="known-issues"></a>Bekannte Probleme 
Nach der Aktualisierung auf Version 1706 wird bei jedem Start von SMS_Executive durch SMS_CERTIFICATE_MANAGER die folgende Warnmeldung zum Status erstellt:
-    Microsoft SQL Server reported SQL message 515, severity 16: [23000][515][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot insert the value NULL into column 'RowVersion', table 'CM_GF1.dbo.AAD_SecretChange_Notify'; column does not allow nulls. INSERT fails. (Microsoft SQL Server meldete SQL 515, Schweregrad 16: [23000][515][Microsoft][SQL Server Native Client 11.0] [SQL Server] Der Wert NULL kann nicht in die Spalte 'RowVersion' der Tabelle 'CM_GF1.dbo.AAD_SecretChange_Notify;' eingefügt werden, da in der Spalte keine Nullen zulässig sind. INSERT ist fehlgeschlagen.)

Diese Meldung können Sie Ignorieren.  Sie tritt auf, wenn vor dem Update auf Version 1706 keine Clouddienste für die Nutzung konfiguriert wurden. Dieses Problem wird in einer zukünftigen Version behoben.
