---
title: "Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem | Microsoft-Dokumentation"
description: "Mit den Tasksequenzen in System Center Configuration Manager kann für ein Betriebssystem automatisch ein Upgrade von Windows 7 oder höher auf Windows 10 durchgeführt werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 4a3c69edc85a4ea7501510b6b3f12c72ad3a24ff
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die Tasksequenzen in System Center Configuration Manager, um auf einem Zielcomputer automatisch ein Betriebssystemupgrade von Windows 7 oder höher auf Windows 10 oder von Windows Server 2012 oder höher auf Windows Server 2016 durchzuführen. Sie erstellen eine Tasksequenz, die auf das Betriebssystemimage, das Sie auf dem Zielcomputer installieren möchten, und auf alle anderen zu installierenden zusätzlichen Inhalte verweist, z. B. Anwendungen oder Softwareupdates. Die Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem ist Teil des Szenarios [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md).  

##  <a name="BKMK_UpgradeOS"></a> Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem  
 Um ein Upgrade des Betriebssystems auf Computern durchzuführen, können Sie eine Tasksequenz erstellen und im Assistenten zum Erstellen von Tasksequenzen die Option zum **Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket** auswählen. Der Assistent fügt die Schritte zum Durchführen des Upgrades für das Betriebssystem, zum Anwenden von Softwareupdates und zum Installieren von Anwendungen hinzu. Bevor Sie die Tasksequenz erstellen, muss Folgendes verfügbar sein:    

-   **Erforderlich**  

     - Das [Upgradepaket für das Betriebssystem](../get-started/manage-operating-system-upgrade-packages.md) muss in der Configuration Manager-Konsole verfügbar sein.
     - Wenn Sie ein Upgrade auf Windows Server 2016 durchführen, müssen Sie im Tasksequenzschritt „Betriebssystem aktualisieren“ die Einstellung **Alle verwerfbaren Konformitätsmeldungen ignorieren** auswählen. Andernfalls tritt beim Upgrade ein Fehler auf.

-   **Erforderlich (sofern verwendet)**  

    -   [Softwareupdates](../../sum/get-started/synchronize-software-updates.md) müssen in der Configuration Manager-Konsole synchronisiert werden.  

    -   [Anwendungen](../../apps/deploy-use/create-applications.md) müssen zur Configuration Manager-Konsole hinzugefügt werden.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>So erstellen Sie eine Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Klicken Sie auf der Seite **Neue Tasksequenz erstellen** auf die Option zum **Durchführen eines Upgrades für ein Betriebssystem mit einem Upgradepaket**, und klicken Sie dann auf **Weiter**.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Tasksequenzname**: Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der Aufgabe an, die von der Tasksequenz ausgeführt wird.  

