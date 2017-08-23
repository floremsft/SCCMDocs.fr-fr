---
title: Planen von Softwareupdates | Microsoft Docs
description: "Ein Plan für die Softwareupdatepunkt-Infrastruktur ist wichtig, bevor Sie Softwareupdates in einer System Center Configuration Manager-Produktionsumgebung verwenden."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 06/27/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: 8b739a01a6bb5cacf0f7109e2e6fa3b31dd666d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-software-updates-in-system-center-configuration-manager"></a>Planen von Softwareupdates in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bevor Sie Softwareupdates in einer System Center Configuration Manager-Produktionsumgebung verwenden, ist es wichtig, den Planungsprozess durchzugehen. Einen guter Plan für die Softwareupdatepunkt-Infrastruktur ist wichtig für eine erfolgreiche Softwareupdateimplementierung.

## <a name="capacity-planning-recommendations-for-software-updates"></a>Empfehlungen für die Kapazitätsplanung bei Softwareupdates  
 Die folgenden Empfehlungen können bei der Ermittlung der für Ihre Organisation geeigneten Informationen zur Kapazitätsplanung für Softwareupdates als Basislinie dienen. Die tatsächlichen Kapazitätsanforderungen können je nach der konkreten Netzwerkumgebung, der zum Hosten des Standortsystems für den Softwareupdatepunkt verwendeten Hardware, der Anzahl installierter Clients und der auf dem Server installierten Standortsystemrollen von den in diesem Thema aufgeführten Empfehlungen abweichen.  

###  <a name="BKMK_SUMCapacity"></a> Kapazitätsplanung für den Softwareupdatepunkt  
 Die Anzahl der unterstützten Clients hängt von der WSUS-Version (Windows Server Update Services), die auf dem Softwareupdatepunkt ausgeführt wird, sowie davon ab, ob neben der Standortsystemrolle „Softwareupdatepunkt“ noch eine weitere Standortsystemrolle existiert:  

-   Vom Softwareupdatepunkt werden bis zu 25.000 Clients unterstützt, wenn WSUS auf dem Softwareupdatepunkt-Computer ausgeführt wird und neben dem Softwareupdatepunkt noch eine weitere Standortsystemrolle existiert  

-   Der Softwareupdatepunkt kann bis zu 150.000 Clients unterstützt, wenn der Remotecomputer die WSUS-Anforderungen erfüllt, WSUS mit Configuration Manager verwendet wird und Sie Folgendes konfigurieren:

    IIS-Anwendungspools:
    - Erhöhen Sie die WsusPool-Warteschlangenlänge auf 2000.
    - Erhöhen Sie die Begrenzung des privaten Speichers für WsusPool auf das Vierfache, oder legen Sie den Wert auf 0 (unbegrenzt) fest.      

    Ausführliche Informationen zu den Hardwareanforderungen für den Softwareupdatepunkt finden Sie unter [Empfohlene Hardware für Standortsysteme](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).

-   Die Konfiguration von Softwareupdatepunkten als NLB-Cluster wird nicht standardmäßig von Configuration Manager unterstützt. Vor Configuration Manager Version 1702 konnten Sie das Configuration Manager SDK verwenden, um bis zu vier Softwareupdatepunkte in einem NLB-Cluster zu konfigurieren. Allerdings werden ab Version 1702 des Configuration Manager Softwareupdatepunkte als NLB-Cluster nicht unterstützt, und Upgrades auf Configuration Manager Version 1702 werden blockiert, wenn diese Konfiguration erkannt wird.

### <a name="capacity-planning-for-software-updates-objects"></a>Kapazitätsplanung für Softwareupdateobjekte  
 Verwenden Sie die folgenden Kapazitätsinformationen zur Planung von Softwareupdateobjekten.  

-   **Limit von 1.000 Softwareupdates in einer Bereitstellung**  

     Sie müssen die Anzahl von Softwareupdates in einer einzelnen Softwareupdatebereitstellung auf 1.000 begrenzen. Geben Sie beim Erstellen einer automatischen Bereitstellungsregel ein Kriterium an, durch das die Anzahl der zurückgegebenen Softwareupdates beschränkt wird. Bei der automatischen Bereitstellungsregel tritt ein Fehler auf, wenn mehr als 1.000 Softwareupdates mit dem von Ihnen angegebenen Kriterium übereinstimmen und somit zurückgegeben werden. Sie können den Status der automatischen Bereitstellungsregel im Knoten **Automatische Bereitstellungsregeln** in der Configuration Manager-Konsole überprüfen. Wenn Sie Softwareupdates manuell bereitstellen, wählen Sie höchstens 1.000 Updates zur Bereitstellung aus.  

     Sie müssen auch die Anzahl von Softwareupdates in einer Konfigurationsbaseline auf 1.000 begrenzen. Weitere Informationen finden Sie unter [Erstellen von Konfigurationsbaselines](../../compliance/deploy-use/create-configuration-baselines.md).

##  <a name="BKMK_SUPInfrastructure"></a> Bestimmen der Softwareupdatepunkt-Infrastruktur  
 Der Standort der zentralen Verwaltung und alle untergeordneten primären Standorte müssen über einen Softwareupdatepunkt verfügen, an dem Softwareupdates bereitgestellt werden Beim Planen der Infrastruktur von Softwareupdatepunkten müssen Sie die folgenden Abhängigkeiten festlegen:
 - wo der Softwareupdatepunkt des Standorts installiert werden soll
 - welche Standorte einen Softwareupdatepunkt erfordern, der Kommunikation von internetbasierten Clients akzeptiert
 - ob Sie einen Softwareupdatepunkt an einem sekundären Standort benötigen.

Verwenden Sie die folgenden Abschnitte, um die Infrastruktur der Softwareupdatepunkte festzulegen.  

> [!IMPORTANT]  
>  Weitere Informationen zu den internen und externen Abhängigkeiten, die für Softwareupdates erforderlich sind, finden Sie unter [Voraussetzungen für Softwareupdates](prerequisites-for-software-updates.md).  

 Sie können mehrere Softwareupdatepunkte zu einem primären Standort von Configuration Manager hinzufügen. Durch die Möglichkeit, mehrere Softwareupdatepunkte an einem Standort zu verwenden, wird eine Fehlertoleranz ohne die mit dem Netzwerklastenausgleich verbundene Komplexität geboten. Allerdings ist das mit mehreren Softwareupdatepunkten einhergehende Failover beim reinen Lastenausgleich weniger robust als der Netzwerklastenausgleich, da bei seiner Konzeption die Fehlertoleranz im Vordergrund stand. Das Failoverdesign des Softwareupdatepunkts unterscheidet sich zudem von dem auf einer rein zufälligen Anordnung beruhenden Modell, das die Designgrundlage für Verwaltungspunkte bildet. Anders als beim Design von Verwaltungspunkten ist bei Softwareupdatepunkten der Wechsel zu einem neuen Softwareupdatepunkt mit Client- und Netzwerkleistungskosten verbunden. Durch den Wechsel des Clients zu einem neuen WSUS-Server zwecks Überprüfung auf Softwareupdates werden die Kataloggröße, die zugehörigen clientseitigen Anforderungen sowie die Anforderungen an die Netzwerkleistung gesteigert. Aus diesem Grund wird vom Client die Affinität mit dem letzten Softwareupdatepunkt aufrechterhalten, bei dem die Überprüfung erfolgreich war.  

 Der erste Softwareupdatepunkt, den Sie an einem primären Standort installieren, dient als Synchronisierungsquelle für alle weiteren Softwareupdatepunkte, die Sie dem primären Standort hinzufügen. Nachdem Sie die Softwareupdatepunkte hinzugefügt und die Softwareupdatesynchronisierung initiiert haben, können Sie den Status der Softwareupdatepunkte und der Synchronisierungsquelle im Arbeitsbereich **Überwachung** im Knoten **Synchronisierungsstatus der Softwareupdatepunkte** anzeigen.  

 Wenn bei einem Softwareupdatepunkt ein Fehler auftritt und dieser Softwareupdatepunkt als Synchronisierungsquelle der anderen Softwareupdatepunkte am Standort konfiguriert ist, müssen Sie den fehlerhaften Softwareupdatepunkt manuell entfernen und einen neuen Softwareupdatepunkt als Synchronisierungsquelle auswählen. Weitere Informationen zum Entfernen eines Softwareupdatepunkts finden Sie unter [Entfernen der Standortsystemrolle des Softwareupdatepunkts](../get-started/remove-a-software-update-point.md).  

