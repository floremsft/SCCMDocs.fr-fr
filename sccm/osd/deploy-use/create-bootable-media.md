---
title: "Erstellen von startbaren Medien – Configuration Manager | Microsoft-Dokumentation"
description: "Startbare Medien in Configuration Manager erleichtern die Installation einer neuen Version von Windows oder ersetzen einen Computer und Übertragungseinstellungen."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 9032698fa12bf453041ea06bf330d3b4687c2a97
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>Erstellen startbarer Medien mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Startbare Medien in Configuration Manager enthalten das Startimage, optionale Prestart-Befehle und zugehörige Dateien sowie Configuration Manager-Dateien. Verwenden Sie vorab bereitgestellte Medien bei folgenden Szenarien für die Betriebssystembereitstellung:  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> Erstellen startbarer Medien  
 Beim Starten von startbaren Medien geschieht Folgendes: Der Zielcomputer wird gestartet, eine Verbindung mit dem Netzwerk wird hergestellt und die angegebene Tasksequenz sowie das Betriebssystemabbild und sämtlicher anderer erforderlicher Inhalt aus dem Netzwerk werden abgerufen. Da sich die Tasksequenz nicht auf den Medien befindet, brauchen Sie die Medien nicht neu zu erstellen, wenn Sie die Tasksequenz oder den Inhalt ändern. Die Pakete auf startbaren Medien sind nicht verschlüsselt. Sie müssen den Paketinhalt mithilfe geeigneter Sicherheitsmaßnahmen vor dem Zugriff Unbefugter schützen, z. B. durch Hinzufügen eines Kennworts für die Medien.  

 Bevor Sie startbaren Medien mithilfe des Assistenten zum Erstellen von Tasksequenzmedien erstellen, achten Sie darauf, dass alle folgenden  Bedingungen erfüllt sind:  

|Aufgabe|Beschreibung|  
|----------|-----------------|  
|Startabbild|Beachten Sie die folgenden Informationen zum Startabbild, das Sie in der Tasksequenz zum Bereitstellen des Betriebssystems verwenden:<br /><br /> - Die Architektur des Startimages muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.<br />- Achten Sie darauf, dass das Startimage die zur Bereitstellung des Zielcomputers erforderlichen Netzwerk- und Massenspeichertreiber enthält.|  
|Erstellen einer Tasksequenz zum Bereitstellen eines Betriebssystems|Als Teil der startbaren Medien müssen Sie die Tasksequenz zum Bereitstellen des Betriebssystems angeben. Die Schritte zum Erstellen einer neuen Tasksequenz finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).|  
|Verteilen aller der Tasksequenz zugeordneten Inhalte|Sie müssen alle für die Tasksequenz erforderlichen Inhalte auf mindestens einen Verteilungspunkt verteilen. Dies schließt das Startabbild und andere zugehörige Prestart-Dateien ein. Die Informationen werden vom Assistenten beim Erstellen startbarer Medien vom Verteilungspunkt abgerufen. Sie benötigen **Lesezugriffsrechte** für die Inhaltsbibliothek am Verteilungspunkt.  Weitere Informationen finden Sie unter [About the content library (Informationen zur Inhaltsbibliothek)](../../core/plan-design/hierarchy/the-content-library.md).|  
|Vorbereiten des USB-Wechseldatenträgers|Für einen USB-Wechseldatenträger:<br /><br /> Bei Verwendung eines USB-Wechseldatenträgers muss das USB-Laufwerk mit dem Computer verbunden werden, auf dem der Assistent ausgeführt wird. Das USB-Laufwerk muss zudem für Windows als Wechselmedium erkennbar sein. Beim Erstellen der Medien wird vom Assistenten direkt auf den USB-Datenträger geschrieben. Von eigenständigen Medien wird ein FAT32-Dateisystem verwendet. Sie können keine eigenständigen Medien auf einem USB-Speicherstick erstellen, der eine Datei mit einer Größe von mehr als 4 GB enthält.|  
|Erstellen eines Ausgabeordners|Für einen CD/DVD-Satz:<br /><br /> Sie müssen für die vom Assistenten zum Erstellen von Tasksequenzmedien erstellten Ausgabedateien einen Ordner anlegen, bevor Sie den Assistenten ausführen, um Medien für einen CD- oder DVD-Satz zu erstellen. Die für einen CD- oder DVD-Satz erstellten Medien werden als ISO-Dateien direkt in den Ordner geschrieben.|  

 Wenden Sie das folgende Verfahren an, um startbare Medien zu erstellen.  

