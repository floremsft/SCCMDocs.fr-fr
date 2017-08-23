---
title: "Erstellen eigenständiger Medien mit System Center Configuration Manager | Microsoft Docs"
description: "Verwenden Sie eigenständige Medien, um das Betriebssystem auf einem Computer ohne Verbindung mit einem Configuration Manager-Standort oder einem Netzwerk bereitzustellen."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
caps.latest.revision: "21"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 98f902429ad1b9965a0dc4cc2e1bd071ad5c0779
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Erstellen eigenständiger Medien mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Eigenständige Medien in Configuration Manager enthalten alles, was zur Bereitstellung des Betriebssystems auf einem Computer ohne Verbindung mit einem Configuration Manager-Standort oder einem Netzwerk erforderlich ist. Verwenden Sie eigenständige Medien bei folgenden Szenarien für die Betriebssystembereitstellung:  

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Upgrade von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md)  

Eigenständige Medien enthalten die Tasksequenz, mit der die Schritte zum Installieren des Betriebssystems und aller anderen erforderlichen Inhalte, einschließlich Startimage, Betriebssystemimage und Gerätetreiber, automatisiert werden. Da alle Komponenten für die Bereitstellung des Betriebssystems auf den eigenständigen Medien gespeichert sind, ist der Speicherplatzbedarf für eigenständige Medien wesentlich größer als für andere Medientypen. Wenn Sie an einem Standort der zentralen Verwaltung eigenständige Medien erstellen, ruft der Client seinen zugewiesenen Standortcode aus Active Directory ab. An einem untergeordneten Standort erstellte eigenständige Medien werden automatisch dem Client und dem Standortcode für diesen Standort zugewiesen.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Erstellen eigenständiger Medien  
Bevor Sie eigenständige Medien mithilfe des Assistenten zum Erstellen von Tasksequenzmedien erstellen, achten Sie darauf, dass die folgenden Bedingungen erfüllt sind:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Erstellen einer Tasksequenz zum Bereitstellen eines Betriebssystems
Als Teil der eigenständigen Medien müssen Sie die Tasksequenz zum Bereitstellen eines Betriebssystems angeben. Die Schritte zum Erstellen einer neuen Tasksequenz finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Die folgenden Aktionen werden für eigenständige Medien nicht unterstützt:
- Der Schritt „Treiber automatisch anwenden“ in der Tasksequenz. Die automatische Anwendung von Gerätetreibern aus dem Treiberkatalog wird nicht unterstützt, Sie können aber den Schritt „Treiberpaket anwenden“ auswählen, um Windows Setup eine angegebene Gruppe von Treibern verfügbar zu machen.
- Der Tasksequenzschritt für das Herunterladen von Paketinhalten. Die Informationen vom Verwaltungspunkt sind nicht auf eigenständigen Medien verfügbar, sodass bei dem Schritt ein Fehler auftritt, wenn versucht wird, die Inhaltsspeicherorte aufzulisten.
- Installieren von Softwareupdates
- Installieren von Software vor dem Bereitstellen des Betriebssystems
- Tasksequenzen für Nicht-Betriebssystembereitstellungen.
- Zuweisen von Benutzern zum Zielcomputer, um die Affinität zwischen Benutzer und Gerät zu unterstützen
- Dynamische Paketinstallationen über den Task „Pakete installieren“.
- Dynamische Anwendungsinstallationen über den Task „Anwendung installieren“.

> [!NOTE]    
> Wenn die Tasksequenz zum Bereitstellen eines Betriebssystems den Schritt [Paket installieren](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) enthält und Sie die eigenständigen Medien an einem Standort der zentralen Verwaltung erstellen, kann ein Fehler auftreten. Der Standort der zentralen Verwaltung verfügt nicht über die erforderlichen Clientkonfigurationsrichtlinien, die während der Ausführung der Tasksequenz zum Aktivieren des Softwareverteilungs-Agents benötigt werden. In der Datei „CreateTsMedia.log“ wird möglicherweise der folgenden Fehler angezeigt:    
>     
> „WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)“    
> 
> Sie müssen eigenständige Medien, die den Schritt **Paket installieren** aufweisen, an einem primären Standort erstellen, für den der Softwareverteilungs-Agent aktiviert ist. Alternativ dazu können Sie den Schritt [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine) nach dem Schritt [Windows und ConfigMgr einrichten](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) und vor dem ersten Schritt **Paket installieren** hinzufügen. Im Schritt **Befehlszeile ausführen** wird ein WMIC-Befehl ausgeführt, um den Softwareverteilungs-Agent vor der Ausführung des ersten Schritts "Paket installieren" zu aktivieren. Sie können im Tasksequenzschritt **Befehlszeile ausführen** Folgendes verwenden:    
>    
> *WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE*


