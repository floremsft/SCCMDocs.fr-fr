---
title: "Erstellen von Konfigurationselementen für Windows Phone-Geräte, die mit Intune verwaltet werden | Microsoft-Dokumentation"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df10dc4d-c9ff-4574-bb33-8d30eb14cfe3
caps.latest.revision: "13"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: bcb2d14ef097afc2915932fe09f6d83c968aecf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-windows-phone-devices-managed-without-the-system-center-configuration-manager-client"></a>Erstellen von Konfigurationselementen für Windows Phone-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden
Verwenden Sie das **Windows Phone**-Konfigurationselement von System Center Configuration Manager, um Einstellungen für Windows Phone-Geräte zu verwalten, die bei Microsoft Intune registriert sind oder lokal von Configuration Manager verwaltet werden.  
  
### <a name="to-create-a-windows-phone-configuration-item"></a>So erstellen Sie ein Windows Phone-Konfigurationselement  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Konformität**.  
  
2.  Erweitern Sie im Arbeitsbereich **Bestand und Konformität** die **Konformitätseinstellungen**, und klicken Sie auf **Konfigurationselemente**.  
  
3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  
  
4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  
  
5.  Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Windows Phone**aus.  
  
6.  Klicken Sie auf **Kategorien**, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  
  
7.  Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die jeweiligen Windows Phone-Plattformen zur Bewertung des Konfigurationselements aus.  
  
