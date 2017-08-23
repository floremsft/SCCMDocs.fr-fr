---
title: Mac-Clients bereitstellen | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie Clients auf Macintosh-Computern in System Center Configuration Manager bereitstellen können."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6ce212c6745b70a47553891e5dbc124b4c4e50fa
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema beschreibt, wie der Configuration Manager-Client auf Macintosh-Computern bereitgestellt und gewartet wird. Sie finden Informationen dazu, welche Einstellungen Sie vor der Bereitstellung von Clients auf Macintosh-Computern konfigurieren müssen, unter [Vorbereiten der Bereitstellung von Clientsoftware auf Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Wenn Sie einen neuen Client für Macintosh-Computer installieren, müssen Sie möglicherweise auch Configuration Manager-Updates installieren, um die neuen Clientinformationen in der Configuration Manager-Konsole darzustellen.

In diesen Verfahren haben Sie zwei Optionen zum Installieren von Clientzertifikaten. Weitere Informationen zu Clientzertifikaten für Macs finden Sie unter [Vorbereiten der Bereitstellung von Clientsoftware auf Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

-   Verwenden der Configuration Manager-Registrierung mithilfe des Tools [CMEnroll](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). Die automatische Zertifikatserneuerung wird bei der Anmeldung nicht unterstützt, sodass Sie Macintosh-Computer vor dem Ablaufdatum des installierten Zertifikats erneut anmelden müssen.    

-   [Verwenden einer von Configuration Manager unabhängigen Zertifikatanforderungs- und -installationsmethode](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager). 

>[!IMPORTANT]
>  Zum Bereitstellen des Clients auf Geräten mit macOS Sierra muss der Antragstellername des Verwaltungspunktzertifikats ordnungsgemäß konfiguriert werden, z. B. mithilfe des FQDN des Verwaltungspunktservers.


## <a name="configure-client-settings-for-enrollment"></a>Konfigurieren Sie die Clienteinstellungen für die Anmeldung  
 Sie müssen zum Konfigurieren der Anmeldung für Macintosh-Computer die [Clientstandardeinstellungen](../../../core/clients/deploy/about-client-settings.md) verwenden. Benutzerdefinierte Clienteinstellungen dürfen hierzu nicht verwendet werden.  

 Dies ist in Configuration Manager zum Anfordern und Installieren des Zertifikats auf dem Macintosh-Computer erforderlich.  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>So konfigurieren Sie die Clientstandardeinstellungen für Configuration Manager zum Registrieren von Zertifikaten für Macintosh-Computer  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie den Abschnitt **Anmeldung** aus, und konfigurieren Sie dann diese Einstellungen:  

    1.  **Benutzern die Registrierung mobiler Geräte und von Macintosh-Computern gestatten: Ja**  

    2.  **Anmeldungsprofil:** Wählen Sie **Profil festlegen**.  

6.  Wählen Sie im Dialogfeld **Anmeldungsprofil für mobile Geräte** **Erstellen**.  

7.  Geben Sie im Dialogfeld **Anmeldungsprofil erstellen** einen Namen für dieses Anmeldungsprofil ein, und konfigurieren Sie dann den **Verwaltungsstandortcode**. Wählen Sie den primären Configuration Manager-Standort aus, der die Verwaltungspunkte enthält, von denen die Macintosh-Computer verwaltet werden sollen.  

    > [!NOTE]  
    >  Wenn ein Auswählen des Standorts nicht möglich ist, achten Sie darauf, dass mindestens ein Verwaltungspunkt am Standort für die Unterstützung mobiler Geräte konfiguriert ist.  

8.  Wählen Sie **Hinzufügen** aus.  

9. Wählen Sie im Dialogfeld **Zertifizierungsstelle für mobile Geräte hinzufügen** den Server der Zertifizierungsstelle aus, von der Zertifikate für Macintosh-Computer ausgestellt werden.  

10. Wählen Sie im Dialogfeld **Anmeldungsprofil erstellen** die Zertifikatvorlage für Macintosh-Computer aus, die Sie in Schritt 3 erstellt haben.  

11. Klicken Sie auf **OK**, um das Dialogfeld **Anmeldungsprofil**, und anschließend das Dialogfeld **Clientstandardeinstellungen** zu schließen.  

    > [!TIP]  
    >  Wenn Sie das Clientrichtlinienintervall ändern möchten, verwenden Sie in der Clienteinstellungsgruppe **Clientrichtlinie** die Clienteinstellung **Clientrichtlinien-Abrufintervall**.  

 Alle Benutzer werden mit diesen Einstellungen beim nächsten Herunterladen der Clientrichtlinie konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [Initiieren des Richtlinienabrufs für einen Configuration Manager-Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Zusätzlich zu den Clienteinstellungen für die Registrierung müssen Sie unbedingt auch die folgenden Clientgeräteeinstellungen konfigurieren:  

-   **Hardwareinventur**: Aktivieren und konfigurieren Sie dies, wenn Sie Hardwareinventurdaten von Macintosh- und Windows-Clientcomputern sammeln möchten. Weitere Informationen finden Sie unter [Erweitern der Hardwareinventur in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Konformitätseinstellungen**: Aktivieren und konfigurieren Sie dies, wenn Sie Einstellungen von Macintosh- und Windows-Clientcomputern auswerten und wiederherstellen möchten. Weitere Informationen finden Sie unter [Planen und Konfigurieren von Kompatibilitätseinstellungen](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  Weitere Informationen zu Configuration Manager-Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

## <a name="download-the-client-source-files-for-macs"></a>Die Clientquelldateien für Macintosh-Computer herunterladen  

1.  Laden Sie das Mac OS X-Clientdateipaket, **ConfigmgrMacClient.msi**, herunter, und speichern Sie es auf einem Computer mit Windows.  

     Diese Datei wird nicht auf den Configuration Manager-Installationsmedien bereitgestellt. Diese Datei steht im [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184)als Download zur Verfügung.  

2.  Führen Sie auf dem Windows-Computer **ConfigmgrMacClient.msi** aus, um das Mac-Clientpaket „Macclient.dmg“ in einen Ordner auf der lokalen Festplatte (standardmäßig **C:\Programme (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**) zu extrahieren.  

3.  Kopieren Sie die Datei Macclient.dmg in einen Ordner auf dem Macintosh-Computer.  

4.  Führen Sie auf dem Macintosh-Computer die Datei Macclient.dmg aus, um die Dateien in einem Ordner auf der lokalen Festplatte zu extrahieren.  

5.  Überprüfen Sie im Ordner, ob die Dateien Ccmsetup und CMClient.pkg extrahiert wurden und ein Ordner mit dem Namen Tools erstellt wurde, in dem die Tools CMDiagnostics, CMUninstall, CMAppUtil und CMEnroll enthalten sind.

    -  **Ccmsetup**: Installiert den Configuration Manager-Client auf Ihren Macintosh-Computern.  

    -   **CMDiagnostics**: Sammelt Diagnoseinformationen zu dem auf Macintosh-Computern installierten Configuration Manager-Client.  

    -   **CMUninstall**: Deinstalliert den Client von Ihren Macintosh-Computern.  

    -   **CMAppUtil**: Konvertiert Apple-Anwendungspakete in ein Format, das als Configuration Manager-Anwendung bereitgestellt werden kann.  

    -   **CMEnroll**: Fordert das Clientzertifikat für einen Macintosh-Computer an und installiert es, damit Sie den Configuration Manager-Client installieren können.   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Installieren Sie den Client, und melden Sie anschließend das Clientzertifikat auf dem Macintosh-Computer an  

Sie können einzelne Clients mithilfe des [Assistenten für die Macintosh-Computeranmeldung](#enroll-the-client-with-the-mac-computer-enrollment-wizard) registrieren.

Verwenden Sie das [Tool „CMEnroll“](#client-and-certificate-automation-with-cmenroll) für die Automatisierung, die die Registrierung vieler Clients ermöglicht.   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>So registrieren Sie den Client mithilfe des Assistenten für die Macintosh-Computeranmeldung  

1.  Nach der Installation des Clients wird der Assistent für die Computeranmeldung wird geöffnet. Wird der Assistent nicht geöffnet, oder haben Sie ihn versehentlich geschlossen, dann klicken Sie auf der Einstellungsseite von **Configuration Manager** auf **Registrieren**, um den Assistenten zu öffnen.  

2.  Geben Sie auf der zweiten Seite des Assistenten Folgendes an:  

    -   **Benutzername** : Der Benutzername kann die folgenden Formate aufweisen:  

        -   'Domäne\Name'. Beispiel: 'contoso\mrankenburg'  

        -   'user@domain'. Beispiel: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Wenn Sie in das Feld **Benutzername** eine E-Mail-Adresse eingeben, wird von Configuration Manager automatisch der Domänenname der E-Mail-Adresse und der Standardname des Registrierungsproxypunkt-Servers für das Feld **Servername** verwendet. Wenn der Domänenname und der Servername nicht mit dem Namen des Anmeldungsproxypunkt-Servers übereinstimmen, müssen Sie die Benutzer über den richtigen Namen informieren, damit sie diesen bei der Registrierung ihrer Macintosh-Computer eingeben können.  

         Der Benutzername und das zugehörige Kennwort müssen mit den entsprechenden Angaben eines Active Directory-Benutzerkontos übereinstimmen, für das in der Mac-Clientzertifikatvorlage die Berechtigungen Lesen und Anmelden zugewiesen wurden.  

    -   **Kennwort** – Geben Sie ein passendes Kennwort für den angegebenen Benutzernamen ein.  

    -   **Servername** – Geben Sie den Namen des Registrierungsproxypunkt-Servers ein.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automatisierung von Client und Zertifikat mit CMEnroll  

Verwenden Sie dieses Verfahren für die Automatisierung der Installation des Clients und zum Anfordern und Registrieren der Clientzertifikate mit dem Tool „CMEnroll“. Sie müssen über ein Active Directory-Benutzerkonto verfügen, um das Tool ausführen zu können.

1.  Navigieren Sie auf dem Macintosh-Computer zu dem Ordner, in dem Sie den Inhalt der Datei Macclient.dmg extrahiert haben.  

2.  Geben Sie die folgende Befehlszeile ein: **sudo ./ccmsetup**  

3.  Warten Sie, bis die Meldung **Installation abgeschlossen** angezeigt wird. Vom Installationsprogramm wird eine Meldung angezeigt, dass Sie den Computer jetzt neu starten müssen. Führen Sie den Neustart nicht aus, sondern fahren Sie mit dem nächsten Schritt fort.  

4.  Geben Sie im Ordner „Extras“ auf dem Macintosh-Computer Folgendes ein: **sudo ./CMEnroll -s &lt;Name_des_Anmeldungsproxyservers> -ignorecertchainvalidation -u &lt;'Benutzername'>**  

    Nach der Clientinstallation wird der Assistent für die Macintosh-Computeranmeldung geöffnet, um Ihnen beim Anmelden des Macintosh-Computers zu helfen. Informationen zum Anmelden des Clients mit dieser Methode finden Sie unter [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) in diesem Thema.  

5. Geben Sie das Kennwort für das Active Directory-Benutzerkonto ein.  Wenn Sie diesen Befehl eingeben, müssen Sie zwei Kennwörter eingeben: Zuerst müssen Sie das Kennwort für das Administratorkonto eingeben, um den Befehl auszuführen. Die zweite Eingabeaufforderung bezieht sich auf das Active Directory-Benutzerkonto. Da beide Eingabeaufforderungen identisch aussehen, achten Sie darauf, dass Sie die richtige Reihenfolge einhalten.  

    Der Benutzername kann die folgenden Formate aufweisen:  

    -   'Domäne\Name'. Beispiel: 'contoso\mrankenburg'  

    -   'user@domain'. Beispiel: 'mnorth@contoso.com'  

     Der Benutzername und das zugehörige Kennwort müssen mit den entsprechenden Angaben eines Active Directory-Benutzerkontos übereinstimmen, für das in der Mac-Clientzertifikatvorlage die Berechtigungen Lesen und Anmelden zugewiesen wurden.  

     Beispiel: Wenn der Name des Registrierungsproxypunkt-Servers **server02.contoso.com**lautet und dem Benutzernamen **contoso\mnorth** Berechtigungen für die Macintosh-Computer-Clientzertifikatvorlage erteilt wurden, geben Sie Folgendes ein: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  Wenn der Benutzername eines der Zeichen **&lt;> "+=,** enthält, tritt ein Fehler bei der Registrierung auf. Rufen Sie ein Out-of-Band-Zertifikat mit einem Benutzernamen ab, der diese Zeichen nicht enthält.  
    >  
    >  Zur Verbesserung der Benutzerfreundlichkeit können Sie ein Skript für die Installationsschritte und -befehle erstellen, sodass die Benutzer nur ihren Benutzernamen und ihr Kennwort angeben müssen.  

5.  Warten Sie, bis die Meldung angezeigt wird, dass die **Anmeldung erfolgreich** war.  

6.  Öffnen Sie auf dem Macintosh-Computer ein Terminalfenster, und nehmen Sie folgende Änderungen vor, um das registrierte Zertifikat auf Configuration Manager zu beschränken:  

    a.  Geben Sie den Befehl **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**ein.  

    b.  Klicken Sie im Dialogfeld **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** auf **System**, und im Abschnitt **Kategorie** anschließend auf **Schlüssel**.  

    c.  Erweitern Sie die Schlüssel, um die Clientzertifikate anzuzeigen. Wenn Sie das Zertifikat mit einem gerade installierten privaten Schlüssel identifiziert haben, doppelklicken Sie auf dem Schlüssel.  

    d.  Wählen Sie auf der Registerkarte **Zugriffssteuerung** die Option **Confirm before allowing access** (Bestätigen, bevor Zugriff zugelassen wird) aus.  

    e.  Navigieren Sie zum Ordner **/Library/Application Support/Microsoft/CCM**, wählen Sie **CCMClient** aus, und wählen Sie dann **Hinzufügen** aus.  

    f.  Wählen Sie **Änderungen sichern** aus, und schließen Sie das Dialogfeld **Schlüsselbundverwaltung**.  

7.  Starten Sie den Macintosh-Computer neu.  

 Überprüfen Sie, ob die Clientinstallation erfolgreich ausgeführt wurde. Öffnen Sie hierzu auf dem Macintosh-Computer in den **Systemeinstellungen** das Element **Configuration Manager** . Sie können auch die Sammlung **Alle Systeme** aktualisieren und anzeigen, um sicherzustellen, dass der Macintosh-Computer jetzt in der Sammlung als verwalteter Client angezeigt wird.  

> [!TIP]  
>  Sie können Probleme mit dem Mac-Client mithilfe des Programms „CMDiagnostics“ beheben, das im Mac OS X-Clientpaket enthalten ist. Damit können die folgenden Diagnoseinformationen gesammelt werden:  
>   
>  -   Eine Liste der ausgeführten Prozesse  
> -   Die Version des Mac OS X-Betriebssystems  
> -   Mac OS X-Absturzberichte, die sich auf den Configuration Manager-Client beziehen, einschließlich **CCM\*.crash** und **System Preference.crash**.  
> -   Die BOM-Datei (Bill of Materials) und die Eigenschaftenlistendatei (PLIST-Datei), die im Rahmen der Configuration Manager-Clientinstallation erstellt wurden  
> -   Der Inhalt des Ordners /Library/Application Support/Microsoft/CCM/Logs  
>   
>  Die von CmDiagnostics gesammelten Informationen werden einer ZIP-Datei hinzugefügt, die auf dem Desktop des Computers gespeichert und den Namen„cmdiag-*<Hostname\>***-***&gt;Datum und Uhrzeit\>*.zip“ erhält.***


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Verwenden einer von Configuration Manager unabhängigen Zertifikatanforderungs- und -installationsmethode  

Führen Sie zuerst die bestimmten Aufgaben unter [Vorbereiten der Bereitstellung von Clientsoftware auf Macs](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients) aus:

1. [Stellen Sie ein Webserverzertifikat für Standortsystemserver bereit](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [Stellen Sie ein Clientauthentifizierungszertifikat für Standortsystemserver bereit](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [Konfigurieren Sie den Verwaltungspunkt und den Verteilungspunkt](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [Optional: Installieren Sie den Reporting Services-Punkt](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

Führen Sie anschließend diese Aufgaben aus:

5. [Laden Sie die Clientquelldateien für Macintosh-Computer herunter](#download-the-client-source-files-for-macs)  
6. Verwenden Sie die Anweisungen der ausgewählten Methode zur Zertifikatbereitstellung, um das Clientzertifikat anzufordern, und auf jedem Macintosh-Computer zu installieren.  
7.  Navigieren Sie zu dem Ordner, in dem Sie den Inhalt der von der Microsoft Download Center-Website heruntergeladenen Datei macclient.dmg extrahiert haben.  

3.  Geben Sie die folgende Befehlszeile ein: **sudo ./ccmsetup -MP <Verwaltungspunkt_Internet-FQDN\> -SubjectName <Wert für Zertifikatantragsteller\>**.  Beim Wert für den Zertifikatantragsteller muss die Groß-/Kleinschreibung beachtet werden, daher muss dieser genauso eingegeben werden, wie er in den Zertifikatdetails angezeigt wird.  

     Beispiel: Wenn der Internet-FQDN in den Standortsystemeigenschaften **server03.contoso.com** lautet und das Macintosh-Client-Zertifikat den FQDN von **mac12.contoso.com** als allgemeinen Namen für den Zertifikatantragsteller verwendet, geben Sie Folgendes ein: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Warten Sie, bis die Meldung **Installation abgeschlossen** angezeigt wird, und starten Sie anschließend den Macintosh-Computer neu.  

5.  Öffnen Sie auf dem Macintosh-Computer ein Terminal-Fenster, und nehmen Sie diese Änderungen vor, um sicherzustellen, dass Configuration Manager auf dieses Zertifikat zugreifen kann:  

    a.  Geben Sie den Befehl **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**ein.  

    b.  Klicken Sie im Dialogfeld **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** auf **System**, und im Abschnitt **Kategorie** anschließend auf **Schlüssel**.  

    c.  Erweitern Sie die Schlüssel, um die Clientzertifikate anzuzeigen. Wenn Sie das Zertifikat mit einem gerade installierten privaten Schlüssel identifiziert haben, doppelklicken Sie auf dem Schlüssel.  

    d.  Wählen Sie auf der Registerkarte **Zugriffssteuerung** die Option **Confirm before allowing access** (Bestätigen, bevor Zugriff zugelassen wird) aus.  

    e.  Navigieren Sie zum Ordner **/Library/Application Support/Microsoft/CCM**, wählen Sie **CCMClient** aus, und wählen Sie dann **Hinzufügen** aus.  

    f.  Wählen Sie **Änderungen sichern** aus, und schließen Sie das Dialogfeld **Schlüsselbundverwaltung**.  

6.  Wenn Sie über mehrere Zertifikate mit dem gleichen Wert für den Antragsteller verfügen, müssen Sie die Seriennummer des Zertifikats angeben, um das für den Configuration Manager-Client zu verwendende Zertifikat zu bestimmen. Verwenden Sie hierzu den folgenden Befehl: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<Seriennummer\>"**.  

     Beispiel: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Überprüfen Sie, ob die Clientinstallation erfolgreich ausgeführt wurde. Öffnen Sie hierzu auf dem Macintosh-Computer in den **Systemeinstellungen** das Element **Configuration Manager**. Sie können auch die Sammlung **Alle Systeme** aktualisieren und anzeigen, um sicherzustellen, dass der Macintosh-Computer in der Sammlung als verwalteter Client angezeigt wird.  

## <a name="renewing-the-mac-client-certificate"></a>Erneuern des Zertifikats für den Macintosh-Client  
 Gehen Sie folgendermaßen vor, bevor Sie das Computerzertifikat auf Macintosh-Computern erneuern.  

 Bei diesem Verfahren wird die SMS-ID entfernt, welche vom Client zur Verwendung eines neuen oder erneuerten Zertifikats auf dem Macintosh-Computer benötigt wird.  

> [!IMPORTANT]  
>  Wenn Sie die Client-SMS-ID entfernen und ersetzen, wird der gesamte gespeicherte Clientverlauf, wie beispielsweise der Bestand, nach dem Löschen des Clients über die Configuration Manager-Konsole gelöscht.  

### <a name="to-renew-the-mac-client-certificate"></a>So erneuern Sie das Macintosh-Clientzertifikat  

1.  Erstellen Sie für die Mac-Computer, deren Benutzerzertifikate verlängert werden müssen, eine Gerätesammlung.  

2.  Starten Sie im Arbeitsbereich **Bestand und Kompatibilität** den **Assistenten zum Erstellen von Konfigurationselementen**.  

3.  Geben Sie auf der Seite **Allgemein** des Assistenten die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Typ:Mac OS X**  

4.  Vergewissern Sie sich auf der Seite **Unterstützte Plattformen** des Assistenten, dass alle Versionen von Mac OS X ausgewählt sind.  

5.  Klicken Sie auf der Seite **Einstellungen** des Assistenten auf **Neu** , und geben Sie anschließend im Dialogfeld **Einstellung erstellen** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Einstellungstyp:Skript**  

    -   **Datentyp:Zeichenfolge**  

6.  Klicken Sie im Dialogfeld **Einstellung erstellen** für **Ermittlungsskript**auf **Skript hinzufügen** , um ein Skript anzugeben, mit dem Macintosh-Computer ermittelt werden können, die über eine konfigurierte SMS-ID verfügen.  

7.  Geben Sie im Dialogfeld **Ermittlungsskript bearbeiten** das folgende Shellskript ein:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Wählen Sie **OK** aus, um das Dialogfeld **Ermittlungsskript bearbeiten** zu schließen.  

9. Wählen Sie im Dialogfeld **Einstellung erstellen** für **Wiederherstellungsskript (optional)** **Skript hinzufügen** aus, um ein Skript anzugeben, mit dem die SMSID von Mac-Computern entfernt wird, wenn sie gefunden wird.  

10. Geben Sie im Dialogfeld **Wiederherstellungsskript erstellen** das folgende Shellskript ein:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Wählen Sie **OK** aus, um das Dialogfeld **Wiederherstellungsskript erstellen** zu schließen.  

12. Wählen Sie auf der Seite **Konformitätsregeln** des Assistenten **Neu** aus, und geben Sie anschließend im Dialogfeld **Regel erstellen** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Ausgewählte Einstellung:** Wählen Sie **Durchsuchen** aus, und wählen Sie anschließend das Ermittlungsskript aus, das Sie zuvor angegeben haben.  

    -   Geben Sie im Feld **die folgenden Werte** **Das Domänen-/Standardpaar (com.microsoft.ccmclient, SMS-ID) existiert nicht**ein.  

    -   Aktivieren Sie die Option **Das angegebene Wiederherstellungsskript ausführen, wenn diese Einstellung nicht kompatibel ist**.  

13. Beenden Sie den Assistenten zum Erstellen von Konfigurationselementen.  

14. Erstellen Sie eine Konfigurationsbasislinie mit dem Konfigurationselement, das Sie gerade erstellt haben, und stellen Sie es für die Gerätesammlung bereit, die Sie in Schritt 1 erstellt haben.  

     Weitere Informationen zum Erstellen und Bereitstellen von Konfigurationsbaselines finden Sie unter [Erstellen von Konfigurationsbaselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Führen Sie den folgenden Befehl aus, nachdem Sie ein neues Zertifikat auf Macintosh-Computern mit entfernter SMS-ID installiert haben, um den Client so zu konfigurieren, dass das neue Zertifikat verwendet wird:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Wenn Sie über mehrere Zertifikate mit dem gleichen Wert für den Antragsteller verfügen, müssen Sie die Seriennummer des Zertifikats angeben, um das für den Configuration Manager-Client zu verwendende Zertifikat zu bestimmen. Verwenden Sie hierzu den folgenden Befehl: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<Seriennummer\>"**.  

     Beispiel: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Neu starten.  


## <a name="see-also"></a>Weitere Informationen:

[Warten von Macintosh-Clients](/sccm/core/clients/manage/maintain-mac-clients)
