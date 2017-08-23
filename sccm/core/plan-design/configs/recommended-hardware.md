---
title: Empfohlene Hardware | Microsoft-Dokumentation
description: "Hier finden Sie Informationen über empfohlene Hardware, mit deren Hilfe Sie Ihre System Center Configuration Manager-Umgebung über eine einfache Bereitstellung hinaus skalieren können."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
caps.latest.revision: "26"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8dac6df60b07461d6410d305723b3f03fb09fa16
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>Empfohlene Hardware für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die folgenden Empfehlungen sind Leitlinien zur Unterstützung der Skalierung Ihrer System Center Configuration Manager-Umgebung, um mehr als eine sehr grundlegende Bereitstellung von Standorten, Standortsystemen und Clients zu unterstützen. Sie sollen nicht jede denkbare Standort- und Hierarchiekonfiguration abdecken.  

 Verwenden Sie diese Informationen in den folgenden Abschnitten als Leitfaden zur Unterstützung bei der Auswahl von Hardware, mit der Clients und Standorte die Verarbeitungslasten für die verfügbaren Configuration Manager-Features mit den Standardkonfigurationen bewältigen können.  


##  <a name="bkmk_ScaleSieSystems"></a> Standortsysteme  
 In diesem Abschnitt werden die empfohlenen Hardwarekonfigurationen für Configuration Manager-Standortsysteme für Bereitstellungen beschrieben, von denen die maximale Anzahl von Clients unterstützt wird und von denen die meisten oder alle Configuration Manager-Features genutzt werden. Für Bereitstellungen, die weniger als die maximale Anzahl von Clients unterstützen und nicht alle verfügbare Features verwenden, werden unter Umständen weniger Computerressourcen benötigt. Im Allgemeinen beschränken unter anderem folgende Hauptfaktoren in dieser Reihenfolge die Gesamtleistung des Systems:  

1.  E/A-Festplattenleistung  

2.  Verfügbarer Arbeitsspeicher  

3.  CPU  

Verwenden Sie zur Leistungsoptimierung RAID 10-Konfigurationen für alle Datenlaufwerke und 1 GBit/s-Ethernet-Netzwerkverbindungen.  

###  <a name="bkmk_ScaleSiteServer"></a> Standortserver  

|Eigenständiger primärer Standort|CPU (Kerne)|Arbeitsspeicher (GB)|Speicherbelegung für SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Eigenständiger primärer Standortserver mit einer Datenbankstandortrolle auf dem gleichen Server<sup>1</sup>|16|96|80|  
|Eigenständiger primärer Standortserver mit einer Remotestandortdatenbank|8|16|-|  
|Remotedatenbankserver für einen eigenständigen primären Standort|16|72|90|  
|Standortserver der zentralen Verwaltung mit einer Datenbankstandortrolle auf dem gleichen Server<sup>1</sup>|20|128|80|  
|Standortserver der zentralen Verwaltung mit einer Remotestandortdatenbank|8|16|-|  
|Remotedatenbankserver für einen Standort der zentralen Verwaltung|16|96|90|  
|Untergeordneter primärer Standort mit einer Datenbankstandortrolle auf dem gleichen Server|16|96|80|  
|Untergeordneter primärer Standortserver mit einer Remotestandortdatenbank|8|16|-|  
|Remotedatenbankserver für einen untergeordneten primären Standort|16|72|90|  
|Sekundärer Standortserver|8|16|-|  

 <sup>1</sup> Wenn Standortserver und SQL Server auf demselben Computer installiert sind, unterstützt die Bereitstellung eine maximale [Größe und Anzahl](/sccm/core/plan-design/configs/size-and-scale-numbers) für Standorte und Clients. Diese Konfiguration kann [Hochverfügbarkeitsoptionen für System Center Configuration Manager](/sccm/protect/understand/high-availability-options) wie die Verwendung eines SQL Server-Clusters begrenzen. Darüber hinaus sollten Benutzer mit größeren Installationen die Verwendung einer Konfiguration mit einem SQL Server-Remotecomputer in Betracht ziehen, weil zur Unterstützung des SQL Server- und Configuration Manager-Standortservers höhere E/A-Anforderungen erforderlich sind, wenn beide auf demselben Computer ausgeführt werden.  

###  <a name="bkmk_RemoteSiteSystem"></a> Remote-Standortsystemserver  
 Der folgende Leitfaden gilt für Computer, die eine einzelne Standortsystemrolle innehaben. Planen Sie Anpassungen ein, wenn Sie mehrere Standortsystemrollen auf demselben Computer installieren.  

