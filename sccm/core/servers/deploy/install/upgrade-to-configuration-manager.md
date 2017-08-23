---
title: Upgrade auf System Center Configuration Manager | Microsoft-Dokumentation
description: "Erfahren Sie die Schritte für die Ausführung eines direkten Upgrades an einem Standort und einer Hierarchie, wo System Center 2012 Configuration Manager ausgeführt wird."
ms.custom: na
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: "21"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1166b739e1e8d667172d97883f484fdbc3a142c1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-to-system-center-configuration-manager"></a>Upgrade auf System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können ein direktes Upgrade zur Aktualisierung auf System Center Configuration Manager von einem Standort und einer Hierarchie ausführen, wo System Center 2012 Configuration Manager ausgeführt wird.  

 Vor dem Upgrade von System Center 2012 Configuration Manager müssen Sie die Standorte vorbereiten. Dazu müssen Sie bestimmte Konfigurationen entfernen, die ein erfolgreiches Upgrade verhindern könnten, und dann die Upgradeschritte ausführen, wenn mehr als ein einzelner Standort beteiligt ist.  

 > [!TIP]
 > Beim Verwalten des System Center Configuration Manager-Standorts und der Hierarchieinfrastruktur werden die Begriffe *Upgrade*, *Update* und *Installation* verwendet, um drei verschiedene Konzepte zu beschreiben. Erfahren Sie mehr über die Verwendung der Begriffe unter [Informationen zu Upgrade, Update und Installation für einen Standort und eine Hierarchieinfrastruktur](/sccm/core/understand/upgrade-update-install).

##  <a name="bkmk_path"></a> Pfade für ein direktes Upgrade  

**Upgrade auf Version 1702**   
Wenn Sie über das Baselinemedium für Version 1702 verfügen, können Sie die folgenden Versionen und Installationen auf eine vollständig lizenzierte Version von System Center Configuration Manager Version 1702 aktualisieren:   
-     Eine Evaluierungsinstallation von System Center Configuration Manager Version 1702
-     System Center 2012 Configuration Manager mit Service Pack 1
-     System Center 2012 Configuration Manager mit Service Pack 2
-     System Center 2012 R2 – Configuration Manager
-     System Center 2012 R2 Configuration Manager mit Service Pack 1

**Upgrade auf Version 1606**  
Am 15. Dezember 2016 wurde das Baselinemedium für Version 1606 erneut veröffentlicht, um Unterstützung für zusätzliche Upgradeszenarios hinzufügen. Die neue Version unterstützt Upgrades der folgenden Versionen und Installationen auf eine vollständig lizenzierte Version von System Center Configuration Manager Version 1606:  
-   Eine Evaluierungsinstallation von System Center Configuration Manager Version 1606
-   Eine Release Candidate-Install von System Center Configuration Manager  
-   System Center 2012 Configuration Manager mit Service Pack 1  
-   System Center 2012 Configuration Manager mit Service Pack 2  
-   System Center 2012 R2 – Configuration Manager  
-   System Center 2012 R2 Configuration Manager mit Service Pack 1  

