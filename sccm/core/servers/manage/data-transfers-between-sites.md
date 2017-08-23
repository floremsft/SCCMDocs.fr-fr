---
title: "Datenübertragungen | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Configuration Manager Daten zwischen Standorten verschiebt, und wie Sie die Übertragung von Daten in Ihrem Netzwerk verwalten können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: "12"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bf0fdc8d4b4a72760b2cfb91231378a17df01594
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Datenübertragungen zwischen Standorten in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager verwendet die **dateibasierte Replikation** und die **Datenbankreplikation** zur Übertragung unterschiedlicher Informationsarten zwischen den Standorten. Erfahren Sie, wie Configuration Manager Daten zwischen Standorten verschiebt, und wie Sie die Übertragung von Daten in Ihrem Netzwerk verwalten können.  


## <a name="bkmk_fileroute"></a> File-based replication  
Mithilfe der dateibasierten Replikation werden dateibasierte Daten von Configuration Manager zwischen den Standorten in Ihrer Hierarchie übertragen. Zu diesen Daten gehören Anwendungen und Pakete, die Sie für Verteilungspunkte an untergeordneten Standorten bereitstellen möchten, sowie unverarbeitete Discovery Data Records (DDRs), die zur Verarbeitung an übergeordnete Standorte übertragen werden.  

Bei der dateibasierten Kommunikation zwischen Standorten wird das **Server Message Block**-Protokoll (SMB) über TCP/IP-Port 445 verwendet. Sie können Bandbreiteneinschränkungen und den Pulsmodus zur Steuerung der im Netzwerk übertragenen Datenmenge festlegen, und Sie können Zeitpläne angeben, um den Zeitpunkt der Datenübertragung im Netzwerk zu steuern.  

### <a name="bkmk_routes"></a> Dateireplikationsrouten  
Die folgenden Informationen unterstützen Sie beim Einrichten und Verwendung von Dateireplikationsrouten:  

#### <a name="file-replication-route"></a>Dateireplikationsroute

Von jeder Dateireplikationsroute wird ein Zielstandort identifiziert, an den dateibasierte Daten übertragen werden können. Von jedem Standort wird eine Dateireplikationsroute zu einem bestimmten Zielstandort unterstützt.  

Folgende Einstellungen können Sie für Dateinreplikationsrouten ändern:  

-  **Dateireplikationskonto**. Dieses Konto stellt eine Verbindung mit dem Zielstandort her und schreibt Daten in die **SMS_Site**-Freigabe dieses Standorts. Daten, die in diese Freigabe geschrieben werden, werden am Zielstandort verarbeitet. Wenn ein Standort der Hierarchie hinzugefügt wird, wird das Computerkonto des Standortservers am neuen Standort von Configuration Manager als Dateireplikationskonto dieses Standorts zugewiesen. Dieses Konto wird dann der Gruppe **SMS_SiteToSiteConnection_&lt;Standortcode\>** des Zielstandorts hinzugefügt. Bei dieser Gruppe handelt es sich um eine lokale Gruppe auf dem Computer, die den Zugriff auf die Freigabe „SMS_Site“ ermöglicht. Sie können dieses Konto in ein Windows-Benutzerkonto ändern. Wenn Sie das Konto ändern, achten Sie darauf, das neue Konto der Gruppe **SMS_SiteToSiteConnection_&lt;Standortcode\>** des Zielstandorts hinzuzufügen.  

    > [!NOTE]  
    >  An sekundären Standorten wird stets das Computerkonto des sekundären Standortservers als **Dateireplikationskonto**verwendet.  

