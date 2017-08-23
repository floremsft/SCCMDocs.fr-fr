---
title: Automatisches Bereitstellen von Softwareupdates | Microsoft Docs
description: "Stellen Sie automatisch Softwareupdates durch Hinzufügen neuer Updates zu einer Updategruppe bereit, die mit einer aktiven Bereitstellung verknüpft ist, oder mithilfe von ADRs."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 804a9d7a32cfbdb498c6748c5d99a1874261c231
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_AutoDeploy"></a> Automatisches Bereitstellen von Softwareupdates  

*Gilt für: System Center Configuration Manager (Current Branch)*

 Softwareupdates können automatisch bereitgestellt werden. Zu diesem Zweck fügen Sie entweder einer Updategruppe mit einer aktiven Bereitstellung neue Softwareupdates hinzu, oder Sie verwenden automatische Bereitstellungsregeln (ADR). Die Bereitstellung per ADR eignet sich insbesondere für monatliche Softwareupdates („Patch-Dienstag“) und für die Verwaltung von Definitionsupdates. Wenn Sie Hilfe bei der Ermittlung der für Sie richtigen Bereitstellungsmethode benötigen, lesen Sie [Bereitstellen von Softwareupdates](deploy-software-updates.md).

##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Hinzufügen von Softwareupdates zu einer bereitgestellten Updategruppe  
Nachdem Sie eine Softwareupdategruppe erstellt und bereitgestellt haben, können Sie ihr Softwareupdates hinzufügen. Diese Updates werden dann ebenfalls automatisch bereitgestellt.  

> [!IMPORTANT]  
>  Wenn Sie einer vorhandenen, bereits bereitgestellten Softwareupdategruppe Softwareupdates hinzufügen, kann dieser Vorgang ein paar Minuten dauern.  

Gehen Sie wie folgt vor, um einer vorhandenen Updategruppe Softwareupdates hinzuzufügen.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>So fügen Sie Softwareupdates einer vorhandenen Softwareupdategruppe hinzu  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Softwareupdates**.  

2.  Wählen Sie die Softwareupdates aus, die der neuen Softwareupdategruppe hinzugefügt werden sollen.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Mitgliedschaft bearbeiten**.  

4.  Wählen Sie die Softwareupdategruppe aus, der Sie die Softwareupdates als Mitglieder hinzufügen möchten.  

5.  Klicken Sie auf den Knoten **Softwareupdategruppen** , um die Softwareupdategruppe anzuzeigen.  

6.  Klicken Sie auf die Softwareupdategruppe. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Mitglieder anzeigen** , um eine Liste der Softwareupdates in der Gruppe anzuzeigen.  

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Erstellen einer automatischen Bereitstellungsregel  
Sie können Softwareupdates mithilfe einer automatischen Bereitstellungsregel automatisch genehmigen und bereitstellen. Sie können festlegen, dass die Regel bei jeder Ausführung Softwareupdates zu einer neuen Softwareupdategruppe hinzufügt oder Softwareupdates zu einer vorhandenen Gruppe hinzufügt. Wenn eine Regel ausgeführt wird und Softwareupdates zu einer vorhandenen Gruppe hinzufügt, entfernt die Regel alle Softwareupdates aus der Gruppe und fügt dann die Softwareupdates, die die definierten Kriterien erfüllen, zur Gruppe hinzu. Um z. B. eine automatische Bereitstellungsregel auszuführen, die jeden Tag nach neu veröffentlichten Softwareupdates sucht und diese für Clients bereitstellt, müssen Sie die Option zum Erstellen einer neuen Softwareupdategruppe anstatt zum Hinzufügen von Softwareupdates zu einer vorhandenen Gruppe auswählen.  

> [!WARNING]  
>  Überprüfen Sie, ob die Softwareupdatesynchronisierung am Standort abgeschlossen ist, und erstellen Sie erst dann die erste automatische Bereitstellungsregel. Dies ist insbesondere wichtig, wenn Sie Configuration Manager in einer anderen Sprache als Englisch ausführen. Die Softwareupdateklassifizierungen werden vor der ersten Synchronisierung in Englisch angezeigt und nach dem Abschluss der Softwareupdatesynchronisierung in der lokalisierten Sprache. Regeln, die Sie vor der Synchronisierung der Softwareupdates erstellen, können nach der Synchronisierung möglicherweise nicht verwendet werden, da die Textzeichenfolgen eventuell nicht übereinstimmen.  

 Gehen Sie wie nachfolgend beschrieben vor, um eine automatische Bereitstellungsregel zu erstellen.  

