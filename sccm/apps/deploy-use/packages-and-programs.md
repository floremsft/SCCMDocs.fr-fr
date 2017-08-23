---
title: Pakete und Programme | Microsoft-Dokumentation
description: "Unterstützung von Bereitstellungen, die Pakete und Programme oder Anwendungen mit System Center Configuration Manager verwenden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6146bcf4e5aa9df6fe0b8cf71898e488ecf217cc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Pakete und Programme in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager unterstützt weiterhin Pakete und Programme, die in Configuration Manager 2007 verwendet wurden. Eine Bereitstellung mit Paketen und Programmen kann beim Bereitstellen der folgenden Objekte besser geeignet sein als eine Bereitstellung, die eine Anwendung verwendet:  

- Anwendungen auf Linux- und UNIX-Servern
- Skripts, mit denen keine Anwendungen auf einem Computer installiert werden, z. B. ein Skript zum Defragmentieren der Computerfestplatte
- „Einmal-Skripts“, die nicht ständig überwacht werden müssen  
- Skripts, die mit regelmäßiger Wiederholung ausgeführt werden und keine globale Auswertung verwenden können

Wenn Sie Pakete von einer früheren Version von Configuration Manager migrieren, können Sie diese in der Configuration Manager-Hierarchie bereitstellen. Nach dem Abschluss der Migration werden die Pakete im Arbeitsbereich **Softwarebibliothek** im Knoten **Pakete** angezeigt.

Sie können diese Pakete genauso ändern und bereitstellen wie bei der Verwendung der Softwareverteilung. In Configuration Manager ist auch weiterhin der **Assistent zum Importieren eines Pakets aus einer Definition** enthalten, um Legacypakete zu importieren. Ankündigungen werden in Bereitstellungen konvertiert, wenn sie von Configuration Manager 2007 zu einer Configuration Manager-Hierarchie migriert werden.  

