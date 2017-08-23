---
title: "Protokolldateien für Configuration Manager | Microsoft-Dokumentation"
description: Verwenden Sie Protokolldateien bei der Problembehandlung in einer System Center Configuration Manager-Hierarchie.
ms.custom: na
ms.date: 7/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 28597cf1cb269fff0872c7f79ef961496aea32ab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="log-files-in-system-center-configuration-manager"></a>Protokolldateien in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Von Client- und Standortserverkomponenten in System Center Configuration Manager werden Prozessinformationen in eigenen Protokolldateien aufgezeichnet. Mithilfe der Information in diesen Protokolldateien können Sie eventuell auftretende Probleme in Ihrer Configuration Manager-Hierarchie beheben. Die Client- und Serverkomponentenprotokollierung ist in Configuration Manager standardmäßig aktiviert.   

 In den folgenden Abschnitten finden Sie Details zu den verschiedenen verfügbaren Protokolldateien. Verwenden Sie diese Informationen, um Protokolldateien der Betriebsdetails für Configuration Manager-Clients und -Server anzuzeigen und zu überwachen und die Fehlerinformationen zu ermitteln, mit denen Sie jegliche Probleme beheben können.  

-   [Informationen zu Configuration Manager-Protokolldateien](#BKMK_AboutLogs)  

    -   [Konfigurieren der Protokollierungsoptionen mithilfe des Dienst-Managers für Configuration Manager](#BKMK_LogOptions)  

    -   [Suchen von Configuration Manager-Protokollen](#BKMK_LogLocation)  

-   [Configuration Manager-Clientprotokolle](#BKMK_ClientLogs)  

    -   [Clientvorgänge](#BKMK_ClientOpLogs)  

    -   [Protokolldateien zur Clientinstallation](#BKMK_ClientInstallLog)  

    -   [Client für Linux und UNIX](#BKMK_LogFilesforLnU)  

    -   [Client für Macintosh-Computer](#BKMK_LogfilesforMac)  

-   [Protokolldateien für Configuration Manager-Standortserver](#BKMK_ServerLogs)  

    -   [Protokolle für Standortserver und Standortsystemserver](#BKMK_SiteSiteServerLog)  

    -   [Protokolldateien zur Standortserverinstallation](#BKMK_SiteInstallLog)  

    -   [Protokolldateien für den Fallbackstatuspunkt](#BKMK_FSPLog)  

    -   [Protokolldateien für den Verwaltungspunkt](#BKMK_MPLog)  

    -   [Protokolldateien für den Softwareupdatepunkt](#BKMK_SUPLog)  

-   [Protokolldateien für Configuration Manager-Funktionen](#BKMK_FunctionLogs)  

    -   [Anwendungsverwaltung](#BKMK_AppManageLog)  

    -   [Asset Intelligence](#BKMK_AILog)  

    -   [Sicherung und Wiederherstellung:](#BKMK_BnRLog)  

    -   [Zertifikatregistrierung](#BKMK_CertificateEnrollment)

    -   [Clientbenachrichtigung](#BKMK_BGB)

    -   [Cloudverwaltungsgateway](#cloud-management-gateway)

    -   [Konformitätseinstellungen und Zugriff auf Unternehmensressourcen](#BKMK_CompSettingsLog)  

    -   [Configuration Manager-Konsole](#BKMK_ConsoleLog)  

    -   [Content Management](#BKMK_ContentLog)  

    -   [Ermittlung](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [Erweiterungen](#BKMK_Extensions)  

    -   [Inventur](#BKMK_InventoryLog)  

    -   [Messung](#BKMK_MeteringLog)  

    -   [Migration](#BKMK_MigrationLog)  

    -   [Mobile Geräte](#BKMK_MDMLog)  

    -   [Betriebssystembereitstellung](#BKMK_OSDLog)  

    -   [Energieverwaltung](#BKMK_PowerMgmtLog)  

    -   [Remotesteuerung](#BKMK_RCLog)  

    -   [Berichterstellung](#BKMK_ReportLog)  

    -   [Rollenbasierte Verwaltung](#BKMK_RBALog)  

    -   [Dienstverbindungspunkt](#BKMK_WITLog)  

    -   [Softwareupdates](#BKMK_SU_NAPLog)  

    -   [Wake-On-LAN](#BKMK_WOLLog)  

    -   [Windows 10-Wartung](#BKMK_WindowsServicingLog)

    -   [Windows Update-Agent](#BKMK_WULog)  

    -   [WSUS-Server](#BKMK_WSUSLog)  

##  <a name="BKMK_AboutLogs"></a> Informationen zu Configuration Manager-Protokolldateien  
 Die meisten Prozesse in Configuration Manager schreiben Betriebsinformationen in eine spezielle Protokolldatei für den jeweiligen Prozess. Diese Protokolldateien werden durch die **.LOG** - oder **.LO_** -Erweiterung identifiziert. Configuration Manager schreibt in die LOG-Protokolldatei, bis das Protokoll die maximale Größe erreicht hat. Wenn dies eintritt, wird die LOG-Datei in eine Datei mit dem gleichen Namen, aber der Erweiterung „.LO_“ kopiert, und der Prozess oder die Komponente schreibt weiterhin in die LOG-Datei. Wenn die Größe der LOG-Datei erneut den zulässigen Maximalwert erreicht, wird die LO_-Datei überschrieben und der Prozess wiederholt. Bei einigen Komponenten wird ein Protokolldateiverlauf geführt, indem dem Namen der Protokolldatei ein Datum- und Zeitstempel hinzugefügt wird, wobei die Erweiterung „.LOG“ erhalten bleibt. Eine Ausnahme in Bezug auf die maximale Größe und Verwendung der .LO_-Datei stellt der Client für Linux und UNIX dar. Weitere Informationen darüber, wie Protokolldateien vom Client für Linux und UNIX verwendet werden, finden Sie unter [Verwalten von Protokolldateien beim Client für Linux und UNIX](#BKMK_ManageLinuxLogs) in diesem Thema.  

 Zum Anzeigen der Protokolle können Sie das Configuration Manager-Protokollanzeigetool „CMTrace“ verwenden, das sich im Ordner \\\SMSSETUP\TOOLS\\ der Configuration Manager-Quellmedien befindet. Das CMTrace-Tool wird ebenfalls allen Startimages hinzugefügt, die in die Softwarebibliothek aufgenommen werden.  

###  <a name="BKMK_LogOptions"></a> Konfigurieren der Protokollierungsoptionen mithilfe des Dienst-Managers für Configuration Manager  
 Sie können den Speicherort und die Größe der Protokolldateien in Configuration Manager ändern.  

 Im folgenden Verfahren wird beschrieben, wie Sie die Größe, den Namen und den Speicherort von Protokolldateien ändern oder mehrere Komponenten für das Schreiben in die gleiche Protokolldatei konfigurieren können.  

#### <a name="to-modify-logging-for-a-component"></a>So ändern Sie die Protokollierung für eine Komponente:  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**, dann auf **Systemstatus** und anschließend auf **Standortstatus** oder **Komponentenstatus**.  
2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Komponente** auf **Starten**, und wählen Sie dann **Dienst-Manager für Configuration Manager** aus.  
3.  Wenn der Dienst-Manager für Configuration Manager geöffnet wird, stellen Sie eine Verbindung mit dem zu verwaltenden Standort her. Wenn der zu verwaltende Standort nicht angezeigt wird, klicken Sie auf **Standort**, dann auf **Verbinden**, und geben Sie dann den Namen des Standortservers für den gewünschten Standort ein.  
4.  Erweitern Sie den Standort und wechseln Sie zu **Komponenten** oder **Server**, je nachdem, wo die zu verwaltenden Komponenten sich befinden.  
5.  Wählen Sie im rechten Fensterbereich eine oder mehrere Komponenten aus.  
6.  Klicken Sie im Menü **Komponente** auf **Protokollierung**.  
7.  Legen Sie im Dialogfeld **Configuration Manager-Komponentenprotokollierung** die verfügbaren Konfigurationsoptionen für Ihre Auswahl fest.  
8.  Klicken Sie auf **OK**, um die Konfiguration zu speichern.  

###  <a name="BKMK_LogLocation"></a> Suchen von Configuration Manager-Protokollen  
Configuration Manager-Protokolldateien werden an verschiedenen Speicherorten gespeichert, die vom Prozess, von dem die Protokolldatei erstellt wurde sowie von der Konfiguration Ihrer Standortsysteme abhängig sind. Da der Speicherort der Protokolldatei auf einem Computern variieren kann, verwenden Sie die Suche, um die relevanten Protokolldateien auf Ihren Configuration Manager-Computern ausfindig zu machen, wenn Sie eine Problembehebung in einem bestimmten Szenario durchführen müssen.  

##  <a name="BKMK_ClientLogs"></a> Configuration Manager-Clientprotokolle  
In den folgenden Abschnitten werden die Protokolldateien für Clientvorgänge und die Clientinstallation aufgelistet.  

###  <a name="BKMK_ClientOpLogs"></a> Clientvorgänge  
In der folgenden Tabelle werden die Protokolldateien auf dem Configuration Manager-Client aufgelistet.  

|Protokollname|Beschreibung|  
|--------------|-----------------|  
|CAS.log|Der Content Access Service. Verwaltet den lokalen Paketcache auf dem Client.|  
|Ccm32BitLauncher.log|Zeichnet Aktionen zum Starten von Anwendungen auf dem Client auf, die mit „Ausführen als 32-Bit“ gekennzeichnet sind.|  
|CcmEval.log|Zeichnet Auswertungsaktivitäten für den Configuration Manager-Clientstatus auf sowie Details für Komponenten, die für den Configuration Manager-Client erforderlich sind|  
|CcmEvalTask.log|Zeichnet die Auswertungsaktivitäten für den Configuration Manager-Clientstatus auf, die vom geplanten Auswertungstask initiiert werden|  
|CcmExec.log|Zeichnet Aktivitäten des Clients und des SMS-Agent-Hostdiensts auf. Diese Protokolldatei enthält auch Informationen zum Aktivieren und Deaktivieren des Aktivierungsproxys.|  
|CcmMessaging.log|Zeichnet Aktivitäten in Zusammenhang mit Kommunikation zwischen Client und Verwaltungspunkten auf.|  
|CCMNotificationAgent.log|Zeichnet Aktivitäten im Zusammenhang mit Client-Benachrichtigungsoperationen auf.|  
|Ccmperf.log|Zeichnet Aktivitäten im Zusammenhang mit Wartung und Erfassung von Daten zu Clientleistungsindikatoren auf.|  
|CcmRestart.log|Zeichnet Neustartaktivitäten zu Clientdiensten auf.|  
|CCMSDKProvider.log|Zeichnet Aktivitäten im Zusammenhang mit den Client-SDK-Schnittstellen auf.|  
|CertificateMaintenance.log|Verwaltet Zertifikate für die Active Directory-Domänendienste und die Verwaltungspunkte.|  
|CIDownloader.log|Zeichnet Details zu Downloads von Konfigurationselementdefinitionen auf.|  
|CITaskMgr.log|Zeichnet Tasks auf, die für jede Anwendung und jeden Bereitstellungstyp initiiert werden, wie z.B. Herunterladen von Inhalten oder Installieren und Deinstallieren von Aktionen.|  
|ClientAuth.log|Zeichnet das Signieren und Authentifizieren des Clients auf.|  
|ClientIDManagerStartup.log|Erstellt und verwaltet die Client-GUID und identifiziert Tasks, die während der Anmeldung und Zuweisung von Clients ausgeführt werden.|  
|ClientLocation.log|Zeichnet Tasks im Zusammenhang mit der Clientstandortzuweisung auf.|  
|CMHttpsReadiness.log|Zeichnet die Ergebnisse der Ausführung des Configuration Manager-Tools zur Überprüfung der HTTPS-Bereitschaft auf. Mithilfe dieses Tools wird überprüft, ob Computer über ein PKI-Clientauthentifizierungszertifikat verfügen, das für Configuration Manager verwendet werden kann.|  
|CmRcService.log|Zeichnet Informationen für den Remotesteuerungsdienst auf.|  
|ContentTransferManager.log|Plant den intelligenten Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS) oder den Server Message Block (SMB), um Pakete herunterzuladen oder darauf zuzugreifen.|  
|DataTransferService.log|Zeichnet die gesamte BITS-Kommunikation für den Richtlinien- oder Paketzugriff auf.|  
|EndpointProtectionAgent|Zeichnet Informationen zur Installation des System Center Endpoint Protection-Clients und zum Anwenden der Antischadsoftwarerichtlinie auf diesen Client auf.|  
|execmgr.log|Zeichnet Details zu Paketen und Tasksequenzen auf, die auf dem Client ausgeführt werden.|  
|ExpressionSolver.log|Zeichnet Details zu erweiterten Erkennungsmethoden auf, die verwendet werden, wenn die ausführliche oder die Debugprotokollierung aktiviert ist.|  
|ExternalEventAgent.log|Zeichnet den Verlauf der Schadsoftware-Erkennung und von Ereignissen von Endpoint Protection auf, die mit dem Clientstatus in Verbindung stehen.|  
|FileBITS.log|Zeichnet alle SMB-Paketzugriffsaufgaben auf.|  
|FileSystemFile.log|Zeichnet die Aktivitäten des WMI-Anbieters (Windows Management Instrumentation) für Softwareinventur und Dateisammlung auf.|  
|FSPStateMessage.log|Zeichnet die Aktivitäten im Zusammenhang mit Zustandsmeldungen auf, die vom Client an den Fallbackstatuspunkt gesendet werden.|  
|InternetProxy.log|Zeichnet die Konfigurations- und Nutzungsaktivitäten des Netzwerkproxys für den Client auf.|  
|InventoryAgent.log|Zeichnet Aktivitäten im Zusammenhang mit Hardwareinventur, Softwareinventur und Frequenzermittlung auf dem Client auf.|  
|LocationCache.log|Zeichnet die Aktivitäten im Zusammenhang mit Standortcachenutzung und -wartung für den Client auf.|  
|LocationServices.log|Zeichnet die Clientaktivitäten im Zusammenhang mit der Suche nach Verwaltungspunkten, Softwareupdatepunkten und Verteilungspunkten auf.|  
|MaintenanceCoordinator.log|Zeichnet die Aktivitäten im Zusammenhang mit allgemeinen Wartungstasks für den Client auf.|  
|Mifprovider.log|Zeichnet die Aktivitäten des WMI-Anbieters für MIF-Dateien auf.|  
|mtrmgr.log|Überwacht alle Softwaremessungen.|  
|PolicyAgent.log|Zeichnet mithilfe des Datenübertragungsdiensts übermittelte Richtlinienanforderungen auf.|  
|PolicyAgentProvider.log|Zeichnet Richtlinienänderungen auf.|  
|PolicyEvaluator.log|Zeichnet Details zur Auswertung von Richtlinien auf Clientcomputern, einschließlich Softwareupdates, auf.|  
|PolicyPlatformClient.log|Zeichnet den Prozess für Wiederherstellung und Konformität für alle Anbieter in „%Program Files%\Microsoft Policy Platform“ mit Ausnahme des Dateianbieters auf.|  
|PolicySdk.log|Zeichnet Aktivitäten für Schnittstellen des Richtliniensystem-SDK auf.|  
|Pwrmgmt.log|Zeichnet Informationen zum Aktivieren oder Deaktivieren sowie Konfigurieren der Clienteinstellungen des Aktivierungsproxys auf.|  
|PwrProvider.log|Zeichnet die Aktivitäten des Energieverwaltungsanbieters (PWRInvProvider) auf, der im WMI-Dienst (Windows Management Instrumentation) gehostet ist. Unter allen unterstützten Windows-Versionen zählt der Anbieter während der Hardwareinventur auf Computern die aktuellen Einstellungen auf und wendet Energiesparplaneinstellungen an.|  
|SCClient_&lt;*Domäne*\>@&lt;*Benutzername*\>_1.log|Zeichnet die Aktivitäten im Software Center für den angegebenen Benutzer auf dem Clientcomputer auf.|  
|SCClient_&lt;*Domäne*\>@&lt;*Benutzername*\>_2.log|Zeichnet die historischen Aktivitäten im Software Center für den angegebenen Benutzer auf dem Clientcomputer auf.|  
|Scheduler.log|Zeichnet Aktivitäten geplanter Tasks für alle Clientvorgänge auf.|  
|SCNotify_&lt;*Domäne*\>@&lt;*Benutzername*\>_1.log|Zeichnet die Aktivitäten im Zusammenhang mit Benutzerbenachrichtigungen über Software für den angegebenen Benutzer auf.|  
|SCNotify_&lt;*Domäne*\>@&lt;*Benutzername*\>_1-&lt;*date_time*>.log|Zeichnet die historischen Informationen im Zusammenhang mit Benutzerbenachrichtigungen über Software für den angegebenen Benutzer auf.|  
|setuppolicyevaluator.log|Zeichnet Aktivitäten im Zusammenhang mit Konfiguration und der Erstellung von Inventurrichtlinien in WMI auf.|  
|SleepAgent_&lt;*Domäne*\>@SYSTEM_0.log|Die wichtigste Protokolldatei für Aktivierungsproxy.|  
|smscliui.log|Zeichnet die Nutzung des Configuration Manager-Clients in der Systemsteuerung auf.|  
|SrcUpdateMgr.log|Zeichnet Aktivitäten im Zusammenhang mit installierten Windows Installer-Anwendungen auf, für die mithilfe aktueller Verteilungspunktquellpfade ein Update ausgeführt wird.|  
|StatusAgent.log|Zeichnet Statusmeldungen auf, die von Clientkomponenten erstellt werden.|  
|SWMTRReportGen.log|Erstellt einen Verwendungsdatenbericht, der von dem Messungsagent gesammelt wird. Diese Daten werden in Mtrmgr.log protokolliert.|  
|UserAffinity.log|Zeichnet Details zur Affinität zwischen Benutzer und Gerät auf.|  
|VirtualApp.log|Zeichnet spezifische Informationen zur Auswertung der App-V-Bereitstellungstypen auf.|  
|Wedmtrace.log|Zeichnet Vorgänge im Zusammenhang mit Schreibfiltern auf Windows Embedded-Clients auf.|  
|wakeprxy-install.log|Zeichnet Installationsinformationen auf, wenn Clients die Clienteinstellungsoption zur Aktivierung des Aktivierungsproxy empfangen.|  
|wakeprxy-uninstall.log|Zeichnet Informationen zur Deinstallation von Aktivierungsproxys auf, wenn von Clients die Clienteinstellungsoption „Aktivierungsproxys nicht zulassen“ empfangen wurde, wenn der Aktivierungsproxy bereits vorher zugelassen war.|  

###  <a name="BKMK_ClientInstallLog"></a> Protokolldateien zur Clientinstallation  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen zur Installation des Configuration Manager-Clients enthalten.  

|Protokollname|Beschreibung|  
|--------------|-----------------|  
|ccmsetup.log|Zeichnet ccmsetup.exe-Tasks für Clienteinstellung, Clientupgrade und Cliententfernung auf. Ist für die Problembehandlung bei Clientinstallationsproblemen hilfreich.|  
|ccmsetup-ccmeval.log|Zeichnet ccmsetup.exe-Tasks für Clientstatus und -wiederherstellung auf.|  
|CcmRepair.log|Zeichnet Reparaturaktivitäten des Client-Agents auf.|  
|client.msi.log|Zeichnet die von „client.msi“ ausgeführten Setuptasks auf. Ist für die Problembehandlung bei Problemen beim Installieren oder Entfernen von Clients hilfreich.|  

###  <a name="BKMK_LogFilesforLnU"></a> Client für Linux und UNIX  
 Vom Configuration Manager-Client für Linux und UNIX werden Informationen in folgenden Protokolldateien aufgezeichnet.  

> [!TIP]  
>  Ab dem kumulativen Update 1 der Clients für Linux und UNIX können Sie CMTrace zum Anzeigen entsprechender Clientprotokolldateien für Linux und UNIX verwenden.  

> [!NOTE]  
>  Wenn Sie die Erstversion des Clients für Linux und UNIX verwenden und die Dokumentation in diesem Abschnitt nutzen, ersetzen Sie die folgenden Verweise in den einzelnen Dateien oder Prozessen:  
>   
>  -   Ersetzen Sie **omiserver.bin** durch **nwserver.bin**  
> -   Ersetzen Sie **omi** durch **nanowbem**  

|Protokollname|Details|  
|--------------|-------------|  
|Scxcm.log|Das ist die Protokolldatei für den Kerndienst des Configuration Manager-Clients für Linux und UNIX (ccmexec.bin). Diese Protokolldatei enthält Informationen zur Installation und zum laufenden Vorgang von ccmexec.bin.<br /><br /> Standardmäßig befindet sich diese Datei unter **/var/opt/microsoft/scxcm.log**<br /><br /> Für das Ändern des Speicherorts der Protokolldatei bearbeiten Sie **/opt/microsoft/configmgr/etc/scxcm.conf** , und ändern Sie das Feld **PATH** . Sie müssen den Clientcomputer oder den Dienst nicht neu starten, damit die Änderungen wirksam werden.<br /><br /> Für den Protokolliergrad können Sie eine von vier unterschiedlichen Einstellungen vornehmen.|  
|Scxcmprovider.log|Das ist die Protokolldatei für den CIM-Dienst des Configuration Manager-Clients für Linux und UNIX (omiserver.bin). Diese Protokolldatei enthält Informationen zu den laufenden Vorgängen von nwserver.bin.<br /><br /> Dieses Protokoll befindet sich unter**/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> Für eine Änderung des Speicherorts der Protokolldatei bearbeiten Sie **/opt/microsoft/omi/etc/scxcmprovider.conf** , und ändern Sie das Feld **PATH** . Sie müssen den Clientcomputer oder den Dienst nicht neu starten, damit die Änderungen wirksam werden.<br /><br /> Für den Protokolliergrad können Sie eine von drei unterschiedlichen Einstellungen vornehmen.|  

 Beide Protokolldateien unterstützen mehrere Protokolliergrade:  

-   **scxcm.log**. Für eine Änderung des Protokolliergrads bearbeiten Sie **/opt/microsoft/configmgr/etc/scxcm.conf** und ändern Sie jede Instanz des Tags **MODUL** auf den gewünschten Protokolliergrad  

    -   FEHLER: Weist auf Probleme hin, die Ihr Eingreifen erfordern.  

    -   WARNUNG: Weist auf mögliche Probleme für Clientvorgänge hin.  

    -   INFO: Ausführlichere Protokollierung, durch die der Status verschiedener Ereignisse auf dem Client angegeben wird.  

    -   ABLAUFVERFOLGUNG: Ausführliche Protokollierung, die normalerweise zur Problemdiagnose verwendet wird.  

-   **scxcmprovider.log**. Für eine Änderung des Protokolliergrads bearbeiten Sie **/opt/microsoft/omi/etc/ scxcmprovider.conf** und ändern Sie jede Instanz des Tags **MODUL** in den erwünschten Protokolliergrad.  

    -   FEHLER: Weist auf Probleme hin, die Ihr Eingreifen erfordern.  

    -   WARNUNG: Weist auf mögliche Probleme für Clientvorgänge hin.

    -   INFO: Ausführlichere Protokollierung, durch die der Status verschiedener Ereignisse auf dem Client angegeben wird.  

Unter normalen Betriebsbedingungen sollte der Protokollgrad FEHLER verwendet werden. Diese Protokollebene erstellt die kleinste Protokolldatei. Mit der Steigerung des Protokollgrads von FEHLER zu WARNUNG zu INFO zu ABLAUFVERFOLGUNG wird die Protokolldatei mit jedem Schritt größer, da mehr Daten hineingeschrieben werden.  

####  <a name="BKMK_ManageLinuxLogs"></a> Verwalten von Protokolldateien für den Client für Linux und UNIX  
Auf dem Client für Linux und UNIX wird weder eine maximale Größe der Clientprotokolldateien vorgegeben noch werden die Inhalte der .LOG-Dateien automatisch in eine andere Datei, z.B. eine .LO_-Datei kopiert: Wenn Sie die maximale Größe von Protokolldateien steuern möchten, müssen Sie unabhängig vom Configuration Manager-Client für Linux und UNIX einen Prozess zum Verwalten der Protokolldateien implementieren.  

Beispielsweise können Sie den Linux- und UNIX-Standardbefehl **logrotate** verwenden, um die Größe und Rotation der Clientprotokolldateien zu verwalten. Auf dem Configuration Manager-Client für Linux und UNIX steht eine Schnittstelle zur Verfügung, mit deren Hilfe dem Client über **logrotate** signalisiert werden kann, wann die Protokollrotation abgeschlossen ist, sodass die Informationserfassung in der Protokolldatei wiederaufgenommen werden kann.  

Weitere Informationen über **logrotate**finden Sie in der Dokumentation zu den Linux und UNIX-Verteilungen, die Sie verwenden.  

###  <a name="BKMK_LogfilesforMac"></a> Client für Macintosh-Computer  
Vom Configuration Manager-Client für Macintosh-Computer werden Informationen in folgenden Protokolldateien aufgezeichnet.  

|Protokollname|Details|  
|--------------|-------------|  
|CCMClient-&lt;*Datum_Zeit>*.log|Zeichnet Aktivitäten auf, die mit Vorgängen des Macintosh-Clients verknüpft sind. Dazu gehören Anwendungsverwaltung, Inventur und Fehlerprotokollierung.<br /><br /> Diese Protokolldatei befindet sich im Ordner „/Library/Application Support/Microsoft/CCM/Logs“ auf dem Macintosh-Computer.|  
|CCMAgent-&lt;*Datum_Zeit>*.log|Zeichnet Informationen zu Clientvorgängen auf, einschließlich Benutzeranmeldungs- und abmeldungsvorgänge und Macintosh-Computeraktivität.<br /><br /> Diese Protokolldatei befindet sich im Ordner ~/Library/Logs auf dem Macintosh-Computer.|  
|CCMNotifications-&lt;*Datum_Zeit>*.log|Zeichnet Aktivitäten auf, die mit Configuration Manager-Benachrichtigungen verknüpft sind, die auf dem Macintosh-Computer angezeigt werden.<br /><br /> Diese Protokolldatei befindet sich im Ordner ~/Library/Logs auf dem Macintosh-Computer.|  
|CCMPrefPane-&lt;*Datum_Zeit>*.log|Zeichnet Aktivitäten auf, die mit dem Configuration Manager-Dialogfeld für Einstellungen auf dem Macintosh-Computer verknüpft sind. Dazu gehören der allgemeine Status und die Fehlerprotokollierung.<br /><br /> Diese Protokolldatei befindet sich im Ordner ~/Library/Logs auf dem Macintosh-Computer.|  

Zusätzlich wird in der Protokolldatei „SMS_DM.log“ auf dem Standortsystemserver die Kommunikation zwischen Macintosh-Computern und dem Verwaltungspunkt aufgezeichnet, der für mobile Geräte und Mac-Computer aktiviert ist.  

##  <a name="BKMK_ServerLogs"></a> Protokolldateien für Configuration Manager-Standortserver  
 In den folgenden Abschnitten werden Protokolldateien aufgelistet, die sich auf dem Standortserver befinden oder im Zusammenhang mit bestimmten Standortsystemrollen stehen.  

###  <a name="BKMK_SiteSiteServerLog"></a> Protokolle für Standortserver und Standortsystemserver  
 In der folgenden Tabelle werden die Protokolldateien auf dem Configuration Manager-Standortserver und den entsprechenden Standortsystemservern aufgelistet.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Zeichnet Aktivitäten im Zusammenhang mit der Anmeldungsverarbeitung auf.|Standortserver|  
|ADForestDisc.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Gesamtstrukturermittlung auf.|Standortserver|  
|ADService.log|Zeichnet Details zur Kontoerstellung und zu Sicherheitsgruppen in Active Directory auf.|Standortserver|  
|adsgdis.log|Zeichnet Aktionen der Active Directory-Gruppenermittlung auf.|Standortserver|  
|adsysdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Systemermittlung auf.|Standortserver|  
|adusrdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Benutzerermittlung auf.|Standortserver|  
|ccm.log|Zeichnet Aktivitäten im Zusammenhang mit der Clientpushinstallation auf.|Standortserver|  
|CertMgr.log|Zeichnet die Zertifikataktivitäten für die standortinterne Kommunikation auf.|Standortsystemserver|  
|chmgr.log|Zeichnet die Aktivitäten des Clientintegritäts-Managers auf.|Standortserver|  
|Cidm.log|Zeichnet Änderungen an den Clienteinstellungen durch den SMS-Clientinstallationsdaten-Manager (CIDM) auf.|Standortserver|  
|colleval.log|Zeichnet Details zum Erstellen, Ändern und Löschen von Sammlungen durch den Sammlungsauswerter auf.|Standortserver|  
|compmon.log|Zeichnet den Status von Threadkomponenten auf, die für den Standortserver überwacht werden.|Standortsystemserver|  
|compsumm.log|Zeichnet die Tasks der Statuszusammenfassung für Komponenten auf.|Standortserver|  
|ComRegSetup.log|Zeichnet die Ergebnisse der Erstinstallation der COM-Registrierung für einen Standortserver auf.|Standortsystemserver|  
|dataldr.log|Zeichnet Informationen zur Verarbeitung von MIF-Dateien und Hardwareinventur in der Configuration Manager-Datenbank auf.|Standortserver|  
|ddm.log|Zeichnet die Aktivitäten des Ermittlungsdaten-Managers auf.|Standortserver|  
|despool.log|Zeichnet die eingehende Datenkommunikation zwischen Standorten auf.|Standortserver|  
|distmgr.log|Zeichnet Details zu Paketerstellung, Komprimierung, Deltareplikation und Informationsupdates auf.|Standortserver|  
|EPCtrlMgr.log|Zeichnet Informationen zur Synchronisierung von Schadsoftwarebedrohungsdaten vom Endpoint Protection-Server für Standortsystemrollen in die Configuration Manager-Datenbank auf.|Standortserver|  
|EPMgr.log|Zeichnet den Status der Endpoint Protection-Standortsystemrolle auf.|Standortsystemserver|  
|EPSetup.log|Stellt Informationen zur Installation der Endpoint Protection-Standortsystemrolle bereit.|Standortsystemserver|  
|EnrollSrv.log|Zeichnet Aktivitäten des Anmeldungsdienstprozesses auf.|Standortsystemserver|  
|EnrollWeb.log|Zeichnet Aktivitäten des Anmeldungswebsiteprozesses auf.|Standortsystemserver|  
|fspmgr.log|Zeichnet Aktivitäten der Fallbackstatuspunkt-Systemrolle auf.|Standortsystemserver|  
|hman.log|Zeichnet Informationen zu Standortkonfigurationsänderungen und zur Veröffentlichung von Standortinformationen in den Active Directory Domain Services auf.|Standortserver|  
|Inboxast.log|Zeichnet die Dateien auf, die vom Verwaltungspunkt in den entsprechenden Ordner INBOXES auf dem Standortserver verschoben werden.|Standortserver|  
|inboxmgr.log|Zeichnet Aktivitäten im Zusammenhang mit der Dateiübertragung zwischen Eingangsboxordnern auf.|Standortserver|  
|inboxmon.log|Zeichnet Aktivitäten in Zusammenhang mit der Verarbeitung von Eingangsboxdateien und Updates von Leistungsindikatoren auf.|Standortserver|  
|invproc.log|Zeichnet die Weiterleitung von MIF-Dateien von einem sekundären Standort an dessen übergeordneten Standort auf.|Standortserver|  
|migmctrl.log|Zeichnet Informationen zu Migrationsaktionen auf, einschließlich Migrationsaufträge, freigegebener Verteilungspunkte und Upgrades von Verteilungspunkten.|Standort der obersten Ebene in der Configuration Manager-Hierarchie und jeder untergeordnete primäre Standort<br /><br /> Verwenden Sie in einer Hierarchie mit mehreren primären Standorten die Protokolldatei, die auf dem Standort der zentralen Verwaltung erstellt wurde.|  
|mpcontrol.log|Zeichnet die Registrierung des Verwaltungspunks in Windows Internet Name Service (WINS) auf. Zeichnet alle 10 Minuten die Verfügbarkeit des Verwaltungspunkts auf.|Standortsystemserver|  
|mpfdm.log|Zeichnet die Aktionen der Verwaltungspunktkomponente auf, von der Clientdateien in den entsprechenden Ordner INBOXES auf dem Standortserver verschoben werden.|Standortsystemserver|  
|mpMSI.log|Zeichnet die Details zur Installation des Verwaltungspunkts auf.|Standortserver|  
|MPSetup.log|Zeichnet den Wrapperprozess der Verwaltungspunktinstallation auf.|Standortserver|  
|netdisc.log|Zeichnet Aktionen im Zusammenhang mit der Netzwerkermittlung auf.|Standortserver|  
|ntsvrdis.log|Zeichnet die Ermittlungsaktivitäten des Standortsystemservers auf.|Standortserver|  
|Objreplmgr|Zeichnet die Verarbeitung von Objektänderungsbenachrichtigungen für die Replikation auf.|Standortserver|  
|offermgr.log|Zeichnet Updates von Ankündigungen auf.|Standortserver|  
|offersum.log|Zeichnet die Zusammenfassung von Bereitstellungstatusmeldungen auf.|Standortserver|  
|OfflineServicingMgr.log|Zeichnet die Aktivitäten im Zusammenhang mit der Anwendung von Updates auf Betriebssystemabbilddateien auf.|Standortserver|  
|outboxmon.log|Zeichnet Aktivitäten in Zusammenhang mit der Verarbeitung von Ausgangsboxdateien und Updates von Leistungsindikatoren auf.|Standortserver|  
|PerfSetup.log|Zeichnet die Ergebnisse der Installation von Leistungsindikatoren auf.|Standortsystemserver|  
|PkgXferMgr.log|Zeichnet die Aktionen der Komponente SMS-Executive auf, über die Inhalte von einem primären Standort an einen Remoteverteilungspunkt gesendet werden.|Standortserver|  
|policypv.log|Zeichnet Aktualisierungen der Clientrichtlinien auf und spiegelt Änderungen der Clienteinstellungen oder -bereitstellungen wider.|Primärer Standortserver|  
|rcmctrl.log|Zeichnet die Aktivitäten im Zusammenhang mit der Datenbankreplikation zwischen Standorten in der Hierarchie auf.|Standortserver|  
|replmgr.log|Zeichnet die Replikation von Dateien zwischen Standortserverkomponenten und den Planerkomponenten auf.|Standortserver|  
|ResourceExplorer.log|Zeichnet Fehler, Warnungen und Informationen zur Ausführung des Ressourcen-Explorers auf.|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|ruleengine.log|Zeichnet Details zu automatischen Bereitstellungsregeln im Zusammenhang mit Identifizierung, Inhaltsdownload sowie Erstellung von Softwareupdategruppen und Bereitstellungen auf.|Standortserver|  
|schedule.log|Zeichnet Details zu Aufträgen zwischen Standorten sowie zur Dateireplikation auf.|Standortserver|  
|sender.log|Zeichnet die Dateien auf, die mithilfe von dateibasierter Replikation zwischen Standorten übertragen werden.|Standortserver|  
|sinvproc.log|Zeichnet Informationen zur Verarbeitung der Softwareinventurdaten in die Standortdatenbank auf.|Standortserver|  
|sitecomp.log|Zeichnet Details zur Wartung der installierten Standortkomponenten auf allen Standortsystemservern des Standorts auf.|Standortserver|  
|sitectrl.log|Zeichnet Änderungen der Standorteinstellungen auf, die an Standortsteuerungsobjekten in der Datenbank vorgenommen werden.|Standortserver|  
|sitestat.log|Zeichnet den Verfügbarkeits- und Speicherplatzüberwachungsprozess aller Standortsysteme auf.|Standortserver|  
|SmsAdminUI.log|Zeichnet die Aktivität der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SMSAWEBSVCSetup.log|Zeichnet die Installationsaktivitäten des Anwendungskatalog-Webdienstes auf.|Standortsystemserver|  
|smsbkup.log|Zeichnet die Ausgabe des Standortsicherungsprozesses auf.|Standortserver|  
|smsdbmon.log|Zeichnet Datenbankänderungen auf.|Standortserver|  
|SMSENROLLSRVSetup.log|Zeichnet die Installationsaktivitäten des Anmeldungswebdienstes auf.|Standortsystemserver|  
|SMSENROLLWEBSetup.log|Zeichnet die Installationsaktivitäten der Anmeldungswebsite auf.|Standortsystemserver|  
|smsexec.log|Zeichnet die Verarbeitung aller Threads der Standortserverkomponenten auf.|Standortserver oder Standortsystemserver|  
|SMSFSPSetup.log|Zeichnet Meldungen auf, die bei der Installation eines Fallbackstatuspunkts generiert werden.|Standortsystemserver|  
|SMSPORTALWEBSetup.log|Zeichnet die Installationsaktivitäten der Anwendungskatalog-Website auf.|Standortsystemserver|  
|SMSProv.log|Zeichnet den Zugriff des WMI-Anbieters auf die Standortdatenbank auf.|Computer mit dem SMS-Anbieter|  
|srsrpMSI.log|Zeichnet detaillierte Ergebnisse der Installation des Berichterstattungspunkts aus der MSI-Ausgabe auf.|Standortsystemserver|  
|srsrpsetup.log|Zeichnet Ergebnisse der Installation des Berichterstattungspunkts auf.|Standortsystemserver|  
|statesys.log|Zeichnet die Verarbeitung von Systemzustandsmeldungen auf.|Standortserver|  
|statmgr.log|Zeichnet Schreibvorgänge aller Statusmeldungen in die Datenbank auf.|Standortserver|  
|swmproc.log|Zeichnet die Verarbeitung von Messungsdateien und -einstellungen auf.|Standortserver|  

###  <a name="BKMK_SiteInstallLog"></a> Protokolldateien zur Standortserverinstallation  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Standortinstallation enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Zeichnet Aktivitäten im Zusammenhang mit der Auswertung und Installation von erforderlichen Komponenten auf.|Standortserver|  
|ConfigMgrSetup.log|Zeichnet Ausgabedetails des Standortserver-Setups auf.|Standortserver|  
|ConfigMgrSetupWizard.log|Zeichnet Informationen im Zusammenhang mit Aktivitäten im Setup-Assistenten auf.|Standortserver|  
|SMS_BOOTSTRAP.log|Zeichnet Informationen zum Fortschritt beim Starten der Installation des sekundären Standorts auf. Informationen zum eigentlichen Installationsvorgang sind in ConfigMgrSetup.log enthalten.|Standortserver|  
|smstsvc.log|Zeichnet Informationen zu Installation, Nutzung und Entfernung eines Windows-Dienstes auf, der zum Testen von Netzwerkverbindungen und Berechtigungen zwischen Servern mithilfe des Computerkontos des Servers, der die Verbindung initiiert, verwendet wird.|Standortserver und Standortsystemserver|  

###  <a name="BKMK_FSPLog"></a> Protokolldateien für den Fallbackstatuspunkt  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Fallbackstatuspunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Zeichnet Details zur Kommunikation von mobilen Legacyclient-Geräten und Clientcomputern mit dem Fallbackstatuspunkt auf.|Standortsystemserver|  
|fspMSI.log|Zeichnet Meldungen auf, die bei der Installation eines Fallbackstatuspunkts generiert werden.|Standortsystemserver|  
|fspmgr.log|Zeichnet Aktivitäten der Fallbackstatuspunkt-Systemrolle auf.|Standortsystemserver|  

###  <a name="BKMK_MPLog"></a> Protokolldateien für den Verwaltungspunkt  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Verwaltungspunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Zeichnet Aktivitäten im Zusammenhang mit Client-Messaging auf dem Endpunkt auf.|Standortsystemserver|  
|MP_CliReg.log|Zeichnet die vom Verwaltungspunkt verarbeiteten Clientregistrierungsaktivitäten auf.|Standortsystemserver|  
|MP_Ddr.log|Zeichnet die Konvertierung von XML DDR-Datensätzen von Clients auf und kopiert diese auf den Standortserver.|Standortsystemserver|  
|MP_Framework.log|Zeichnet die Aktivitäten von Hauptverwaltungspunkt und Clientframeworkkomponenten auf.|Standortsystemserver|  
|MP_GetAuth.log|Zeichnet Aktivitäten im Zusammenhang mit der Clientautorisierung auf.|Standortsystemserver|  
|MP_GetPolicy.log|Zeichnet Aktivitäten im Zusammenhang mit Richtlinienanforderungen von Clientcomputern auf.|Standortsystemserver|  
|MP_Hinv.log|Zeichnet Details zum Konvertieren von XML-Hardwareinventurdatensätzen von Clients und zum Kopieren der Dateien auf den Standortserver auf.|Standortsystemserver|  
|MP_Location.log|Zeichnet Aktivitäten im Zusammenhang mit Suchanforderungen und Antworten von Clients auf.|Standortsystemserver|  
|MP_OOBMgr.log|Zeichnet die Verwaltungspunktaktivitäten im Zusammenhang mit dem Empfangen von OTP von einem Client auf.|Standortsystemserver|  
|MP_Policy.log|Zeichnet die Richtlinienkommunikation auf.|Standortsystemserver|  
|MP_Relay.log|Zeichnet das Übertragen von Dateien auf, die vom Client gesammelt werden.|Standortsystemserver|  
|MP_Retry.log|Zeichnet die Wiederholungsprozesse der Hardwareinventur auf.|Standortsystemserver|  
|MP_Sinv.log|Zeichnet Details zum Konvertieren von XML-Softwareinventurdatensätzen von Clients und zum Kopieren der Dateien auf den Standortserver auf.|Standortsystemserver|  
|MP_SinvCollFile.log|Zeichnet Details zur Dateisammlung auf.|Standortsystemserver|  
|MP_Status.log|Zeichnet Details zum Konvertieren von XML-Statusmeldungsdateien (SVF-Dateien) von Clients und zum Kopieren der Dateien auf den Standortserver auf.|Standortsystemserver|  
|mpcontrol.log|Zeichnet die Registrierung des Verwaltungspunks in WINS auf. Zeichnet alle 10 Minuten die Verfügbarkeit des Verwaltungspunkts auf.|Standortserver|  
|mpfdm.log|Zeichnet die Aktionen der Verwaltungspunktkomponente auf, von der Clientdateien in den entsprechenden Ordner INBOXES auf dem Standortserver verschoben werden.|Standortsystemserver|  
|mpMSI.log|Zeichnet die Details zur Installation des Verwaltungspunkts auf.|Standortserver|  
|MPSetup.log|Zeichnet den Wrapperprozess der Verwaltungspunktinstallation auf.|Standortserver|  

###  <a name="BKMK_SUPLog"></a> Protokolldateien für den Softwareupdatepunkt  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen zum Softwareupdatepunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Zeichnet Details zur Replikation von Benachrichtigungsdateien für Softwareupdates von einem übergeordneten an untergeordnete Standorte auf.|Standortserver|  
|PatchDownloader.log|Zeichnet Details zum Download von Softwareupdates von der Updatequelle in das Downloadziel auf dem Standortserver.|Der Computer, auf dem die Configuration Manager-Konsole gehostet wird, von der Downloads initiiert werden|  
|ruleengine.log|Zeichnet Details zu automatischen Bereitstellungsregeln im Zusammenhang mit Identifizierung, Inhaltsdownload sowie Erstellung von Softwareupdategruppen und Bereitstellungen auf.|Standortserver|  
|SUPSetup.log|Zeichnet Details zur Installation des Softwareupdatepunkts auf. Nach Abschluss der Softwareupdatepunkt-Installation wird **Installation was successful** in diese Protokolldatei geschrieben.|Standortsystemserver|  
|WCM.log|Zeichnet Details zur Konfiguration des Softwareupdatepunkts und zum Herstellen einer Verbindung mit dem WSUS-Server für abonnierte Updatekategorien, Klassifizierungen und Sprachen auf.|Standortserver, die eine Verbindung mit dem WSUS-Server herstellen|  
|WSUSCtrl.log|Zeichnet Details zur Konfiguration, Datenbankverbindungen und der Integrität von WSUS-Servern für den Standort auf.|Standortsystemserver|  
|wsyncmgr.log|Zeichnet Details zum Synchronisierungsprozess für Softwareupdates auf.|Standortsystemserver|  
|WUSSyncXML.log|Zeichnet Details zum Synchronisierungsvorgang des Inventurprogramms für Microsoft Updates auf.|Der Clientcomputer, der als Synchronisierungshost für das Inventurprogramm für Microsoft Updates konfiguriert ist|  

##  <a name="BKMK_FunctionLogs"></a> Protokolldateien für Configuration Manager-Funktionen  
 In den folgenden Abschnitten werden Protokolldateien für die Funktionen in Configuration Manager aufgelistet.  

###  <a name="BKMK_AppManageLog"></a> Anwendungsverwaltung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Anwendungsverwaltung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Zeichnet Details zum aktuellen und beabsichtigten Zustand von Anwendungen sowie zu ihrer Anwendbarkeit, Bereitstellungstypen, Abhängigkeiten und dazu, ob Anforderungen erfüllt wurden.|Client|  
|AppDiscovery.log|Zeichnet die Details über die Ermittlung oder die Erkennung von Anwendungen auf Clientcomputern auf.|Client|  
|AppEnforce.log|Zeichnet Details zu vorgenommenen Erzwingungsaktionen (Installieren und Deinstallieren) für Anwendungen auf dem Client auf.|Client|  
|awebsctl.log|Zeichnet die Überwachungsmaßnahmen für die Standortsystemrolle „Anwendungskatalog-Webdienstpunkt“ auf.|Standortsystemserver|  
|awebsvcMSI.log|Zeichnet detaillierte Installationsinformationen für die Standortsystemrolle „Anwendungskatalog-Webdienstpunkt“ auf.|Standortsystemserver|  
|CCMSDKProvider.log|Zeichnet die Aktivitäten des Anwendungsverwaltungs-SDK auf.|Client|  
|colleval.log|Zeichnet Details zum Erstellen, Ändern und Löschen von Sammlungen durch den Sammlungsauswerter auf.|Standortsystemserver|  
|ConfigMgrSoftwareCatalog.log|Zeichnet die Aktivitäten des Anwendungskatalogs auf, darunter auch dessen Verwendung von Silverlight.|Client|  
|portlctl.log|Zeichnet die Überwachungsmaßnahmen für die Standortsystemrolle „Anwendungskatalog-Websitepunkt“ auf.|Standortsystemserver|  
|portlwebMSI.log|Zeichnet die MSI-Installationsaktivitäten für die Anwendungskatalog-Websiterolle auf.|Standortsystemserver|  
|PrestageContent.log|Zeichnet die Details zur Verwendung des Tools ExtractContent.exe auf einem vorab bereitgestellten Remoteverteilungspunkt auf. Mit diesem Tool werden Inhalte extrahiert, die in eine Datei exportiert wurden.|Standortsystemserver|  
|ServicePortalWebService.log|Zeichnet die Aktivitäten des Anwendungskatalog-Webdienstes auf.|Standortsystemserver|  
|ServicePortalWebSite.log|Zeichnet die Aktivitäten der Anwendungskatalog-Website auf.|Standortsystemserver|  
|SMSdpmon.log|Zeichnet Details zum geplanten Task für die Integritätsüberwachung des Verteilungspunkts auf, der auf einem Verteilungspunkt konfiguriert wurde.|Standortserver|  
|SoftwareCatalogUpdateEndpoint.log|Zeichnet die Aktivitäten im Zusammenhang mit der Verwaltung der im Softwarecenter angezeigten URL für den Anwendungskatalog auf.|Client|  
|SoftwareCenterSystemTasks.log|Zeichnet die Aktivitäten im Zusammenhang mit der Überprüfung der erforderlichen Komponenten für das Softwarecenter auf.|Client|  

 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Bereitstellung von Paketen und Programmen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|colleval.log|Zeichnet Details zum Erstellen, Ändern und Löschen von Sammlungen durch den Sammlungsauswerter auf.|Standortserver|  
|execmgr.log|Zeichnet Details zu Paketen und ausgeführten Tasksequenzen auf.|Client|  

###  <a name="BKMK_AILog"></a> Asset Intelligence  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Asset Intelligence enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Zeichnet Aktivitäten im Zusammenhang mit Asset Intelligence-Inventuraktionen auf.|Client|  
|aikbmgr.log|Zeichnet Details zur Verarbeitung von XML-Dateien aus der Eingangsbox zum Update des Asset Intelligence-Katalogs auf.|Standortserver|  
|AIUpdateSvc.log|Zeichnet Details zur Interaktion des Asset Intelligence-Synchronisierungspunkts mit System Center Online (SCO), dem Online-Webdienst, auf.|Standortsystemserver|  
|AIUSMSI.log|Zeichnet Details zur Installation der Standortsystemrolle „Asset Intelligence-Synchronisierungspunkt“ auf.|Standortsystemserver|  
|AIUSSetup.log|Zeichnet Details zur Installation der Standortsystemrolle „Asset Intelligence-Synchronisierungspunkt“ auf.|Standortsystemserver|  
|ManagedProvider.log|Zeichnet Details zur Ermittlung von Software mit einem zugehörigen Software ID-Tag auf. Zeichnet zusätzlich Aktivitäten im Zusammenhang mit der Hardwareinventur auf.|Standortsystemserver|  
|MVLSImport.log|Zeichnet Details zur Verarbeitung importierter Lizenzierungsdateien auf.|Standortsystemserver|  

###  <a name="BKMK_BnRLog"></a> Sicherung und Wiederherstellung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Sicherungs- und Wiederherstellungsaktionen enthalten, darunter das Zurücksetzen von Standorten und Änderungen am SMS-Provider.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Zeichnet Informationen zu Setup- und Wiederherstellungstasks auf, wenn in Configuration Manager ein Standort aus einer Sicherung wiederhergestellt wird|Standortserver|  
|smsbkup.log|Erfasst Details zu Standortsicherungsaktivitäten.|Standortserver|  
|smssqlbkup.log|Zeichnet die Ausgabe der Standortdatenbanksicherung auf, wenn SQL Server auf einem Server als dem Standortserver installiert ist.|Standortdatenbankserver|  
|Smswriter.log|Zeichnet Informationen zum Zustand von Configuration Manager VSS Writer auf, der im Sicherungsprozess verwendet wird.|Standortserver|  

###  <a name="BKMK_CertificateEnrollment"></a> Zertifikatregistrierung  
 In der folgenden Tabelle werden die Configuration Manager-Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Zertifikatregistrierung enthalten. Die Zertifikatregistrierung verwendet den Zertifikatregistrierungspunkt und das Configuration Manager-Richtlinienmodul auf dem Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|Crp.log|Zeichnet die Registrierungsaktivitäten auf.|Zertifikatregistrierungspunkt|  
|Crpctrl.log|Zeichnet die Betriebsintegrität des Zertifikatregistrierungspunkts auf.|Zertifikatregistrierungspunkt|  
|Crpsetup.log|Zeichnet Einzelheiten über die Installation und Konfiguration des Zertifikatregistrierungspunkts auf.|Zertifikatregistrierungspunkt|  
|Crpmsi.log|Zeichnet Einzelheiten über die Installation und Konfiguration des Zertifikatregistrierungspunkts auf.|Zertifikatregistrierungspunkt|  
|NDESPlugin.log|Zeichnet die Aktivitäten der Abfrageüberprüfung und Zertifikatregistrierung auf.|Configuration Manager-Richtlinienmodul und der Registrierungsdienst für Netzwerkgeräte|  

 Prüfen Sie außer den Configuration Manager-Protokolldateien auch die Windows-Anwendungsprotokolle in der Ereignisanzeige auf dem Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, sowie auf dem Hostserver des Zertifikatregistrierungspunkts. Achten Sie beispielsweise auf Nachrichten mit der Quellangabe **NetworkDeviceEnrollmentService** . Sie können auch die folgenden Protokolldateien verwenden:  

-   IIS-Protokolldateien für den Registrierungsdienst für Netzwerkgeräte: **&lt;Pfad\>\inetpub\logs\LogFiles\W3SVC1**  

-   IIS-Protokolldateien für den Zertifikatregistrierungspunkt: **&lt;Pfad\>\inetpub\logs\LogFiles\W3SVC1**  

-   Protokolldatei für den Registrierungsdienst für Netzwerkgeräte: **mscep.log**  

    > [!NOTE]  
    >  Diese Datei befindet sich im Ordner des Kontoprofils des Registrierungsdiensts für Netzwerkgeräte, z. B. C:\Benutzer\SCEPSvc. Weitere Informationen zum Aktivieren der Protokollierung für den Registrierungsdienst für Netzwerkgeräte finden Sie im Abschnitt [Enable Logging (Aktivieren der Protokollierung)](http://go.microsoft.com/fwlink/?LinkId=320576) im Artikel „Network Device Enrollment Service (NDES) in Active Directory Certificate Services (AD CS)“ (Registrierungsdienst für Netzwerkgeräte (NDES) im Zertifikatdienst von Active Directory (AD CS)) im TechNet-Wiki.  

###  <a name="BKMK_BGB"></a> Clientbenachrichtigung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Clientbenachrichtigungen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Zeichnet Details zu den Aktivitäten auf dem Standortserver im Zusammenhang mit Clientbenachrichtigungstasks und der Verarbeitung von Online- und Taskstatusdateien auf.|Standortserver|  
|BGBServer.log|Zeichnet die Aktivitäten des Benachrichtigungsservers auf, z.B. die Kommunikation zwischen Client und Server und das Verteilen von Tasks an Clients. Außerdem werden Informationen zur Erstellung von Online- und Taskstatusdateien aufgezeichnet, die an den Standortserver gesendet werden.|Verwaltungspunkt|  
|BgbSetup.log|Zeichnet die Aktivitäten des Wrapperprozesses der Benachrichtigungsserverinstallation während der Installation und Deinstallation auf.|Verwaltungspunkt|  
|bgbisapiMSI.log|Zeichnet Details zur Installation und Deinstallation des Benachrichtigungsservers auf.|Verwaltungspunkt|  
|BgbHttpProxy.log|Zeichnet die Aktivitäten des Benachrichtigungs-HTTP-Proxys auf, wenn von diesem die Meldungen von Clients mittels HTTP von und an den Benachrichtigungsserver übermittelt werden.|Client|  
|CCMNotificationAgent.log|Zeichnet die Aktivitäten des Benachrichtigungsagenten auf, wie die Client-Server-Kommunikation und Informationen zu empfangenen und an andere Clientagenten versendeten Tasks.|Client|  

### <a name="cloud-management-gateway"></a>Cloudverwaltungsgateway

In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Cloudverwaltungsgateways enthalten.

||||
|-|-|-|
|Protokollname|Beschreibung|Computer mit Protokolldatei|
|CloudMgr.log|Zeichnet Details zur Bereitstellung des Cloudverwaltungsgateway-Dienstes, den laufenden Dienststatus und Nutzungsdaten, die mit dem Dienst verknüpft sind, auf.<br>Sie können die Protokollierungsstufe konfigurieren, indem Sie die Registrierung **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_CLOUD_SERVICES_MANAGER\Logging level** bearbeiten.|Der Ordner *installdir* auf dem primären Standortserver oder Clientzugriffsserver.|
|CMGSetup.log oder CMG-*RoleInstanceID*-CMGSetup.log<sup>1</sup>|Zeichnet Details über die 2. Phase der Bereitstellung des Cloudverwaltungsgateways (lokale Bereitstellung in Azure) auf.<br>Sie können die Protokollierungsstufe mithilfe der Einstellung **Ablaufverfolgungsebene** (**Informationen** (Standard), **Ausführlich**, **Fehler**) auf der Registerkarte **Azure-Portal\Konfiguration der Clouddienste** konfigurieren.|Die **%approot%\logs** auf Ihrem Azure-Server oder der Ordner „SMS/Logs“ auf dem Standortsystemserver|
|CMGHttpHandler.log oder CMG-*RoleInstanceID*- CMGHttpHandler.log<sup>1</sup>|Zeichnet Details zur HTTP-Handlerbindung des Cloudverwaltungsgateways mit Internetinformationsdiensten in Azure auf.<br>Sie können die Protokollierungsstufe mithilfe der Einstellung **Ablaufverfolgungsebene** (**Informationen** (Standard), **Ausführlich**, **Fehler**) auf der Registerkarte **Azure-Portal\Konfiguration der Clouddienste** konfigurieren.|Die **%approot%\logs** auf Ihrem Azure-Server oder der Ordner „SMS/Logs“ auf dem Standortsystemserver|
|CMGService.log oder CMG-*RoleInstanceID*- CMGService.log<sup>1</sup>|Zeichnet Details über die Kernkomponente des Cloudverwaltungsgateway-Diensts in Azure auf.<br>Sie können die Protokollierungsstufe mithilfe der Einstellung **Ablaufverfolgungsebene** (**Informationen** (Standard), **Ausführlich**, **Fehler**) auf der Registerkarte **Azure-Portal\Konfiguration der Clouddienste** konfigurieren.|Die **%approot%\logs** auf Ihrem Azure-Server oder der Ordner „SMS/Logs“ auf dem Standortsystemserver|
|SMS_Cloud_ProxyConnector.log|Zeichnet Details zum Einrichten von Verbindungen zwischen dem Cloud-Management-Gateway-Dienst und dem Verbindungspunkt für das Cloudverwaltungsgateway auf.|Standortsystemserver|

<sup>1</sup> Hierbei handelt es sich um lokale Configuration Manager-Protokolldateien, die der Clouddienst-Manager alle 5 Minuten aus dem Azure-Speicher synchronisiert. Das Cloudverwaltungsgateway wird alle 5 Minuten Protokolle zum Azure-Speicher übertragen. Daher wird die maximale Verzögerung 10 Minuten betragen. Ausführliche Switches wirken sich auf lokale und Remoteprotokolle aus.

- Verwenden Sie für die Problembehandlung von Bereitstellungen **CloudMgr.log** und **CMGSetup.log**.
- Verwenden Sie für die Problembehandlung der Dienstintegrität **CMGService.log** und **SMS_Cloud_ProxyConnector.log**.
- Verwenden Sie für die Problembehandlung des Client-Datenverkehrs **CMGHttpHandler.log**, **CMGService.log** und **SMS_Cloud_ProxyConnector.log**.

###  <a name="BKMK_CompSettingsLog"></a> Konformitätseinstellungen und Zugriff auf Unternehmensressourcen  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Kompatibilitätseinstellungen und dem Zugriff auf Unternehmensressourcen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Zeichnet Details zum Wiederherstellungsprozess sowie zu Kompatibilität für Kompatibilitätseinstellungen, Softwareupdates und Anwendungsverwaltung auf.|Client|  
|CITaskManager.log|Zeichnet Informationen zur Taskplanung für Konfigurationselemente auf.|Client|  
|DCMAgent.log|Zeichnet detaillierte Informationen zu Auswertung, Konfliktberichterstattung und Wiederherstellung von Konfigurationselementen und Anwendungen auf.|Client|  
|DCMReporting.log|Zeichnet Informationen zur Berichterstattung von Richtlinienplattformergebnissen in Statusmeldungen für Konfigurationselemente auf.|Client|  
|DcmWmiProvider.log|Zeichnet Informationen im Zusammenhang mit dem Einlesen von Konfigurationselement-Synclets aus WMI auf.|Client|  

###  <a name="BKMK_ConsoleLog"></a> Configuration Manager-Konsole  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen zur Configuration Manager-Konsole enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Zeichnet die Installation der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SmsAdminUI.log|Zeichnet Informationen zum Betrieb der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SMSProv.log|Zeichnet die vom SMS-Anbieter ausgeführten Aktivitäten auf. Configuration Manager-Konsolenaktivitäten verwenden den SMS-Anbieter.|Standortserver oder Standortsystemserver|  

###  <a name="BKMK_ContentLog"></a> Content Management  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Inhaltsverwaltung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Zeichnet Einzelheiten eines speziellen cloudbasierten Verteilungspunkts auf, einschließlich Informationen über die Speicherung und den Zugriff auf Inhalten.|Standortsystemserver|  
|CloudMgr.log|Zeichnet Einzelheiten über die Bereitstellung von Inhalten, die Sammlung von Speicherungs- und Bandbreitenstatistiken sowie vom Administrator ergriffene Maßnahmen zum Anhalten oder Starten des Clouddiensts, der an einem cloudbasierten Verteilungspunkt ausgeführt wird, auf.|Standortsystemserver|  
|DataTransferService.log|Zeichnet die gesamte BITS-Kommunikation für den Richtlinien- oder Paketzugriff auf. Dieses Protokoll wird auch für das Content Management von Pullverteilungspunkten verwendet.|Ein Computer, der als Pullverteilungspunkt konfiguriert ist|  
|PullDP.log|Zeichnet Details über Inhalte auf, die der Pullverteilungspunkt aus Quellverteilungspunkten überträgt.|Ein Computer, der als Pullverteilungspunkt konfiguriert ist|  
|PrestageContent.log|Zeichnet die Details zur Verwendung des Tools ExtractContent.exe auf einem vorab bereitgestellten Remoteverteilungspunkt auf. Mit diesem Tool werden Inhalte extrahiert, die in eine Datei exportiert wurden.|Standortsystemrolle|  
|SMSdpmon.log|Zeichnet Details zum geplanten Task für die Integritätsüberwachung des Verteilungspunkts auf, der auf einem Verteilungspunkt konfiguriert wurde.|Standortsystemrolle|  
|smsdpprov.log|Zeichnet Details zur Extrahierung komprimierter Dateien auf, die von einem primären Standort stammen. Dieses Protokoll wird vom WMI-Anbieter des Remoteverteilungspunkts generiert.|Ein Verteilungspunktcomputer an einem anderen Standort als der Standortserver|  


###  <a name="BKMK_DiscoveryLog"></a> Ermittlung  
In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen zur Ermittlung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Sicherheitsgruppenermittlung auf.|Standortserver|  
|adsysdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Systemermittlung auf.|Standortserver|  
|adusrdis.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Benutzerermittlung auf.|Standortserver|  
|ADForestDisc.log|Zeichnet Aktionen im Zusammenhang mit der Active Directory-Gesamtstrukturermittlung auf.|Standortserver|  
|ddm.log|Zeichnet die Aktivitäten des Ermittlungsdaten-Managers auf.|Standortserver|  
|InventoryAgent.log|Zeichnet Aktivitäten im Zusammenhang mit Hardwareinventur, Softwareinventur und Frequenzermittlung auf dem Client auf.|Client|  
|netdisc.log|Zeichnet Aktionen im Zusammenhang mit der Netzwerkermittlung auf.|Standortserver|  

###  <a name="BKMK_EPLog"></a> Endpoint Protection  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Endpoint Protection enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Zeichnet Details zur Installation des Endpoint Protection-Clients und zum Anwenden der Richtlinie für Antischadsoftware auf diesen Client auf.|Client|  
|EPCtrlMgr.log|Zeichnet Details zur Synchronisierung von Schadsoftwarebedrohungsdaten vom Endpoint Protection-Rollenserver in die Configuration Manager-Datenbank auf.|Standortsystemserver|  
|EPMgr.log|Überwacht den Status der Endpoint Protection-Standortsystemrolle.|Standortsystemserver|  
|EPSetup.log|Stellt Informationen zur Installation der Endpoint Protection-Standortsystemrolle bereit.|Standortsystemserver|  

###  <a name="BKMK_Extensions"></a> Erweiterungen  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Erweiterungen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Zeichnet Informationen zum Download von Erweiterungen von Microsoft sowie zur Installation und Deinstallation aller Erweiterungen auf.|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|FeatureExtensionInstaller.log|Zeichnet Informationen zur Installation und Deinstallation von einzelnen Erweiterungen auf, wenn diese in der Configuration Manager-Konsole aktiviert oder deaktiviert werden|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SmsAdminUI.log|Zeichnet die Aktivität der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  

###  <a name="BKMK_InventoryLog"></a> Inventur  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Verarbeitung von Inventurdaten enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Zeichnet Informationen zur Verarbeitung von MIF-Dateien und Hardwareinventur in der Configuration Manager-Datenbank auf.|Standortserver|  
|invproc.log|Zeichnet die Weiterleitung von MIF-Dateien von einem sekundären Standort an dessen übergeordneten Standort auf.|Sekundärer Standortserver|  
|sinvproc.log|Zeichnet Informationen zur Verarbeitung der Softwareinventurdaten in die Standortdatenbank auf.|Standortserver|  

###  <a name="BKMK_MeteringLog"></a> Messung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Messungen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Überwacht alle Softwaremessungen.|Standortserver|  

###  <a name="BKMK_MigrationLog"></a> Migration  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Migration enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Zeichnet Informationen zu Migrationsaktionen auf, einschließlich Migrationsaufträge, freigegebener Verteilungspunkte und Upgrades von Verteilungspunkten.|Standort der obersten Ebene in der Configuration Manager-Hierarchie und jeder untergeordnete primäre Standort<br /><br /> Verwenden Sie in einer Hierarchie mit mehreren primären Standorten die Protokolldatei, die auf dem Standort der zentralen Verwaltung erstellt wurde.|  

###  <a name="BKMK_MDMLog"></a> Mobile Geräte  
 In den folgenden Abschnitten werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Verwaltung mobiler Geräte enthalten.  

####  <a name="BKMK_EnrollmentLog"></a> Registrierung  
 In der folgenden Tabelle werden Protokolle aufgelistet, die Informationen im Zusammenhang mit der Anmeldung mobiler Geräte enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Zeichnet die Kommunikation zwischen Verwaltungspunkten, die für mobile Geräte aktiviert sind, und den Endpunkten der Verwaltungspunkte auf.|Standortsystemserver|  
|dmpmsi.log|Zeichnet die Windows Installer-Daten für die Konfiguration eines für mobile Geräte aktivierten Verwaltungspunkts auf.|Standortsystemserver|  
|DMPSetup.log|Zeichnet die Konfiguration des Verwaltungspunkts auf, wenn dieser für mobile Geräte aktiviert wird.|Standortsystemserver|  
|enrollsrvMSI.log|Zeichnet die Windows Installer-Daten für die Konfiguration eines Anmeldungspunkts auf.|Standortsystemserver|  
|enrollmentweb.log|Zeichnet die Kommunikation zwischen mobilen Geräten und dem Anmeldungsproxypunkt auf.|Standortsystemserver|  
|enrollwebMSI.log|Zeichnet die Windows Installer-Daten für die Konfiguration eines Anmeldungsproxypunkts auf.|Standortsystemserver|  
|enrollmentservice.log|Zeichnet die Kommunikation zwischen einem Anmeldungsproxypunkt und einem Anmeldungspunkt auf.|Standortsystemserver|  
|SMS_DM.log|Zeichnet die Kommunikation zwischen mobilen Geräten, Macintosh-Computern und dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  

####  <a name="BKMK_ExchSrvLog"></a> Exchange Server-Connector  
 Die folgenden Protokolle enthalten Informationen im Zusammenhang mit dem Exchange Server-Connector.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Zeichnet die Aktivitäten und den Status des Exchange Server-Connectors auf.|Standortserver|  

####  <a name="BKMK_MDLegLog"></a> Legacyclient für mobile Geräte  
 In der folgenden Tabelle werden Protokolle aufgelistet, die Informationen im Zusammenhang mit dem Legacyclient für mobile Geräte enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Zeichnet Details zu Zertifikatanmeldungsdaten auf Legacyclients für mobile Geräte auf.|Client|  
|DMCertResp.htm|Zeichnet die HTML-Antwort des Zertifikatsservers auf die Anforderung eines PKI-Zertifikats durch das Anmeldungsprogramm des Legacyclients für mobile Geräte auf.|Client|  
|DmClientHealth.log|Zeichnet die GUIDs aller Legacyclients für mobile Geräte auf, die mit dem für mobile Geräte aktivierten Verwaltungspunkt kommunizieren.|Standortsystemserver|  
|DmClientRegistration.log|Zeichnet Registrierungsanforderungen und -antworten im Zusammenhang mit Legacyclients für mobile Geräte auf.|Standortsystemserver|  
|DmClientSetup.log|Zeichnet Daten des Client-Setup für Legacyclients für mobile Geräte auf.|Client|  
|DmClientXfer.log|Zeichnet die Clientübertragungsdaten für Legacyclients für mobile Geräte und für ActiveSync-Bereitstellungen auf.|Client|  
|DmCommonInstaller.log|Zeichnet die Installation von Clientübertragungsdateien für die Konfiguration von Übertragungsdateien von Legacyclients für mobile Geräte auf.|Client|  
|DmInstaller.log|Zeichnet auf, ob „DmClientSetup“ ordnungsgemäß von „DMInstaller“ aufgerufen wird und ob „DmClientSetup“ erfolgreich oder mit einem Fehler auf Legacyclients für mobile Geräte abgeschlossen wird.|Client|  
|DmpDatastore.log|Zeichnet alle Verbindungen zur Standortdatenbank und alle Abfragen vom für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmpDiscovery.log|Zeichnet alle Ermittlungsdaten von den Legacyclients für mobile Geräte auf dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmpHardware.log|Zeichnet alle Hardwareinventurdaten von den Legacyclients für mobile Geräte auf dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmpIsapi.log|Zeichnet die Kommunikation zwischen dem Legacyclient für mobile Geräte und dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|dmpmsi.log|Zeichnet die Windows Installer-Daten für die Konfiguration eines für mobile Geräte aktivierten Verwaltungspunkts auf.|Standortsystemserver|  
|DMPSetup.log|Zeichnet die Konfiguration des Verwaltungspunkts auf, wenn dieser für mobile Geräte aktiviert wird.|Standortsystemserver|  
|DmpSoftware.log|Zeichnet Softwareverteilungsdaten von den Legacyclients für mobile Geräte auf einem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmpStatus.log|Zeichnet Statusmeldungsdaten von den Clients für mobile Geräte auf einem für mobile Geräte aktivierten Verwaltungspunkt auf.|Standortsystemserver|  
|DmSvc.log|Zeichnet die Kommunikation zwischen dem Legacyclient für mobile Geräte und dem für mobile Geräte aktivierten Verwaltungspunkt auf.|Client|  
|FspIsapi.log|Zeichnet Details zur Kommunikation von mobilen Legacyclient-Geräten und Clientcomputern mit dem Fallbackstatuspunkt auf.|Standortsystemserver|  

###  <a name="BKMK_OSDLog"></a> Betriebssystembereitstellung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Bereitstellung von Betriebssystemen enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CAS.log|Zeichnet die Details von Verteilungspunkten auf, die für referenzierten Inhalt gefunden werden.|Client|  
|ccmsetup.log|Zeichnet ccmsetup-Tasks für Clienteinstellung, Clientupgrade und Cliententfernung auf. Ist für die Problembehandlung bei Clientinstallationsproblemen hilfreich.|Client|  
|CreateTSMedia.log|Zeichnet Details zur Tasksequenz „Medienerstellung“ auf.|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|DeployToVhd.log|Hier werden Details zum VHD-Erstellungs- und Änderungsvorgang aufgezeichnet.|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|Dism.log|Zeichnet Aktionen im Zusammenhang mit der Treiberinstallation oder der Anwendung von Updates für die Offlinewartung auf.|Standortsystemserver|  
|distmgr.log|Zeichnet Details zur Konfiguration beim Aktivieren eines Verteilungspunkts für Preboot Execution Environment (PXE) auf.|Standortsystemserver|  
|DriverCatalog.log|Zeichnet Details zu Gerätetreibern auf, die in den Treiberkatalog importiert wurden.|Standortsystemserver|  
|mcsisapi.log|Zeichnet Informationen im Zusammenhang mit Multicast-Paketübertragungen und Clientanforderungsantworten auf.|Standortsystemserver|  
|mcsexec.log|Zeichnet Aktionen im Zusammenhang mit Integritätsprüfung, Namespaces, Sitzungserstellung und Zertifikatprüfung auf.|Standortsystemserver|  
|mcsmgr.log|Zeichnet Änderungen an Konfiguration, Sicherheitsmodus und Verfügbarkeit auf.|Standortsystemserver|  
|mcsprv.log|Zeichnet die Interaktion zwischen Multicastanbieter und WDS (Windows Deployment Services) auf.|Standortsystemserver|  
|MCSSetup.log|Zeichnet Details zur Installation der Multicastserverrolle auf.|Standortsystemserver|  
|MCSMSI.log|Zeichnet Details zur Installation der Multicastserverrolle auf.|Standortsystemserver|  
|Mcsperf.log|Zeichnet Details zu Updates von Multicastleistungsindikatoren auf.|Standortsystemserver|  
|MP_ClientIDManager.log|Zeichnet Antworten des Verwaltungspunkts auf Tasksequenzen zur Anforderung der Client-ID auf, die von PXE oder von Startmedien initiiert wurden.|Standortsystemserver|  
|MP_DriverManager.log|Zeichnet Antworten des Verwaltungspunkts auf Aktionsanforderungen über die Tasksequenz „Treiber automatisch anwenden“ auf.|Standortsystemserver|  
|OfflineServicingMgr.log|Zeichnet Details zur Planung von Offlinewartungsmaßnahmen und zum Anwenden von Updates auf WIM-Dateien des Betriebssystems auf.|Standortsystemserver|  
|Setupact.log|Zeichnet Details zu Windows-Sysprep- und -Setup-Protokollen auf.|Client|  
|Setupapi.log|Zeichnet Details zu Windows-Sysprep- und -Setup-Protokollen auf.|Client|  
|Setuperr.log|Zeichnet Details zu Windows-Sysprep- und -Setup-Protokollen auf.|Client|  
|smpisapi.log|Zeichnet Details zum Erfassen und Wiederherstellen des Clientzustands sowie Schwellenwertinformationen auf.|Client|  
|Smpmgr.log|Zeichnet Details zu den Ergebnissen von Integritätsprüfungen und Konfigurationsänderungen von Zustandsmigrationspunkten auf.|Standortsystemserver|  
|smpmsi.log|Zeichnet Installations- und Konfigurationsdetails zum Zustandsmigrationspunkt auf.|Standortsystemserver|  
|smpperf.log|Zeichnet Details zu Updates von Leistungsindikatoren für Zustandsmigrationspunkte auf.|Standortsystemserver|  
|smspxe.log|Zeichnet Details zu den Antworten an Clients mit PXE-Start sowie Details zur Erweiterung von Startimages und Startdateien auf.|Standortsystemserver|  
|smssmpsetup.log|Zeichnet Installations- und Konfigurationsdetails zum Zustandsmigrationspunkt auf.|Standortsystemserver|  
|Smsts.log|Zeichnet Tasksequenzaktivitäten auf.|Client|  
|TSAgent.log|Zeichnet das Ergebnis von Tasksequenzabhängigkeiten vor dem Starten einer Tasksequenz auf.|Client|  
|TaskSequenceProvider.log|Zeichnet Details zu Tasksequenzen auf, wenn diese importiert, exportiert oder bearbeitet werden.|Standortsystemserver|  
|loadstate.log|Zeichnet Details zum Migrationsprogramm für den Benutzerzustand (USMT) sowie zur Wiederherstellung von Benutzerzustandsdaten auf.|Client|  
|scanstate.log|Zeichnet Details zum Migrationsprogramm für den Benutzerzustand (USMT) sowie zur Erfassung von Benutzerzustandsdaten auf.|Client|  

###  <a name="BKMK_PowerMgmtLog"></a> Energieverwaltung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Energiewaltung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|Zeichnet Details zu Energieverwaltungsaktivitäten auf dem Clientcomputer auf, einschließlich der Überwachung und Erzwingung von Einstellungen durch den Energieverwaltungsclient-Agent.|Client|  

###  <a name="BKMK_RCLog"></a> Remotesteuerung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Remotesteuerung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Zeichnet Details zur Aktivität des Remotesteuerungsviewers auf.|Im %temp%-Ordner auf dem Computer, auf dem der Remotesteuerungsviewer ausgeführt wird|  

###  <a name="BKMK_ReportLog"></a> Berichterstellung  
 In der folgenden Tabelle werden die Configuration Manager-Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Berichterstattung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Zeichnet Informationen im Zusammenhang mit den Aktivitäten und dem Status des Reporting Services-Punkts auf.|Standortsystemserver|  
|srsrpMSI.log|Zeichnet detaillierte Ergebnisse der Installation des Reporting Services-Punkts aus der MSI-Ausgabe auf.|Standortsystemserver|  
|srsrpsetup.log|Zeichnet Ergebnisse der Installation des Reporting Services-Punkts auf.|Standortsystemserver|  

###  <a name="BKMK_RBALog"></a> Rollenbasierte Verwaltung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der rollenbasierten Verwaltung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|hman.log|Zeichnet Informationen zu Standortkonfigurationsänderungen und zur Veröffentlichung von Standortinformationen in Active Directory Domain Services auf.|Standortserver|  
|SMSProv.log|Zeichnet den Zugriff des WMI-Anbieters auf die Standortdatenbank auf.|Computer mit dem SMS-Anbieter|  

###  <a name="BKMK_WITLog"></a> Dienstverbindungspunkt  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Dienstverbindungspunkt enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Zeichnet Zertifikat- und Proxykontoinformationen auf.|Standortserver|  
|colleval.log|Zeichnet Details zum Erstellen, Ändern und Löschen von Sammlungen durch den Sammlungsauswerter auf.|Primärer Standort und Standort der zentralen Verwaltung|  
|Cloudusersync.log|Zeichnet die Lizenzaktivierung für Benutzer auf.|Computer mit dem Dienstverbindungspunkt|  
|dataldr.log|Zeichnet Informationen über die Verarbeitung von MIF-Dateien auf.|Standortserver|  
|ddm.log|Zeichnet die Aktivitäten des Ermittlungsdaten-Managers auf.|Standortserver|  
|distmgr.log|Zeichnet Details zu Inhaltsverteilungsanforderungen auf.|Standortserver auf oberster Ebene|  
|Dmpdownloader.log|Zeichnet Details zu Downloads von Microsoft Intune auf.|Computer mit dem Dienstverbindungspunkt|  
|Dmpuploader.log|Zeichnet Details für das Hochladen von Datenbankänderungen in Microsoft Intune auf.|Computer mit dem Dienstverbindungspunkt|  
|hman.log|Zeichnet Informationen zur Meldungsweiterleitung auf.|Standortserver|  
|objreplmgr.log|Zeichnet die Verarbeitung von Richtlinien und Zuweisung auf.|Primärer Standortserver|  
|policypv.log|Zeichnet die Richtliniengenerierung aller Richtlinien auf.|Standortserver|  
|outgoingcontentmanager.log|Zeichnet Inhalte auf, die auf Microsoft Intune hochgeladen werden|Computer mit dem Dienstverbindungspunkt|  
|sitecomp.log|Zeichnet Details zur Installation des Dienstverbindungspunkts auf.|Standortserver|  
|SmsAdminUI.log|Zeichnet die Aktivität der Configuration Manager-Konsole auf|Computer, auf dem die Configuration Manager-Konsole ausgeführt wird|  
|SMSProv.log|Zeichnet die vom SMS-Anbieter ausgeführten Aktivitäten auf. Configuration Manager-Konsolenaktivitäten verwenden den SMS-Anbieter.|Computer mit dem SMS-Anbieter|  
|SrvBoot.log|Zeichnet Details zum Dienstverbindungspunkt-Installationsdienst auf.|Computer mit dem Dienstverbindungspunkt|  
|Statesys.log|Zeichnet die Verarbeitung von Verwaltungsmeldungen zu mobilen Geräten auf.|Primärer Standort und Standort der zentralen Verwaltung|  

###  <a name="BKMK_SU_NAPLog"></a> Softwareupdates  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit Softwareupdates enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|Ccmperf.log|Zeichnet Aktivitäten im Zusammenhang mit Wartung und Erfassung von Daten zu Clientleistungsindikatoren auf.|Client|  
|PatchDownloader.log|Zeichnet Details zum Download von Softwareupdates von der Updatequelle in das Downloadziel auf dem Standortserver.|Der Computer, auf dem die Configuration Manager-Konsole gehostet wird, von der Downloads initiiert werden|  
|PolicyEvaluator.log|Zeichnet Details zur Auswertung von Richtlinien auf Clientcomputern, einschließlich Softwareupdates, auf.|Client|  
|RebootCoordinator.log|Zeichnet Details zur Koordinierung von Systemneustarts auf Clientcomputern nach der Installation von Softwareupdates auf.|Client|  
|ScanAgent.log|Zeichnet Details zu Überprüfungsanforderungen für Softwareupdates, zum WSUS-Speicherort sowie zu entsprechenden Aktionen auf.|Client|  
|SdmAgent.log|Zeichnet Details zur Nachverfolgung von Wiederherstellung und Konformität auf. Die Protokolldatei für Softwareupdates „Updateshandler.log“ bietet jedoch umfangreichere Informationen zur Installation der für die Konformität benötigten Softwareupdates.<br /><br /> Diese Protokolldatei wird mit Kompatibilitätseinstellungen gemeinsam genutzt.|Client|  
|ServiceWindowManager.log|Zeichnet Details zur Auswertung von Wartungsfenstern auf.|Client|  
|SmsWusHandler.log|Zeichnet Details zum Überprüfungsvorgang für das Inventurprogramm für Microsoft Updates auf.|Client|  
|StateMessage.log|Zeichnet Details zu Zustandsmeldungen für Softwareupdates auf, die erstellt und an den Verwaltungspunkt gesendet werden.|Client|  
|SUPSetup.log|Zeichnet Details zur Installation des Softwareupdatepunkts auf. Nach Abschluss der Softwareupdatepunkt-Installation wird **Installation was successful** in diese Protokolldatei geschrieben.|Standortsystemserver|  
|UpdatesDeployment.log|Zeichnet Details zu Bereitstellungen auf dem Client auf, einschließlich Softwareupdateaktivierung, Auswertung und Erzwingung. Die ausführliche Protokollierung zeigt zusätzliche Informationen zur Interaktion mit der Clientbenutzeroberfläche an.|Client|  
|UpdatesHandler.log|Zeichnet Details zur Softwareupdate-Kompatibilitätsüberprüfung, zum Download und zur Installation von Softwareupdates auf dem Client auf.|Client|  
|UpdatesStore.log|Zeichnet Details zum Kompatibilitätsstatus für Softwareupdates auf, die im Rahmen des Kompatibilitätsüberprüfungszyklus bewertet wurden.|Client|  
|WCM.log|Zeichnet Details zur Konfiguration von Softwareupdatepunkten und zum Herstellen einer Verbindung mit WSUS-Server für abonnierte Updatekategorien, Klassifizierungen und Sprachen auf.|Standortserver|  
|WSUSCtrl.log|Zeichnet Details zur Konfiguration, Datenbankverbindungen und der Integrität von WSUS-Servern für den Standort auf.|Standortsystemserver|  
|wsyncmgr.log|Zeichnet Details zum Synchronisierungsprozess von Softwareupdates auf.|Standortserver|  
|WUAHandler.log|Zeichnet Details zum Windows Update-Agent auf dem Client bei der Suche nach Softwareupdates auf.|Client|  

###  <a name="BKMK_WOLLog"></a> Wake-On-LAN  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Verwendung von Wake-On-LAN enthalten.  

> [!NOTE]  
>  Wenn Sie Wake-On-LAN durch die Verwendung des Aktivierungsproxys ergänzen, wird diese Aktivität auf dem Client protokolliert. Siehe beispielsweise „CcmExec.log“ und SleepAgent_<*Domäne*\>@SYSTEM_0.log im Abschnitt [Clientvorgänge](#BKMK_ClientOpLogs) in diesem Thema.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Zeichnet Details dazu auf, welche Clients Aktivierungspakete erhalten müssen, die Anzahl der gesendeten Aktivierungspakete und die Anzahl an wiederholten Aktivierungspaketen.|Standortserver|  
|wolmgr.log|Zeichnet Details zu Aktivierungsverfahren auf, beispielsweise zum Zeitpunkt der Aktivierung von Bereitstellungen, die für Wake-On-LAN konfiguriert wurden.|Standortserver|  

###  <a name="BKMK_WindowsServicingLog"></a> Windows 10-Wartung  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit der Windows 10-Wartung enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|Ccmperf.log|Zeichnet Aktivitäten im Zusammenhang mit Wartung und Erfassung von Daten zu Clientleistungsindikatoren auf.|Client|  
|CcmRepair.log|Zeichnet Reparaturaktivitäten des Client-Agents auf.|Client|
|PatchDownloader.log|Zeichnet Details zum Download von Softwareupdates von der Updatequelle in das Downloadziel auf dem Standortserver.|Der Computer, auf dem die Configuration Manager-Konsole gehostet wird, von der Downloads initiiert werden|  
|PolicyEvaluator.log|Zeichnet Details zur Auswertung von Richtlinien auf Clientcomputern, einschließlich Softwareupdates, auf.|Client|  
|RebootCoordinator.log|Zeichnet Details zur Koordinierung von Systemneustarts auf Clientcomputern nach der Installation von Softwareupdates auf.|Client|  
|ScanAgent.log|Zeichnet Details zu Überprüfungsanforderungen für Softwareupdates, zum WSUS-Speicherort sowie zu entsprechenden Aktionen auf.|Client|  
|SdmAgent.log|Zeichnet Details zur Nachverfolgung von Wiederherstellung und Konformität auf. Die Protokolldatei für Softwareupdates „Updateshandler.log“ bietet jedoch umfangreichere Informationen zur Installation der für die Konformität benötigten Softwareupdates.<br /><br /> Diese Protokolldatei wird mit Kompatibilitätseinstellungen gemeinsam genutzt.|Client|  
|ServiceWindowManager.log|Zeichnet Details zur Auswertung von Wartungsfenstern auf.|Client|  
|setupact.log|Primäre Protokolldatei für die meisten Fehler, die während der Installation von Windows auftreten. Die Protokolldatei befindet sich im Ordner % windir%\$Windows.~BT\sources\panther.|Client|
|SmsWusHandler.log|Zeichnet Details zum Überprüfungsvorgang für das Inventurprogramm für Microsoft Updates auf.|Client|  
|StateMessage.log|Zeichnet Details zu Softwareupdate-Zustandsmeldungen auf, die erstellt und an den Verwaltungspunkt gesendet werden.|Client|  
|SUPSetup.log|Zeichnet Details zur Installation des Softwareupdatepunkts auf. Nach Abschluss der Softwareupdatepunkt-Installation wird **Installation was successful** in diese Protokolldatei geschrieben.|Standortsystemserver|  
|UpdatesDeployment.log|Zeichnet Details zu Bereitstellungen auf dem Client auf, einschließlich Softwareupdateaktivierung, Auswertung und Erzwingung. Die ausführliche Protokollierung zeigt zusätzliche Informationen zur Interaktion mit der Clientbenutzeroberfläche an.|Client|  
|Updateshandler.log|Zeichnet Details zur Softwareupdate-Kompatibilitätsüberprüfung, zum Download und zur Installation von Softwareupdates auf dem Client auf.|Client|  
|UpdatesStore.log|Zeichnet Details zum Kompatibilitätsstatus für Softwareupdates auf, die im Rahmen des Kompatibilitätsüberprüfungszyklus bewertet wurden.|Client|  
|WCM.log|Zeichnet Details zur Konfiguration von Softwareupdatepunkten und zum Herstellen einer Verbindung mit WSUS-Server für abonnierte Updatekategorien, Klassifizierungen und Sprachen auf.|Standortserver|  
|WSUSCtrl.log|Zeichnet Details zur Konfiguration, Datenbankverbindungen und der Integrität von WSUS-Servern für den Standort auf.|Standortsystemserver|  
|wsyncmgr.log|Zeichnet Details zum Synchronisierungsprozess von Softwareupdates auf.|Standortserver|  
|WUAHandler.log|Zeichnet Details zum Windows Update-Agent auf dem Client bei der Suche nach Softwareupdates auf.|Client|  

###  <a name="BKMK_WULog"></a> Windows Update-Agent  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem Windows Update-Agent enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Zeichnet Details dazu auf, wann der Windows Update-Agent eine Verbindung mit dem WSUS-Server herstellt und die Softwareupdates für die Konformitätsbewertung abruft und ob Updates für die Agent-Komponenten vorhanden sind.|Client|  

###  <a name="BKMK_WSUSLog"></a> WSUS-Server  
 In der folgenden Tabelle werden die Protokolldateien aufgelistet, die Informationen im Zusammenhang mit dem WSUS-Server enthalten.  

|Protokollname|Beschreibung|Computer mit Protokolldatei|  
|--------------|-----------------|----------------------------|  
|Change.log|Zeichnet Details zu geänderten WSUS-Server-Datenbankinformationen auf.|WSUS-Server|  
|SoftwareDistribution.log|Zeichnet Details zu Softwareupdates auf, die von der konfigurierten Updatequelle zur WSUS-Serverdatenbank synchronisiert werden.|WSUS-Server|  
