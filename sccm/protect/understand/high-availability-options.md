---
title: "Hohe Verfügbarkeit | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über das Bereitstellen von System Center Configuration Manager mithilfe von Optionen, die eine hohe Dienstverfügbarkeit gewährleisten."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d3e9afb90cdc85bc7299626b642c52be659e3bdf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="high-availability-options-for-system-center-configuration-manager"></a>Hochverfügbarkeitsoptionen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*



Sie können System Center Configuration Manager mithilfe von Optionen bereitstellen, die eine hohe Dienstverfügbarkeit gewährleisten.   

Optionen, die hohe Verfügbarkeit unterstützen:   

-   Von Standorten werden mehrere Instanzen von Standortsystemservern, die wichtige Dienste für Clients bereitstellen, unterstützt.  

-   Von Standorten der zentralen Verwaltung und primären Standorten wird die Sicherung der Standortdatenbank unterstützt. Die Standortdatenbank enthält sämtliche Konfigurationen für Standorte und Clients. In einer Hierarchie, die einen Standort der zentralen Verwaltung umfasst, wird die Datenbank für die verschiedenen Standorte freigegeben.  

-   Durch integrierte Wiederherstellungsoptionen kann die Serverdowntime reduziert werden. Die Wiederherstellung wird bei einer Hierarchie mit einem Standort der zentralen Verwaltung durch erweiterte Optionen vereinfacht.  

-   Typische Probleme können von Clients automatisch und ohne Eingreifen des Administrators behoben werden.  

-   Von Standorten werden Warnungen zu Clients ausgegeben, von denen keine aktuellen Daten übermittelt werden. Administratoren werden so auf potenzielle Probleme aufmerksam gemacht.  

-   Configuration Manager bietet mehrere integrierte Berichte, mit denen Sie Probleme und Trends identifizieren können, bevor diese sich zu Problemen für Server- oder Clientvorgänge entwickeln.  

 Configuration Manager stellt keinen Echtzeitdienst bereit, und Sie müssen sich auf ein gewisses Maß an Datenlatenz einstellen. Es ist daher ungewöhnlich, dass eine vorübergehende Dienstunterbrechung sich zu einem kritischen Problem entwickelt. Wenn Sie Ihre Standorte und Hierarchien mit Blick auf eine hohe Verfügbarkeit konfiguriert haben, kann die Downtime auf ein Minimum reduziert, die Autonomie der Vorgänge aufrechterhalten und ein hoher Servicelevel bereitgestellt werden.  

 Beispielsweise führen Configuration Manager-Clients Verarbeitungsvorgänge in der Regel autonom aus. Dabei werden bekannte Zeitpläne und Konfigurationen für Vorgänge sowie Zeitpläne für die Übermittlung der zu verarbeitenden Daten an den Standort verwendet.  

-   Wenn von den Clients keine Verbindung mit dem Standort hergestellt werden kann, werden die zu übermittelnden Daten zwischengespeichert, bis eine Verbindung zustande kommt.  

-   Kann keine Verbindung mit dem Standort hergestellt werden, werden Clientvorgänge zudem mithilfe der letzten bekannten Zeitpläne und der zwischengespeicherten Informationen fortgesetzt, bis eine Verbindung mit dem Standort hergestellt werden kann und neue Richtlinien empfangen werden. Beispielsweise werden zuvor heruntergeladene Anwendungen ausgeführt bzw. installiert.  

-   Die Standortsysteme und Clients eines Standorts werden auf regelmäßige Statusaktualisierungen überwacht. Wenn diese Aktualisierungen nicht registriert werden können, werden vom Standort entsprechende Warnungen ausgegeben.  

-   Über integrierte Berichte erhalten Sie einen Einblick in den laufenden Betrieb sowie in historische Vorgänge und Trends. Configuration Manager unterstützt auch statusbasierte Meldungen, über die Informationen zu laufenden Vorgängen beinahe in Echtzeit bereitgestellt werden.  

  Verwenden Sie die Informationen in diesem Thema mit den Informationen in den folgenden Artikeln:
