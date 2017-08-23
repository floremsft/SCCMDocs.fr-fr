---
title: Manuelles Bereitstellen von Softwareupdates | Microsoft Docs
description: "Zum manuellen Bereitstellen von Updates wählen Sie Updates über die Configuration Manager-Konsole aus, und stellen Sie sie manuell bereit, oder fügen Sie Updates einer Updategruppe hinzu, und stellen Sie die Gruppe bereit."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: 2a0d5f12b99689749833c109d4fa399f99451d8a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_ManualDeploy"></a> Manuelles Bereitstellen von Softwareupdates  

*Gilt für: System Center Configuration Manager (Current Branch)*

 Bei der manuellen Bereitstellung von Softwareupdates werden Softwareupdates in der Configuration Manager-Konsole ausgewählt, und der Bereitstellungsprozess wird manuell gestartet. Alternativ können Sie ausgewählte Softwareupdates einer Softwareupdategruppe hinzufügen und dann die Updategruppe manuell bereitstellen. Mit der manuellen Bereitstellung sorgen Sie in der Regel dafür, dass die aktuell erforderlichen Softwareupdates auf den Clientgeräten vorhanden sind, bevor Sie automatische Bereitstellungsregeln zur Verwaltung der laufenden monatlichen Softwareupdatebereitstellungen erstellen. Die manuelle Methode dient auch dazu, Out-of-Band-Softwareupdates bereitzustellen. Wenn Sie Hilfe bei der Ermittlung der für Sie geeigneten Bereitstellungsmethode benötigen, lesen Sie [Bereitstellen von Softwareupdates](deploy-software-updates.md).

 Die folgenden Abschnitte enthalten die Schritte für die manuelle Bereitstellung von Softwareupdates.  

##  <a name="BKMK_1SearchCriteria"></a> Schritt 1: Angeben von Suchkriterien für Softwareupdates  
 In der Configuration Manager-Konsole werden potenziell Tausende Softwareupdates angezeigt. Der erste Schritt des Workflows für die manuelle Bereitstellung von Softwareupdates besteht daher darin, die Softwareupdates zu suchen, die Sie bereitstellen möchten. Beispielsweise könnten Sie anhand geeigneter Kriterien angeben, dass alle Softwareupdates abgerufen werden sollen, die auf mehr als 50 Clientgeräten benötigt werden und deren Softwareupdateklassifizierung **Sicherheit** oder **Kritisch** lautet.  

> [!IMPORTANT]  
>  Eine einzelne Softwareupdatebereitstellung kann maximal 1000 Softwareupdates umfassen.  

#### <a name="to-specify-search-criteria-for-software-updates"></a>So geben Sie Suchkriterien für Softwareupdates an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich „Softwarebibliothek“ den Eintrag **Softwareupdates**, und klicken Sie auf **Alle Softwareupdates**. Die synchronisierten Softwareupdates werden angezeigt.  

    > [!NOTE]  
    >  Im Knoten **Alle Softwareupdates** zeigt Configuration Manager nur Softwareupdates an, die die Klassifizierungen **Kritisch** und **Sicherheit** aufweisen und in den letzten 30 Tagen veröffentlicht wurden.  

3.  Filtern Sie im Suchbereich das erforderliche Softwareupdate mit einem oder beiden der folgenden Schritte heraus:  

    -   Geben Sie im Suchtextfeld eine Suchzeichenfolge ein, anhand derer die Softwareupdates gefiltert werden. Beispielsweise können Sie die Artikel-ID oder die Bulletin-ID eines bestimmten Softwareupdates oder eine Zeichenfolge, die im Titel mehrerer Softwareupdates erscheint, eingeben.  

    -   Klicken Sie auf **Kriterien hinzufügen**, wählen Sie die zum Filtern der Softwareupdates gewünschten Kriterien aus, und klicken Sie auf **Hinzufügen**. Geben Sie dann Werte für die Kriterien ein.  