-  **Zeitplan**. Sie können den Zeitplan für jede Dateireplikationsroute so festlegen, dass der Datentyp und der Zeitpunkt der Datenübertragung an den Zielstandort eingeschränkt werden.  
-  **Begrenzung der Datenübertragungsrate**. Sie können eine Begrenzung der Datenübertragungsrate für jede Dateireplikationsroute festlegen, um die bei der Datenübertragung an den Zielstandort in Anspruch genommene Netzwerkbandbreite zu steuern:  

    -  Verwenden Sie den **Pulsmodus** , um die Größe der Datenblöcke anzugeben, die an den Zielstandort gesendet werden. Sie können auch eine zeitliche Verzögerung zwischen dem Senden der einzelnen Datenblöcke angeben. Wählen Sie diese Option aus, wenn Sie Daten über Netzwerke mit sehr niedriger Bandbreite an den Zielstandort senden müssen. Dies kann beispielsweise der Fall sein, wenn eine Beschränkung vorliegt, dass unabhängig von der Geschwindigkeit der Verknüpfung oder deren Auslastung zu einem bestimmten Zeitpunkt nur alle fünf Sekunden 1 KB Daten gesendet werden dürfen und nicht alle drei Sekunden.
    -  Wählen Sie das Optionsfeld **Begrenzt auf angegebene maximale Übertragungsraten pro Stunde** aus, damit die Datenübertragung an den Zielstandort nur in dem von Ihnen angegebenen Zeitanteil erfolgt. Wenn Sie diese Option verwenden, ermittelt Configuration Manager nicht die verfügbare Netzwerkbandbreite. Stattdessen wird die Zeit, innerhalb derer Daten gesendet werden können, in Blöcke aufgeteilt. Die Daten werden dann innerhalb eines kurzen Zeitblocks gesendet. In den darauffolgenden Zeitblöcken werden keine Daten gesendet. Wenn die Höchstrate beispielsweise auf **50 %**festgelegt ist, überträgt Configuration Manager die Daten für eine bestimmte Dauer, und für eine ebenso lange Dauer werden anschließend keine Daten übertragen. Die tatsächliche Datenmenge bzw. die Größe der Datenblöcke wird nicht verwaltet. Stattdessen wird nur die Dauer der Datenübertragung verwaltet.  

        > [!CAUTION]  
        > Von einem Standort können standardmäßig bis zu 3 **gleichzeitige Sendevorgänge** zur Datenübertragung an einen Zielstandort verwendet werden. Wenn Sie für eine Dateireplikationsroute die Begrenzung der Datenübertragungsrate aktivieren, ist die Anzahl **gleichzeitiger Sendevorgänge** an den entsprechenden Standort auf 1 begrenzt. Dies gilt auch dann, wenn für die Option **Verfügbare Bandbreite beschränken (%)** der Wert **100 %**festgelegt ist. Wenn Sie beispielsweise für den Sender die Standardeinstellungen verwenden, wird hierdurch die Übertragungsrate an den Zielstandort auf ein Drittel der Standardkapazität reduziert.  

-  Sie können eine Dateireplikationsroute zwischen zwei sekundären Standorten zum Weiterleiten dateibasierten Inhalts zwischen diesen Standorten konfigurieren.  

Zur Verwaltung einer Dateireplikationsroute erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Hierarchiekonfiguration** und wählen **Dateireplikation** aus.  

#### <a name="sender"></a>Sender

An jedem Standort ist ein Sender verfügbar. Von diesem Sender wird die Netzwerkverbindung von einem Standort zu einem Zielstandort verwaltet. Der Sender kann auch verwendet werden, um Verbindungen zu mehreren Standorten gleichzeitig herzustellen. Zum Herstellen einer Verbindung mit einem Standort wird vom Sender mithilfe der Dateireplikationsroute zum Standort das Konto identifiziert, über das die Verbindungsherstellung erfolgt. Dieses Konto wird vom Sender auch dazu verwendet, Daten in die „SMS_Site“-Freigabe des Zielstandorts zu schreiben.  

Vom Sender werden Daten standardmäßig mithilfe von gleichzeitigen Sendevorgängen, die in der Regel als **Thread**bezeichnet werden, in den Zielstandort geschrieben. Von jedem gleichzeitigen Sendevorgang oder Thread kann ein anderes dateibasiertes Objekt an den Zielstandort übertragen werden. Nachdem der Sendevorgang für ein Objekt gestartet wurde, werden vom Sender standardmäßig so lange Datenblöcke für dieses Objekt geschrieben, bis die Übertragung des gesamten Objekts abgeschlossen ist. Anschließend kann der Sendevorgang oder Thread für ein weiteres Objekt gestartet werden.  

Sie können die folgenden Einstellungen für einen Sender ändern:  

