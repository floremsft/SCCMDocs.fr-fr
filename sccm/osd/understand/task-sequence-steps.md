---
title: "Tasksequenzschritte – Configuration Manager | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über die Tasksequenzschritte, die einer Configuration Manager-Tasksequenz hinzugefügt werden können."
ms.custom: na
ms.date: 03/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: "26"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: e0726febc4c36a26c5e067914734838bf2681e6c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Tasksequenzschritte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die folgenden Tasksequenzschritte können einer Configuration Manager-Tasksequenz hinzugefügt werden. Weitere Informationen zum Bearbeiten einer Tasksequenz finden Sie unter [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  


##  <a name="BKMK_ApplyDataImage"></a> Anwenden eines Tasksequenzschritts „Datenimage anwenden“  
 Mithilfe des Tasksequenzschritts **Datenabbild anwenden** können Sie das Datenabbild auf die angegebene Zielpartition kopieren.  

 Dieser Schritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Tasksequenz-Aktionsvariablen](task-sequence-action-variables.md).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Imagepaket**  
 Gibt das **Abbildpaket** an, das von diesem Tasksequenzschritt verwendet wird. Klicken Sie dazu auf **Durchsuchen**. Wählen Sie das zu installierende Paket im Dialogfeld **Paket auswählen** aus. Die zugeordneten Eigenschaftsinformationen für jedes vorhandene Abbildpaket werden unten im Dialogfeld **Paket auswählen** angezeigt. Wählen Sie mithilfe der Dropdownliste das zu installierende **Abbild** aus dem ausgewählten **Abbildpaket**aus.  

> [!NOTE]  
>  Bei dieser Tasksequenzaktion wird das Abbild wie eine Datendatei behaltet; es werden keine der erforderlichen Konfigurationsmaßnahmen ergriffen, damit das Abbild als Betriebssystem gestartet werden kann.  

 **Ziel**  
 Gibt eine vorhandene formatierte Partition und Festplatte, einen bestimmten Buchstaben für ein logisches Laufwerk oder den Namen einer Tasksequenzvariablen an, die den Buchstaben für das logische Laufwerk enthält.  

-   **Nächste verfügbare Partition**: Verwendet die nächste verfügbare Partition, die in dieser Tasksequenz nicht bereits für eine Aktion „Betriebssystem anwenden“ oder „Datenimage anwenden“ verwendet wurde.  

-   **Bestimmter Datenträger und Partition**: Wählen Sie die Nummer des **Datenträgers** (beginnend mit 0) und die Nummer der **Partition** (beginnend mit 1) aus.  

-   **Bestimmter Buchstabe für logisches Laufwerk**: Geben Sie den **Laufwerkbuchstaben** ein, der der Partition von Windows PE zugewiesen wurde. Beachten Sie, dass sich dieser Laufwerkbuchstabe von dem Laufwerkbuchstaben unterscheiden kann, der von dem neu bereitgestellten Betriebssystem zugewiesen wird.  

-   **In Variable gespeicherter Buchstabe für logisches Laufwerk**: Geben Sie die Tasksequenzvariable an, die den der Partition von Windows PE zugewiesenen Laufwerksbuchstaben enthält. Diese Variable wurde in der Regel im Bereich „Erweitert“ des Dialogfelds **Partitionseigenschaften** für die Tasksequenzaktion **Datenträger formatieren und partitionieren** eingestellt.  

 **Vor dem Anwenden des Images den gesamten Inhalt der Partition löschen**  
 Gibt an, dass alle Dateien in der Zielpartition gelöscht werden, bevor das Abbild installiert wird. Indem der Inhalt dieser Partition nicht gelöscht wird, kann mit diesem Schritt einer zuvor eingerichteten Partition weiterer Inhalt zugewiesen werden.  

##  <a name="BKMK_ApplyDriverPackage"></a> Treiberpaket anwenden  
 Mithilfe des Tasksequenzschritts **Treiberpaket anwenden** können Sie alle Treiber im Treiberpaket herunterladen und auf dem Windows-Betriebssystem installieren.

 Mit dem Tasksequenzschritt **Treiberpaket anwenden** können Sie alle Gerätetreiber eines Treiberpakets zur Verwendung in Windows bereitstellen. Dieser Schritt kann in einer Tasksequenz zwischen den Schritten **Betriebssystem anwenden**  und **Windows und ConfigMgr einrichten** eingefügt werden, um Windows die im Treiberpaket enthaltenen Gerätetreiber zur Verfügung zu stellen. Der Schritt **Treiberpaket anwenden** wird in der Regel hinter dem Schritt **Treiber automatisch anwenden** eingefügt. Der Tasksequenzschritt **Treiberpaket anwenden** ist auch für die Bereitstellung mithilfe eigenständiger Medien nützlich.  

 Stellen Sie sicher, dass ähnliche Gerätetreiber in einem Treiberpaket zusammengestellt werden, und verteilen Sie diese auf die entsprechenden Verteilungspunkte. Nachdem die Treiber verteilt sind, können sie von Configuration Manager-Clientcomputern installiert werden. Beispiel: Sie können alle Gerätetreiber eines Herstellers in einem Treiberpaket zusammenstellen und das Paket dann an Verteilungspunkte verteilen, an denen die zugeordneten Computer auf das Paket zugreifen können.

 Dieser Schritt unterstützt eigenständige Medien und Administratoren, die bestimmte Treiber installieren möchten, darunter Treiber für Geräte, die im Rahmen einer Plug-and-Play-Prüfung nicht erkannt würden (beispielsweise Netzwerkdrucker).  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Apply Driver Package Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Treiberpaket**  
 Klicken Sie auf **Durchsuchen** , und öffnen Sie das Dialogfeld **Paket auswählen** , um das Treiberpaket anzugeben, das die erforderlichen Gerätetreiber enthält. Geben Sie ein vorhandenes Paket an, das verfügbar gemacht werden soll. Die zugehörigen Paketeigenschaften werden unten im Dialogfeld angezeigt.  

 **Wählen Sie den Massenspeichertreiber im Paket aus, der bei allen Betriebssystemen vor Vista vor dem Setup installiert werden muss**  
 Geben Sie alle Massenspeichertreiber an, die für die Installation von Betriebssystemen vor Windows Vista erforderlich sind.  

 **Treiber**  
 Wählen Sie die Massenspeicher-Treiberdatei aus, die installiert werden muss, bevor das Setup auf Bereitstellungen von Betriebssystemen vor Windows Vista durchgeführt werden kann. Die Dropdownliste wird mit den Treibern aus dem angegebenen Paket aufgefüllt.  

 **Modell**  
 Geben Sie das für den Systemstart erforderliche Gerät an, das für Bereitstellungen von Betriebssystemen vor Windows Vista erforderlich ist.  

 **Unbeaufsichtigte Installation von nicht signierten Treibern bei Windows-Versionen ausführen, wenn zulässig**  
 Wählen Sie diese Option aus, um Windows die Installation von nicht signierten Treibern auf dem Referenzcomputer zu gewähren.  

