---
title: Aktualisieren der lokalen Infrastruktur | Microsoft-Dokumentation
description: "Hier erfahren Sie, wie für eine Infrastruktur wie etwa SQL Server und das Standortbetriebssystem von Standortsystemen ein Upgrade durchgeführt wird."
ms.custom: na
ms.date: 06/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 188b7f2537dd0e569a5c00995620124512cf311b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Aktualisieren der lokalen Infrastruktur, die System Center Configuration Manager unterstützt

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die Informationen in diesem Thema, um die Serverinfrastruktur zu aktualisieren, in der System Center Configuration Manager ausgeführt wird.  

 - Informationen über das Upgrade von einer früheren Version von Configuration Manager auf System Center Configuration Manager finden Sie unter [Upgrade auf System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

- Wenn Sie Ihre System Center Configuration Manager-Infrastruktur auf eine neue Version aktualisieren möchten, lesen Sie [Updates für System Center Configuration Manager](/sccm/core/servers/manage/updates).

##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Durchführen eines Upgrades für das Betriebssystem von Standortsystemen  
 Configuration Manager unterstützt in folgenden Situationen das direkte Upgrade des Betriebssystems von Servern, auf denen ein Standortserver gehostet wird, sowie von Remoteservern, auf denen eine Standortsystemrolle gehostet wird:  

-   Direktes Upgrade auf ein höheres Windows Server Service Pack, sofern die gewählte Windows Service Pack-Stufe von Configuration Manager unterstützt wird.  
-   Direktes Upgrade von:
    - Windows Server 2012 R2 auf Windows Server 2016 ([weitere Informationen](#bkmk_2016)).
    - Windows Server 2012 auf Windows Server 2016 ([weitere Informationen](#bkmk_2016)).
    - Windows Server 2012 auf Windows Server 2012 R2 ([weitere Informationen](#bkmk_2012r2)).
    - Wenn Sie Configuration Manager Version 1602 oder höher verwenden, wird darüber hinaus auch ein Upgrade von Windows Server 2008 R2 auf Windows Server 2012 R2 unterstützt ([weitere Informationen](#bkmk_from2008r2)).

    > [!WARNING]  
    >  Vor dem Upgrade auf Windows Server 2012 R2 *müssen Sie WSUS 3.2 vom Server deinstallieren* .  
    >   
    >  Informationen zu diesem wichtigen Schritt finden Sie im Abschnitt „Neue und geänderte Funktionalität“ in der [Übersicht über Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) in der Windows Server-Dokumentation.  

Verwenden Sie für das Upgrade eines Servers die Upgradeverfahren, die von dem Betriebssystem bereitgestellt werden, auf das aktualisiert werden soll.  Weitere Informationen finden Sie in den folgenden Themen:
  -  [Upgradeoptionen für Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) in der Windows Server-Dokumentation.  
  - [Upgrade- und Konvertierungsoptionen für Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths) in der Windows Server-Dokumentation.

### <a name="bkmk_2016"></a> Upgrade von Windows Server 2012 oder Windows Server 2012 R2 auf Windows Server 2016
Wenn Sie Windows Server 2012 oder Windows Server 2012 R2 auf Windows Server 2016 aktualisieren, gilt Folgendes:


**Vor dem Upgrade:**  
-   Entfernen Sie den SCEP-Client (System Center Endpoint Protection). In Windows Server 2016 ist Windows Defender integriert, sodass der SCEP-Client nicht mehr erforderlich ist. Durch das Vorhandensein des SCEP-Clients wird ein Upgrade auf Windows Server 2016 möglicherweise verhindert.

**Nach dem Upgrade:**
-   Stellen Sie sicher, dass Windows Defender aktiviert ist, automatisch gestartet und ausgeführt wird.
-   Stellen Sie sicher, dass die folgenden Configuration Manager-Dienste ausgeführt werden:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Stellen Sie sicher, dass der **Windows-Prozessaktivierungsdienst** und der Dienst **WWW/W3svc** aktiviert sind, automatisch gestartet und für die folgenden Standortsystemrollen ausgeführt werden (diese Dienste werden beim Upgrade deaktiviert):
  -     Standortserver
  -     Verwaltungspunkt
  -     Anwendungskatalog-Webdienstpunkt
  -     Anwendungskatalog-Websitepunkt

-   Stellen Sie sicher, dass alle Server, auf denen eine Standortsystemrolle gehostet wird, weiterhin alle [Voraussetzungen für Standortsystemrollen](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) erfüllen, die auf diesem Server ausgeführt werden. Möglicherweise müssen Sie BITS oder WSUS neu installieren oder bestimmte Einstellungen für IIS konfigurieren.

-   Nachdem Sie alle erforderlichen Komponenten wiederhergestellt haben, starten Sie den Server erneut, um sicherzustellen, dass alle Dienste gestartet wurden und funktionsfähig sind.

**Bekanntes Problem für die Configuration Manager-Remotekonsole:**  
Nach dem Upgrade des Standortservers oder eines Servers, auf dem eine Instanz des SMS-Anbieters gehostet wird, auf Windows Server 2016 können Administratoren möglicherweise keine Verbindung mit einer Configuration Manager-Konsole am Standort herstellen. Um dieses Problem zu umgehen, müssen Sie Berechtigungen für die SMS-Administratorengruppe in WMI manuell wiederherstellen. Berechtigungen müssen auf dem Standortserver sowie auf allen Remoteservern, auf denen eine Instanz des SMS-Anbieters gehostet wird, festgelegt werden:

1. Öffnen Sie auf den entsprechenden Servern die Microsoft Management Console (MMC), fügen Sie das Snap-In für die **WMI-Steuerung** hinzu, und wählen Sie dann **Lokaler Computer** aus.
2. Öffnen Sie in der MMC die **Eigenschaften** von **WMI-Steuerung (Lokal)**, und wählen Sie die Registerkarte **Sicherheit** aus.
3. Erweitern Sie die Struktur unter dem Stamm, wählen Sie den Knoten **SMS** aus, und wählen Sie dann **Sicherheit**.  Stellen Sie sicher, dass die Gruppe **SMS-Administratoren** über folgende Berechtigungen verfügt:
  -     Konto aktivieren
  -     Remoteaktivierung
4. Wählen Sie auf der Registerkarte **Sicherheit** unter dem Knoten **SMS** den Knoten **Standort_&lt;Standortcode**> und anschließend **Sicherheit** aus. Stellen Sie sicher, dass die Gruppe **SMS-Administratoren** über folgende Berechtigungen verfügt:
  -   Methoden ausführen
  -   Anbieterschreibzugriff
  -   Konto aktivieren
  -   Remoteaktivierung
5. Speichern Sie die Berechtigungen, um den Zugriff für die Configuration Manager-Konsole wiederherzustellen.

### <a name="bkmk_2012r2"></a> Windows Server 2012 auf Windows Server 2012 R2

**Vor dem Upgrade:**
-  Im Gegensatz zu den anderen unterstützten Szenarios müssen bei diesem Szenario vor dem Upgrade keine weiteren Aspekte berücksichtigt werden.

**Nach dem Upgrade:**
  - Stellen Sie sicher, dass der Windows-Bereitstellungsdienst gestartet wurde und für die folgenden Standortsystemrollen ausgeführt wird (dieser Dienst wird beim Upgrade beendet):
    - Standortserver
    - Verwaltungspunkt
    - Anwendungskatalog-Webdienstpunkt
    - Anwendungskatalog-Websitepunkt

  -     Stellen Sie sicher, dass der **Windows-Prozessaktivierungsdienst** und der Dienst **WWW/W3svc** aktiviert sind, automatisch gestartet und für die folgenden Standortsystemrollen ausgeführt werden (diese Dienste werden beim Upgrade deaktiviert):
    -   Standortserver
    -   Verwaltungspunkt
    -   Anwendungskatalog-Webdienstpunkt
    -   Anwendungskatalog-Websitepunkt


  -     Stellen Sie sicher, dass alle Server, auf denen eine Standortsystemrolle gehostet wird, weiterhin alle [Voraussetzungen für Standortsystemrollen](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) erfüllen, die auf diesem Server ausgeführt werden. Möglicherweise müssen Sie BITS oder WSUS neu installieren oder bestimmte Einstellungen für IIS konfigurieren.

  Nachdem Sie alle erforderlichen Komponenten wiederhergestellt haben, starten Sie den Server erneut, um sicherzustellen, dass alle Dienste gestartet wurden und funktionsfähig sind.

### <a name="bkmk_from2008r2"></a>  Upgrade von Windows Server 2008 R2 auf Windows Server 2012 R2
Für dieses Szenario für ein Betriebssystemupgrade gelten folgende Bedingungen:  

**Vor dem Upgrade:**
-   Deinstallieren Sie WSUS 3.2.  
    Vor dem Upgrade eines Serverbetriebssystems auf Windows Server 2012 R2 müssen Sie WSUS 3.2 auf dem Server deinstallieren. Informationen zu diesem wichtigen Schritt finden Sie im Abschnitt „Neue und geänderte Funktionalität“ in der „Übersicht über Windows Server Update Services“ in der Windows Server-Dokumentation.

**Nach dem Upgrade:**
  - Stellen Sie sicher, dass der Windows-Bereitstellungsdienst gestartet wurde und für die folgenden Standortsystemrollen ausgeführt wird (dieser Dienst wird beim Upgrade beendet):
    - Standortserver
    - Verwaltungspunkt
    - Anwendungskatalog-Webdienstpunkt
    - Anwendungskatalog-Websitepunkt


  -     Stellen Sie sicher, dass der **Windows-Prozessaktivierungsdienst** und der Dienst **WWW/W3svc** aktiviert sind, automatisch gestartet und für die folgenden Standortsystemrollen ausgeführt werden (diese Dienste werden beim Upgrade deaktiviert):
    -   Standortserver
    -   Verwaltungspunkt
    -   Anwendungskatalog-Webdienstpunkt
    -   Anwendungskatalog-Websitepunkt


  -     Stellen Sie sicher, dass alle Server, auf denen eine Standortsystemrolle gehostet wird, weiterhin alle [Voraussetzungen für Standortsystemrollen](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) erfüllen, die auf diesem Server ausgeführt werden. Möglicherweise müssen Sie BITS oder WSUS neu installieren oder bestimmte Einstellungen für IIS konfigurieren.

  Nachdem Sie alle erforderlichen Komponenten wiederhergestellt haben, starten Sie den Server erneut, um sicherzustellen, dass alle Dienste gestartet wurden und funktionsfähig sind.


### <a name="unsupported-upgrade-scenarios"></a>Nicht unterstützte Upgradeszenarios
Die folgenden Windows Server-Upgradeszenarios werden zwar häufig angefragt, werden aber von Configuration Manager nicht unterstützt:  

-   Windows Server 2008 auf Windows Server 2012 oder höher  
-   Windows Server 2008 R2 auf Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a> Durchführen eines Upgrades für das Betriebssystem von Configuration Manager-Clients  
 Configuration Manager unterstützt in den folgenden Situationen ein direktes Upgrade für das Betriebssystem von Configuration Manager-Clients:  

-   Direktes Upgrade auf ein höheres Windows Service Pack, sofern die gewählte Service Pack-Stufe von Configuration Manager unterstützt wird.  

-   Direktes Windows-Upgrade von einer unterstützten Version auf Windows 10. Weitere Informationen finden Sie unter [Aktualisieren von Windows auf die neueste Version mit System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Windows 10-Dienstupgrades von Build zu Build.  Weitere Informationen finden Sie unter [Verwalten von Windows als Dienst mit System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Ausführen eines Upgrades für SQL Server auf dem Standortdatenbankserver  
  Configuration Manager unterstützt ein direktes Upgrade von SQL Server von einer unterstützten Version von SQL auf dem Standortdatenbankserver. Der SQL Server-Upgradeszenarios in diesem Bereich, die von Configuration Manager unterstützt werden, und enthalten Anforderungen für die einzelnen Szenarios.

 Weitere Informationen über SQL Server-Versionen, die von Configuration Manager unterstützt werden, finden Sie unter [Support for SQL Server versions for System Center Configuration Manager (Unterstützung für SQL Server-Versionen für System Center Configuration Manager)](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 **Upgrade der Service Pack-Version von SQL Server:**    
 Configuration Manager unterstützt das direkte Upgrade von SQL Server auf ein höheres Service Pack, sofern die gewählte SQL Server Service Pack-Stufe von Configuration Manager unterstützt wird.

 Wenn Sie über mehrere Configuration Manager-Standorte in einer Hierarchie verfügen, kann an jedem Standort eine andere Service Pack-Version von SQL Server ausgeführt werden. Außerdem gibt es keine Beschränkung bezüglich der Reihenfolge, in der die für die Standortdatenbank verwendete SQL Server Service Pack-Version an den Standorten aktualisiert wird.

 **Upgrade auf eine neue Version von SQL Server:**   
 Configuration Manager unterstützt das direkte Upgrade von SQL Server auf die folgenden Versionen:

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

Wenn Sie für die Version von SQL Server, unter der die Standortdatenbank gehostet wird, ein Upgrade ausführen, müssen Sie die verwendete SQL Server-Version in der folgenden Reihenfolge an den Standorten aktualisieren:

 1. Aktualisieren Sie zuerst SQL Server am Standort der zentralen Verwaltung.
 2. Aktualisieren Sie sekundäre Standorte, bevor Sie den übergeordneten primären Standort der sekundären Standorte aktualisieren.
 3. Aktualisieren Sie übergeordnete primäre Standorte zuletzt. Dies schließt sowohl untergeordnete primäre Standorte, die einem Standort der zentralen Verwaltung unterstellt sind, als auch eigenständige primäre Standorte ein, die den Standort der obersten Ebene einer Hierarchie darstellen.

**SQL Server-Kardinalitätsschätzungsgrad und Standortdatenbank:**   
Wenn eine Standortdatenbank von einer früheren Version von SQL Server aktualisiert wird, behält die Datenbank den vorhandenen SQL-Kardinalitätsschätzungsgrad (CE-Grad), wenn dieser dem Minimum entspricht, der für diese Instanz von SQL Server zulässig ist. Wenn SQL Server mit einer Datenbank aktualisiert wird, deren Kompatibilitätsgrad niedriger ist als der zulässige Grad, wird die Datenbank automatisch auf den niedrigsten Kompatibilitätsgrad gesetzt, der in SQL Server zulässig ist.

Die folgende Tabelle zeigt die empfohlenen Kompatibilitätsgrade für Standortdatenbanken von Configuration Manager:

|SQL Server-Version | Unterstützte Kompatibilitätsgrade |Empfohlener Grad|
|----------------|--------------------|--------|
| SQL Server 2016| 130, 120, 110, 100 | 130|
| SQL Server 2014| 120, 110, 100      | 110|

Um den SQL Server-CE-Kompatibilitätsgrad zu ermitteln, der für Ihre Standortdatenbank verwendet wird, führen Sie die folgende SQL-Abfrage auf dem Standortdatenbankserver aus: **SELECT name, compatibility_level FROM sys.databases**.

 Weitere Informationen zu SQL-CE-Kompatibilitätsgraden und deren Festlegung finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx).


Weitere Informationen zu SQL Server finden Sie in der SQL Server-Dokumentation auf TechNet:
-   [Upgrade auf SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [Upgrade auf SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [Upgrade auf SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>So führen Sie ein SQL Server-Upgrade auf dem Standortdatenbankserver aus  

1.  Beenden Sie alle Configuration Manager-Dienste am Standort.  
2.  Führen Sie für SQL Server ein Upgrade auf eine unterstützte Version aus.  
3.  Starten Sie die Configuration Manager-Dienste neu.  

> [!NOTE]  
>  Wenn Sie die verwendete SQL Server-Edition am Standort der zentralen Verwaltung von einer Standard Edition entweder in eine Datencenter oder Enterprise Edition ändern, wird die Datenbankpartition, die die Anzahl der von der Hierarchie unterstützten Clients begrenzt, nicht geändert.
