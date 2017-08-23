---
title: Erstellen von vorab bereitgestellten Medien mit System Center Configuration Manager | Microsoft-Dokumentation
description: Erstellen Sie zur Vereinfachung der Bereitstellung von Windows in verschiedenen Szenarios in System Center Configuration Manager vorab bereitgestellte Medien.
ms.custom: na
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 33abf3853d912d423e427db4d35fb4a16167164e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-prestaged-media-with-system-center-configuration-manager"></a>Erstellen von vorab bereitgestellten Medien mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei System Center Configuration Manager handelt es sich bei vorab bereitgestellten Medien um eine WIM-Datei (Windows Imaging Format), die vom Hersteller auf einem Computer ohne Betriebssystem oder im Staging Center eines Unternehmens ohne Verbindung zur Configuration Manager-Umgebung installiert werden kann.  
Vorab bereitgestellte Medien enthalten das Startabbild, mit dem der Zielcomputer gestartet wird, und das Betriebssystemabbild, das auf den Zielcomputer angewendet wird. Sie können auch Anwendungen, Pakete und Treiberpakete als Teil der vorab bereitgestellten Medien angeben. Die Tasksequenz zur Bereitstellung des Betriebssystems ist nicht in den Medien enthalten. Vorab bereitgestellte Medien werden auf die Festplatte eines neuen Computers angewendet, bevor dieser an den Endbenutzer ausgeliefert wird. Verwenden Sie vorab bereitgestellte Medien bei folgenden Szenarien für die Betriebssystembereitstellung:  

-   [Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Bereitstellen von Windows To Go](deploy-windows-to-go.md)  

 Wenn der Computer nach der Anwendung der vorab bereitgestellte Medien zum ersten Mal gestartet wird, wird er mit Windows PE gestartet und stellt eine Verbindung zu einem Verwaltungspunkt her. Dort wird nach der Tasksequenz gesucht, mit der Vorgang der Bereitstellung des Betriebssystems abgeschlossen wird. Sie können Anwendungen, Pakete und Treiberpakete als Teil der vorab bereitgestellten Medien angeben. Beim Bereitstellen einer Tasksequenz mit Verwendung von vorab bereitgestellten Medien wird der lokale Tasksequenzcache vom Assistenten zuerst auf gültige Inhalte geprüft. Falls keine Inhalte gefunden werden oder falls diese geändert wurden, werden die Inhalte vom Assistenten vom Verteilungspunkt heruntergeladen.  

##  <a name="BKMK_CreatePrestagedMedia"></a> Erstellen vorab bereitgestellter Medien  
 Bevor Sie vorab bereitgestellte Medien mithilfe des Assistenten zum Erstellen von Tasksequenzmedien erstellen, achten Sie darauf, dass alle folgenden  Bedingungen erfüllt sind:  

|Aufgabe|Beschreibung|  
|----------|-----------------|  
|Startabbild|Beachten Sie die folgenden Informationen zum Startabbild, das Sie in der Tasksequenz zum Bereitstellen des Betriebssystems verwenden:<br /><br /> - Die Architektur des Startimages muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.<br />- Achten Sie darauf, dass das Startimage die zur Bereitstellung des Zielcomputers erforderlichen Netzwerk- und Massenspeichertreiber enthält.|  
|Erstellen einer Tasksequenz zum Bereitstellen eines Betriebssystems|Als Teil der vorab bereitgestellten Medien müssen Sie die Tasksequenz zum Bereitstellen des Betriebssystems angeben.<br /><br /> - Die Schritte zum Erstellen einer neuen Tasksequenz finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems in System Center Configuration Manager](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md).<br />- Weitere Informationen zu Tasksequenzen finden Sie unter [Manage task sequences to automate tasks (Verwalten von Tasksequenzen)](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).|  
|Verteilen aller der Tasksequenz zugeordneten Inhalte|Sie müssen alle für die Tasksequenz erforderlichen Inhalte auf mindestens einen Verteilungspunkt verteilen. Dies schließt das Startabbild, Betriebssystemabbild und andere zugehörige Dateien ein. Die Informationen werden vom Assistenten beim Erstellen des eigenständigen Mediums vom Verteilungspunkt abgerufen. Sie benötigen **Lesezugriffsrechte** für die Inhaltsbibliothek an diesem Verteilungspunkt.  Weitere Informationen finden Sie unter [About the content library (Informationen zur Inhaltsbibliothek)](../../core/plan-design/hierarchy/the-content-library.md).|  
|Festplatte auf dem Zielcomputer|Die Festplatte des Zielcomputers muss formatiert werden, bevor das vorab bereitgestellte Medium auf der Festplatte des Computers bereitgestellt wird. Wenn die Festplatte bei der Anwendung des Mediums nicht formatiert ist und von der Tasksequenz zur Betriebssystembereitstellung versucht wird, den Zielcomputer zu starten, tritt in der Tasksequenz ein Fehler auf.|  