##  <a name="BKMK_ApplyNetworkSettings"></a> Schritt „Netzwerkeinstellungen anwenden“  
 Mithilfe des Tasksequenzschritts **Netzwerkeinstellungen anwenden** können Sie die Konfigurationsinformationen für das Netzwerk oder die Arbeitsgruppe des Zielcomputers angeben. Die angegebenen Werte werden im entsprechenden Antwortdateiformat gespeichert und für die Verwendung durch Windows-Setup beim Ausführen des Tasksequenzschritts **Windows und ConfigMgr einrichten** zur Verfügung gestellt.  

 Dieser Tasksequenzschritt wird entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Apply Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Einer Arbeitsgruppe beitreten**  
 Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Arbeitsgruppe hinzuzufügen. Geben Sie den Namen der Arbeitsgruppen in die Zeile **Arbeitsgruppe** ein. Dieser Wert kann durch den Wert überschrieben werden, der mit dem Tasksequenzschritt **Netzwerkeinstellungen erfassen** erfasst wird.  

 **Einer Domäne beitreten**  
 Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Domäne hinzuzufügen. Geben Sie die Domäne an, oder klicken Sie auf "Durchsuchen", um die Domäne auszuwählen, z. B. *fabricam.com*. Geben Sie einen LDAP-Pfad (Lightweight Directory Access Protocol) für eine Organisationseinheit an, oder suchen Sie nach dem LDAP-Pfad (z.B. LDAP//OU=computers, DC=Fabricam.com, C=com).  

 **Konto**  
 Klicken Sie auf **Festlegen** , um ein Konto anzugeben, das die für den Beitritt zur Domäne erforderlichen Berechtigungen aufweist. Im Dialogfeld **Windows-Benutzerkonto** können Sie den Benutzernamen in folgendem Format eingeben: **Domäne\Benutzer** .  

 **Netzwerkkarteneinstellungen**  
 Geben Sie die Netzwerkkonfigurationen für alle Netzwerkadapter auf dem Computer an. Klicken Sie auf **Neu** , um das Dialogfeld **Netzwerkeinstellungen** zu öffnen, und geben Sie dann die Netzwerkeinstellungen an. Wenn die Netzwerkeinstellungen in einem vorherigen Tasksequenzschritt **Netzwerkeinstellungen erfassen** erfasst wurden, werden die vorherigen Einstellungen auf den Netzwerkadapter angewendet und die in diesem Schritt angegebenen Einstellungen werden ignoriert. Wenn zuvor noch keine Netzwerkeinstellungen erfasst wurden, werden die im Schritt **Netzwerkeinstellungen anwenden** angegebenen Einstellungen in der Reihenfolge der Windows-Geräteaufzählung auf Netzwerkadapter angewendet.  

##  <a name="BKMK_ApplyOperatingSystemImage"></a> Betriebssystemimage anwenden  
 Mithilfe des Tasksequenzschritts **Betriebssystemabbild anwenden** können Sie ein Betriebssystem auf dem Zielcomputer installieren. Bei dieser Tasksequenzaktion wird eine Reihe von Aktionen ausgeführt, die davon abhängen, ob ein Betriebssystemabbild oder ein Installationspaket für ein Betriebssystem verwendet wird.  

 Wenn ein Betriebssystemabbild verwendet wird, werden mit dem Schritt **Betriebssystemabbild anwenden** die folgenden Aktionen ausgeführt:  

1.  Mit Ausnahme der Dateien in dem mit der Tasksequenzvariablen &#95;SMSTSUserStatePath angegebenen Ordner wird der gesamte Inhalt auf dem Zielvolumen gelöscht.  

2.  Extrahiert den Inhalt der angegebenen WIM-Datei in die angegebene Zielpartition.  

3.  Bereitet die Antwortdatei vor:  

    1.  Eine neue Standardantwortdatei für Windows Setup (sysprep.inf oder unattend.xml) wird für das bereitzustellende Betriebssystem erstellt.  

    2.  Übernimmt alle Werte aus der vom Benutzer bereitgestellten Antwortdatei.  

4.  Kopiert Windows-Startladeprogramme in die aktive Partition.  

5.  Konfiguriert die Datei „boot.ini“ bzw. die Startkonfigurationsdaten (Boot Configuration Data, BCD) mit einem Verweis auf das neu installierte Betriebssystem.  

 Wenn ein Installationspaket für das Betriebssystemabbild verwendet wird, werden mit dem Schritt **Betriebssystemabbild anwenden** die folgenden Aktionen ausgeführt:  

1.  Mit Ausnahme der Dateien in dem mit der Tasksequenzvariablen &#95;SMSTSUserStatePath angegebenen Ordner wird der gesamte Inhalt auf dem Zielvolumen gelöscht.  

2.  Bereitet die Antwortdatei vor:  

    1.  Erstellt eine neue Antwortdatei mit von Configuration Manager erstellten Standardwerten.  

    2.  Übernimmt alle Werte aus der vom Benutzer bereitgestellten Antwortdatei.  

> [!NOTE]  
>  Die eigentliche Windows-Installation wird vom Tasksequenzschritt **Windows und ConfigMgr einrichten** gestartet. Nach Ausführung der Tasksequenzaktion **Betriebssystem anwenden** wird die Tasksequenzvariable „OSDTargetSystemDrive“ auf den Laufwerksbuchstaben der Partition gesetzt, in der sich die Betriebssystemdateien befinden.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Apply Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   **Auf Inhalt direkt vom Verteilungspunkt aus zugreifen**:  

     Verwenden Sie diese Option, um anzugeben, ob die Tasksequenz direkt vom Verteilungspunkt aus auf das Betriebssystemabbild zugreifen soll. Sie können diese Option z. B. verwenden, wenn Sie Betriebssysteme für eingebettete Geräte mit begrenzter Speicherkapazität bereitstellen. Wenn diese Option aktiviert ist, müssen Sie auch die Einstellungen für die Paketfreigabe auf der Registerkarte **Datenzugriff** der Paketeigenschaften konfigurieren.  

    > [!NOTE]  
    >  Mit dieser Einstellung wird die auf der Seite **Verteilungspunkte** im **Assistenten zum Bereitstellen von Software** abgegebene Bereitstellungsoption nur für das Betriebssystemabbild überschrieben, das in diesem Tasksequenzschritt angegeben ist, nicht jedoch für den ganzen Inhalt der gesamten Tasksequenz.  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Betriebssystem von einem erfassten Image übernehmen**  
 Installiert ein zuvor erfasstes Betriebssystemabbild. Klicken Sie auf **Durchsuchen** , um das Dialogfeld **Paket auswählen** zu öffnen, und wählen Sie dann das vorhandene Abbildpaket aus, das Sie installieren möchten. Wenn mehrere Abbilder mit dem angegebenen **Abbildpaket**verknüpft sind, geben Sie das zugehörige Abbild für diese Bereitstellung mithilfe der Dropdownliste an. Sie können zu jedem vorhandenen Abbild grundlegende Informationen anzeigen, indem Sie auf das Abbild klicken.  

 **Betriebssystem von einer ursprünglichen Installationsquelle übernehmen**  
 Installiert ein Betriebssystem mithilfe einer ursprünglichen Installationsquelle. Klicken Sie auf **Durchsuchen** , um das Dialogfeld **Betriebssysteminstallationspaket auswählen** zu öffnen, und wählen Sie dann das Betriebssysteminstallationspaket aus, das Sie verwenden möchten. Sie können zu jeder vorhandenen Abbildquelle grundlegende Informationen anzeigen, indem Sie auf die Abbildquelle klicken. Die zugeordneten Eigenschaften der Abbildquelle werden unten im Dialogfeld im Ergebnisbereich angezeigt. Falls dem angegebenen Paket mehrere Editionen zugeordnet sind, geben Sie die verwendete zugeordnete **Edition** in der Dropdownliste an.  

 **Datei für unbeaufsichtigte Installation oder Antwortdatei für Systemvorbereitung bei benutzerdefinierter Installation verwenden**  
 Stellen Sie mit dieser Option je nach Betriebssystemversion und Installationsmethode eine Windows Setup-Antwortdatei (**unattend.xml**, **unattend.txt**oder **sysprep.inf**) bereit. Die von Ihnen angegebene Datei kann alle Standardkonfigurationsoptionen enthalten, die von Windows-Antwortdateien unterstützt werden. Sie können damit beispielsweise die Standardstartseite im Internet Explorer angeben. Sie müssen das Paket mit der Antwortdatei sowie den entsprechenden Pfad zu der Datei im Paket angeben.  

> [!NOTE]  
>  Die angegebene Windows Setup-Antwortdatei kann eingebettete Tasksequenzvariablen im Format %*varname*% enthalten, wobei „varname“ der Name der Variable ist. Die Zeichenfolge %*varname*% wird in der Tasksequenzaktion **Windows und ConfigMgr einrichten** durch die richtigen Variablenwerte ersetzt. Beachten Sie jedoch, dass diese eingebetteten Tasksequenzvariablen in den Antwortdateien „unattend.xml“ nicht in rein numerischen Feldern verwendet werden können.  

 Wenn Sie keine Windows Setup-Antwortdatei angeben, generiert diese Tasksequenzaktion automatisch eine Antwortdatei.  

 **Ziel**  
 Gibt eine vorhandene formatierte Partition und Festplatte, einen bestimmten Buchstaben für ein logisches Laufwerk oder den Namen einer Tasksequenzvariablen an, die den Buchstaben für das logische Laufwerk enthält.  

-   **Nächste verfügbare Partition**: Verwendet die nächste verfügbare Partition, die in dieser Tasksequenz nicht bereits für eine Aktion „Betriebssystem anwenden“ oder „Datenimage anwenden“ verwendet wurde.  

-   **Bestimmter Datenträger und Partition**: Wählen Sie die Nummer des **Datenträgers** (beginnend mit 0) und die Nummer der **Partition** (beginnend mit 1) aus.  

-   **Bestimmter Buchstabe für logisches Laufwerk**: Geben Sie den **Laufwerkbuchstaben** ein, der der Partition von Windows PE zugewiesen wurde. Beachten Sie, dass sich dieser Laufwerkbuchstabe von dem Laufwerkbuchstaben unterscheiden kann, der von dem neu bereitgestellten Betriebssystem zugewiesen wird.  

-   **In Variable gespeicherter Buchstabe für logisches Laufwerk**: Geben Sie die Tasksequenzvariable an, die den der Partition von Windows PE zugewiesenen Laufwerksbuchstaben enthält. Diese Variable wurde in der Regel im Bereich „Erweitert“ des Dialogfelds **Partitionseigenschaften** für die Tasksequenzaktion **Datenträger formatieren und partitionieren** eingestellt.  

##  <a name="BKMK_ApplyWindowsSettings"></a> Windows-Einstellungen anwenden  
 Mithilfe des Tasksequenzschritts **Windows-Einstellungen anwenden** können Sie die Windows-Einstellungen für den Zielcomputer konfigurieren. Die angegebenen Werte werden im entsprechenden Antwortdateiformat gespeichert und für die Verwendung durch Windows-Setup beim Ausführen des Tasksequenzschritts **Windows und ConfigMgr einrichten** zur Verfügung gestellt.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Apply Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Benutzername**  
 Geben Sie den registrierten Benutzernamen an, der dem Zielcomputer zugeordnet ist. Dieser Wert kann durch den Wert überschrieben werden, der mit der Tasksequenzaktion **Windows-Einstellungen erfassen** erfasst wird.  

 **Name der Organisation**  
 Geben Sie den registrierten Organisationsnamen an, der dem Zielcomputer zugeordnet ist. Dieser Wert kann durch den Wert überschrieben werden, der mit der Tasksequenzaktion **Windows-Einstellungen erfassen** erfasst wird.  

 **Product Key**  
 Geben Sie den Product Key an, der für die Windows-Installation auf dem Bereitstellungszielcomputer verwendet wird.  

 **Serverlizenzierung**  
 Geben Sie den Serverlizenzierungsmodus an. Sie können als Lizenzierungsmodus **Pro Server** oder **Pro Benutzer** auswählen. Wenn Sie „Pro Server“ als Lizenzierungsmodus auswählen, müssen Sie auch die maximale Anzahl der Verbindungen angeben, die gemäß Ihrem Lizenzvertrag zulässig sind. Falls der Bereitstellungszielcomputer kein Server ist oder Sie den Lizenzierungsmodus nicht angeben möchten, wählen Sie **Nicht angeben** aus.  

 **Maximale Verbindungen**  
 Geben Sie die maximale Anzahl der Verbindungen an, die für diesen Computer gemäß Ihrem Lizenzvertrag zulässig sind.  

 **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren (empfohlen)**  
 Wählen Sie diese Option aus, um ein lokales Administratorkennwort zufällig zu generieren. Hiermit wird ein lokales Administratorkennwort erstellt und veranlasst, dass das Konto auf unterstützten Plattformen deaktiviert wird.  

 **Konto aktivieren und lokales Administratorkennwort angeben**  
 Wählen Sie diese Option aus, wenn Sie das lokale Administratorkonto aktivieren und das lokale Administratorkennwort erstellen möchten. Geben Sie das Kennwort in der Zeile **Kennwort** ein, und bestätigen Sie es in der Zeile **Kennwort bestätigen** .  

 **Zeitzone**  
 Geben Sie die zu konfigurierende Zeitzone auf dem Zielcomputer an. Dieser Wert kann durch den Wert überschrieben werden, der mit dem Tasksequenzschritt **Windows-Einstellungen erfassen** erfasst wird.  

##  <a name="BKMK_AutoApplyDrivers"></a> Treiber automatisch anwenden  
 Mithilfe des Tasksequenzschritts **Treiber automatisch anwenden** können Sie die geeigneten Treiber als Teil einer Betriebssystembereitstellung auswählen und installieren.  

 Mit dem Tasksequenzschritt **Treiber automatisch anwenden** werden folgende Aktionen ausgeführt:  

1.  Überprüft die Hardware und ermittelt die Plug-and-Play-IDs für alle auf dem System vorhandenen Geräte.  

2.  Sendet die Liste mit den Geräten und den ihnen zugeordneten Plug-and-Play-IDs an den Verwaltungspunkt. Der Verwaltungspunkt gibt für jedes Gerät eine Liste mit kompatiblen Treibern aus dem Treiberkatalog zurück. Der Verwaltungspunkt berücksichtigt alle Treiber unabhängig davon, in welchem Treiberpaket sie enthalten sind. Nur mit der angegebenen Treiberkategorie gekennzeichnete Treiber und Treiber, die nicht als deaktiviert gekennzeichnet sind, werden berücksichtigt.  

3.  Der Client wählt für jedes Gerät den Treiber aus, der sich für das Betriebssystem, auf dem er installiert wird, am besten eignet, und der sich auf einem verfügbaren Verteilungspunkt befindet.  

4.  Die ausgewählten Treiber werden von einem Verteilungspunkt heruntergeladen und auf dem Zielbetriebssystem bereitgestellt.  

    1.  Für abbildbasierte Installationen werden die Treiber im Treiberspeicher des Betriebssystems abgelegt.  

    2.  Bei setupbasierten Installationen wird im Windows-Setup festgelegt, wo die Treiber zu finden sind.  

5.  Wenn die Tasksequenzaktion **Windows und ConfigMgr einrichten** ausgeführt wird, werden die von dieser Aktion bereitgestellten Treiber beim ersten Windows-Start gefunden.  

> [!IMPORTANT]
>  Der Tasksequenzschritt **Treiber automatisch anwenden** kann nicht auf eigenständigen Medien verwendet werden, da Windows Setup in diesem Fall nicht über eine Verbindung mit dem Configuration Manager-Standort verfügt.

Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Auto Apply Drivers Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Nur Treiber mit der höchsten Kompatibilität installieren**  
 Hiermit wird angegeben, dass vom Tasksequenzschritt nur der am besten geeignete Treiber für das jeweilige erkannte Hardwaregerät installiert wird.  

 **Alle kompatiblen Treiber installieren**  
 Hiermit wird angegeben, dass vom Tasksequenzschritt alle kompatiblen Treiber für das jeweilige erkannte Hardwaregerät installiert werden und der beste Treiber von Windows Setup ausgewählt werden kann. Von dieser Option werden mehr Netzwerkbandbreite und Speicherplatz beansprucht, da mit ihr mehr Treiber heruntergeladen werden. Möglicherweise wird dadurch jedoch ein besserer Treiber ausgewählt.  

 **Treiber aller Kategorien berücksichtigen**  
 Hiermit wird angegeben, dass von der Tasksequenzaktion in allen verfügbaren Treiberkategorien nach den geeigneten Gerätetreibern gesucht wird.  

 **Nur Treiber in bestimmten Kategorien berücksichtigen**  
 Hiermit wird angegeben, dass von der Tasksequenzaktion in angegebenen Treiberkategorien nach den geeigneten Gerätetreibern gesucht wird.  

 **Unbeaufsichtigte Installation von nicht signierten Treibern bei Windows-Versionen ausführen, wenn zulässig**  
 Ermöglicht dieser Tasksequenzaktion, nicht signierte Windows-Gerätetreiber zu installieren.  

> [!IMPORTANT]  
>  Diese Option gilt nicht für Betriebssysteme, deren Richtlinie für Treibersignierung nicht konfiguriert werden kann.  

##  <a name="BKMK_CaptureNetworkSettings"></a> Netzwerkeinstellungen erfassen  
 Verwenden Sie den Tasksequenzschritt **Netzwerkeinstellungen erfassen** zum Erfassen der Microsoft-Netzwerkeinstellungen des Computers, auf dem die Tasksequenz ausgeführt wird. Die Einstellungen werden in Tasksequenzvariablen gespeichert, die die im Tasksequenzschritt **Netzwerkeinstellungen anwenden** konfigurierten Standardeinstellungen außer Kraft setzen.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Capture Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Gibt einen kurzen benutzerdefinierten Namen an, der die in diesem Schritt vorgenommene Aktion beschreibt.  

 **Beschreibung**  
 Bietet ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Domänen- und Arbeitsgruppenmitgliedschaft migrieren**  
 Hiermit werden Informationen zur Domänen- und Arbeitsgruppenmitgliedschaft des Zielcomputers erfasst.  

 **Netzwerkkartenkonfiguration migrieren**  
 Hiermit wird die Netzwerkadapterkonfiguration des Zielcomputers erfasst. Diese Informationen umfassen die globalen Netzwerkeinstellungen, die Anzahl der Netzwerkkarten und die den Karten zugeordneten Netzwerkeinstellungen. Diese Einstellungen umfassen auch DNS-, WINS-, IP- und Portfiltereinstellungen.  

##  <a name="BKMK_CaptureOperatingSystemImage"></a> Betriebssystemabbild erfassen  
 Mithilfe des Tasksequenzschritts **Betriebssystemabbild erfassen** können Sie Abbilder von einem Referenzcomputer erfassen und in einer WIM-Datei auf der angegebenen Netzwerkfreigabe speichern. Diese WIM-Datei kann dann mithilfe des Assistenten zum Hinzufügen eines Betriebssystemimages in Configuration Manager importiert werden, damit sie für imagebasierte Betriebssystembereitstellungen genutzt werden kann.  

 Jedes Volume (Laufwerk) auf dem Referenzcomputer wird als ein separates Abbild in der WIM-Datei erfasst. Wenn der Referenzcomputer über mehrere Volumes verfügt, enthält die erstellte WIM-Datei für jedes Volume ein separates Abbild. Es werden nur als NTFS oder FAT32 formatierte Volumes erfasst. Volumes in anderen Formaten sowie USB-Volumes werden nicht berücksichtigt.  

 Das auf dem Referenzcomputer installierte Betriebssystem muss in einer von Configuration Manager unterstützten Windows-Version vorliegen und mithilfe des SysPrep-Tools vorbereitet worden sein. Bei dem Volume mit dem installierten Betriebssystem und dem Startvolume muss es sich um dasselbe Volume handeln.  

 Sie müssen außerdem ein Windows-Konto eingeben, das über Schreibberechtigung für die von Ihnen ausgewählte Netzwerkfreigabe verfügt.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Capture Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Ziel**  
 Dies ist der Name des Dateisystempfads, der von Configuration Manager zum Speichern des erfassten Betriebssystemimages verwendet wird.  

 **Beschreibung**  
 Eine optionale benutzerdefinierte Beschreibung des erfassten Betriebssystemabbilds, die in der WIM-Datei gespeichert wird.  

 **Version**  
 Eine optionale benutzerdefinierte Versionsnummer, die dem erfassten Betriebssystemabbild zugewiesen wird. Dieser Wert kann aus einer beliebigen Kombination aus Buchstaben und Ziffern bestehen und wird in der WIM-Datei gespeichert.  

 **Erstellt von**  
 Der optionale Name des Benutzers, der das Betriebssystemabbild erstellt hat. Dieser Name wird in der WIM-Datei gespeichert.  

 **Konto für die Erfassung des Betriebssystemimages**  
 Sie müssen das Windows-Konto eingeben, das über Berechtigungen für den Zugriff auf die von Ihnen ausgewählte Netzwerkfreigabe verfügt. Klicken Sie auf **Festlegen** , um den Namen dieses Windows-Kontos anzugeben.  

##  <a name="BKMK_CaptureUserState"></a> Benutzerzustand erfassen  
 Verwenden Sie den Tasksequenzschritt **Benutzerzustand erfassen** , um mithilfe von Windows-EasyTransfer bzw. USMT den Benutzerzustand und die Benutzereinstellungen des Computers zu erfassen, auf dem die Tasksequenz ausgeführt wird. Dieser Tasksequenzschritt wird in Verbindung mit dem Tasksequenzschritt **Benutzerzustand wiederherstellen** verwendet. In USMT 3.0.1 und höher wird der USMT-Zustandsspeicher mit dieser Option stets mit einem von Configuration Manager generierten und verwalteten Verschlüsselungsschlüssel verschlüsselt.  

 Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

 Sie können auch den Tasksequenzschritt **Benutzerzustand erfassen** zusammen mit den Tasksequenzschritten **Zustandsspeicher anfordern** und **Zustandsspeicher freigeben** verwenden, wenn Sie die Zustandseinstellungen in einem Zustandsmigrationspunkt am Configuration Manager-Standort speichern oder von dort aus wiederherstellen möchten.  

 Mit dem Tasksequenzschritt **Benutzerzustand erfassen** kann eine begrenzte Teilmenge der am häufigsten verwendeten USMT-Optionen gesteuert werden. Zusätzliche Befehlszeilenoptionen können mithilfe der Tasksequenzvariablen „OSDMigrateAdditionalCaptureOptions“ angegeben werden.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Capture User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureUserState).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **USMT-Paket (Migrationsprogramm für den Benutzerzustand)**  
 Geben Sie das Configuration Manager-Paket ein, das die USMT-Version enthält, die von diesem Tasksequenzschritt beim Erfassen des Benutzerzustands und der Einstellungen verwendet werden soll. Für dieses Paket ist kein Programm erforderlich. Beim Ausführen des Tasksequenzschritts wird die USMT-Version im angegebenen Paket ausgeführt. Geben Sie je nach Architektur des Betriebssystems, von dem Sie den Zustand erfassen, ein Paket an, das die 32-Bit-Version oder die x64-Version von USMT enthält.  

 **Alle Benutzerprofile mit Standardoptionen erfassen**  
 Wählen Sie diese Option aus, um alle Benutzerprofilinformationen zu migrieren. Diese Option ist standardmäßig ausgewählt.  

 Wenn Sie diese Option auswählen, nicht jedoch die Option zum Wiederherstellen der lokalen Benutzerprofile im Tasksequenzschritt „Benutzerzustand wiederherstellen“, tritt ein Fehler in der Tasksequenz auf, da die neuen Konten nicht von Configuration Manager migriert werden können, ohne dass ihnen Kennwörter zugewiesen werden. Zusätzlich gilt: Wenn Sie im Tasksequenzerstellungs-Assistenten eine Tasksequenz erstellen, um ein bestehendes Abbildpaket zu installieren, wird für die Tasksequenz standardmäßig die Option **Alle Benutzerprofile mit Standardoptionen erfassen** ausgewählt, nicht jedoch die Option **Lokale Computerbenutzerprofile wiederherstellen**(d. h. Nicht-Domänenkontos).  

 Wählen Sie **Lokale Computerbenutzerprofile wiederherstellen** aus, und geben Sie für das zu migrierende Konto ein Kennwort ein. In einer manuell erstellten Tasksequenz finden Sie diese Einstellung im Schritt „Benutzerzustand wiederherstellen“. Wird die Tasksequenz vom **Tasksequenzerstellungs-Assistenten** erstellt, befindet sich diese Einstellung auf der Seite **Benutzerdateien und -einstellungen wiederherstellen** des Assistenten.  

 Wenn Sie über keine lokalen Benutzerkonten verfügen, ist dies nicht relevant.  

 **Erfassung der Benutzerprofile anpassen**  
 Wählen Sie diese Option aus, um eine benutzerdefinierte Profildateimigration anzugeben. Klicken Sie auf **Dateien** , um die von USMT bei diesem Schritt zu verwendenden Konfigurationsdateien auszuwählen. Sie müssen eine benutzerdefinierte XML-Datei angeben, die Rollen zur Definition der zu migrierenden Benutzerzustandsdateien enthält.  

 **Klicken Sie zum Auswählen der Konfigurationsdateien auf diese Schaltfläche:**  
 Wählen Sie diese Option aus, um im USMT-Paket die Konfigurationsdateien auszuwählen, die Sie zum Erfassen von Benutzerprofilen verwenden möchten. Klicken Sie auf die Schaltfläche **Dateien** , um das Dialogfeld **Konfigurationsdateien** zu öffnen. Zum Angeben einer Konfigurationsdatei geben Sie in die Zeile **Dateiname** den Dateinamen ein und klicken auf die Schaltfläche **Hinzufügen** .  

 **Ausführliche Protokollierung aktivieren**  
 Aktivieren Sie diese Option, um ausführlichere Protokolldateiinformationen zu generieren. Beim Erfassen des Zustands wird das Protokoll „Scanstate.log“ generiert und standardmäßig im Tasksequenzprotokoll im Ordner „\windows\system32\ccm\Logs “ gespeichert.  

 **Dateien mit EFS (Encrypted File System) überspringen**  
 Aktivieren Sie diese Option, wenn Sie mit Encrypted File System (EFS) verschlüsselte Dateien (einschließlich Profildateien) beim Erfassen überspringen möchten. Je nach Betriebssystem und USMT-Version sind verschlüsselte Dateien nach der Wiederherstellung möglicherweise nicht lesbar. Weitere Informationen finden Sie in der USMT-Dokumentation.  

 **Mithilfe des normalen Dateisystemzugriffs kopieren**  
 Aktivieren Sie diese Option, um alle oder einige der folgenden Einstellungen anzugeben:  

