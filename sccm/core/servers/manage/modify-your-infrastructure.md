---
title: "Ändern der Infrastruktur | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie Änderungen vornehmen oder Aktionen durchführen, die sich auf die von Ihnen bereitgestellte Configuration Manager-Infrastruktur auswirken."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: a5228c4984347be4b115bfa5563791fa2fb7319c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>Ändern Ihrer System Center Configuration Manager-Infrastruktur

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachdem Sie einen oder mehrere Standorte installiert haben, müssen Sie möglicherweise Konfigurationen ändern oder Aktionen ausführen, die sich auf die von Ihnen bereitgestellte Infrastruktur auswirken.  


##  <a name="BKMK_ManageSMSprovider"></a> Verwalten des SMS-Anbieters  
 Der SMS-Anbieter (eine Dynamic-Link Library-Datei: smsprov.dll) stellt den administrativen Kontaktpunkt für eine oder mehrere Configuration Manager-Konsolen bereit. Wenn Sie mehrere SMS-Anbieter installieren, können Sie Redundanz für Kontaktpunkte zur Verwaltung des Standorts und der Hierarchie bereitstellen.  

 An jedem Configuration Manager-Standort können Sie das Setup mit folgenden Zielen erneut ausführen:  

-   Hinzufügen einer zusätzlichen Instanz des SMS-Anbieters (jede zusätzliche Instanz des SMS-Anbieters muss sich auf einem separaten Computer befinden)  

-   Entfernen einer Instanz des SMS-Anbieters (um den letzten SMS-Anbieter für einen Standort zu entfernen, müssen Sie den Standort deinstallieren)  

 Sie können die Installation bzw. das Entfernen eines SMS-Anbieters anhand der Protokolldatei **ConfigMgrSetup.log** überwachen. Sie finden die Datei im Stammordner des Standortservers, auf dem Sie Setup ausführen.  

 Machen Sie sich mit den Informationen unter [Plan for the SMS Provider for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Planen des SMS-Anbieters für System Center Configuration Manager) vertraut, bevor Sie den SMS-Anbieter an einem Standort ändern.  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>So verwalten Sie die SMS-Anbieterkonfiguration für einen Standort  

1.  Führen Sie das **Configuration Manager-Setup** über den **&lt;Installationsordner des Configuration Manager-Standorts \>\BIN\X64\setup.exe** aus.  

2.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**aus, und klicken Sie dann auf **Weiter**.  

3.  Wählen Sie auf der Seite **Standortwartung** die Option **SMS-Anbieterkonfiguration ändern**aus, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie auf der Seite **SMS-Anbieter verwalten** eine der folgenden Optionen aus, und schließen Sie dann den Assistenten der Option entsprechend ab:  

    -   Wenn Sie diesem Standort einen zusätzlichen SMS-Anbieter hinzufügen möchten:  

         Wählen Sie **Neuen SMS-Anbieter hinzufügen**aus, geben Sie den FQDN für einen Computer an, auf dem der SMS-Anbieter gehostet werden soll und auf dem zurzeit kein SMS-Anbieter gehostet wird, und klicken Sie dann auf **Weiter**.  

    -   Wenn Sie einen SMS-Anbieter entfernen möchten:  

         Wählen Sie **Angegebenen SMS-Anbieter deinstallieren**aus, wählen Sie den Namen des Computers aus, von dem der SMS-Anbieter entfernt werden soll, klicken Sie auf **Weiter**, und bestätigen Sie dann die Aktion.  

        > [!TIP]  
        >  Wenn Sie einen SMS-Anbieter von einem Computer auf einen anderen Computer verschieben möchten, müssen Sie den SMS-Anbieter auf dem neuen Computer installieren und ihn vom ursprünglichen Speicherort entfernen. Es gibt keine spezielle Option, mit der ein SMS-Anbieter in einem Schritt von einem Computer auf einen anderen verschoben werden kann.  

 Mit dem Beenden des Setup-Assistenten ist die SMS-Anbieterkonfiguration abgeschlossen. Sie können auf der Registerkarte **Allgemein** im Dialogfeld **Standorteigenschaften** können Sie die Computer überprüfen, bei denen ein SMS-Anbieter für einen Standort installiert ist.  

##  <a name="bkmk_Console"></a> Verwalten der Configuration Manager-Konsole  
 Nachfolgend sind Aufgaben aufgeführt, mit denen Sie die Configuration Manager-Konsole verwalten können:  

