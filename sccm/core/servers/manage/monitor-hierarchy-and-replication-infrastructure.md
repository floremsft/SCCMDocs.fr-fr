---
title: "Überwachen der Replikation | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie Infrastruktur und Vorgänge in Configuration Manager durch Verwendung des Arbeitsbereichs „Überwachung“ in der Konsole überwachen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fab4d67-8d2a-45ce-8b06-471280102cf6
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 132803a1aa9aad5c5462686bd656688418e47d07
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-hierarchy-and-replication-infrastructure-in-system-center-configuration-manager"></a>Überwachen der Hierarchie- und Replikationsinfrastruktur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie zum Überwachen von Infrastruktur und Vorgängen in System Center Configuration Manager den Arbeitsbereich **Überwachung** in der Configuration Manager-Konsole.  

> [!NOTE]  
>  Eine Ausnahme gilt für die Migration, die direkt im Knoten **Migration** im Arbeitsbereich **Verwaltung** überwacht wird. Weitere Informationen finden Sie unter [Operations for migrating to System Center Configuration Manager](../../../core/migration/operations-for-migration.md).  

 Zusätzlich zur Configuration Manager-Konsole können Sie zur Überwachung auch Configuration Manager-Berichte verwenden oder Configuration Manager-Protokolldateien für Configuration Manager-Komponenten anzeigen. Informationen zu Berichten finden Sie unter [Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/reporting.md). Informationen zu Protokolldateien finden Sie unter [Protokolldateien in System Center Configuration Manager](../../../core/plan-design/hierarchy/log-files.md).  

 Achten Sie beim Überwachen von Standorten auf Anzeichen für Probleme, die Ihren Eingriff erfordern. Beispiel:  

-   Dateirückstand auf Standortservern und Standortsystemen  

-   Statusmeldungen, die auf einen Fehler oder ein Problem hinweisen  

-   Fehlerhafte standortinterne Kommunikation  

-   Fehler- und Warnmeldungen im Systemereignisprotokoll auf Servern  

-   Fehler- und Warnmeldungen im Fehlerprotokoll von Microsoft SQL Server  

-   Standorte oder Clients, die über einen längeren Zeitraum nichts berichtet haben  

-   Lange Antwortzeiten der SQL Server-Datenbank  

-   Anzeichen für Hardwareausfälle  

Wenn Überwachungstasks Anzeichen für Probleme finden, sollten Sie die Ursache des betreffenden Problems untersuchen und es so schnell wie möglich beheben. Auf diese Weise minimieren Sie das Risiko eines Standortausfalls.  