8.  Wählen Sie auf der Seite **Geräteeinstellungen** des Assistenten die Einstellungsgruppe aus, die Sie konfigurieren möchten. Informieren Sie sich in diesem Thema unter [Referenz zu den Einstellungen für Windows Phone-Konfigurationselemente](#BKMK_Setref) über die Details, und klicken Sie dann auf **Weiter**.  
  
    > [!TIP]  
    >  Ist die gewünschte Einstellung nicht aufgeführt, aktivieren Sie das Kontrollkästchen **Zusätzliche Einstellungen konfigurieren, die in den Standardeinstellungsgruppen nicht enthalten sind**.  
  
9. Konfigurieren Sie auf jeder Einstellungsseite die erforderlichen Einstellungen, und legen Sie fest, ob sie korrigiert werden sollen, wenn sie auf Geräten nicht kompatibel sind (sofern unterstützt).  
  
10. Sie können für jede Einstellungsgruppe auch den Schweregrad konfigurieren, der gemeldet wird, wenn die Inkompatibilität eines Konfigurationselements festgestellt wird. Die Einstellungen lauten wie folgt:  
  
    -   **Keiner**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  
  
    -   **Information**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  
  
    -   **Warnung**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  
  
    -   **Kritisch**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  
  
    -   **Kritisch mit Ereignis**: Von Geräten, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  
  
11. Überprüfen Sie auf der Seite **Plattformanwendbarkeit** des Assistenten alle Einstellungen, die mit den zuvor ausgewählten unterstützten Plattformen nicht kompatibel sind. Sie können zurückkehren und diese Einstellungen entfernen oder den Vorgang fortsetzen.  
  
    > [!TIP]  
    >  Nicht unterstützte Einstellungen werden nicht auf Kompatibilität überprüft.  
  
12. Schließen Sie den Assistenten ab.  
  
 Sie können das neue Konfigurationselement im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Konfigurationselemente** anzeigen.  
  
##  <a name="windows-phone-configuration-item-settings-reference"></a>Referenz zu den Einstellungen für Windows Phone-Konfigurationselemente  
  
### <a name="password"></a>Kennwort  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Kennworteinstellungen auf Geräten erforderlich**|Auf unterstützten Geräten ein Kennwort erfordern.|  
|**Minimale Kennwortlänge (Zeichen)**|Die Mindestlänge für das Kennwort.|  
|**Kennwortablauf in Tagen**|Die Anzahl der Tage, bevor ein Kennwort geändert werden muss.|  
|**Anzahl der gespeicherten Kennwörter**|Verhindert die Wiederverwendung zuvor verwendeter Kennwörter.|  
|**Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts**|Setzt das Gerät zurück, wenn diese Anzahl von Anmeldeversuchen fehlschlägt.|  
|**Kennwortkomplexität**|Wählen Sie aus, ob Sie eine PIN wie „1234“ angeben können oder, ob ein sicheres Kennwort erforderlich ist.|  
|**Kennwortwiederherstellungs-PIN an Exchange Server senden**||  
  
### <a name="device"></a>Gerät  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Bildschirmaufnahme**|Ermöglicht dem Benutzer, einen Screenshot der Geräteanzeige aufzunehmen.<br /><br /> (Nur Windows Phone 8.1)|  
|**Übermittlung von Diagnosedaten**|Ermöglicht die Übermittlung von Protokolldateien der App.|  
|**Geolocation**|Ermöglicht dem Gerät die Verwendung von Ortungsdienstinformationen.<br /><br /> (Nur Windows Phone 8.1)|  
|**Kopieren und Einfügen**|Verwenden Sie zum Übertragen von Daten zwischen Apps das Kopieren und Einfügen.<br /><br /> (Nur Windows Phone 8.1)|  
|**Bluetooth**|Ermöglicht die Verwendung der Bluetooth-Funktion des Geräts.|  
  
### <a name="email-management"></a>E-Mail-Verwaltung  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**POP- und IMAP-E-Mail**|Ermöglicht die Verbindung mit E-Mail-Konten, die POP- und IMAP-Standards verwenden.|  
|**Maximale Zeitdauer für die Speicherung von E-Mails**|Dauer der Speicherung von E-Mails, bevor sie vom Server gelöscht werden.|  
|**Zulässige Nachrichtenformate**|Geben Sie an, ob E-Mails HTML oder Nur-Text verwenden können.|  
|**Maximale Größe für E-Mails im Nur-Text-Format (automatisch heruntergeladen)**|Steuert die maximale Größe für E-Mails im Nur-Text-Format beim automatischen Herunterladen.|  
|**Maximale Größe für E-Mails im HTML-Format (automatisch heruntergeladen)**|Steuert die maximale Größe für E-Mails im HTML-Format beim automatischen Herunterladen.|  
|**Maximale Größe eines Anhangs (automatisch heruntergeladen)**|Konfiguriert die maximale Größe für E-Mails, die automatisch heruntergeladen werden.|  
|**Kalendersynchronisierung**||  
|**Benutzerdefiniertes E-Mail-Konto**|Ermöglicht die Verwendung eines Nicht-Microsoft-Kontos auf dem Gerät.|  
|**Microsoft-Konto in Windows Mail-App optional machen**|Erfordert keine Verwendung des Microsoft-Kontos, um sich bei Windows Mail anzumelden.|  
  
### <a name="store"></a>Speicher  
 Diese Einstellungen gelten nur für Windows Phone 8.1-Geräte.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Anwendungsstore**|Ermöglicht den Zugriff auf den App Store auf dem Gerät.|  
  
### <a name="browser"></a>Browser  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Webbrowser zulassen**|Aktivieren oder Deaktivieren des Standardinternetbrowsers.|  
|**Automatisch ausfüllen**|Benutzer können die Einstellungen für AutoVervollständigen im Browser ändern.|  
|**Active Scripting**|Browser können Skripts ausführen, z. B. ActiveX-Skripts.|  
|**Plug-Ins**|Benutzer können Plug-Ins zu Internet Explorer hinzufügen.|  
|**Popupblocker**|Aktiviert oder deaktiviert den Popupblocker des Browsers.|  
|**Betrugswarnung**|Aktivieren oder deaktivieren von Warnungen zu potenziell betrügerischen Websites.|  
  
### <a name="internet-explorer"></a>Internet Explorer  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Header „Do Not Track“ (Nicht nachverfolgen) immer senden**|Verhindert das Senden von Informationen zum Durchsuchen an Drittanbieterwebsites.|  
|**Intranetsicherheitszone**||  
|**Sicherheitsstufe für Internetzone**|Konfigurieren Sie die Sicherheitsstufe für die Internetzone.|  
|**Sicherheitsstufe für Intranetzone**|Konfigurieren Sie die Sicherheitsstufe für die Intranetzone.|  
|**Sicherheitsstufe für Zone vertrauenswürdiger Sites**|Konfigurieren Sie die Sicherheitsstufe für die Zone vertrauenswürdiger Sites.|  
|**Sicherheitsstufe für Zone eingeschränkter Sites**|Konfigurieren Sie die Sicherheitsstufe für Zone eingeschränkter Sites.|  
|**Namespaces für Intranetzone**||  
|**Durch Eingabe eines einzelnen Worts zu einer Intranetsite wechseln**|Aktiviert oder deaktiviert die Einstellung, die Internet Explorer den automatischen Wechsel zu einer Intranetsite ermöglicht, wenn ein gültiger Sitename ohne voranstehendes „HTTP:“ eingegeben wird.|  
|**Menüoption für Unternehmensmodus**|Ermöglicht Benutzern das Aktivieren und Deaktivieren des Unternehmensmodus über das Internet Explorer-Menü **Extras** .|  
|**Protokollieren des Berichtsspeicherorts (URL)**|Geben Sie eine URL an, unter der besuchte Websites protokolliert werden, wenn der Unternehmensmodus aktiv ist.|  
|**Unternehmensmodus-Websitelistenspeicherort (URL)**|Geben Sie den Speicherort der Liste der Websites an, die den Unternehmensmodus verwenden, wenn er aktiv ist.|  
  
### <a name="cloud"></a>Cloud  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Synchronisierung der Einstellungen**|Ermöglicht die Synchronisierung von Einstellungen zwischen Geräten.|  
|**Synchronisierung der Anmeldeinformationen**|Ermöglicht die Synchronisierung von Anmeldeinformationen zwischen Geräten.|  
|**Microsoft-Konto**|Ermöglicht die Verwendung eines Microsoft-Kontos auf dem Gerät.<br /><br /> (Nur Windows Phone 8.1)|  
|**Synchronisierung von Einstellungen über getaktete Verbindungen**|Ermöglicht die Synchronisierung von Einstellungen, wenn die Internetverbindung getaktet ist.|  
  
### <a name="security"></a>Sicherheit  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Installation nicht signierter Dateien**|Ermöglicht das Laden von nicht signierten Dateien.|  
|**Nicht signierte Anwendungen**|Ermöglicht das Laden von nicht signierten Apps.|  
|**SMS- und MMS-Nachrichten**|Ermöglicht SMS- und MMS-Nachrichten über das Gerät.|  
|**Wechselmedien**|Ermöglicht die Verwendung von Wechselmedien auf dem Gerät, z. B. SD-Karten.|  
|**Kamera**|Ermöglicht die Verwendung der Gerätekamera.|  
|**NFC (Near Field Communication)**|Ermöglicht auf dem Gerät die Kommunikation über NFC.<br /><br /> (Nur Windows Phone 8.1)|  
|**USB-Verbindung zulassen**|Ermöglicht die Verbindung von Peripheriegeräten zu diesem Gerät über USB.|
  
### <a name="peak-synchronization"></a>Hauptzeitsynchronisierung  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Angabe der Hauptzeit**|Legt ein Zeitfenster fest, das von den folgenden beiden Einstellungen verwendet wird.|  
|**Häufigkeit der Hauptzeitsynchronisierung**|Wählen Sie aus, wie oft das Gerät während der Hauptzeit, die Sie angegeben haben, synchronisiert wird.|  
|**Häufigkeit der Nebenzeitsynchronisierung**|Wählen Sie aus, wie oft das Gerät außerhalb der Hauptzeit, die Sie angegeben haben, synchronisiert wird.|  
  
### <a name="roaming"></a>Roaming  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Geräteverwaltung beim Roaming**|Ermöglicht die Verwaltung des Geräts durch Configuration Manager beim Roaming.|  
|**Softwaredownload beim Roaming**|Ermöglicht das Herunterladen von Apps und Software beim Roaming.|  
|**E-Mail-Download beim Roaming**|Ermöglicht E-Mail-Downloads beim Roaming.|  
|**Datenroaming**|Ermöglicht beim Zugriff auf Daten das Roaming zwischen Netzwerken.|  
  
### <a name="encryption"></a>Verschlüsselung  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Speicherkartenverschlüsselung**|Erfordert eine Verschlüsselung, wenn Speicherkarten mit dem Gerät verwendet werden.|  
|**Dateiverschlüsselung auf Gerät**|Erfordert die Verschlüsselung von Dateien auf dem mobilen Gerät.|  
|**E-Mail-Signierung erforderlich**|Erfordert, dass E-Mails vor dem Senden signiert werden.|  
|**Signaturalgorithmus**|Dient zum Auswählen des zum Signieren von E-Mails verwendeten Algorithmus.|  
|**E-Mail-Verschlüsselung erforderlich**|Erfordert, dass E-Mails vor dem Senden verschlüsselt werden.|  
|**Verschlüsselungsalgorithmus**|Dient zum Auswählen des zum Verschlüsseln von E-Mails verwendeten Algorithmus.|  
  
###  <a name="wireless-communications"></a>Funkkommunikation  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Drahtlosnetzwerkverbindung**|Aktivieren oder deaktivieren der WLAN-Funktion der Geräte.|  
|**WLAN-Tethering**|Ermöglicht Benutzern die Verwendung ihres Geräts als mobilen Hotspot.|  
|**Auslagern von Daten an Wi-Fi, wenn möglich**||  
|**Berichterstellung für WLAN-Hotspots**||  
  
##### <a name="to-configure-a-wireless-network-connection"></a>So konfigurieren Sie eine Drahtlosnetzwerkverbindung  
  
1.  Klicken Sie auf der Seite **Einstellungen für die Funkkommunikation mit Mobilgeräten konfigurieren** auf **Hinzufügen**.  
  
2.  Geben Sie im Dialogfeld **Drahtlosnetzwerkverbindung** die folgenden Informationen zur Drahtlosverbindung ein, die auf mobilen Geräten bereitgestellt wird:  
  
|Einstellung|Weitere Informationen|  
|-------------|----------------------|  
|**Netzwerkname (SSID)**||  
|**Netzwerkverbindung**|Wählen Sie **Internet** oder **Arbeit**aus.|  
|**Authentifizierung**|Wählen Sie eine der folgenden Authentifizierungsmethoden für die Drahtlosverbindung aus:<br><br> - **Offen**<br> - **Freigegeben**<br> - **WPA**<br> - **WPA-PSK**<br> - **WPA2**<br> - **WPA2-PSK**|  
|**Datenverschlüsselung**|Wählen Sie die von dieser Verbindung verwendete Verschlüsselungsmethode aus. Die verfügbaren Werte variieren je nach ausgewählter **Authentifizierungsmethode** :<br><br> - **Deaktiviert**<br> - **WEP**<br> - **TKIP**<br> - **AES**|  
|**Schlüsselindex**|Wählen Sie einen Schlüsselindex von **1** bis **4** aus, der mit der Einstellung **WEP** der **Datenverschlüsselung**-verwendet wird.|  
|**Von diesem Netzwerk wird eine Verbindung zum Internet hergestellt**|Wählen Sie diese Option aus, wenn Sie Proxyeinstellungen angeben möchten, mit denen mobile Geräte über eine Drahtlosverbindung eine Verbindung mit dem Internet herstellen können.|  
|**Proxyservereinstellungen**|Geben Sie je nach Bedarf die Einstellungen **Server** und **Port** für **HTTP**, **WAP** und **Sockets**an.|  
|**802.1X-Netzwerkzugriff aktivieren**|Wählen Sie diese Option aus, wenn Sie die Verbindung sichern möchten, indem Sie einen EAP-Typ angeben.|  
|**EAP-Typ**|Wählen Sie den EAP-Typ aus:<br><br> - **PEAP**<br> - **Smartcard oder Zertifikat**|  
    
  
###  <a name="certificates"></a>Zertifikate  
 Ermöglicht Ihnen das Importieren von Zertifikaten für die Installation auf mobilen Geräten.  
  
 Klicken Sie auf **Importieren**, und geben Sie dann folgende Werte an:  
  
-   **Zertifikatsdatei** : Klicken Sie auf **Durchsuchen** , und wählen Sie dann die Zertifikatsdatei mit der Erweiterung **.cer** aus, die Sie importieren möchten.  
  
-   **Zielspeicher** : Wählen Sie mindestens einen Zielspeicher, dem das importierte Zertifikat auf dem mobilen Gerät hinzugefügt wird, unter den folgenden Optionen aus:  
  
    -   **Stamm**  
  
    -   **Zertifizierungsstelle**  
  
    -   **Normal**  
  
    -   **Privilegiert**  
  
    -   **SPC**  
  
    -   **Peer**  
  
-   **Rolle** : Wenn **SPC** (Software Publisher Certificate) als Zielspeicher ausgewählt ist, wählen Sie die Rolle, die dem Zertifikat zugeordnet wird, unter den folgenden Optionen aus:  
  
    -   **Mobilfunkanbieter**  
  
    -   **Verwalter**  
  
    -   **Benutzer authentifiziert**  
  
    -   **IT-Administrator**  
  
    -   **Benutzer nicht authentifiziert**  
  
    -   **Vertrauenswürdiger Bereitstellungsserver**  
  
### <a name="system-security"></a>Systemsicherheit  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Benutzerkontensteuerung**|Aktiviert oder deaktiviert die Windows-Benutzerkontensteuerung auf dem Gerät.|  
|**Netzwerkfirewall**|Aktiviert oder deaktiviert die Windows-Firewall.|  
|**Updates**|Wählen Sie aus, wie Windows-Softwareupdates auf Computer heruntergeladen werden. Sie können z. B. Updates automatisch herunterladen, aber den Zeitpunkt der Installation vom Benutzer auswählen lassen.|  
|**Minimale Klassifizierung von Updates**|Wählen Sie die minimale Klassifizierung von Updates, die auf Windows-Computer heruntergeladen werden: **Keine**, **Wichtig**oder **Empfohlen**.|  
|**SmartScreen**|Aktivieren oder deaktivieren von Windows SmartScreen.|  
|**Virenschutz**|Stellt sicher, dass das Gerät durch Antivirensoftware geschützt ist.|  
|**Virenschutzsignaturen sind aktuell**|Stellt sicher, dass die Antivirensoftwaresignaturen auf dem neuesten Stand sind.|
|**Manuelle Aufhebung der Registrierung zulassen**|Der Benutzer kann sein Gerät aus MDM entfernen.|  
  
### <a name="windows-server-work-folders"></a>Arbeitsordner von Windows Server  
 Diese Einstellungen gelten für Windows Phone 8 und Windows Phone 8.1.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**URL der Arbeitsordner**|Konfiguriert den Speicherort eines Windows Server-Arbeitsordners, mit dem Benutzer über ihr Gerät eine Verbindung herstellen können.|  
  
### <a name="allowed-and-blocked-apps-list-windows-phone-81-only"></a>Liste der zulässigen und blockierten Apps (nur Windows Phone 8.1)  
 Dient zum Angeben einer Liste von Windows Phone-Apps, die in Ihrem Unternehmen kompatibel oder nicht kompatibel sind. Apps, die Sie als blockiert angeben, können von Benutzern nicht installiert werden. Wenn Sie eine Liste zulässiger Apps angeben, können Benutzer nur Apps in der Liste installieren.  
  
 Es ist nicht möglich, zulässige und blockierte Apps im selben Konfigurationselement anzugeben.  
  
> [!IMPORTANT]  
>  Wenn Sie eine Liste zulässiger Apps angeben, müssen Sie sicherstellen, dass die Unternehmensportal-App und andere Apps, die Sie für Windows Phone 8.1-Geräte bereitgestellt haben, in der Liste zulässiger Apps ****  enthalten sind.  
  
##### <a name="to-specify-an-allowed-or-blocked-apps-list"></a>So geben Sie eine Liste zulässiger oder blockierter Apps an  
  
1.  Geben Sie auf der Seite **Liste der zulässigen und blockierten Apps (Windows Phone 8.1)** die folgende Informationen an:  
  
|||  
|-|-|  
|Einstellung|Weitere Informationen|  
|**Liste der blockierten Apps**|Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die Benutzer nicht installieren dürfen.|  
|**Liste der zulässigen Apps**|Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die Benutzer installieren dürfen.|  
|**Hinzufügen**|Fügt eine App zur ausgewählten Liste hinzu. Geben Sie einen Namen Ihrer Wahl und optional den Herausgeber der App an. Geben Sie zudem die URL zur App im App-Store an.<br /><br /> Suchen Sie auf der Seite „Windows Phone Store“ die App, die Sie verwenden möchten, um die URL anzugeben.<br /><br /> **Beispiel:** Durchsuchen Sie den Store nach der App **Skype** . Die URL, die Sie verwenden, ist "http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51".<br /><br /> Für die Unternehmensportal-App oder Branchen-Apps müssen Sie keine vollständige URL, sondern nur die GUID der App angeben.|  
|**Bearbeiten**|Ermöglicht Ihnen das Bearbeiten von Name, Herausgeber und URL der ausgewählten App.|  
|**Entfernen**|Löscht die ausgewählte App aus der Liste.|  
|**Importierenieren**|Importiert eine Liste von Apps, die Sie in einer CSV-Datei angegeben haben. Verwenden Sie in der Datei das Format Anwendungsname, Herausgeber und App-URL.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationselemente für Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)