> [!NOTE]  
>  Der Assistent zum Erstellen von Tasksequenzvariablen legt die folgende medienbezogene Bedingung für Tasksequenzvariablen fest: **_SMSTSMediaType = OEMMedia**. Sie können diese Bedingung in der Tasksequenz verwenden.  

 Gehen Sie wie folgt vor, um vorab bereitgestellte Medien zu erstellen.  

#### <a name="to-create-prestaged-media"></a>So erstellen Sie vorab bereitgestellte Medien  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenzmedien erstellen** , um den Assistenten zum Erstellen von Tasksequenzmedien zu starten.  

4.  Geben Sie auf der Seite **Medientyp wählen** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   Wählen Sie **Vorab bereitgestellte Medien**aus.  

    -   Optional können Sie **Unbeaufsichtigte Betriebssystembereitstellung zulassen**auswählen, wenn Sie die Bereitstellung des Betriebssystems ohne Benutzereingabe gestatten möchten. Wenn Sie diese Option auswählen, wird der Benutzer nicht aufgefordert, Informationen zur Netzwerkkonfiguration oder optionale Tasksequenzen anzugeben. Allerdings wird der Benutzer weiterhin zur Eingabe eines Kennworts aufgefordert, wenn die Medien für den Kennwortschutz konfiguriert sind.  

5.  Geben Sie auf der Seite **Medienverwaltung** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   Wählen Sie **Dynamisches Medium** aus, wenn Sie zulassen möchten, dass das Medium ausgehend vom Clientstandort innerhalb der Standortgrenzen von einem Verwaltungspunkt an einen anderen Verwaltungspunkt umgeleitet wird.  

    -   Wählen Sie **Standortbasiertes Medium** aus, wenn Sie wünschen, dass von dem Medium nur mit dem angegebenen Verwaltungspunkt Kontakt aufgenommen wird.  

6.  Geben Sie auf der Seite **Medieneigenschaften**  die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   **Erstellt von**: Geben Sie an, von wem das Medium erstellt wurde.  

    -   **Version**: Geben Sie die Versionsnummer des Mediums an.  

    -   **Kommentar**: Geben Sie eine eindeutige Beschreibung des Verwendungszwecks des Mediums an.  

    -   **Mediendatei**: Geben Sie den Namen und Pfad der Ausgabedateien an. Die Ausgabedateien werden vom Assistenten an diesen Speicherort geschrieben. Beispiel: **\\\Servername\Ordner\Ausgabedatei.wim**  