#### <a name="to-create-an-adr"></a>So erstellen Sie eine automatische Bereitstellungsregel  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** **Übersicht** > **Softwareupdates** > **Automatische Bereitstellungsregeln**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Automatische Bereitstellungsregel erstellen**. Der Assistent zum Erstellen automatischer Bereitstellungsregeln wird geöffnet.  

3.  Konfigurieren Sie auf der Seite **Allgemein** die folgenden Einstellungen:  

    -   **Name**: Geben Sie den Namen der automatischen Bereitstellungsregel an. Der Name muss eindeutig sein, das Ziel der Regel angeben und sich am Configuration Manager-Standort leicht von anderen Namen unterscheiden lassen.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der automatischen Bereitstellungsregel an. Die Beschreibung muss einen Überblick über die Bereitstellungsregel und alle anderen relevanten Informationen umfassen, die die Identifizierung und Unterscheidung der Regel am Configuration Manager-Standort erleichtern. Das Feld „Beschreibung“ ist optional, hat eine Begrenzung auf 256 Zeichen und ist standardmäßig leer.  

    -   **Bereitstellungsvorlage auswählen**: Geben Sie an, ob eine zuvor gespeicherte Bereitstellungsvorlage angewendet werden soll. Sie können eine Bereitstellungsvorlage konfigurieren, die mehrere allgemeine Bereitstellungseigenschaften für Softwareupdates umfasst und bei der Erstellung automatischer Bereitstellungsregeln eingesetzt werden kann. Mit diesen Vorlagen sorgen Sie nicht nur für Konsistenz mit ähnlichen Bereitstellungen, sondern verringern auch Ihren Zeitaufwand.  

         Im Assistenten zum Erstellen automatischer Bereitstellungsregeln stehen zwei integrierte Vorlagen für die Softwareupdatebereitstellung zur Auswahl. Die Vorlage **Definitionsupdates** enthält allgemeine Einstellungen für die Bereitstellung von Softwaredefinitionsupdates. Die Vorlage **Patch-Dienstag** enthält allgemeine Einstellungen für die monatliche Bereitstellung von Softwaredefinitionsupdates.  

    -   **Sammlung**: Gibt die für die Bereitstellung zu verwendende Zielsammlung an. Mitglieder dieser Sammlung erhalten die in der Bereitstellung definierten Softwareupdates.  

    -   Entscheiden Sie, ob Softwareupdates einer neuen oder bereits vorhandenen Softwareupdategruppe hinzugefügt werden sollen. In den meisten Fällen dürften Sie sich dafür entscheiden, beim Ausführen der automatischen Bereitstellungsregel eine neue Softwareupdategruppe zu erstellen. Falls für die Regel ein aggressiverer Zeitplan gilt, bietet es sich jedoch an, eine vorhandene Gruppe auszuwählen. Wenn Sie die Regel beispielsweise täglich für Definitionsupdates ausführen, können Sie die Softwareupdates einer vorhandenen Softwareupdategruppe hinzufügen.  

    -   **Bereitstellung nach Ausführung dieser Regel aktivieren**: Geben Sie an, ob die Softwareupdatebereitstellung nach der Ausführung der automatischen Bereitstellungsregel aktiviert werden soll. Hinsichtlich dieser Spezifikation ist Folgendes zu beachten:  

        -   Wenn Sie die Bereitstellung aktivieren, werden die Softwareupdates, die die in der Regel definierten Kriterien erfüllen, einer Softwareupdategruppe hinzugefügt. Dann wird der Inhalt für die Softwareupdates nach Bedarf heruntergeladen und auf die angegebenen Verteilungspunkte kopiert. Schließlich werden die Softwareupdates den Clients in der Zielsammlung bereitgestellt.  

        -   Wenn Sie die Bereitstellung nicht aktivieren, werden die Softwareupdates, die die in der Regel definierten Kriterien erfüllen, einer Softwareupdategruppe hinzugefügt. Die Bereitstellungsrichtlinie für Softwareupdates ist zwar konfiguriert, aber die Softwareupdates werden nicht heruntergeladen oder den Clients bereitgestellt. Sie haben somit Zeit, die Bereitstellung der Softwareupdates vorzubereiten, zu prüfen, ob die den Kriterien entsprechenden Softwareupdates geeignet sind, sowie die Bereitstellung zu einem späteren Zeitpunkt zu aktivieren.  

