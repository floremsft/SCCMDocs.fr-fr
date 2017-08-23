---
title: SQL Server AlwaysOn | Microsoft-Dokumentation
description: "Planen Sie die Verwendung einer SQL Server-AlwaysOn-Verfügbarkeitsgruppe mit SCCM."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: "16"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: c746365238e1255d73387a9496521bb03a56b21b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Vorbereiten der Verwendung von SQL Server AlwaysOn-Verfügbarkeitsgruppen mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bereiten Sie System Center Configuration Manager auf die Verwendung von SQL Server AlwaysOn-Verfügbarkeitsgruppen als Lösung für hohe Verfügbarkeit und Notfallwiederherstellung für die Standortdatenbank vor.  
Configuration Manager unterstützt die Verwendung von Verfügbarkeitsgruppen:
-     An primären Standorten und am Standort der zentralen Verwaltung.
-     Lokal oder in Microsoft Azure.

Wenn Sie Verfügbarkeitsgruppen in Microsoft Azure verwenden, können Sie die Verfügbarkeit Ihrer Standortdatenbank weiter steigern, indem Sie *Azure-Verfügbarkeitsgruppen* einsetzen. Weitere Informationen zu Azure-Verfügbarkeitsgruppen finden Sie unter [Verwalten der Verfügbarkeit von virtuellen Computern](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

>  [!Important]   
>  Machen Sie sich mit der Konfiguration von SQL Server und SQL Server-Verfügbarkeitsgruppen vertraut, bevor Sie fortfahren. In den folgenden Informationen wird auf die SQL Server-Dokumentationsbibliothek und entsprechende Verfahren verwiesen.

## <a name="supported-scenarios"></a>Unterstützte Szenarien
Die folgenden Szenarios werden für die Verwendung von Verfügbarkeitsgruppen mit Configuration Manager unterstützt. Ausführliche Informationen und Vorgehensweisen für die einzelnen Szenarien finden Sie unter [Konfigurieren von Verfügbarkeitsgruppen für Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).


-      [Erstellen einer Verfügbarkeitsgruppe für die Verwendung mit Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group).
-     [Konfigurieren eines Standorts zur Verwendung einer Verfügbarkeitsgruppe](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group).
-     [Add or remove synchronous replica members from an availability group that hosts a site database (Hinzufügen oder Entfernen von synchronen Replikationsmitgliedern zu einer Verfügbarkeitsgruppe, die eine Standortdatenbank hostet)](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members)
-     [Configure asynchronous commit replicas (Konfigurieren von Replikaten mit asynchronem Commit)](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca) (Erfordert Configuration Manager Version 1706 oder höher.)
-     [Recover a site from an asynchronous commit replica (Wiederherstellen eines Standorts aus einem Replikat mit asynchronem Commit)](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site) (Erfordert Configuration Manager Version 1706 oder höher.)
-     [Verschieben einer Standortdatenbank aus einer Verfügbarkeitsgruppe in eine Standardinstanz oder eine benannte Instanz einer eigenständigen SQL Server-Instanz](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group).


## <a name="prerequisites"></a>Voraussetzungen
Die folgenden Voraussetzungen gelten für alle Szenarien. Wenn zusätzliche Voraussetzungen für ein bestimmtes Szenario gelten, werden sie für das Szenario angegeben.   

### <a name="configuration-manager-accounts-and-permissions"></a>Konten und Berechtigungen in Configuration Manager
**Zugriff auf Standortserver und Replikationsmitglieder:**   
Das Computerkonto des Standortservers muss Mitglied der Gruppe **Lokale Administratoren** auf allen Computern sein, die zur Verfügbarkeitsgruppe gehören.

### <a name="sql-server"></a>SQL Server
**Version:**  
Jedes Replikat in der Verfügbarkeitsgruppe muss eine Version von SQL Server ausführen, die von Ihrer Configuration Manager-Version unterstützt wird. Wenn von SQL Server unterstützt, können die verschiedenen Knoten einer Verfügbarkeitsgruppe unterschiedliche Versionen von SQL Server ausführen.

**Edition:**  
Sie müssen eine *Enterprise* Edition von SQL Server verwenden.

**Konto:**  
Jede Instanz von SQL Server kann mit einem Domänenbenutzerkonto (**Dienstkonto**) oder mit einem Nicht-Domänenkonto ausgeführt werden. Jedes Replikat in einer Gruppe kann eine andere Konfiguration aufweisen. Die [bewährten Methoden für SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd) raten dazu, ein Konto mit möglichst geringen Berechtigungen zu verwenden.

-   Informationen zum Konfigurieren von Dienstkonten und Berechtigungen für SQL Server 2016 finden Sie unter [Configure Windows Service Accounts and Permissions (Konfigurieren von Windows-Dienstkonten und -Berechtigungen)](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) auf MSDN.
-   Sie müssen Zertifikate verwenden, um ein Nicht-Domänenkonto zu verwenden. Weitere Informationen finden Sie unter [Use Certificates for a Database Mirroring Endpoint (Transact-SQL) (Verwenden von Zertifikaten für einen Datenbankspiegelungs-Endpunkt (Transact-SQL))](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).


Weitere Informationen finden Sie unter [Erstellen eines Endpunkts für die Datenbankspiegelung für AlwaysOn-Verfügbarkeitsgruppen](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### <a name="availability-group-configurations"></a>Konfigurationen von Verfügbarkeitsgruppen
**Replikationsmitglieder:**  
-   Die Verfügbarkeitsgruppe muss ein primäres Replikat besitzen.
-   Vor Version 1706 können Sie bis zu zwei synchrone sekundäre Replikate verwenden.
-   Ab Version 1706 können Sie die gleiche Anzahl und Art von Replikaten in einer Verfügbarkeitsgruppe nutzen, die von der von Ihnen verwendeten Version von SQL Server unterstützt wird.

    Sie können ein Replikat mit asynchronem Commit zum Wiederherstellen Ihres synchronen Replikats verwenden. Unter [Wiederherstellungsoptionen für die Standortdatenbank]( /sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) finden Sie im Thema zu Sicherung und Wiederherstellung weiterführende Informationen dazu.
    > [!CAUTION]  
    > Configuration Manager unterstützt kein Failover, um das Replikat mit asynchronem Commit als Standortdatenbank zu verwenden.
Da Configuration Manager nicht den Status des Replikats mit asynchronem Commit dahingehend überprüft, ob es aktuell ist, und [ein solches Replikat asynchron sein kann]( https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), kann das Verwenden eines Replikats mit asynchronem Commit als Standortdatenbank die Integrität Ihres Standorts und Ihrer Daten gefährden.

Jedes Replikationsmitglied muss:
-   die **Standardinstanz**verwenden.  
    *Ab Version 1702 können Sie eine* ***benannte Instanz*** verwenden.

-     **Ja** für **Verbindungen in primärer Rolle** aufweisen.
-     **Ja** für **Lesbare sekundäre Rolle** aufweisen.  
-     auf **Manuelles Failover**festgelegt sein.      

    >  [!TIP]
    >  Configuration Manager unterstützt bei Festlegung auf **Automatisches Failover** die Verwendung der synchronen Verfügbarkeitsgruppenreplikate. Ein **manuelles Failover** muss jedoch in folgenden Fällen festgelegt werden:
    >  -  Sie führen das Setup aus, um die Verwendung der Standortdatenbank in der Verfügbarkeitsgruppe anzugeben.
    >  -  Wenn Sie ein Update für Configuration Manager installieren (nicht nur Updates für die Standortdatenbank).  

**Speicherort der Replikationsmitglieder:**  
Alle Replikate in einer Verfügbarkeitsgruppe müssen lokal oder in Microsoft Azure gehostet werden. Eine Gruppe, die ein lokales Mitglied und ein Mitglied in Azure enthält, wird nicht unterstützt.     

Wenn Sie eine Verfügbarkeitsgruppe in Azure einrichten und die Gruppe sich hinter einem internen oder externen Lastenausgleich befindet, müssen Sie die folgenden Standardports öffnen, damit das Setup auf jedes Replikat zugreifen kann:   

-     RCP-Endpunktzuordnung: **TCP 135**   
-     Server Message Block: **TCP 445**  
    *Wenn das Verschieben der Datenbank abgeschlossen ist, können Sie diesen Port entfernen. Ab Version 1702 ist dieser Port nicht mehr erforderlich.*
-     SQL Server Service Broker: **TCP 4022**
-     SQL über TCP: **TCP 1433**   

Nach Abschluss des Setups müssen die folgenden Ports zugänglich bleiben:
-     SQL Server Service Broker: **TCP 4022**
-     SQL über TCP: **TCP 1433**

Ab Version 1702 können Sie benutzerdefinierte Ports für diese Konfigurationen verwenden. Die gleichen Ports müssen vom Endpunkt und auf allen Replikaten in der Verfügbarkeitsgruppe verwendet werden.


**Listener:**   
Die Verfügbarkeitsgruppe muss mindestens einen **Verfügbarkeitsgruppenlistener**besitzen. Der virtuelle Name dieses Listeners wird verwendet, wenn Sie Configuration Manager für die Verwendung der Standortdatenbank in der Verfügbarkeitsgruppe konfigurieren. Eine Verfügbarkeitsgruppe kann zwar mehrere Listener enthalten, Configuration Manager kann aber nur einen nutzen. Weitere Informationen finden Sie unter [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

**Dateipfade:**   
Wenn Sie das Setup von Configuration Manager so ausführen, dass ein Standort für die Verwendung der Datenbank in einer Verfügbarkeitsgruppe konfiguriert wird, muss jeder sekundäre Replikatserver einen SQL Server-Dateipfad aufweisen, der identisch mit dem Dateipfad der Standortdatenbank-Dateien für das aktuelle primäre Replikat ist.
-   Wenn kein identischer Pfad vorhanden ist, kann das Setup die Instanz für die Verfügbarkeitsgruppe nicht als neuen Speicherort der Standortdatenbank hinzufügen.
-   Darüber hinaus muss das lokale SQL Server-Dienstkonto über die Berechtigung **Vollzugriff** für diesen Ordner verfügen.

Die sekundären Replikatserver benötigen diesen Dateipfad nur, während Sie Setup verwenden, um die Datenbankinstanz der Verfügbarkeitsgruppe anzugeben. Nachdem vom Setup die Konfiguration der Standortdatenbank in der Verfügbarkeitsgruppe durchgeführt wurde, können Sie den nicht verwendeten Pfad von sekundären Replikatservern löschen.

Betrachten Sie beispielsweise das folgende Szenario:
-   Sie erstellen eine Verfügbarkeitsgruppe, die drei SQL Server-Instanzen verwendet.

-   Ihr primärer Replikatserver ist eine Neuinstallation von SQL Server 2014. Standardmäßig werden die Datenbankdateien der Typen MDF und LDF in „C:\Programme\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA“ gespeichert.

-   Ihre beiden sekundären Replikatserver wurden von früheren Versionen auf SQL Server 2014 aktualisiert, und Sie behalten den ursprünglichen Dateipfad zum Speichern von Datenbankdateien bei, nämlich: C:\Programme\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA.

-   Bevor Sie versuchen, die Standortdatenbank in diese Verfügbarkeitsgruppe zu verschieben, müssen Sie auf allen sekundären Replikatservern den folgenden Dateipfad erstellen, auch wenn die sekundären Replikate diesen Dateispeicherort nicht nutzen: C:\Programme\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (ein Duplikat des Pfads, der für das primäre Replikat verwendet wird).

-   Anschließend gewähren Sie dem SQL Server-Dienstkonto für jedes sekundäre Replikat Vollzugriff auf den neu erstellten Speicherort auf dem Server.

-   Sie können nun das Setup von Configuration Manager erfolgreich so ausführen, dass die Standortdatenbank in der Verfügbarkeitsgruppe verwendet wird.

**Konfigurieren der Datenbank für ein neues Replikat:**   
 Die Datenbank der einzelnen Replikate muss mit folgenden Einstellungen festgelegt werden:
-   **CLR-Integration** muss *aktiviert* werden.
-     **Max text repl size** muss *2147483647* sein.
-     Der Datenbankbesitzer muss das *SA-Konto* sein.
-     **TRUSTWORTY** muss **ON** sein.
-     **Service Broker** muss *aktiviert* werden.

Sie können diese Konfigurationen nur für ein primäres Replikat festlegen. Um ein sekundäres Replikat zu konfigurieren, müssen Sie zuerst ein Failover des primären Replikats auf das sekundäre Replikat vornehmen, wodurch das sekundäre Replikat das neue primäre Replikat wird.   

Verwenden Sie bei Bedarf die SQL Server-Dokumentation, um die Einstellungen zu konfigurieren. Lesen Sie beispielsweise die Abschnitte [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) oder [CLR-Integration](/sql/relational-databases/clr-integration/clr-integration-enabling) in der SQL Server-Dokumentation.

### <a name="verification-script"></a>Überprüfungsskript
Sie können das folgende Skript ausführen, um die Datenbankkonfigurationen für primäre und sekundäre Replikate zu überprüfen. Bevor Sie für ein sekundäres Replikat ein Problem beheben können, müssen Sie dieses sekundäre Replikat zum primären Replikat machen.

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:

## <a name="limitations-and-known-issues"></a>Einschränkungen und bekannte Probleme
Die folgenden Einschränkungen gelten für alle Szenarien.   

**Basis-Verfügbarkeitsgruppen werden nicht unterstützt:**  
[Basis-Verfügbarkeitsgruppen](https://msdn.microsoft.com/library/mt614935.aspx) wurden mit SQL Server 2016 Standard Edition eingeführt und unterstützen den Lesezugriff auf sekundäre Replikate – und somit eine Voraussetzung für die Verwendung mit Configuration Manager – nicht.

**SQL-Server, die zusätzliche Verfügbarkeitsgruppen hosten:**   
Vor Configuration Manager, Version 1610, galt: Wenn eine Verfügbarkeitsgruppe auf einer SQL Server-Instanz neben der Gruppe für Configuration Manager eine oder mehrere Verfügbarkeitsgruppen hostet, muss jedes Replikat in jeder zusätzlichen Verfügbarkeitsgruppe zum Zeitpunkt der Ausführung des Configuration Manager-Setups oder der Installation eines Updates für Configuration Manager die folgenden Konfigurationen aufweisen:
-   **Manuelles Failover**
-   **Alle schreibgeschützten Verbindungen zulassen**

**Verwendung nicht unterstützter Datenbanken:**
-   **Configuration Manager unterstützt nur die Standortdatenbank in einer Verfügbarkeitsgruppe:** Folgende Datenbanken werden nicht unterstützt:
    -   Reporting-Datenbank
    -   WSUS-Datenbank
-   **Bereits vorhandene Datenbank:** Sie können keine neue Datenbank verwenden, die auf dem Replikat erstellt wurde. Stattdessen müssen Sie eine Kopie einer vorhandenen Configuration Manager-Datenbank auf dem primären Replikat wiederherstellen, wenn Sie eine Verfügbarkeitsgruppe konfigurieren.

**Setupfehler in „ConfigMgrSetup.log“:**  
Beim Ausführen des Setups zum Verschieben einer Standortdatenbank in eine Verfügbarkeitsgruppe versucht das Setup, Datenbankrollen in den sekundären Replikaten der Verfügbarkeitsgruppe zu verarbeiten, und protokolliert z.B. den folgenden Fehler:
-   Fehler: SQL Server-Fehler: [25000] [3906] [Microsoft] [SQL Server Native Client 11.0] [SQL Server]-Fehler beim Aktualisieren der Datenbank „CM_AAA“, weil die Datenbank schreibgeschützt ist. Configuration Manager-Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)  

Solche Fehler können ignoriert werden.

## <a name="changes-for-site-backup"></a>Änderungen für die Standortsicherung
**Sichern von Datenbankdateien**  
Wenn eine Datenbank in einer Verfügbarkeitsgruppe ausgeführt wird, muss der integrierte Wartungstask **Standortserver sichern** ausgeführt werden, um allgemeine Configuration Manager-Einstellungen und -Dateien zu sichern. Verwenden Sie jedoch nicht die MDF-oder LDF-Dateien, die von dieser Sicherung erstellt werden. Erstellen Sie stattdessen mithilfe von SQL Server direkte Sicherungskopien dieser Datenbankdateien.

**Transaktionsprotokoll:**  
Das Wiederherstellungsmodell der Standortdatenbank muss auf **Vollständig** festgelegt werden (eine Voraussetzung für die Verwendung in einer Verfügbarkeitsgruppe). Planen Sie mit dieser Konfiguration das Überwachen und Verwalten der Größe des Transaktionsprotokolls für die Standortdatenbank. Beim Wiederherstellungsmodell „Vollständig“ werden Transaktionen erst festgeschrieben, nachdem eine vollständige Sicherung der Datenbank oder des Transaktionsprotokolls erfolgt ist. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von SQL Server-Datenbanken](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases) in der SQL Server-Dokumentation.

## <a name="changes-for-site-recovery"></a>Änderungen für die Standortwiederherstellung
Sie können die Wiederherstellungsoption **Datenbankwiederherstellung überspringen (diese Option verwenden, wenn die Standortdatenbank nicht betroffen war)** verwenden, wenn zumindest ein Knoten der Verfügbarkeitsgruppe funktionsfähig bleibt.

 Bevor Sie den Standort wiederherstellen können, wenn alle Knoten einer Verfügbarkeitsgruppe verloren gegangen sind, müssen Sie die Verfügbarkeitsgruppe neu erstellen. Configuration Manager kann den Verfügbarkeitsknoten nicht neu erstellen oder wiederherstellen. Nachdem die Gruppe neu erstellt und eine Sicherung wiederhergestellt und neu konfiguriert wurde, können Sie die Wiederherstellungsoption für den Standort **Datenbankwiederherstellung überspringen (diese Option verwenden, wenn die Standortdatenbank nicht betroffen war)** verwenden.

Weitere Informationen finden Sie unter [Sicherung und Wiederherstellung für System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="changes-for-reporting"></a>Änderungen für die Berichterstattung
**Installieren des Reporting Services-Punkts:**  
Der Reporting Services-Punkt unterstützt die Verwendung des virtuellen Listenernamens der Verfügbarkeitsgruppe oder das Hosting der Reporting Services-Datenbank in einer SQL Server AlwaysOn-Verfügbarkeitsgruppe nicht:
-   Standardmäßig wird durch die Installation des Reporting Services-Punkts der **Name des Standortdatenbankservers** auf den virtuellen Namen festgelegt, der als Listener angegeben ist. Ändern Sie diese Option, um einen Computernamen und die Instanz eines Replikats in der Verfügbarkeitsgruppe anzugeben.
-   Um die Last durch die Berichterstattung zu verlagern und die Verfügbarkeit zu erhöhen, wenn ein Replikatknoten offline ist, könnten Sie zusätzliche Reporting Services-Punkte auf jedem Replikatknoten installieren und jeden Reporting Services-Punkt so konfigurieren, dass er auf seinen eigenen Computernamen verweist.

Bei der Installation eines Reporting Services-Punkts in jedem Replikat der Verfügbarkeitsgruppe kann zur Berichterstattung immer eine Verbindung mit einem aktiven Server mit einem Berichterstattungspunkt hergestellt werden.

**Wechseln des Reporting Services-Punkts, der von der Konsole verwendet wird:**  
Wechseln Sie zum Ausführen von Berichten in der Konsole zu **Überwachung** > **Übersicht** > **Berichterstellung** > **Berichte**, und wählen Sie dann **Berichtsoptionen** aus. Wählen Sie im Dialogfeld „Berichtoptionen“ den gewünschten Reporting Services-Punkt aus.

## <a name="next-steps"></a>Nächste Schritte
Wenn Sie die Voraussetzungen, Einschränkungen und Änderungen an allgemeinen Aufgaben verstehen, die für die Verwendung von Verfügbarkeitsgruppen erforderlich sind, finden Sie unter [Konfigurieren von Verfügbarkeitsgruppen für Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag) Verfahren zum Einrichten und Konfigurieren Ihres Standorts zur Nutzung von Verfügbarkeitsgruppen.