> [!IMPORTANT]    
> Bei Verwendung des Tasksequenzschritts **Windows und ConfigMgr einrichten** in der Tasksequenz „Betriebssystem“ aktivieren Sie die Einstellung **Clientpaket vor der Produktion verwenden, wenn verfügbar** nicht für eigenständige Medien. Wenn diese Einstellung aktiviert ist, und das Clientpaket vor der Produktion verfügbar ist, wird es in den eigenständigen Medien verwendet. Dies wird nicht unterstützt. Einzelheiten zu dieser Einstellung finden Sie unter [Windows und ConfigMgr einrichten](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Verteilen aller der Tasksequenz zugeordneten Inhalte
Sie müssen alle für die Tasksequenz erforderlichen Inhalte auf mindestens einen Verteilungspunkt verteilen. Dies schließt das Startabbild, Betriebssystemabbild und andere zugehörige Dateien ein. Die Informationen werden vom Assistenten beim Erstellen des eigenständigen Mediums vom Verteilungspunkt abgerufen. Sie benötigen **Lesezugriffsrechte**  für die Inhaltsbibliothek an diesem Verteilungspunkt.  Details finden Sie unter [Verteilen von Inhalt, auf den von einer Tasksequenz verwiesen wird](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Vorbereiten des USB-Wechseldatenträgers
*Für einen USB-Wechseldatenträger:*

Bei Verwendung eines USB-Wechseldatenträgers muss das USB-Laufwerk mit dem Computer verbunden werden, auf dem der Assistent ausgeführt wird. Das USB-Laufwerk muss zudem für Windows als Wechselmedium erkennbar sein. Beim Erstellen der Medien wird vom Assistenten direkt auf den USB-Datenträger geschrieben. Von eigenständigen Medien wird ein FAT32-Dateisystem verwendet. Sie können keine eigenständigen Medien auf einem USB-Speicherstick erstellen, der eine Datei mit einer Größe von mehr als 4 GB enthält.

### <a name="create-an-output-folder"></a>Erstellen eines Ausgabeordners
*Für einen CD/DVD-Satz:*

Sie müssen für die vom Assistenten zum Erstellen von Tasksequenzmedien erstellten Ausgabedateien einen Ordner anlegen, bevor Sie den Assistenten ausführen, um Medien für einen CD- oder DVD-Satz zu erstellen. Die für einen CD- oder DVD-Satz erstellten Medien werden als ISO-Dateien direkt in den Ordner geschrieben.


 Gehen Sie wie folgt vor, um eigenständige Medien für einen USB-Wechseldatenträger oder einen CD-/DVD-Satz zu erstellen.  

## <a name="to-create-stand-alone-media"></a>So erstellen Sie eigenständige Medien  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenzmedien erstellen** , um den Assistenten zum Erstellen von Tasksequenzmedien zu starten.  

4.  Geben Sie auf der Seite **Medientyp wählen** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Wählen Sie **Eigenständige Medien**aus.  

    -   Optional können Sie **Unbeaufsichtigte Betriebssystembereitstellung zulassen**auswählen, wenn Sie die Bereitstellung des Betriebssystems ohne Benutzereingabe gestatten möchten. Wenn Sie diese Option auswählen, wird der Benutzer nicht aufgefordert, Informationen zur Netzwerkkonfiguration oder optionale Tasksequenzen anzugeben. Allerdings wird der Benutzer weiterhin zur Eingabe eines Kennworts aufgefordert, wenn die Medien für den Kennwortschutz konfiguriert sind.  

5.  Geben Sie auf der Seite **Medientyp** an, ob das Medium ein Speicherstick oder ein CD/DVD-Satz ist, und klicken Sie dann, um Folgendes zu konfigurieren:  

    > [!IMPORTANT]  
    >  Von eigenständigen Medien wird ein FAT32-Dateisystem verwendet. Sie können keine eigenständigen Medien auf einem USB-Speicherstick erstellen, der eine Datei mit einer Größe von mehr als 4 GB enthält.  

    -   Wenn Sie **USB-Speicherstick**auswählen, geben Sie das Laufwerk an, auf dem der Inhalt gespeichert wird.  

    -   Wenn Sie **CD/DVD-Satz**auswählen, geben Sie die Kapazität der Medien und Namen sowie Pfad der Ausgabedateien an. Die Ausgabedateien werden vom Assistenten an diesen Speicherort geschrieben. Beispiel: **\\\Servername\Ordner\Ausgabedatei.iso**  

         Wenn die Medienkapazität zu gering zum Speichern des gesamten Inhalts ist, werden mehrere Dateien erstellt, und Sie müssen den Inhalt auf mehreren CDs oder DVDs speichern. Falls mehrere Medien erforderlich sind, wird dem Namen jeder von Configuration Manager erstellten Ausgabedatei eine Sequenznummer hinzugefügt. Außerdem wird die Anwendung von Configuration Manager auf mehreren Medien gespeichert, wenn Sie eine Anwendung zusammen mit dem Betriebssystem bereitstellen und die Anwendung nicht auf ein einzelnes Medium passt. Wenn das eigenständige Medium ausgeführt wird, wird der Benutzer von Configuration Manager zum Angeben des nächsten Mediums aufgefordert, auf dem die Anwendung gespeichert ist.   

         > [!IMPORTANT]  
         >  Wenn Sie ein vorhandenes ISO-Abbild auswählen, wird dieses ISO-Abbild vom Assistenten zum Erstellen von Tasksequenzmedien auf dem Laufwerk oder der Freigabe gelöscht, sobald Sie mit der nächsten Seite des Assistenten fortfahren. Das vorhandene Abbild wird selbst dann gelöscht, wenn Sie den Assistenten anschließend abbrechen.  

     Klicken Sie auf **Weiter**.  

6.  Wählen Sie auf der Seite **Sicherheit** die folgenden Einstellungen aus, und klicken Sie dann auf **Weiter**:
    - **Medien durch Kennwort schützen**: Geben Sie ein sicheres Kennwort zum Schutz der Medien ein. Wenn Sie ein Kennwort angeben, ist dieses zum Verwenden der Medien erforderlich.  

        > [!IMPORTANT]  
        >  Auf eigenständigen Medien werden nur die Tasksequenzschritte und die dazugehörigen Variablen verschlüsselt. Der restliche Inhalt der Medien wird nicht verschlüsselt. Tasksequenzskripts dürfen daher keine vertraulichen Informationen enthalten. Speichern und implementieren Sie alle vertraulichen Informationen mithilfe von Tasksequenzvariablen.  

    - **Datumsbereich für dieses eigenständige Medium auswählen, damit es gültig ist** (ab Version 1702): Optionale Start- und Ablaufdaten auf den Medien festlegen. Standardmäßig sind diese Einstellungen deaktiviert. Vor der Ausführung des eigenständigen Mediums werden die Datums- und Zeitangaben für den Zeitraum mit der Systemzeit auf dem Computer verglichen. Wenn die Systemzeit vor der Startzeit oder hinter der Ablaufzeit liegt, wird das eigenständige Medium nicht gestartet. Diese Optionen sind auch über das PowerShell-Cmdlet „New-CMStandaloneMedia“ verfügbar.
7.  Geben Sie auf der Seite **Eigenständige CD/DVD** die Tasksequenz an, mit der das Betriebssystem bereitgestellt wird, und klicken Sie dann auf **Weiter**. Wählen Sie **Zugeordnete Anwendungsabhängigkeiten erkennen und diesem Medium hinzufügen** aus, um eigenständigen Medien für Anwendungsabhängigkeiten Inhalt hinzuzufügen.
    > [!TIP]
    > Wenn Sie die erwarteten Anwendungsabhängigkeiten nicht angezeigt bekommen, dann heben Sie die Auswahl auf und wählen erneut die Einstellung **Zugeordnete Anwendungsabhängigkeiten erkennen und diesem Medium hinzufügen** aus, um die Liste zu aktualisieren.

    Im Assistenten können Sie nur die Tasksequenzen auswählen, die einem Startabbild zugewiesen sind.  

8. Wählen Sie auf der Seite **Anwendung auswählen** (verfügbar ab Version 1702) den als Teil der Mediendatei hinzuzufügenden Anwendungsinhalt aus, und klicken Sie anschließend auf **Weiter**.
9. Wählen Sie auf der Seite **Paket auswählen** (verfügbar ab Version 1702) den als Teil der Mediendatei hinzuzufügenden Paketinhalt aus, und klicken Sie anschließend auf **Weiter**.
10. Wählen Sie auf der Seite **Treiberpaket auswählen** (verfügbar ab Version 1702) den als Teil der Mediendatei hinzuzufügenden Treiberpaketinhalt aus, und klicken Sie anschließend auf **Weiter**.
11.  Geben Sie auf der Seite **Verteilungspunkte** die Verteilungspunkte an, die den für die Tasksequenz erforderlichen Inhalt enthalten, und klicken Sie dann auf **Weiter**.  

     Configuration Manager zeigt nur Verteilungspunkte an, die Inhalt aufweisen. Sie müssen alle der Tasksequenz zugeordneten Inhalte (Startabbild, Betriebssystemabbild usw.) auf mindestens einen Verteilungspunkt aufteilen, bevor Sie fortfahren können. Nachdem Sie den Inhalt verteilt haben, können Sie entweder den Assistenten neu starten oder Verteilungspunkte entfernen, die Sie bereits auf dieser Seite ausgewählt haben, zur vorherigen Seite wechseln und dann zur Seite **Verteilungspunkte** zurückkehren, um die Liste der Verteilungspunkte zu aktualisieren. Weitere Informationen zur Inhaltsverteilung finden Sie unter [Verteilen von Inhalt, auf den von einer Tasksequenz verwiesen wird](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS). Weitere Informationen zu Verteilungspunkten sowie zum Content Management finden Sie unter [Manage content and content infrastructure for System Center Configuration Manager (Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager)](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  Sie benötigen **Lesezugriffsrechte** für die Inhaltsbibliothek an den Verteilungspunkten.  

12. Geben Sie auf der Seite **Anpassung** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie die Variablen an, die von der Tasksequenz zur Bereitstellung des Betriebssystems verwendet werden.  

    -   Geben Sie alle Prestart-Befehle an, die Sie vor der Tasksequenz ausführen möchten. Bei Prestart-Befehlen handelt es sich um eine Skriptdatei oder ausführbare Datei, über die eine Interaktion mit dem Benutzer in Windows PE möglich ist, bevor die Tasksequenz zur Installation des Betriebssystems ausgeführt wird. Weitere Informationen zu Prestart-Befehlen für Medien finden Sie unter [Prestart-Befehle für Tasksequenzmedien in System Center Configuration Manager](../understand/prestart-commands-for-task-sequence-media.md).  

         Wählen Sie optional **Dateien für den Prestart-Befehl einbeziehen** aus, um alle für den Prestart-Befehl erforderlichen Dateien einzubeziehen.  

        > [!TIP]  
        >  Während der Erstellung der Tasksequenzmedien werden die Paket-ID und die Prestart-Befehlszeile einschließlich des Wertes vorhandener Tasksequenzvariablen von der Tasksequenz in die Protokolldatei „CreateTSMedia.log“ auf dem Computer geschrieben, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können diese Protokolldatei überprüfen, um den Wert für die Tasksequenzvariablen zu überprüfen.  

13. Schließen Sie den Assistenten ab.  

 Die Dateien der eigenständigen Medien (ISO) werden im Zielordner erstellt. Wenn Sie **Eigenständige CD/DVD**ausgewählt haben, können Sie nun die Ausgabedateien auf einen Satz von CDs oder DVDs kopieren.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Beispiel für eine Tasksequenz für eigenständige Medien  
 Orientieren Sie sich an der folgenden Tabelle, während Sie eine Tasksequenz zur Bereitstellung eines Betriebssystems mithilfe eigenständiger Medien erstellen. Mithilfe dieser Tabelle können Sie die allgemeine Sequenz für Ihre Tasksequenzschritte festlegen und diese Tasksequenzschritte in logischen Gruppen organisieren. Die von Ihnen erstellte Tasksequenz kann von diesem Beispiel abweichen und eine andere Anzahl von Tasksequenzschritten und Tasksequenzgruppen enthalten.  

> [!NOTE]  
>  Sie müssen eigenständige Medien stets mithilfe des Assistenten zum Erstellen von Tasksequenzmedien erstellen.  

|Tasksequenzgruppe/-schritt|Beschreibung|  
|---------------------------------|-----------------|  
|Dateien und Einstellungen erfassen – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine Tasksequenzgruppe. Mithilfe einer Tasksequenzgruppe können Sie ähnliche Tasksequenzschritte zur besseren Organisation und Fehlersteuerung gruppieren.|  
|Windows-Einstellungen erfassen|Identifizieren Sie mithilfe dieses Tasksequenzschritts die Microsoft Windows-Einstellungen, die vom vorhandenen Betriebssystem auf dem Zielcomputer erfasst werden, bevor neue Abbilder erstellt werden. Sie können den Computernamen, Benutzer- und Unternehmensinformationen sowie Zeitzoneneinstellungen erfassen.|  
|Netzwerkeinstellungen erfassen|Mithilfe dieses Tasksequenzschritts können Sie Netzwerkeinstellungen auf dem Computer erfassen, auf dem die Tasksequenz empfangen wird. Sie können die Domänen- oder Arbeitsgruppenmitgliedschaft des Computers sowie Informationen zur Netzwerkkarteneinstellung erfassen.|  
|Benutzerdateien und Einstellungen erfassen – **(Neue Tasksequenz-Untergruppe)**|Erstellen Sie eine Tasksequenzgruppe innerhalb einer anderen Tasksequenzgruppe. Diese Untergruppe enthält die Schritte, die erforderlich sind, um Benutzerzustandsdaten vom vorhandenen Betriebssystem auf dem Zielcomputer zu erfassen, bevor neue Abbilder erstellt werden. Ähnlich wie mithilfe der ersten von Ihnen hinzugefügten Gruppe können Sie mithilfe dieser Untergruppe ähnliche Tasksequenzschritte zur besseren Organisation und Fehlersteuerung gruppieren.|  
|Lokalen Zustandsspeicherort festlegen|Mithilfe dieses Tasksequenzschritts können Sie einen lokalen Speicherort unter Verwendung der Tasksequenzvariablen für den geschützten Pfad angeben. Der Benutzerzustand wird in einem geschützten Verzeichnis auf der Festplatte gespeichert.|  
|Benutzerzustand erfassen|Mithilfe dieses Tasksequenzschritts können Sie die Benutzerdateien und Einstellungen erfassen, die zum neuen Betriebssystem migriert werden sollen.|  
|Betriebssystem installieren – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Installieren des Betriebssystems erforderlichen Schritte.|  
|Neustart mit Windows PE oder Festplatte ausführen|Mithilfe dieses Tasksequenzschritts können Sie die Neustartoptionen für den Computer angeben, auf dem diese Tasksequenz empfangen wird. In diesem Schritt wird eine Meldung angezeigt, um den Benutzer darüber zu informieren, dass der Computer zum Fortsetzen der Installation neu gestartet wird.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSInWinPE** verwendet. Wenn der zugeordnete Wert **false** ist, wird der Tasksequenzschritt fortgesetzt.|  
|Betriebssystem anwenden|Mithilfe dieses Tasksequenzschritts können Sie das Betriebssystemabbild auf dem Zielcomputer installieren. In diesem Schritt werden alle Dateien auf diesem Volume (mit Ausnahme Configuration Manager-spezifischer Steuerungsdateien) gelöscht und anschließend alle in der WIM-Datei enthaltenen Volumeimages auf das entsprechende sequenzielle Datenträgervolume angewendet. Sie können auch durch Angeben einer **sysprep**-Antwortdatei konfigurieren, welche Festplattenpartition für die Installation verwendet wird.|  
|Windows-Einstellungen anwenden|Mithilfe dieses Tasksequenzschritts können Sie die Konfigurationsinformationen für die Windows-Einstellungen des Zielcomputers angeben. Folgende Windows-Einstellungen können anwendet werden: Benutzer- und Unternehmensinformationen, Produkt- oder Lizenzschlüsselinformationen, Zeitzone und lokales Administratorkennwort.|  
|Netzwerkeinstellungen anwenden|Mithilfe dieses Tasksequenzschritts können Sie die Konfigurationsinformationen für das Netzwerk oder die Arbeitsgruppe des Zielcomputers angeben. Sie können auch angeben, ob vom Computer ein DHCP-Server verwendet wird, oder Sie können die IP-Adressinformationen statisch zuweisen.|  
|Treiberpaket anwenden|Mithilfe dieses Tasksequenzschritts können Sie alle Gerätetreiber in einem Treiberpaket für Windows Setup zur Verfügung stellen. Alle notwendigen Gerätetreiber müssen auf den eigenständigen Medien enthalten sein.|  
|Betriebssystem einrichten – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Installieren des Configuration Manager-Clients erforderlichen Schritte.|  
|Windows und ConfigMgr einrichten|Mit diesem Tasksequenzschritt können Sie die Configuration Manager-Clientsoftware installieren. Mit dem Configuration Manager wird die GUID des Configuration Manager-Clients installiert und registriert. Sie können die erforderlichen Installationsparameter im Fenster **Installationseinstellungen** zuweisen.|  
|Benutzerdateien und Einstellungen wiederherstellen – **(Neue Tasksequenz-Untergruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Wiederherstellen des Benutzerzustands erforderlichen Schritte.|  
|Benutzerzustand wiederherstellen|Mithilfe dieses Tasksequenzschritts können Sie Windows-EasyTransfer bzw. USMT initiieren, um den Benutzerzustand und die Benutzereinstellungen, die mit der Aktion Benutzerzustand erfassen erfasst wurden, auf einem Zielcomputer wiederzuherstellen.|  