-   **Fortsetzen, wenn einige Dateien nicht erfasst werden können**: Aktivieren Sie diese Einstellung, um den Migrationsprozess auch dann fortzusetzen, wenn einige Dateien nicht erfasst werden können. Wenn Sie diese Option deaktivieren und eine Datei nicht erfasst werden kann, kann der Tasksequenzschritt nicht ausgeführt werden. Diese Option ist standardmäßig aktiviert.  

-   **Lokal erfassen mithilfe von Links statt durch Kopieren von Dateien**: Aktivieren Sie diese Einstellung, um feste NTFS-Links zum Erfassen von Dateien zu verwenden.  

     Weitere Informationen zum Migrieren von Daten mithilfe von festen Links finden Sie unter [Migrationsspeicher mit festem Link](http://go.microsoft.com/fwlink/p/?LinkId=240222).  

-   **Im Offlinemodus erfassen (nur Windows PE)**: Aktivieren Sie diese Einstellung, um den Benutzerzustand nicht im vollständigen Betriebssystem, sondern in Windows PE zu erfassen.  

 **Mithilfe des Volumeschattenkopie-Diensts (VSS) erfassen**  
 Mithilfe dieser Option können Sie Dateien sogar dann erfassen, wenn sie durch eine andere Anwendung für die Bearbeitung gesperrt sind.  

##  <a name="BKMK_CaptureWindowsSettings"></a> Windows-Einstellungen erfassen  
 Verwenden Sie den Tasksequenzschritt **Windows-Einstellungen erfassen** zum Erfassen der Windows-Einstellungen des Computers, auf dem die Tasksequenz ausgeführt wird. Die Einstellungen werden in Tasksequenzvariablen gespeichert, die die im Tasksequenzschritt **Windows-Einstellungen anwenden** konfigurierten Standardeinstellungen außer Kraft setzen.  

 Dieser Tasksequenzschritt wird entweder in Windows PE oder in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Capture Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Computernamen migrieren**  
 Wählen Sie diese Option aus, um den NetBIOS-Computernamen des Computers zu erfassen.  

 **Registrierte Benutzer- und Organisationsnamen migrieren**  
 Wählen Sie diese Option aus, um auf dem Computer die Namen registrierter Benutzer und Organisationen zu erfassen.  

 **Zeitzone migrieren**  
 Mit dieser Option werden die Zeitzoneneinstellungen auf dem Computer erfasst.  

##  <a name="BKMK_CheckReadiness"></a> Bereitschaft überprüfen  
 Mit dem Tasksequenzschritt **Bereitschaft überprüfen** können Sie überprüfen, ob der Zielcomputer die angegebenen Bereitstellungsvoraussetzungen erfüllt.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt Wählen Sie diese Einstellung für diesen Schritt nicht aus, da der Schritt andernfalls lediglich die Bereitschaftsprüfungen protokolliert, die Tasksequenz bei einem Überprüfungsfehler aber nicht beendet wird.  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Mindestens erforderlicher Arbeitsspeicher (MB)**  
 Wählen Sie diese Einstellung, um zu überprüfen, ob der auf dem Zielcomputer installierte Arbeitsspeicher (in Megabytes) dem angegebenen Speicherplatz entspricht oder diesen übersteigt. Diese Einstellung ist standardmäßig aktiviert.  

 **Mindestens erforderliche Prozessorgeschwindigkeit (MHz)**  
 Wählen Sie diese Einstellung, um zu überprüfen, ob die Geschwindigkeit des im Zielcomputer installierten Prozessors in Megahertz (MHz) dem angegebenen Wert entspricht oder diesen übersteigt. Diese Einstellung ist standardmäßig aktiviert.  

 **Mindestens erforderlicher freier Speicherplatz (MB)**  
 Wählen Sie diese Einstellung aus, um zu überprüfen, ob der auf dem Zielcomputer freie Speicherplatz in Megabytes dem angegebenen Wert entspricht oder diesen übersteigt.  

 **Aktuelles Betriebssystem, das aktualisiert wird**  
 Wählen Sie diese Einstellung aus, um zu überprüfen, ob das auf dem Zielcomputer installierte Betriebssystem die angegebene Anforderung erfüllt. Standardmäßig ist diese Einstellung aktiviert und auf **CLIENT**festgelegt.  

##  <a name="BKMK_ConnectToNetworkFolder"></a> Verbindung mit Netzwerkordner herstellen  
 Verwenden Sie die Tasksequenzaktion **Verbindung mit Netzwerkordner herstellen** , um eine Verbindung mit einem freigegebenen Netzwerkordner herzustellen.  

 Dieser Tasksequenzschritt wird in einem Standardbetriebssystem oder in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Connect to Network Folder Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

##  <a name="BKMK_ConvertDisktoDynamic"></a> In dynamischen Datenträger konvertieren  
 Mit der Tasksequenz **In dynamischen Datenträger konvertieren** können Sie einen physischen Datenträger von einem Basisdatenträgertyp in einen dynamischen Datenträgertyp konvertieren.  

 Dieser Schritt wird entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Convert Disk to Dynamic Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConvertDisk).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Datenträgernummer**  
 Die Nummer des physischen Datenträgers, der konvertiert werden soll.  

##  <a name="BKMK_DisableBitLocker"></a> BitLocker deaktivieren  
 Mit dem Tasksequenzschritt **BitLocker deaktivieren** können Sie die BitLocker-Verschlüsselung auf dem aktuellen Betriebssystemlaufwerk oder einem bestimmten Laufwerk deaktivieren. Nach dieser Aktion sind die Schlüsselschutzkomponenten im Klartext auf der Festplatte sichtbar, die Inhalte des Laufwerks werden jedoch nicht entschlüsselt. Dieser Vorgang ist daher praktisch sofort beendet.  

> [!NOTE]  
>  BitLocker-Laufwerkverschlüsselung bietet eine niedrige Verschlüsselungsstufe der Inhalte eines Datenträgervolumes.  

 Wenn Sie über mehrere verschlüsselte Laufwerke verfügen, müssen Sie „BitLocker deaktivieren“ zuerst für alle Datenlaufwerke anwenden, bevor Sie die BitLocker-Verschlüsselung des Betriebssystemlaufwerks deaktivieren können.  

 Dieser Schritt wird nur in Standardbetriebssystemen ausgeführt. Er wird nicht in Windows PE ausgeführt.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Gibt einen kurzen benutzerdefinierten Namen an, der die in diesem Schritt vorgenommene Aktion beschreibt.  

 **Beschreibung**  
 Bietet ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Aktuelles Betriebssystemlaufwerk**  
 Deaktiviert BitLocker auf dem aktuellen Betriebssystemlaufwerk.  

 **Bestimmtes Laufwerk**  
 Deaktiviert BitLocker auf einem bestimmten Laufwerk. Geben Sie in der Dropdownliste das Laufwerk an, auf dem BitLocker deaktiviert ist.  

##  <a name="BKMK_DownloadPackageContent"></a> Paketinhalt herunterladen  
 Verwenden Sie den Tasksequenzschritt **Paketinhalt herunterladen** , um die folgenden Pakettypen herunterzuladen:  

-   Betriebssystemabbilder  

-   Betriebssystem-Upgradepakete  

-   Treiberpakete  

-   Pakete  

 Dieser Schritt funktioniert gut in einer Tasksequenz zum Aktualisieren eines Betriebssystems in den folgenden Szenarien:  

-   Zum Verwenden einer einzigen Upgradetasksequenz für x86- und x64-Plattformen. Um dies zu erreichen, fügen Sie zwei **Paketinhalt herunterladen** -Schritte zur Gruppe **Vorbereitung auf das Upgrade** hinzu, und geben Sie Bedingungen an, um die Clientarchitektur zu ermitteln und nur das entsprechende Betriebssystemupgradepaket herunterzuladen. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den Medienpfad im Schritt **Betriebssystem aktualisieren** .  

-   Um dynamisch ein passendes Treiberpaket herunterzuladen, verwenden Sie zwei **Paketinhalt herunterladen** -Schritte mit Bedingungen zum Ermitteln des geeigneten Hardwaretyps für jedes Treiberpaket. Konfigurieren Sie jeden **Paketinhalt herunterladen** -Schritt zur Verwendung derselben Variablen, und verwenden Sie die Variable für den **Bereitgestellter Inhalt** -Wert im Bereich „Treiber“ im Schritt **Betriebssystem aktualisieren** .  

> [!NOTE]    
> Wenn Sie eine Tasksequenz bereitstellen, die den Schritt „Paketinhalt herunterladen“ enthält, aktivieren Sie im Assistenten zum Bereitstellen von Software auf der Seite **Verteilungspunkte** für **Bereitstellungsoptionen** nicht **Alle Inhalte vor dem Start der Tasksequenz lokal herunterladen**.  