-  **Maximale Anzahl gleichzeitiger Sendevorgänge**. Standardmäßig verwendet jeder Standort fünf gleichzeitige Sendevorgänge, wobei drei dieser Sendevorgänge zur Datenübertragung an einen beliebigen Zielstandort verfügbar sind. Wenn Sie diese Anzahl erhöhen, nimmt der Datendurchsatz zwischen Standorten zu, da von Configuration Manager mehr Dateien gleichzeitig übertragen werden können. Die Erhöhung dieser Anzahl bedeutet auch höhere Anforderungen an die Netzwerkbandbreite zwischen Standorten.  

-  **Wiederholungseinstellungen**. Standardmäßig wiederholt jeder Standort die Herstellung einer problematischen Verbindung zweimal im Abstand von einer Minute. Sie können sowohl die Anzahl der Verbindungsversuche als auch deren Abstand ändern.  

Zur Verwaltung des Senders eines Standorts erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Standortkonfiguration**. Erweitern Sie dann den Knoten **Standorte**, und wählen Sie die **Eigenschaften** des zu verwaltenden Standorts aus. Wählen Sie die Registerkarte **Sender**, um die Sendereinstellungen zu ändern.  

## <a name="bkmk_dbrep"></a> Database replication  
SQL Server wird von der Configuration Manager-Datenbankreplikation dazu verwendet, Daten zu übertragen und an Standortdatenbanken ausgeführte Änderungen mit den Informationen in den Datenbanken anderer Standorte in der Hierarchie zusammenzuführen. Bitte beachten Sie bei der Datenbankreplikation Folgendes:

-  Alle Standorte verfügen über die gleichen Informationen.  
-  Wenn Sie einen Standort in einer Hierarchie installieren, wird automatisch eine Datenbankreplikation zwischen dem neuen Standort und dem vorgesehenen übergeordneten Standort hergestellt.  
-  Nach Abschluss der Standortinstallation wird die Datenbankreplikation automatisch gestartet.  

Wenn Sie einer Hierarchie einen neuen Standort hinzufügen, wird an diesem neuen Standort eine generische Datenbank von Configuration Manager erstellt. Anschließend wird eine Momentaufnahme der relevanten Daten in der Datenbank des übergeordneten Standorts erstellt und anschließend mithilfe dateibasierter Replikation an den neuen Standort übertragen. Mithilfe von BCP, eines Massenkopierprogramms für SQL Server, werden die Informationen dann in die lokale Kopie der Configuration Manager-Datenbank am neuen Standort geladen. Nach dem Laden des Snapshots wird an jedem Standort eine Datenbankreplikation mit dem anderen Standort ausgeführt.  

Daten werden von Configuration Manager mithilfe eines Datenbankreplikationsdienstes zwischen Standorten repliziert. Hierbei kommen die Änderungsnachverfolgung von SQL Server, mit der die lokale Standortdatenbank auf Änderungen hin überwacht wird, und ein SQL Server Service Broker (SSB), mit dem alle Änderungen auf andere Standorte repliziert werden, zum Einsatz. Für diesen Prozess wird standardmäßig TCP/IP-Port 4022 verwendet.  

Daten, die mithilfe der Datenbankreplikation repliziert werden, werden von Configuration Manager in verschiedene Replikationsgruppen unterteilt. Bitte beachten Sie bei Replikationsgruppen Folgendes:

-  Für jede Replikationsgruppe gibt es einen separaten, festen Replikationszeitplan, aus dem hervorgeht, wie häufig Änderungen an den Daten in der Gruppe an andere Standorte repliziert werden.  

     Beispielsweise wird eine Änderung an der rollenbasierten Verwaltung rasch auf andere Standorte repliziert, um zu gewährleisten, dass diese Änderung so schnell wie möglich erzwungen wird. Währenddessen wird eine Konfigurationsänderung mit niedrigerer Priorität, wie etwa die Installation eines neuen sekundären Standorts, mit geringerer Dringlichkeit repliziert. Es kann einige Minuten in Anspruch nehmen, bis eine neue Standortanfrage den primären Zielort erreicht hat.  