4.  Klicken Sie auf **Suchen** , um die Softwareupdates zu filtern.  

    > [!TIP]  
    >  Sie haben auf der Registerkarte **Suchen** und in der Gruppe **Speichern** die Möglichkeit, die Filterkriterien zu speichern.  

##  <a name="BKMK_2UpdateGroup"></a> Schritt 2: Erstellen einer Softwareupdategruppe, die die Softwareupdates enthält  
 Mithilfe von Softwareupdategruppen können Sie Softwareupdates auf wirksame Weise für die Bereitstellung vorbereiten. Sie können Softwareupdates einer Softwareupdategruppe manuell hinzufügen. Mit einer automatischen Bereitstellungsregel können Softwareupdates einer neuen oder vorhandenen Softwareupdategruppe von Configuration Manager auch automatisch hinzugefügt werden. Gehen Sie wie folgt vor, um Softwareupdates einer neuen Softwareupdategruppe manuell hinzuzufügen.  

#### <a name="to-manually-add-software-updates-to-a-new-software-update-group"></a>So fügen Sie Softwareupdates einer neuen Softwareupdategruppe manuell hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Klicken Sie im Arbeitsbereich „Softwarebibliothek“ auf **Softwareupdates**.  

3.  Wählen Sie die Softwareupdates aus, die der neuen Softwareupdategruppe hinzugefügt werden sollen.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Softwareupdategruppe erstellen**.  

5.  Geben Sie den Namen und optional eine Beschreibung für die Softwareupdategruppe ein. Achten Sie darauf, dass der Name und die Beschreibung aussagekräftig sind, damit Sie den Typ der einzelnen Softwareupdates in der Softwareupdategruppe schnell ermitteln können. Klicken Sie auf **Erstellen**, um den Vorgang fortzusetzen.  

6.  Klicken Sie auf den Knoten **Softwareupdategruppen** , um die neue Softwareupdategruppe anzuzeigen.  

7.  Wählen Sie die Softwareupdategruppe aus. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Mitglieder anzeigen** , um eine Liste der Softwareupdates in der Gruppe anzuzeigen.  

##  <a name="BKMK_3DownloadContent"></a> Schritt 3: Herunterladen des Inhalts für die Softwareupdategruppe  
 Optional können Sie den Inhalt für die Softwareupdates in der Softwareupdategruppe herunterladen, bevor Sie die Softwareupdates bereitstellen. Dies bietet sich möglicherweise an, wenn Sie vor der Bereitstellung der Softwareupdates überprüfen möchten, ob der Inhalt auf den Verteilungspunkten verfügbar ist. Auf diese Weise können Sie unerwartete Probleme mit der Inhaltsübermittlung vermeiden. Sie können diesen Schritt überspringen. Der Inhalt wird dann im Rahmen des Bereitstellungsprozesses heruntergeladen und auf die Verteilungspunkte kopiert. Gehen Sie wie folgt vor, um den Inhalt für Softwareupdates in die Softwareupdategruppe herunterzuladen.  



#### <a name="to-download-content-for-the-software-update-group"></a>So laden Sie den Inhalt für die Softwareupdategruppe herunter
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### <a name="to-monitor-content-status"></a>So überwachen Sie den Inhaltsstatus
1. Zur Überwachung des Inhaltsstatus der Softwareupdates klicken Sie in der -Configuration Manager-Konsole auf **Überwachung**.  

2. Erweitern Sie im Arbeitsbereich „Überwachung“ den Eintrag **Verteilungsstatus**, und klicken Sie dann auf **Inhaltsstatus**.  

3. Wählen Sie das Softwareupdatepaket aus, das Sie bereits zum Herunterladen der Softwareupdates in die Softwareupdategruppe ausgewählt haben.  

4. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Inhalt** auf **Status anzeigen**.  

##  <a name="BKMK_4DeployUpdateGroup"></a> Schritt 4: Bereitstellen der Softwareupdategruppe  
 Nachdem Sie entschieden haben, welche Softwareupdates Sie bereitstellen möchten, und diese Softwareupdates einer Softwareupdategruppe hinzugefügt haben, können Sie die Softwareupdates in der Softwareupdategruppe manuell bereitstellen. Gehen Sie wie folgt vor, um die Softwareupdates in einer Softwareupdategruppe manuell bereitzustellen.  