##  <a name="BKMK_MonintorMgmtTasks"></a> Überwachen allgemeiner Verwaltungstasks für Configuration Manager  
 Configuration Manager bietet integrierte Überwachungsfunktionen in der Configuration Manager-Konsole. Sie können zahlreiche Tasks überwachen, darunter Tasks im Zusammenhang mit Softwareupdates, Energieverwaltung und Bereitstellung von Inhalten in der gesamten Hierarchie.  

 Verwenden Sie die folgenden Informationen, um allgemeine Configuration Manager-Tasks zu überwachen:  

 **Warnungen**  
   Siehe [Überwachen von Warnungen](../../../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorAlerts) unter [Verwenden von Benachrichtigungen und des Statussystems für System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Kompatibilitätseinstellungen**  
   Informationen finden Sie unter [Überwachen von Kompatibilitätseinstellungen in System Center Configuration Manager](../../../compliance/deploy-use/monitor-compliance-settings.md)  

 **Bereitstellung von Inhalten**  
   Allgemeine Informationen zur Überwachung von Inhalt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

Informationen zum Überwachen bestimmter Typen von Bereitstellungsinhalten:
-   Informationen zum Überwachen von Anwendungen finden Sie unter [Überwachen von Anwendungen mit System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

-   Zum Überwachen von Paketen und Programmen gehen Sie zu „Verwalten von Paketen und Programmen“ im Thema [Pakete und Programme in System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

**Endpoint Protection**  
   Informationen finden Sie unter [Überwachen von Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

**Überwachen der Energieverwaltung**  
 Informationen finden Sie unter [Überwachen und Planen der Energieverwaltung in System Center Configuration Manager](../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

**Überwachen der Softwaremessung**  
Informationen finden Sie unter [Überwachen der App-Nutzung mit der Softwaremessung in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

**Überwachen von Softwareupdates**  
 Weitere Informationen finden Sie unter [Überwachen von Softwareupdates in System Center Configuration Manager](../../../sum/deploy-use/monitor-software-updates.md).  


##  <a name="BKMK_MonitorInfrastructure"></a> Überwachen der Hierarchieinfrastruktur für Configuration Manager  
Configuration Manager bietet mehrere Methoden zum Überwachen von Status und Vorgängen in Ihrer Hierarchie. Sie können den Systemstatus von Standorten hierarchieweit überprüfen, die Replikation zwischen Standorten anhand von Standorthierarchie- oder geografischen Ansichten überwachen, Replikationslinks zwischen Standorten zur Datenbankreplikation überwachen und das Replikationslinkanalyse-Tool verwenden, um Replikationsprobleme zu beheben.  

###  <a name="BKMK_SH_Node"></a> Informationen zum Knoten "Standorthierarchie"  
Im Knoten **Standorthierarchie** des Arbeitsbereichs **Überwachung** finden Sie eine Übersicht Ihrer Configuration Manager-Hierarchie sowie Links zwischen Standorten. Sie können zwei Ansichten verwenden:  

-   **Hierarchiediagramm**: In dieser Ansicht wird Ihre Hierarchie als Topologiezuordnung angezeigt, die so vereinfacht wurde, dass nur wichtige Informationen dargestellt werden.  

-   **Geografische Ansicht**: In dieser Ansicht werden Ihre Standorte in einer geografischen Zuordnung angezeigt. Dabei werden die geografischen Orte der von Ihnen konfigurierten Standorte dargestellt.  

Verwenden Sie den Knoten **Standorthierarchie** , um die Integrität jedes Standorts, die Replikationslinks zwischen Standorten sowie deren Beziehungen zu externen Faktoren wie einem geografischen Standort zu überwachen.  

Wenn Sie Ihre Configuration Manager-Konsole mit einem untergeordneten primären Standort verbinden, können Sie den Standort- oder Linkstatus weder von anderen primären Standorten noch von deren untergeordneten sekundären Standorten anzeigen. Dies ist darauf zurückzuführen, dass der Standortstatus und der Status von Links zwischen Standorten als Standortdaten und nicht als globale Daten repliziert werden. Wenn Sie beispielsweise in einer Hierarchie mit mehreren primären Standorten Ihre Configuration Manager-Konsole mit einem primären Standort verbinden, können Sie den Status von untergeordneten sekundären Standorten, vom primären Standort sowie vom Standort der zentralen Verwaltung anzeigen. Den Status von anderen Knoten der Hierarchie unterhalb des Standorts der zentralen Verwaltung können Sie jedoch nicht anzeigen.  

 Verwenden Sie den Befehl **Einstellungen konfigurieren** , um zu steuern, wie die Anzeige der Standorthierarchie gerendert wird. Konfigurationen, die Sie an der **Standorthierarchie** ausführen, wenn Ihre Configuration Manager-Konsole mit einem Standort verbunden ist, werden an allen anderen Standorten repliziert.  

#### <a name="hierarchy-diagram"></a>Hierarchiediagramm  
 Im Hierarchiediagramm werden Ihre Standorte als Topologiezuordnung dargestellt. Sie können in dieser Ansicht einen Standort auswählen, eine Zusammenfassung von Statusmeldungen anzeigen, einen Drillthrough zum Anzeigen von Statusmeldungen ausführen und auf das Dialogfeld **Eigenschaften** der Standorte zugreifen.  

 Zusätzlich können Sie mit dem Mauszeiger auf einen Standort oder Replikationslink zwischen Standorten zeigen, um den allgemeinen Status der Objekte anzuzeigen. In einer Hierarchie mit mehreren primären Standorten müssen Sie Ihre Configuration Manager-Konsole mit dem Standort der zentralen Verwaltung verbinden, um Details zu Replikationslinks zwischen allen Standorten anzuzeigen, da der Replikationslinkstatus nicht global repliziert wird.  

 Mit den folgenden Optionen können Sie das Hierarchiediagramm ändern:  

-   **Gruppen**: Sie können die Anzahl von primären und sekundären Standorten, von denen Änderungen in der Anzeige des Hierarchiediagramms ausgelöst werden, konfigurieren, sodass die Standorte zu einem einzigen Objekt kombiniert werden. Wenn die Standorte zu einem einzigen Objekt kombiniert werden, sehen Sie die Gesamtzahl der Standorte und einen allgemeinen Rollup von Statusnachrichten sowie des Standortstatus. Von Gruppenkonfigurationen wird die geografische Ansicht nicht beeinflusst.  

-   **Favoriten**: Sie können einzelne Standorte als Favoriten angeben. Favoriten sind im Hierarchiediagramm mit einem Sternsymbol gekennzeichnet. Favoriten werden nicht mit anderen Standorten kombiniert, wenn Sie Gruppen verwenden, sondern werden immer einzeln angezeigt.  

#### <a name="geographical-view"></a>Geografische Ansicht  
 Von der geografischen Ansicht werden Ihre Standorte in einer geografischen Zuordnung angezeigt. Es werden nur Standorte angezeigt, die mit einem geografischen Ort konfiguriert sind. Wenn Sie in dieser Ansicht einen Standort auswählen, werden Replikationslinks zu über- und untergeordneten Standorten angezeigt. Im Unterschied zur Hierarchiediagrammansicht können Sie in dieser Ansicht keine Details zu Statusmeldungen und Replikationslinks der Standorte anzeigen.  

> [!NOTE]  
>  Wenn Sie die geografische Ansicht verwenden möchten, muss auf dem Computer, mit dem Sie Ihre Configuration Manager-Konsole verbinden, Internet Explorer installiert sein, und ein Zugriff auf Bing Maps mithilfe von HTTP muss möglich sein.  

Mit der folgenden Option können Sie die geografische Ansicht ändern:  

-   **Ort des Standorts**: Sie können einen geographischen Standort für jeden Standort angeben. Sie können den Standort als Straßenadresse, als Namen eines Ortes wie Stadtname, oder mithilfe von Längen- und Breitengradkoordinaten angeben. Für die Angabe des Längen- und Breitengrads von Redmond Washington würden Sie beispielsweise **N 47 40 26.3572 W 122 7 17.4432** als Ort des Standorts angeben. Sie müssen die Symbole für Grad, Minuten oder Sekunden der geografischen Länge und Breite nicht angeben. Configuration Manager verwendet Bing Maps, um den Ort als geografische Ansicht anzuzeigen. Damit haben Sie die Möglichkeit, Ihre Hierarchie im Verhältnis zu einem geografischen Ort anzuzeigen und Einsichten in regionale Probleme zu gewinnen, von denen bestimmte Standorte oder die Replikation zwischen Standorten betroffen sein können.  

     Wenn Sie einen geografischen Ort angeben, können Sie das Feld **Ort** verwenden, um nach einem bestimmten Standort in Ihrer Hierarchie zu suchen. Wenn Sie den Standort ausgewählt haben, geben Sie den Ort als Namen einer Stadt oder als Straßenadresse in die Spalte **Ort** ein. Configuration Manager verwendet Bing Maps zur Auflösung des Orts.  

###  <a name="BKMK_MonitorRepLinksAndStatuss"></a> Überwachen der Datenbankreplikationslinks und des Replikationsstatus  
 Zusätzlich zu den Details auf hoher Ebene, auf die über den Knoten **Standorthierarchie** im Arbeitsbereich **Überwachung** zugegriffen werden kann, können Sie Details zur Datenbankreplikation auch über den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** überwachen. Aus der **Datenbankreplikation** können Sie den Status der Replikationslinks zwischen Standorten überwachen, ebenso wie die Initialisierungs- und Replikationsdetails für Replikationsgruppen an dem Standort, mit dem Ihre Configuration Manager-Konsole verbunden ist.  

> [!TIP]  
>  Obwohl auch im Arbeitsbereich **Verwaltung** unter dem Knoten **Hierarchiekonfiguration** ein Knoten zur **Datenbankreplikation** vorhanden ist, können Sie sich den Replikationsstatus für Datenbankreplikationslinks von diesem Ort aus nicht anzeigen lassen.  

####  <a name="BKMK_MonitorReplicationLinks"></a> Replikationslinkstatus  
Bei der Datenbankreplikation zwischen Standorten werden mehrere Informationssätze, genannt Replikationsgruppen, repliziert. Jede Replikationsgruppe wird mit unterschiedlichen Replikationsprioritäten repliziert. Standardmäßig können weder die in einer Replikationsgruppe enthaltenen Daten noch die Replikationshäufigkeit geändert werden.  

 Wenn ein Replikationslink aktiv ist und sein Status weder Fehlgeschlagennoch Heruntergestuftist, dann werden alle Replikationsgruppen rechtzeitig repliziert. Wenn die Replikation nicht innerhalb des erwarteten Zeitraums von einer oder mehreren Repliaktionsgruppen abgeschlossen wird, dann wird der Link als Heruntergestuft angezeigt. Heruntergestufte Links sind zwar noch funktionsfähig, Sie sollten sie jedoch überwachen, um zu gewährleisten, dass der aktive Status wiederhergestellt wird, oder sie untersuchen, um weitere Herabstufungen und Fehler bei der Linkreplikation auszuschließen.  

 Sie können für jeden Replikationslink angeben, wie oft für eine nicht erfolgreich replizierte Replikationsgruppe der Replikationsversuch wiederholt werden soll, bevor der Status des Links auf "Herabgestuft" oder "Fehlerhaft" festgelegt wird. Auch wenn alle außer einer Replikationsgruppe erfolgreich repliziert wurden, wird der Status des Links auf Herabgestuftoder Fehlgeschlagengesetzt, weil von einer Replikationsgruppe die Replikation im Rahmen der angegebenen Versuche nicht erfolgreich abgeschlossen werden konnte. Informationen zu Replikationsschwellenwerten finden Sie im Abschnitt [Schwellenwerte für die Datenbankreplikation](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) des Themas [Datenübertragungen zwischen Standorten in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

 Verwenden Sie die Informationen in folgender Tabelle, um den Replikationslinkstatus zu erfahren, bei dem weitere Überprüfungen erforderlich sind.  

|Linkbeschreibung|Weitere Informationen|  
|----------------------|----------------------|  
|**Link ist aktiv**|Es wurden keine Probleme erkannt, und die Kommunikation über den Link ist aktuell.|  
|**Link heruntergestuft**|Die Replikation ist funktionsfähig, aber es kam bei mindestens einem Replikationsobjekt oder einer Replikationsgruppe zu Verzögerungen. Überwachen Sie Links mit diesem Status, und überprüfen Sie Informationen von beiden beteiligten Standorten auf Hinweise, dass bei diesem Link ein Fehler auftreten könnte.<br /><br /> Von einem Link kann der Status Herabgestuftauch dann angezeigt werden, wenn vom Standort, von dem replizierte Daten empfangen wurden, diese nicht schnell an die Datenbank übergeben werden können. Dies kann geschehen, wenn große Mengen an Daten repliziert werden. Wenn Sie beispielsweise ein Softwareupdate auf einer großen Anzahl von Computern bereitstellen, ist die Verarbeitung des Datenvolumens durch den übergeordneten Standort des Links möglicherweise zeitaufwendig. Ein Verarbeitungsstau am übergeordneten Standort kann dazu führen, dass der Linkstatus auf Herabgestuftgesetzt wird, bis vom übergeordneten Standort der Datenrückstand erfolgreich verarbeitet werden kann.|  
|**Fehler bei Link**|Die Replikation ist nicht funktionsfähig. Eine spontane Wiederherstellung des Replikationslinks ohne weitere Aktion ist möglich. Verwenden Sie die Replikationslinkanalyse, um den Link zu überprüfen und die Replikationsprobleme zu beheben.<br /><br /> Mit diesem Status kann auch ein Problem mit dem physischen Netzwerk zwischen dem übergeordneten und dem untergeordneten Standort des Replikationslinks aufgezeigt werden.|  

 Wenn Sie während des Upgrades eines übergeordneten Standorts auf ein neues Service Pack den Linkstatus vom untergeordneten Standort anzeigen, wird dieser als aktiv angezeigt. Nach dem Upgrade und bis am untergeordneten Standort dasselbe Service Pack wie am übergeordnete Standort ausgeführt wird, wird der Linkstatus als aktiv angezeigt, wenn er vom übergeordneten Standort angezeigt wird, und als konfiguriert, wenn er vom untergeordneten Standort angezeigt wird.  

####  <a name="BKMK_MonitorReplicationStatus"></a> Replikationsstatus  
 Über den Knoten **Datenbankreplikation** im Arbeitsbereich **Überwachung** können Sie sich den Status der Replikation für einen Replikationslink anzeigen lassen, sowie die Details zur Standortdatenbank an jedem Standort des Replikationslinks. Sie können auch Details zu Replikationsgruppen anzeigen lassen. Für das Anzeigen von Details wählen Sie einen Replikationslink und anschließend die entsprechende Registerkarte für den Replikationsstatus aus, den Sie sich anzeigen lassen möchten. Es folgen Details zu den verschiedenen Registerkarten für den Replikationsstatus.  

 **Zusammenfassung**  
 Lassen Sie sich wichtige Informationen zur Replikation von Standortdaten und globalen Daten zwischen zwei Standorten über einen Link anzeigen.  

 Sie können auch auf **Berichte für Verkehrsverlaufsdaten anzeigen** klicken, um sich einen Bericht mit Details zur Netzwerkbandbreite anzeigen zu lassen, die zur Replikation via den Replikationslink verwendet wird.  

 **Übergeordneter Standort**  
 Für den übergeordneten Standort auf einem Replikationslink können Sie Details zur Datenbank anzeigen, darunter auch:  

-   Firewallports für den SQL Server  

-   Freier Speicherplatz  

-   Datenbank-Dateispeicherorte  

-   Zertifikate  

**Untergeordneter Standort**  
 Für den untergeordneten Standort auf einem Replikationslink können Sie sich Details zur Datenbank anzeigen, darunter auch:  

-   Firewallports für den SQL Server  

-   Freier Speicherplatz  

-   Datenbank-Dateispeicherorte  

-   Zertifikate  

**Initialisierungsdetail**    
 Lassen Sie sich den Initialisierungsstatus für Replikationsgruppen anzeigen, die über den Replikationslink repliziert werden. Anhand dieser Informationen können Sie ermitteln, wann die Initialisierung der Replikationsdaten durchgeführt wird oder fehlgeschlagen ist.  

 Außerdem können Sie diese Informationen nutzen, um zu ermitteln, wann ein Standort sich im Interoperabilitätsmodus befindet. Der Interoperabilitätsmodus tritt dann auf, wenn vom untergeordneten Standort nicht dieselbe Version von Configuration Manager wie vom übergeordneten Standort ausgeführt wird.  

**Replikationsdetail**    
 Lassen Sie sich den Replikationsstatus für jede Replikationsgruppe anzeigen, die über den Link repliziert wird. Anhand dieser Informationen können Sie Probleme oder Verspätungen bei der Replikation bestimmter Daten erkennen, um die geeigneten Schwellenwerte der Datenbankreplikation für diesen Link zu ermitteln. Informationen zu Replikationsschwellenwerten der Datenbank finden Sie im Abschnitt [Schwellenwerte für die Datenbankreplikation](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) des Themas [Datenübertragungen zwischen Standorten in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

> [!TIP]  
>  Replikationsgruppen für Standortdaten werden nur vom untergeordneten Standort an den übergeordneten Standort versendet. Replikationsgruppen für globale Daten werden in beide Richtungen repliziert.  

###  <a name="BKMK_RLA"></a> Informationen zur Replikationslinkanalyse  
 Configuration Manager schließt die **Replikationslinkanalyse** ein, die Sie zum Analysieren und Beheben von Replikationsproblemen verwenden können. Sie können mithilfe der Replikationslinkanalyse Fehler bei den Replikationslinks beheben, wenn bei der Replikation ein Fehler aufgetreten ist oder die Replikation nicht richtig ausgeführt wird, obwohl noch keine Fehlermeldung vorliegt. Die Replikationslinkanalyse kann zur Fehlerbehebung bei Replikationsproblemen zwischen den folgenden Computern in der Configuration Manager-Hierarchie verwendet werden (die Richtung des Replikationsfehlers ist dabei nicht maßgeblich):  

-   Zwischen einem Standortserver und dem Standortdatenbankserver  

-   Zwischen dem Standortdatenbankserver eines Standorts und dem Datenbankcomputer eines anderen Standorts (Replikation zwischen Standorten)  

Sie können die Replikationslinkanalyse entweder mithilfe der Configuration Manager-Konsole oder mithilfe einer Eingabeaufforderung ausführen:  

-   Wenn Sie die Replikationslinkanalyse mithilfe der Configuration Manager-Konsole ausführen möchten: Klicken Sie im Arbeitsbereich **Überwachung** auf den Knoten **Datenbankreplikation**, wählen Sie den Replikationslink, den Sie überwachen möchten, und dann in der Gruppe **Datenbankreplikation** auf der Registerkarte **Startseite** die Option **Replikationslinkanalyse** aus.  

-   Wenn Sie eine Eingabeaufforderung ausführen möchten, geben Sie den folgenden Befehl ein: **%path%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe &lt;Quellstandortserver-FQDN\> &lt;Zielstandortserver-FQDN\>**  

Wenn Sie die Replikationslinkanalyse ausführen, werden mithilfe mehrerer Diagnoseregeln und Prüfungen Probleme erkannt. Wenn das Tool ausgeführt wird, können Sie sich die Probleme anzeigen lassen, die vom Tool ermittelt werden. Wenn Anweisungen zur Problembehebung bekannt sind, werden diese angezeigt. Wenn eine automatische Problembehebung durch die Replikationslinkanalyse möglich ist, wird Ihnen diese Option angezeigt. Bei Abschluss der Replikationslinkanalyse werden die Ergebnisse im folgenden XML-basierten Bericht sowie in der folgenden Protokolldatei auf dem Desktop des Benutzers, der das Tool ausgeführt hat, angezeigt:  

-   ReplicationAnalysis.xml  

-   ReplicationLinkAnalysis.log  

Wenn die Replikationslinkanalyse ausgeführt wird, stoppt sie die folgenden Dienste während der Behebung einiger Probleme und startet sie nach Fertigstellung der Fehlerbehebung erneut.  

-   SMS_SITE_COMPONENT_MANAGER  

-   SMS_EXECUTIVE  

Wenn die Replikationslinkanalyse die Fehlerbehebung nicht erfolgreich abschließt, sollten Sie den Standortserver überprüfen und die gestoppten Dienste erneut starten.  

Es werden erfolgreiche sowie nicht erfolgreiche Aktionen zur Problembehebung protokolliert, um zusätzliche Details bereitzuhalten, die nicht in der Oberfläche des Tools angezeigt werden.  

**Voraussetzungen für die Verwendung der Replikationslinkanalyse:**  

-   Sie benötigen für das Konto, das Sie zum Ausführen der Replikationslinkanalyse verwenden, lokale Administratorrechte auf jedem am Replikationslink beteiligten Computer. Für das Konto ist keine bestimmte rollenbasierte Verwaltungssicherheitsrolle erforderlich. Daher können Administratoren mit Zugriff auf den Knoten **Datenbankreplikation** das Tool mithilfe der Configuration Manager-Konsole ausführen, oder Systemadministratoren mit ausreichenden Rechten für jeden Computer können das Tool mithilfe einer Eingabeaufforderung ausführen.  

-   Sie benötigen für das Konto, das Sie zum Ausführen der Replikationslinkanalyse verwenden, Systemadministratorrechte auf jeder am Replikationslink beteiligten SQL Server-Datenbank.  

**Bekannte Probleme bei der Replikationslinkanalyse:**  

-   Seit der Veröffentlichung des System Center Configuration Manager-Release 1511 generiert die Replikationslinkanalyse für primäre Standorte, die von System Center 2012 Configuration Manager upgegradet wurden, Fehler in Verbindung mit SQL Server Service Broker-Zertifikaten. Dies liegt daran, dass die Namen der mit Version 1511 eingeführten Zertifikate geändert wurden und dass die Replikationslinkanalyse noch nicht für die neue Version aktualisiert wurde. Diese Fehler können problemlos ignoriert werden.  

###  <a name="BKMK_ProcsforMonitoringReplication"></a> Prozeduren zum Überwachen der Datenbankreplikation  

##### <a name="to-monitor-high-level-site-to-site-database-replication-status"></a>So überwachen Sie den allgemeinen Datenbankreplikationsstatus zwischen Standorten    
1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Standorthierarchie** , um die Ansicht **Hierarchiediagramm** zu öffnen.  

3.  Zeigen Sie kurz mit dem Mauszeiger auf die Linie zwischen den beiden Standorten, um den Status der globalen und der Standortdatenreplikation für diese beiden Standorte anzuzeigen.  

##### <a name="to-monitor-the-replication-status-for-a-replication-link"></a>Überwachen des Replikationsstatus für einen Replikationslink    
1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Datenbankreplikation**, und wählen Sie dann den Replikationslink aus, der überwacht werden soll. Wählen Sie anschließend im Arbeitsbereich die entsprechende Registerkarte aus, um sich die verschiedenen Details zum Replikationsstatus für diesen Link anzeigen zu lassen.  