###  <a name="BKMK_SUPList"></a> Softwareupdatepunkt-Liste  
 Configuration Manager stellt in den folgenden Szenarios eine Softwareupdatepunkt-Liste für den Client bereit: wenn ein neuer Client die Richtlinie zur Aktivierung von Softwareupdates erhält, oder wenn der Wechsel zu einem anderen Softwareupdatepunkt erforderlich ist, weil keine Verbindung zwischen dem Client und seinem Softwareupdatepunkt hergestellt werden kann. Vom Client wird in der Liste auf Zufallsbasis ein Softwareupdatepunkt ausgewählt. Dabei haben die Softwareupdatepunkte Priorität, die sich in der gleichen Gesamtstruktur befinden. Configuration Manager stellt Clients je nach Clienttyp eine andere Liste zur Verfügung.  

-   **Intranetbasierte Clients**: Diese Clients erhalten eine Liste mit Softwareupdatepunkten, die Sie so konfigurieren können, dass nur Verbindungen mit dem Intranet zulässig sind, bzw. eine Liste mit Softwareupdatepunkten, bei denen Clientverbindungen mit dem Internet und dem Intranet möglich sind.  

-   **Internetbasierte Clients**: Diese Clients erhalten eine Liste mit Softwareupdatepunkten, die Sie so konfigurieren können, dass nur Verbindungen mit dem Internet zulässig sind, bzw. eine Liste mit Softwareupdatepunkten, bei denen Clientverbindungen mit dem Internet und dem Intranet möglich sind.  

###  <a name="BKMK_SUPSwitching"></a> Wechseln des Softwareupdatepunkts  
> [!NOTE]
> Ab Version 1702 verwenden Client Begrenzungsgruppen, um einen neuen Softwareupdatepunkt zu finden, und um ein Fallback durchzuführen und einen neuen Softwareupdatepunkt zu finden, wenn auf ihren aktuellen nicht mehr zugriffen werden kann. Sie können verschiedenen Begrenzungsgruppen einzelne Softwareupdatepunkte hinzufügen, um zu steuern, welchen Server ein Client finden kann. Weitere Informationen finden Sie im Thema [Configuring Boundary Groups (Konfigurieren von Begrenzungsgruppen)](/sccm/core/servers/deploy/configure/boundary-groups) unter [Software Update Points (Softwareupdatepunkte)](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).

Wenn es an einem Standort mehrere Softwareupdatepunkte gibt und einer davon fehlerhaft oder nicht mehr verfügbar ist, wird von Clients eine Verbindung mit einem anderen Softwareupdatepunkt hergestellt und die Überprüfung auf die jüngsten Softwareupdates dort fortgesetzt. Die ursprüngliche Zuweisung eines Clients zu einem Softwareupdatepunkt bleibt solange bestehen, bis bei der Überprüfung dieses Softwareupdatepunkts auf Softwareupdates ein Fehler auftritt.  

Bei der Überprüfung auf Softwareupdates kann eine Reihe unterschiedlicher Wiederholungs- bzw. Nichtwiederholungsfehlercodes ausgegeben werden. Bei einem Überprüfungsfehler mit einem Wiederholungsfehlercode wird vom Client ein Wiederholungsprozess zur Überprüfung des Softwareupdatepunkts auf Softwareupdates gestartet. Ein Wiederholungsfehlercode ist in der Regel darauf zurückzuführen, dass der WSUS-Server nicht verfügbar oder vorübergehend überlastet ist. Wenn bei der Überprüfung auf Softwareupdates ein Fehler auftritt, werden folgende Vorgänge ausgeführt:  

1.  Die Überprüfung auf Softwareupdates wird vom Client zum geplanten Zeitpunkt ausgeführt. Sie kann auch über die Systemsteuerung auf dem Client oder mithilfe des SDK initiiert werden. Bei einem Überprüfungsfehler wird die Überprüfung des gleichen Softwareupdatepunkts nach einer 30-minütigen Wartezeit vom Client wiederholt.  

2.  Vom Client werden mindestens vier Wiederholungsversuche in Abständen von 30 Minuten ausgeführt. Nach dem vierten Fehler und einer weiteren Wartezeit von 2 Minuten wird zum nächsten Softwareupdatepunkt in der Softwareupdatepunkt-Liste gewechselt.  

3.  Der Client durchläuft auf dem neuen Softwareupdatepunkt denselben Prozess. Nach einer erfolgreichen Überprüfung wird vom Client fortan eine Verbindung mit dem neuen Softwareupdatepunkt hergestellt.

 Die folgende Liste enthält zusätzliche Informationen, die Sie bei Wiederholungsversuchen und beim Wechseln von Softwareupdatepunkten erwägen müssen:  

-   Wenn ein Client vom Unternehmensintranet getrennt ist und bei der Überprüfung auf Softwareupdates ein Fehler auftritt, findet kein Wechsel zu einem anderen Softwareupdatepunkt statt. Dies ist ein erwarteter Fehler, da es nicht möglich ist, eine Verbindung zwischen dem Client und dem Firmennetzwerk oder dem Softwareupdatepunkt, über den Intranetverbindungen zulässig sind, herzustellen. Der Configuration Manager-Client bestimmt die Verfügbarkeit des Softwareupdatepunkts im Intranet.  

-   Wenn die internetbasierte Clientverwaltung aktiviert ist und es mehrere Softwareupdatepunkte gibt, die dafür konfiguriert sind, Kommunikation von internetbasierten Clients zu akzeptieren, erfolgt der Wechsel nach dem im vorherigen Beispiel beschriebenen Standardwiederholungsprozess.  

-   Wenn der Überprüfungsprozess gestartet, aber der Client vor dessen Abschluss heruntergefahren wurde, gilt dies weder als Überprüfungsfehler noch als eine der vier Wiederholungen.  

Wenn Configuration Manager die folgenden Fehlercodes des Windows Update-Agents erhält, muss der Client den Verbindungsaufbau wiederholen:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Um die Bedeutung eines Fehlercodes nachzuschlagen, müssen Sie den dezimalen Fehlercode in einen Hexadezimalwert umwandeln und diesen dann auf einer Website suchen, wie z. B. im [Wiki zu den Fehlercodes des Windows Update-Agents](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx).