7.  Geben Sie auf der Seite **Sicherheit** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   Aktivieren Sie das Kontrollkästchen **Unterstützung für unbekannte Computer aktivieren**, um zuzulassen, dass von dem Medium ein Betriebssystem auf einem nicht von Configuration Manager verwalteten Computer bereitgestellt wird. Für diese Computer gibt es in der Configuration Manager-Datenbank keine Einträge.  Weitere Informationen finden Sie unter [Prepare for unknown computer deployments (Vorbereiten auf Bereitstellungen für unbekannte Computer)](../get-started/prepare-for-unknown-computer-deployments.md).  

    -   Aktivieren Sie das Kontrollkästchen **Medien durch Kennwort schützen** , und geben Sie ein sicheres Kennwort ein, um das Medium vor dem Zugriff Unbefugter zu schützen. Wenn Sie ein Kennwort angeben, kann der Benutzer das vorab bereitgestellte Medium nur nach Eingabe dieses Kennworts verwenden.  

        > [!IMPORTANT]  
        >  Aus Sicherheitsgründen wird empfohlen, zum Schutz vorab bereitgestellter Medien immer ein Kennwort zuzuweisen.  

    -   Wählen Sie für die HTTP-Kommunikation die Option **Selbstsigniertes Medienzertifikat erstellen**aus, und geben Sie dann das Start- und Ablaufdatum des Zertifikats an.  

    -   Wählen Sie für die HTTPS-Kommunikation **PKI-Zertifikat importieren**aus, und geben Sie dann das zu importierende Zertifikat und das zugehörige Kennwort an.  

         Weitere Informationen zu diesem für Startimages verwendeten Clientzertifikat finden Sie unter [PKI certificate requirements (PKI-Zertifikatanforderungen)](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Affinität zwischen Benutzer und Gerät**: Geben Sie an, wie die Zuordnung von Benutzern zum Zielcomputer durch das Medium erfolgen soll, um die benutzerzentrierte Verwaltung in Configuration Manager zu unterstützen. Weitere Informationen dazu, wie die Affinität zwischen Benutzer und Gerät durch die Bereitstellung von Betriebssystemen unterstützt wird, finden Sie unter [Associate users with a destination computer (Zuordnen von Benutzern zu einem Zielcomputer)](../get-started/associate-users-with-a-destination-computer.md).  

        -   Geben Sie **Affinität zwischen Benutzer und Gerät mit automatischer Genehmigung zulassen** an, wenn die Zuordnung von Benutzern zum Zielcomputer durch das Medium automatisch erfolgen soll. Diese Funktionalität basiert auf den Aktionen der Tasksequenz, von der das Betriebssystem bereitgestellt wird. In diesem Fall wird von der Tasksequenz während der Bereitstellung des Betriebssystems an den Zielcomputer eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt.  

        -   Geben Sie **Affinität zwischen Benutzer und Gerät mit ausstehender Genehmigung durch den Administrator zulassen** an, wenn die Zuordnung von Benutzern zum Zielcomputer durch das Medium nach einer entsprechenden Genehmigung erfolgen soll. Diese Funktionalität basiert auf dem Geltungsbereich der Tasksequenz, von der das Betriebssystem bereitgestellt wird. In diesem Fall wird von der Tasksequenz eine Beziehung zwischen den angegebenen Benutzern und dem Zielcomputer erstellt. Es wird jedoch auf die Genehmigung durch den Administrator gewartet, bevor das Betriebssystem bereitgestellt wird.  

        -   Geben Sie **Affinität zwischen Benutzer und Gerät nicht zulassen** an, wenn keine Zuordnung von Benutzern zum Zielcomputer durch das Medium erfolgen soll. In diesem Fall wird während der Bereitstellung des Betriebssystems keine Beziehung zwischen Benutzern und dem Zielcomputer erstellt.  

8.  Geben Sie auf der Seite **Tasksequenz** die Tasksequenz an, die auf dem Zielcomputer ausgeführt wird. Der Inhalt, auf den die Tasksequenz verweist, wird im Fenster **Diese Tasksequenz verweist auf den folgenden Inhalt**angezeigt. Überprüfen Sie den Inhalt, und klicken Sie dann auf **Weiter**.  

9. Geben Sie auf der Seite **Startabbild** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    > [!IMPORTANT]  
    >  Die Architektur des verteilten Startabbilds muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.  

    -   Geben Sie im Feld **Startabbild** das Startabbild zum Starten des Zielcomputers an. Weitere Informationen finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

    -   Geben Sie im Feld **Verteilungspunkt** den Verteilungspunkt an, auf dem das Startabbild sich befindet. Das Startabbild wird von dem Assistenten vom Verteilungspunkt abgerufen und auf das Medium geschrieben.  

        > [!NOTE]  
        >  Sie benötigen **Lesezugriffsrechte** für die Inhaltsbibliothek am Verteilungspunkt. Weitere Informationen finden Sie unter [Informationen zur Inhaltsbibliothek](../../core/plan-design/hierarchy/the-content-library.md).  

    -   Wenn Sie auf der Seite **Medienverwaltung** des Assistenten die Option **Standortbasiertes Medium** ausgewählt haben, müssen Sie im Feld **Verwaltungspunkt** einen Verwaltungspunkt eines primären Standorts angeben.  

    -   Wenn Sie auf der Seite **Medienverwaltung** des Assistenten die Option **Dynamisches Medium** ausgewählt haben, müssen Sie im Feld **Zugehörige Verwaltungspunkte** die zu verwendenden Verwaltungspunkte des primären Standorts sowie eine Prioritätsreihenfolge für die erste Kommunikation angeben.  

10. Geben Sie auf der Seite **Abbilder** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie im Dialogfeld **Imagepaket** das Betriebssystemimage an. Weitere Informationen finden Sie unter [Manage operating system images (Verwalten von Betriebssystemimages)](../get-started/manage-operating-system-images.md).  

    -   Wenn das Paket mehrere Betriebssystemabbilder enthält, geben Sie im Dialogfeld **Abbildindex** das bereitzustellende Abbild an.  

    -   Geben Sie im Feld **Verteilungspunkt** den Verteilungspunkt an, auf dem das Paket mit dem Betriebssystemabbild sich befindet. Das Betriebssystemabbild wird von dem Assistenten vom Verteilungspunkt abgerufen und auf das Medium geschrieben.  

11. Geben Sie auf der Seite **Anpassung** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie die Variablen an, die von der Tasksequenz zur Bereitstellung des Betriebssystems verwendet werden.  

    -   Geben Sie alle Prestart-Befehle an, die Sie vor der Tasksequenz ausführen möchten. Bei Prestart-Befehlen handelt es sich um eine Skriptdatei oder ausführbare Datei, über die eine Interaktion mit dem Benutzer in Windows PE möglich ist, bevor die Tasksequenz zur Installation des Betriebssystems ausgeführt wird. Weitere Informationen zu Prestart-Befehlen für Medien finden Sie unter [Prestart-Befehle für Tasksequenzmedien](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Während der Erstellung der Tasksequenzmedien werden die Paket-ID und die Prestart-Befehlszeile einschließlich des Wertes vorhandener Tasksequenzvariablen von der Tasksequenz in die Protokolldatei „CreateTSMedia.log“ auf dem Computer geschrieben, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können diese Protokolldatei überprüfen, um den Wert für die Tasksequenzvariablen zu überprüfen.  

12. Schließen Sie den Assistenten ab.  

## <a name="next-steps"></a>Nächste Schritte
[Szenarien für die Bereitstellung von Unternehmensbetriebssystemen](scenarios-to-deploy-enterprise-operating-systems.md)