> [!NOTE]  
>  Sie können Microsoft System Center Configuration Manager Package Conversion Manager verwenden, um Pakete und Programme in System Center Configuration Manager-Anwendungen zu konvertieren.  
>   
>  Weitere Informationen finden Sie unter [Configuration Manager Package Conversion Manager](https://technet.microsoft.com/library/hh531519.aspx).  

In Paketen können einige neue Features von Configuration Manager verwendet werden, darunter Verteilungspunktgruppen und die Überwachungsfunktion. Microsoft Application Virtualization (App-V)-Anwendungen können nicht mithilfe von Paketen und Programmen in Configuration Manager verteilt werden. Zum Verteilen virtueller Anwendungen müssen diese als Configuration Manager-Anwendungen erstellt werden.  

##  <a name="create-a-package-and-program"></a>Erstellen eines Pakets und Programms  
 Verwenden Sie eines der folgenden Verfahren, wenn Sie Pakete und Programme erstellen oder importieren möchten.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Erstellen Sie mithilfe des Assistenten zum Erstellen von Paketen und Programmen ein Paket und Programm.  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Pakete** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Paket erstellen** aus.  

4.  Auf der **Paket** auf der Seite der **Erstellen eines Pakets und Programms Assistenten**, geben Sie die folgende Informationen:  

    -   **Name**: Geben Sie einen Paketnamen mit maximal 50 Zeichen an.  

    -   **Beschreibung**: Geben Sie eine Paketbeschreibung mit maximal 128 Zeichen an.  

    -   **Hersteller** (optional): Geben Sie einen Herstellernamen an, um das Paket in der Configuration Manager-Konsole besser identifizieren zu können. Der Name darf maximal 32 Zeichen umfassen.

    -   **Sprache** (optional): Geben Sie die Sprachversion des Pakets mit maximal 32 Zeichen an.  

    -   **Version** (optional): Geben Sie eine Versionsnummer für das Paket mit maximal 32 Zeichen an.

    -   **Dieses Paket enthält Quelldateien**: Diese Einstellung gibt an, ob für das Paket Quelldateien auf Clientgeräten vorhanden sein müssen. Dieses Kontrollkästchen ist standardmäßig deaktiviert, und von Configuration Manager werden keine Verteilungspunkte für das Paket verwendet. Wenn dieses Kontrollkästchen aktiviert ist, werden Verteilungspunkte verwendet.  

    -   **Quellordner**: Wenn das Paket Quelldateien enthält, wählen Sie **Durchsuchen** aus, um das Dialogfeld **Quellordner festlegen** zu öffnen und anschließend den Quelldateipfad für das Paket anzugeben.  

        > [!NOTE]  
        >  Das Computerkonto des Standortservers muss über Lesezugriffsberechtigungen für den angegebenen Quellordner verfügen.  

5.  Wählen Sie auf der Seite **Programmtyp** im **Assistent zum Erstellen von Paketen und Programmen** den Typ des zu erstellenden Programms aus, und wählen Sie dann **Weiter** aus. Sie können ein Programm für einen Computer oder für ein Gerät erstellen oder diesen Schritt überspringen und später ein Programm erstellen.  

    > [!TIP]  
    >  Um ein neues Programm für ein vorhandenes Paket zu erstellen, müssen Sie zuerst das Paket auswählen. Wählen Sie dann auf der Registerkarte **Startseite** in der Gruppe **Paket** die Option **Programm erstellen** aus, um den **Assistenten zum Erstellen einer Anwendung** zu öffnen.  

6.  Wenden Sie eines der folgenden Verfahren an, um ein Standardprogramm oder ein Geräteprogramm zu erstellen.  

    #### <a name="create-a-standard-program"></a>Erstellen eines Standardprogramms  

  1.  Wählen Sie auf der Seite **Programmtyp** im **Assistent zum Erstellen von Paketen und Programmen** die Option **Standardprogramm** und danach die Option **Weiter** aus.     

    2.  Geben Sie auf der Seite **Standardprogramm** folgende Informationen an:  

        -   **Name:** Geben Sie einen Namen für das Programm mit maximal 50 Zeichen.  

            > [!NOTE]  
            >  Programmnamen müssen innerhalb eines Pakets eindeutig sein. Nachdem Sie ein Programm erstellt haben, können Sie seinen Namen nicht mehr ändern.  

        -   **Befehlszeile**: Geben Sie die Befehlszeile zum Starten dieses Programms ein, oder wählen Sie **Durchsuchen** aus, um nach dem Speicherort der Datei zu suchen.  

            Wenn für den Dateinamen keine Erweiterung angegeben wurde, werden von Configuration Manager „.com“, „.exe“ und „.bat“ als mögliche Erweiterungen verwendet.  

             Wird das Programm auf einem Client ausgeführt, wird in Configuration Manager zunächst im Paket nach dem Dateinamen aus der Befehlszeile gesucht, dann im lokalen Windows-Ordner und schließlich in den über die lokale Umgebungsvariable *%path%* konfigurierten Pfaden. Wird die Datei nicht gefunden, kann das Programm nicht ausgeführt werden.  

        -   **Startordner** (optional): Geben Sie den Ordner an, von dem aus das Programm ausgeführt wird (maximal 127 Zeichen). Dieser Ordner kann als absoluter Pfad auf dem Client oder relativ zu dem Verteilungspunktordner angegeben werden, in dem das Paket enthalten ist.

        -   **Ausführen**: Geben Sie den Modus an, in dem das Programm auf Clientcomputern ausgeführt wird. Wählen Sie eine der folgenden Einstellungen aus:  

            -   **Normal**: Das Programm wird basierend auf den Standardeinstellungen des Systems und des Programms im normalen Modus ausgeführt. Dies ist der Standardmodus.  

            -   **Minimiert**: Das Programm wird auf Clientgeräten minimiert ausgeführt. Benutzer können Installationsaktivitäten möglicherweise im Infobereich oder in der Taskleiste sehen.  

            -   **Maximiert**: Das Programm wird auf Clientgeräten maximiert ausgeführt. Benutzer sehen alle Installationsaktivitäten.  

            -   **Ausgeblendet**: Die Anwendung wird auf Clientgeräten im Hintergrund ausgeführt. Benutzer sehen keine Installationsaktivitäten.  

        -   **Programm kann ausgeführt werden**: Geben Sie an, ob das Programm nur ausgeführt werden kann, wenn ein Benutzer beim Clientcomputer angemeldet ist, wenn kein Benutzer angemeldet ist, oder ob die Ausführung in beiden Fällen möglich sein soll.  

        -   **Ausführmodus**: Geben Sie an, ob das Programm mit den Administratorberechtigungen oder den Berechtigungen des angemeldeten Benutzers ausgeführt werden soll.  

        -   **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren**: Verwenden Sie diese Einstellung, falls verfügbar, um anzugeben, ob der Benutzer mit der Programminstallation interagieren darf. Dieses Kontrollkästchen steht nur zur Verfügung, wenn für **Programm kann ausgeführt werden** die Option **Nur wenn kein Benutzer angemeldet ist** oder **Unabhängig von Benutzeranmeldung** und für **Ausführmodus** die Option **Mit Administratorrechten ausführen** ausgewählt ist.  

        -   **Laufwerkmodus**: Geben Sie hier Informationen zur Ausführung des Programms im Netzwerk an. Wählen Sie eine der folgenden Optionen aus:  

            -   **Unterstützt UNC-Namen**: Geben Sie hier an, dass das Programm mit einem UNC-Namen (Universal Naming Convention) ausgeführt wird. Dies ist die Standardeinstellung.  

            -   **Erfordert Laufwerkbuchstaben**: Geben Sie hier an, dass das Programm zur vollständigen Kennzeichnung seines Speicherortes einen Laufwerkbuchstaben erfordert. Für diese Einstellung kann von Configuration Manager jeder verfügbare Laufwerkbuchstabe auf dem Client verwendet werden.  

            -   **Erfordert einen bestimmten Laufwerkbuchstaben**: Geben Sie hier an, dass das Programm einen bestimmten von Ihnen angegebenen Laufwerkbuchstaben erfordert, um seinen Speicherort vollständig zu kennzeichnen (beispielsweise **Z:**). Falls der angegebene Laufwerkbuchstabe auf einem Client bereits verwendet wird, kann das Programm nicht ausgeführt werden.  

        -   **Verteilungspunkt beim Anmelden wiederherstellen auf**: Verwenden Sie dieses Kontrollkästchen, um anzugeben, ob der Clientcomputer erneut eine Verbindung zum Verteilungspunkt herstellt, wenn sich der Benutzer anmeldet. Standardmäßig ist dieses Kontrollkästchen deaktiviert.  

  3.  Geben Sie im **Assistent zum Erstellen von Paketen und Programmen** auf der Seite **Anforderungen** die folgenden Informationen an:  

        -   **Ein anderes Programm zuerst ausführen**: Verwenden Sie diese Einstellung, um ein Paket und Programm anzugeben, das vor diesem Paket und Programm ausgeführt werden soll.  

        -   **Plattformanforderungen**: Wählen Sie die Option **Dieses Programm kann auf jeder Plattform ausgeführt werden** oder **Dieses Programm kann nur auf bestimmten Plattformen ausgeführt werden** aus, und wählen Sie dann das Betriebssystem aus, das auf Clients ausgeführt werden muss, um das Paket und Programm installieren zu können.  

        -   **Geschätzter Speicherplatz**: Geben Sie hier den Speicherplatz an, der zur Ausführung des Softwareprogramms auf dem Computer erforderlich ist. Er kann als **Unknown** (die Standardeinstellung) oder als eine ganze Zahl größer oder gleich Null angegeben werden. Wenn ein Wert angegeben ist, müssen auch Einheiten für diesen Wert angegeben werden.  

        -   **Maximal zulässige Laufzeit (Minuten)**: Hiermit wird die maximal zulässige Zeit für die Ausführung des Programms auf dem Clientcomputer angegeben. Er kann als **Unknown** (die Standardeinstellung) oder als eine ganze Zahl größer Null angegeben werden.  

             Standardmäßig ist dieser Wert auf 120 Minuten festgelegt.  

            > [!IMPORTANT]  
            >  Wenn Sie bei der Sammlung, für die dieses Programm ausgeführt wird, Wartungsfenster verwenden, kann ein Konflikt auftreten, wenn die **Maximal zulässige Laufzeit** länger ist als das geplante Wartungsfenster. Wenn die maximal zulässige Laufzeit jedoch auf **Unbekannt** festgelegt ist, wird das Programm gestartet und während des Wartungsfensters und nach dessen Schließen so lange wie nötig ausgeführt. Wenn der Benutzer die maximal zulässige Laufzeit auf einen bestimmten Zeitraum festlegt, der die Länge des verfügbaren Wartungsfensters überschreitet, wird das Programm nicht ausgeführt.  

             Wenn der Wert auf **Unbekannt** festgelegt ist, legt Configuration Manager für die maximal zulässige Laufzeit 12 Stunden (720 Minuten) fest.  

            > [!NOTE]  
            >  Wenn die (vom Benutzer festgelegte oder als Standardwert verwendete) maximal zulässige Laufzeit überschritten wird, wird das Programm von Configuration Manager beendet, sofern die Einstellung **Mit Administratorrechten ausführen** aktiviert und die Einstellung **Benutzern erlauben, die Programminstallation anzuzeigen und mit ihr zu interagieren** deaktiviert ist.  

  4.  Wählen Sie **Weiter** aus.  

    #### <a name="create-a-device-program"></a>Erstellen eines Geräteprogramms  

  1.  Wählen Sie auf der Seite **Programmtyp** im **Assistent zum Erstellen von Paketen und Programmen** die Option **Programm für Gerät** aus, und wählen Sie dann **Weiter** aus.  

  2.  Geben Sie auf der Seite **Programm für Gerät** Folgendes an:  

        -   **Name**: Geben Sie einen Namen für das Programm an (maximal 50 Zeichen).  

            > [!NOTE]  
            >  Programmnamen müssen innerhalb eines Pakets eindeutig sein. Nachdem Sie ein Programm erstellt haben, können Sie seinen Namen nicht mehr ändern.  

        -   **Kommentar** (optional): Geben Sie einen Kommentar für dieses Geräteprogramm an (maximal 127 Zeichen).  

        -   **Downloadordner**: Geben Sie den Namen des Ordners auf dem Windows CE-Gerät an, in dem die Paketquelldateien gespeichert werden sollen. Der Standardwert ist **\Temp\\**.  

        -   **Befehlszeile**: Geben Sie die Befehlszeile zum Starten dieses Programms ein, oder wählen Sie **Durchsuchen** aus, um nach dem Speicherort der Datei zu suchen.  

        -   **Befehlszeile im Downloadordner ausführen**: Bei Auswahl dieser Option wird das Programm aus dem zuvor angegebenen Downloadordner ausgeführt.  

        -   **Befehlszeile von diesem Ordner ausführen**: Bei Auswahl dieser Option können Sie einen anderen Ordner angeben, von dem aus das Programm ausgeführt wird.  

    3.  Geben Sie auf der Seite **Anforderungen** Folgendes an:  

        -   **Geschätzter Speicherplatz**: Geben Sie die Menge des Speicherplatzes an, der für die Software erforderlich ist. Dieser Wert wird Benutzern von mobilen Geräten vor der Installation des Programms angezeigt.  

        -   **Programm herunterladen**: Geben Sie Informationen dazu an, wann dieses Programm auf mobile Geräte heruntergeladen werden kann. Zur Auswahl stehen die Optionen **So bald wie möglich**, **Nur über ein schnelles Netzwerk**oder **Nur, wenn das Gerät in der Dockingstation ist**.  

        -   **Zusätzliche Anforderungen**: Geben Sie ggf. zusätzliche Anforderungen für dieses Programm an. Diese werden dem Benutzer angezeigt, bevor er die Software installiert. Sie können z. B. die Benutzer benachrichtigen, die sie benötigen, um alle anderen Programme schließen, bevor Sie das Programm ausführen.  

  4.  Wählen Sie **Weiter** aus.  

  7.  Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die auszuführenden Aktionen, und schließen Sie anschließend den Assistenten ab.  

 Das neue Paket und das neue Programm werden im Arbeitsbereich **Softwarebibliothek** im Knoten **Pakete** angezeigt.  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Erstellen von Paketen und Programmen aus Paketdefinitionsdateien  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Pakete** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Paket aus Definition erstellen** aus.  

4.  Wählen Sie auf der Seite **Paketdefinition** im **Assistent zum Erstellen von Paketen und Programmen** eine vorhandene Paketdefinitionsdatei aus, oder wählen Sie **Durchsuchen** aus, um eine neue Paketdefinitionsdatei zu öffnen. Nachdem Sie eine neue Paketdefinitionsdatei angegeben haben, wählen Sie sie in der Liste **Paketdefinition** aus. Wählen Sie dann **Weiter** aus.  

5.  Geben Sie auf der Seite **Quelldateien** Informationen zu ggf. erforderlichen Quelldateien für das Paket und Programm an, und wählen Sie **Weiter** aus.  

6.  Wenn für das Paket Quelldateien erforderlich sind, geben Sie auf der Seite **Quellordner** den Speicherort zum Abrufen der Quelldateien an, und wählen Sie **Weiter** aus.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die auszuführenden Aktionen, und schließen Sie anschließend den Assistenten ab. Das neue Paket und das neue Programm werden im Arbeitsbereich **Softwarebibliothek** im Knoten **Pakete** angezeigt.  

 Weitere Informationen zu Paketdefinitionsdateien finden Sie unter [Informationen zum Format von Paketdefinitionsdateien](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) in diesem Thema.  

##  <a name="deploy-packages-and-programs"></a>Bereitstellen von Paketen und Programmen  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Pakete** aus.  

2.  Wählen Sie das Paket aus, das Sie bereitstellen möchten, und wählen Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** die Option **Bereitstellen** aus.  

3.  Geben Sie auf der Seite **Allgemein** im **Assistent zum Bereitstellen von Software** den Namen des Pakets und des Programms an, das Sie bereitstellen möchten. Geben Sie außerdem die Sammlung, in der Sie das Paket und Programm bereitstellen möchten, sowie optionale Kommentare zur Bereitstellung an.  

     Wählen Sie **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind** aus, wenn der Paketinhalt in der Standardverteilungspunktgruppe der Sammlung gespeichert werden soll. Wenn die ausgewählte Sammlung keiner Verteilungspunktgruppe zugeordnet ist, ist diese Option nicht verfügbar.  

4.  Wählen Sie auf der Seite **Inhalt** die Option **Hinzufügen** aus, und wählen Sie anschließend die Verteilungspunkte oder Verteilungspunktgruppen aus, auf denen der diesem Paket und diesem Programm zugeordnete Inhalt bereitgestellt werden soll.  

5.  Wählen Sie auf der Seite **Bereitstellungseinstellungen** einen Zweck für diese Bereitstellung aus, und geben Sie Optionen für Aktivierungspakete und getaktete Verbindungen an:  

    -   **Zweck**: Nutzen Sie folgende Auswahlmöglichkeiten:  

        -   **Verfügbar**: Wenn die Anwendung für einen Benutzer bereitgestellt wird, werden das veröffentlichte Paket und das Programm im Anwendungskatalog angezeigt, und der Benutzer kann sie bei Bedarf anfordern. Wenn das Paket und das Programm auf einem Gerät bereitgestellt werden, werden sie dem Benutzer im Softwarecenter angezeigt, und der Benutzer kann sie bei Bedarf installieren.  

        -   **Erforderlich**: Das Paket und das Programm werden entsprechend dem konfigurierten Zeitplan automatisch bereitgestellt. Allerdings kann ein Benutzer den Bereitstellungsstatus des Pakets und Programms nachverfolgen und diese vor Ablauf der Frist über das Softwarecenter installieren.  

    -   **Aktivierungspakete senden**: Wenn der Bereitstellungszweck auf **Erforderlich** festgelegt und diese Option ausgewählt wird, wird vor der Installation der Bereitstellung ein Aktivierungspaket an den Computer gesendet, um ihn zum Installationsstichtag aus dem Standbymodus zu aktivieren. Sie können diese Option nur verwenden, wenn Computer für Wake-On-LAN konfiguriert sind.  

    -  **Clients mit einer getakteten Internetverbindung dürfen den Inhalt nach dem Installationsstichtag herunterladen (Zusatzkosten können anfallen)**: Wählen Sie bei Bedarf diese Option aus.  

    > [!NOTE]  
    >  Die Option **Software vorab auf dem primären Gerät des Benutzers bereitstellen** ist nicht verfügbar, wenn Sie ein Paket und ein Programm bereitstellen.  

6.  Konfigurieren Sie auf der Seite **Zeitplanung**, wann dieses Paket und dieses Programm bereitgestellt oder für Clientgeräte verfügbar gemacht werden.  

     Welche Optionen auf dieser Seite verfügbar sind, ist davon abhängig, ob die Bereitstellungsaktion auf **Verfügbar** oder **Erforderlich**gesetzt ist.  

7.  Wenn der Bereitstellungszweck auf **Erforderlich** gesetzt ist, konfigurieren Sie das Verhalten beim erneuten Ausführen des Programms mithilfe des Dropdownmenüs **Verhalten beim erneuten Ausführen**. Wählen Sie aus den folgenden Optionen:  

    |Verhalten beim erneuten Ausführen|Weitere Informationen|  
    |--------------------|----------------------|  
    |Bereitgestelltes Programm nie erneut ausführen|Das Programm wird nicht erneut auf dem Client ausgeführt, selbst wenn das Programm ursprünglich fehlgeschlagen ist oder die Programmdateien geändert wurden.|  
    |Programm immer erneut ausführen|Das Programm wird immer erneut auf dem Client ausgeführt, wenn die Bereitstellung geplant ist, auch wenn das Programm bereits erfolgreich ausgeführt wurde. Dies kann nützlich sein, wenn Sie wiederholte Bereitstellungen verwenden, in denen das Programm, z. B. mit antivirus-Software aktualisiert wird.|  
    |Bei fehlgeschlagenem vorherigen Versuch erneut ausführen|Das Programm wird bei geplanter Bereitstellung nur dann erneut ausgeführt, wenn bei der vorherigen Ausführung ein Fehler aufgetreten ist.|  
    |Bei erfolgreichem vorherigen Versuch erneut ausführen|Das Programm wird nur dann erneut ausgeführt, wenn es zuvor erfolgreich auf dem Client ausgeführt wurde. Dies ist nützlich, wenn sich wiederholende Ankündigungen verwendet werden, in denen das Programm regelmäßig aktualisiert wird und eine erfolgreiche Installation des jeweils vorherigen Updates erforderlich ist.|  

8. Geben Sie auf der Seite **Benutzerfreundlichkeit** die folgenden Informationen an:  

    -   **Benutzern zuweisungsunabhängige Programmausführung erlauben**: Wenn diese Funktion aktiviert ist, können Benutzer diese Software unabhängig von der geplanten Installationszeit aus dem Softwarecenter installieren.  

    -   **Softwareinstallation**: Die Software kann außerhalb konfigurierter Wartungsfenster installiert werden.  

    -   **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist)**: Wenn für den Abschluss der Softwareinstallation ein Geräteneustart erforderlich ist, kann dieser auch außerhalb konfigurierter Wartungsfenster ausgeführt werden.  

    -   **Eingebettete Geräte**: Beim Bereitstellen von Paketen und Programmen für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass die Pakete und Programme auf dem temporären Overlay gespeichert und die Änderungen später ausgeführt werden. Alternativ können Sie die Änderungen auch am Installationsstichtag oder während eines Wartungsfensters bereitstellen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters bereitgestellt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

        > [!NOTE]  
        >  Wenn Sie ein Paket oder ein Programm auf einem Windows Embedded-Gerät bereitstellen, stellen Sie sicher, dass das Gerät Mitglied einer Sammlung mit einem konfigurierten Wartungsfenster. Weitere Informationen zur Verwendung von Wartungsfenstern beim Bereitstellen von Paketen und Programmen auf Windows Embedded-Geräten finden Sie unter [Creating Windows Embedded applications (Erstellen von Windows Embedded-Anwendungen)](../../apps/get-started/creating-windows-embedded-applications.md).  