|Standortsystemrolle|CPU (Kerne)|Arbeitsspeicher (GB)|Speicherplatz (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Verwaltungspunkt|4|8|50|  
|Verteilungspunkt|2|8|Je nach Bedarf des Betriebssystems und zum Speichern von bereitgestelltem Inhalt erforderlich|  
|Anwendungskatalog mit Webdienst und Website auf dem Standortsystemcomputer|4|16|50|  
|Softwareupdatepunkt<sup>1</sup>|8|16|Je nach Bedarf des Betriebssystems und zum Speichern von bereitgestellten Updates erforderlich|  
|Alle anderen Standortsystemrollen|4|8|50|  

 <sup>1</sup> Der Computer, auf dem ein Softwareupdatepunkt gehostet wird, erfordert die folgenden Konfigurationen für IIS-Anwendungspools:  

-   Erhöhen Sie die **WsusPool-Warteschlangenlänge** auf **2000**.  

-   Erhöhen Sie die **Begrenzung des privaten Speichers für WsusPool** auf das Vierfache, oder legen Sie den Wert auf **0** (unbegrenzt) fest.  

###  <a name="bkmk_DiskSpace"></a> Speicherplatz für Standortsysteme  
 Die Datenträgerzuordnung und -konfiguration trägt zur Leistung von Configuration Manager bei. Da jede Configuration Manager-Umgebung anders ist, können die gewählten Werte vom folgenden Leitfaden abweichen.  

 Platzieren Sie jedes Objekt zur Leistungsoptimierung auf einem separaten, dedizierten RAID-Volume. Verwenden Sie zur Leistungsoptimierung für alle Datenvolumes (Configuration Manager und Datenbankdateien) RAID 10.  

|Datennutzung|Mindesspeicherplatz auf dem Datenträger|25.000 Clients|50.000 Clients|100.000 Clients|150.000 Clients|700.000 Clients (Standort der zentralen Verwaltung)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Betriebssystem|Siehe Leitfaden für das Betriebssystem|Siehe Leitfaden für das Betriebssystem|Siehe Leitfaden für das Betriebssystem|Siehe Leitfaden für das Betriebssystem|Siehe Leitfaden für das Betriebssystem|Siehe Leitfaden für das Betriebssystem|  
|Configuration Manager-Anwendung und Protokolldateien|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|MDF-Standortdatenbankdatei|75 GB je 25.000 Clients|75 GB|150 GB|300 GB|500 GB|2 TB|  
|LDF-Standortdatenbankdatei|25 GB je 25.000 Clients|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Temporäre Datenbankdateien (MDF und LDF)|Nach Bedarf|Nach Bedarf|Nach Bedarf|Nach Bedarf|Nach Bedarf|Nach Bedarf|  
|Inhalt (Verteilungspunktfreigaben)|Nach Bedarf<sup>1</sup>|Nach Bedarf<sup>1</sup>|Nach Bedarf<sup>1</sup>|Nach Bedarf<sup>1</sup>|Nach Bedarf<sup>1</sup>|Nach Bedarf<sup>1</sup>|  

 <sup>1</sup> Die Speicherplatzrichtlinien für Datenträger verstehen sich ausschließlich des für Inhalte in der Inhaltsbibliothek auf dem Standortserver oder an Verteilungspunkten erforderlichen Speicherplatzes. Informationen zur Planung der Inhaltsbibliothek finden Sie unter [The content library in System Center Configuration Manager](../../../core/plan-design/hierarchy/the-content-library.md) (Inhaltsbibliothek in System Center Configuration Manager).  

 Beachten Sie bei der Planung für Speicherplatzanforderungen zusätzlich zu diesem Leitfaden die folgenden Leitlinien:  

-   Für jeden Client sind ca. 5 MB Speicherplatz erforderlich.  

-   Planen Sie für die temporäre Datenbank eines primären Standorts 25 % bis 30 % der Größe der MDF-Standortdatenbankdatei ein. Der tatsächliche Platzbedarf kann erheblich geringer oder höher sein. Dies ist von der Leistung des Standortservers und der Menge kurz- und langfristig eingehender Daten abhängig.  

    > [!NOTE]  
    >  Wenn Sie über 50.000 oder mehr Clients an einem Standort verfügen, planen Sie die Verwendung von vier oder mehr MDF-Dateien für die temporäre Datenbank ein.  

-   Die temporäre Datenbank für einen Standort der zentralen Verwaltung ist in der Regel deutlich kleiner als die Datenbank für einen primären Standort.  

-   Die Datenbankgröße für den sekundären Standort ist durch folgende Faktoren eingeschränkt:  

    -   SQL Server 2012 Express: 10 GB  

    -   SQL Server 2014 Express: 10 GB  

##  <a name="bkmk_ScaleClient"></a> Clients  
 In diesem Abschnitt werden die empfohlenen Hardwarekonfigurationen für Computer bestimmt, die durch die Verwendung von Configuration Manager-Clientsoftware verwaltet werden.  

### <a name="client-for-windows-computers"></a>Client für Windows-Computer  
 Nachfolgend sind die Mindestanforderungen für Windows-Computer aufgeführt, die Sie mit Configuration Manager verwalten, einschließlich Embedded-Betriebssysteme:  

-   **Prozessor und Arbeitsspeicher:** Informationen hierzu entnehmen Sie den Prozessor- und Arbeitsspeicheranforderungen für das Betriebssystem des jeweiligen Computers.  

-   **Speicherplatz:** 500 MB verfügbarer Speicherplatz (5 GB empfohlen) für den Configuration Manager-Clientcache. Weniger Speicherplatz ist erforderlich, wenn Sie benutzerdefinierte Einstellungen zur Installation des Configuration Manager-Clients verwenden:  

    -   Verwenden Sie die CCMSetup-Befehlszeileneigenschaft „/skipprereq“, um die Installation von Dateien zu vermeiden, die vom Client nicht benötigt werden. Beispiel: **CCMSetup.exe /skipprereq:silverlight.exe**, falls der Client den Anwendungskatalog nicht verwendet.  

    -   Verwenden Sie die Client.msi-Eigenschaft SMSCACHESIZE, um eine Cachedatei festzulegen, die kleiner als die Standardgröße von 5.120 MB ist. Die Mindestgröße beträgt 1 MB. Beispiel: Durch **CCMSetup.exe SMSCachesize=2** wird ein Cache von 2 MB erstellt.  

    Weitere Informationen zu diesen Clientinstallationseinstellungen finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    >  Die Clientinstallation mit minimalem Speicherplatz ist hilfreich für Windows Embedded-Geräte, die in der Regel über kleinere Datenträgergrößen als Windows-Standardcomputer verfügen.  



 Nachfolgend sind zusätzliche Mindestanforderungen an die Hardware für optionale Funktionen in Configuration Manager aufgeführt.  

-   **Betriebssystembereitstellung:** 384 MB Arbeitsspeicher  

-   **Softwarecenter:** Prozessor mit 500 MHz  

-   **Remotesteuerung:** Pentium 4 mit Hyperthreading 3 GHz (Single Core) oder vergleichbare CPU mit mindestens 1 GB RAM für optimale Leistung  

### <a name="client-for-linux-and-unix"></a>Client für Linux und UNIX  
 Nachfolgend sind die Mindestanforderungen für Linux- und UNIX-Server aufgeführt, die Sie mit Configuration Manager verwalten.  

|Anforderungen|Details|  
|-----------------|-------------|  
|Prozessor und Arbeitsspeicher|Weitere Informationen entnehmen Sie den Prozessor- und Arbeitsspeicheranforderungen des Computerbetriebssystems.|  
|Speicherplatz|500 MB verfügbarer Speicherplatz (5 GB empfohlen) für den Configuration Manager-Clientcache|  
|Netzwerkverbindungen|Configuration Manager-Clientcomputer müssen über eine Netzwerkverbindung mit Configuration Manager-Standortsystemen verfügen, um die Verwaltung zu ermöglichen.|  

##  <a name="bkmk_ScaleConsole"></a> Configuration Manager-Konsole  
 Die Anforderungen in der folgenden Tabelle gelten für alle Computer, auf denen die Configuration Manager-Konsole ausgeführt wird.  

 **Mindestkonfiguration der Hardware:**  

-   Intel i3 oder vergleichbare CPU  

-   2 GB RAM  

-   2 GB Speicherplatz  

|DPI-Einstellung|Mindestauflösung|  
|-----------------|------------------------|  
|96 / 100 %|1024 x 768|  
|120 /125 %|1280 x 960|  
|144 / 150 %|1600 x 1200|  
|196 / 200 %|2500 x 1600|  

 **Unterstützung für PowerShell:**  

 Wenn Sie PowerShell-Unterstützung auf einem Computer installieren, auf dem die Configuration Manager-Konsole ausgeführt wird, können Sie PowerShell-Cmdlets auf diesem Computer ausführen, um Configuration Manager zu verwalten.

 - PowerShell 3.0 oder höher wird unterstützt.

Zusätzlich zu PowerShell wird die Windows Management Framework-Version (WMF) 3.0 unterstützt.   


##  <a name="bkmk_ScaleLab"></a> Laborbereitstellungen  
 Verwenden Sie die folgenden Hardwaremindestempfehlungen für Labor- und Testbereitstellungen von Configuration Manager. Diese Empfehlungen gelten für alle Standorttypen mit bis zu 100 Clients:  

|Rolle|CPU (Kerne)|Arbeitsspeicher (GB)|Speicherplatz (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Standort- und Datenbankserver|2 - 4|7 - 12|100|  
|Standortsystemserver|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  