###  <a name="BKMK_ManuallySwitchSUPs"></a> Manuelles Wechseln von Clients auf einen neuen Softwareupdatepunkt
Ab Version 1606 von Configuration Manager können Sie für Configuration Manager-Clients die Option zum Wechsel zu einem neuen Softwareupdatepunkt aktivieren, wenn beim aktiven Softwareupdatepunkt Probleme auftreten. Diese Option hat nur Änderungen zur Folge, wenn ein Client mehrere Softwareupdatepunkte von einem Verwaltungspunkt erhält.

> [!IMPORTANT]    
> Wenn Sie die Geräte wechseln, um einen neuen Server zu verwenden, verwenden die Geräte einen Fallback, um den neuen Server zu finden. Deshalb sollten Sie vor diesem Wechsel die Konfigurationen Ihrer Begrenzungsgruppen überprüfen und sicherstellen, dass sich Ihre Softwareupdatepunkte in den korrekten Begrenzungsgruppen befinden. Weitere Informationen finden Sie unter [Software update points (Softwareupdatepunkte)](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).
>
> Der Wechsel zu einem neuen Softwareupdatepunkt wird zusätzlichen Netzwerkdatenverkehr generieren. Die Größe des Datenverkehrs hängt von Ihren WSUS-Konfigurationseinstellungen ab (Updateklassifizierungen, Produkte, ob die Softwareupdatepunkte eine gemeinsame WSUS-Datenbank verwenden usw.). Wenn Sie mehrere Geräte wechseln möchten, sollten Sie dies während der Wartung von Windows tun, um die Auswirkungen auf Ihr Netzwerk während der Synchronisation mit dem neuen Softwareupdatepunkt-Server zu reduzieren.

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>So aktivieren Sie die Option zum Wechseln von Softwareupdatepunkten  
Aktivieren Sie diese Option auf einer Gerätesammlung oder auf einer Reihe von Geräten. Nach der Aktivierung suchen die Clients nach anderen Softwareupdatepunkten bei der nächsten Überprüfung.

1.  Gehen Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität > Übersicht > Gerätesammlungen**.  

2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Sammlung** auf **Clientbenachrichtigung**, und klicken Sie anschließend auf **Zum nächsten Softwareupdatepunkt wechseln**.  


###  <a name="BKMK_SUP_CrossForest"></a> Softwareupdatepunkte in einer nicht vertrauenswürdigen Gesamtstruktur  
 Sie können an einem Standort mindestens einen Softwareupdatepunkt zur Unterstützung von Clients in einer nicht vertrauenswürdigen Gesamtstruktur erstellen. Zum Hinzufügen eines Softwareupdatepunkts zu einer anderen Gesamtstruktur müssen Sie in dieser Gesamtstruktur zuerst einen WSUS-Server installieren und konfigurieren. Starten Sie dann den Assistenten, um einen Configuration Manager-Standortserver mit der Standortsystemrolle des Softwareupdatepunkts hinzuzufügen. Konfigurieren Sie im Assistenten die folgenden Einstellungen, damit eine Verbindung mit dem WSUS-Server in der nicht vertrauenswürdigen Gesamtstruktur hergestellt werden kann:  

-   Geben Sie ein Standortsystem-Installationskonto mit Zugriff auf den WSUS-Server in der Gesamtstruktur an.  

-   Geben Sie das Verbindungskonto für WSUS-Server an, über das die Verbindung mit dem WSUS-Server hergestellt werden soll.  

 Angenommen, Sie verfügen in Gesamtstruktur A über einen primären Standort mit zwei Softwareupdatepunkten (SUP01 und SUP02). Darüber hinaus verfügen Sie für denselben primären Standort über zwei Softwareupdatepunkte (SUP03 und SUP04) in Gesamtstruktur B. Wenn in diesem Beispiel der Wechsel erfolgt, haben zunächst die Softwareupdatepunkte Priorität, die sich in der gleichen Gesamtstruktur wie der Client befinden.  