### <a name="to-create-bootable-media"></a>So erstellen Sie startbare Medien  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenzmedien erstellen** , um den Assistenten zum Erstellen von Tasksequenzmedien zu starten.  

4.  Geben Sie auf der Seite **Medientyp wählen** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Wählen Sie **Startbare Medien**aus.  

    -   Optional können Sie **Unbeaufsichtigte Betriebssystembereitstellung zulassen**auswählen, wenn Sie die Bereitstellung des Betriebssystems nur ohne Benutzereingabe gestatten möchten.  

        > [!IMPORTANT]  
        >  Wenn Sie diese Option auswählen, wird der Benutzer nicht aufgefordert, Informationen zur Netzwerkkonfiguration oder optionale Tasksequenzen anzugeben. Allerdings wird der Benutzer weiterhin zur Eingabe eines Kennworts aufgefordert, wenn die Medien für den Kennwortschutz konfiguriert sind.  

5.  Geben Sie auf der Seite **Medienverwaltung** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Wählen Sie **Dynamisches Medium** aus, wenn Sie zulassen möchten, dass das Medium ausgehend vom Clientstandort innerhalb der Standortgrenzen von einem Verwaltungspunkt an einen anderen Verwaltungspunkt umgeleitet wird.  

    -   Wählen Sie **Standortbasiertes Medium** aus, wenn Sie wünschen, dass von dem Medium nur mit dem angegebenen Verwaltungspunkt Kontakt aufgenommen wird.  

6.  Geben Sie auf der Seite **Medientyp** an, ob das Medium ein Speicherstick oder ein CD/DVD-Satz ist, und klicken Sie dann, um Folgendes zu konfigurieren:  

    > [!IMPORTANT]  
    >  Von eigenständigen Medien wird ein FAT32-Dateisystem verwendet. Sie können keine eigenständigen Medien auf einem USB-Speicherstick erstellen, der eine Datei mit einer Größe von mehr als 4 GB enthält.  

    -   Wenn Sie **USB-Speicherstick**auswählen, geben Sie das Laufwerk an, auf dem der Inhalt gespeichert wird.  

    -   Wenn Sie **CD/DVD-Satz**auswählen, geben Sie die Kapazität der Medien und Namen sowie Pfad der Ausgabedateien an. Die Ausgabedateien werden vom Assistenten an diesen Speicherort geschrieben. Beispiel: **\\\Servername\Ordner\Ausgabedatei.iso**  

         Wenn die Medienkapazität zu gering zum Speichern des gesamten Inhalts ist, werden mehrere Dateien erstellt, und Sie müssen den Inhalt auf mehreren CDs oder DVDs speichern. Falls mehrere Medien erforderlich sind, wird dem Namen jeder von Configuration Manager erstellten Ausgabedatei eine Sequenznummer hinzugefügt. Außerdem wird die Anwendung von Configuration Manager auf mehreren Medien gespeichert, wenn Sie eine Anwendung zusammen mit dem Betriebssystem bereitstellen und die Anwendung nicht auf ein einzelnes Medium passt. Wenn das eigenständige Medium ausgeführt wird, wird der Benutzer von Configuration Manager zum Angeben des nächsten Mediums aufgefordert, auf dem die Anwendung gespeichert ist.  

        > [!IMPORTANT]  
        >  Wenn Sie ein vorhandenes ISO-Abbild auswählen, wird dieses ISO-Abbild vom Assistenten zum Erstellen von Tasksequenzmedien auf dem Laufwerk oder der Freigabe gelöscht, sobald Sie mit der nächsten Seite des Assistenten fortfahren. Das vorhandene Abbild wird selbst dann gelöscht, wenn Sie den Assistenten anschließend abbrechen.  

     Klicken Sie auf **Weiter**.  