Wenn Sie ein vor dem 15. Dezember 2016 heruntergeladenes Baselinemedium für Version 1606 verwenden, können Sie nur die folgenden Versionen und Installationen auf eine vollständig lizenzierte Version von System Center Configuration Manager Version 1606 aktualisieren:
-   Eine Evaluierungsinstallation von System Center Configuration Manager Version 1606
-   System Center 2012 Configuration Manager mit Service Pack 2
-   System Center 2012 R2 Configuration Manager mit Service Pack 1

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  Wenn Sie das Upgrade für eine Version von System Center 2012 Configuration Manager auf Current Branch ausführen, können Sie den Upgradeprozess unter Umständen vereinfachen. Weitere Informationen finden Sie unter:  
>   
>  -   Der Abschnitt [Baseline und Update-Versionen](../../../../core/servers/manage/updates.md#bkmk_Baselines) unter [Updates für System Center Configuration Manager](../../../../core/servers/manage/updates.md)  
>  -   [Der Ordner „CD.Latest“ für System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **Folgendes wird nicht unterstützt:**  
-   Das Upgrade einer Technical Preview für System Center Configuration Manager auf eine vollständig lizenzierte Installation wird nicht unterstützt.  Eine Technical Preview-Version kann nur auf eine neuere Version der Technical Preview aktualisiert werden.  

-   Die Migration von einer Technical Preview auf eine vollständig lizenzierte Version wird nicht unterstützt.  

##  <a name="bkmk_checklist"></a> Checklisten zu Aktualisierungen  
 Die folgenden Checklisten helfen Ihnen bei der Planung einer erfolgreichen Aktualisierung auf System Center Configuration Manager.  

### <a name="before-you-upgrade"></a>Vor dem Upgrade  

**Überprüfen Sie Ihre System Center 2012 Configuration Manager-Umgebung**, und beheben Sie die in KB4018655, [Configuration Manager-Clients werden alle fünf Stunden aufgrund eines periodischen Wiederholungstasks neu installiert und, was zu einem unbeabsichtigten Clientupgrade führen kann](https://support.microsoft.com/help/4018655), beschriebenen Probleme.

**Stellen Sie sicher, dass Ihre Computerumgebung zu den unterstützten Konfigurationen** für ein Upgrade auf System Center Configuration Manager gehört:  

Überprüfen Sie die zum Hosten der Standortsystemrollen verwendeten Serverbetriebssysteme:  

-   Einige von System Center 2012 Configuration Manager unterstützte ältere Betriebssysteme werden von System Center Configuration Manager nicht unterstützt, und die Standortsystemrollen auf diesen Betriebssystemen müssen vor dem Upgrade verschoben oder entfernt werden. Lesen Sie die Dokumentation [Unterstützte Betriebssysteme für Standortsystemserver](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).   
-   Mit der Voraussetzungsprüfung für Configuration Manager werden die Voraussetzungen für Standortsystemrollen auf dem Standortserver oder auf Remotestandortsystemen nicht geprüft.  

Überprüfen Sie die Voraussetzungen für jeden Computer, auf dem eine Standortsystemrolle gehostet wird:  

-   Zum Bereitstellen eines Betriebssystems verwendet System Center Configuration Manager z.B. das Windows 10 Assessment and Deployment Kit (Windows ADK). Vor dem Ausführen von Setup müssen Sie Windows 10 ADK herunterladen und auf dem Standortserver sowie auf jedem Computer installieren, auf dem eine Instanz des SMS-Anbieters ausgeführt wird.  

Allgemeine Informationen über unterstützte Plattformen und die Konfiguration von Voraussetzungen finden Sie unter [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

Weitere Informationen zur Verwendung von Windows ADK mit Configuration Manager finden Sie unter [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung in System Center Configuration Manager](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

**Überprüfen des Standort- und Hierarchiestandorts, um ungelöste Probleme zu beheben:**  
Bevor Sie das Upgrade für einen Standort durchführen, sollten Sie alle Betriebsprobleme beheben, die den Standortserver, den Standortdatenbankserver und die auf Remotecomputern installierten Standortsystemrollen betreffen. Betriebsprobleme können die Ursache für Fehler beim Upgrade von Standorten sein.  

**Installieren aller anwendbaren wichtigen Updates für Betriebssysteme auf Computern, auf denen der Standort, der Standortdatenbankserver und die Remotestandort-Systemrollen gehostet werden:**  
Bevor Sie das Upgrade für einen Standort durchführen, sollten Sie für jedes relevante Standortsystem sämtliche wichtigen Updates installieren. Wenn für ein von Ihnen installiertes Update ein Neustart erforderlich ist, starten Sie die jeweiligen Computer neu, bevor Sie mit dem Service Pack-Update beginnen.  

Weitere Informationen erhalten Sie unter [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851).  

**Deinstallieren der Standortsystemrollen, die von System Center Configuration Manager nicht unterstützt werden:**  
Die folgenden Standortsystemrollen werden in System Center Configuration Manager nicht mehr verwendet und müssen deinstalliert werden, bevor Sie von System Center 2012 Configuration Manager upgraden:  

-   Out-of-Band-Verwaltungspunkt  
-   Systemintegritätsprüfungspunkt  

**Deaktivieren von Datenbankreplikaten für Verwaltungspunkte an primären Standorten:**  
Configuration Manager kann kein Upgrade eines primären Standorts durchführen, wenn dort Datenbankreplikate für Verwaltungspunkte aktiviert sind. Deaktivieren Sie die Datenbankreplikation, bevor Sie folgende Schritte ausführen:  

-   Erstellen einer Sicherung der Standortdatenbank zum Testen des Datenbankupgrades  
-   Upgrade des Produktionsstandorts auf System Center Configuration Manager  

Weitere Informationen finden Sie unter:  
-   System Center 2012 Configuration Manager: [Konfigurieren von Datenbankreplikaten für Verwaltungspunkte](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager: [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

**Erneutes Konfigurieren von Softwareupdatepunkten, die NLBs verwenden:**  
Configuration Manager kann kein Upgrade für Standorte durchführen, an denen Softwareupdatepunkte mithilfe eines NLB-Clusters gehostet werden.  

Wenn Sie für Softwareupdatepunkte NLB-Cluster verwenden, entfernen Sie den NLB-Cluster mithilfe von PowerShell. (Ab System Center 2012 Configuration Manager SP1 gab es in der Configuration Manager-Konsole keine Option zum Konfigurieren von NLB-Cluster)  

**Deaktivieren aller Standortwartungsaufgaben an allen Standorten für die Dauer des Standortupgrades:**  
Bevor Sie ein Upgrade auf System Center Configuration Manager durchführen, deaktivieren Sie alle Standortwartungstasks, die möglicherweise zu dem Zeitpunkt ausgeführt werden, zu dem der Upgradeprozess aktiv ist. Zu diesen Tasks gehören u. a. folgende:  

-   Standortserver sichern  
-   Veraltete Clientvorgänge löschen  
-   Veraltete Ermittlungsdaten löschen  

Wenn während des Upgradeprozesses ein Wartungstask für die Standortdatenbank ausgeführt wird, tritt beim Standortupgrade möglicherweise ein Fehler auf.  

Zeichnen Sie den Zeitplan eines Tasks vor dem Deaktivieren auf, sodass Sie die Konfiguration nach Abschluss des Standortupgrades wiederherstellen können.  

Weitere Informationen zu Standortwartungstasks finden Sie unter:  

-   System Center 2012 Configuration Manager: [Planen von Wartungstasks für Configuration Manager](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center Configuration Manager: [Referenz für Wartungstasks für System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md)  

**Führen Sie die Setup-Voraussetzungsprüfung aus.**:  
Bevor Sie das Upgrade für einen Standort durchführen, können Sie die **Voraussetzungsprüfung** unabhängig von Setup ausführen, um zu prüfen, ob Ihr Standort die Voraussetzungen erfüllt. Beim späteren Durchführen des Upgrades wird die Voraussetzungsprüfung erneut ausgeführt.  

Wenn Sie das Baselinemedium für Version 1606 aus der Oktober 2016-Version verwenden, durchsucht die unabhängige Voraussetzungsprüfung die Website nach Upgrades für die Current Branch-Version und die Long-Term Servicing Branch-Version (LTSB) von System Center Configuration Manager. Da einige Funktionen nicht von der LTSB-Version unterstützt werden, werden möglicherweise im Protokoll *ConfigMgrPrereq.log*-Einträge wie die folgenden angezeigt:
 - INFO: The site is a LTSB edition. (Info: Die Website ist eine LTSB-Edition.)
 - Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. (Nicht unterstützte Standortsystemrolle „Asset Intelligence-Synchronisierungspunkt“ für die LTSB-Edition;...Fehler;...Configuration Manager hat eine Installation von „Asset Intelligence-Synchronisierungspunkt“ erkannt.) Asset Intelligence is not supported on the LTSB edition. (Asset Intelligence wird auf der LTSB-Edition nicht unterstützt.) You must uninstall the Asset Intelligence synchronization point site system role before you can continue. (Sie müssen die Synchronisierungspunkt-Standortsystemrolle von Asset Intelligence deinstallieren, bevor Sie fortfahren können.)

Wenn Sie ein Upgrade auf die Current Branch-Version planen, können Fehler für die LTSB-Edition einfach ignoriert werden. Sie sind nur dann relevant, wenn Sie ein Upgrade auf die LTSB-Edition planen.

Wenn Sie später Configuration Manager-Setup für das Upgrade ausführen, wird die Voraussetzungsprüfung erneut ausgeführt und bewertet Ihren Standort auf der Basis der Branch-Version von System Center Configuration Manager, die Sie installieren möchten (Current Branch oder LTSB). Wenn Sie sich für ein Upgrade auf die Current Branch-Version entscheiden, wird die Prüfung von Features, die nicht von der LTSB-Edition unterstützt werden, nicht ausgeführt.

Weitere Informationen finden Sie unter [Voraussetzungsprüfung für System Center Configuration Manager](/sccm/core/servers/deploy/install/prerequisite-checker) und in der [Liste der Voraussetzungsprüfungen für System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

**Herunterladen von Dateien für die Voraussetzungsprüfung sowie von weitervertreibbaren Dateien für System Center Configuration Manager:**    
Verwenden Sie das **Setup-Downloadprogramm**, um die erforderlichen weitervertreibbaren Dateien, die Sprachpakete und die neuesten Produktupdates für System Center Configuration Manager herunterzuladen.  

Informationen hierzu finden Sie unter [Setup-Downloadprogramm für System Center Configuration Manager](/sccm/core/servers/deploy/install/setup-downloader).  

**Planen Sie die Verwaltung von Server- und Clientsprachen ein.**:  
Beim Aktualisieren eines Standorts werden nur die Sprachpaketversionen installiert, die Sie während des Upgrades auswählen.  

-   Setup überprüft die aktuelle Sprachkonfiguration Ihres Standorts. Es wird ermittelt, welche Sprachpakete in dem Ordner verfügbar sind, in dem die zuvor heruntergeladenen erforderlichen Dateien gespeichert wurden.  
-   Anschließend können Sie die Auswahl der aktuellen Server- und Clientsprachpakete bestätigen oder diese ändern und die Unterstützung von Sprachen hinzufügen oder entfernen.  
-   Nur die Sprachpakete, die beim Ausführen von Setup verfügbar sind (die Sie mit den erforderlichen heruntergeladenen Dateien erhalten), können ausgewählt werden.  

> [!NOTE]  
>  Sie können die Sprachpakete aus System Center 2012 Configuration Manager nicht verwenden, um Sprachen für einen System Center Configuration Manager-Standort zu aktivieren.  

Weitere Informationen zu Sprachpaketen finden Sie unter [Sprachpakete in System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

**Sehen Sie sich die Überlegungen zum Upgrade von Standorten an.**:  
Wenn Sie ein Upgrade für einen Standort durchführen, werden einige Funktionen und Konfigurationen auf die Standardkonfiguration zurückgesetzt. Informationen zur Vorbereitung auf diese und ähnliche Änderungen finden Sie unter  [Upgradeüberlegungen](#bkmk_considerations).  

**Erstellen einer Sicherung der Standortdatenbank am Standort der zentralen Verwaltung und an primären Standorten:**  
Bevor Sie das Upgrade für einen Standort durchführen, sollten Sie die Standortdatenbank sichern, damit Sie über eine Sicherung für die Notfallwiederherstellung verfügen.  

Informationen finden Sie unter [Sicherung und Wiederherstellung für System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

**Erstellen Sie eine Sicherung der benutzerdefinierten Datei „Configuration.mof“**:  
Wenn Sie eine benutzerdefinierte Datei „Configuration.mof“ verwenden, um die bei der Hardwareinventur verwendeten Datenklassen zu definieren, müssen Sie vor dem Upgrade des Standorts eine Sicherung dieser Datei erstellen. Nach dem Upgrade stellen Sie diese Datei an dem Standort wieder her. Weitere Informationen zur Verwendung dieser Datei finden Sie unter [Erweitern der Hardwareinventur in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

**Testen des Datenbank-Upgradeprozesses mit einer Kopie der letzten Sicherung der Standortdatenbank:**  
Bevor Sie das Upgrade für einen Standort der zentralen Verwaltung oder einen primären Standort von Configuration Manager durchführen, testen Sie den Datenbankupgradeprozess mit einer Kopie der letzten Sicherung der Standortdatenbank.  

-   Sie sollten den Standortdatenbank-Upgradeprozess testen, da die Standortdatenbank während der Aktualisierung eines Standorts geändert werden kann.  
-   Ein Testdatenbankupgrade ist zwar nicht erforderlich, doch können dadurch Probleme beim Upgrade ermittelt werden, bevor die Produktionsdatenbank betroffen ist.  
-   Wenn beim Upgrade einer Standortdatenbank Fehler auftreten, ist die Datenbank möglicherweise nicht mehr betriebsfähig, und es müsste eine Standortwiederherstellung erfolgen.  
-   Obwohl die Standortdatenbank von allen Standorten in einer Hierarchie gemeinsam genutzt wird, sollten Sie die Datenbank an jedem relevanten Standort testen, bevor Sie das Upgrade für diesen Standort durchführen.  
-   Wenn Sie an einem primären Standort Datenbankreplikate für Verwaltungspunkte verwenden, deaktivieren Sie die Replikation, bevor Sie die Sicherung der Standortdatenbank erstellen.  

Configuration Manager unterstützt weder die Sicherung sekundärer Standorte noch das Testupgrade einer sekundären Standortdatenbank.  

Das Testen des Datenbankupgrades für die Datenbank des Produktionsstandorts wird nicht unterstützt. Dadurch würde ein Upgrade der Standortdatenbank durchgeführt, und Ihr Standort wäre möglicherweise nicht mehr betriebsfähig.  

Weitere Informationen finden Sie unter [Testen des Standortdatenbankupgrades](#bkmk_test).  

**Erneutes Starten des Standortservers und aller Computer, auf denen eine Standortsystemrolle gehostet wird:**  
Damit können Sie sicherstellen, dass keine Aktionen aus kürzlich durchgeführten Installationen von Updates oder hinsichtlich der Voraussetzungen mehr ausstehen. Es handelt sich um einen internen Prozess, der unternehmensspezifisch ist.  

**Aktualisieren Sie Standorte.**:  
Beginnen Sie mit dem Standort der obersten Ebene in der Hierarchie, und führen Sie „Setup.exe“ aus dem Quellmedium von System Center Configuration Manager aus.  

Wenn das Upgrade am Standort der obersten Ebene abgeschlossen ist, können Sie mit dem Upgrade der untergeordneten Standorte beginnen. Schließen Sie jeweils das Upgrade eines Standorts ab, bevor Sie das Upgrade des nächsten Standorts durchführen.  

Bis für alle Standorte in der Hierarchie das Upgrade auf System Center Configuration Manager durchgeführt wurde, erfolgt der Betrieb im gemischten Versionsmodus.  

Informationen zum Ausführen des Upgrades finden Sie unter [Aktualisieren Sie Standorte](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Nach dem Upgrade  
**Upgrade der eigenständigen Configuration Manager-Konsolen**:  
Standardmäßig wird beim Upgrade eines Standorts der zentralen Verwaltung oder eines primären Standorts auch für eine auf dem Standortserver installierte Configuration Manager-Konsole ein Upgrade ausgeführt. Allerdings müssen Sie für jede Konsole, die auf einem anderen Computer als dem Standortserver installiert ist, ein manuelles Upgrade ausführen.  

> [!TIP]  
>  Schließen Sie vor dem Starten des Upgrades jede geöffnete Konsole.  

Weitere Informationen finden Sie unter [Install System Center Configuration Manager consoles](../../../../core/servers/deploy/install/install-consoles.md) (Installieren von System Center Configuration Manager-Konsolen).  

**Neukonfigurieren von Datenbankreplikaten für Verwaltungspunkte an primären Standorten:**  
Beim Verwenden von Datenbankreplikaten für Verwaltungspunkte an primären Standorten müssen Sie die Datenbankreplikate deinstallieren, bevor Sie den Standort aktualisieren. Konfigurieren Sie das Datenbankreplikat für Verwaltungspunkte nach dem Upgrade eines primären Standorts neu.   
Weitere Informationen finden Sie unter  [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Erneutes Konfigurieren von Datenbankwartungsaufgaben, die Sie vor dem Upgrade deaktiviert haben:**  
Wenn Sie die Datenbank-[Referenz für Wartungstasks für System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) vor dem Upgrade an einem Standort deaktiviert haben, konfigurieren Sie diese Tasks an dem Standort mithilfe der vor dem Upgrade verwendeten Einstellungen neu.  

**Aktualisieren Sie Clients.**:  
Nach der Aktualisierung aller Standorte auf System Center Configuration Manager planen Sie das Upgraden von Clients.  

Wenn Sie ein Upgrade für einen Client ausführen, wird die aktuelle Clientsoftware deinstalliert und die neue Version der Clientsoftware installiert. Für Upgrades von Clients können Sie ein beliebiges Verfahren verwenden, das von Configuration Manager unterstützt wird.  

> [!TIP]  
>  Wenn Sie für den Standort der obersten Ebene einer Hierarchie ein Upgrade durchführen, wird das Clientinstallationspaket auf den einzelnen Verteilungspunkten der Hierarchie ebenfalls aktualisiert. Beim Upgrade eines primären Standorts wird das Clientupgradepaket aktualisiert, das vom primären Standort zur Verfügung gestellt wird.  

Informationen zum Ausführen eines Upgrades für vorhandene Clients und zum Installieren neuer Clients finden Sie unter [Aktualisieren von Clients für Windows-Computer in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

##  <a name="bkmk_considerations"></a> Upgradeüberlegungen  
**Automatische Aktionen:**  
Wenn Sie ein Upgrade auf System Center Configuration Manager durchführen, werden die folgenden Aktionen automatisch ausgeführt:  

-   Vom Standort wird eine Standortrücksetzung ausgeführt, die auch eine Neuinstallation aller Standortsystemrollen umfasst.  
-   Wenn es sich bei dem Standort um den Standort der obersten Ebene einer Hierarchie handelt, wird das Clientinstallationspaket auf allen Verteilungspunkten der Hierarchie aktualisiert. Vom Standort werden auch die Standardstartabbilder aktualisiert, sodass die neue Windows PE-Version verwendet wird, die in Windows Assessment and Deployment Kit 10 enthalten ist. Beim Durchführen des Upgrades werden vorhandene Medien jedoch nicht für die Verwendung mit der Abbildbereitstellung aktualisiert.  
-   Wenn es sich bei dem Standort um einen primären Standort handelt, wird das Clientupgradepaket für den Standort aktualisiert.  

**Manuelle Aktionen für den Administrator nach einem Upgrade:**   
Nachdem Sie für einen Standort ein Upgrade ausgeführt haben, müssen Sie sicherstellen, dass die folgenden Aktionen durchgeführt werden:  

-   Vergewissern Sie sich, dass auf Clients, die den einzelnen primären Standorten zugewiesen sind, das Upgrade ausgeführt und die Clientsoftware für die neue Version installiert wird.  
-   Führen Sie ein Upgrade für jede Configuration Manager-Konsole aus, die eine Verbindung zum Standort herstellt und auf einem Computer ausgeführt wird, der sich gegenüber dem Standortserver an einem Remotestandort befindet.  
-   Konfigurieren Sie die Datenbankreplikate an den primären Standorten neu, an denen Sie Datenbankreplikate für Verwaltungspunkte verwenden.  
-   Nach dem Upgrade des Standorts müssen Sie physische Medien wie ISO-Dateien für CDs und DVDs, USB-Flashlaufwerke, oder vorab bereitgestellte für Windows To Go-Bereitstellungen verwendete oder für Hardwarehersteller bereitgestellte Medien manuell aktualisieren. Obwohl durch das Upgrade die standardmäßigen Startimages aktualisiert werden, werden diese von Configuration Manager extern verwendeten Mediendateien nicht upgegradet.  
-   Planen Sie die Aktualisierung von nicht standardmäßigen Startabbildern ein, wenn die ursprüngliche (ältere) Version von Windows PE nicht erforderlich ist.  

**Aktionen, die sich auf Konfigurationen und Einstellungen auswirken:**   
Wenn für einen Standort ein Upgrade auf System Center Configuration Manager durchgeführt wird, werden einige Konfigurationen und Einstellungen nach dem Upgrade nicht beibehalten oder auf eine neue Standardkonfiguration festgelegt. Die folgende Tabelle enthält Einstellungen, die nicht beibehalten oder geändert werden, und Details zur damit verbundenen Planung während des Upgrades eines Standorts:  

-   **Softwarecenter:**  
    Die folgenden Elemente des Softwarecenters werden auf ihre Standardwerte zurückgesetzt:  
    -   Die Option**Arbeitsinformationen** wird auf die Geschäftszeiten **5:00** bis **22:00** Monday bis Friday.  
    -   Der Wert für **Computerwartung** wird auf **Softwarecenter-Aktivitäten anhalten, wenn sich der Computer im Präsentationsmodus befindet**festgelegt.  
    -   Der Wert für **Remotesteuerung** wird auf den Wert in den Clienteinstellungen festgelegt, die dem Computer zugewiesen sind.  
-   **Zeitpläne für Softwareupdate-Zusammenfassung:**  
     Benutzerdefinierte Zusammenfassungszeitpläne für Softwareupdates oder Softwareupdategruppen werden auf den Standardwert von einer Stunde zurückgesetzt. Setzen Sie benutzerdefinierte Zusammenfassungswerte nach Abschluss des Upgrades auf die erforderliche Häufigkeit zurück.  

##  <a name="bkmk_test"></a> Testen des Standortdatenbankupgrades  
Die folgenden Informationen gelten nur, wenn Sie eine vorherige Version wie System Center 2012 Configuration Manager auf System Center Configuration Manager aktualisieren.

Bevor Sie das Upgrade eines Standorts durchführen, sollten Sie es anhand einer Kopie der Datenbank dieses Standorts testen.  

Zum Testen der Datenbank für ein Upgrade stellen Sie zunächst eine Kopie der Standortdatenbank auf einer Instanz von SQL Server wieder her, von der kein Configuration Manager-Standort gehostet wird. Zum Hosten der Datenbankkopie müssen Sie eine Version von SQL Server verwenden, die von der Version von Configuration Manager, die Quelle der Datenbank ist, unterstützt wird.  

Führen Sie nach dem Wiederherstellen der Standortdatenbank auf dem SQL Server-Computer das Configuration Manager-Setup aus dem System Center Configuration Manager-Ordner auf dem Quellmedium aus. Verwenden Sie dazu die Befehlszeilenoption **/TESTDBUPGRADE**.  

-   Weitere Informationen über das Erstellen und Wiederherstellen der Sicherung einer Standortdatenbank erhalten Sie unter [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md) (Befehlszeilenoption für Setup).  
-   Informationen über die Befehlszeilenoption **/TESTDBUPGRADE** bietet die Tabelle im unter [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md) (Befehlszeilenoption für Setup).  
-   Weitere Informationen über die unterstützten SQL Server-Versionen finden Sie unter [Unterstützung für SQL Server-Versionen für System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!TIP]  
>  Wenn Sie Microsoft Intune mit Configuration Manager integrieren:  
>   
>  Wenn Sie ein Testdatenbankupgrade für eine Kopie der Standortdatenbank ausführen, die mindestens 5 Tage alt ist, wird möglicherweise eine der folgenden Meldungen angezeigt:  
>   
>  -   WARNUNG: Upgrade erzwingt eine vollständige Synchronisierung mit der Cloud.  
>  -   FEHLER: Datenbankupgrade erzwingt eine vollständige Synchronisierung mit der Cloud.  
>   
> Beide Meldungen können während des Tests eines Datenbankupgrades ohne weitere Auswirkungen ignoriert werden, da sie nicht auf Fehler oder Probleme mit dem Testupgrade hinweisen. Stattdessen zeigen sie an, dass während des tatsächlichen Upgrades Daten aus der Datenbankreplikationsgruppe **Cloud** möglicherweise mit Microsoft Intune synchronisiert werden.  

Führen Sie für alle Standorte der zentralen Verwaltung sowie für alle primären Standorte, für die ein Upgrade geplant ist, folgende Schritte aus.  

#### <a name="to-test-a-site-database-for-upgrade"></a>So testen Sie eine Standortdatenbank für ein Upgrade  

1.  Erstellen Sie eine Kopie der Standortdatenbank. Stellen Sie diese Kopie dann auf einer Instanz von SQL Server wieder her, deren Edition der von der Standortdatenbank verwendeten entspricht und von der kein Configuration Manager-Standort gehostet wird. Wird auf der Standortdatenbank beispielsweise eine Instanz der Enterprise Edition von SQL Server ausgeführt, muss die Datenbank auf einer Instanz von SQL Server wiederhergestellt werden, auf der ebenfalls die Enterprise Edition von SQL Server ausgeführt wird.  

2.  Nach der Wiederherstellung der Datenbankkopie führen Sie das Setup vom Quellmedium der System Center Configuration Manager-Version aus. Verwenden Sie beim Ausführen von Setup die Befehlszeilenoption **/TESTDBUPGRADE** . Handelt es sich bei der SQL Server-Instanz, von der die Datenbankkopie gehostet wird, nicht um die Standardinstanz, müssen Sie auch die Befehlszeilenargumente angeben. Damit können Sie ermitteln, von welcher Instanz die Kopie der Standortdatenbank gehostet wird.  

     Angenommen, Sie planen das Upgrade einer Standortdatenbank namens „SMS_ABC“. Sie stellen eine Kopie dieser Standortdatenbank auf einer unterstützten Instanz von SQL Server wieder her, die Sie „DBTest“ genannt haben. Verwenden Sie folgende Befehlszeile, um ein Upgrade dieser Kopie der Standortdatenbank zu testen: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Die Datei „Setup.exe“ befindet sich auf dem Quellmedium für System Center Configuration Manager an folgendem Speicherort: **SMSSETUP\BIN\X64**.  

3.  Überprüfen Sie den Fortschritt und den Erfolg des Upgrades auf der Instanz von SQL Server, auf der Sie den Test ausführen. Die nötigen Angaben dazu finden Sie in der Datei ConfigMgrSetup.log im Stamm des Systemlaufwerks:  

    -   Wenn beim Testen des Upgrades Fehler auftreten, beheben Sie die Probleme, die mit dem Upgrade der Standortdatenbank in Verbindung stehen. Erstellen Sie eine neue Sicherung der Standortdatenbank, und testen Sie anschließend das Upgrade der neuen Kopie der Standortdatenbank.  
    -   Wenn der Prozess erfolgreich abgeschlossen ist, können Sie die Datenbankkopie löschen.  

        > [!NOTE]  
        >  Es wird nicht unterstützt, die für den Upgradetest verwendete Kopie der Datenbank mit dem Ziel der Verwendung als Standortdatenbank wiederherzustellen.  

Nachdem Sie für eine Kopie der Standortdatenbank erfolgreich ein Upgrade durchgeführt haben, fahren Sie mit dem Upgrade des Configuration Manager-Standorts und dessen Standortdatenbank fort.  

##  <a name="bkmk_upgrade"></a> Aktualisieren Sie Standorte.  
Wenn Sie die Konfigurationen vor dem Upgrade für Ihren Standort abgeschlossen sowie das Upgrade der Standortdatenbank an einer Datenbankkopie getestet und die für die geplante Service Pack-Installation erforderlichen Dateien und Sprachpakete heruntergeladen haben, können Sie das Upgrade für Ihren Configuration Manager-Standort durchführen.  

Beim Durchführen eines Upgrades für einen Standort in einer Hierarchie führen Sie als Erstes ein Upgrade für den Standort der obersten Ebene der Hierarchie durch. Bei dem Standort der obersten Ebene handelt es sich entweder um einen Standort der zentralen Verwaltung oder um einen eigenständigen primären Standort. Wenn das Upgrade des Standorts der zentralen Verwaltung abgeschlossen ist, können Sie für die untergeordneten primären Standorte in beliebiger Reihenfolge Upgrades durchführen. Nach dem Durchführen eines Upgrades für einen primären Standort können Sie für dessen untergeordnete sekundäre Standorte oder für zusätzliche primäre Standorte ein Upgrade durchführen, bevor Sie sekundäre Standorte aktualisieren.  

Führen Sie Setup über das System Center Configuration Manager-Quellmedium aus, um ein Upgrade für einen Standort der zentralen Verwaltung oder einen primären Standort durchzuführen. Für ein Upgrade sekundärer Standorte führen Sie dagegen Seutp nicht aus. Stattdessen verwenden Sie die Configuration Manager-Konsole, um das Upgrade eines sekundären Standorts durchzuführen, nachdem das Upgrade des primären übergeordneten Standorts abgeschlossen ist.  

Schließen Sie die auf dem Standortserver installierte Configuration Manager-Konsole, bevor Sie das Upgrade eines Standorts durchführen, bis dieses abgeschlossen ist. Schließen Sie außerdem jede Configuration Manager-Konsole, die auf anderen Computern als dem Standortserver ausgeführt wird. Sie können die Konsole nach Abschluss des Upgrades wieder verbinden. Bis Sie allerdings das Upgrade einer Configuration Manager-Konsole auf die neue Configuration Manager-Version durchführen, können in dieser Konsole nicht alle Objekte und Informationen angezeigt werden, die in der neuen Configuration Manager-Version verfügbar sind.  

Verwenden Sie die folgenden Verfahren zum Aktualisieren von Configuration Manager-Standorten:  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>So führen Sie ein Upgrade für einen Standort der zentralen Verwaltung oder einen primären Standort durch  

1.  Überprüfen Sie, ob der Benutzer, der Setup ausführt, über die folgenden Sicherheitsrechte verfügt:  

    -   Lokale Administratorrechte auf dem primären Standortservercomputer  
    -   Lokale Administratorrechte auf dem Datenbankserver des Remotestandorts für den Standort, falls es sich um einen Remotestandort handelt    </br></br>

2.  Öffnen Sie auf dem Standortservercomputer den Windows-Explorer, und wechseln Sie zu **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**.  

3.  Doppelklicken Sie auf **Setup.exe**. Der Setup-Assistent für Configuration Manager wird geöffnet.  

4.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  

5.  Wählen Sie auf der Seite **Erste Schritte** die Option **Upgrade dieser Configuration Manager-Installation ausführen**, und klicken Sie dann auf **Weiter**.  

6.  Klicken Sie auf der Seite **Product Key** auf **Weiter**.  

     Wenn Sie zuvor eine Evaluierungsversion von Configuration Manager installiert haben, können Sie die Option **Lizenzierte Edition des Produkts installieren** auswählen und dann den Product Key für die vollständige Installation von Configuration Manager eingeben. Dadurch wird der Standort zur Vollversion konvertiert.  

     Seit der Veröffentlichung des Baselinemediums des System Center Configuration Manager-Release 1606 im Oktober 2016 können Sie das Ablaufdatum Ihres Software Assurance-Vertrags angeben. Sie haben auch die Möglichkeit, das **Ablaufdatum von Software Assurance** als praktische Erinnerung an dieses Datum anzugeben. Wenn Sie das Datum nicht während des Setups eingeben, können Sie es später in der Configuration Manager-Konsole angeben.

     >  [!NOTE]   
     >  Microsoft überprüft das angegebene Ablaufdatum nicht und verwendet es ebenso wenig, um die Lizenz zu überprüfen.  Stattdessen können Sie das Ablaufdatum angeben, um daran erinnert zu werden. Dies ist hilfreich, da Configuration Manager regelmäßig überprüft, ob neue Softwareupdates online angeboten werden, und Ihr Software Assurance-Lizenzstatus sollte aktuell sein, damit Sie von diesen zusätzlichen Updates profitieren können.    

     Weitere Informationen finden Sie unter [Lizenzierung und Branches für System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

7.  Lesen und akzeptieren Sie auf der Seite **Microsoft Software-Lizenzbedingungen** die Lizenzbedingungen, und klicken Sie anschließend auf **Weiter**.  

8.  Lesen und akzeptieren Sie auf der Seite **Lizenzen für erforderliche Komponenten** die Lizenzbedingungen für die erforderliche Software, und klicken Sie anschließend auf **Weiter**. Die Software wird gegebenenfalls heruntergeladen und automatisch auf Standortsystemen oder Clients installiert. Die nächste Seite wird erst angezeigt, nachdem Sie alle Kontrollkästchen aktiviert haben.  

9. Geben Sie auf der Seite **Download der Voraussetzungskomponenten** an, ob die aktuellsten Voraussetzungen, Sprachpakete und Produktupdates aus dem Internet heruntergeladen oder bereits heruntergeladene Dateien verwendet werden sollen. Klicken Sie dann auf **Weiter**. Falls Sie bereits Dateien mit dem Setup-Downloadprogramm heruntergeladen haben, wählen Sie **Bereits heruntergeladene Dateien verwenden** aus, und geben Sie den Downloadordner an. Weitere Informationen finden Sie unter [Setup Downloader (Setup-Downloadprogramm)](/sccm/core/servers/deploy/install/setup-downloader).

    > [!NOTE]  
    >  Wenn Sie bereits heruntergeladene Dateien verwenden, überprüfen Sie, ob der Downloadordner die aktuellsten Dateiversionen enthält.  

10. Zeigen Sie auf der Seite **Serversprachauswahl** die Liste der Sprachen an, die zurzeit für den Standort installiert sind. Wählen Sie weitere Sprachen aus, die an diesem Standort für die Configuration Manager-Konsole sowie für Berichte verfügbar sind, oder entfernen Sie Sprachen, die an diesem Standort nicht mehr unterstützt werden sollen. Klicken Sie anschließend auf **Weiter**. Englisch ist standardmäßig aktiviert und kann nicht entfernt werden.  

    > [!IMPORTANT]  
    >  Jede Version von Configuration Manager kann keine Sprachpakete aus einer früheren Version von Configuration Manager verwenden. Soll die Unterstützung einer bestimmten Sprache an einem Configuration Manager-Standort aktiviert werden, der upgegradet wird, müssen Sie die Sprachpaketversion für die neue Softwareversion verwenden. Wenn beispielsweise während des Upgrades von System Center 2012 Configuration Manager auf System Center Configuration Manager die System Center Configuration Manager-Version eines Sprachpakets nicht unter den erforderlichen Dateien verfügbar ist, die Sie herunterladen, kann die Unterstützung für diese Sprache nicht installiert werden.  

11. Zeigen Sie auf der Seite **Clientsprachauswahl** die Liste der Sprachen an, die zurzeit für den Standort installiert sind. Wählen Sie weitere Sprachen aus, die an diesem Standort für Clientcomputer verfügbar sind, oder entfernen Sie Sprachen, die an diesem Standort nicht mehr unterstützt werden sollen. Geben Sie an, ob alle Clientsprachen für mobile Geräteclients aktiviert werden sollen. Klicken Sie dann auf **Weiter**. Englisch ist standardmäßig aktiviert und kann nicht entfernt werden.  

    > [!IMPORTANT]  
    >  Jede Version von Configuration Manager kann keine Sprachpakete aus einer früheren Version von Configuration Manager verwenden. Soll die Unterstützung einer bestimmten Sprache an einem Configuration Manager-Standort aktiviert werden, der upgegradet wird, müssen Sie die Sprachpaketversion für die neue Softwareversion verwenden. Wenn beispielsweise während des Upgrades von System Center 2012 Configuration Manager auf System Center Configuration Manager die System Center Configuration Manager-Version eines Sprachpakets nicht unter den erforderlichen Dateien verfügbar ist, die Sie herunterladen, kann die Unterstützung für diese Sprache nicht installiert werden.  

12. Klicken Sie auf der Seite **Zusammenfassung der Einstellungen** auf **Weiter** , um die Voraussetzungsprüfung zu starten und damit zu prüfen, ob der Server für das Upgrade des Standorts bereit ist.  

13. Klicken Sie auf der Seite **Voraussetzungsprüfung** auf **Weiter** , falls keine Probleme aufgeführt werden. Daraufhin wird das Upgrade des Standorts und der Standortsystemrollen durchgeführt. Wenn bei der Voraussetzungsprüfung ein Problem festgestellt wird, klicken Sie in der Liste auf einen Eintrag, um Details zur Behebung des Problems anzuzeigen. Sie können mit der Installation erst dann fortfahren, wenn alle in der Liste mit dem Status **Fehler** aufgeführten Elemente korrigiert wurden. Klicken Sie nach der Problembehebung auf **Prüfung ausführen** , um die Voraussetzungsprüfung zu wiederholen. Sie können die Ergebnisse der Voraussetzungsprüfung überprüfen, indem Sie die Datei ConfigMgrPrereq.log im Stamm des Systemlaufwerks öffnen. Die Protokolldatei enhält möglicherweise weitere Informationen, die nicht auf der Benutzeroberfläche angezeigt werden. Eine Liste der Regeln und Beschreibungen zu den Installationsvoraussetzungen finden Sie unter [Voraussetzungsprüfung](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

Auf der Seite **Upgrade** wird der Gesamtstatus der Installation angezeigt. Wenn die Hauptinstallation des Standortservers und des Standortsystems abgeschlossen ist, können Sie den Assistenten schließen. Die Standortkonfiguration wird im Hintergrund fortgesetzt.  

#### <a name="to-upgrade-a-secondary-site"></a>So führen Sie das Upgrade eines sekundären Standorts durch  

1.  Überprüfen Sie, ob der Administrator, der die Installation ausführt, über die folgenden Sicherheitsrechte verfügt:  

    -   Lokale Administratorrechte auf dem sekundären Standortcomputer  
    -   Sicherheitsrolle „Infrastrukturadministrator“ oder „Hauptadministrator“ am übergeordneten primären Standort  
    -   Systemadministratorrechte (SA) für die Standortdatenbank des sekundären Standorts  
    </br>
2.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

3.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

4.  Wählen Sie den sekundären Standort aus, für den Sie das Upgrade durchführen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Standort** auf **Upgrade**.  

5.  Klicken Sie zum Bestätigen auf **Ja** . Daraufhin wird das Upgrade des sekundären Standorts gestartet.  

Das Upgrade des sekundären Standorts erfolgt im Hintergrund. Nach Abschluss des Upgrades können Sie den Status in der Configuration Manager-Konsole bestätigen. Wenn Sie den Status bestätigen möchten, wählen Sie den Server des sekundären Standorts aus, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standort** auf **Installationsstatus anzeigen**.  

##  <a name="BKMK_PostUpgrade"></a> Ausführen der Aufgaben nach einem Upgrade  
Nachdem Sie für einen Standort ein Upgrade auf ein neues Service Pack durchgeführt haben, müssen Sie möglicherweise einige zusätzliche Aufgaben ausführen, um das Upgrade oder die Neukonfiguration des Standorts abzuschließen. Dazu zählt beispielsweise das Durchführen eines Upgrades von Configuration Manager-Clients oder Configuration Manager-Konsolen, das erneute Aktivieren von Datenbankreplikaten für Verwaltungspunkte oder das Wiederherstellen von Configuration Manager-Funktionen, die Sie verwenden und die nach dem Service Pack-Upgrade nicht beibehalten werden.  

**Bekannte Probleme bei sekundären Standorten:**  
- **Bei einem Upgrade auf Version 1511:** Um sicherzustellen, dass Clients auf sekundären Standorten den Verwaltungspunkt vom sekundären Standort (Proxyverwaltungspunkt) finden, fügen Sie den Verwaltungspunkt manuell zu Begrenzungsgruppen hinzu, die auch die Verteilungspunkte am sekundären Standort enthalten.  

- **Bei einem Upgrade auf Version 1606 oder höher:** Proxyverwaltungspunkte werden automatisch zu Begrenzungsgruppen hinzugefügt, die Verteilungspunkte am sekundären Standort enthalten.