9. Geben Sie auf der Seite **Verteilungspunkte** die folgenden Informationen an:  

    -   **Bereitstellungsoptionen**: Geben Sie die Aktionen an, die ein Client zum Ausführen von Programminhalten ausführen soll. Sie können Verhalten angeben, wenn der Client in einem schnellen Netzwerk befindet oder eine langsame oder unzuverlässige Netzwerkgrenze befindet.  

    -   **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Wählen Sie diese Option aus, um die Auslastung des Netzwerks zu reduzieren. Sie erlaubt es Clients, Inhalte von anderen Clients im Netzwerk herunterzuladen, die diese Inhalte bereits heruntergeladen und zwischengespeichert haben. Diese Option wird Windows BranchCache und oder höher auf Computern mit Windows Vista SP2 verwendet werden kann.  

    -   **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen**:  

        -  **Versionen vor 1610**: Sie können das Kontrollkästchen **Fallbackquellpfad für Inhalt zulassen** aktivieren, um für Clients außerhalb solcher Begrenzungsgruppen ein Ausweichen auf den Verteilungspunkt als Quellort für Inhalt zu ermöglichen, wenn keine anderen Verteilungspunkte verfügbar sind.

        - **Version 1610 und später**: Sie können **Fallbackquellpfad für Inhalt zulassen** nicht mehr konfigurieren.  Stattdessen können Sie Beziehungen zwischen Begrenzungsgruppen konfigurieren, die festlegen, ab wann ein Client mit der Suche nach zusätzlichen Begrenzungsgruppen für einen gültigen Quellspeicherort für den Inhalt suchen kann.

10. Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die auszuführenden Aktionen, und schließen Sie anschließend den Assistenten ab.  

     Sie können die Bereitstellung im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** im Detailbereich der Registerkarte für die Paketbereitstellung anzeigen, wenn Sie die Bereitstellung auswählen. Weitere Informationen finden Sie unter [Überwachen von Paketen und Programmen](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) in diesem Thema.  

> [!IMPORTANT]  
>  Wenn Sie die Option **Programm vom Verteilungspunkt ausführen** auf der Seite **Verteilungspunkte** im **Assistent zum Bereitstellen von Software** konfiguriert haben, dürfen Sie die Option **Den Inhalt in diesem Paket in eine Paketfreigabe auf Verteilungspunkten kopieren** nicht deaktivieren, da das Paket ansonsten nicht mehr von Verteilungspunkten aus ausgeführt werden kann.  

##  <a name="monitor-packages-and-programs"></a>Überwachen von Paketen und Programmen  
 Zum Überwachen von Paket- und Programmbereitstellungen verwenden Sie dieselben Verfahren wie zur Überwachung von Anwendungen. Diese Verfahren werden unter [Überwachen von Anwendungen](/sccm/apps/deploy-use/monitor-applications-from-the-console) beschrieben.  

 Pakete und Programme umfassen darüber hinaus mehrere integrierte Berichte, mit denen eine Überwachung der Informationen zum Bereitstellungsstatus von Paketen und Programmen möglich ist. Diesen Berichten sind die Berichtskategorien **Softwareverteilung – Paket- und Programmbereitstellung** und **Softwareverteilung – Status der Paket- und Programmbereitstellung**zugeordnet.  

 Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Verwalten von Paketen und Programmen  
 Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Knoten **Anwendungsverwaltung**, wählen Sie **Pakete** aus, wählen Sie das zu verwaltende Paket aus, und wählen Sie anschließend einen Verwaltungstask aus der folgenden Tabelle aus:  