###  <a name="BKMK_WSUSSyncSource"></a> Verwenden eines vorhandenen WSUS-Servers als Synchronisierungsquelle am Standort der obersten Ebene  
 Der Standort der obersten Ebene in einer Hierarchie ist in der Regel für die Synchronisierung der Metadaten für Softwareupdates mit Microsoft Update konfiguriert. Wenn der Zugriff auf das Internet vom Standort der obersten Ebene aufgrund der Sicherheitsrichtlinie Ihres Unternehmens nicht möglich ist, können Sie die Synchronisierungsquelle für den Standort der obersten Ebene konfigurieren, um einen vorhandenen WSUS-Server zu verwenden, der sich außerhalb Ihrer Configuration Manager-Hierarchie befindet. Angenommen, ein WSUS-Server ist im Umkreisnetzwerk installiert, das im Gegensatz zum Standort der obersten Ebene Zugriff auf das Internet hat. Sie können den WSUS-Server in dem Umkreisnetzwerk als Synchronisierungsquelle für die Metadaten für Softwareupdates konfigurieren. Sie müssen sicherstellen, dass der WSUS-Server im Umkreisnetzwerk Softwareupdates synchronisiert, die die in Ihrer Configuration Manager-Hierarchie erforderlichen Kriterien erfüllen. Andernfalls werden vom Standort der obersten Ebene nicht die von Ihnen erwarteten Softwareupdates synchronisiert. Konfigurieren Sie beim Erstellen des Softwareupdatepunkts ein WSUS-Verbindungskonto mit Zugriff auf den WSUS-Server in dem Umkreisnetzwerk. Bestätigen Sie außerdem, dass der Datenverkehr von der Firewall über die entsprechenden Ports zugelassen wird. Weitere Informationen finden Sie im Abschnitt zu den [Ports, die vom Softwareupdatepunkt als Synchronisierungsquelle genutzt werden](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  

###  <a name="BKMK_NLBSUPSP1"></a> Für die Verwendung eines NLB konfigurierter Softwareupdatepunkt  
 Durch den Wechsel zu einem anderen Softwareupdatepunkt dürften Ihre Anforderungen an die Fehlertoleranz erfüllt werden. Die Konfiguration von Softwareupdatepunkten als NLB-Cluster wird nicht standardmäßig von Configuration Manager unterstützt. Vor Configuration Manager Version 1702 konnten Sie das Configuration Manager SDK verwenden, um bis zu vier Softwareupdatepunkte in einem NLB-Cluster zu konfigurieren. Allerdings werden ab Version 1702 des Configuration Manager Softwareupdatepunkte als NLB-Cluster nicht unterstützt, und Upgrades auf Configuration Manager Version 1702 werden blockiert, wenn diese Konfiguration erkannt wird. Weitere Informationen zum PowerShell-Cmdlet „Set-CMSoftwareUpdatePoint“ finden Sie unter [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834).

###  <a name="BKMK_SUPSecSite"></a> Softwareupdatepunkt an sekundärem Standort  
 An sekundären Standorten ist der Softwareupdatepunkt optional. Bei der Installation eines Softwareupdatepunkts an einem sekundären Standort wird die WSUS-Datenbank als Replikat des Standard-Softwareupdatepunkts am übergeordneten primären Standort konfiguriert. An einem sekundären Standort können Sie nur einen Softwareupdatepunkt installieren. Die einem sekundären Standort zugewiesenen Geräte werden so konfiguriert, dass sie einen Softwareupdatepunkt am übergeordneten Standort verwenden, wenn am sekundären Standort kein Softwareupdatepunkt installiert ist. In der Regel installieren Sie einen Softwareupdatepunkt an einem sekundären Standort, wenn die Netzwerkbandbreite zwischen den Geräten, die dem sekundären Standort zugewiesen sind, und den Softwareupdatepunkten am übergeordneten primären Standort beschränkt ist oder wenn die Kapazität des Softwareupdatepunkts fast aufgebraucht ist. Nach der erfolgreichen Installation und Konfiguration eines Softwareupdatepunkts am sekundären Standort wird auf den Clientcomputern, die dem Standort zugewiesen sind, ein Update für eine standortweite Richtlinie durchgeführt. Der neue Softwareupdatepunkt wird danach von den Clientcomputern verwendet.  

##  <a name="BKMK_SUPInstallation"></a> Planen der Installation von Softwareupdatepunkten  
 Je nach Configuration Manager-Infrastruktur müssen Sie vor dem Erstellen der Standortsystemrolle „Softwareupdatepunkte“ in Configuration Manager eine Reihe von Anforderungen sorgfältig prüfen. Wenn Sie den Softwareupdatepunkt für die SSL-Kommunikation konfigurieren, ist dieser Abschnitt besonders wichtig, da Sie zusätzliche Schritte ausführen müssen, damit die Softwareupdatepunkte in der Hierarchie ordnungsgemäß verwendet werden können. Dieser Abschnitt enthält Informationen zu den Schritten, die für die erfolgreiche Planung und Vorbereitung der Installation von Softwareupdatepunkten erforderlich sind.  

###  <a name="BKMK_SUPSystemRequirements"></a> Anforderungen für den Softwareupdatepunkt  
 Die Standortsystemrolle „Softwareupdatepunkt“ muss auf einem Standortsystem installiert werden, das die Mindestanforderungen für WSUS erfüllt und den unterstützten Konfigurationen für Configuration Manager-Standortsysteme entspricht.  

-   Weitere Informationen zu den Mindestanforderungen für die WSUS-Serverrolle in Windows Server 2012 finden Sie unter [Überprüfen der Überlegungen und Systemanforderungen](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1) in der Dokumentationsbibliothek von Windows Server 2012.  

-   Weitere Informationen zu den unterstützten Konfigurationen für Configuration Manager-Standortsysteme finden Sie unter [Anforderungen an Standorte und Standortsysteme](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

###  <a name="BKMK_PlanningForWSUS"></a> Planen der WSUS-Installation  

Für Softwareupdates ist es erforderlich, dass eine unterstützte Version von WSUS auf allen Standortsystemservern installiert ist, die Sie für die Standortsystemrolle „Softwareupdatepunkt“ konfigurieren. Wenn Sie den Softwareupdatepunkt nicht auf dem Standortserver installieren, müssen Sie zudem die WSUS-Verwaltungskonsole auf dem Standortservercomputer installieren, sofern sie nicht bereits installiert ist. Hierdurch wird die Kommunikation des Standortservers mit WSUS auf dem Softwareupdatepunkt ermöglicht.  

 Wenn Sie WSUS mit Windows Server 2012 verwenden, müssen Sie zusätzliche Berechtigungen konfigurieren. Hierdurch wird sichergestellt, dass eine Verbindung zwischen **WSUS Configuration Manager** in Configuration Manager und WSUS hergestellt werden kann, um regelmäßig Integritätsprüfungen auszuführen. Zum Konfigurieren der Berechtigungen stehen folgende Möglichkeiten zur Auswahl:  

-   Fügen Sie der Gruppe **WSUS-Administratoren** das Konto **SYSTEM** hinzu.  

-   Fügen Sie das Konto **NT AUTHORITY\SYSTEM** als Benutzer der WSUS-Datenbank (SUSDB) hinzu, und konfigurieren Sie mindestens die Mitgliedschaft in der Datenbankrolle „webService“.  

 Weitere Informationen zum Installieren von WSUS unter Windows Server 2012 finden Sie unter [Install the WSUS Server Role (Installieren der WSUS-Serverrolle)](http://go.microsoft.com/fwlink/p/?LinkId=272355) in der Dokumentationsbibliothek zu Windows Server 2012.  

 Wenn Sie an einem primären Standort mehrere Softwareupdatepunkte installieren, sollten Sie für jeden Softwareupdatepunkt einer Active Directory-Gesamtstruktur die gleiche WSUS-Datenbank verwenden. Durch die Nutzung der gleichen Datenbank können Sie die Auswirkungen auf die Client- und Netzwerkleistung, die sich beim Wechsel eines Clients zu einem neuen Softwareupdatepunkt ergeben können, erheblich abmildern, aber nicht vollständig beseitigen. Wenn ein Client zu einem neuen Softwareupdatepunkt wechselt, der eine Datenbank gemeinsam mit dem alten Softwareupdatepunkt nutzt, wird weiterhin eine Deltaüberprüfung ausgeführt. Diese Überprüfung ist jedoch weit weniger umfangreich als bei einem WSUS-Server mit eigener Datenbank.  

####  <a name="BKMK_CustomWebSite"></a> Konfigurieren Sie WSUS für die Verwendung einer benutzerdefinierten Website.  
 Beim Installieren von WSUS haben Sie die Möglichkeit, die vorhandene IIS-Standardwebsite zu verwenden oder eine benutzerdefinierte WSUS-Website zu erstellen. Erstellen Sie eine benutzerdefinierte Website für WSUS, sodass die WSUS-Dienste von IIS in einer dedizierten virtuellen Website gehostet werden, anstatt die gleiche Website zu verwenden wie die Configuration Manager-Standortsysteme oder andere Anwendungen. Dies trifft insbesondere auf die Installation der Standortsystemrolle „Softwareupdatepunkt“ auf dem Standortserver zu. Wenn Sie WSUS unter Windows Server 2012 oder Windows Server 2016 ausführen, wird WSUS standardmäßig für die Verwendung von Port 8530 für HTTP und Port 8531 für HTTPS konfiguriert. Sie müssen diese Porteinstellungen beim Erstellen des Softwareupdatepunkts an einem Standort angeben.  

####  <a name="BKMK_WSUSInfrastructure"></a> Verwenden einer vorhandenen WSUS-Infrastruktur  
 Sie können einen WSUS-Server, der bereits vor der Installation von Configuration Manager in Ihrer Umgebung aktiv war, als Softwareupdatepunkt wählen. Beim Konfigurieren des Softwareupdatepunkts müssen Sie die Synchronisierungseinstellungen angeben. Configuration Manager stellt eine Verbindung mit dem WSUS-Server auf dem Softwareupdatepunkt-Server her, und konfiguriert WSUS mit den gleichen Einstellungen. Wenn Sie den WSUS-Server zuvor als Softwareupdatepunkt mit Produkten oder Klassifizierungen konfiguriert haben, die Sie nicht als Teil der Synchronisierungseinstellungen für den Softwareupdatepunkt konfiguriert haben, werden die Metadaten der Softwareupdates für die Produkte und Klassifizierungen unabhängig von Ihren Synchronisierungseinstellungen für den Softwareupdatepunkt für sämtliche Metadaten der Softwareupdates in der WSUS-Datenbank synchronisiert. Dies kann zu unerwarteten Metadaten für Softwareupdates in der Standortdatenbank führen. Dieses Verhalten kann auch beobachtet werden, wenn Sie Produkte oder Klassifizierungen direkt in der WSUS-Verwaltungskonsole hinzufügen und die Synchronisierung sofort initiieren. Im Rahmen einer von Configuration Manager standardmäßig stündlich hergestellten Verbindung mit WSUS auf dem Softwareupdatepunkt werden alle Einstellungen zurückgesetzt, die außerhalb von Configuration Manager geändert wurden. Softwareupdates, die nicht den von Ihnen in den Synchronisierungseinstellungen angegebenen Produkten und Klassifizierungen entsprechen, werden als abgelaufen festgelegt und dann aus der Standortdatenbank entfernt

 Wenn ein WSUS-Server als Softwareupdatepunkt konfiguriert wurde, können Sie diesen nicht mehr als eigenständigen WSUS-Server verwenden. Wenn Sie einen einzelnen, eigenständigen WSUS-Server benötigen, der nicht von Configuration Manager verwaltet wird, müssen Sie diesen auf einem anderen Server konfigurieren.

####  <a name="BKMK_WSUSAsReplica"></a> Konfigurieren von WSUS als Replikatserver  
 Beim Erstellen der Standortsystemrolle „Softwareupdatepunkt“ auf einem primären Standortserver kann kein WSUS-Server verwendet werden, der als Replikat konfiguriert ist. Ist der WSUS-Server als Replikat konfiguriert, kann er nicht von Configuration Manager konfiguriert werden, und bei der WSUS-Synchronisierung tritt ebenfalls ein Fehler auf. Wenn ein Softwareupdatepunkt an einem sekundären Standort erstellt wird, wird WSUS von Configuration Manager als Replikatserver für die WSUS-Instanz konfiguriert, die auf dem Softwareupdatepunkt am übergeordneten primären Standort ausgeführt wird. Der erste Softwareupdatepunkt, den Sie an einem primären Standort installieren, ist der Standard-Softwareupdatepunkt. Weitere Softwareupdatepunkte am Standort werden als Replikate des Standard-Softwareupdatepunkts konfiguriert.  

####  <a name="BKMK_WSUSandSSL"></a> Entscheiden, ob WSUS zur Verwendung von SSL konfiguriert werden soll  
 Zum Schutz von WSUS auf dem Softwareupdatepunkt können Sie das SSL-Protokoll verwenden. SSL wird von WSUS zur Authentifizierung von Clientcomputern und WSUS-Downstreamservern gegenüber dem WSUS-Server verwendet. SSL wird von WSUS auch zum Verschlüsseln von Metadaten für Softwareupdates verwendet. Wenn Sie sich dafür entscheiden, WSUS durch SSL zu schützen, müssen Sie den WSUS-Server vor der Installation des Softwareupdatepunkts entsprechend vorbereiten.  

 Beim Installieren und Konfigurieren des Softwareupdatepunkts müssen Sie die Einstellung **SSL-Kommunikation mit dem WSUS-Server erforderlich** auswählen. Andernfalls wird Configuration Manager WSUS nicht zur Verwendung von SSL konfigurieren. Wenn Sie SSL für WSUS auf einem Softwareupdatepunkt aktivieren, muss WSUS auf den Softwareupdatepunkten an allen untergeordneten Standorten ebenfalls zur Verwendung von SSL konfiguriert werden.  

###  <a name="BKMK_ConfigureFirewalls"></a> Konfigurieren von Firewalls  
 Zwischen Softwareupdates an einem Configuration Manager-Standort der zentralen Verwaltung und WSUS auf dem Softwareupdatepunkt sowie zwischen WSUS und der Synchronisierungsquelle findet eine Kommunikation statt, um Metadaten für Softwareupdates zu synchronisieren. Softwareupdatepunkte an einem untergeordneten Standort und der Softwareupdatepunkt am übergeordneten Standort kommunizieren miteinander. Wenn es an einem primären Standort mehrere Softwareupdatepunkte gibt, muss zwischen dem ersten am Standort installierten Softwareupdatepunkt (dem Standard-Softwareupdatepunkt) und den zusätzlichen Softwareupdatepunkten eine Kommunikation stattfinden.  

 Unter den folgenden Umständen muss die Firewall möglicherweise so konfiguriert werden, dass die von WSUS verwendeten HTTP- bzw. HTTPS-Ports zugelassen werden: wenn sich zwischen dem Configuration Manager-Softwareupdatepunkt und dem Internet eine Unternehmensfirewall befindet, wenn es einen Softwareupdatepunkt und eine zugehörige Upstreamsynchronisierungsquelle gibt, oder wenn es zusätzliche Softwareupdatepunkte gibt. Die Verbindung mit Microsoft Update ist immer für die Verwendung von Port 80 für HTTP und von Port 443 für HTTPS konfiguriert. Für die Verbindung zwischen WSUS auf dem Softwareupdatepunkt an einem untergeordneten Standort und WSUS auf dem Softwareupdatepunkt am übergeordneten Standort können Sie einen benutzerdefinierten Port verwenden. Wenn die Verbindung aufgrund ihrer Sicherheitsrichtlinie nicht möglich ist, müssen Sie die Export-/Import-Synchronisierungsmethode verwenden. Weitere Informationen finden Sie im Abschnitt [Synchronisierungsquelle](#BKMK_SyncSource) in diesem Thema. Weitere Informationen zu den Ports, die von WSUS verwendet werden, finden Sie unter [Bestimmen der Porteinstellungen für WSUS in System Center Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  

#### <a name="restrict-access-to-specific-domains"></a>Einschränken des Zugriffs auf bestimmte Domänen  
 Wenn es in Ihrer Organisation nicht zulässig ist, dass die Ports und Protokolle für alle Adressen der Firewall zwischen dem aktiven Softwareupdatepunkt und dem Internet offen sind, können Sie den Zugriff auf die folgenden Domänen beschränken, damit von WSUS und „Automatische Updates“ eine Verbindung mit Microsoft Update hergestellt werden kann:  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 Wenn es untergeordnete Standorte mit einem Softwareupdatepunkt bzw. einen aktiven internetbasierten Remote-Softwareupdatepunkt an einem Standort gibt, müssen die folgenden Adressen möglicherweise ebenfalls der Firewall zwischen den beiden Standortsystemen hinzugefügt werden:  

 **Softwareupdatepunkt am untergeordneten Standort**  

-   http://<*FQDN für Softwareupdatepunkts an untergeordnetem Standort*>  

-   https://<*FQDN des Softwareupdatepunkts an untergeordnetem Standort*>  

-   http://<*FQDN des Softwareupdatepunkts an übergeordnetem Standort*>  

-   https://<*FQDN des Softwareupdatepunkts an übergeordnetem Standort*>  

##  <a name="BKMK_SyncSettings"></a> Planen der Synchronisierungseinstellungen  
 Bei der Softwareupdatesynchronisierung in Configuration Manager werden die Metadaten für Softwareupdates ausgehend von den von Ihnen konfigurierten Kriterien abgerufen. Die von Microsoft Update stammenden Softwareupdates werden vom Standort der obersten Ebene in der Hierarchie, vom Standort der zentralen Verwaltung oder von einem eigenständigen primären Standort synchronisiert. Sie haben die Möglichkeit, den Softwareupdatepunkt am Standort der obersten Ebene so zu konfigurieren, dass er mit einem vorhandenen WSUS-Server, der sich nicht in der Configuration Manager-Hierarchie befindet, synchronisiert wird. Von untergeordneten primären Standorten werden Metadaten für Softwareupdates synchronisiert, die vom Softwareupdatepunkt am Standort der zentralen Verwaltung stammen. Planen Sie mithilfe dieses Abschnitts die Synchronisierungseinstellungen, bevor Sie einen Softwareupdatepunkt installieren und konfigurieren.  

###  <a name="BKMK_SyncSource"></a> Synchronisierungsquelle  
 In den Einstellungen für die Synchronisierungsquelle des Softwareupdatepunkts wird angegeben, von welchem Ort die Metadaten für Softwareupdates vom Softwareupdatepunkt abgerufen werden und ob während des Synchronisierungsprozesses WSUS-Berichterstattungsereignisse erstellt werden sollen.  

-   **Synchronisierungsquelle:** Die Synchronisierungsquelle für Microsoft Update wird standardmäßig vom Softwareupdatepunkt am Standort der obersten Ebene konfiguriert. Sie haben die Möglichkeit, den Standort der obersten Ebene mit einem vorhandenen WSUS-Server zu synchronisieren. Vom Softwareupdatepunkt an einem untergeordneten primären Standort wird die Synchronisierungsquelle standardmäßig als Softwareupdatepunkt des Standorts der zentralen Verwaltung konfiguriert.  

    > [!NOTE]  
    >  Der erste Softwareupdatepunkt, den Sie an einem primären Standort installieren und der als Standard-Softwareupdatepunkt dient, wird mit dem Standort der zentralen Verwaltung synchronisiert. Weitere Softwareupdatepunkte am primären Standort werden mit dem Standard-Softwareupdatepunkts am primären Standort synchronisiert.  

     Wenn ein Softwareupdatepunkt von Microsoft Update oder dem Upstream-Updateserver getrennt ist, können Sie die Synchronisierungsquelle so konfigurieren, dass die Synchronisierung nicht mit einer konfigurierten Synchronisierungsquelle erfolgt, sondern stattdessen die Export- und Importfunktion des Tools „WSUSUtil“ verwendet wird. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates bei einem getrennten Softwareupdatepunkt](../get-started/synchronize-software-updates-disconnected.md).  

-   **WSUS-Berichterstattungsereignisse:** Der Windows Update-Agent auf Clientcomputern kann Ereignismeldungen erstellen, die für die WSUS-Berichterstattung verwendet werden. Diese Ereignisse werden nicht von Softwareupdates in Configuration Manager verwendet. Die Option **Keine WSUS-Berichterstellungsereignisse erstellen** ist daher standardmäßig ausgewählt. Wenn diese Ereignisse nicht erstellt werden, sollte der Clientcomputer lediglich während der Softwareupdatebewertung und Kompatibilitätsüberprüfung eine Verbindung mit dem WSUS-Server herstellen. Wenn diese Ereignisse für die Berichterstellung außerhalb der Softwareupdates in Configuration Manager benötigt werden, müssen Sie diese Einstellung ändern, damit WSUS-Berichterstellungsereignisse erstellt werden können.  

###  <a name="BKMK_SyncSchedule"></a> Synchronisierungszeitplan  
 Sie können den Synchronisierungszeitplan nur auf dem Softwareupdatepunkt am Standort der obersten Ebene in der Configuration Manager-Hierarchie konfigurieren. Wenn Sie den Synchronisierungszeitplan konfigurieren, findet die Synchronisierung des Softwareupdatepunkts mit der Synchronisierungsquelle zum angegebenen Zeitpunkt statt. Mit einem benutzerdefinierten Zeitplan können Sie Softwareupdates zu einem Zeitpunkt synchronisieren, zu dem die Anforderungen des WSUS-Servers, Standortservers und Netzwerks gering sind, beispielsweise jede Woche an einem bestimmten Tag um 02:00 Uhr. Alternativ kann die Synchronisierung am Standort der oberste Ebene mit der Aktion **Softwareupdates synchronisieren** initiiert werden. Diese Aktion befindet sich im Knoten **Alle Softwareupdates** oder **Softwareupdategruppen** in der Configuration Manager-Konsole.  

> [!TIP]  
>  Planen Sie die Ausführung der Softwareupdatesynchronisierung in einem für Ihre Umgebung geeigneten Zeitrahmen. Eine Möglichkeit besteht darin, den Zeitplan so zu konfigurieren, dass die Softwareupdatesynchronisierung kurz nach der Veröffentlichung der Microsoft-Sicherheitsupdates jeweils am zweiten Dienstag eines Monats („Patch-Dienstag“) ausgeführt wird. Eine andere Möglichkeit besteht darin, den Zeitplan so zu konfigurieren, dass die Softwareupdatesynchronisierung täglich ausgeführt wird, wenn Sie mithilfe von Softwareupdates Endpoint Protection-Definitions- und Modulupdates bereitstellen.  

 Nach dem erfolgreichen Abschluss der Synchronisierung durch den Softwareupdatepunkt wird eine Synchronisierungsanforderung an untergeordnete Standorte gesendet. Eine Synchronisierungsanforderung wird an alle Softwareupdatepunkte gesendet, wenn es an einem primären Standort weitere Softwareupdatepunkte gibt. Der Prozess wird an jedem Standort der Hierarchie wiederholt.  

###  <a name="BKMK_UpdateClassifications"></a> Updateklassifizierungen  
 Jedes Softwareupdate ist mit einer Updateklassifizierung definiert, die bei der Einteilung in verschiedene Updatearten behilflich ist. Bei der Synchronisierung werden die Metadaten der Softwareupdates für die angegebenen Klassifizierungen synchronisiert. Mit Configuration Manager können Sie Softwareupdates mit folgenden Updateklassifizierungen synchronisieren:  

-   **Wichtige Updates:** Hierbei handelt es sich um ein im großen Umfang freigegebenes Update für ein bestimmtes Problem, mit dem ein wichtiger, nicht sicherheitsrelevanter Fehler behoben wird.  

-   **Definitionsupdates:** Hierbei handelt es sich um ein Update für Virus- oder andere Definitionsdateien.  

-   **Feature Packs:** Hierbei handelt es sich um neue Produktfunktionen, die außerhalb einer Produktversion verteilt werden, und Funktionen, die in der Regel in der nächsten vollständigen Produktversion enthalten sind.  

-   **Sicherheitsupdates:** Hierbei handelt es sich um ein großen Umfang freigegebenes Update für ein produktspezifisches, sicherheitsrelevantes Problem.  

-   **Service Packs:** Hierbei handelt es sich um einen kumulativen Satz von Hotfixes, die auf eine Anwendung angewendet werden. Diese Hotfixes können Sicherheitsupdates, wichtige Updates, Softwareupdates usw. umfassen.  

-   **Tools:** Hierbei handelt es sich um ein Dienstprogramm oder Funktion, mit dem mindestens eine Aufgabe leichter ausgeführt werden kann.  

-   **Aktualisierungsrollups:** Hierbei handelt es sich um einen kumulativen Satz von Hotfixes, die gebündelt sind, um die Bereitstellung einfacher zu gestalten. Diese Hotfixes können Sicherheitsupdates, wichtige Updates, Updates usw. umfassen. Ein Aktualisierungsrollup betrifft in der Regel einen bestimmten Bereich, z. B. Sicherheit oder eine Produktkomponente.  

-   **Updates:** Hierbei handelt es sich um ein Update für eine gegenwärtig installierte Anwendung oder Datei.  

 Die Updateklassifizierungseinstellungen werden nur am Standort der obersten Ebene konfiguriert. Diese Einstellungen werden nicht auf dem Softwareupdatepunkt untergeordneter Standorte konfiguriert, da die Metadaten der Softwareupdates vom Standort der obersten Ebene auf untergeordnete primäre Standorte repliziert werden. Beim Auswählen der Updateklassifizierungen nimmt die Synchronisierung der Softwareupdate-Metadaten umso mehr Zeit in Anspruch, je mehr Klassifizierungen ausgewählt werden.  

> [!WARNING]  
>  Es wird empfohlen, die Auswahl sämtlicher Klassifizierungen aufzuheben, bevor Sie Softwareupdates zum ersten Mal synchronisieren. Wählen Sie die Klassifizierungen nach der Erstsynchronisierung in den Eigenschaften der Softwareupdatepunktkomponente aus, und initiieren Sie dann die Synchronisierung erneut.  

###  <a name="BKMK_UpdateProducts"></a> Produkte  
 Anhand der Metadaten für die einzelnen Softwareupdates werden ein oder mehrere Produkte definiert, für die das Update gilt. Ein Produkt ist eine bestimmte Edition eines Betriebssystems oder einer Anwendung. Ein Beispiel für ein Produkt ist Microsoft Windows Server 2008. Eine Produktfamilie ist das Basisbetriebssystem bzw. die Basisanwendung, von dem bzw. der die einzelnen Produkte abgeleitet sind. Ein Beispiel für eine Produktfamilie ist Microsoft Windows. Microsoft Windows Server 2008 ist ein Mitglied dieser Produktfamilie. Sie können eine Produktfamilie oder einzelne Produkte innerhalb einer Produktfamilie angeben.  

 Wenn Softwareupdates auf mehrere Produkte anwendbar sind, und mindestens eines der Produkte für die Synchronisierung ausgewählt wird, werden sämtliche Produkte in der Configuration Manager-Konsole angezeigt, auch wenn einige Produkte nicht ausgewählt wurden. Wenn z. B. Windows Server 2012 das einzige Betriebssystem ist, das Sie abonniert haben, und ein Softwareupdate für Windows Server 2012 und Windows Server 2012 Datacenter Edition gilt, werden beide Produkte in der Standortdatenbank angezeigt.  

 Die Produkteinstellungen werden nur am Standort der obersten Ebene konfiguriert. Diese Einstellungen werden nicht auf dem Softwareupdatepunkt für untergeordnete Standorte konfiguriert, da die Metadaten der Softwareupdates vom Standort der obersten Ebene auf untergeordnete primäre Standorte repliziert werden. Bedenken Sie, dass beim Auswählen der Produkte die Synchronisierung der Softwareupdate-Metadaten umso mehr Zeit in Anspruch nimmt, je mehr Produkte ausgewählt werden.  

> [!IMPORTANT]  
>  Configuration Manager speichert eine Liste der Produkte und Produktfamilien, aus denen Sie bei der Erstinstallation des Softwareupdatepunkts eine Auswahl treffen können. Produkte und Produktfamilien, die nach der Veröffentlichung von Configuration Manager freigegeben werden, können möglicherweise erst ausgewählt werden, nachdem Sie die Softwareupdatesynchronisierung abgeschlossen haben. Dabei wird die Liste der verfügbaren Produkte und Produktfamilien, aus denen Sie auswählen können, aktualisiert. Es empfiehlt sich, die Auswahl sämtlicher Produkte aufzuheben, bevor Sie Softwareupdates zum ersten Mal synchronisieren. Wählen Sie die Produkte nach der Erstsynchronisierung in den Eigenschaften der Softwareupdatepunkt-Komponente aus, und initiieren Sie die Synchronisierung dann erneut.  

###  <a name="BKMK_SupersedenceRules"></a> Ablösungsregeln  
 Mit einem Softwareupdate, das ein anderes Softwareupdate ablöst, werden in der Regel folgende Aktionen ausgeführt:  

-   Erweiterung, Verbesserung oder Aktualisierung der Korrekturen, die von früher herausgegebenen Updates bereitgestellt wurden.  

-   Steigerung der Effizienz des abgelösten Updatedateipakets, das auf Clientcomputern installiert wird, sofern die Installation des Updates genehmigt wird. Beispielsweise kann das abgelöste Update Dateien enthalten, die für die Korrektur oder die vom neuen Update unterstützten Betriebssysteme nicht mehr relevant sind. Diese Dateien sind dann im Dateipaket des neuen Updates nicht mehr enthalten.  

-   Ausführung eines Updates für neuere Produktversionen. Anders ausgedrückt: Es werden Versionen aktualisiert, die für ältere Versionen oder Konfigurationen eines Produkts nicht mehr gültig sind. Updates können außerdem durch andere Updates abgelöst werden, wenn zur Erweiterung der Sprachunterstützung entsprechende Änderungen vorgenommen wurden. Beispielsweise wäre es möglich, dass in einer späteren Version eines Produktupdates für Microsoft Office ein älteres Betriebssystem nicht mehr unterstützt, dafür aber in der Erstversion des Updates die Sprachunterstützung erweitert wird.  

 In den Eigenschaften für den Softwareupdatepunkt können Sie angeben, dass abgelöste Softwareupdates sofort ablaufen sollen. Hierdurch verhindern Sie, dass diese Softwareupdates in neue Bereitstellungen eingeschlossen werden. Zudem wird bei bestehenden Bereitstellungen durch eine Kennzeichnung darauf hingewiesen, dass sie mindestens ein abgelöstes Softwareupdate enthalten. Sie können auch angeben, dass die abgelösten Softwareupdates erst nach einem bestimmten Zeitraum ablaufen. In diesem Fall können Sie diese Updates weiterhin bereitstellen. Die Bereitstellung eines abgelösten Softwareupdates kann in folgenden Situationen empfehlenswert sein:  

-   Von einem ablösenden Softwareupdate werden nur neuere Versionen eines Betriebssystems unterstützt, und auf einigen Clientcomputern werden frühere Versionen des Betriebssystems ausgeführt.  

-   Die Anwendbarkeit eines ablösenden Softwareupdates ist stärker eingeschränkt als die des abzulösenden Softwareupdates. Das ablösende Softwareupdate wäre dadurch für einige Clientcomputer ungeeignet.  

-   Die Bereitstellung eines ablösenden Softwareupdates wurde in Ihrer Produktionsumgebung nicht genehmigt.  

    > [!NOTE]  
    > Wenn Configuration Manager ein abgelöstes Softwareupdate auf **Expired** (Abgelaufen) festlegt, wird das Update in WSUS nicht auf **Declined** (Abgelehnt) festgelegt. Wenn die WSUS-Bereinigungsaufgabe ausgeführt wird, werden jedoch die Updates, die in Configuration Manager auf **Expired** (Abgelaufen) festgelegt sind, auf dem WSUS-Server auf **Declined** (Abgelehnt) festgelegt. Dies führt dazu, dass der Windows Update-Agent auf Computern nicht mehr nach diesen Updates sucht. Dies bedeutet, dass Clients so lange nach einem abgelaufenen Update suchen, bis die Bereinigungsaufgabe ausgeführt wurde. Informationen zur WSUS-Bereinigungsaufgabe finden Sie unter [Wartung für Softwareupdates](/sccm/sum/deploy-use/software-updates-maintenance).

###  <a name="BKMK_UpdateLanguages"></a> Sprachen  
 Über die Spracheinstellungen für den Softwareupdatepunkt können Sie die Sprachen konfigurieren, für die die Übersichtsdetails (Softwareupdate-Metadaten) für Softwareupdates synchronisiert werden sollen, und die Sprachen, in denen die Softwareupdatedateien heruntergeladen werden sollen.  

#### <a name="software-update-file"></a>Softwareupdatedatei  
 Die Sprachen, die Sie in den Eigenschaften des Softwareupdatepunkts für die Einstellung **Softwareupdatedatei** konfigurieren, sind beim Herunterladen von Softwareupdates auf einen Standort standardmäßig verfügbar. Sie können anpassen, welche Sprachen beim Herunterladen oder Bereitstellen von Softwareupdates standardmäßig ausgewählt sind. Während des Herunterladens werden die verfügbaren Softwareupdatedateien für die konfigurierten Sprachen an den Quellspeicherort des Bereitstellungspakets heruntergeladen, wenn die Softwareupdatedateien in der ausgewählten Sprache verfügbar sind. Anschließend werden sie in die Inhaltsbibliothek auf dem Standortserver kopiert und auf die für das Paket konfigurierten Verteilungspunkte kopiert.  

 Die Spracheinstellungen der Softwareupdatedatei sollten mit den Sprachen konfiguriert werden, die in Ihrer Umgebung am häufigsten verwendet werden. Beispiel: Wenn die Betriebssysteme oder Anwendungen auf den Clientcomputern, die dem Standort zugewiesen sind, überwiegend in den Sprachen Deutsch und Englisch und nur zu einem geringen Teil in anderen Sprachen verwendet werden, wählen Sie beim Herunterladen oder Bereitstellen des Softwareupdates in der Spalte **Softwareupdatedatei** die Sprachen Deutsch und Englisch aus und heben die Auswahl der anderen Sprachen auf. So können Sie in den Assistenten zum Bereitstellen und Herunterladen auf der Seite **Sprachauswahl** die Standardeinstellungen verwenden. Dadurch wird auch verhindert, dass nicht benötigte Updatedateien heruntergeladen werden. Diese Einstellung wird auf jedem Softwareupdatepunkt in der Configuration Manager-Hierarchie konfiguriert.  

#### <a name="summary-details"></a>Übersichtsdetails  
 Während des Synchronisierungsprozesses werden die Übersichtsdetails (Softwareupdate-Metadaten) für Softwareupdates in den angegebenen Sprachen aktualisiert. Die Metadaten enthalten Informationen zum Softwareupdate wie Name, Beschreibung, vom Update unterstützte Produkte, Updateklassifizierung, Artikel-ID, Download-URL, Anwendbarkeitsregeln usw.  

 Die Übersichtsdetails werden nur am Standort der obersten Ebene konfiguriert. Sie werden nicht auf dem aktiven Softwareupdatepunkt für untergeordnete Standorte konfiguriert, da die Metadaten der Softwareupdates mithilfe von dateibasierter Replikation vom Standort der zentralen Verwaltung auf diese Standorte repliziert werden. Wählen Sie für die Übersichtsdetails nur die in der Umgebung erforderlichen Sprachen aus. Je mehr Sprachen ausgewählt sind, desto länger dauert die Synchronisierung der Softwareupdate-Metadaten. Configuration Manager zeigt die Metadaten der Softwareupdates im Gebietsschema des Betriebssystems an, unter dem die Configuration Manager-Konsole ausgeführt wird. Falls die lokalisierten Eigenschaften der Softwareupdates im Gebietsschema des Betriebssystems nicht verfügbar sind, werden die Softwareupdateinformationen in Englisch angezeigt.  

> [!IMPORTANT]  
>  Achten Sie darauf, alle Sprachen für Übersichtsdetails auszuwählen, die in Ihrer Configuration Manager-Hierarchie erforderlich sind. Beim Synchronisieren des Softwareupdatepunkts am Standort der obersten Ebene mit der Synchronisierungsquelle wird anhand der Sprachen für Übersichtsdetails bestimmt, welche Softwareupdate-Metadaten abgerufen werden. Wenn Sie die Sprachen für Übersichtsdetails ändern, nachdem die Synchronisierung mindestens einmal ausgeführt wurde, werden die Metadaten für die geänderten Übersichtsdetailsprachen nur für neue und aktualisierte Softwareupdates abgerufen. Für die bereits synchronisierten Softwareupdates werden neue Metadaten für die geänderten Sprachen nur abgerufen, wenn auf der Synchronisierungsquelle eine Änderung des Softwareupdates vorgenommen wurde.  

##  <a name="BKMK_MaintenanceWindow"></a> Planung eines Wartungsfensters für Softwareupdates  
 Sie können ein für die Installation von Softwareupdates reserviertes Wartungsfenster hinzufügen. Dadurch können Sie ein allgemeines Wartungsfenster und ein anderes Wartungsfenster für Softwareupdates konfigurieren. Wenn ein allgemeines Wartungsfenster und ein Wartungsfenster für Softwareupdates konfiguriert sind, werden Softwareupdates auf Clients nur während des Wartungsfensters für Softwareupdates installiert. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="BKMK_RestartOptions"></a> Neustartoptionen für Windows 10-Clients nach der Installation von Softwareupdates
Wenn ein Softwareupdate, das einen Neustart benötigt, mit Configuration Manager bereitgestellt und auf einem Computer installiert wird, wird ein ausstehender Neustart geplant, und das Neustartdialogfeld wird angezeigt.

Ab Version 1606 von Configuration Manager ist die Option **Aktualisieren und neu starten**sowie **Aktualisieren und herunterfahren** für Computer unter Windows 10 in den Windows-Energieoptionen verfügbar und zwar für jeden ausstehenden Neustart eines Configuration Manager-Softwareupdates. Nach der Verwendung einer dieser Optionen, wird das Dialogfeld „Neustart“ nach dem Neustart des Computers nicht angezeigt.

Wenn in früheren Versionen von Configuration Manager für die unter Windows 8 oder höher laufenden Computer ein Neustart aussteht, und wenn Sie den Computer mithilfe der Windows Power-Optionen (anstatt über den Neustartdialog) herunterfahren oder neu starten, wird der Neustartdialog auch nach dem Neustart weiterhin angezeigt. Der Computer muss trotzdem innerhalb der konfigurierten Zeitspanne neu gestartet werden.

## <a name="next-steps"></a>Nächste Schritte
Lesen Sie [Vorbereiten der Softwareupdateverwaltung](../get-started/prepare-for-software-updates-management.md), sobald Sie Softwareupdates planen.