-   Sie können folgende Einstellungen für die Datenbankreplikation ändern:  

    -  **Datenbankreplikationslinks**. Steuern, wann bestimmter Datenverkehr das Netzwerk durchläuft.  
    -  **Verteilte Ansichten**. Nehmen Änderungen an Einstellungen für Replikationslinks vor, mithilfe derer Anfragen, die am Standort der zentralen Verwaltung für ausgewählte Standortdaten gestellt wurden, direkt von der Datenbank eines untergeordneten primären Standorts auf diese Standortdaten zugreifen können.  
    -  **Zeitpläne**. Legen den Zeitpunkt der Verwendung eines Replikationslink fest und wann verschiedene Arten von Standortdaten repliziert werden.  
    -  **Zusammenfassung**. Nehmen Änderungen an Einstellungen für die Datenzusammenfassung vor, die den Netzwerkverkehr betrifft, der die Replikationslinks durchläuft. Die Zusammenfassung wird standardmäßig alle 15 Minuten vorgenommen, und sie wird in Datenreplikationsberichten verwendet.  
    -  **Schwellenwerte für die Datenbankreplikation**. Definieren, wann Links als heruntergestuft oder fehlgeschlagen gemeldet werden. Sie können auch festlegen, wann von Configuration Manager Warnungen zu Replikationslinks mit dem heruntergestuften oder fehlerhaften Status ausgelöst werden.  

Configuration Manager klassifiziert die Daten, die repliziert werden, entweder als **globale Daten** oder als **Standortdaten** über die Datenbankreplikation. Im Rahmen der Datenbankreplikation werden Änderungen an globalen Daten und Standortdaten über den Datenbankreplikationslink übertragen. Globale Daten können auf einen über- oder untergeordneten Standort repliziert werden. Standortdaten können nur auf übergeordnete Standorte repliziert werden. Die sogenannten lokalen Daten als dritter Datentyp werden nicht auf andere Standorte repliziert. Lokale Daten sind Informationen, die für andere Standorte nicht erforderlich sind. Bitte beachten Sie bei den Datentypen Folgendes:  

-  **Globale Daten**. Als globale Daten werden Objekte bezeichnet, die von Administratoren erstellt wurden und die an alle Standorte innerhalb der Hierarchie repliziert werden, wobei sekundäre Standorte nur eine Untergruppe globaler Daten wie beispielsweise globale Proxydaten erhalten. Zu den globalen Daten werden Softwarebereitstellungen, Softwareupdates, Sammlungsdefinitionen und rollenbasierte Verwaltungssicherheitsbereiche gezählt. Administratoren können globale Daten an Standorten der zentralen Verwaltung und an primären Standorten erstellen.  
-  **Standortdaten**. Als Standortdaten werden Betriebsinformationen bezeichnet, die von primären Configuration Manager-Standorten und den Clients, die primären Standorten unterstellt sind, erstellt werden. Standortdaten werden am Standort der zentralen Verwaltung repliziert, jedoch nicht an anderen Standorten. Zu den Standortdaten werden beispielsweise Hardwareinventurdaten, Statusmeldungen, Warnungen und die Ergebnisse von abfragebasierten Sammlungen gezählt. Standortdaten können nur am Standort der zentralen Verwaltung und an dem primären Standort, von dem sie stammen, angezeigt werden. Standardortdaten können nur an dem primären Standort geändert werden, an dem sie erstellt wurden.  

     Alle Standortdaten werden am Standort der zentralen Verwaltung repliziert. Der Standort der zentralen Verwaltung führt die Verwaltung und Berichterstattung für die gesamte Standorthierarchie durch.  

In den folgenden Abschnitten sind Einstellungen beschrieben, die Sie zum Verwalten der Datenbankreplikation ändern können.  

### <a name="bkmk_Dblinks"></a> Datenbankreplikationslinks  
Wenn Sie in einer Hierarchie einen neuen Standort installieren, wird von Configuration Manager ein Datenbankreplikationslink zwischen dem übergeordneten und neuen Standort erstellt. Für die Verbindung der beiden Standorte wird ein einzelner Link erstellt.  

Sie können die Einstellungen jedes Datenbankreplikationslinks ändern, um die Datenübertragung über den Replikationslink zu steuern. Von jedem Replikationslink werden separate Konfigurationen unterstützt. Die Steuerelemente für Datenbankreplikationslinks umfassen Folgendes:  

-  Beenden die Replikation ausgewählter Standortdaten von einem primären Standort zum Standort der zentralen Verwaltung, damit der Standort der zentralen Verwaltung direkt auf diese Daten in der Datenbank des primären Standorts zugreifen kann.  
-  Festlegen des Zeitpunkts der Übertragung ausgewählter Standortdaten von einem untergeordneten primären Standort zum Standort der zentralen Verwaltung.
-  Definition, wann sich ein Datenbankreplikationslink im Status „Heruntergestuft“ oder „Fehler“ befindet.
-  Angeben, wann Warnungen zu einem fehlgeschlagenen Replikationslink ausgelöst werden sollen.
-  Geben Sie an, wie häufig Daten zum Replikationsverkehr, der über den Replikationslink abgewickelt wird, von Configuration Manager zusammengefasst werden. Diese Daten werden in Berichten verwendet.