7.  Geben Sie auf der Seite **Sicherheit** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren**, um zuzulassen, dass von dem Medium ein Betriebssystem auf einem nicht von Configuration Manager verwalteten Computer bereitgestellt wird. Für diese Computer gibt es in der Configuration Manager-Datenbank keine Einträge.  

         Zu unbekannten Computern gehören die folgenden:  

        -   Computer, auf denen kein Configuration Manager-Client installiert ist  

        -   Computer, die nicht in Configuration Manager importiert wurden  

        -   Computer, die von Configuration Manager nicht ermittelt wurden  

    -   Aktivieren Sie das Kontrollkästchen **Medien durch Kennwort schützen** , und geben Sie ein sicheres Kennwort ein, um das Medium vor dem Zugriff Unbefugter zu schützen. Wenn Sie ein Kennwort angeben, kann der Benutzer das startbare Medium nur nach Eingabe dieses Kennworts verwenden.  

        > [!IMPORTANT]  
        >  Aus Sicherheitsgründen wird empfohlen, zum Schutz startbarer Medien immer ein Kennwort zuzuweisen.  

    -   Wählen Sie für die HTTP-Kommunikation die Option **Selbstsigniertes Medienzertifikat erstellen**aus, und geben Sie dann das Start- und Ablaufdatum des Zertifikats an.  

    -   Wählen Sie für die HTTPS-Kommunikation **PKI-Zertifikat importieren**aus, und geben Sie dann das zu importierende Zertifikat und das zugehörige Kennwort an.  

         Weitere Informationen zu diesem für Startimages verwendeten Clientzertifikat finden Sie unter [PKI certificate requirements (PKI-Zertifikatanforderungen)](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Affinität zwischen Benutzer und Gerät**: Geben Sie an, wie die Zuordnung von Benutzern zum Zielcomputer durch das Medium erfolgen soll, um die benutzerzentrierte Verwaltung in Configuration Manager zu unterstützen. Weitere Informationen dazu, wie die Affinität zwischen Benutzer und Gerät durch die Bereitstellung von Betriebssystemen unterstützt wird, finden Sie unter [Associate users with a destination computer (Zuordnen von Benutzern zu einem Zielcomputer)](../get-started/associate-users-with-a-destination-computer.md).  

        -   Geben Sie **Affinität zwischen Benutzer und Gerät mit automatischer Genehmigung zulassen** an, wenn die Zuordnung von Benutzern zum Zielcomputer durch das Medium automatisch erfolgen soll. Diese Funktionalität basiert auf den Aktionen der Tasksequenz, von der das Betriebssystem bereitgestellt wird. In diesem Fall wird von der Tasksequenz während der Bereitstellung des Betriebssystems an den Zielcomputer eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt.  

        -   Geben Sie **Affinität zwischen Benutzer und Gerät mit ausstehender Genehmigung durch den Administrator zulassen** an, wenn die Zuordnung von Benutzern zum Zielcomputer durch das Medium nach einer entsprechenden Genehmigung erfolgen soll. Diese Funktionalität basiert auf dem Geltungsbereich der Tasksequenz, von der das Betriebssystem bereitgestellt wird.  In diesem Fall wird von der Tasksequenz eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt. Es wird jedoch auf die Genehmigung durch den Administrator gewartet, bevor das Betriebssystem bereitgestellt wird.  

        -   Geben Sie **Affinität zwischen Benutzer und Gerät nicht zulassen** an, wenn keine Zuordnung von Benutzern zum Zielcomputer durch das Medium erfolgen soll. In diesem Fall wird während der Bereitstellung des Betriebssystems keine Beziehung zwischen Benutzern und dem Zielcomputer erstellt.  

8.  Geben Sie auf der Seite **Startabbild** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    > [!IMPORTANT]  
    >  Die Architektur des verteilten Startabbilds muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.  

    -   Geben Sie im Feld **Startabbild** das Startabbild zum Starten des Zielcomputers an.  

    -   Geben Sie im Feld **Verteilungspunkt** den Verteilungspunkt an, auf dem das Startabbild sich befindet. Das Startabbild wird von dem Assistenten vom Verteilungspunkt abgerufen und auf das Medium geschrieben.  

        > [!NOTE]  
        >  Sie benötigen ****  Lesezugriffsrechte für die Inhaltsbibliothek am Verteilungspunkt.  

    -   Wenn Sie auf der Seite **Medienverwaltung** des Assistenten standortbasierte startbare Medien erstellen, geben Sie im Feld **Verwaltungspunkt** einen Verwaltungspunkt eines primären Standorts an.  

    -   Wenn Sie auf der Seite **Medienverwaltung** des Assistenten dynamische startbare Medien erstellen, geben Sie die zu verwendenden Verwaltungspunkte des primären Standorts sowie eine Prioritätsreihenfolge für die erste Kommunikation im Feld **Zugehörige Verwaltungspunkte**an.  

9. Geben Sie auf der Seite **Anpassung** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie die Variablen an, die von der Tasksequenz zur Bereitstellung des Betriebssystems verwendet werden.  

    -   Geben Sie alle Prestart-Befehle an, die Sie vor der Tasksequenz ausführen möchten. Bei Prestart-Befehlen handelt es sich um eine Skriptdatei oder ausführbare Datei, über die eine Interaktion mit dem Benutzer in Windows PE möglich ist, bevor die Tasksequenz zur Installation des Betriebssystems ausgeführt wird. Weitere Informationen finden Sie unter [Prestart-Befehle für Tasksequenzmedien](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Während der Erstellung der Tasksequenzmedien werden die Paket-ID und die Prestart-Befehlszeile einschließlich des Wertes vorhandener Tasksequenzvariablen von der Tasksequenz in die Protokolldatei „CreateTSMedia.log“ auf dem Computer geschrieben, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können diese Protokolldatei überprüfen, um den Wert für die Tasksequenzvariablen zu überprüfen.  

         Aktivieren Sie optional das Kontrollkästchen **Dateien für den Prestart-Befehl einbeziehen** , um alle für den Prestart-Befehl erforderlichen Dateien einzubeziehen.  

10. Schließen Sie den Assistenten ab.  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>Erstellen startbarer Medien auf einem USB-Laufwerk über eine Netzwerkfreigabe
Die Informationen in diesem Abschnitt unterstützen Sie beim Erstellen startbarer Medien auf einem USB-Speicherstick, wenn der Speicherstick nicht mit dem Computer verbunden ist, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können zum Erstellen startbarer Medien auf dem USB-Laufwerk Tasksequenz-Bootmedien erstellen, die das ISO-Image bereitstellen, und die Dateien aus dem ISO-Image in das USB-Laufwerk verschieben.

1. [Create the task sequence boot media (Erstellen der Tasksquenz-Bootmedien)](#to-create-task-boobable-media). Wählen Sie auf der Seite **Medientyp** **CD/DVD-Satz** aus. Die Ausgabedateien werden vom Assistenten an den Speicherort geschrieben, den Sie angeben. Beispiel: **\\\Servername\Ordner\Ausgabedatei.iso**.  
2. Bereiten Sie den USB-Wechseldatenträger vor. Der Datenträger muss formatiert, leer und startbar sein.
3. Stellen Sie die ISO-Datei aus dem freigegebenen Speicherort bereit, und übertragen Sie die Dateien aus der ISO-Datei in das USB-Laufwerk.

## <a name="next-steps"></a>Nächste Schritte  
[Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  