6.  Geben Sie auf der Seite zum **Durchführen eines Upgrades für das Windows-Betriebssystem** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Upgradepaket**: Geben Sie die Upgradepaket, das die Quelldateien für das Upgrade des Betriebssystems enthält. Sie können überprüfen, ob Sie das richtige Paket ausgewählt haben, indem Sie die Informationen im **Eigenschaften** -Bereich betrachten. Weitere Informationen finden Sie unter [Verwalten von Betriebssystem-Upgradepaketen](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Editionsindex**: Wenn mehrere Editionsindizes für das Betriebssystem im Paket verfügbar sind, wählen Sie den gewünschten Editionsindex aus. Standardmäßig wird das erste Element ausgewählt.  

    -   **Product key**: Geben Sie den Product Key für das zu installierende Windows-Betriebssystem an. Sie können codierte Volumenlizenzschlüssel und standardmäßige Product Keys angeben. Wenn Sie einen nicht codierten Product Key verwenden, muss jede Gruppe aus fünf Zeichen durch einen Bindestrich (-) getrennt werden. Beispiel: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Wenn das Upgrade für eine Volumenlizenzedition vorgesehen ist, ist der Product Key nicht erforderlich. Sie benötigen nur einen Product Key, wenn das Upgrade für eine Verkaufsversion von Windows vorgesehen ist.  

    -   **Alle verwerfbaren Konformitätsmeldungen ignorieren**: Wählen Sie diese Einstellung aus, wenn Sie ein Upgrade auf Windows Server 2016 durchführen. Wenn Sie diese Einstellung nicht auswählen, kann die Tasksequenz nicht abgeschlossen werden, weil Windows Setup darauf wartet, dass der Benutzer in einem Bestätigungsdialogfeld in einer Windows-App auf **Bestätigen** klickt.   

7.  Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche Softwareupdates, alle Softwareupdates oder keine Softwareupdates installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur Softwareupdates installiert, die für Sammlungen bestimmt sind, in denen der Zielcomputer Mitglied ist.  

8.  Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

9. Schließen Sie den Assistenten ab.  



## <a name="configure-pre-cache-content"></a>Konfigurieren des zwischengespeicherten Inhalts
Ab Version 1702 können Sie für verfügbare Bereitstellungen von Tasksequenzen die Zwischenspeicherungsfunktion verwenden, damit Clients nur relevante Inhalte herunterladen, bevor ein Benutzer den Inhalt installiert.
> [!TIP]  
> Seit der Version 1702 ist das Zwischenspeichern eine vorab veröffentlichtes Funktion. Wie Sie es aktivieren, erfahren Sie unter [Features der Vorabversion in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

Ein Beispiel: Es soll eine Tasksequenz für ein direktes Upgrade von Windows 10 bereitgestellt werden, es soll nur eine einzige Tasksequenz für alle Benutzer verwendet werden und es sollen mehrere Architekturen und/oder Sprachen verfügbar sein. Wenn Sie in einer Version vor der Version 1702 eine verfügbare Bereitstellung erstellen und der Benutzer anschließend im Software Center auf **Installieren** klickt, wird der Inhalt zu diesem Zeitpunkt heruntergeladen. Dadurch verzögert sich der Installationsstart. Alle Inhalte, auf die in der Tasksequenz verwiesen wird, werden heruntergeladen. Dies schließt das Betriebssystem-Aktualisierungspaket für alle Sprachen und Architekturen mit ein. Wenn jede Sprache/Architektur ungefähr drei GB umfasst, kann das Downloadpaket sehr groß sein.

Mit der Funktion zum Zwischenspeichern von Inhalten können Sie den Client dahingehend einschränken, dass er nur zutreffenden Inhalt herunterladen darf, wenn er die Bereitstellung empfängt. Wenn der Benutzer dann im Softwarecenter auf **Installieren** klickt, steht der Inhalt bereit, und die Installation startet sofort, da der Inhalt bereits auf der lokalen Festplatte gespeichert ist.

### <a name="to-configure-the-pre-cache-feature"></a>So konfigurieren Sie die Zwischenspeicherungsfunktion

1. Erstellen Sie Betriebssystem-Aktualisierungspakete für bestimmte Architekturen und Sprachen. Geben Sie die Architektur und die Sprache auf der Registerkarte **Datenquelle** des Pakets an. Verwenden Sie für die Sprache die Dezimalkonvertierung (1033 ist beispielsweise der Dezimalwert für Englisch, 0x0409 seine hexadezimale Entsprechung). Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    Die Architektur- und Sprachwerte werden verwendet, um Tasksequenz-Schrittbedingungen abzugleichen, die Sie im nächsten Schritt erstellen, um festzulegen, ob das Betriebssystem-Aktualisierungspaket zwischengespeichert werden soll.
2. Erstellen Sie eine Tasksequenz mit bedingten Schritten für die verschiedenen Sprachen und Architekturen. Für die englische Version könnten Sie z.B. wie folgt einen Schritt erstellen:

    ![Zwischenspeicherungseigenschaften](../media/precacheproperties2.png)

    ![Zwischenspeicherungsoptionen](../media/precacheoptions2.png)  

3. Bereitstellen der Tasksequenz Konfigurieren Sie für die Zwischenspeicherungsfunktion Folgendes:
    - Wählen Sie auf der Registerkarte **Allgemein** die Option **Inhalt für diese Tasksequenz vorab herunterladen** aus.
    - Konfigurieren Sie auf der Registerkarte **Bereitstellungseinstellungen** die Tasksequenz mit der Einstellung **Verfügbar** für **Zweck**. Bei der Erstellung einer Bereitstellung des Typs **Erforderlich** ist die Zwischenspeicherfunktion nicht verfügbar.
    - Wählen Sie auf der Registerkarte **Planung** für die Einstellung **Verfügbarkeitsdatum der Bereitstellung festlegen** einen in der Zukunft liegenden Zeitpunkt aus, der Clients genügend Zeit bietet, um den Inhalt zwischenzuspeichern, bevor die Bereitstellung für Benutzer verfügbar gemacht wird. Sie können den Verfügbarkeitszeitpunkt beispielsweise auf drei Stunden später setzen, um ausreichend Zeit für das Zwischenspeichern des Inhalts vorzusehen.  
    - Konfigurieren Sie auf der Registerkarte **Verteilungspunkte** die Einstellungen der **Bereitstellungsoptionen**. Wenn der Inhalt noch nicht auf einem Client zwischengespeichert ist, wenn ein Benutzer die Installation startet, werden diese Einstellungen verwendet.


### <a name="user-experience"></a>Benutzerfreundlichkeit
- Wenn der Client die Bereitstellungsrichtlinie erhält, startet er mit der Zwischenspeicherung des Inhalts. Dies umfasst alle referenzierten Inhalte (alle anderen Pakettypen) und nur das Betriebssystem-Aktualisierungspaket, das dem Client entspricht, und zwar basierend auf den von Ihnen in der Tasksequenz festgelegten Bedingungen.
- Wenn die Bereitstellung Benutzern verfügbar gemacht wird (Einstellung auf der Registerkarte **Planung** der Bereitstellung), wird eine Benachrichtigung angezeigt, um Benutzer über die neue Bereitstellung zu informieren. Die Bereitstellung wird dann ferner im Softwarecenter angezeigt. Der Benutzer kann zum Softwarecenter navigieren und auf **Installieren** klicken, um die Installation zu starten.
- Wenn der Inhalt nicht vollständig zwischengespeichert ist, werden die Einstellungen verwendet, die auf der Registerkarte **Bereitstellungsoptionen** der Bereitstellung angegeben wurden. Es wird empfohlen, genügend Zeit zwischen der Erstellung der Bereitstellung und dem Zeitpunkt der Verfügbarmachung der Bereitstellung für Benutzer vorzusehen, damit Clients ausreichend Zeit haben, um den Inhalt zwischenzuspeichern.



## <a name="download-package-content-task-sequence-step"></a>Paketinhalt herunterladen – Tasksequenzschritt  
 Der Schritt [Paketinhalt herunterladen](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) kann in den folgenden Szenarios vor dem Schritt **Betriebssystem aktualisieren** ausgeführt werden:  

-   Sie verwenden eine einzige Upgradetasksequenz, die sowohl für x86- als auch für x64-Plattformen verwendet werden kann. Um dies zu erreichen, fügen Sie zwei **Paketinhalt herunterladen** -Schritte zur Gruppe **Vorbereitung auf das Upgrade** hinzu, und geben Sie Bedingungen an, um die Clientarchitektur zu ermitteln und nur das entsprechende Betriebssystemupgradepaket herunterzuladen. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den Medienpfad im Schritt **Betriebssystem aktualisieren** .  

-   Um dynamisch ein passendes Treiberpaket herunterzuladen, verwenden Sie zwei **Paketinhalt herunterladen** -Schritte mit Bedingungen zum Ermitteln des geeigneten Hardwaretyps für jedes Treiberpaket. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den **Bereitgestellter Inhalt** -Wert im Bereich „Treiber“ im Schritt **Betriebssystem aktualisieren** .  

   > [!NOTE]
   > Wenn es mehrere Pakete gibt, fügt Configuration Manager dem Variablennamen ein numerisches Suffix hinzu. Wenn Sie beispielsweise eine Variable %mycontent% als eine benutzerdefinierte Variable angeben, ist dies das Stammverzeichnis, in dem alle referenzierten Inhalte gespeichert werden (dies können mehrere Pakete sein). Wenn Sie in einem Untersequenzschritt auf die Variable verweisen, z. B. „Betriebssystem aktualisieren“, wird sie mit einem numerischen Suffix verwendet. In diesem Beispiel %mycontent01% oder %mycontent02%, wobei die Nummer der Reihenfolge entspricht, in der das Paket in diesem Schritt aufgelistet ist.

## <a name="optional-post-processing-task-sequence-steps"></a>Optionale Nachbearbeitung – Tasksequenzschritte  
 Nachdem Sie die Tasksequenz erstellt haben, können Sie zusätzliche Schritte zum Deinstallieren von Anwendungen mit bekannten Kompatibilitätsproblemen oder Maßnahmen zur Nachbearbeitung hinzufügen, die nach einem Neustart des Computers und der erfolgreichen Durchführung des Upgrades auf Windows 10 ausgeführt werden. Fügen Sie diese zusätzlichen Schritte in der Nachbearbeitungsgruppe der Tasksequenz hinzu.  

> [!NOTE]  
>  Da diese Tasksequenz nicht linear verläuft, gibt es Situationen bei den einzelnen Schritten, die sich auf die Ergebnisse der Tasksequenz auswirken können, je nachdem, ob der Clientcomputer erfolgreich aktualisiert wurde oder ob ein Rollback des Clientcomputers auf die ursprüngliche Betriebssystemversion durchgeführt werden muss.  

## <a name="optional-rollback-task-sequence-steps"></a>Optionales Rollback – Tasksequenzschritte  
 Wenn beim Upgradeprozess nach dem Neustart des Computers ein Fehler auftritt, führt Setup eine Rollback für das Upgrade auf das vorherige Betriebssystem durch und die Tasksequenz wird mit den Schritten in der Rollbackgruppe fortgesetzt. Nach dem Erstellen der Tasksequenz können Sie optionale Schritte zur Rollbackgruppe hinzufügen.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Nach Computerneustart entfernte Ordner und Dateien  
 Wenn die Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem auf Windows 10 und alle anderen Schritte in der Tasksequenz durchgeführt wurden, werden die Nachbearbeitungs- und Rollback-Skripts erst nach dem Neustart des Computers entfernt.  Diese Skriptdateien enthalten keine vertraulichen Informationen.  