-   **Ändern der Sprache, in der die Configuration Manager-Konsole angezeigt wird** – Informationen zum Ändern der installierten Sprachen finden Sie unter [Verwalten der Sprache der Configuration Manager-Konsole](#BKMK_ManageConsoleLanguages) in diesem Thema.  

-   **Installieren zusätzlicher Konsolen** – Informationen zum Installieren zusätzlicher Konsolen finden Sie unter [Installieren von System Center Configuration Manager-Konsolen](/sccm/core/servers/deploy/install/install-consoles).  

-   **Konfigurieren von DCOM** – Informationen zum Konfigurieren der DCOM-Berechtigung für das Aktivieren von Konsolen, die sich nicht am selben Ort wie der Standortserver befinden, finden Sie unter [Konfigurieren von DCOM-Berechtigungen für Configuration Manager-Remotekonsolen](#BKMK_ConfigDCOMforRemoteConsole) in diesem Thema.  

-   **Ändern von Berechtigungen, um die Anzeige in der Konsole für Administratoren zu begrenzen** – Informationen zum Ändern von Administratorberechtigungen, sodass die Anzeige und der Bereich möglicher Aktionen in der Konsole für Benutzer begrenzt werden, finden Sie unter [Ändern des Verwaltungsbereichs eines Administrators](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser).     

###  <a name="BKMK_ManageConsoleLanguages"></a> Verwalten der Sprache der Configuration Manager-Konsole  
 Während der Installation des Standortservers werden die Configuration Manager-Konsoleninstallationsdateien und unterstützten Sprachpakete für den Standort in den Unterordner **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup** auf dem Standortserver kopiert.  

-   Wenn Sie die Installation der Configuration Manager-Konsole von diesem Ordner auf dem Standortserver aus starten, werden die Configuration Manager-Konsole und die unterstützten Sprachpaketdateien auf den Computer kopiert  

-   Wenn ein Sprachpaket für die aktuelle Spracheinstellung des Computers verfügbar ist, wird die Configuration Manager-Konsole in der betreffenden Sprache geöffnet  

-   Anderenfalls wird die Configuration Manager-Konsole in englischer Sprache geöffnet  

Stellen Sie sich beispielsweise ein Szenario vor, in dem Sie die Configuration Manager-Konsole von einem Standortserver aus installieren, der die Sprachen Deutsch, Englisch und Französisch unterstützt. Wenn Sie die Configuration Manager-Konsole auf einem Computer mit der konfigurierten Spracheinstellung „Französisch“ öffnen, wird die Konsole in französischer Sprache geöffnet. Wenn Sie die Configuration Manager-Konsole auf einem Computer mit der konfigurierten Spracheinstellung „Japanisch“ öffnen, wird die Konsole in englischer Sprache geöffnet, da das japanische Sprachpaket nicht verfügbar ist.  

 Bei jedem Öffnen der Configuration Manager-Konsole wird die konfigurierte Spracheinstellung für den Computer ermittelt und überprüft, ob ein zugeordnetes Sprachpaket für die Configuration Manager-Konsole verfügbar ist. Anschließend wird die Konsole unter Verwendung des entsprechenden Sprachpakets geöffnet. Wenn Sie die Configuration Manager-Konsole unabhängig von den konfigurierten Spracheinstellungen des Computers in englischer Sprache öffnen möchten, müssen Sie die Sprachpaketdateien auf dem Computer manuell entfernen oder umbenennen.  

 Wenden Sie die folgenden Verfahren an, um die Configuration Manager-Konsole unabhängig von der konfigurierten Gebietsschemaeinstellung des Computers in englischer Sprache zu öffnen.  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>So installieren Sie nur die englische Version der Configuration Manager-Konsole auf Computern  

1.  Wechseln Sie in Windows-Explorer zu **&lt;ConfigMgrInstallationPath\>\Tools\ConsoleSetup\LanguagePack**  

2.  Benennen Sie die **.msp** - und **.mst** -Dateien um. Sie könnten beispielsweise **&lt;Dateiname\>.MSP** in **&lt;Dateiname\>.MSP.disabled** ändern.  

3.  Installieren Sie die Configuration Manager-Konsole auf dem Computer.  

    > [!IMPORTANT]  
    >  Wenn für den Standortserver neue Serversprachen konfiguriert werden, werden die MSP- und MST-Dateien erneut in den Ordner **LanguagePack** kopiert, und Sie müssen dieses Verfahren wiederholen, um Configuration Manager-Konsolen nur auf Englisch zu installieren.  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>So deaktivieren Sie vorübergehend eine Konsolensprache bei einer vorhandenen Configuration Manager-Konsoleninstallation  

1.  Schließen Sie auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, die Configuration Manager-Konsole.  

2.  Wechseln Sie in Windows Explorer auf dem Computer mit der Configuration Manager-Konsole zu &lt;*ConsoleInstallationPath*>\Bin\.  

3.  Benennen Sie den entsprechenden Sprachordner für die Sprache um, die auf dem Computer konfiguriert ist. Wenn beispielsweise beim Computer die Spracheinstellung "Deutsch" konfiguriert ist, könnten Sie den Ordner **de** in **de.deaktiviert**umbenennen.  

4.  Wenn Sie die Configuration Manager-Konsole wieder in der Sprache öffnen möchten, die für den Computer konfiguriert ist, benennen Sie den Ordner in den ursprünglichen Namen um. Benennen Sie beispielsweise **de.deaktiviert** wieder in **de**um.  

##  <a name="BKMK_ConfigDCOMforRemoteConsole"></a> Konfigurieren von DCOM-Berechtigungen für Configuration Manager-Remotekonsolen  
 Für das Benutzerkonto, unter dem die Configuration Manager-Konsole ausgeführt wird, sind Berechtigungen für den Zugriff auf die Standortdatenbank über den SMS-Anbieter erforderlich. Administratoren, die eine Configuration Manager-Remotekonsole verwenden, benötigen zudem DCOM-Berechtigungen für eine **Remoteaktivierung** auf folgenden Computern:  

-   Den Standortservercomputer  

-   Jedem Computer, der eine Instanz des SMS-Anbieters hostet  

 Über die Sicherheitsgruppe mit Namen **SMS-Administratoren** ist der Zugriff auf den SMS-Anbieter auf einem Computer möglich, und auch die erforderlichen DCOM-Berechtigungen können mithilfe dieser Gruppe gewährt werden. (Wenn der SMS-Anbieter auf einem Mitgliedsserver ausgeführt wird, ist diese Gruppe eine lokale Computergruppe. Wenn der SMS-Anbieter auf einem Domänencontroller ausgeführt wird, ist diese Gruppe eine lokale Domänengruppe.)  

> [!IMPORTANT]  
>  Die Configuration Manager-Konsole stellt mithilfe von Windows Management Instrumentation (WMI) eine Verbindung mit dem SMS-Anbieter her. WMI verwendet intern DCOM. Aus diesem Grund benötigt Configuration Manager Berechtigungen zum Aktivieren eines DCOM-Servers auf dem SMS-Anbietercomputer, wenn die Configuration Manager-Konsole auf einem anderen Computer als dem SMS-Anbietercomputer ausgeführt wird. Die Berechtigung zur Remoteaktivierung wird standardmäßig nur den Mitgliedern der integrierten Gruppe Administratoren erteilt. Wenn Sie der Gruppe SMS-Administratoren die Berechtigung Remoteaktivierung erteilen, kann jedes Mitglied dieser Gruppe DCOM-Angriffe gegen den SMS-Anbietercomputer unternehmen. Zudem wird die Angriffsfläche des Computers durch diese Konfiguration erhöht. Überwachen Sie sorgfältig die Mitgliedschaften der Gruppe SMS-Administratoren, um dieses Risiko zu verringern.  

 Gehen Sie wie folgt vor, um die Standorte der zentralen Verwaltung, die primären Standortserver sowie alle Computer, auf denen der SMS-Anbieter installiert wird, für den Remotezugriff durch Administratoren mithilfe der Configuration Manager-Konsole zu konfigurieren.  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>So konfigurieren Sie DCOM-Berechtigungen für Remoteverbindungen der Configuration Manager-Konsole  

1.  Öffnen Sie  **Komponentendienste** , indem Sie **Dcomcnfg.exe**ausführen.  

2.  Klicken Sie unter **Komponentendienste**auf **Konsolenstamm** >  **Komponentendienste** > **Computer**aus, und klicken Sie dann auf **Arbeitsplatz**. Klicken Sie im Menü **Aktion** auf **Eigenschaften**.  

3.  Klicken Sie im Dialogfeld **Eigenschaften von Arbeitsplatz** auf der Registerkarte **COM-Sicherheit** im Abschnitt **Start- und Aktivierungsberechtigungen** auf **Limits bearbeiten**.  

4.  Klicken Sie im Dialogfeld **Start- und Aktivierungsberechtigungen** auf **Hinzufügen**.  

5.  Geben Sie im Dialogfeld **Benutzer, Computer, Dienstkonten oder Gruppen auswählen** im Feld **Geben Sie die Namen der auszuwählenden Objekte ein. (Beispiele)** die Zeichenfolge **SMS Admins**ein, und klicken Sie dann auf **OK**.  

    > [!NOTE]  
    >  Möglicherweise müssen Sie die Einstellung für **Von diesem Speicherort** ändern, um die Gruppe „SMS-Administratoren“ zu finden. Wenn der SMS-Anbieter auf einem Mitgliedsserver ausgeführt wird, ist diese Gruppe eine lokale Computergruppe. Wenn der SMS-Anbieter auf einem Domänencontroller ausgeführt wird, ist diese Gruppe eine lokale Domänengruppe.  

6.  Aktivieren Sie im Abschnitt **Berechtigungen für SMS-Administratoren** das Kontrollkästchen **Remoteaktivierung** .  

7.  Klicken Sie auf **OK** , klicken Sie noch einmal auf **OK** , und schließen Sie dann die **Computerverwaltung**. Ihr Computer ist jetzt für den Remotezugriff über die Configuration Manager-Konsole durch Mitglieder der Gruppe „SMS-Administratoren“ konfiguriert.  

 Wiederholen Sie dieses Verfahren auf jedem SMS-Anbietercomputer, durch den Configuration Manager-Remotekonsolen möglicherweise unterstützt werden.  

##  <a name="bkmk_dbconfig"></a> Ändern der Konfiguration für die Standortdatenbank  
 Nach der Installation eines Standorts können Sie die Konfiguration der Standortdatenbank und des Standortdatenbankserver ändern, indem Sie Setup auf dem Standortserver der zentralen Verwaltung oder einem primären Standortserver ausführen. Sie können die Standortdatenbank auf eine neue SQL Server-Instanz auf dem gleichen Computer oder auf einen anderen Computer verschieben, auf dem eine unterstützte Version von SQL Server ausgeführt wird. Diese und verwandte Änderungen werden für die Datenbankkonfiguration an sekundären Standorten nicht unterstützt.  

 Weitere Informationen zu den Grenzen der Unterstützung finden Sie unter [Supportrichtlinie für manuelle Datenbankänderungen in einer Configuration Manager-Umgebung](https://support.microsoft.com/kb/3106512).  

> [!NOTE]  
>  Wenn Sie die Datenbankkonfiguration eines Standorts ändern, werden die Configuration Manager-Dienste auf dem Standortserver und den Systemservern von Remotestandorten, von denen aus Kommunikation mit der Datenbank erfolgt, von Configuration Manager neu gestartet oder neu installiert.  

**Zum Ändern der Datenbankkonfiguration**müssen Sie Setup auf dem Standortserver ausführen und die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**auswählen. Wählen Sie dann die Option **SQL Server-Konfiguration ändern** aus. Sie können die folgenden Konfigurationen der Standortdatenbank ändern:  

-   Den Windows-basierten Server, auf dem die Datenbank gehostet wird  

-   Die SQL Server-Instanz, die auf einem Server verwendet wird, auf dem die SQL Server-Datenbank gehostet wird  

-   Der Datenbankname.  

-   SQL Server-Port wird von Configuration Manager verwendet  

-   SQL Server Service Broker-Port wird von Configuration Manager verwendet  

**Wenn Sie die Standortdatenbank verschieben, müssen Sie Folgendes konfigurieren:**  

-   **Konfigurieren des Zugriffs** : Wenn Sie die Standortdatenbank auf einen neuen Computer verschieben, fügen Sie das Computerkonto des Standortservers der Gruppe **Lokale Administratoren** auf dem Computer, auf dem SQL Server ausgeführt wird, hinzu. Wenn Sie für die Standortdatenbank einen SQL Server-Cluster verwenden, müssen Sie das Computerkonto der Gruppe **Lokale Administratoren** jedes Windows Server-Clusterknotencomputers hinzufügen.  

-   **Aktivieren der CLR-Integration (Common Language Runtime):**  Wenn Sie die Standortdatenbank auf eine neue SQL Server-Instanz oder einen neuen SQL Server-Computer verschieben, müssen Sie die CLR-Integration (Common Language Runtime) aktivieren. Stellen Sie zum Aktivieren der CLR-Integration mithilfe von **SQL Server Management Studio** eine Verbindung mit der SQL Server-Instanz her, auf der die Standortdatenbank gehostet wird, und führen Sie dann die folgende gespeicherte Prozedur als Abfrage aus: **sp_configure 'clr enabled',1; reconfigure**.  
-  **Stellen Sie sicher, dass der neue SQL-Server Zugriff auf den Speicherort der Sicherung hat:** Wenn Sie eine UNC verwenden, um die Sicherung der Standortdatenbank nach dem Verschieben der Datenbank einschließlich dem Verschieben einer SQL Server Always On-Verfügbarkeitsgruppe zu einem neuen SQL Server oder zu einem SQL Server-Cluster zu speichern, müssen Sie sicherstellen, dass das Computerkonto des neuen SQL Servers über **Schreibberechtigungen** für den UNC-Standort verfügt.  


> [!IMPORTANT]  
>  Vor dem Verschieben einer Datenbank, die über mindestens ein Datenbankreplikat für Verwaltungspunkte verfügt, müssen Sie zuerst die Datenbankreplikate entfernen. Nachdem das Verschieben der Datenbank abgeschlossen ist, können Sie die Datenbankreplikate neu konfigurieren. Weitere Informationen finden Sie unter [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

##  <a name="bkmk_SPN"></a> Verwalten des SPN für den Standortdatenbankserver  
Sie können das Konto auswählen, mit dem SQL-Dienste für die Standortdatenbank ausgeführt werden:  

-   Wenn die Dienste mit dem Systemkonto des Computers ausgeführt werden, wird der SPN automatisch für Sie registriert.  

-   Wenn die Dienste mit einem lokalen Domänenbenutzerkonto ausgeführt werden, müssen Sie den SPN manuell registrieren, um sicherzustellen, dass SQL-Clients und andere Standortsysteme eine Kerberos-Authentifizierung ausführen können. Ohne Kerberos-Authentifizierung kann die Kommunikation mit der Datenbank fehlschlagen.  

Die SQL Server-Dokumentation bietet Ihnen Hilfe beim [manuellen Registrieren des SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx)und stellt zusätzliche Hintergrundinformationen zu SPNs und Kerberos-Verbindungen bereit.  

> [!IMPORTANT]  
>  -   Wenn Sie einen SPN für einen gruppierten SQL Server erstellen, müssen Sie den virtuellen Namen des SQL Server-Clusters als SQL Server-Computernamen angeben.  
> -   Der Befehl zum Registrieren eines SPN für eine benannte SQL Server-Instanz ist der gleiche wie zum Registrieren eines SPN für eine Standardinstanz. Allerdings muss die Portnummer mit der von der benannten Instanz verwendeten Portnummer übereinstimmen.  

Sie können einen SPN für das SQL Server-Dienstkonto des Standortdatenbankservers mithilfe des Tools **Setspn** registrieren. Sie müssen das Dienstprogramm Setspn auf einem Computer ausführen, der sich in der Domäne von SQL Server befindet. Zur Ausführung des Dienstprogramms sind die Anmeldeinformationen eines Domänenadministrators erforderlich.  

 Verwenden Sie die folgenden Verfahren als Beispiele für das Verwalten des SPN für das SQL Server-Dienstkonto mithilfe des Tools Setspn unter Windows Server 2008 R2. Umfassende Hinweise zu Setspn finden Sie in der [Übersicht über Setspn](http://go.microsoft.com/fwlink/p/?LinkId=226343)oder in der entsprechenden Dokumentation zu Ihrem Betriebssystem.  

> [!NOTE]  
>  Die folgenden Verfahren beziehen sich auf das Befehlszeilenprogramm Setspn. Das Befehlszeilenprogramm Setspn ist Bestandteil der Windows Server 2003-Supporttools, die Sie von der Produkt-CD installieren oder im [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=100114)herunterladen können. Weitere Informationen zum Installieren der Windows-Supporttools von der Produkt-CD finden Sie unter [Installieren der Windows-Supporttools](http://go.microsoft.com/fwlink/p/?LinkId=62270).  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>So erstellen Sie manuell einen Domänenbenutzer-SPN (Service Principal Name) für das SQL Server-Dienstkonto  

1.  Klicken Sie auf **Start** , klicken Sie auf **Ausführen**, und geben Sie dann im Dialogfeld „Ausführen“ den Befehl **cmd** ein.  

2.  Wechseln Sie an der Befehlszeile in das Installationsverzeichnis für die Windows Server-Supporttools. Standardmäßig befinden sich diese Tools im Verzeichnis **C:\Program Files\Support Tools** .  

3.  Geben Sie einen gültigen Befehl ein, um den SPN zu erstellen. Zum Erstellen des SPN können Sie den NetBIOS-Namen oder den FQDN (vollqualifizierter Domänenname) des Computers verwenden, auf dem SQL Server ausgeführt wird. Allerdings müssen Sie einen SPN sowohl für den NetBIOS-Namen als auch für den FQDN erstellen.  

    > [!IMPORTANT]  
    >  Wenn Sie einen SPN für einen gruppierten SQL Server erstellen, müssen Sie den virtuellen Namen des SQL Server-Clusters als SQL Server-Computernamen angeben.  

    -   Zum Erstellen eines SPN für den NetBIOS-Namen des SQL Server-Computers geben Sie den folgenden Befehl ein: **setspn -A MSSQLSvc/&lt;SQL Server-Computername\>:1433 &lt;Domäne\Konto>**  

    -   Zum Erstellen eines SPN für den FQDN des SQL Server-Computers geben Sie den folgenden Befehl ein: **setspn -A MSSQLSvc/&lt;SQL Server- FQDN\>:1433 &lt;Domäne\Konto>**  

    > [!NOTE]  
    >  Der Befehl zum Registrieren eines SPN für eine benannte SQL Server-Instanz ist der gleiche wie zum Registrieren eines SPN für eine Standardinstanz. Allerdings muss die Portnummer mit der von der benannten Instanz verwendeten Portnummer übereinstimmen.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>So überprüfen Sie mithilfe des Befehls „Setspn“, ob der Domänenbenutzer-SPN richtig registriert wurde  

1.  Klicken Sie auf **Start** , klicken Sie auf **Ausführen**, und geben Sie dann im Dialogfeld **Ausführen** den Befehl **cmd** ein.  

2.  Geben Sie an der Eingabeaufforderung den folgenden Befehl ein: **setspn –L &lt;Domäne\SQL-Dienstkonto>**.  

3.  Überprüfen Sie den registrierten **ServicePrincipalName** , um sicherzustellen, dass ein gültiger SPN für den SQL Server erstellt wurde.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>So überprüfen Sie mithilfe der ADSIEdit-MMC-Konsole, ob der Domänenbenutzer-SPN richtig registriert wurde  

1.  Klicken Sie auf **Start** , klicken Sie auf **Ausführen**, und geben Sie dann **adsiedit.msc** ein, um die ADSIEdit-MMC-Konsole zu starten.  

2.  Stellen Sie ggf. eine Verbindung mit der Domäne des Standortservers her.  

3.  Erweitern Sie im Konsolenbereich die Domäne des Standortservers, erweitern Sie **DC=&lt;definierter Name des Servers\>** und anschließend **CN=Benutzer**, klicken Sie mit der rechten Maustaste auf **CN=&lt;Dienstkontobenutzer\>**, und klicken Sie dann auf **Eigenschaften**.  

4.  Überprüfen Sie im Dialogfeld **CN=&lt;Eigenschaften von \>Dienstkontobenutzer** den Wert **servicePrincipalName**, um sicherzustellen, dass ein gültiger SPN erstellt und dem richtigen SQL Server-Computer zugeordnet wurde.  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>So ändern Sie das SQL Server-Dienstkonto von einem lokalen Systembenutzerkonto in ein Domänenbenutzerkonto  

1.  Erstellen Sie ein Domänenbenutzerkonto oder ein lokales Systembenutzerkonto, das dann als SQL Server-Dienstkonto verwendet wird, oder wählen Sie es aus.  

2.  Öffnen Sie **SQL Server Configuration Manager**.  

3.  Klicken Sie auf **SQL Server-Dienste**, und doppelklicken Sie dann auf **SQL Server&lt; INSTANZNAME\>**.  

4.  Wählen Sie auf der Registerkarte **Anmelden** die Option **Dieses Konto**aus, und geben Sie dann den Benutzernamen und das Kennwort für das in Schritt 1 erstellte Domänenbenutzerkonto ein, oder klicken Sie auf **Durchsuchen** , um das Benutzerkonto in den Active Directory-Domänendiensten zu suchen, und klicken Sie dann auf **Übernehmen**.  

5.  Klicken Sie im Dialogfeld **Kontenänderung bestätigen** auf **Ja** , um die Änderung des Dienstkontos zu bestätigen und den SQL Server-Dienst neu zu starten.  

6.  Klicken Sie auf **OK** , nachdem das Dienstkonto erfolgreich geändert wurde.  

##  <a name="bkmk_reset"></a> Ausführen einer Standortrücksetzung  
 Wenn eine Standortrücksetzung an einem Standort der zentralen Verwaltung oder primären Standort ausgeführt wird, geschieht Folgendes:  

-   Die Configuration Manager-Standarddatei und die standardmäßigen Registrierungsberechtigungen werden erneut angewendet  

-   Alle Standortkomponenten und alle Standortsystemrollen werden am Standort neu installiert.  

Für sekundäre Standorte wird das Zurücksetzen des Standorts nicht unterstützt.  

Standortrücksetzungen können auf Wunsch manuell ausgeführt werden oder automatisch erfolgen, nachdem Sie die Standortkonfiguration geändert haben.  

Wenn beispielsweise die von Configuration Manager-Komponenten verwendeten Konten geändert wurden, sollten Sie eine manuelle Standortrücksetzung in Erwägung ziehen, um sicherzustellen, dass die Standortkomponenten für die Verwendung der neuen Kontodetails aktualisiert werden. Wenn Sie dagegen die Sprachen für Client oder Server an einem Standort ändern, setzt Configuration Manager den Standort automatisch zurück, da dies erforderlich ist, bevor die Änderungen auf dem Standort wirksam werden.  

> [!NOTE]  
>  Beim Zurücksetzen des Standorts werden ausschließlich die Zugriffsberechtigungen für Configuration Manager-Objekte zurückgesetzt.  

Beim Zurücksetzen eines Standorts geschieht Folgendes:  

1.  Der Dienst **SMS_SITE_COMPONENT_MANAGER** und die Threadkomponenten des Diensts **SMS_EXECUTIVE** werden beendet und neu gestartet.  

2.  Der Freigabeordner des Standortsystems und die Komponente **SMS-Executive** auf dem lokalen Computer und auf Remote-Standortsystemcomputern werden entfernt und anschließend neu erstellt.  

3.  Der Dienst **SMS_SITE_COMPONENT_MANAGER** wird neu gestartet, und von diesem Dienst werden die Dienste **SMS_EXECUTIVE** und **SMS_SQL_MONITOR** installiert.  

Des Weiteren werden bei einer Standortrücksetzung folgende Objekte wiederhergestellt:  

-   Die Registrierungsschlüssel **SMS** oder **NAL** sowie alle diesen Schlüsseln untergeordneten Schlüssel  

-   Die Configuration Manager-Dateiverzeichnisstruktur sowie alle Standarddateien und -verzeichnisse in dieser Verzeichnisstruktur.  

**Voraussetzungen für das Ausführen einer Standortrücksetzung**  

Das Konto, mit dem Sie das Zurücksetzen eines Standorts ausführen, muss über folgende Berechtigungen verfügen:  

-   Das Konto, mit dem Sie das Zurücksetzen eines Standorts ausführen, muss über folgende Berechtigungen verfügen:  

    -   **Standort der zentralen Verwaltung**: Das Konto, das Sie zum Zurücksetzen dieses Standorts verwenden, muss auf dem Standort der zentralen Verwaltung über lokale Administratorrechte verfügen sowie über Berechtigungen, die der rollenbasierten Verwaltungssicherheitsrolle **Hauptadministrator** entsprechen.  

    -   **Primärer Standort**: Das Konto, das Sie zum Zurücksetzen dieses Standorts verwenden, muss auf dem primären Standort über lokale Administratorrechte verfügen sowie über Berechtigungen, die der rollenbasierten Verwaltungssicherheitsrolle **Hauptadministrator** entsprechen. Wenn der primäre Standort sich in der gleichen Hierarchie befindet wie ein Standort der zentralen Verwaltung, muss dieses Konto darüber hinaus über lokale Administratorrechte auf dem Standortserver der zentralen Verwaltung verfügen.  

**Einschränkungen für eine Standortrücksetzung**
  - Ab Version 1602 können Sie einen Standort zurücksetzen, um den Server oder Clientsprachpakete zu ändern, die an Standorten installiert sind. Als Voraussetzung muss die Hierarchie so konfiguriert sein, dass sie das [Testen von Clientupgrades in einer Präproduktionssammlung](/sccm/core/clients/manage/upgrade/test-client-upgrades) unterstützt.

#### <a name="to-perform-a-site-reset"></a>So führen Sie eine Standortrücksetzung durch  

1.  Führen Sie das **Configuration Manager-Setup** über **&lt;Installationsordner des Configuration Manager-Standorts\>\BIN\X64\setup.exe** aus.  

    > [!TIP]  
    >  Sie können eine Standortrücksetzung auch ausführen, indem Sie das Configuration Manager-Setup im **Startmenü** auf dem Standortservercomputer oder aus dem Configuration Manager-Quellmedium starten.  

2.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**aus, und klicken Sie dann auf **Weiter**.  

3.  Wählen Sie auf der Seite **Standortwartung** die Option **Standort ohne Konfigurationsänderung zurücksetzen**aus, und klicken Sie dann auf **Weiter**.  

4.  Klicken Sie auf **Ja** , um das Zurücksetzen des Standorts zu beginnen.  

Wenn das Zurücksetzen des Standorts beendet ist, klicken Sie auf **Schließen** , um dieses Verfahren abzuschließen.  

##  <a name="bkmk_sitelang"></a> Verwalten von Sprachpaketen an einem Standort  
Nach der Installation eines Standorts können Sie die verwendeten Sprachpakete für Server und Client ändern:  

**Serversprachpakete:**  

-   **Gilt für:**  

     Configuration Manager-Konsoleninstallationen  

     Neue Installationen von relevanten Standortsystemrollen  

-   **Details:**  

     Nach dem Aktualisieren der Serversprachpakete an einem Standort können Sie Configuration Manager-Konsolen die Unterstützung für die Sprachpakete hinzufügen.  

     Zum Hinzufügen der Unterstützung für ein Serversprachpaket zu einer Configuration Manager-Konsole müssen Sie die Configuration Manager-Konsole aus dem Ordner **ConsoleSetup** eines Standortservers installieren, der das gewünschte Sprachpaket enthält. Falls die Configuration Manager-Konsole bereits installiert ist, müssen Sie sie zuerst deinstallieren, damit für die neue Installation die aktuelle Liste der unterstützten Sprachpakete identifiziert werden kann.  

**Clientsprachpakete:**  

-   **Gilt für:**  

     Durch Änderungen der Clientsprachpakete werden die Quelldateien für die Clientinstallation aktualisiert, damit bei neuen Clientinstallationen und Upgrades die Unterstützung für die aktualisierte Liste der Clientsprachen hinzugefügt wird.  

-   **Details:**  

     Nachdem Sie die Clientsprachpakete an einem Standort aktualisiert haben, müssen Sie jeden Client, von dem die Sprachpakete verwendet werden, mithilfe der Quelldateien mit den Clientsprachpaketen installieren.  

Informationen zu den von Configuration Manager unterstützten Client- und Serversprachen finden Sie unter [Sprachpakete in System Center Configuration Manager](../../../core/servers/deploy/install/language-packs.md)  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>So ändern Sie die Sprachpakete, die an einem Standort unterstützt werden  

1.  Führen Sie auf dem Standortserver das Configuration Manager-Setup unter **&lt;Configuration Manager-Installationsordner des Standorts\>\BIN\X64\setup.exe** aus.  

2.  Wählen Sie auf der Seite **Erste Schritte** die Option **Standortwartung durchführen oder diesen Standort zurücksetzen**aus, und klicken Sie dann auf **Weiter**.  

3.  Wählen Sie auf der Seite **Standortwartung** die Option **Sprachkonfiguration ändern**aus, und klicken Sie dann auf **Weiter**.  

4.  Aktivieren Sie auf der Seite **Download der Voraussetzungskomponenten** die Option **Erforderliche Dateien herunterladen** , damit Updates für Sprachpakete abgerufen werden. Sie können auch die Option **Bereits heruntergeladene Dateien verwenden** aktivieren, um die bereits heruntergeladenen Dateien zu verwenden, in denen die gewünschten Sprachpakete für den Standort enthalten sind. Klicken Sie auf **Weiter** , um die Dateien zu überprüfen und den Vorgang fortzusetzen.  

5.  Aktivieren Sie auf der Seite **Serversprachauswahl** das Kontrollkästchen für die Serversprachen, die vom Standort unterstützt werden, und klicken Sie dann auf **Weiter**.  

6.  Aktivieren Sie auf der Seite **Clientsprachauswahl** das Kontrollkästchen für die Clientsprachen, die vom Standort unterstützt werden, und klicken Sie dann auf **Weiter**.  

7.  Klicken Sie auf **Weiter**, um die Sprachunterstützung für den Standort zu ändern.  

    > [!NOTE]  
    >  Configuration Manager initiiert das Zurücksetzen des Standorts, wobei auch alle Standortsystemrollen des Standorts neu installiert werden.  

8.  Klicken Sie auf **Schließen** , um dieses Verfahren abzuschließen.  

##  <a name="BKMK_ModDBAlert"></a> Ändern des Warnungsschwellenwerts für Datenbankserver  
 Configuration Manager gibt standardmäßig Warnungen aus, wenn auf einem Standortdatenbankserver wenig Speicherplatz verfügbar ist. Normalerweise wird eine Warnung ausgegeben, wenn der freie Festplattenspeicher 10 GB oder weniger beträgt. Bei 5 GB oder weniger wird eine kritische Warnung ausgegeben. Sie können diese Werte ändern oder die Warnungen für die einzelnen Standorte deaktivieren.  

 So ändern Sie diese Einstellungen  

1.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.  

2.  Wählen Sie den Standort aus, den Sie konfigurieren möchten, und öffnen Sie die **Eigenschaften** dieses Standorts.  

3.  Klicken Sie im Dialogfeld **Standorteigenschaften** auf die Registerkarte **Warnung**, und bearbeiten Sie dann die Einstellungen.  

4.  Klicken Sie zum Schließen des Dialogfelds „Standorteigenschaften“ auf **OK** .  