#### <a name="to-manually-deploy-the-software-updates-in-a-software-update-group"></a>So stellen Sie die Softwareupdates in einer Softwareupdategruppe manuell bereit  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich „Softwarebibliothek“ den Eintrag **Softwareupdates**, und klicken Sie auf **Softwareupdategruppen**.  

3.  Wählen Sie die Softwareupdategruppe aus, die Sie bereitstellen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**. Der Assistent zum Bereitstellen von Softwareupdates ****  wird geöffnet.  

5.  Konfigurieren Sie auf der Seite Allgemein die folgenden Einstellungen:  

    -   **Name**: Geben Sie den Namen für die Bereitstellung an. Der Name der Bereitstellung muss eindeutig sein, den Zweck der Bereitstellung angeben und sich am Configuration Manager-Standort leicht von anderen Bereitstellungen unterscheiden lassen. Configuration Manager gibt für die Bereitstellung standardmäßig automatisch einen Namen im folgenden Format an: **Microsoft-Softwareupdates -** <*Datum*><*Uhrzeit*>  

    -   **Beschreibung**: Geben Sie eine Beschreibung für die Bereitstellung an. Die Beschreibung gibt einen Überblick über die Bereitstellung und umfasst alle anderen relevanten Informationen, die die Identifizierung und Unterscheidung der Bereitstellung am Configuration Manager-Standort erleichtern. Das Feld „Beschreibung“ ist optional, hat eine Begrenzung auf 256 Zeichen und ist standardmäßig leer.  

    -   **Softwareupdate/Softwareupdategruppe**: Überprüfen Sie, ob die angezeigte Softwareupdategruppe bzw. das angezeigte Softwareupdate richtig ist.  

    -   **Bereitstellungsvorlage auswählen**: Geben Sie an, ob eine zuvor gespeicherte Bereitstellungsvorlage angewendet werden soll. Sie können eine Bereitstellungsvorlage konfigurieren, die mehrere allgemeine Bereitstellungseigenschaften für Softwareupdates umfasst. Wenn Sie diese Vorlage bei der Bereitstellung nachfolgender Softwareupdates anwenden, sorgen Sie nicht nur für Konsistenz mit ähnlichen Bereitstellungen, sondern verringern auch Ihren Zeitaufwand.  

    -   **Sammlung**: Geben Sie gegebenenfalls die Sammlung der Bereitstellung an. Mitglieder dieser Sammlung erhalten die in der Bereitstellung definierten Softwareupdates.  

6.  Konfigurieren Sie auf der Seite Bereitstellungseinstellungen die folgenden Einstellungen:  

    -   **Bereitstellungstyp**: Geben Sie für die Softwareupdatebereitstellung den Bereitstellungstyp an. Wählen Sie **Erforderlich** aus, um eine obligatorische Softwareupdatebereitstellung zu erstellen, bei der Softwareupdates automatisch bis zu einem vorgegebenen Installationsstichtag auf Clients installiert werden. Wählen Sie **Verfügbar** aus, um eine optionale Softwareupdatebereitstellung zu erstellen, die im Softwarecenter zur Verfügung gestellt wird und von Benutzern installiert werden kann.  

        > [!IMPORTANT]  
        >  Nachdem Sie die Softwareupdatebereitstellung einmal erstellt haben, können Sie den Bereitstellungstyp nicht mehr ändern.  

        > [!NOTE]  
        >  Eine als **Erforderlich** bereitgestellte Softwareupdategruppe wird im Hintergrund heruntergeladen und berücksichtigt BITS-Einstellungen (sofern konfiguriert).  
        > Als **Verfügbar** bereitgestellte Softwareupdategruppen werden jedoch im Vordergrund heruntergeladen und ignorieren BITS-Einstellungen.  

    -   **Wake-on-LAN verwenden, um Clients für erforderliche Bereitstellungen zu aktivieren**: Geben Sie an, ob Wake-On-LAN am Stichtag aktiviert werden soll, damit Aktivierungspakete an Computer gesendet werden, für die mindestens eines der in der Bereitstellung enthaltenen Softwareupdates erforderlich ist. Alle Computer, die sich am Installationsstichtag im Energiesparmodus befinden, werden aktiviert, damit die Softwareupdateinstallation initiiert werden kann. Clients, die sich im Energiesparmodus befinden und für die keine der in der Bereitstellung enthaltenen Softwareupdates erforderlich sind, werden nicht gestartet. Diese Einstellung ist standardmäßig deaktiviert und nur verfügbar, wenn unter **Bereitstellungstyp** die Einstellung **Erforderlich**ausgewählt wurde.  

        > [!WARNING]  
        >  Sie können diese Option nur verwenden, wenn Computer und Netzwerke für Wake-On-LAN konfiguriert sind.  

    -   **Detailstufe**: Geben Sie die Detailstufe für die von den Clientcomputern zurückgegebenen Zustandsmeldungen an.  