Zum Konfigurieren eines Datenbankreplikationslinks müssen Sie die Eigenschaften des Links in der Configuration Manager-Konsole im Knoten **Datenbankreplikation** bearbeiten. Dieser Knoten wird sowohl im Arbeitsbereich **Überwachung** als auch unter dem Knoten **Hierarchiekonfiguration** des Arbeitsbereichs **Verwaltung** angezeigt. Sie können einen Replikationslink entweder am übergeordneten Standort oder am untergeordneten Standort des Replikationslinks bearbeiten.  

> [!TIP]  
> Sie können Datenbankreplikationslinks über den Knoten **Datenbankreplikation** in beiden Arbeitsbereichen bearbeiten. Wenn Sie aber den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** verwenden, können Sie auch den Status der Datenbankreplikation für Replikationslinks anzeigen. Außerdem haben Sie Zugriff auf die Replikationslinkanalyse, mit der Sie Probleme bei der Datenbankreplikation untersuchen können.  

Informationen zum Konfigurieren von Replikationslinks finden Sie unter [Steuerelemente für die Replikation von Standortdatenbanken](#BKMK_DBRepControls). Weitere Informationen zur Überwachung der Replikation finden Sie unter [Überwachen der Datenbankreplikationslinks und des Replikationsstatus](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) im Thema [Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Verwenden Sie die Informationen in den folgenden Abschnitten, um Datenbankreplikationslinks zu planen.  

### <a name="bkmk_distviews"></a> Verteilte Ansichten  
Durch das Verwendung verteilter Ansichten können Anfragen am Standort der zentralen Verwaltung direkt auf ausgewählte Standortdaten in der Datenbank eines untergeordneten primären Standorts zugreifen. Da ein direkter Zugriff gewährt wird, ist es nicht mehr erforderlich, diese Standortdaten vom primären Standort an den Standort der zentralen Verwaltung zu replizieren. Sie können verteilte Ansichten nur auf den von Ihnen ausgewählten Replikationslinks verwenden, da Replikationslinks voneinander unabhängig sind. Sie können verteilte Ansichten nicht zwischen einem primären und einem sekundären Standort verwenden.  

Aus verteilten Ansichten ergeben sich die folgenden Vorteile:  

-  Verringerung der CPU-Last bei der Verarbeitung von Datenbankänderungen am Standort der zentralen Verwaltung und an primären Standorten
-  Verringerung der Datenmengen, die über das Netzwerk an den Standort der zentralen Verwaltung übertragen werden
-  Verbesserung der Leistung der SQL Server-Instanz, auf dem die Datenbank des Standorts der zentralen Verwaltung gehostet wird
-  Verringerung des Speicherplatzes, der von der Datenbank am Standort der zentralen Verwaltung in Anspruch genommen wird

Die Verwendung verteilter Ansichten bietet sich an, wenn sich ein primärer Standort im Netzwerk in der Nähe des Standorts der zentralen Verwaltung befindet und beide Standorte stets aktiviert und verbunden sind. Der Grund hierfür ist, dass die Replikation ausgewählter Daten zwischen den Standorten dank der verteilten Ansichten durch direkte Verbindungen zwischen den SQL Server-Instanzen an beiden Standorten ersetzt wird. Eine direkte Verbindung wird jedes Mal hergestellt, wenn diese Daten am Standort der zentralen Verwaltung angefordert werden. Daten, die Sie für verteilte Ansichten aktivieren, werden in der Regel angefordert, wenn Sie Berichte oder Abfragen ausführen bzw. Informationen im Ressourcen-Explorer anzeigen. Daten werden auch bei der Auswertung von Sammlungen angefordert, die auf den Standortdaten beruhende Regeln umfassen.  

Verteilte Ansichten sind standardmäßig für alle Replikationslinks deaktiviert. Wenn Sie verteilte Ansicht für einen Replikationslink aktivieren, wählen Sie die Standortdaten aus, die nicht über diesen Link auf den Standort der zentralen Verwaltung repliziert werden. Der Zugriff auf diese Daten in der Datenbank des primären Standorts erfolgt direkt von der Datenbank des untergeordneten primären Standorts aus, der den Link freigibt. Sie können die folgenden Arten von Standortdaten für verteilte Ansichten konfigurieren:  

-  Hardwareinventurdaten von Clients
-  Softwareinventurdaten und Softwaremessungsdaten von Clients
-  Statusmeldungen von Clients, vom primären Standort und von allen sekundären Standorten

Verteilte Ansichten sind für Administratoren, die Daten in der Configuration Manager-Konsole oder in Berichten anzeigen, nicht sichtbar. Wenn Daten angefordert werden, die für verteilte Ansichten aktiviert sind, wird von der SQL Server-Instanz, auf der die Datenbank für den Standort der zentralen Verwaltung gehostet wird, direkt auf die SQL Server-Instanz am untergeordneten primären Standort zugegriffen, um die gewünschten Informationen abzurufen. Angenommen, Sie fordern am Standort der zentralen Verwaltung über eine Configuration Manager-Konsole Hardwareinventurinformationen von zwei Standorten an, und nur an einem der Standorte ist die Hardwareinventur für eine verteilte Ansicht aktiviert. Die Inventurinformationen für Clients an dem Standort, der nicht für verteilte Ansichten konfiguriert ist, werden aus der Datenbank am Standort der zentralen Verwaltung abgerufen. Die Inventurinformationen für Clients an dem Standort, der für verteilte Ansichten konfiguriert ist, werden aus der Datenbank am untergeordneten primären Standort abgerufen. Diese Informationen werden in der Configuration Manager-Konsole bzw. in einem Bericht ohne Hinweise auf die Quelle angezeigt.  

Solange bei einem Replikationslink ein Datentyp für verteilte Ansichten aktiviert ist, werden diese Daten nicht vom untergeordneten primären Standort auf den Standort der zentralen Verwaltung repliziert. Sobald verteilte Ansichten für einen Datentyp deaktiviert werden, wird die Replikation dieser Daten vom untergeordneten primären Standort auf den Standort der zentralen Verwaltung im Rahmen der normalen Datenreplikation wiederaufgenommen. Allerdings müssen die Replikationsgruppen, die diese Daten enthalten, zwischen dem primären Standort und dem Standort der zentralen Verwaltung neu initialisiert werden, damit diese Daten am Standort der zentralen Verwaltung verfügbar sind. Nach der Deinstallation eines primären Standorts mit aktivierten verteilten Ansichten müssen die Daten des Standorts der zentralen Verwaltung neu initialisiert werden, damit Sie auf Daten zugreifen können, die am Standort der zentralen Verwaltung für verteilte Ansichten aktiviert waren.  

> [!IMPORTANT]  
> Wenn Sie verteilte Ansichten auf einem Replikationslink in der Hierarchie verwenden, müssen Sie die verteilten Ansichten aller Replikationslinks deaktivieren, bevor Sie einen primären Standort deinstallieren. Weitere Informationen finden Sie unter [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Voraussetzungen und Einschränkungen für verteilte Ansichten  

-  Sie können verteilte Ansichten nur auf Replikationslinks zwischen einem Standort der zentralen Verwaltung und einem primären Standort verwenden.
- Der Standort der zentralen Verwaltung muss eine Enterprise Edition von SQL Server verwenden. Der primäre Standort verfügt nicht über diese Anforderung.
-  Am Standort der zentralen Verwaltung darf nur eine Instanz des SMS-Anbieters installiert sein, und diese Instanz muss sich auf dem Standortdatenbankserver befinden. Dies ist zur Unterstützung der Kerberos-Authentifizierung erforderlich, damit der SQL Server am Standort der zentralen Verwaltung auf den SQL Server am untergeordneten primären Standort zugreifen kann. Für den SMS-Anbieter am untergeordneten primären Standort gelten keine Einschränkungen.
-  Am Standort der zentralen Verwaltung darf nur ein SQL Server Reporting Services-Punkt installiert sein, und dieser Punkt muss sich auf dem Standortdatenbankserver befinden. Dies ist zur Unterstützung der Kerberos-Authentifizierung erforderlich, durch die es dem SQL Server am Standort der zentralen Verwaltung ermöglicht wird, auf den SQL Server am untergeordneten primären Standort zuzugreifen.
-  Die Standortdatenbank darf nicht auf einem SQL Server-Cluster gehostet werden.
-  Die Standortdatenbank darf nicht auf einer SQL Server-Always On-Verfügbarkeitsgruppe gehostet werden.
-  Für das Computerkonto des Datenbankservers am Standort der zentralen Verwaltung sind Leseberechtigungen für die Standortdatenbank des primären Standorts erforderlich.

> [!IMPORTANT]  
>  Bei einem Datenbankreplikationslink schließen verteilte Ansichten und Zeitpläne für die Datenreplikation einander aus.  

### <a name="BKMK_schedules"></a> Geplante Übertragung von Standortdaten auf Datenbankreplikationslinks  
Sie können einen Zeitplan aufstellen, aus dem hervorgeht, wann ein Replikationslink verwendet wird und wann verschiedene Arten von Standortdaten repliziert werden. Auf diese Weise können Sie die Netzwerkbandbreite steuern, die beim Replizieren von Standortdaten von einem untergeordneten primären Standort an den entsprechenden Standort der zentralen Verwaltung in Anspruch genommen wird. Sie können festlegen, wann Statusmeldungen, Inventurdaten und Messungsdaten vom primären Standort repliziert werden. Zeitpläne für Standortdaten werden von Datenbankreplikationslinks sekundärer Standorte nicht unterstützt. Für die Übertragung globaler Daten kann kein Zeitplan festgelegt werden.  

Beim Festlegen eines Zeitplans für einen Datenbankreplikationslink können Sie die Übertragung ausgewählter Standortdaten vom primären Standort zum Standort der zentralen Verwaltung einschränken und unterschiedliche Zeiten für die Replikation unterschiedlicher Arten von Standortdaten konfigurieren.  

> [!IMPORTANT]  
> Bei einem Datenbankreplikationslink schließen verteilte Ansichten und Zeitpläne für die Datenreplikation einander aus.  

### <a name="BKMK_SummarizeDBReplication"></a> Zusammenfassung des Datenbankreplikationsverkehrs  
Daten zum Netzwerkverkehr, der über die Datenbankreplikationslinks der Standorte abgewickelt wird, werden von jedem Standort regelmäßig zusammengefasst. Zusammengefasste Daten fließen in Berichte über die Datenbankreplikation ein. Der der über einen Replikationslink abgewickelte Netzwerkverkehr wird von beiden Standorten des Replikationslinks zusammengefasst. Die Datenzusammenfassung wird vom SQL Server ausgeführt, auf dem die Standortdatenbank gehostet wird. Nach der Datenzusammenfassung werden die Informationen als globale Daten an andere Standorte repliziert.  

Die Zusammenfassung erfolgt standardmäßig alle 15 Minuten. Sie können die Häufigkeit, mit der der Netzwerkverkehr zusammengefasst wird, ändern. Bearbeiten Sie dazu das **Zusammenfassungsintervall** in den Eigenschaften des Datenbankreplikationslinks. Die Häufigkeit der Zusammenfassung wirkt sich auf die Informationen aus, die Sie in Berichten über die Datenbankreplikation sehen. Sie können das Intervall auf einen Länge von 5 bis 60 Minuten festlegen. Wenn Sie die Häufigkeit der Zusammenfassung erhöhen, steigern Sie die Verarbeitungslast des SQL Servers an jedem Standort des Replikationslinks.  

### <a name="BKMK_DBRepThresholds"></a> Schwellenwerte für die Datenbankreplikation  
Mit Schwellenwerten für die Datenbankreplikation wird bestimmt, wann ein Datenbankreplikationslink als heruntergestuft oder fehlerhaft gemeldet wird. Ein Link wird standardmäßig auf den Status „heruntergestuft“ festgelegt, wenn eine Replikationsgruppe die Replikation zwölf Mal hintereinander nicht abschließen kann. Der Link wird auf den Status „fehlerhaft“ festgelegt, wenn eine Replikationsgruppe die Replikation 24 Mal hintereinander nicht abschließen kann.  

Sie können durch benutzerdefinierte Werte bestimmen, wann ein Replikationslink von Configuration Manager als heruntergestuft oder fehlerhaft gemeldet wird. Durch Festlegen des Zeitpunkts, zu dem der Status der einzelnen Datenreplikationslinks von Configuration Manager gemeldet wird, können Sie die Integrität der Datenbankreplikation über diese Links genauer überwachen.  

Es kann vorkommen, dass einige Replikationsgruppen nicht repliziert werden können, während die Replikation anderer Replikationsgruppen weiterhin erfolgreich ist. Planen Sie daher, den Replikationsstatus eines Replikationslinks zu prüfen, wenn er zum ersten Mal als „heruntergestuft“ gemeldet wird. Wenn bei bestimmten Replikationsgruppen wiederholt Verzögerungen auftreten, die kein Problem darstellen, oder wenn für die Netzwerkverbindung zwischen Standorten nur eine geringe Bandbreite verfügbar ist, erwägen Sie, den Wiederholungswert für den heruntergestuften oder fehlerhaften Status des Links zu ändern. Wenn Sie die Anzahl der Wiederholungen erhöhen, nach denen der Link als heruntergestuft oder fehlerhaft gilt, können Sie falsche Warnungen für bekannte Probleme verhindern und den Linkstatus genauer nachverfolgen.  

Sie sollten auch das Synchronisierungsintervall jeder Replikationsgruppe in Betracht ziehen, um zu verstehen, wie häufig diese Gruppe repliziert wird. Um das **Synchronisierungsintervall** für Replikationsgruppen anzuzeigen, wählen Sie im Arbeitsbereich **Überwachung** im Knoten **Datenbankreplikation** die Registerkarte **Replikationsdetails** eines Replikationslinks aus.  

Weitere Informationen zur Überwachung der Replikation, wie etwa die Ansicht des Replikationsstatus, finden Sie unter [Überwachen der Datenbankreplikationslinks und des Replikationsstatus](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) im Thema [Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Informationen zum Konfigurieren von Schwellenwerten für die Datenbankreplikation finden Sie unter [Steuerelemente für die Replikation von Standortdatenbanken](#BKMK_DBRepControls).  

## <a name="BKMK_DBRepControls"></a> Steuerelemente für die Replikation von Standortdatenbanken  
Sie können die Einstellung jeder Datenbank ändern, damit Sie die für die Datenbankreplikation verwendete Netzwerkbandbreite steuern können. Die Einstellungen gelten nur für die Standortdatenbank, in der Sie die Einstellungen konfigurieren. Die Einstellungen kommen immer dann zur Anwendung, wenn der Standort beliebige Daten mithilfe von Datenbankreplikation auf jeden anderen Standort repliziert.  

Folgende Steuerelemente können Sie für jede Datenbank modifizieren:  

-  Den SSB-Port ändern.  
-  Konfigurieren Sie den Zeitraum, nach dessen Ablauf der Standort aufgrund von Replikationsfehlern dazu veranlasst wird, seine Kopie der Standortdatenbank neu zu konfigurieren.  
-  Konfigurieren Sie eine Standortdatenbank so, dass die von ihr bei der Datenbankreplikation replizierten Daten komprimiert werden. Die Daten werden nur für die Übertragung zwischen Standorten komprimiert, nicht aber für die Speicherung in den Standortdatenbanken der Standorte.  

Zum Ändern der Einstellungen der Replikationssteuerelemente für eine Standortdatenbank müssen Sie die Eigenschaften der Standortdatenbank in der Configuration Manager-Konsole über den Knoten **Datenbankreplikation** bearbeiten. Dieser Knoten befindet sich unter dem Knoten **Hierarchiekonfiguration** der Arbeitsbereiche **Verwaltung** und **Überwachung**. Zur Bearbeitung der Eigenschaften der Standortdatenbank wählen Sie den Replikationslink zwischen den Standorten aus und öffnen dann entweder **Eigenschaften der übergeordneten Datenbank** oder **Eigenschaften der untergeordneten Datenbank**.  

> [!TIP]  
> In beiden Arbeitsbereichen können Sie Steuerelemente für die Datenbankreplikation über den Knoten **Datenbankreplikation** konfigurieren. Wenn Sie aber den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** verwenden, können Sie auch den Status der Datenbankreplikation für einen Replikationslink anzeigen. Außerdem haben Sie Zugriff auf die Replikationslinkanalyse, mit der Sie Probleme bei der Replikation untersuchen können.  