Dieser Schritt wird entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt. WinPE unterstützt die Option, die Pakete im Clientcache des Configuration Manager zu speichern, jedoch nicht.

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Gibt einen kurzen benutzerdefinierten Namen an, der die in diesem Schritt vorgenommene Aktion beschreibt.  

 **Beschreibung**  
 Bietet ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Paket auswählen** -Symbol  
 Klicken Sie auf das Symbol, um das Paket zum Herunterladen auszuwählen. Nachdem Sie ein Paket ausgewählt haben, können Sie erneut auf das Symbol klicken, um ein anderes Paket auszuwählen.  

 **In folgendem Verzeichnis speichern**  
 Sie können das Paket in einem der folgenden Verzeichnisse speichern:  

 -   **Tasksequenz-Arbeitsverzeichnis**  

 -   **Configuration Manager-Clientcache**: Sie verwenden diese Option, um den Inhalt im Clientcache zu speichern. Dadurch kann der Client als Peercachequelle für andere Peercacheclients fungieren. Weitere Informationen finden Sie unter [Vorbereiten des Windows PE-Peercache zum Reduzieren des WAN-Datenverkehrs](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -   **Benutzerdefinierter Pfad**  

 **Pfad als Variable speichern**  
 Sie können den Pfad als Variable speichern, die in einem anderen Tasksequenzschritt verwendet werden kann. Configuration Manager fügt dem Variablennamen ein numerisches Suffix hinzu. Wenn Sie beispielsweise eine Variable %*mycontent*% als eine benutzerdefinierte Variable angeben, ist dies das Stammverzeichnis, in dem alle referenzierten Inhalte gespeichert werden (dies können mehrere Pakete sein). Wenn Sie auf die Variable verweisen, fügen Sie der Variablen ein numerisches Suffix hinzu. Beispielsweise verweisen Sie für das erste Paket auf die Variable %*mycontent01*% Wenn Sie auf die Variable in einem Untersequenzschritt verweisen, z.B. „Betriebssystem aktualisieren“, verwenden Sie %*mycontent02*% oder %*mycontent03*%, wobei die Anzahl der Reihenfolge entspricht, in dem das Paket im Schritt aufgelistet wird.  

 **Wenn ein Fehler bei einem Paketdownload auftritt, mit anderen Paketen in der Liste fortfahren**  
 Gibt an, dass im Falle eines Fehlers beim Paketdownload zum nächsten Paket in der Liste gewechselt und der Download gestartet wird.  

##  <a name="BKMK_EnableBitLocker"></a> BitLocker aktivieren  
 Verwenden Sie den Tasksequenzschritt **BitLocker aktivieren** , um die BitLocker-Verschlüsselung auf mindestens zwei Partitionen auf der Festplatte zu aktivieren. Die erste aktive Partition enthält den Windows-Bootstrap-Code. Eine weitere Partition beinhaltet das Betriebssystem. Die Bootstrap-Partition muss unverschlüsselt bleiben.  

 Verwenden Sie den Tasksequenzschritt **BitLocker vorab bereitstellen** zum Aktivieren von BitLocker auf einem Laufwerk in Windows PE. Weitere Informationen finden Sie im Abschnitt [BitLocker vorab bereitstellen](#BKMK_PreProvisionBitLocker) in diesem Thema.  

> [!NOTE]  
>  BitLocker-Laufwerkverschlüsselung bietet eine niedrige Verschlüsselungsstufe der Inhalte eines Datenträgervolumes.  

 Der Schritt **BitLocker aktivieren** wird nur in Standardbetriebssystemen ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

 Das Trusted Platform Module (TPM) muss bei Angabe von **Nur TPM**, **TPM &amp; Schlüssel zum Systemstart auf USB** oder **TPM-und-PIN**den folgende Zustand aufweisen, bevor Sie den Schritt **BitLocker aktivieren** ausführen können:  

-   Aktiviert  

-   Aktiviert  

-   Besitz zulässig  

 Mit dem Tasksequenzschritt kann jegliche verbleibende TPM-Initialisierung abgeschlossen werden, da für die restlichen Schritte keine physische Präsenz und keine Neustarts erforderlich sind. Zu den verbleibenden TPM-Initialisierungsschritten, die bei Bedarf transparent über **BitLocker aktivieren** abgeschlossen werden können, gehören:  

-   Endorsement Key-Paar erstellen  

-   Besitzerauthentifizierungswert erstellen und in Active Directory hinterlegen, welches zur Unterstützung dieses Werts erweitert worden sein muss  

-   Besitz übernehmen  

-   Storage Root Key (SRK, Speicherstammschlüssel) erstellen bzw. zurücksetzen, falls bereits einer vorhanden ist, der jedoch inkompatibel ist  

 Wenn der Schritt **BitLocker aktivieren** verzögert werden soll, bis der Laufwerksverschlüsselungsvorgang abgeschlossen ist, bevor mit dem nächsten Schritt in der Tasksequenz fortgefahren wird, aktivieren Sie das Kontrollkästchen **Warten** . Wenn Sie das Kontrollkästchen **Warten** nicht aktivieren, wird die Laufwerksverschlüsselung im Hintergrund ausgeführt und in der Tasksequenzausführung sofort der nächste Schritt aufgerufen.  

 Mithilfe von BitLocker können mehrere Laufwerke in einem Computersystem (sowohl Betriebssystem- als auch Datenlaufwerke) verschlüsselt werden. Zur Verschlüsselung eines Datenlaufwerks muss das Betriebssystem bereits verschlüsselt und der Verschlüsselungsvorgang abgeschlossen sein, da die Schlüsselschutzvorrichtungen für Datenlaufwerke auf dem Betriebssystemlaufwerk gespeichert werden. Wenn Sie also das Betriebssystemlaufwerk und das Datenlaufwerk im Rahmen desselben Vorgangs verschlüsseln, muss für den Schritt, bei dem BitLocker für das Betriebssystemlaufwerk aktiviert wird, die Option „Warten“ aktiviert werden.  

 Wenn die Festplatte bereits verschlüsselt, BitLocker jedoch deaktiviert ist, werden durch „Bitlocker aktivieren“ die Schlüsselschutzvorrichtung(en) erneut aktiviert, und der Schritt wird nahezu umgehend abgeschlossen. Eine erneute Verschlüsselung des Laufwerks ist in diesem Fall nicht notwendig.  

 Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Gibt einen beschreibenden Namen für diesen Tasksequenzschritt an.  

 **Beschreibung**  
 Hiermit können Sie optional eine Beschreibung für diesen Tasksequenzschritt eingeben.  

 **Wählen Sie das zu verschlüsselnde Laufwerk aus**  
 Gibt das zu verschlüsselnde Laufwerk an. Um das aktuelle Betriebssystemlaufwerk zu verschlüsseln, wählen Sie **Aktuelles Betriebssystemlaufwerk** aus und konfigurieren anschließend eine der folgenden Optionen für die Schlüsselverwaltung.  

-   **Nur TPM**: Wählen Sie diese Option, um nur Trusted Platform Module (TPM) zu verwenden.  

-   **Nur Schlüssel zum Systemstart auf USB**: Wählen Sie diese Option, um einen auf einem USB-Flashlaufwerk gespeicherten Systemstartschlüssel zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis ein USB-Gerät mit einem BitLocker-Systemstartschlüssel an den Computer angeschlossen wird.  

-   **TPM &amp; Schlüssel zum Systemstart auf USB**: Wählen Sie diese Option, um TPM und einen auf einem USB-Flashlaufwerk gespeicherten Systemstartschlüssel zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis ein USB-Gerät mit einem BitLocker-Systemstartschlüssel an den Computer angeschlossen wird.  

-   **TPM-und-PIN**: Wählen Sie diese Option, um TPM und eine persönliche Identifikationsnummer (PIN) zu verwenden. Wenn Sie diese Option auswählen, sperrt BitLocker den normalen Startvorgang, bis der Benutzer die PIN eingibt.  

 Um ein bestimmtes Datenlaufwerk (kein Betriebssystemlaufwerk) zu verschlüsseln, wählen Sie **Bestimmtes Laufwerk**, und wählen Sie dann das Laufwerk in der Liste aus.  

 **Wählen Sie aus, wo der Wiederherstellungsschlüssel erstellt werden soll**  
 Wählen Sie **In Active Directory** aus, um anzugeben, wo das Wiederherstellungskennwort erstellt werden soll, und um das Kennwort in Active Directory zu hinterlegen. Wenn Sie diese Option auswählen, müssen Sie Active Directory für den Standort erweitern, sodass die zugeordneten BitLocker-Wiederherstellungsinformationen gespeichert werden. Sie können auch beschließen, gar kein Kennwort zu erstellen, indem Sie **Keinen Wiederherstellungsschlüssel erstellen**auswählen. Das Erstellen eines Kennworts ist jedoch eine bewährte Methode.  

 **Vor dem Fortsetzen der Tasksequenzausführung warten, bis BitLocker den Laufwerkverschlüsselungsvorgang auf allen Laufwerken abgeschlossen hat**  
 Wählen Sie diese Option aus, damit die BitLocker-Laufwerkverschlüsselung abgeschlossen wird, bevor der nächste Schritt in der Tasksequenz ausgeführt wird. Wenn diese Option ausgewählt ist, wird das gesamte Datenträgervolume verschlüsselt, bevor sich der Benutzer beim Computer anmelden kann.  

 Bei Verschlüsselung eines umfangreichen Festplattenlaufwerks kann es Stunden dauern, bevor der Verschlüsselungsvorgang abgeschlossen ist. Wenn diese Option nicht ausgewählt wird, kann die Tasksequenz sofort fortgesetzt werden.  

##  <a name="BKMK_FormatandPartitionDisk"></a> Datenträger formatieren und partitionieren  
 Mit dem Tasksequenzschritt **Datenträger formatieren und partitionieren** können Sie einen angegebenen Datenträger auf einem Zielcomputer formatieren und partitionieren.  

> [!IMPORTANT]  
>  Jede von Ihnen für diesen Tasksequenzschritt angegebene Einstellung gilt nur für einen angegebenen Datenträger. Wenn Sie einen anderen Datenträger auf dem Zielcomputer formatieren und partitionieren möchten, müssen Sie der Tasksequenz einen weiteren Tasksequenzschritt zum **Formatieren und Partitionieren des Datenträgers** hinzufügen.  

 Dieser Tasksequenzschritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Aktion finden Sie unter [Format and Partition Disk Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Datenträgernummer**  
 Die Nummer des physischen Datenträgers, der formatiert wird Die Nummer basiert auf der Reihenfolge der Datenträgerenumeration in Windows.  

 **Datenträgertyp**  
 Typ des Datenträgers, der formatiert wird In der Dropdownliste stehen zwei Optionen zur Auswahl zur Verfügung:  

-   Standard (MBR) – Master Boot Record.  

-   GPT – GUID-Partitionstabelle  

> [!NOTE]  
>  Wenn Sie den Datenträgertyp von **Standard (MBR)** in **GPT**ändern und das Partitionslayout eine erweiterte Partition enthält, werden alle erweiterten und logischen Partitionen aus dem Layout entfernt. Sie werden aufgefordert, diese Aktion vor dem Ändern des Datenträgertyps zu bestätigen.  

 **Volume**  
 Spezielle Informationen zur Partition oder dem Volume, die/das erstellt wird, einschließlich:  

-   Name  

-   Verbleibender Speicherplatz  

 Zum Erstellen einer neuen Partition klicken Sie auf **Neu** , um das Dialogfeld **Partitionseigenschaften** aufzurufen. Sie können den Typ und die Größe der Partition angeben. Außerdem können Sie angeben, ob es sich um eine Startpartition handeln soll. Zum Ändern einer vorhandenen Partition klicken Sie auf die zu ändernde Partition und dann auf die Schaltfläche „Eigenschaften“. Weitere Informationen zum Konfigurieren von Festplattenpartitionen finden Sie in einem der folgenden Themen:  

-   [Konfigurieren von UEFI-/GPT-basierten Festplattenpartitionen](http://go.microsoft.com/fwlink/?LinkID=272104)  

-   [Konfigurieren von BIOS-/MBR-basierten Festplattenpartitionen](http://go.microsoft.com/fwlink/?LinkId=272105)  

 Wählen Sie zum Löschen einer Partition die zu löschende Partition aus, und klicken Sie dann auf **Löschen**.  

##  <a name="BKMK_InstallApplication"></a> Anwendung installieren  
 Mit dem Tasksequenzschritt **Anwendung installieren** können Sie Anwendungen als Teil der Tasksequenz installieren. Mit diesem Schritt können Sie einen Satz von Anwendungen installieren, die vom Tasksequenzschritt angegeben werden, oder einen Satz von Anwendungen, die von einer dynamischen Liste mit Tasksequenzvariablen angegeben werden. Wenn dieser Schritt ausgeführt wird, beginnt die Anwendungsinstallation sofort; das nächste Richtlinienabfrageintervall wird nicht abgewartet.  

 Von Anwendungen, die installiert werden, müssen die folgenden Kriterien erfüllt werden:  

-   Die Anwendung muss ein Bereitstellungstyp von Windows Installer oder des Skriptinstallationsprogramms sein. Bereitstellungstypen des Windows-App-Pakets (APPX-Datei) werden nicht unterstützt.  

-   Es muss unter dem lokalen Systemkonto ausgeführt werden und nicht unter dem Benutzerkonto.  

-   Es darf keine Interaktion mit dem Desktop erfolgen. Das Programm muss im Hintergrund oder in einem unbeaufsichtigten Modus ausgeführt werden.  

-   Es darf durch die Anwendung kein eigenständiger Computerneustart initiiert werden. Ein Computerneustart muss über den Standardneustartcode (Exitcode 3010) angefordert werden. Dadurch wird sichergestellt, dass der Neustart ordnungsgemäß ausgeführt wird. Wenn ein Exitcode 3010 von der Anwendung zurückgegeben wird, so wird der Neustart vom zugrundeliegenden Tasksequenzmodul ausgeführt. Nach dem Neustart wird die Tasksequenz automatisch fortgesetzt.  

 Bei Ausführung des Schritts **Anwendung installieren** wird die Anwendbarkeit der Anforderungsregeln und der Ermittlungsmethode für die Bereitstellungstypen der Anwendung geprüft. Auf Basis der Ergebnisse dieser Überprüfung wird der anwendbare Bereitstellungstyp installiert. Wenn ein Bereitstellungstyp Abhängigkeiten enthält, wird der abhängige Bereitstellungstyp im Rahmen des Anwendungsinstallationsschritts ausgewertet und installiert. Abhängigkeiten von Anwendungen werden für eigenständige Medien nicht unterstützt.  

> [!NOTE]  
>  Zum Installieren einer Anwendung, die eine andere Anwendung ablöst, müssen die Inhaltsdateien für die abgelöste Anwendung verfügbar sein, andernfalls tritt beim Tasksequenzschritt ein Fehler auf. Beispiel: Microsoft Visio 2010 ist auf einem Client oder in einem erfassten Abbild installiert. Beim Ausführen des Tasksequenzschritts „Anwendung installieren“ zum Installieren von Microsoft Visio 2013 müssen die Inhaltsdateien für Microsoft Visio 2010 (die abgelöste Anwendung) an einem Verteilungspunkt verfügbar sein, andernfalls tritt bei der Tasksequenz ein Fehler auf. Auf einem Client oder erfassten Abbild ohne Microsoft Visio-Installation wird die Installation von Microsoft Visio 2013 durchgeführt, ohne nach den Microsoft Visio 2010-Inhaltsdateien zu suchen.  

> [!NOTE]
> Verwenden Sie die integrierten Variablen SMSTSMPListRequestTimeoutEnabled und SMSTSMPListRequestTimeout, um anzugeben, wie viele Millisekunden eine Tasksequenz nach dem erfolglosen Abrufen der Verwaltungspunktliste von Standortdiensten warten soll, bevor sie erneut versucht, eine Anwendung oder einen Softwareupdate zu installieren. Weitere Informationen finden Sie unter [Integrierte Tasksequenzvariablen](task-sequence-built-in-variables.md).

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Geben Sie an, dass Sie diesen Schritt wiederholen, wenn der Computer unerwartet neu gestartet wird. Sie können auch angeben, wie viele Wiederholungen nach einem Neustart erfolgen sollen.  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Folgende Anwendungen installieren**  
 Mit dieser Einstellung geben Sie die Anwendungen an, die in der Reihenfolge installiert werden, in der sie angegeben sind.  

 Deaktivierte Anwendungen und Anwendungen mit den folgenden Einstellungen werden von Configuration Manager herausgefiltert. Diese Anwendungen erscheinen nicht im Dialogfeld **Zu installierende Anwendung auswählen** .  

-   Nur wenn ein Benutzer angemeldet ist  

-   Mit Benutzerrechten ausführen  

 **Anwendungen entsprechend der dynamischen Variablenliste installieren**  
 Mit dieser Einstellung geben Sie den Basisnamen für einen Satz von Tasksequenzvariablen an, die für einen Sammlung oder einen Computer definiert sind. Von diesen Variablen werden die Anwendungen angegeben, die für die Sammlung bzw. den Computer installiert werden. Jeder Variablenname besteht aus einem allgemeinen Basisnamen sowie einem numerischen bei 01 beginnenden Suffix Der Wert jeder Variable darf nur den Namen der Anwendung und nichts anderes enthalten.  

 Bei Anwendungen, die mithilfe einer dynamischen Variablenliste installiert werden sollen, muss im Dialogfeld **Eigenschaften** der Anwendung auf der Registerkarte **Allgemein** die folgende Einstellung aktiviert sein: **Installation dieser Anwendung durch die Tasksequenzaktion „Anwendung installieren“ ohne Bereitstellung zulassen**  

> [!NOTE]  
>  Bei Bereitstellungen mit eigenständigen Medien können Sie Anwendungen nicht mithilfe einer dynamischen Variablenliste installieren.  

 Beispiel: Geben Sie folgende Variable an, um eine einzelne Anwendung mithilfe einer Tasksequenzvariablen namens AA01 zu installieren:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

 Bei der Installation von zwei Anwendungen sind folgende zusätzliche Variablen anzugeben:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

 Es ist von folgenden Bedingungen abhängig, welche Komponenten installiert werden:  

-   Der Variablenwert enthält noch andere bzw. keine anderen Informationen als den Namen der Anwendung. Diese Anwendung wird nicht installiert, und die Tasksequenz wird fortgesetzt.  

-   Wenn keine Variable mit dem angegebenen Basisnamen und dem Suffix „01“ gefunden wird, werden keine Anwendungen installiert. Wenn Sie auf der Registerkarte „Optionen“ des Tasksequenzschritts die Option **Bei Fehler fortsetzen** auswählen, wird die Tasksequenz bei einem Fehler der Anwendungsinstallation fortgesetzt. Wenn die Einstellung nicht ausgewählt ist, tritt ein Fehler in der Tasksequenz auf, und die verbleibenden Anwendungen werden nicht installiert.  

 **Wenn ein Fehler bei einer Anwendungsinstallation auftritt, mit anderen Anwendungen in der Liste fortfahren**  
 Mit dieser Einstellung geben Sie an, dass der Schritt fortgesetzt werden soll, wenn bei einer einzelnen Anwendungsinstallation ein Fehler auftritt. Wenn diese Einstellung angegeben ist, wird die Tasksequenz unabhängig davon, ob Installationsfehler zurückgegeben werden, fortgesetzt. Wenn diese Einstellung nicht angegeben ist und bei einer Installation ein Fehler auftritt, wird der Tasksequenzschritt sofort beendet.  

##  <a name="BKMK_InstallDeploymentTools"></a> Bereitstellungstools installieren  
 Verwenden Sie den Tasksequenzschritt **Bereitstellungstools installieren**, um das Configuration Manager-Paket zu installieren, das die Sysprep-Bereitstellungstools enthält.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Systemvorbereitungspaket**  
 Mit dieser Einstellung geben Sie das Configuration Manager-Paket an, das die Sysprep-Bereitstellungstools für die folgenden Betriebssysteme enthält:  

-   Windows XP SP3  

-   Windows XP X64 SP2  

-   Windows Server 2003 SP2  

##  <a name="BKMK_InstallPackage"></a> Paket installieren

 Mit dem Tasksequenzschritt **Paket installieren** können Sie Software als Teil der Tasksequenz installieren. Wenn dieser Schritt ausgeführt wird, beginnt die Installation sofort; das nächste Richtlinienabfrageintervall wird nicht abgewartet.  

 Von Software, die installiert wird, müssen die folgenden Kriterien erfüllt werden:  

-   Es muss unter dem lokalen Systemkonto ausgeführt werden und nicht unter dem Benutzerkonto.  

-   Es sollte nicht mit dem Desktop interagieren. Das Programm muss im Hintergrund oder in einem unbeaufsichtigten Modus ausgeführt werden.  

-   Es darf durch die Anwendung kein eigenständiger Computerneustart initiiert werden. Ein Computerneustart muss über den Standardneustartcode (Exitcode 3010) angefordert werden. Dadurch wird sichergestellt, dass der Tasksequenzschritt den Neustart ordnungsgemäß ausführt. Wenn ein Exitcode 3010 von der Software zurückgegeben wird, so wird der Neustart vom zugrundeliegenden Tasksequenzmodul ausgeführt. Nach dem Neustart wird die Tasksequenz automatisch fortgesetzt.  

 Programme, von denen die Option **Ein anderes Programm zuerst ausführen** zur Installation eines abhängigen Programms verwendet wird, werden bei der Bereitstellung eines Betriebssystems nicht unterstützt. Wenn die Option **Ein anderes Programm zuerst ausführen** für eine Software aktiviert ist und das abhängige Programm bereits auf dem Zielcomputer ausgeführt wurde, wird das abhängige Programm ausgeführt, und die Tasksequenz wird fortgesetzt. Wurde das abhängige Programm jedoch noch nicht auf dem Zielcomputer ausgeführt, tritt bei diesem Tasksequenzschritt ein Fehler auf.  

> [!NOTE]  
>  Der Standort der zentralen Verwaltung verfügt nicht über die erforderlichen Clientkonfigurationsrichtlinien, die während der Ausführung der Tasksequenz zum Aktivieren des Softwareverteilungs-Agents benötigt werden. Wenn Sie am Standort der zentralen Verwaltung eigenständige Medien für eine Tasksequenz erstellen und die Tasksequenz den Schritt **Paket installieren** enthält, kann in der Datei "CreateTsMedia.log" der folgende Fehler enthalten sein:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Sie müssen eigenständige Medien, die über den Schritt **Paket installieren** verfügen, an einem primären Standort erstellen, für den der Softwareverteilungs-Agent aktiviert ist. Alternativ dazu können Sie den Schritt **Befehlszeile ausführen** nach dem Schritt **Windows und ConfigMgr einrichten** und vor dem ersten Schritt "Paket installieren" hinzufügen. Im Schritt **Befehlszeile ausführen** wird ein WMIC-Befehl ausgeführt, um den Softwareverteilungs-Agent vor der Ausführung des ersten Schritts "Paket installieren" zu aktivieren. Sie können im Tasksequenzschritt **Befehlszeile ausführen** Folgendes verwenden:  
>   
>  **Command Line**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  
>   
>  Weitere Informationen zum Erstellen eigenständiger Medien finden Sie unter [Erstellen eigenständiger Medien](../deploy-use/create-stand-alone-media.md).  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Einzelnes Softwarepaket installieren**  
 Diese Einstellung gibt ein Configuration Manager-Softwarepaket an. Bei diesem Schritt wird gewartet, bis die Installation abgeschlossen ist.  

 **Softwarepakete entsprechend der dynamischen Variablenliste installieren**  
 Mit dieser Einstellung geben Sie den Basisnamen für einen Satz von Tasksequenzvariablen an, die für einen Sammlung oder einen Computer definiert sind. Von diesen Variablen werden die Pakete angegeben, die für die Sammlung bzw. den Computer installiert werden. Jeder Variablenname besteht aus einem allgemeinen Basisnamen sowie einem numerischen bei 001 beginnenden Suffix. Der Wert jeder Variablen muss eine Paket-ID und den Namen der Software (durch einen Doppelpunkt getrennt) enthalten.  

 Bei Software, die mithilfe einer dynamischen Variablenliste installiert werden soll, muss im Dialogfeld **Eigenschaften** des Pakets auf der Registerkarte **Erweitert** die folgende Einstellung aktiviert sein: **Installation dieses Programms aus der Tasksequenz „Paket installieren“ ohne Bereitstellung zulassen**  

> [!NOTE]  
>  Bei Bereitstellungen mit eigenständigen Medien können Sie Softwarepakete nicht mithilfe einer dynamischen Variablenliste installieren.  

 Beispiel: Geben Sie folgende Variable an, um ein einzelnes Softwarepaket mithilfe einer Tasksequenzvariablen namens AA001 zu installieren:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 Bei der Installation von drei Softwarepaketen sind folgende zusätzliche Variablen anzugeben:  

|Variablenname|Variablenwert|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 Es ist von folgenden Bedingungen abhängig, welche Komponenten installiert werden:  

-   Wenn der Wert einer Variablen nicht im richtigen Format erstellt wurde oder damit keine gültige Anwendungs-ID bzw. kein gültiger Anwendungsname angegeben wird, tritt bei der Installation der Software ein Fehler auf.  

-   Wenn die Paket-ID Kleinbuchstaben enthält, tritt bei der Installation der Software ein Fehler auf.  

-   Wenn keine Variablen mit dem angegebenen Basisnamen und dem Suffix „001“ gefunden werden, werden keine Pakete installiert, und die Tasksequenz wird fortgesetzt.  

 **Wenn ein Fehler bei einer Softwarepaketinstallation auftritt, mit anderen Paketen in der Liste fortfahren**  
 Mit dieser Einstellung geben Sie an, dass der Schritt fortgesetzt werden soll, wenn bei einer einzelnen Softwarepaketinstallation ein Fehler auftritt. Wenn diese Einstellung angegeben ist, wird die Tasksequenz unabhängig davon, ob Installationsfehler zurückgegeben werden, fortgesetzt. Wenn diese Einstellung nicht angegeben ist und bei einer Installation ein Fehler auftritt, wird der Tasksequenzschritt sofort beendet.  

##  <a name="BKMK_InstallSoftwareUpdates"></a> Softwareupdates installieren  
 Verwenden Sie den Tasksequenzschritt **Softwareupdates installieren** zum Installieren von Softwareupdates auf einem Zielcomputer. Der Zielcomputer wird erst beim Ausführen dieses Tasksequenzschritts hinsichtlich anwendbarer Softwareupdates ausgewertet. An diesem Punkt wird der Zielcomputer wie jeder andere von Configuration Manager verwaltete Client hinsichtlich Softwareupdates ausgewertet. Insbesondere werden mit diesem Schritt nur Softwareupdates installiert, die für Sammlungen bestimmt sind, in denen der Computer derzeit Mitglied ist.  
>  [!IMPORTANT]
>Es wird empfohlen, die neueste Version des Windows Update-Agents zu installieren, da die Leistung sich so deutlich verbessert, wenn Sie den Tasksequenzschritt „Softwareupdates installieren“ verwenden.
>* Für Windows 7 siehe [Knowledge Base-Artikel 3161647](https://support.microsoft.com/kb/3161647).
>* Für Windows 8 siehe [Knowledge Base-Artikel 3163023](https://support.microsoft.com/kb/3163023).

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Install Software Updates Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Verwenden Sie die integrierten Variablen SMSTSMPListRequestTimeoutEnabled und SMSTSMPListRequestTimeout, um anzugeben, wie viele Millisekunden eine Tasksequenz nach dem erfolglosen Abrufen der Verwaltungspunktliste von Standortdiensten warten soll, bevor sie erneut versucht, eine Anwendung oder einen Softwareupdate zu installieren. Weitere Informationen finden Sie unter [Task sequence built-in variables (Integrierte Tasksequenzvariablen)](task-sequence-built-in-variables.md).

> [!NOTE]
>Auf der Registerkarte „Optionen“ können Sie diese Tasksequenz so konfigurieren, dass eine Wiederholung erfolgt, wenn der Computer unerwartet neu gestartet wird. Beispiel: Die Installation eines Softwareupdates startet den Computer automatisch neu. Ab Configuration Manager 1602 können Sie die Variable SMSTSWaitForSecondReboot konfigurieren, um anzugeben, wie lang (in Sekunden) die Tasksequenz beim Installieren von Softwareupdates nach den Computerneustarts anhalten sollte. Weitere Informationen finden Sie unter [Integrierte Tasksequenzvariablen](task-sequence-built-in-variables.md).

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Geben Sie an, dass Sie diesen Schritt wiederholen, wenn der Computer unerwartet neu gestartet wird. Sie können auch angeben, wie viele Wiederholungen nach einem Neustart erfolgen sollen.  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Installation erforderlich – Nur obligatorische Softwareupdates**  
 Wählen Sie diese Option aus, um alle Softwareupdates zu installieren, die in Configuration Manager als obligatorisch für die Tasksequenz empfangende Zielcomputer gekennzeichnet sind. Obligatorische Softwareupdates verfügen über vom Administrator definierte Installationsstichtage.  

 **Bereit zur Installation – Alle Softwareupdates**  
 Wählen Sie diese Option aus, um alle Softwareupdates zu installieren, die für die Configuration Manager-Sammlung bestimmt sind, der die Tasksequenz zugewiesen wird. Alle verfügbaren Softwareupdates werden auf den Zielcomputern installiert.  

 **Softwareupdates anhand von zwischengespeicherten Überprüfungsergebnissen auswerten**  
Ab der Configuration Manager-Version 1606 steht Ihnen die Option zur Verfügung, eine vollständige Überprüfung für Softwareupdates durchzuführen statt die zwischengespeicherten Überprüfungsergebnisse zu verwenden. Standardmäßig verwendet die Tasksequenz zwischengespeicherte Ergebnisse. Sie können das Kontrollkästchen deaktivieren, damit der Client eine Verbindung mit dem Softwareupdatepunkt herstellen kann, um den neuesten Softwareupdatekatalog zu verarbeiten und herunterzuladen. Diese Option eignet sich, wenn Sie eine Tasksequenz zum [Erfassen und Erstellen eines Betriebssystemabbilds](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md) verwenden, und wissen, dass eine große Anzahl Softwareupdates notwendig sein wird und dass viele davon Abhängigkeiten aufweisen (X muss installiert sein, damit Y zur Verfügung steht). Wenn Sie diese Einstellung deaktivieren und die Tasksequenz für eine große Anzahl von Clients bereitstellen, werden alle zur selben Zeit eine Verbindung mit dem Softwareupdatepunkt herstellen. Dies kann während des Prozesses und dem Download des Katalogs zu Leistungsproblemen führen. Wir empfehlen in den meisten Fällen, die Standardeinstellung zu verwenden.

Es wurde eine neue Tasksequenzvariable, SMSTSSoftwareUpdateScanTimeout, in Configuration Manager-Version 1606 eingeführt. Sie ermöglicht Ihnen, das Timeout für die Softwareupdateprüfung während des Tasksequenzschritts „Softwareupdates installieren“ zu kontrollieren. Der Standardwert beträgt 30 Minuten. Weitere Informationen finden Sie unter [Task sequence built-in variables (Integrierte Tasksequenzvariablen)](task-sequence-built-in-variables.md).


##  <a name="BKMK_JoinDomainorWorkgroup"></a> Einer Domäne oder Arbeitsgruppe beitreten  
 Mithilfe des Tasksequenzschritts **Einer Domäne oder Arbeitsgruppe beitreten** können Sie den Zielcomputer einer Arbeitsgruppe oder Domäne hinzufügen.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Join Domain or Workgroup Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Einer Arbeitsgruppe beitreten**  
 Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Arbeitsgruppe hinzuzufügen. Wenn der Computer derzeit Mitglied einer Domäne ist, wird er durch Auswählen dieser Option neu gestartet.  

 **Einer Domäne beitreten**  
 Wählen Sie diese Option aus, um den Zielcomputer einer angegebenen Domäne hinzuzufügen.  

 Sie können optional eine Organisationseinheit (OU), der der Computer beitreten soll, eingeben oder in der angegebenen Domäne danach suchen. Wenn der Computer derzeit Mitglied einer anderen Domäne oder Arbeitsgruppe ist, wird er dadurch neu gestartet. Wenn der Computer bereits Mitglied einer anderen Organisationseinheit ist, lässt Active Directory-Domänendienste das Ändern der Organisationseinheit nicht zu, und die Einstellung wird ignoriert.  

 **Geben Sie das Konto ein, das zum Beitreten zur Domäne berechtigt ist**  
 Klicken Sie auf **Festlegen** , um ein Konto (und Kennwort) mit der Berechtigungen für den Domänenbeitritt einzugeben. Das Konto muss im folgenden Format eingegeben werden  

 *Domäne\Konto*  

## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> ConfigMgr-Client für Erfassung vorbereiten  
Mithilfe des Tasksequenzschritts **ConfigMgr-Client für Erfassung vorbereiten** können Sie den Configuration Manager-Client vom Referenzcomputer entfernen oder konfigurieren, um ihn im Rahmen des Imageerstellungsprozesses für die Erfassung vorzubereiten.

Ab Version 1610 von Configuration Manager wird der Configuration Manager-Client im Schritt „Configuration Manager-Client vorbereiten“ vollständig entfernt, und es werden nicht nur die wichtigen Informationen entfernt. Wenn die Tasksequenz das erfasste Betriebssystemimage bereitstellt, wird jedes Mal ein neuer Configuration Manager-Client installiert.  

Vor der Configuration Manager-Version 1610 werden bei diesem Schritt folgende Aufgaben ausgeführt:  

-   Entfernt den Abschnitt mit den Clientkonfigurationseigenschaften aus der Datei „smscfg.ini“ im Windows-Verzeichnis. Diese Eigenschaften umfassen clientspezifische Informationen, darunter die Configuration Manager-GUID und andere Clientbezeichner.  

-   Löscht alle SMS- oder Configuration Manager-Computerzertifikate  

-   Löscht den Configuration Manager-Clientcache  

-   Löscht die zugewiesene Standortvariable für den Configuration Manager-Client  

-   Löscht alle lokalen Configuration Manager-Richtlinien  

-   Entfernt den vertrauenswürdigen Stammschlüssel für den Configuration Manager-Client  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

##  <a name="BKMK_PrepareWindowsforCapture"></a> Windows für die Erfassung vorbereiten  
 Mithilfe des Tasksequenzschritts **Windows für die Erfassung vorbereiten** können Sie die Sysprep-Optionen angeben, die beim Erfassen eines Betriebssystemabbilds auf dem Referenzcomputer verwendet werden. Mit dieser Tasksequenzaktion wird Sysprep ausgeführt. Der Computer wird anschließend über das für die Tasksequenz angegebene Windows PE-Startabbild neu gestartet. Damit diese Aktion erfolgreich abgeschlossen werden kann, darf der Referenzcomputer keiner Domäne angehören.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Prepare Windows for Capture Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Automatisch Liste der Massenspeichertreiber erstellen**  
 Wählen Sie diese Option aus, damit Sysprep automatisch eine Liste der Massenspeichertreiber vom Referenzcomputer erstellt. Mit dieser Option wird die Option „Build Mass Storage Drivers“ (Massenspeichertreiber erstellen) in der Datei Sysprep.inf auf dem Referenzcomputer aktiviert. Weitere Informationen zu dieser Option finden Sie in der Sysprep-Dokumentation.  

 **Aktivierungskennzeichnung nicht zurücksetzen**  
 Wählen Sie diese Option aus, damit Sysprep das Produktaktivierungsflag nicht zurücksetzt.  

##  <a name="BKMK_PreProvisionBitLocker"></a> BitLocker vorab bereitstellen  
 Verwenden Sie den Tasksequenzschritt **BitLocker vorab bereitstellen** zum Aktivieren von BitLocker auf einem Laufwerk in Windows PE. Es wird nur der auf dem Laufwerk verwendete Speicherplatz verschlüsselt, sodass die Verschlüsselungszeit erheblich verkürzt wird. Sie wenden die Schlüsselverwaltungsoptionen an, indem Sie den Tasksequenzschritt [Aktivieren von BitLocker](#BKMK_EnableBitLocker) nach der Betriebssysteminstallation ausführen. Dieser Schritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt.  

> [!IMPORTANT]  
>  Um BitLocker vorab bereitzustellen, müssen Sie Windows 7 oder höher als Betriebssystem bereitstellen, und TPM muss unterstützt werden und auf dem Computer aktiviert sein.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Geben Sie einen kurzen benutzerdefinierten Namen an, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Geben Sie ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion an.  

 **BitLocker auf das angegebene Laufwerk anwenden**  
 Geben Sie das Laufwerk aus, für das Sie BitLocker aktivieren möchten. Nur der verwendete Speicherplatz auf dem Laufwerk wird verschlüsselt.  

 **Diesen Schritt bei Computern überspringen, die nicht über ein TPM verfügen oder bei denen das TPM nicht aktiviert ist**  
 Wählen Sie diese Option, um die Laufwerkverschlüsselung zu überspringen, wenn die Computerhardware TPM nicht unterstützt oder TPM nicht aktiviert ist. Sie können diese Option beispielsweise verwenden, wenn Sie ein Betriebssystem für einen virtuellen Computer bereitstellen.  

##  <a name="BKMK_ReleaseStateStore"></a> Zustandsspeicher freigeben  
 Mithilfe des Tasksequenzschritts **Zustandsspeicher freigeben** können Sie den Zustandsmigrationspunkt darüber benachrichtigen, dass die Erfassungs- oder Wiederherstellungsaktion abgeschlossen ist. Dieser Schritt wird zusammen mit den Tasksequenzschritten **Zustandsspeicher anfordern**, **Benutzerzustand erfassen**und **Benutzerzustand wiederherstellen** verwendet, um Benutzerzustandsdaten mithilfe von USMT und eines Zustandsmigrationspunkts zu migrieren.  

 Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

 Wenn Sie im Tasksequenzschritt **Zustandsspeicher anfordern**  zum Erfassen des Benutzerzustands den Zugriff auf einen Zustandsmigrationspunkt angefordert haben, wird der Zustandsmigrationspunkt darüber benachrichtigt, dass der Erfassungsvorgang abgeschlossen ist und die Benutzerzustandsdaten zur Wiederherstellung zur Verfügung stehen. Der Zustandsmigrationspunkt legt die Zugriffssteuerungsberechtigungen für den erfassten Zustand so fest, dass nur der wiederherstellende Computer den (schreibgeschützten) Zugriff erhält.  

 Wenn Sie im Tasksequenzschritt **Zustandsspeicher anfordern** zum Wiederherstellen des Benutzerzustands den Zugriff auf einen Zustandsmigrationspunkt angefordert haben, erhält der Zustandsmigrationspunkt vom Tasksequenzschritt eine Meldung, dass der Wiederherstellungsvorgang abgeschlossen ist. Zu diesem Zeitpunkt werden die von Ihnen konfigurierten Beibehaltungseinstellungen für den Zustandsmigrationspunkt aktiviert.  

> [!IMPORTANT]  
>  Eine bewährte Methode besteht darin, die Option **Bei Fehler fortsetzen** für alle Tasksequenzschritte zwischen den Schritten **Zustandsspeicher anfordern** und **Zustandsspeicher freigeben** festzulegen, damit jede Tasksequenzaktion des Typs **Zustandsspeicher anfordern** über eine entsprechende Tasksequenzaktion des Typs **Zustandsspeicher freigeben** verfügt.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Release State Store Sequence Action Variables](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

##  <a name="BKMK_RequestStateStore"></a> Zustandsspeicher anfordern  
 Fordern Sie mit dem Tasksequenzschritt **Zustandsspeicher anfordern** beim Erfassen oder Wiederherstellen eines Computerzustands Zugriff auf einen Zustandsmigrationspunkt an.  

 Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

 Sie können den Tasksequenzschritt **Zustandsspeicher anfordern** zusammen mit den Tasksequenzschritten **Zustandsspeicher freigeben**, **Benutzerzustand erfassen**und **Benutzerzustand wiederherstellen** verwenden, um den Computerzustand mithilfe von Windows-EasyTransfer bzw. USMT und eines Zustandsmigrationspunkts zu migrieren.  

> [!NOTE]  
>  Wenn Sie gerade eine neue Standortrolle für den Zustandsmigrationspunkt (State Migration Point, SMP) erstellt haben, kann es bis zu einer Stunde dauern, bis er für den Benutzerzustandsspeicher verfügbar ist. Um die Verfügbarkeit des SMP zu beschleunigen, können Sie alle SMP-Eigenschaftseinstellungen so anpassen, dass die Aktualisierung der Standortsteuerungsdatei ausgelöst wird.  

 Dieser Tasksequenzschritt wird in einem Standardbetriebssystem und in Windows PE für Offline-USMT ausgeführt. Weitere Informationen zu den Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Request State Store Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RequestState).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Zustand des Computers erfassen**  
 Ermittelt einen Zustandsmigrationspunkt, der die in den Einstellungen für den Zustandsmigrationspunkt konfigurierten Mindestanforderungen erfüllt (maximale Anzahl von Clients und Mindestgröße des freien Speicherplatzes). Eine Gewährleistung, dass zum Zeitpunkt der Zustandsmigration genügend Speicherplatz zur Verfügung steht, wird mit dieser Option jedoch nicht gegeben. Durch Auswählen dieser Option wird Zugriff auf den Zustandsmigrationspunkt angefordert, um den Benutzerzustand und die Einstellungen eines Computers zu erfassen.  

 Wenn am Configuration Manager-Standort mehrere Zustandsmigrationspunkte aktiviert sind, wird mit diesem Tasksequenzschritt nach einem Zustandsmigrationspunkt mit verfügbarem Speicherplatz gesucht. Zu diesem Zweck wird der Verwaltungspunkt des Standorts nach einer Liste von Zustandsmigrationspunkten abgefragt. Anschließend werden die einzelnen Punkte bewertet, bis ein Punkt gefunden wird, der die Mindestanforderungen erfüllt.  

 **Zustand von anderem Computer wiederherstellen**  
 Wählen Sie diese Option, um Zugriff auf einen Zustandsmigrationspunkt anzufordern, um einen zuvor erfassten Benutzerzustand und Einstellungen auf einem Bereitstellungszielcomputer wiederherzustellen.  

 Wenn der Configuration Manager-Standort über mehrere Zustandsmigrationspunkte verfügt, wird mit diesem Tasksequenzschritt der Zustandsmigrationspunkt mit dem Computerzustand gesucht, der für den Bereitstellungszielcomputer gespeichert wurde.  

 **Anzahl von Wiederholungen**  
 Die Anzahl der Versuche, die von diesem Tasksequenzschritt unternommen werden, um einen entsprechenden Zustandsmigrationspunkt zu suchen, bevor der Vorgang abgebrochen wird  

 **Wiederholungsverzögerung (in Sekunden)**  
 Hiermit wird die Anzahl der Sekunden angegeben, die vom Tasksequenzschritt zwischen Wiederholversuchen gewartet wird.  

 **Das Netzwerkzugriffskonto verwenden, falls das Computerkonto keine Verbindung mit dem Zustandsspeicher herstellen kann.**  
 Gibt an, dass mithilfe der Anmeldeinformationen des Configuration Manager-Netzwerkzugriffskontos eine Verbindung zum Zustandsmigrationspunkt hergestellt wird, wenn der Configuration Manager-Client nicht über das Computerkonto auf den SMP-Zustandsspeicher zugreifen kann. Diese Option ist weniger sicher, da von anderen Computern mithilfe des Netzwerkzugriffskontos auf Ihren gespeicherten Zustand zugegriffen werden könnte. Wenn der Zielcomputer noch keiner Domäne angehört, ist diese Option jedoch möglicherweise erforderlich.  

##  <a name="BKMK_RestartComputer"></a> Computer neu starten  
 Verwenden Sie den Tasksequenzschritt **Computer neu starten** , um den Computer, auf dem die Tasksequenz ausgeführt wird, neu zu starten. Nach dem Neustart wird automatisch der nächste Schritt der Tasksequenz verarbeitet.  

 Dieser Schritt kann entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Weitere Informationen zu den Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Variablen der Tasksequenzaktion „Computer neu starten“](task-sequence-action-variables.md#BKMK_RestartComputer).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Der Tasksequenz zugewiesenes Startimage**  
 Wenn Sie diese Option auswählen, wird das der Tasksequenz zugewiesene Startabbild vom Zielcomputer verwendet. Das Startabbild wird zur Ausführung nachfolgender Tasksequenzschritte verwendet, die in Windows PE ausgeführt werden müssen.  

 **Aktuell installiertes Standardbetriebssystem**  
 Wenn Sie diese Option auswählen, wird der Zielcomputer mit dem installierten Betriebssystem neu gestartet.  

 **Benutzer vor dem Neustart benachrichtigen**  
 Wenn Sie diese Option auswählen, wird dem Benutzer eine Benachrichtigung angezeigt, dass der Zielcomputer neu gestartet wird. Diese Option ist standardmäßig ausgewählt.  

 **Benachrichtigungsmeldung**  
 Geben Sie eine Benachrichtigungsmeldung ein, die dem Benutzer vor einem Neustart des Zielcomputers angezeigt wird.  

 **Timeout der Meldungsanzeige**  
 Geben Sie den Zeitraum in Sekunden an, der einem Benutzer bis zum Neustart des Zielcomputers verbleibt. Der Standardzeitraum beträgt sechzig (60) Sekunden.  

##  <a name="BKMK_RestoreUserState"></a> Benutzerzustand wiederherstellen  
 Mithilfe des Tasksequenzschritts **Benutzerzustand wiederherstellen** können Sie Windows-EasyTransfer (früher USMT) initiieren, um den Benutzerzustand und die Benutzereinstellungen auf einem Zielcomputer wiederzuherstellen. Dieser Tasksequenzschritt wird in Verbindung mit dem Tasksequenzschritt **Benutzerzustand erfassen** verwendet.  

 Weitere Informationen zum Verwalten des Benutzerzustands beim Bereitstellen von Betriebssystemen finden Sie unter [Verwalten des Benutzerzustands](../get-started/manage-user-state.md).  

 Sie können auch den Tasksequenzschritt **Benutzerzustand wiederherstellen** zusammen mit den Tasksequenzschritten **Zustandsspeicher anfordern** und **Zustandsspeicher freigeben** verwenden, wenn Sie die Zustandseinstellungen in einem Zustandsmigrationspunkt am -Standort speichern oder von dort aus wiederherstellen möchten. In USMT 3.0 und höher wird der USMT-Zustandsspeicher mit dieser Option stets mit einem von Configuration Manager generierten und verwalteten Verschlüsselungsschlüssel entschlüsselt.  

 Mit dem Tasksequenzschritt **Benutzerzustand wiederherstellen** kann eine begrenzte Teilmenge der am häufigsten verwendeten USMT-Optionen gesteuert werden. Zusätzliche Befehlszeilenoptionen können mithilfe der Tasksequenzvariablen „OSDMigrateAdditionalRestoreOptions“ angegeben werden.  

> [!IMPORTANT]  
>  Wenn Sie den Tasksequenzschritt **Benutzerzustand wiederherstellen** für eine Aufgabe verwenden, die nicht im Zusammenhang mit einem Szenario der Betriebssystembereitstellung steht, fügen Sie den Tasksequenzschritt [Computer neu starten](#BKMK_RestartComputer) unmittelbar nach dem Tasksequenzschritt **Benutzerzustand wiederherstellen** hinzu.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt. Weitere Informationen zu den Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Restore User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RestoreUserState).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Gibt einen kurzen benutzerdefinierten Namen an, der die in diesem Schritt vorgenommene Aktion beschreibt.  

 **Beschreibung**  
 Gibt ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion an.  

 **USMT-Paket (Migrationsprogramm für den Benutzerzustand)**  
 Geben Sie das Configuration Manager-Paket ein, das die von diesem Schritt beim Wiederherstellen des Benutzerzustands und der Benutzereinstellungen zu verwendende USMT-Version enthält. Für dieses Paket ist kein Programm erforderlich. Beim Ausführen des Tasksequenzschritts wird die USMT-Version im angegebenen Paket ausgeführt. Geben Sie je nach Architektur des Betriebssystems, auf dem Sie den Zustand wiederherstellen, ein Paket an, das die 32-Bit-Version oder die x64-Version von Windows-EasyTransfer bzw. USMT enthält.  

 **Alle erfassten Benutzerprofile mit Standardoptionen wiederherstellen**  
 Stellt die erfassten Benutzerprofile mit den Standardoptionen wieder her. Zum Anpassen der wiederherzustellenden Optionen wählen Sie **Erfassung der Benutzerprofile anpassen**aus.  

 **Wiederherstellung von Benutzerprofilen anpassen**  
 Ermöglicht Ihnen die Anpassung der Dateien, die Sie auf dem Zielcomputer wiederherstellen möchten. Klicken Sie auf **Dateien** , um im USMT-Paket die Konfigurationsdateien anzugeben, die Sie für die Wiederherstellung der Benutzerprofile verwenden möchten. Zum Hinzufügen einer Konfigurationsdatei geben Sie einen Namen im Feld **Dateiname** an, und klicken Sie dann auf **Hinzufügen**. Die Konfigurationsdateien, die für den Vorgang verwendet werden, werden im Bereich „Dateien“ angezeigt. Die von Ihnen angegebene XML-Datei legt fest, welche Benutzerdatei wiederhergestellt wird.  

 **Lokale Computerbenutzerprofile wiederherstellen**  
 Stellt die lokalen Computerbenutzerprofile (d. h. Nicht-Domänenbenutzer) wieder her. Sie müssen den wiederhergestellten lokalen Benutzerkonten neue Kennwörter zuweisen, da die Kennwörter der ursprünglichen lokalen Benutzerkonten nicht migriert werden können. Geben Sie das Kennwort im Feld **Kennwort** ein, und bestätigen Sie es im Feld **Kennwort bestätigen** .  

 **Fortsetzen, wenn einige Dateien nicht wiederhergestellt werden können**  
 Setzt die Wiederherstellung des Benutzerzustands und der Benutzereinstellungen auch dann fort, wenn einige Dateien nicht wiederhergestellt werden können. Diese Option ist standardmäßig aktiviert. Wenn Sie diese Option aktivieren und beim Wiederherstellen von Dateien Fehler auftreten, wird der Tasksequenzschritt sofort mit einem Fehler beendet, sodass nicht alle Dateien wiederhergestellt werden.  

 **Ausführliche Protokollierung aktivieren**  
 Aktivieren Sie diese Option, um ausführlichere Protokolldateiinformationen zu generieren. Beim Wiederherstellen des Zustands wird das Protokoll „Loadstate.log“ generiert und standardmäßig im Tasksequenzprotokoll im Ordner „\windows\system32\ccm\Logs “ gespeichert.  

##  <a name="BKMK_RunCommandLine"></a> Befehlszeile ausführen  
 Mit dem Tasksequenzschritt **Befehlszeile ausführen** können Sie eine angegebene Befehlszeile ausführen.  

 Dieser Schritt kann in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Run Command Line Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RunCommand).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Gibt einen kurzen, benutzerdefinierten Namen an, der die auszuführende Befehlszeile beschreibt.  

 **Beschreibung**  
 Gibt ausführlichere Informationen zur ausgeführten Befehlszeile an.  

 **Befehlszeile**  
 Gibt die ausgeführte Befehlszeile an. Dieses Feld ist erforderlich. Die Verwendung von Dateinamenerweiterungen, wie .vbs und .exe, ist eine bewährte Methode. Sie sollten alle erforderlichen Einstellungsdateien, Befehlszeilenoptionen oder -parameter einschließen.  

 Wenn der Dateiname ohne Dateinamenerweiterung angegeben ist, versucht Configuration Manager, die Erweiterung .com, .exe oder .bat zu verwenden. Enthält der Dateiname eine Erweiterung, die keiner ausführbaren Datei zugeordnet ist, versucht Configuration Manager eine lokale Zuordnung anzuwenden. Lautet die Befehlszeile z.B. „readme.gif“, startet Configuration Manager die Anwendung, die auf dem Zielcomputer zum Öffnen von GIF-Dateien angegeben ist.  

 Beispiele:  

 **setup.exe /a**  

 **cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat**  

> [!NOTE]  
>  Befehlszeilenaktionen, wie Umleitung, Piping oder Kopieren, muss, wie im obigen Beispiel gezeigt, der Befehl **cmd.exe /c** vorangestellt werden, damit sie erfolgreich ausgeführt werden können.  

 **64-Bit-Dateisystemumleitung deaktivieren**  
 Unter einem 64-Bit-Betriebssystem wird die ausführbare Datei in der Befehlszeile standardmäßig gesucht und mithilfe des Dateisystem-Redirectors von WOW64 ausgeführt, sodass die 32-Bit-Versionen der ausführbaren Betriebssystemdateien und DLLs gefunden werden.  Wenn Sie diese deaktivieren, wird die Verwendung des Dateisystem-Redirectors von WOW64 deaktiviert, sodass die systemeigenen 64-Bit-Versionen der ausführbaren Betriebssystemdateien und DLLs gefunden werden können.  Unter einem 32-Bit-Betriebssystem hat das Auswählen dieser Option keine Auswirkungen.  

 **Starten in**  
 Gibt den ausführbaren Ordner für das Programm mit bis zu 127 Zeichen an. Für diesen Ordner kann ein absoluter Pfad auf dem Zielcomputer oder ein relativer Pfad zum Verteilungspunktordner mit dem Paket angegeben werden. Dieses Feld ist optional.  

 Beispiele:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  Mithilfe der Schaltfläche **Durchsuchen** werden Dateien und Ordner auf dem lokalen Computer gesucht und ausgewählt, was bedeutet, dass sich alles, was Sie auf diese Weise auswählen, auch auf dem Zielcomputer an dem gleichen Speicherort befinden und den gleichen Datei- und Ordnernamen aufweisen muss.  

 **Paket**  
 Wenn Sie Dateien oder Programme in der Befehlszeile angeben, die sich nicht bereits auf dem Zielcomputer befinden, wählen Sie diese Option aus, um das Configuration Manager-Paket anzugeben, das die entsprechenden Dateien enthält. Für das Paket ist kein Programm erforderlich. Diese Option ist nicht erforderlich, wenn die angegebenen Dateien auf dem Zielcomputer vorhanden sind.  

 **Timeout**  
 Dieser Wert legt fest, wie lange Configuration Manager das Ausführen einer Befehlszeile zulässt. Dieser Wert kann aus dem Bereich von 1 bis 999 Minuten stammen. Der Standardwert beträgt 15 Minuten.  

 Diese Option ist standardmäßig deaktiviert.  

> [!IMPORTANT]  
>  Wenn Sie einen Wert festlegen, der dem Tasksequenzschritt „Befehlszeile ausführen“ nicht genug Zeit gewährt, um erfolgreich abgeschlossen zu werden, kann der Tasksequenzschritt nicht ausgeführt werden, was je nach Steuerungseinstellung möglicherweise die gesamte Tasksequenz fehlschlagen lässt. Wenn das Timeout abläuft, beendet Configuration Manager den Befehlszeilenprozess.  

 **Diesen Schritt mit folgendem Konto ausführen**  
 Hiermit wird angegeben, dass die Befehlszeile unter einem anderen Windows-Benutzerkonto als dem lokalen Systemkonto ausgeführt wird.  

> [!NOTE]  
>  Wenn Sie ein anderes Konto für diesen Schritt angeben, und dies nach einem Betriebssystem-Installationsschritt vorkommt, muss das Konto auf dem Computer hinzugefügt werden, bevor Sie einfache Skripts oder Befehle ausführen können, und das Profil für das Windows-Benutzerkonto muss für komplexere Programme, z. B. einen MSI, wiederhergestellt werden.  

 **Konto**  
 Gibt das Windows-Konto „Ausführen als“ für den Befehlszeilentask in der von dieser Aktion auszuführenden Tasksequenz an. Die Befehlszeile wird mit den Berechtigungen des angegebenen Kontos ausgeführt. Klicken Sie auf **Festlegen** , um das lokale Benutzer- oder Domänenkonto anzugeben.  

> [!IMPORTANT]  
>  Wenn mit der Tasksequenzaktion **Befehlszeile ausführen** ein Benutzerkonto angegeben wird, schlägt diese Aktion beim Ausführen in Windows PE fehl, da Windows PE nicht mit einer Domäne verknüpft werden kann. Der Fehler wird in der Datei „smsts.log“ aufgezeichnet.  

##  <a name="BKMK_RunPowerShellScript"></a> PowerShell-Skript ausführen  
 Verwenden Sie den Tasksequenzschritt **PowerShell-Skript ausführen** zum Ausführen eines angegebenen PowerShell-Skripts.  

 Dieser Schritt kann in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Um diesen Schritt in Windows PE auszuführen, muss PowerShell im Startabbild aktiviert sein. Sie können Windows PowerShell (WinPE-PowerShell) auf der Registerkarte **Optionale Komponenten** in den Eigenschaften des Startabbilds aktivieren. Weitere Informationen dazu, wie ein Startimage geändert wird, finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  PowerShell ist unter Windows Embedded-Betriebssystemen nicht standardmäßig aktiviert.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Gibt einen kurzen, benutzerdefinierten Namen an, der die auszuführende Befehlszeile beschreibt.  

 **Beschreibung**  
 Gibt ausführlichere Informationen zur ausgeführten Befehlszeile an.  

 **Paket**  
 Gibt das Configuration Manager-Paket mit dem PowerShell-Skript an. Ein Paket kann mehrere PowerShell-Skripts enthalten.  

 **Skriptname**  
 Gibt den Namen des auszuführenden PowerShell-Skripts an. Dieses Feld ist erforderlich.  

 **Parameter**  
 Gibt die an das Windows PowerShell-Skript zu übergebenden Parameter an. Konfigurieren Sie die Parameter wie beim Hinzufügen zum Windows PowerShell-Skript über die Befehlszeile.  

> [!IMPORTANT]  
>  Geben Sie die Parameter an, die vom Skript verwendet werden, nicht die für die Windows PowerShell-Befehlszeile.  
>   
>  Das folgende Beispiel enthält gültige Parameter:  
>   
>  **-MyParameter1 MyValue1 -MyParameter2 MyValue2**  
>   
>  Das folgende Beispiel enthält ungültige Parameter. Die fett formatierten Elemente sind Windows PowerShell-Befehlszeilenparameter (-nologo und -executionpolicy unrestricted) und werden vom Skript nicht verwendet.  
>   
>  **-nologo-executionpolicy unrestricted-File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2**  

 **PowerShell-Ausführungsrichtlinie**  
 Durch Auswahl der PowerShell-Ausführungsrichtlinie können Sie bestimmen, welche Windows PowerShell-Skripts (sofern vorhanden) auf dem Computer ausgeführt werden dürfen. Wählen Sie eine der folgenden Ausführungsrichtlinien aus:  

-   **Alle signiert**: Nur Skripts, die von einem vertrauenswürdigen Herausgeber signiert wurden, dürfen ausgeführt werden.  

-   **Undefiniert**: Es ist keine Ausführungsrichtlinie definiert. .  

-   **Umgehung**: Lädt alle Konfigurationsdateien und führt alle Skripts aus. Wenn Sie ein unsigniertes Skript ausführen, das aus dem Internet heruntergeladen wurde, werden Sie nicht zur Bestätigung aufgefordert, bevor es ausgeführt wird.  

> [!IMPORTANT]  
>  Die Ausführungsrichtlinien „Undefiniert“ und „Umgehung“ werden von PowerShell 1.0 nicht unterstützt.  

##  <a name="BKMK_SetDynamicVariables"></a> Dynamische Variablen festlegen  
 Verwenden Sie den Tasksequenzschritt **Dynamische Variablen festlegen** zum Ausführen der folgenden Aufgaben:  

1.  Sammeln von Informationen vom Computer und aus der Umgebung, in der er sich befindet, und Festlegen angegebener Tasksequenzvariablen anhand dieser Informationen.  

2.  Auswerten definierter Regeln und Festlegen von Tasksequenzvariablen basierend auf den Variablen und Werten, die für als „Wahr“ ausgewertete Regeln konfiguriert wurden.  

 Die Tasksequenz legt automatisch die folgenden schreibgeschützten Tasksequenzvariablen fest:  

 -   &#95;SMSTSMake  

 -   &#95;SMSTSModel  

 -   &#95;SMSTSMacAddresses  

 -   &#95;SMSTSIPAddresses  

 -   &#95;SMSTSSerialNumber  

 -   &#95;SMSTSAssetTag  

 -   &#95;SMSTSUUID  

 Dieser Schritt kann entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Weitere Informationen zu Tasksequenzvariablen finden Sie unter [Tasksequenz-Aktionsvariablen](task-sequence-action-variables.md).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

**Name**  
 Ein kurzer benutzerdefinierter Name für diesen Tasksequenzschritt.  

**Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

**Dynamische Regeln und Variablen**  
 Um eine dynamische Variable für die Verwendung in der Tasksequenz festzulegen, können Sie eine Regel hinzufügen und anschließend einen Wert für jede Variable angeben, die Sie für die Regel angeben, oder eine oder mehrere Variablen hinzufügen, ohne eine Regel hinzuzufügen. Wenn Sie eine Regel hinzufügen, können Sie unter den folgenden Regelkategorien wählen:  

 -   **Computer**: Verwenden Sie diese Regelkategorie, um Werte für Bestandskennzeichen, UUID, Seriennummer oder Mac-Adresse auszuwerten. Sie können mehrere Werte festlegen, und wenn jeder Wert wahr ist, wird die Regel als „Wahr“ ausgewertet. Die folgende Regel wird z. B. als „Wahr“ ausgewertet, wenn die Seriennummer 5892087 lautet, unabhängig davon, ob die MAC-Adresse 26-78-13-5A-A4-22 entspricht.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Speicherort**: Verwenden Sie diese Regelkategorie, um Werte für das Standardgateway auszuwerten.  

-   **Hersteller und Modell**: Verwenden Sie diese Regelkategorie, um Werte für den Hersteller und das Modell eines Computers auszuwerten. Sowohl Hersteller als auch Modell müssen als „Wahr“ ausgewertet werden, damit die Regel als „Wahr“ ausgewertet wird.   

    Ab Version 1610 von Configuration Manager können Sie ein Sternchen (*****) und ein Fragezeichen (**?**) als Platzhalter an der Stelle angeben, an der ***** mehreren Zeichen und **?** entspricht. entspricht einem einzelnen Zeichen. Zum Beispiel die Zeichenfolge „DELL*900?“ wird „DELL-ABC-9001“ und „DELL9009“ entsprechen.

-   **Tasksequenzvariable**: Verwenden Sie diese Regelkategorie, um eine Tasksequenzvariable, eine Bedingung und einen Wert zum Auswerten anzugeben. Die Regel wird als „Wahr“ ausgewertet, wenn der für die Variable festgelegte Wert die angegebene Bedingung erfüllt.  

Sie können eine oder mehrere Variablen angeben, die für eine Regel festgelegt werden, die als „Wahr“ ausgewertet wird, oder Variablen ohne Verwendung einer Regel festlegen. Sie können eine vorhandene Variable auswählen oder eine benutzerdefinierte Variable erstellen.  

 -   **Vorhandene Tasksequenzvariablen**: Verwenden Sie diese Einstellung, um eine oder mehrere Variablen aus einer Liste vorhandener Tasksequenzvariablen auszuwählen. Arrayvariablen stehen nicht zur Auswahl.  

 -   **Benutzerdefinierte Tasksequenzvariablen**: Verwenden Sie diese Einstellung, um eine benutzerdefinierte Tasksequenzvariable zu definieren. Sie können auch eine vorhandene Tasksequenzvariable angeben. Dies ist nützlich, um ein vorhandenes Variablenarray wie z. B. OSDAdapter anzugeben, da Variablenarrays nicht in der Liste der vorhandenen Tasksequenzvariablen enthalten sind.  

Nachdem Sie die Variablen für eine Regel ausgewählt haben, müssen Sie einen Wert für jede Variable angeben. Die Variable wird auf den angegebenen Wert festgelegt, wenn die Regel als „Wahr“ ausgewertet wird. Sie können für jede Variable **Geheimer Wert** auswählen, um den Wert der Variablen auszublenden. Standardmäßig werden Werte für einige vorhandene Variablen ausgeblendet, z. B. für die Tasksequenzvariable OSDCaptureAccountPassword.  

> [!IMPORTANT]  
>  Wenn Sie eine Tasksequenz mit dem Schritt „Dynamische Variablen festlegen“ importieren und **Geheimer Wert** für den Wert der Variablen ausgewählt ist, wird der Wert beim Importieren der Tasksequenz entfernt. Daher müssen Sie den Wert für die dynamische Variable nach dem Import der Tasksequenz erneut eingeben.  

##  <a name="BKMK_SetTaskSequenceVariable"></a> Tasksequenzvariable festlegen  
Mithilfe des Tasksequenzschritts **Tasksequenzvariable festlegen** können Sie den Wert einer Variablen festlegen, die für die Tasksequenz verwendet wird.  

Dieser Schritt kann entweder in einem Standardbetriebssystem oder in Windows PE ausgeführt werden. Tasksequenzvariablen werden von Tasksequenzaktionen gelesen und definieren das Verhalten dieser Aktionen. Weitere Informationen zu bestimmten Tasksequenzvariablen finden Sie unter [Tasksequenz-Aktionsvariablen](task-sequence-action-variables.md).  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name für diesen Tasksequenzschritt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Tasksequenzvariable**  
 Ein benutzerdefinierter Name für die Tasksequenzvariable.  

 **Wert**  
 Der Wert, der der Tasksequenzvariable zugeordnet wird. Der Wert kann eine andere Tasksequenzvariable mit der Syntax %<varname\>% sein.  

## <a name="hide-task-sequence-progress"></a>Ausblenden des Tasksequenzstatus
<!-- 1354291 -->
Mit dem Release 1706 können Sie mithilfe einer neuen Variablen steuern, wann Endbenutzern der Tasksequenzstatus angezeigt wird. Verwenden Sie in der Tasksequenz den Schritt **Tasksequenzvariable festlegen** zum Festlegen des Werts der Variablen **TSDisableProgressUI**, um den Tasksequenzstatus ein- oder auszublenden. Den Schritt „Tasksequenzvariable festlegen“ können Sie in einer Tasksequenz mehrmals verwenden, um den Wert der Variablen zu ändern. Dadurch können Sie den Tasksequenzstatus in unterschiedlichen Abschnitten der Tasksequenz anzeigen oder ausblenden.

 - **So blenden Sie den Tasksequenzstatus aus**  
Verwenden Sie im Tasksequenz-Editor den Schritt [Tasksequenzvariable festlegen](#BKMK_SetTaskSequenceVariable) zum Festlegen des Werts der Variablen **TSDisableProgressUI** auf **TRUE**, um den Tasksequenzstatus auszublenden.

 - **So zeigen Sie den Tasksequenzstatus an**  
Verwenden Sie im Tasksequenz-Editor den Schritt [Tasksequenzvariable festlegen](#BKMK_SetTaskSequenceVariable) zum Festlegen des Werts der Variablen **TSDisableProgressUI** auf **FALSE**, um den Tasksequenzstatus anzuzeigen.

##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Windows und ConfigMgr einrichten  
 Mithilfe des Tasksequenzschritts **Windows und ConfigMgr einrichten** können Sie den Übergang von Windows PE zum neuen Betriebssystem vollziehen. Dieser Tasksequenzschritt muss bei jeder Betriebssystembereitstellung ausgeführt werden. Mit diesem Schritt wird der Configuration Manager-Client im neuen Betriebssystem installiert und die weitere Ausführung der Tasksequenz im neuen Betriebssystem ermöglicht.  

 Dieser Schritt wird nur in Windows PE ausgeführt. Er wird nicht in einem Standardbetriebssystem ausgeführt. Weitere Informationen zu Tasksequenzvariablen für diese Tasksequenzaktion finden Sie unter [Variablen der Tasksequenzaktion „Windows und ConfigMgr einrichten“](task-sequence-action-variables.md#BKMK_SetupWindows).  

 Mit der Tasksequenzaktion **Windows und ConfigMgr einrichten** werden sysprep.inf- oder unattend.xml-Verzeichnisvariablen wie %WINDIR% und %ProgramFiles% durch das Windows°PE-Installationsverzeichnis „X:\Windows“ ersetzt. Mit diesen Umgebungsvariablen angegebene Tasksequenzvariablen werden ignoriert.  

 Verwenden Sie diesen Tasksequenzschritt zur Durchführung der nachstehend beschriebenen Aktionen:  

1.  Vorbereitende Maßnahmen: Windows°PE  

    1.  Ersetzt die Tasksequenzvariable in der Datei „unattend.xml“.  

    2.  Das Paket, das den Configuration Manager-Client enthält, wird heruntergeladen und in das bereitgestellte Image eingefügt.  

2.  Einrichten von Windows  

    1.  Imagebasierte Installation.  

        1.  Der Configuration Manager-Client im Image wird deaktiviert (d.h. der automatische Start für den Configuration Manager-Clientdienst wird deaktiviert).  

        2.  Es wird ein Update der Registrierung im bereitgestellten Abbild ausgeführt, um zu sicherzustellen, dass das bereitgestellte Betriebssystem mit demselben Laufwerksbuchstaben gestartet wird wie auf dem Referenzcomputer.  

        3.  Es wird ein Neustart im bereitgestellten Betriebssystem ausgeführt.  

        4.  Die Windows-Miniinstallation wird unter Verwendung der zuvor angegebenen Datei sysprep.inf oder unattend.xml ausgeführt. Bei diesem Vorgang werden alle Interaktionen mit Endbenutzern unterdrückt. Hinweis: Wenn unter **Netzwerkeinstellungen anwenden** ein Domänenbeitritt angegeben wurde, wird diese Information in der Datei „sysprep.inf“ oder „unattend.xml“ gespeichert, und der Domänenbeitritt erfolgt im Rahmen der Windows-Miniinstallation.  

    2.  Setup.exe-basierte Installation.  Führt „Setup.exe“ aus. Dieser Vorgang entspricht dem normalen Windows-Installationsprozess:  

        1.  Das zu einem früheren Zeitpunkt in der Tasksequenz **Betriebssystem anwenden** angegebene Betriebssystem wird auf die Festplatte kopiert.  

        2.  Es wird ein Neustart im neu bereitgestellten Betriebssystem ausgeführt.  

        3.  Die Windows-Miniinstallation wird unter Verwendung der zuvor angegebenen Datei sysprep.inf oder unattend.xml ausgeführt. Bei diesem Vorgang werden alle Einstellungen der Benutzeroberfläche unterdrückt. Hinweis: Wenn unter **Netzwerkeinstellungen anwenden** ein Domänenbeitritt angegeben wurde, wird diese Information in der Datei „sysprep.inf“ oder „unattend.xml“ gespeichert, und der Domänenbeitritt erfolgt im Rahmen der Windows-Miniinstallation.  

3.  Einrichten des Configuration Manager-Clients  

    1.  Nachdem die Windows-Miniinstallation abgeschlossen ist, wird die Tasksequenz mithilfe von „setupcomplete.cmd“ fortgesetzt.  

    2.  Das lokale Administratorkonto wird aktiviert oder deaktiviert, je nachdem, welche Option im Schritt **Windows-Einstellungen anwenden** ausgewählt wurde.  

    3.  Der Configuration Manager-Client wird mithilfe des zuvor heruntergeladenen Downloadpakets (1.b) und unter Verwendung der im Tasksequenz-Editor angegebenen Installationseigenschaften installiert. Der Client wird im Bereitstellungsmodus installiert, um zu verhindern, dass neue Richtlinienanforderungen verarbeitet werden, bevor die Tasksequenz abgeschlossen ist.  

    4.  Wartet, bis der Client voll funktionstüchtig ist.  

    5.  Wenn der Computer in einer Umgebung mit aktiviertem Netzwerkzugriffsschutz ausgeführt wird, führt der Client eine Überprüfung auf Updates durch und installiert alle erforderlichen Updates. Damit wird gewährleistet, dass alle erforderlichen Updates vorhanden sind, bevor die Tasksequenz weiter ausgeführt wird.  

4.  Die Ausführung der Tasksequenz wird mit dem nächsten Schritt fortgesetzt.  

> [!NOTE]  
>  Die Tasksequenzaktion **Windows und ConfigMgr einrichten** ist für die Ausführung des Tools „Gruppenrichtlinie“ auf dem neu installierten Computer verantwortlich. Die Gruppenrichtlinie wird nach Abschluss der Tasksequenz angewendet.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Wählen Sie nicht aus, dass die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt. Bei einem Fehler wird die Tasksequenz nicht ausgeführt, und zwar unabhängig davon, ob Sie diese Einstellung auswählen oder nicht.  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Gibt einen kurzen benutzerdefinierten Namen an, der die in diesem Schritt vorgenommene Aktion beschreibt.  

 **Beschreibung**  
 Gibt zusätzliche Informationen zu der in diesem Schritt ausgeführten Aktion an.  

 **Clientpaket**  
 Gibt das Configuration Manager-Clientinstallationspaket an, das von diesem Tasksequenzschritt verwendet wird. Klicken Sie auf **Durchsuchen**, und wählen Sie das Clientinstallationspaket aus, das Sie zum Installieren des Configuration Manager-Clients verwenden möchten.  

 **Clientpaket vor der Produktion verwenden, wenn verfügbar**  
 Gibt an, dass im Tasksequenzschritt bei Verfügbarkeit eines Präproduktionsclient-Pakets dieses Paket anstelle des Produktionsclientpakets verwendet wird. Der Präproduktionsclient ist normalerweise eine neuere Version, die in der Produktionsumgebung getestet wird. Klicken Sie auf **Durchsuchen**, und wählen Sie das Präproduktions-Clientinstallationspaket aus, das Sie zum Installieren des Configuration Manager-Clients verwenden möchten.  

 **Installationseigenschaften**  
 Die Standortzuweisung und die Standardkonfiguration werden von der Tasksequenzaktion automatisch angegeben. Sie können in diesem Feld zusätzliche Installationseigenschaften angeben, die bei der Installation des Clients verwendet werden sollen. Wenn sie mehrere Installationseigenschaften eingeben möchten, müssen Sie sie durch ein Leerzeichen trennen.  

 Sie können Befehlszeilenoptionen angeben, die während der Clientinstallation verwendet werden sollen. Sie können beispielsweise **/skipprereq: silverlight.exe** eingeben, um „CCMSetup.exe“ anzuweisen, die erforderliche Komponente Microsoft Silverlight nicht zu installieren. Weitere Informationen zu diesen Befehlszeileneigenschaften für CCMSetup.exe finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="BKMK_UpgradeOS"></a> Betriebssystem aktualisieren  
 Verwenden Sie den Tasksequenzschritt **Betriebssystem aktualisieren** zum Aktualisieren eines vorhandenen Windows 7-, Windows 8-, Windows 8.1- oder Windows 10-Betriebssystems auf Windows 10.  

 Dieser Tasksequenzschritt wird nur in einem Standardbetriebssystem ausgeführt. Er wird nicht in Windows PE ausgeführt.  

### <a name="details"></a>Details  
 Die in diesem Abschnitt beschriebenen Einstellungen können Sie auf der Registerkarte **Eigenschaften** für diesen Schritt konfigurieren.  

 Verwenden Sie zudem die Registerkarte **Optionen** für die folgenden Aktionen:  

-   Schritt deaktivieren  

-   Angeben, ob die Tasksequenz fortgesetzt wird, wenn während der Ausführung dieses Schritts ein Fehler auftritt  

-   Bedingungen angeben, die für die Ausführung dieses Schritts erfüllt sein müssen  

 **Name**  
 Ein kurzer benutzerdefinierter Name, der die in diesem Schritt ausgeführte Aktion beschreibt.  

 **Beschreibung**  
 Ausführlichere Informationen zu der in diesem Schritt ausgeführten Aktion.  

 **Upgradepaket**  
 Wählen Sie diese Option aus, um das für das Upgrade zu verwendende Windows 10-Betriebssystemupgradepaket anzugeben.  

 **Quellpfad**  
 Gibt einen lokalen oder Netzwerkpfad zu den zu verwendenden Windows 10-Medien an (entspricht der Befehlszeilenoption „/installFrom“). Sie können auch eine Variable angeben, z. B. %mycontentpath% oder %DPC01%. Wenn Sie eine Variable als Quellpfad verwenden, muss diese zuvor in der Tasksequenz festgelegt werden. Wenn Sie beispielsweise den Schritt [Paketinhalt herunterladen](#BKMK_DownloadPackageContent) in der Tasksequenz verwenden, können Sie eine Variable für den Speicherort des Betriebssystemupgradepakets festlegen. Anschließend können Sie die Variable in diesem Schritt als Quellpfad verwenden.  

 **Edition**  
 Geben Sie die für das Upgrade zu verwendende Edition in den Betriebssystemmedien an.  

 **Product Key**  
 Geben Sie den auf den Upgradeprozess anzuwendenden Product Key an.  

 **Folgenden Treiberinhalt während des Upgrades für Windows Setup bereitstellen**  
 Wählen Sie diese Einstellung aus, um während des Upgradeprozesses Treiber zum Zielcomputer hinzuzufügen (entspricht der Befehlszeilenoption „/InstallDriver“). Die Treiber müssen mit Windows 10 kompatibel sein. Geben Sie eine der folgenden Optionen an:  

-   **Treiberpaket**: Klicken Sie auf **Durchsuchen** , und wählen Sie ein vorhandenes Treiberpaket aus der Liste aus.  

-   **Bereitgestellter Inhalt**: Wählen Sie diese Option, um den Speicherort für das Treiberpaket anzugeben. Sie können einen lokalen Ordner, einen Netzwerkpfad oder eine Tasksequenzvariable angeben. Wenn Sie eine Variable als Quellpfad verwenden, muss diese zuvor in der Tasksequenz festgelegt werden. Zum Beispiel mithilfe des Schritts [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) .  

 **Timeout (Minuten)**  
 Gibt an, wie lange Setup ausgeführt werden muss (in Minuten), bevor Configuration Manager für den Tasksequenzschritt einen Fehler ausgibt.  

 **Kompatibilitätsprüfung für Windows Setup ausführen, ohne Upgrade zu starten**  
 Gibt an, dass die Windows Setup-Kompatibilitätsüberprüfung ohne Starten des Upgradeprozesses ausgeführt werden soll (entspricht der Befehlszeilenoption „/Compat ScanOnly“). Wenn Sie diese Option verwenden, müssen Sie trotzdem die gesamte Installationsquelle bereitstellen. Setup gibt als Ergebnis der Überprüfung einen Exitcode zurück. Die folgende Tabelle enthält einige der häufigeren Exitcodes.  

|Exitcode|Details|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Keine Kompatibilitätsprobleme (Erfolg).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Kompatibilitätsprobleme mit Handlungsbedarf.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Ausgewählte Migrationsoption ist nicht verfügbar, z. B. Enterprise zu Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Nicht für Windows 10 geeignet.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Nicht genügend freier Speicherplatz.|  

 Weitere Informationen zu diesem Parameter finden Sie unter [Windows Setup-Befehlszeilenoptionen](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).  

 **Alle ablehnbaren Kompatibilitätsmeldungen ignorieren**  
 Gibt an, dass Setup die Installation abschließt und dabei alle vernachlässigbaren Kompatibilitätsmeldungen ignoriert (entspricht der Befehlszeilenoption „/Compat IgnoreWarning“).  

 **Windows Setup dynamisch mit Windows Update aktualisieren**  
 Gibt an, ob Setup dynamische Updatevorgänge durchführt, z. B. Suchen, Herunterladen und Installieren von Updates (entspricht der Befehlszeilenoption „/DynamicUpdate“). Diese Einstellung ist nicht kompatibel mit Configuration Manager-Softwareupdates, kann aber aktiviert werden, wenn Sie Updates mit WSUS (eigenständig) oder Windows Update verarbeiten.  

 **Richtlinie überschreiben und standardmäßiges Microsoft Update verwenden**: Wenn Sie diese Einstellung auswählen, wird die lokale Richtlinie vorübergehend in Echtzeit außer Kraft gesetzt, um dynamische Updatevorgänge auszuführen und den Computer Updates von Windows Update abrufen zu lassen.  