|Aufgabe|Weitere Informationen|  
|----------|----------------------|  
|**Datei für vorab bereitgestellten Inhalt erstellen**|Mit dieser Option wird der **Assistent zum Erstellen von vorab bereitgestellten Inhaltsdateien** geöffnet, mit dem Sie eine Datei erstellen können, die den Paketinhalt enthält, der manuell an einem anderen Standort importiert werden kann. Dies bietet sich an, wenn die Bandbreite zwischen Standortserver und Verteilungspunkt eingeschränkt ist.|  
|**Programm erstellen**|Mit dieser Option wird der **Assistent zum Erstellen von Programmen** geöffnet, mit dem Sie ein neues Programm für dieses Paket erstellen können.|  
|**Exportierenieren**|Mit dieser Option wird der **Assistent zum Exportieren von Paketen** geöffnet, mit dem Sie das ausgewählte Paket und seinen Inhalt in eine Datei exportieren können.<br /><br /> Informationen zum Importieren von Paketen und Programmen finden Sie im Abschnitt [Erstellen von Paketen und Programmen](/sccm/apps/deploy-use/packages-and-programs#create-packages-and-programs) in diesem Thema.|  
|**Bereitstellen**|Mit dieser Option wird der **Assistent zum Bereitstellen von Software** geöffnet, mit dem Sie das ausgewählte Paket und Programm in einer Sammlung bereitstellen können. Weitere Informationen finden Sie unter [Bereitstellen von Paketen und Programmen](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) in diesem Thema.|  
|**Treiberpakete**|Mit dieser Option wird der **Assistent für die Verteilung von Inhalt** geöffnet, mit dem Sie den Inhalt, der dem Paket und Programm zugeordnet ist, an ausgewählte Verteilungspunkte oder Verteilungspunktgruppen senden können.|  
|**Verteilungspunkte aktualisieren**|Aktualisiert Verteilungspunkte mit dem neuesten Inhalt für das ausgewählte Paket und Programm.|  

##  <a name="about-the-package-definition-file-format"></a>Informationen zum Format von Paketdefinitionsdateien  
 Paketdefinitionsdateien sind Skripts, die Sie bei der automatischen Erstellung von Paketen und Programmen mit Configuration Manager unterstützen. Sie enthalten alle Informationen, die von Configuration Manager benötigt werden, um ein Paket und Programm zu erstellen (außer dem Speicherort der Paketquelldateien). Jede Paketdefinitionsdatei liegt als ASCII- oder UTF-8-Textdatei im INI-Dateiformat vor und enthält folgende Abschnitte:  

###  <a name="pdf"></a>[PDF]  
 Dieser Abschnitt kennzeichnet die Datei als Paketdefinitionsdatei. Es enthält die folgende Informationen:  

-   **Version**: Geben Sie hier die Version des Paketdefinitionsdateiformats an, das von der Datei verwendet wird. Dies entspricht der Version von Systems Management Server (SMS) oder Configuration Manager, für die sie geschrieben wurde. Dieser Eintrag ist obligatorisch.  

###  <a name="package-definition"></a>[Package Definition]  
 Geben Sie hier die Eigenschaften des Pakets und des Programms an. Es enthält die folgende Informationen:  

-   **Name**: Der Name des Pakets, bis zu 50 Zeichen.  

-   **Version** (optional): Die Version des Pakets, bis zu 32 Zeichen.  

-   **Symbol** (optional): Die Datei, die das für dieses Paket zu verwendende Symbol enthält. Wenn angegeben, ersetzt dieses Symbol das Standardpaketsymbol in der Configuration Manager-Konsole.

-   **Publisher**: Der Herausgeber des Pakets, bis zu 32 Zeichen.

-   **Sprache**: Die Sprachversion des Pakets, bis zu 32 Zeichen.

-   **Comment** (optional): Ein Kommentar zum Paket, bis zu 127 Zeichen.

-   **ContainsNoFiles**: Dieser Eintrag gibt an, ob dem Paket eine Quelle zugeordnet ist.  

-   **Programs**: Die für dieses Paket definierten Programme. Jeder Programmname entspricht einem **[Program]** -Abschnitt in dieser Paketdefinitionsdatei.  

     Beispiel:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: Der Name der MIF-Datei (Management Information Format), die den Paketstatus enthält, bis zu 50 Zeichen.  

-   **MIFName**: Der Name des Pakets (für die MIF-Statusabstimmung), bis zu 50 Zeichen.  

-   **MIFVersion**: Die Versionsnummer des Pakets (für die MIF-Statusabstimmung), bis zu 32 Zeichen.  

-   **MIFPublisher**: Der Softwareherausgeber des Pakets (für die MIF-Statusabstimmung), bis zu 32 Zeichen.  

###  <a name="program"></a>[Program]  
 Für jedes Programm, das gemäß dem Eintrag **Programme** im Abschnitt **[Package Definition]** angegeben ist, muss die Paketdefinitionsdatei einen Abschnitt [Program] enthalten, der dieses Programm definiert. Jedes Programm Abschnitt enthält die folgenden Informationen:  

-   **Name**: Der Name des Programms, bis zu 50 Zeichen. Dieser Eintrag muss innerhalb eines Pakets eindeutig sein. Dieser Name wird verwendet, wenn Ankündigungen zu definieren. Auf Clientcomputern, sehen Sie der Namen des Programms **angekündigte Programme ausführen** in der Systemsteuerung.  

-   **Symbol** (optional): Geben Sie hier die Datei an, die das für dieses Programm zu verwendende Symbol enthält. Wenn angegeben, ersetzt dieses Symbol das Standardprogrammsymbol in der Configuration Manager-Konsole und wird bei der Ankündigung des Programms auf Clientcomputern angezeigt.

-   **Kommentar** (optional): Ein Kommentar zum Programm, bis zu 127 Zeichen.

-   **CommandLine**: Geben Sie hier die Befehlszeile für das Programm an, bis zu 127 Zeichen. Der Befehl ist relativ zum Paketquellordner.

-   **StartIn**: Geben Sie hier den Arbeitsordner für das Programm an, bis zu 127 Zeichen. Dies kann ein absoluter Pfad auf dem Clientcomputer oder ein Pfad relativ zum Paketquellordner sein.

-   **Run**: Geben Sie hier den Programmmodus an, in dem das Programm ausgeführt wird. Sie können **Minimized**, **Maximized**oder **Hidden**angeben. Wenn dieser Eintrag nicht angegeben wird, wird das Programm im Normalmodus ausgeführt.  

-   **AfterRunning**: Geben Sie hier alle speziellen Aktionen an, die nach dem erfolgreichen Programmabschluss ausgeführt werden sollen. Die verfügbaren Optionen sind **SMSRestart**, **ProgramRestart**, oder **SMSLogoff**. Ohne diesen Eintrag führt das Programm keine speziellen Aktionen aus.  

-   **EstimatedDiskSpace**: Geben Sie hier die Menge des Speicherplatzes an, den das Programm benötigt, um auf dem Computer ausgeführt zu werden. Er kann als **Unknown** (die Standardeinstellung) oder als eine ganze Zahl größer oder gleich Null angegeben werden. Wenn kein Wert angegeben ist, müssen auch die Einheiten für diesen Wert angegeben werden.  

     Beispiel:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: Geben Sie hier (in Minuten) an, wie lange das Programm voraussichtlich auf dem Clientcomputer ausgeführt wird. Er kann als **Unknown** (die Standardeinstellung) oder als eine ganze Zahl größer Null angegeben werden.  

     Beispiel:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: Geben Sie hier die Prozessoren und Betriebssysteme an, auf denen das Programm ausgeführt werden kann. Zu den angegebenen Plattformen müssen durch Kommas getrennt werden. Ohne diesen Eintrag wird die Überprüfung der unterstützten Plattformen für dieses Programm deaktiviert.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Geben Sie hier den Versionsnummernbereich (Von, Bis) für die Betriebssysteme an, die im Eintrag **SupportedClients** angegeben sind.  

     Beispiel:  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements** (optional): Geben Sie hier etwaige sonstige Informationen oder Anforderungen zu Clientcomputern an, bis zu 127 Zeichen.

-   **CanRunWhen**: Geben Sie hier den Benutzerstatus an, der für die Ausführung des Programms auf dem Clientcomputer erforderlich ist. Es stehen die Werte **UserLoggedOn**, **NoUserLoggedOn**, oder **AnyUserStatus**zur Verfügung. Der Standardwert ist **UserLoggedOn**.  

-   **UserInputRequired**: Geben Sie hier an, ob das Programm Benutzereingriffe erfordert. Es stehen die Werte **True** oder **False**zur Verfügung. Der Standardwert ist **True**. Dieser Eintrag ist auf **False** festgelegt, wenn **CanRunWhen** nicht auf **UserLoggedOn**festgelegt ist.  

-   **AdminRightsRequired**: Geben Sie hier an, ob das Programm für die Ausführung auf dem Computer Administratoranmeldeinformationen erfordert. Es stehen die Werte **True** oder **False**zur Verfügung. Der Standardwert ist **False**. Dieser Eintrag ist auf **True** festgelegt, wenn **CanRunWhen** nicht auf **UserLoggedOn**festgelegt ist.  

-   **UseInstallAccount**: Geben Sie hier an, ob das Programm das Clientsoftwareinstallationskonto verwendet, wenn es auf Clientcomputern ausgeführt wird. Standardmäßig ist dieser Wert **False**. Der Wert ist auch dann **False** , wenn **CanRunWhen** auf **UserLoggedOn**festgelegt ist.  

-   **DriveLetterConnection**: Geben Sie hier an, ob das Programm eine Laufwerkbuchstabenverbindung zu den Paketdateien benötigt, die sich auf dem Verteilungspunkt befinden. Sie können entweder **True** oder **False**angeben. Der Standardwert ist **False**, was dem Programm die Verwendung einer UNC-Verbindung (Universal Naming Convention) ermöglicht. Wenn dieser Wert auf **True** festgelegt ist, wird der nächste verfügbare Laufwerkbuchstabe verwendet (beginnend mit Z: und in absteigender Reihenfolge).  

-   **SpecifyDrive** (optional): Geben Sie hier einen Laufwerkbuchstaben an, den das Programm für die Verbindung zu den Paketdateien auf dem Verteilungspunkt benötigt. Diese Spezifikation erzwingt die Verwendung der angegebene Laufwerkbuchstabe für Clientverbindungen an Verteilungspunkte.

-   **ReconnectDriveAtLogon**: Geben Sie hier an, ob der Computer die Verbindung zum Verteilungspunkt erneut herstellt, wenn sich der Benutzer anmeldet. Es stehen die Werte **True** oder **False**zur Verfügung. Der Standardwert ist **False**.  

-   **DependentProgram**: Geben Sie hier ein Programm in diesem Paket an, das vor dem aktuellen Programm ausgeführt werden muss. Für diesen Eintrag wird folgendes Format verwendet: **DependentProgram**=<**Programmname>**, wobei **<Programmname\>** der Eintrag **Name** für das Programm in der Paketdefinitionsdatei ist. Lassen Sie den Eintrag leer, wenn keine abhängigen Programme vorhanden sind.  

     Beispiel:  

     DependentProgram = Admin  
    DependentProgram =  

-   **Assignment**: Geben Sie hier an, wie das Programm Benutzern zugewiesen wird. Folgende Werte sind möglich: **FirstUser** (das Programm wird nur für den ersten Benutzer ausgeführt, der sich am Client anmeldet) oder **EveryUser** (das Programm wird für alle Benutzer ausgeführt, sie sich am Client anmelden). Dieser Eintrag ist auf **FirstUser** festgelegt, wenn **CanRunWhen**nicht auf **UserLoggedOn**festgelegt ist.  

-   **Deaktiviert**: Geben Sie hier an, ob das Programm für Clients angekündigt werden kann. Es stehen die Werte **True** oder **False**zur Verfügung. Der Standardwert ist **False**.  