4.  Konfigurieren Sie auf der Seite Bereitstellungseinstellungen die folgenden Einstellungen:  

    -   **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren**: Gibt an, ob Wake-On-LAN am Stichtag aktiviert werden soll, damit Aktivierungspakete an Computer gesendet werden, für die mindestens eines der in der Bereitstellung enthaltenen Softwareupdates erforderlich ist. Alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, werden aktiviert, damit die Softwareupdateinstallation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert.  

        > [!WARNING]  
        >  Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.  

    -   **Detailstufe**: Geben Sie die Detailstufe für die von den Clientcomputern zurückgegebenen Zustandsmeldungen an.  

        > [!IMPORTANT]  
        >  Stellen Sie die Detailstufe beim Bereitstellen von Definitionsupdates auf **Nur Fehler** ein, damit vom Client nur dann eine Zustandsmeldung zurückgegeben wird, wenn ein Definitionsupdate nicht an den Client geliefert werden kann. Andernfalls gehen vom Client zahlreiche Zustandsmeldungen ein, die sich auf die Leistung des Standortservers auswirken können.  

    -   **Lizenzbedingungen**: Geben Sie an, ob Softwareupdates mit zugehörigen Lizenzbedingungen automatisch bereitgestellt werden sollen. Einige Softwareupdates enthalten Lizenzbedingungen, z. B. Service Packs. Bei der automatischen Bereitstellung von Softwareupdates werden die Lizenzbedingungen nicht angezeigt, und es gibt keine Option zum Annehmen der Lizenzbedingungen. Nach Wunsch können Sie alle Softwareupdates unabhängig von den zugehörigen Lizenzbedingungen automatisch bereitstellen. Sie können aber auch nur Softwareupdates bereitstellen, für die es keine zugehörigen Lizenzbedingungen gibt.  

        > [!NOTE]  
        >  Zum Überprüfen der Lizenzbedingungen eines Softwareupdates wählen Sie das Softwareupdate im Arbeitsbereich **Softwarebibliothek** im Knoten **Alle Softwareupdates** aus. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Lizenz lesen**.  
        >   
        >  Zum Identifizieren der Softwareupdates mit zugehörigen Lizenzbedingungen fügen Sie dem Ergebnisbereich im Knoten **Alle Softwareupdates** die Spalte **Lizenzbedingungen** hinzu. Klicken Sie dann auf die Spaltenüberschrift, um die Spalte nach Softwareupdates mit Lizenzbedingungen zu sortieren.  