7.  Konfigurieren Sie auf der Seite Zeitplanung die folgenden Einstellungen:  

    -   **Auswertung planen**: Geben Sie an, ob die verfügbare Zeit und die Installationsstichtage mit UTC oder der lokalen Zeit des Computers, auf dem die Consolidation Manager-Konsole ausgeführt wird, ausgewertet werden sollen.  

        > [!NOTE]  
        >  Wenn Sie die Ortszeit auswählen und dann **So bald wie möglich** für **Zeitpunkt der Verfügbarkeit der Software** oder **Installationsstichtag** auswählen, wird die aktuelle Uhrzeit auf dem Computer mit der Configuration Manager-Konsole verwendet, um zu bestimmen, wann Updates verfügbar sind, oder auf einem Client installiert werden. Wenn sich der Client in einer anderen Zeitzone befindet, erfolgen diese Aktionen, sobald die Evaluierungszeit des Clients erreicht ist.  

    -   **Zeitpunkt der Verfügbarkeit der Software**: Wählen Sie eine der folgenden Einstellungen aus, um anzugeben, wann die Softwareupdates den Clients zur Verfügung stehen:  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clients so bald wie möglich zur Verfügung gestellt werden. Beim Erstellen der Bereitstellung wird die Clientrichtlinie aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Die Softwareupdates stehen anschließend für die Installation zur Verfügung.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung den Clients zu einem bestimmten Termin (Datum und Uhrzeit) zur Verfügung gestellt werden. Beim Erstellen der Bereitstellung wird für die Clientrichtlinie aktualisiert. Clients werden beim nächsten Abfragezyklus der Clientrichtlinie von der Bereitstellung benachrichtigt. Allerdings stehen die Softwareupdates in der Bereitstellung erst nach dem angegebenen Termin (Datum und Uhrzeit) für die Installation zur Verfügung.  

    -   **Installationsstichtag**: Wählen Sie eine der folgenden Einstellungen aus, um den Installationsstichtag für die Softwareupdates in der Bereitstellung anzugeben.  

        > [!NOTE]  
        >  Der Installationsstichtag kann nur konfiguriert werden, wenn auf der Seite „Bereitstellungseinstellungen“ unter **Bereitstellungstyp** die Option **Erforderlich** ausgewählt wurde.  

        -   **So bald wie möglich**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung so bald wie möglich automatisch installiert werden.  

        -   **Bestimmte Zeit**: Wählen Sie diese Einstellung aus, damit die Softwareupdates in der Bereitstellung zu einem bestimmten Termin (Datum und Uhrzeit) automatisch installiert werden.  

        > [!NOTE]  
        >  Der tatsächliche Installationsstichtag ergibt sich aus der Addition der angegebenen bestimmten Zeit und eines willkürlichen Zeitraums von bis zu 2 Stunden. Dadurch werden die potenziellen Auswirkungen reduziert, die mit der gleichzeitigen Installation der Softwareupdates in der Bereitstellung durch alle Clientcomputer in der Zielsammlung einhergehen.  
        >   
        >  Sie können die Clienteinstellung **Zufällige Stichtaganordnung deaktivieren** für den **Computer-Agent** konfigurieren, um die zufällige Verzögerung der Installation für die erforderlichen Softwareupdates zu deaktivieren. Weitere Informationen finden Sie unter [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8.  Konfigurieren Sie auf der Seite Benutzerfreundlichkeit die folgenden Einstellungen:  

    -   **Benutzerbenachrichtigungen**: Geben Sie an, ob zum vorgegebenen **Zeitpunkt der Verfügbarkeit der Software** auf dem Clientcomputer eine Benachrichtigung zu den Softwareupdates im Softwarecenter angezeigt werden soll. Geben Sie auch an, ob auf den Clientcomputern Benutzerbenachrichtigungen angezeigt werden sollen. Wenn auf der Seite „Bereitstellungseinstellungen“ unter **Bereitstellungstyp** die Einstellung **Verfügbar** ausgewählt ist, können Sie **In Softwarecenter und allen Benachrichtigungen ausblenden**nicht auswählen.  

    -   **Verhalten am Stichtag**: *Diese Option ist nur verfügbar, wenn auf der Seite „Bereitstellungseinstellungen“ unter **Bereitstellungstyp** *die Option **Erforderlich** *ausgewählt wurde.*   
    Geben Sie das Verhalten am Stichtag der Softwareupdatebereitstellung an. Geben Sie an, ob die Softwareupdates in der Bereitstellung installiert werden sollen. Geben Sie auch, ob nach einer Softwareupdateinstallation unabhängig von einem konfigurierten Wartungsfenster ein Systemneustart ausgeführt werden soll. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Verhalten beim Geräteneustart**: *Diese Option ist nur verfügbar, wenn auf der Seite „Bereitstellungseinstellungen“ unter **Bereitstellungstyp** *die Option **Erforderlich** *ausgewählt wurde.*    
    Geben Sie an, ob nach der Installation der Softwareupdates ein Systemneustart auf den Servern und Arbeitsstationen unterdrückt werden soll, wenn der Systemneustart zum Abschließen der Installation erforderlich ist.  

        > [!IMPORTANT]  
        >  Das Unterdrücken von Systemneustarts kann in Serverumgebungen oder in Fällen hilfreich sein, in denen Computer nach der Installation von Softwareupdates nicht standardmäßig neu gestartet werden sollen. Allerdings kann dies zu einem unsicheren Computerzustand führen. Durch Erzwingen eines Neustarts hingegen wird gewährleistet, dass die Softwareupdateinstallation umgehend abgeschlossen wird.

    -   **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Beim Bereitstellen von Softwareupdates für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass das Softwareupdate auf dem temporären Overlay installiert wird und die Änderungen entweder später, am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden sollen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters ausgeführt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

        > [!NOTE]  
        >  Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist.  

    - **Neubewertungsverhalten bei Softwareupdatebereitstellungen nach einem Neustart:** Ab Version 1606 von Configuration Manager können Sie mit dieser Einstellung die Bereitstellung von Softwareupdates so konfigurieren, dass Clients direkt nach dem Neustart im Anschluss an die Installation von Softwareupdates eine Complianceüberprüfung durchführen. So kann der Client nach zusätzlichen Softwareupdates suchen, die nach dem Neustart des Clients relevant werden, und diese im gleichen Wartungsfenster installieren (und so für Kompatibilität sorgen).

9. Geben Sie auf der Seite „Warnungen“ an, wie Configuration Manager und System Center Operations Manager Warnungen für diese Bereitstellung generieren sollen. Warnungen können nur konfiguriert werden, wenn auf der Seite „Bereitstellungseinstellungen“ unter **Bereitstellungstyp** die Option **Erforderlich** ausgewählt wurde.  

    > [!NOTE]  
    >  Sie können die letzten Warnungen zu Softwareupdates im Arbeitsbereich **Softwarebibliothek** im Knoten **Softwareupdates** prüfen.  

10. Konfigurieren Sie auf der Seite Downloadeinstellungen die folgenden Einstellungen:  

    - Geben Sie an, ob die Softwareupdates vom Client heruntergeladen und installiert werden, wenn ein Client mit einer langsamen Netzwerkverbindung oder einer Fallbackinhaltsquelle vorliegt.  

    - Geben Sie an, ob die Softwareupdates vom Client von einem Fallbackverteilungspunkt heruntergeladen und installiert werden sollen, wenn der Inhalt für die Softwareupdates an einem bevorzugten Verteilungspunkt nicht verfügbar ist.  

    - **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob BranchCache beim Herunterladen von Inhalten verwendet werden soll. Weitere Informationen zu BranchCache finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Inhalt von Microsoft Updates herunterladen, falls Softwareupdates in aktuellen oder benachbarten Begrenzungsgruppen oder in Standortbegrenzungsgruppen am Verteilungspunkt nicht verfügbar sind**: Wählen Sie diese Einstellung aus, damit Clients, die mit dem Intranet verbunden sind, Softwareupdates von Microsoft Update herunterladen, wenn keine Softwareupdates auf Verteilungspunkten verfügbar sind. Internetbasierte Clients können Softwareupdates immer von Microsoft Update herunterladen.

    - Geben Sie an, ob es Clients mit einer getakteten Internetverbindung möglich sein soll, Inhalt nach dem Installationsstichtag herunterzuladen. Bei getakteten Internetverbindungen berechnen einige Internetanbieter die anfallenden Gebühren anhand der Datenmenge, die Sie senden und empfangen.  

    > [!NOTE]  
    >  Der Inhaltsort für die Softwareupdates in einer Bereitstellung wird von den Clients von einem Verwaltungspunkt angefordert. Das Downloadverhalten richtet sich danach, wie Sie den Verteilungspunkt, das Bereitstellungspaket und die Einstellungen auf dieser Seite konfiguriert haben. Weitere Informationen finden Sie unter [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Wenn Sie [Schritt 3: Herunterladen des Inhalts für die Softwareupdategruppe](#BKMK_3DownloadContent)durchgeführt haben, werden die Seiten „Bereitstellungspaket“, „Verteilungspunkte“ und „Sprachauswahl“ nicht angezeigt, und Sie können mit Schritt 15 des Assistenten fortfahren.  

    > [!IMPORTANT]  
    >  Softwareupdates, die bereits in die Inhaltsbibliothek auf dem Standortserver heruntergeladen wurden, werden nicht erneut heruntergeladen. Dies ist auch der Fall, wenn Sie für die Softwareupdates ein neues Bereitstellungspaket erstellen. Wenn alle Softwareupdates bereits heruntergeladen wurden, wird der Vorgang auf der Seite **Sprachauswahl** (Schritt 15) fortgesetzt.  

12. Wählen Sie auf der Seite Bereitstellungspaket ein vorhandenes Bereitstellungspaket aus, oder geben Sie anhand der nachfolgenden Einstellungen ein neues Bereitstellungspaket an:  

    1.  **Name**: Geben Sie den Namen des Bereitstellungspakets an. Dies muss ein eindeutiger Name sein, der den Paketinhalt beschreibt. Er ist auf 50 Zeichen begrenzt.  

    2.  **Beschreibung**: Geben Sie eine Beschreibung mit Informationen zum Bereitstellungspaket an. Die Beschreibung ist auf 127 Zeichen begrenzt.  

    3.  **Paketquelle**: Geben Sie den Speicherort der Quelldateien der Softwareupdates an.  Geben Sie für den Quellspeicherort einen Netzwerkpfad wie **\\\Server\Freigabename\Pfad**ein. Alternativ können Sie auf **Durchsuchen** klicken, um den Netzwerkpfad zu suchen. Sie müssen den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets erstellen, bevor Sie mit der nächsten Seite fortfahren.  

        > [!NOTE]  
        >  Der von Ihnen angegebene Quellspeicherort des Bereitstellungspakets kann von keinem anderen Softwarebereitstellungspaket verwendet werden.  

        > [!IMPORTANT]  
        >  Das Computerkonto für den SMS-Anbieter und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen über die NTFS-Berechtigung **Schreiben** für den Downloadort verfügen. Sie müssen den Zugriff auf den Downloadort beschränken, um das Risiko zu verringern, dass Angreifer die Quelldateien der Softwareupdates manipulieren.  

        > [!IMPORTANT]  
        >  Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt von der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.  

    4.  **Sendepriorität**: Geben Sie die Sendepriorität für das Bereitstellungspaket an. Configuration Manager verwendet Sendepriorität für das Bereitstellungspaket beim Senden des Pakets an Verteilungspunkte. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: „Hoch“, „Mittel“ oder „Niedrig“. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet.  

13. Geben Sie auf der Seite Verteilungspunkte die Verteilungspunkte oder Verteilungspunktgruppen an, auf denen die Softwareupdatedateien gehostet werden sollen. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurationen für Verteilungspunkte](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

14. Geben Sie auf der Seite Downloadort an, ob die Softwareupdatedateien vom Internet oder aus dem lokalen Netzwerk heruntergeladen werden sollen. Konfigurieren Sie die folgenden Einstellungen:  

    -   **Softwareupdates aus dem Internet herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates von einem bestimmten Speicherort im Internet herunterzuladen. Diese Einstellung ist standardmäßig aktiviert.  

    -   **Softwareupdates von einem Pfad im lokalen Netzwerk herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates aus einem lokalen Ordner oder aus einem freigegebenen Netzwerkordner herunterzuladen. Diese Einstellung ist nützlich, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist. Die Softwareupdates können von jedem Computer mit Internetverbindung heruntergeladen, an einem Ort im lokalen Netzwerk gespeichert und bei der Installation abgerufen werden.  

15. Wählen Sie auf der Seite Sprachauswahl die Sprachen aus, für die die ausgewählten Softwareupdates heruntergeladen werden. Die Softwareupdates werden nur dann heruntergeladen, wenn sie in den ausgewählten Sprachen verfügbar sind. Softwareupdates, die nicht sprachspezifisch sind, werden immer heruntergeladen. Standardmäßig werden vom Assistenten die Sprachen ausgewählt, die Sie in den Eigenschaften des Softwareupdatepunkts konfiguriert haben. Es muss mindestens eine Sprache ausgewählt werden, bevor die nächste Seite angezeigt werden kann. Wenn Sie nur Sprachen auswählen, die von einem Softwareupdate nicht unterstützt werden, kann das Softwareupdate nicht heruntergeladen werden.  

16. Überprüfen Sie die Einstellungen auf der Seite Zusammenfassung. Zum Speichern der Einstellungen in einer Bereitstellungsvorlage klicken Sie auf **Als Vorlage speichern**. Geben Sie einen Namen ein, wählen Sie die Einstellungen aus, die Sie in die Vorlage aufnehmen möchten, und klicken Sie auf **Speichern**. Zum Ändern einer konfigurierten Einstellung klicken Sie auf die entsprechende Assistentenseite, und nehmen Sie die Änderung vor.  

    > [!WARNING]  
    >  Der Vorlagenname kann alphanumerische ASCII-Zeichen sowie die Zeichen **\\** (umgekehrter Schrägstrich) oder **‘** (einfaches Anführungszeichen) enthalten.  

17. Klicken Sie auf **Weiter** , um das Softwareupdate bereitzustellen.  

 Nachdem Sie den Assistenten abgeschlossen haben, werden die Softwareupdates von Configuration Manager in die Inhaltsbibliothek auf dem Standortserver heruntergeladen und an die konfigurierten Verteilungspunkte verteilt. Anschließend wird die Softwareupdategruppe den Clients in der Zielsammlung bereitgestellt. Weitere Informationen zum Bereitstellungsprozess finden Sie unter [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Nächste Schritte
[Überwachen von Softwareupdates](monitor-software-updates.md)