-   [Empfohlene Hardware](../../core/plan-design/configs/recommended-hardware.md)
-   [Unterstützte Betriebssysteme für Standortsystemserver](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  

-   [Voraussetzungen für Standorte und Standortsysteme](../../core/plan-design/configs/site-and-site-system-prerequisites.md)


##  <a name="bkmk_snh"></a> Hohe Verfügbarkeit für Standorte und Hierarchien  
 **Hosten der Standortdatenbank mit einem SQL Server-Cluster:**  

 Wenn Sie für die Datenbank an einem Standort der zentralen Verwaltung oder einem primären Standort einen SQL Server-Cluster verwenden, profitieren Sie von der in SQL Server integrierten Failoverunterstützung.  

 Von sekundären Standorten können keine SQL Server-Cluster verwendet werden, und die Sicherung oder Wiederherstellung ihrer Standortdatenbank wird nicht unterstützt. Zur Wiederherstellung eines sekundären Standorts installieren Sie den sekundären Standort vom übergeordneten primären Standort aus neu.  

 **Verwenden einer SQL Server Always On-Verfügbarkeitsgruppe zum Hosten der Standortdatenbank:**  

 Beginnend mit der Version 1602 können Sie SQL Server-AlwaysOn-Verfügbarkeitsgruppen zum Hosten der Standortdatenbank an primären Standorten und am Standort der zentralen Verwaltung als Lösung für hohe Verfügbarkeit und Notfallwiederherstellung nutzen. Weitere Informationen finden Sie unter [SQL Server Always On für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

 **Bereitstellen einer Standorthierarchie mit einem Standort der zentralen Verwaltung und untergeordneten primären Standorten:**  

 Mithilfe dieser Konfiguration kann eine Fehlertoleranz bereitgestellt werden, falls überlappende Netzwerksegmente von den Standorten verwaltet werden. Darüber hinaus wird mit dieser Konfiguration eine zusätzliche Wiederherstellungsoption angeboten. So wird es möglich, die Standortdatenbank am wiederhergestellten Standort anhand der Informationen in der an einem anderen Standort verfügbaren, freigegebenen Datenbank neu zu erstellen. Mit dieser Option können Sie eine fehlerhafte oder nicht verfügbare Sicherung der fehlerhaften Standortdatenbank ersetzen.  

 **Erstellen regelmäßiger Sicherungen am Standort der zentralen Verwaltung und an primären Standorten:**  

 Wenn Sie regelmäßige Standortsicherungen erstellen und testen, stehen Ihnen jederzeit die zur Wiederherstellung eines Standorts erforderlichen Daten zur Verfügung, und Sie verfügen über die notwendige Erfahrung, um einen Standort mit minimalem Zeitaufwand wiederherzustellen.  

 **Installieren mehrerer Instanzen von Standortsystemrollen:**  

 Wenn Sie mehrere Instanzen kritischer Standortsystemrollen, wie beispielsweise Verwaltungspunkt und Verteilungspunkt, installieren, stellen Sie für den Fall, dass ein bestimmter Standortsystemserver offline ist, redundante Kontaktpunkte für Clients bereit.  

 **Installieren Sie mehrere Instanzen des SMS-Anbieters an einem Standort:** Der SMS-Anbieter stellt den administrativen Kontaktpunkt für eine oder mehrere Configuration Manager-Konsolen bereit. Wenn Sie mehrere SMS-Anbieter installieren, können Sie Redundanz für Kontaktpunkte zur Verwaltung des Standorts und der Hierarchie bereitstellen.  

##  <a name="bkmk_ssr"></a> Hohe Verfügbarkeit für Standortsystemrollen  
 Sie stellen an jedem Standort Standortsystemrollen bereit, um die Dienste verfügbar zu machen, die an diesem Standort von Clients verwendet werden sollen. Die Standortdatenbank enthält die Konfigurationsinformationen für den Standort und sämtliche Clients. Verwenden Sie mindestens eine der verfügbaren Optionen, um eine hohe Verfügbarkeit der Standortdatenbank sowie bei Bedarf die Wiederherstellung des Standorts und der Standortdatenbank zu ermöglichen.  

 **Redundanz für wichtige Standortsystemrollen:**  

-   Anwendungskatalog-Webdienstpunkt  

-   Anwendungskatalog-Websitepunkt  

-   Verteilungspunkt  

-   Verwaltungspunkt  

-   Softwareupdatepunkt  

-   Zustandsmigrationspunkt  

 Sie können mehrere Instanzen der Reporting Services-Punktrolle installieren, um Redundanz für die Berichterstattung an Standorten und auf Clients bereitzustellen.

 Sie können die folgende Softwareupdatepunkt-Standortsystemrolle auf einem Windows NLB-Cluster (Network Load Balancing, Netzwerklastenausgleich) installieren, um Failoverunterstützung bereitzustellen  


 **Integrierte Standortsicherung:**  

 Configuration Manager enthält einen integrierten Sicherungstask, mit dessen Hilfe Sie einen Standort und kritische Informationen regelmäßig sichern können. Darüber hinaus unterstützt der Setup-Assistent von Configuration Manager Standortwiederherstellungsaktionen, mit denen Sie die Betriebsfähigkeit eines Standorts wiederherstellen können.  

 **Veröffentlichen in Active Directory Domain Services und DNS:**  

 Sie können jeden Standort zur Veröffentlichung von Daten zu Standortsystemservern und -diensten in den Active Directory-Domänendiensten und DNS konfigurieren. Von den Clients kann dann der zugänglichste Server im Netzwerk identifiziert werden. Zudem können neue Standortsystemserver, von denen wichtige Dienste wie Verwaltungspunkte bereitgestellt werden können, erkannt werden.  

 **SMS-Anbieter und Configuration Manager-Konsole:**  

 Configuration Manager unterstützt die Installation mehrerer SMS-Anbieter auf separaten Computern, damit für die Configuration Manager-Konsole mehrere Zugriffspunkte verfügbar sind. Auf diese Weise wird sichergestellt, dass Sie selbst dann Configuration Manager-Standorte und Clients anzeigen und neu konfigurieren können, wenn ein SMS-Anbietercomputer offline ist.  

 Beim Herstellen einer Verbindung mit einem Standort stellt eine Configuration Manager-Konsole eine Verbindung mit einer Instanz des SMS-Anbieters an diesem Standort her. Die Instanz des SMS-Anbieters wird nicht deterministisch ausgewählt. Wenn der ausgewählte SMS-Anbieter nicht verfügbar ist, haben Sie folgende Möglichkeiten:  

-   Verbinden Sie die Konsole erneut mit dem Standort. Jede neue Verbindungsanforderung wird auf nicht deterministische Weise einer Instanz des SMS-Anbieters zugewiesen. Es ist möglich, dass der neuen Verbindung eine verfügbare Instanz zugewiesen wird.  

-   Verbinden Sie die Konsole mit einem anderen Configuration Manager-Standort, und verwalten Sie die Konfiguration über diese Verbindung. Bei dieser Vorgehensweise tritt bei Konfigurationsänderungen eine kurze Verzögerung von ein paar Minuten auf. Sobald der SMS-Anbieter des Standorts online ist, können Sie die Configuration Manager-Konsole wieder direkt mit dem zu verwaltenden Standort verbinden.  

 Sie können die Configuration Manager-Konsole auf mehreren Computern installieren, die von Administratoren verwendet werden. Jeder SMS-Anbieter unterstützt Verbindungen von mehreren Configuration Manager-Konsolen.  

 **Verwaltungspunkt:**  

 Installieren Sie an jedem primären Standort mehrere Verwaltungspunkte, und sorgen Sie dafür, dass die Veröffentlichung von Standortdaten in der Active Directory-Infrastruktur und DNS durch die Standorte möglich ist.  

 Sind mehrere Verwaltungspunkte vorhanden, können Sie einen Lastenausgleich vornehmen, wenn ein einzelner Verwaltungspunkt von mehreren Clients in Anspruch genommen wird. Außerdem können Sie mehrere Datenbankreplikate für Verwaltungspunkte installieren, um CPU-intensive Vorgänge eines Verwaltungspunkts zu verringern und die Verfügbarkeit dieser kritischen Standortsystemrolle zu steigern.  

 Da Sie an einem sekundären Standort, der sich auf dem sekundären Standortserver befinden muss, nur einen Verwaltungspunkt installieren können, wird die Konfiguration von Verwaltungspunkten an sekundären Standorten nicht als hoch verfügbar angesehen.  

> [!NOTE]  
>  Von der lokalen mobilen Geräteverwaltung verwaltete Geräte werden nur mit einem einzigen Verwaltungspunkt an einem primären Standort verbunden. Der Verwaltungspunkt wird dem mobilen Gerät von Configuration Manager während der Registrierung zugewiesen und danach nicht mehr geändert. Wenn Sie mehrere Verwaltungspunkte installieren und für mobile Geräte mehr als einen dieser Punkte aktivieren, ist der Verwaltungspunkt, der einem mobilen Geräteclient zugewiesen ist, nicht deterministisch.  
>   
>  Falls der von einem mobilen Geräteclient verwendete Verwaltungspunkt nicht mehr verfügbar ist, müssen Sie das Problem für diesen Verwaltungspunkt beheben. Sie können das mobile Gerät auch zurücksetzen und neu registrieren, damit es einem betriebsbereiten Verwaltungspunkt zugewiesen werden kann, der für mobile Geräte aktiviert ist.  

 **Verteilungspunkt:**  

 Installieren Sie mehrere Verteilungspunkte, und stellen Sie Inhalte für mehrere Verteilungspunkte bereit. Sie können überlappende Begrenzungsgruppen für Inhaltsorte konfigurieren und so sicherstellen, dass Clients auf den einzelnen Subnetzen von mehreren Verteilungspunkten aus Zugriff auf die Bereitstellung haben. Erwägen Sie schließlich, mindestens einen Verteilungspunkt als Fallbackpfad für Inhalt zu konfigurieren.  

 Weitere Informationen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 **Anwendungskatalog-Webdienstpunkt und Anwendungskatalog-Websitepunkt:**  

 Es können mehrere Instanzen dieser Standortsystemrollen installiert werden. Zur Leistungsoptimierung sollten Sie jeweils eine Instanz beider Rollen auf dem gleichen Standortsystemcomputer installieren.  

 Von jeder Standortsystemrolle für den Anwendungskatalog werden die gleichen Informationen wie von anderen Instanzen dieser Standortsystemrolle bereitgestellt, unabhängig davon, wo diese Standortsystemrolle sich in der Hierarchie befindet. Wenn von einem Client also eine Anforderung an den Anwendungskatalog gesendet wird und Sie für die Geräteclienteinstellung „Websitepunkt des Standardanwendungskatalogs“ die Option „Automatisch ermitteln“ konfiguriert haben, kann der Client an eine verfügbare Instanz weitergeleitet werden. Dabei wird, ausgehend vom aktuellen Netzwerkort des Clients, lokalen Standortsystemservern für den Anwendungskatalog Priorität eingeräumt.  

 Weitere Informationen zu dieser Clienteinstellung und zur automatischen Ermittlung finden Sie im Abschnitt zur [Computer-Agent](../../core/clients/deploy/about-client-settings.md#computer-agent) des Themas [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

##  <a name="bkmk_client"></a> Hohe Verfügbarkeit für Clients  
 **Autonomie von Clientvorgängen:**  

 In den folgenden Bereichen werden Configuration Manager-Clientvorgänge autonom ausgeführt:  

-   Für Clients ist keine ständige Verbindung mit bestimmten Standortsystemservern erforderlich. Von den Clients werden bekannte Konfigurationen verwendet, um vorkonfigurierte Aktionen nach einem Zeitplan auszuführen.  

-   Jede verfügbare Instanz einer Standortsystemrolle, von der Dienste für Clients bereitgestellt werden, kann von Clients verwendet werden. Von den Clients wird versucht, mit bekannten Servern eine Verbindung herzustellen, bis ein verfügbarer Server gefunden wird.  

-   Von Clients können Inventuren, Softwarebereitstellungen und ähnliche geplante Aktionen auch ohne direkte Verbindung mit Standortsystemservern ausgeführt werden.  

-   Von Clients, die zur Verwendung eines Fallbackstatuspunkts konfiguriert sind, können Details an den Fallbackstatuspunkt gesendet werden, wenn die Kommunikation mit einem Verwaltungspunkt nicht möglich ist.  

 **Clients können sich selbst reparieren:**  

 Die meisten typischen Probleme werden von Clients automatisch und ohne direkten Eingriff durch einen Administrator behoben:  

-   Der eigene Status wird von Clients regelmäßig bewertet. Standardprobleme werden ggf. unter Verwendung der lokal gespeicherten Wiederherstellungsschritte und Quelldateien behoben.  

-   Wenn von einem Client keine Statusinformationen an den ihm zugewiesenen Standort übermittelt werden, kann vom Standort eine Warnung ausgegeben werden. Administratoren, bei denen diese Warnungen eingehen, können sofort handeln, um den normalen Betrieb des Clients wiederherzustellen.  

 **Clients können Informationen zur späteren Verwendung zwischenspeichern:**  

 Bei der Kommunikation eines Clients mit einem Verwaltungspunkt können die folgenden Informationen vom Client abgerufen und zwischengespeichert werden:  

-   Clienteinstellungen  

-   Clientzeitpläne  

-   Informationen über Softwarebereitstellungen und einen Download der Software, die laut Zeitplan vom Client installiert werden soll, sofern die Bereitstellung für diese Aktion konfiguriert ist  

 Wenn ein Client einen Verwaltungspunkt nicht kontaktieren kann, werden der Status, der Zustand und die Clientinformationen, die dem Standort gemeldet werden, vom Client im lokalen Cache gespeichert. Diese Daten werden übertragen, sobald eine Verbindung mit einem Verwaltungspunkt zustande kommt.  

 **Übermittlung des Status an einen Fallbackstatuspunkt:**  

 Wenn Sie einen Client zur Verwendung eines Fallbackstatuspunkts konfigurieren, weisen Sie dem Client einen zusätzlichen Kontaktpunkt für die Übermittlung wichtiger Details zu seinen Vorgängen zu. Von Clients, die zur Verwendung eines Fallbackstatuspunkts konfiguriert sind, werden auch dann weiterhin Statusinformationen über ihre Vorgänge an diese Standortsystemrolle gesendet, wenn keine Verbindung mit einem Verwaltungspunkt hergestellt werden kann.  

 **Zentrale Verwaltung von Clientdaten und Clientidentität:**  

 Wichtige Informationen über die Identität eines Clients werden nicht jeweils vom Client selbst, sondern von der Standortdatenbank gespeichert und einem bestimmten Computer oder Benutzer zugeordnet. Dies bedeutet:  

-   Die Clientquelldateien auf einem Computer können ohne Auswirkungen auf die historischen Datensätze für den Computer mit dem installierten Client deinstalliert und erneut installiert werden.  

-   Fehler auf einem Clientcomputer wirken sich nicht auf die Integrität der in der Datenbank gespeicherten Informationen aus. Diese Informationen können für die Berichterstellung verfügbar bleiben.  

##  <a name="bkmk_nonHAoptions"></a> Optionen für Standorte und Standortsystemrollen ohne hohe Verfügbarkeit  
 Von einigen Standortsystemen wird nur eine Instanz an einem Standort oder in der Hierarchie unterstützt. Die Informationen können Ihnen bei der Vorbereitung auf das Offlineschalten dieser Standortsysteme helfen.  

 **Standortserver (Standort):**  

 Configuration Manager unterstützt die Installation des Standortservers für jeden Standort auf einem Windows Server-Cluster oder NLB-Cluster nicht.  

 Mithilfe der folgenden Informationen können Sie sich auf Probleme und Betriebsausfälle bei einem Standortserver vorbereiten:  

-   Verwenden Sie den integrierten Sicherungstask, um regelmäßig eine Sicherung des Standorts auszuführen. Üben Sie in Testumgebungen regelmäßig das Wiederherstellen von Standorten aus einer Sicherung.  

-   Stellen Sie in einer Hierarchie mit einem Standort der zentralen Verwaltung mehrere primäre Configuration Manager-Standorte bereit, um für Redundanz zu sorgen. Im Fall eines Standortausfalls können Sie Clients mithilfe von Windows-Gruppenrichtlinien oder Anmeldeskripts einem funktionsbereiten Standort zuweisen.  

-   In einer Hierarchie mit einem Standort der zentralen Verwaltung können Sie den Standort der zentralen Verwaltung oder einen untergeordneten primären Standort mithilfe der Option zum Wiederherstellen einer Standortdatenbank von einem anderen Standort in Ihrer Hierarchie wiederherstellen.  

-   Sekundäre Standorte können nicht wiederhergestellt werden und müssen neu installiert werden.  

 **Asset Intelligence-Synchronisierungspunkt (Hierarchie):**  

 Diese Standortsystemrolle wird als nicht unternehmenskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

-   Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

-   Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  

 **Endpoint Protection-Punkt (Hierarchie):**  

 Diese Standortsystemrolle wird als nicht unternehmenskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

-   Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

-   Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  

 **Anmeldungspunkt (Standort):**  

 Diese Standortsystemrolle wird als nicht unternehmenskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

-   Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

-   Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  

 **Anmeldungsproxypunkt (Standort):**  

 Diese Standortsystemrolle wird als nicht unternehmenskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Allerdings können Sie mehrere Instanzen dieser Standortsystemrolle auf einem Standort sowie auf mehreren Standorten in der Hierarchie installieren. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

-   Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

-   Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server.  

 Wenn Sie auf einem Standort über mehrere Anmeldungsproxypunkte verfügen, verwenden Sie für den Servernamen einen DNS-Alias. Wenn Sie diese Konfiguration verwenden, werden Benutzern beim Anmelden Ihrer mobilen Geräte mithilfe von DNS-Roundrobin Fehlertoleranz und Lastenausgleich zur Verfügung gestellt.  

 **Fallbackstatuspunkt (Standort oder Hierarchie):**  

 Diese Standortsystemrolle wird als nicht unternehmenskritisch betrachtet. Sie stellt optionale Funktionen in Configuration Manager bereit. Wenn dieses Standortsystem offline geschaltet wird, verwenden Sie eine der folgenden Optionen:  

-   Beseitigen Sie die Ursache für den Offlinezustand des Standortsystems.  

-   Deinstallieren Sie die Rolle vom aktuellen Server, und installieren Sie sie auf einem neuen Server. Da Clients der Fallbackstatuspunkt während der Clientinstallation zugewiesen wird, müssen Sie vorhandene Clients ändern, damit sie den neuen Standortsystemserver verwenden.  

### <a name="see-also"></a>Weitere Informationen:  
 [Unterstützte Konfigurationen für System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)