5.  Konfigurieren Sie auf der Seite „Softwareupdates“ die Kriterien für die Softwareupdates, die von der automatischen Bereitstellungsregel abgerufen und der Softwareupdategruppe hinzugefügt werden.  

    > [!IMPORTANT]  
    >  Das Limit für Softwareupdates in einer automatischen Bereitstellungsregel ist 1.000. Wenn Sie sicherstellen möchten, dass mit den auf dieser Seite angegebenen Kriterien weniger als 1000 Softwareupdates abgerufen werden, empfiehlt es sich, die gleichen Kriterien im Arbeitsbereich **Softwarebibliothek** im Knoten **Alle Softwareupdates** festzulegen.  

    > [!NOTE]
    > Ab Version 1610 von Configuration Manager können Sie nach Inhaltsgrößen für Softwareupdates in automatischen Bereitstellungsregeln filtern. Sie können z.B. den Filter **Inhaltsgröße (KB)** auf **< 2048** festlegen, um nur die Softwareupdates herunterzuladen, die kleiner als 2 MB sind. Mit diesem Filter wird verhindert, dass große Softwareupdates automatisch heruntergeladen werden, um die vereinfachte Windows-Wartung vorheriger Versionen zu unterstützen, wenn die Bandbreite eingeschränkt ist. Details finden Sie unter [Configuration Manager und vereinfachte Windows-Wartung auf vorherigen Betriebssystemebene](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

6.  Geben Sie auf der Seite „Auswertungszeitplan“ an, ob die Ausführung der automatischen Bereitstellungsregel nach einem Zeitplan aktiviert werden soll. Ist dies der Fall, klicken Sie auf **Anpassen** , und legen Sie den Wiederholungszeitplan fest.  

    > [!IMPORTANT]  
    >  Der Zeitplan für die Synchronisierung des Softwareupdatepunkts wird angezeigt, damit Sie die Häufigkeit des Auswertungszeitplans leichter festlegen können. Legen Sie für den Auswertungszeitplan niemals eine Häufigkeit fest, die über den Zeitplan der Softwareupdatesynchronisierung hinausgeht. Die für den Zeitplan konfigurierte Startzeit basiert auf der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird.  

    > [!NOTE]  
    >  Sie können die automatische Bereitstellungsregel manuell ausführen. Wählen Sie dazu die Regel aus, und klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Automatische Bereitstellungsregel** auf **Jetzt ausführen** . Führen Sie die automatische Bereitstellungsregel erst manuell aus, nachdem Sie überprüft haben, ob die Softwareupdatesynchronisierung seit der letzten Ausführung der Regel ausgeführt wurde.  

    > [!IMPORTANT]  
    >  Die Auswertung der automatischen Bereitstellungsregel kann dreimal täglich ausgeführt werden.  

7.  Konfigurieren Sie auf der Seite Bereitstellungszeitplan die folgenden Einstellungen:  

    -   **Auswertung planen**: Geben Sie an, ob die verfügbare Zeit und die Installationsstichtage von Configuration Manager mit UTC oder der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird, ausgewertet werden sollen.  

        > [!NOTE]  
        >  Wenn Sie die Ortszeit auswählen und dann **So bald wie möglich** für **Zeitpunkt der Verfügbarkeit der Software** oder **Installationsstichtag** auswählen, wird die aktuelle Uhrzeit auf dem Computer mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind, oder auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.  

    -   **Zeitpunkt der Verfügbarkeit der Software**: Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung stehen:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clientcomputern so bald wie möglich zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung ausgewählt ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Die zur Installation verfügbaren Updates können dann abgerufen werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clientcomputern zu einem bestimmten Termin (Datum und Uhrzeit) zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung aktiviert ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem konfigurierten Termin (Datum und Uhrzeit) für die Installation zur Verfügung.  

    -   **Installationsstichtag**: Wählen Sie eine der folgenden Einstellungen aus, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung so bald wie möglich automatisch installiert werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung zu einem bestimmten Termin (Datum und Uhrzeit) automatisch installiert werden. Configuration Manager bestimmt den Stichtag zum Installieren von Softwareupdates durch Hinzufügen der konfigurierten Intervalle **Bestimmte Zeit** zu **Zeitpunkt der Verfügbarkeit der Software**.  

        > [!NOTE]  
        >  Der tatsächliche Installationsstichtag ergibt sich aus der Addition des angezeigten Stichtags und eines willkürlichen Zeitraums von bis zu 2 Stunden. Dadurch werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Softwareupdates in der Bereitstellung durch alle Clientcomputer in der Zielsammlung einhergehen.  
        >   
        >  Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für den **Computer-Agent** konfigurieren, um die zufällige Verzögerung der Installation für die erforderlichen Softwareupdates zu deaktivieren. Weitere Informationen finden Sie unter [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. Konfigurieren Sie auf der Seite Benutzerfreundlichkeit die folgenden Einstellungen:  

    -   **Benutzerbenachrichtigungen**: Geben Sie an, ob zum vorgegebenen **Zeitpunkt der Verfügbarkeit der Software** auf dem Clientcomputer eine Benachrichtigung zu den Softwareupdates im Softwarecenter angezeigt werden soll. Geben Sie auch an, ob auf den Clientcomputern Benutzerbenachrichtigungen angezeigt werden sollen.  

    -   **Verhalten am Stichtag**: Geben Sie das gewünschte Verhalten am Stichtag der Softwareupdatebereitstellung an. Geben Sie an, ob die Softwareupdates in der Bereitstellung installiert werden sollen. Geben Sie auch, ob nach einer Softwareupdateinstallation unabhängig von einem konfigurierten Wartungsfenster ein Systemneustart ausgeführt werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Verhalten beim Geräteneustart**: Geben Sie an, ob nach der Installation der Softwareupdates ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn der Systemneustart zum Abschließen der Installation erforderlich ist.  

        > [!IMPORTANT]  
        >  Das Unterdrücken von Systemneustarts kann in Serverumgebungen oder in Fällen hilfreich sein, in denen Computer nach der Installation von Softwareupdates nicht standardmäßig neu gestartet werden sollen. Allerdings kann dies zu einem unsicheren Computerzustand führen. Durch Erzwingen eines Neustarts hingegen wird gewährleistet, dass die Softwareupdateinstallation umgehend abgeschlossen wird.  

    -   **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Beim Bereitstellen von Softwareupdates für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass das Softwareupdate auf dem temporären Overlay installiert wird und die Änderungen entweder später, am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

        > [!NOTE]  
        >  Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist.  

    - **Neubewertungsverhalten bei Softwareupdatebereitstellungen nach einem Neustart:** Ab Version 1606 von Configuration Manager können Sie mit dieser Einstellung die Bereitstellung von Softwareupdates so konfigurieren, dass Clients direkt nach dem Neustart im Anschluss an die Installation von Softwareupdates eine Complianceüberprüfung durchführen. So kann der Client nach zusätzlichen Softwareupdates suchen, die nach dem Neustart des Clients relevant werden, und diese im gleichen Wartungsfenster installieren (und so für Kompatibilität sorgen).

9. Geben Sie auf der Seite „Warnungen“ an, wie Configuration Manager und System Center Operations Manager Warnungen für diese Bereitstellung generieren sollen.  

    > [!NOTE]  
    >  Sie können die letzten Warnungen zu Softwareupdates im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** prüfen.  

10. Konfigurieren Sie auf der Seite Downloadeinstellungen die folgenden Einstellungen:  

    - Geben Sie an, ob die Softwareupdates vom Client heruntergeladen und installiert werden, wenn ein Client mit einer langsamen Netzwerkverbindung oder einer Fallbackinhaltsquelle vorliegt.  

    - Geben Sie an, ob die Softwareupdates vom Client von einem Fallbackverteilungspunkt heruntergeladen und installiert werden sollen, wenn der Inhalt für die Softwareupdates an einem bevorzugten Verteilungspunkt nicht verfügbar ist.  

    - **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob BranchCache beim Herunterladen von Inhalten verwendet werden soll. Weitere Informationen zu BranchCache finden Sie unter [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Inhalt von Microsoft Updates herunterladen, falls Softwareupdates in aktuellen oder benachbarten Begrenzungsgruppen oder in Standortbegrenzungsgruppen am Verteilungspunkt nicht verfügbar sind**: Wählen Sie diese Einstellung aus, damit Clients, die mit dem Intranet verbunden sind, Softwareupdates von Microsoft Update herunterladen, wenn keine Softwareupdates auf Verteilungspunkten verfügbar sind. Internetbasierte Clients können Softwareupdates immer von Microsoft Update herunterladen.

    - Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

    > [!NOTE]  
    >  Der Inhaltsort für die Softwareupdates in einer Bereitstellung wird von den Clients von einem Verwaltungspunkt angefordert. Das Downloadverhalten richtet sich danach, wie Sie den Verteilungspunkt, das Bereitstellungspaket und die Einstellungen auf dieser Seite konfiguriert haben. Weitere Informationen finden Sie unter [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Wählen Sie auf der Seite Bereitstellungspaket ein vorhandenes Bereitstellungspaket aus, oder erstellen Sie anhand der nachfolgenden Einstellungen ein neues Bereitstellungspaket:  

    1.  **Name**: Geben Sie den Namen des Bereitstellungspakets an. Dies muss ein eindeutiger Name sein, der den Paketinhalt beschreibt. Er ist auf 50 Zeichen begrenzt.  

    2.  **Beschreibung**: Geben Sie eine Beschreibung mit Informationen zum Bereitstellungspaket an. Die Beschreibung ist auf 127 Zeichen begrenzt.  

    3.  **Paketquelle**: Gibt den Speicherort der Quelldateien der Softwareupdates an.  Geben Sie für den Quellspeicherort einen Netzwerkpfad wie **\\\Server\Freigabename\Pfad**ein. Alternativ können Sie auf **Durchsuchen** klicken, um den Netzwerkpfad zu suchen. Sie müssen den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets erstellen, bevor Sie mit der nächsten Seite fortfahren.  

        > [!NOTE]  
        >  Der von Ihnen angegebene Quellspeicherort des Bereitstellungspakets kann von keinem anderen Softwarebereitstellungspaket verwendet werden.  

        > [!IMPORTANT]  
        >  Das Computerkonto für den SMS-Anbieter und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen über die NTFS-Berechtigung **Schreiben** für den Downloadort verfügen. Sie müssen den Zugriff auf den Downloadort beschränken, um das Risiko zu verringern, dass Angreifer die Quelldateien der Softwareupdates manipulieren.  

        > [!IMPORTANT]  
        >  Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt von der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.  

    4.  **Sendepriorität**: Geben Sie die Sendepriorität für das Bereitstellungspaket an. Configuration Manager verwendet Sendepriorität für das Bereitstellungspaket beim Senden des Pakets an Verteilungspunkte. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: „Hoch“, „Mittel“ oder „Niedrig“. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet.  

12. Geben Sie auf der Seite Verteilungspunkte die Verteilungspunkte oder Verteilungspunktgruppen an, auf denen die Softwareupdatedateien gehostet werden sollen. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurationen für Verteilungspunkte](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  Diese Seite ist nur verfügbar, wenn Sie ein neues Softwareupdate-Bereitstellungspaket erstellen.  

13. Geben Sie auf der Seite Downloadort an, ob die Softwareupdatedateien vom Internet oder aus dem lokalen Netzwerk heruntergeladen werden sollen. Konfigurieren Sie die folgenden Einstellungen:  

    -   **Softwareupdates aus dem Internet herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates von einem bestimmten Speicherort im Internet herunterzuladen. Diese Einstellung ist standardmäßig aktiviert.  

    -   **Softwareupdates von einem Pfad im lokalen Netzwerk herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates aus einem lokalen Verzeichnis oder aus einem freigegebenen Ordner herunterzuladen. Diese Einstellung ist nützlich, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist. Die Softwareupdates können von jedem Computer mit Internetzugriff vorläufig heruntergeladen und im lokalen Netzwerk an einem Speicherort abgelegt werden, der von dem Computer aus zugänglich ist, auf dem der Assistent ausgeführt wird.  

14. Wählen Sie auf der Seite Sprachauswahl die Sprachen aus, für die die ausgewählten Softwareupdates heruntergeladen werden. Die Softwareupdates werden nur dann heruntergeladen, wenn sie in den ausgewählten Sprachen verfügbar sind. Softwareupdates, die nicht sprachspezifisch sind, werden immer heruntergeladen. Standardmäßig werden vom Assistenten die Sprachen ausgewählt, die Sie in den Eigenschaften des Softwareupdatepunkts konfiguriert haben. Es muss mindestens eine Sprache ausgewählt werden, bevor die nächste Seite angezeigt werden kann. Wenn Sie nur Sprachen auswählen, die von einem Softwareupdate nicht unterstützt werden, kann das Softwareupdate nicht heruntergeladen werden.  

15. Überprüfen Sie die Einstellungen auf der Seite Zusammenfassung. Zum Speichern der Einstellungen in einer Bereitstellungsvorlage klicken Sie auf **Als Vorlage speichern**. Geben Sie einen Namen ein, wählen Sie die Einstellungen aus, die Sie in die Vorlage aufnehmen möchten, und klicken Sie auf **Speichern**. Zum Ändern einer konfigurierten Einstellung klicken Sie auf die entsprechende Assistentenseite, und nehmen Sie die Änderung vor.  

    > [!NOTE]  
    >  Der Vorlagenname kann alphanumerische ASCII-Zeichen sowie die Zeichen **\\** (umgekehrter Schrägstrich) oder **‘** (einfaches Anführungszeichen) enthalten.  

16. Klicken Sie auf **Weiter** , um die automatische Bereitstellungsregel zu erstellen.  

 Nachdem Sie den Assistenten abgeschlossen haben, wird die automatische Bereitstellungsregel ausgeführt. Dabei werden die Softwareupdates, die die angegebenen Kriterien erfüllen, einer Softwareupdategruppe hinzugefügt. Dann werden die Softwareupdates in die Inhaltsbibliothek auf dem Standortserver heruntergeladen und an die konfigurierten Verteilungspunkte verteilt. Die Softwareupdategruppe wird schließlich den Clients in der Zielsammlung bereitgestellt.  

##  <a name="BKMK_AddDeploymentToADR"></a> Hinzufügen einer neuen Bereitstellung zu einer vorhandenen automatischen Bereitstellungsregel  
 Nach der Erstellung einer automatischen Bereitstellungsregel können Sie zusätzliche Bereitstellungen zur Regel hinzufügen. Dies hilft Ihnen dabei, die Komplexität der Bereitstellung verschiedener Updates für verschiedene Sammlungen zu verwalten. Jede neue Bereitstellung verfügt über sämtliche Funktionen und die Bereitstellungsüberwachungsumgebung.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>So fügen Sie einer vorhandenen automatischen Bereitstellungsregel eine neue Bereitstellung hinzu  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Softwareupdates** > **Automatische Bereitstellungsregeln**, und wählen Sie dann die gewünschte Regel.  

2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Automatische Bereitstellungsregel** auf **Bereitstellung hinzufügen**. Der Assistent zum Hinzufügen einer Bereitstellung wird geöffnet.  

3.  Konfigurieren Sie auf der Seite **Sammlung** die folgenden Einstellungen:  

    -   **Sammlung**: Gibt die für die Bereitstellung zu verwendende Zielsammlung an. Mitglieder dieser Sammlung erhalten die in der Bereitstellung definierten Softwareupdates.  

    -   **Bereitstellung nach Ausführung dieser Regel aktivieren**: Geben Sie an, ob die Softwareupdatebereitstellung nach der Ausführung der automatischen Bereitstellungsregel aktiviert werden soll. Hinsichtlich dieser Spezifikation ist Folgendes zu beachten:  

        -   Wenn Sie die Bereitstellung aktivieren, werden die Softwareupdates, die die in der Regel definierten Kriterien erfüllen, einer Softwareupdategruppe hinzugefügt. Dann wird der Inhalt für die Softwareupdates nach Bedarf heruntergeladen und auf die angegebenen Verteilungspunkte kopiert. Schließlich werden die Softwareupdates den Clients in der Zielsammlung bereitgestellt.  

        -   Wenn Sie die Bereitstellung nicht aktivieren, werden die Softwareupdates, die die in der Regel definierten Kriterien erfüllen, einer Softwareupdategruppe hinzugefügt. Die Bereitstellungsrichtlinie für Softwareupdates ist zwar konfiguriert, aber die Softwareupdates werden nicht heruntergeladen oder den Clients bereitgestellt. Sie haben somit Zeit, die Bereitstellung der Softwareupdates vorzubereiten, zu prüfen, ob die den Kriterien entsprechenden Softwareupdates geeignet sind, sowie die Bereitstellung zu einem späteren Zeitpunkt zu aktivieren.  

4.  Konfigurieren Sie auf der Seite Bereitstellungseinstellungen die folgenden Einstellungen:  

    -   **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren**: Gibt an, ob Wake-On-LAN am Stichtag aktiviert werden soll, damit Aktivierungspakete an Computer gesendet werden, für die mindestens eines der in der Bereitstellung enthaltenen Softwareupdates erforderlich ist. Alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, werden aktiviert, damit die Softwareupdateinstallation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert.  

        > [!WARNING]  
        >  Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.  

    -   **Detailstufe**: Geben Sie die Detailstufe für die von den Clientcomputern zurückgegebenen Zustandsmeldungen an.  

        > [!IMPORTANT]  
        >  Stellen Sie die Detailstufe beim Bereitstellen von Definitionsupdates auf **Nur Fehler** ein, damit vom Client nur dann eine Zustandsmeldung zurückgegeben wird, wenn ein Definitionsupdate nicht an den Client geliefert werden kann. Andernfalls gehen vom Client zahlreiche Zustandsmeldungen ein, die sich auf die Leistung des Standortservers auswirken können.  

5.  Konfigurieren Sie auf der Seite Bereitstellungszeitplan die folgenden Einstellungen:  

    -   **Auswertung planen**: Geben Sie an, ob die verfügbare Zeit und die Installationsstichtage von Configuration Manager mit UTC oder der lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird, ausgewertet werden sollen.  

        > [!NOTE]  
        >  Wenn Sie die Ortszeit auswählen und dann **So bald wie möglich** für **Zeitpunkt der Verfügbarkeit der Software** oder **Installationsstichtag** auswählen, wird die aktuelle Uhrzeit auf dem Computer mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind, oder auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.  

    -   **Zeitpunkt der Verfügbarkeit der Software**: Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung stehen:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clientcomputern so bald wie möglich zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung ausgewählt ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Die zur Installation verfügbaren Updates können dann abgerufen werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clientcomputern zu einem bestimmten Termin (Datum und Uhrzeit) zur Verfügung gestellt werden. Wenn diese Einstellung beim Erstellen der Bereitstellung aktiviert ist, wird die Clientrichtlinie von Configuration Manager aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem konfigurierten Termin (Datum und Uhrzeit) für die Installation zur Verfügung.  

    -   **Installationsstichtag**: Wählen Sie eine der folgenden Einstellungen aus, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung so bald wie möglich automatisch installiert werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung zu einem bestimmten Termin (Datum und Uhrzeit) automatisch installiert werden. Configuration Manager bestimmt den Stichtag zum Installieren von Softwareupdates durch Hinzufügen der konfigurierten Intervalle **Bestimmte Zeit** zu **Zeitpunkt der Verfügbarkeit der Software**.  

        > [!NOTE]  
        >  Der tatsächliche Installationsstichtag ergibt sich aus der Addition des angezeigten Stichtags und eines willkürlichen Zeitraums von bis zu 2 Stunden. Dadurch werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Softwareupdates in der Bereitstellung durch alle Clientcomputer in der Zielsammlung einhergehen.  
        >   
        >  Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für den **Computer-Agent** konfigurieren, um die zufällige Verzögerung der Installation für die erforderlichen Softwareupdates zu deaktivieren. Weitere Informationen finden Sie unter [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  Konfigurieren Sie auf der Seite Benutzerfreundlichkeit die folgenden Einstellungen:  

    -   **Benutzerbenachrichtigungen**: Geben Sie an, ob zum vorgegebenen **Zeitpunkt der Verfügbarkeit der Software** auf dem Clientcomputer eine Benachrichtigung zu den Softwareupdates im Softwarecenter angezeigt werden soll. Geben Sie auch an, ob auf den Clientcomputern Benutzerbenachrichtigungen angezeigt werden sollen.  

    -   **Verhalten am Stichtag**: Geben Sie das gewünschte Verhalten am Stichtag der Softwareupdatebereitstellung an. Geben Sie an, ob die Softwareupdates in der Bereitstellung installiert werden sollen. Geben Sie auch, ob nach einer Softwareupdateinstallation unabhängig von einem konfigurierten Wartungsfenster ein Systemneustart ausgeführt werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Verhalten beim Geräteneustart**: Geben Sie an, ob nach der Installation der Softwareupdates ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn der Systemneustart zum Abschließen der Installation erforderlich ist.  

        > [!IMPORTANT]  
        >  Das Unterdrücken von Systemneustarts kann in Serverumgebungen oder in Fällen hilfreich sein, in denen Computer nach der Installation von Softwareupdates nicht standardmäßig neu gestartet werden sollen. Allerdings kann dies zu einem unsicheren Computerzustand führen. Durch Erzwingen eines Neustarts hingegen wird gewährleistet, dass die Softwareupdateinstallation umgehend abgeschlossen wird.  

    -   **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Beim Bereitstellen von Softwareupdates für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass das Softwareupdate auf dem temporären Overlay installiert wird und die Änderungen entweder später, am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

        > [!NOTE]  
        >  Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist.  

7.  Geben Sie auf der Seite „Warnungen“ an, wie Configuration Manager und System Center Operations Manager Warnungen für diese Bereitstellung generieren sollen.  

    > [!WARNING]  
    >  Sie können die letzten Warnungen zu Softwareupdates im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** prüfen.  

8. Konfigurieren Sie auf der Seite Downloadeinstellungen die folgenden Einstellungen:  

    - Geben Sie an, ob die Softwareupdates vom Client heruntergeladen und installiert werden, wenn ein Client mit einer langsamen Netzwerkverbindung oder einer Fallbackinhaltsquelle vorliegt.  

    - Geben Sie an, ob die Softwareupdates vom Client von einem Fallbackverteilungspunkt heruntergeladen und installiert werden sollen, wenn der Inhalt für die Softwareupdates an einem bevorzugten Verteilungspunkt nicht verfügbar ist.  

    - **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob BranchCache beim Herunterladen von Inhalten verwendet werden soll. Weitere Informationen zu BranchCache finden Sie unter [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Inhalt von Microsoft Updates herunterladen, falls Softwareupdates in aktuellen oder benachbarten Begrenzungsgruppen oder in Standortbegrenzungsgruppen am Verteilungspunkt nicht verfügbar sind**: Wählen Sie diese Einstellung aus, damit Clients, die mit dem Intranet verbunden sind, Softwareupdates von Microsoft Update herunterladen, wenn keine Softwareupdates auf Verteilungspunkten verfügbar sind. Internetbasierte Clients können Softwareupdates immer von Microsoft Update herunterladen.

    - Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

    > [!NOTE]  
    > Der Inhaltsort für die Softwareupdates in einer Bereitstellung wird von den Clients von einem Verwaltungspunkt angefordert. Das Downloadverhalten richtet sich danach, wie Sie den Verteilungspunkt, das Bereitstellungspaket und die Einstellungen auf dieser Seite konfiguriert haben. Weitere Informationen finden Sie unter [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Weitere Informationen zum Bereitstellungsprozess finden Sie unter [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Nächste Schritte
[Überwachen von Softwareupdates](monitor-software-updates.md)
