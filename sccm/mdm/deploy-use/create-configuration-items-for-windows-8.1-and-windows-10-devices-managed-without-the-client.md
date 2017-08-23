---
title: "Erstellen von Konfigurationselementen für Windows 8.1 und Windows 10-Geräte, die mit Intune verwaltet werden | Microsoft-Dokumentation"
description: "Verwenden Sie das Windows 10-Konfigurationselement von System Center Configuration Manager, um die Einstellungen für Windows 10-Computer zu verwalten."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
caps.latest.revision: "20"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: cbfc5f178e72b40526a4cb540f962a3b82203699
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-windows-81-and-windows-10-devices-managed-without-the-system-center-configuration-manager-client"></a>Erstellen von Konfigurationselementen für Windows 8.1- und Windows 10-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden

  
 Verwenden Sie das Konfigurationselement **Windows 8.1- und Windows 10** von System Center Configuration Manager, um Einstellungen für Windows 8.1- und Windows 10-Geräte zu verwalten, die bei Microsoft Intune registriert sind oder lokal von Configuration Manager verwaltet werden.  
  
### <a name="to-create-a-windows-81-and-windows-10-configuration-item"></a>So erstellen Sie ein Konfigurationselement für Windows 8.1 und Windows 10  
  
1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Konformität**.  
  
2.  Erweitern Sie im Arbeitsbereich **Bestand und Konformität** die **Konformitätseinstellungen**, und klicken Sie auf **Konfigurationselemente**.  
  
3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  
  
4.  Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  
  
5.  Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Windows 8.1 und Windows 10**aus.  
  
6.  Klicken Sie auf **Kategorien**, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  
  
7.  Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die jeweiligen Windows-Plattformen zur Bewertung des Konfigurationselements aus.  
  
8.  Wählen Sie auf der Seite **Geräteeinstellungen** des Assistenten die Einstellungsgruppe aus, die Sie konfigurieren möchten. Informieren Sie sich in diesem Thema unter [Referenz zu Einstellungen des Konfigurationselements für Windows 8.1 und Windows 10](#BKMK_Setref) über die Details, und klicken Sie dann auf **Weiter**.  
  
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
  
##  <a name="windows-81-and-windows-10-configuration-item-settings-reference"></a>Referenz zu Einstellungen des Konfigurationselements für Windows 8.1 und Windows 10  
  
### <a name="password"></a>Kennwort  
 Diese Einstellungen gelten nur für Geräte unter Windows 10 und höher.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Kennworteinstellungen auf Geräten erforderlich**|Auf unterstützten Geräten ein Kennwort erfordern.|  
|**Minimale Kennwortlänge (Zeichen)**|Die Mindestlänge für das Kennwort.|  
|**Kennwortablauf in Tagen**|Die Anzahl der Tage, bevor ein Kennwort geändert werden muss.|  
|**Anzahl der gespeicherten Kennwörter**|Verhindert die Wiederverwendung zuvor verwendeter Kennwörter.|  
|**Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts**|Setzt das Gerät zurück, wenn diese Anzahl von Anmeldeversuchen fehlschlägt.|  
|**Leerlaufzeit vor dem Sperren des Geräts**|Geben Sie die Zeitdauer an, die ein Gerät im Leerlauf sein darf (ohne Benutzereingabe), bevor es gesperrt ist.|  
|**Kennwortkomplexität**|Wählen Sie aus, ob Sie eine PIN wie „1234“ angeben können oder, ob ein sicheres Kennwort erforderlich ist.|  
|**Kennwortqualität**|Wählen Sie den erforderlichen Grad der Kennwortkomplexität aus. Wählen Sie zudem aus, ob biometrische Geräte zulässig sind.|  
|**Kennwortwiederherstellungs-PIN an Exchange Server senden**|-|
|**Geräteverschlüsselung**|aktiviert die Verschlüsselung auf Geräten, für die diese Einstellung gilt|  
  
###  <a name="device"></a>Gerät  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Bildschirmaufnahme**|Ermöglicht die Aufnahme eines Screenshots der Geräteanzeige.<br /><br /> (ausschließlich Windows 10)|  
|**Übermittlung von Diagnosedaten**|Ermöglicht die Übermittlung von Protokolldateien der App.<br /><br /> (ausschließlich Windows 8.1)|  
|**Übermittlung von Diagnosedaten (Windows 10)**|Ermöglicht die Übermittlung von Protokolldateien der App.<br /><br /> (ausschließlich Windows 10)|  
|**Geolocation**|Ermöglicht dem Gerät die Verwendung von Ortungsdienstinformationen.<br /><br /> (ausschließlich Windows 10)|  
|**Kopieren und Einfügen**|Verwenden Sie zum Übertragen von Daten zwischen Apps das Kopieren und Einfügen.<br /><br /> (ausschließlich Windows 10)|
|**Zurücksetzen auf Werkseinstellungen**|Der Endbenutzer kann das Gerät auf die ursprünglichen Einstellungen zurücksetzen.<br /><br /> (ausschließlich Windows 10)|  
|**Bluetooth**|Ermöglicht die Verwendung der Bluetooth-Funktion des Geräts.|  
|**Sichtbarer Modus für Bluetooth**|Ermöglicht die Ermittlung anderer Bluetooth-Geräte durch das Gerät.<br /><br /> (ausschließlich Windows 10)|  
|**Bluetooth-Werbung**|Ermöglicht die Verwendung von Bluetooth-Werbung.<br /><br /> (ausschließlich Windows 10)|  
|**Sprachaufzeichnung**|Ermöglicht die Verwendung von Sprachaufzeichnungsfeatures auf dem Gerät.<br /><br /> (ausschließlich Windows 10)|
|**Cortana**|Ermöglicht die Verwendung des Sprach-Assistenten Cortana.<br /><br /> (ausschließlich Windows 10)|
|**Info-Center-Benachrichtigungen**|Aktivieren oder Deaktivieren des Bereichs „Benachrichtigung“ in Windows 10. <br /><br /> (ausschließlich Windows 10)|
|**Änderung der Regionseinstellungen (nur Desktop)**|hindert Benutzer daran, die Regionseinstellungen auf dem Gerät zu ändern.|
|**Änderung der Energie- und Energiesparmoduseinstellungen (nur für Desktopcomputer)**|hindert Benutzer daran, die Einstellungen für die Stromversorgung und den Standbymodus zu ändern|
|**Änderung der Spracheinstellungen (nur Desktop)**|hindert Benutzer daran, die Spracheinstellungen auf dem Gerät zu ändern|
|**Änderung der Systemzeit**|hindert Benutzer daran, die Systemzeit auf dem Gerät zu ändern.|
|**Änderung des Gerätenamens**|hindert Benutzer daran, den Gerätenamen zu ändern|
  
### <a name="email-management"></a>E-Mail-Verwaltung  
 Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**POP- und IMAP-E-Mail**|Ermöglicht die Verbindung mit E-Mail-Konten, die POP- und IMAP-Standards verwenden.|  
|**Maximale Zeitdauer für die Speicherung von E-Mails**|Dauer der Speicherung von E-Mails, bevor sie vom Server gelöscht werden.|  
|**Zulässige Nachrichtenformate**|Geben Sie an, ob E-Mails HTML oder Nur-Text verwenden können.|  
|**Maximale Größe für E-Mails im Nur-Text-Format (automatisch heruntergeladen)**|Steuert die maximale Größe für E-Mails im Nur-Text-Format beim automatischen Herunterladen.|  
|**Maximale Größe für E-Mails im HTML-Format (automatisch heruntergeladen)**|Steuert die maximale Größe für E-Mails im HTML-Format beim automatischen Herunterladen.|  
|**Maximale Größe eines Anhangs (automatisch heruntergeladen)**|legt fest, bis zu welcher Größe E-Mails automatisch heruntergeladen werden.|  
|**Kalendersynchronisierung**|Ermöglicht die Synchronisierung von Kalendern mit dem Gerät.|  
|**Benutzerdefiniertes E-Mail-Konto**|Ermöglicht die Verwendung eines Nicht-Microsoft-Kontos auf dem Gerät.|  
|**Microsoft-Konto in Windows Mail-App optional machen**|Konfigurieren Sie diese Option, wenn ein Microsoft-Konto in Windows Mail nicht zwingend erforderlich sein soll.|  
  
### <a name="store"></a>Speicher  
 Diese Einstellungen gelten nur für Geräte unter Windows 10 und höher.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Anwendungsstore**|Ermöglicht den Zugriff auf den App Store auf dem Gerät.|  
|**Geben Sie ein Kennwort für den Zugriff auf den Anwendungsstore ein.**|Benutzer müssen ein Kennwort für den Zugriff auf den App Store eingeben.|  
|**In-App-Käufe**|Bietet Benutzern die Möglichkeit zu In-App-Käufen.|
|**Apps aus Store automatisch aktualisieren**|Apps aus dem Windows Store können automatisch aktualisiert werden|
|**Nur privaten Store verwenden**|Aktivieren Sie diese Option, um Benutzern das Herunterladen von Apps aus Ihrem privaten Store zu erlauben.|
|**Store-App starten**|Mit dieser Option deaktivieren Sie auf Geräten alle Apps, die vorinstalliert waren oder aus dem Windows Store heruntergeladen wurden.|
  
### <a name="browser"></a>Browser  
 Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Webbrowser zulassen**|Mit dieser Option wird die Verwendung des Webbrowsers auf dem Gerät zugelassen.|  
|**Automatisch ausfüllen**|Benutzer können die Einstellungen für AutoVervollständigen im Browser ändern.|  
|**Active Scripting**|Browser können Skripts ausführen, z. B. ActiveX-Skripts.|  
|**Plug-Ins**|Benutzer können Plug-Ins zu Internet Explorer hinzufügen.|  
|**Popupblocker**|Aktiviert oder deaktiviert den Popupblocker des Browsers.|  
|**Cookies**|Ermöglicht das Speichern von Cookies auf dem Gerät.|  
|**Betrugswarnung**|Aktivieren oder deaktivieren von Warnungen zu potenziell betrügerischen Websites.|  
  
###  <a name="internet-explorer"></a>Internet Explorer  
 Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Header „Do Not Track“ (Nicht nachverfolgen) immer senden**|Verhindert das Senden von Informationen zum Durchsuchen an Drittanbieterwebsites.|  
|**Intranetsicherheitszone**|Weisen Sie der Intranetsicherheitszone eine Sicherheitsstufe zu.|  
|**Sicherheitsstufe für Internetzone**|Konfigurieren Sie die Sicherheitsstufe für die Internetzone.|  
|**Sicherheitsstufe für Intranetzone**|Konfigurieren Sie die Sicherheitsstufe für die Intranetzone.|  
|**Sicherheitsstufe für Zone vertrauenswürdiger Sites**|Konfigurieren Sie die Sicherheitsstufe für die Zone vertrauenswürdiger Sites.|  
|**Sicherheitsstufe für Zone eingeschränkter Sites**|Konfigurieren Sie die Sicherheitsstufe für Zone eingeschränkter Sites.|  
|**Namespaces für Intranetzone**|Konfigurieren Sie Websites, die der Intranetzone hinzugefügt oder daraus entfernt werden.|  
|**Durch Eingabe eines einzelnen Worts zu einer Intranetsite wechseln**|Aktiviert oder deaktiviert die Einstellung, die Internet Explorer den automatischen Wechsel zu einer Intranetsite ermöglicht, wenn ein gültiger Sitename ohne voranstehendes „HTTP:“ eingegeben wird.|  
|**Menüoption für Unternehmensmodus**|Ermöglicht Benutzern das Aktivieren und Deaktivieren des Unternehmensmodus über das Internet Explorer-Menü **Extras** .|  
|**Protokollieren des Berichtsspeicherorts (URL)**|Geben Sie eine URL an, unter der besuchte Websites protokolliert werden, wenn der Unternehmensmodus aktiv ist.|  
|**Unternehmensmodus-Websitelistenspeicherort (URL)**|Geben Sie den Speicherort der Liste der Websites an, die den Unternehmensmodus verwenden, wenn er aktiv ist.|  
  
###  <a name="cloud"></a>Cloud  
 Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.  
  
|Name der Einstellung|Details|Windows 8.1|Windows 10|  
|------------------|-------------|-----------------|----------------|  
|**Synchronisierung der Einstellungen**|Ermöglicht die Synchronisierung von Einstellungen zwischen Geräten.|Ja|Ja|  
|**Synchronisierung der Anmeldeinformationen**|Ermöglicht die Synchronisierung von Anmeldeinformationen zwischen Geräten.|Ja|Ja|  
|**Microsoft-Konto**|Ermöglicht die Verwendung eines Microsoft-Kontos auf dem Gerät.|Ja|Ja|  
|**Synchronisierung von Einstellungen über getaktete Verbindungen**|Ermöglicht die Synchronisierung von Einstellungen, wenn die Internetverbindung getaktet ist.|Ja|Ja|  
  
###  <a name="security"></a>Sicherheit  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Installation nicht signierter Dateien**|Ermöglicht das Laden von nicht signierten Dateien.<br /><br /> (ausschließlich Windows 10)|  
|**Nicht signierte Anwendungen**|Ermöglicht das Laden von nicht signierten Apps.<br /><br /> (ausschließlich Windows 10)|  
|**SMS- und MMS-Nachrichten**|Ermöglicht SMS- und MMS-Nachrichten über das Gerät.<br /><br /> (ausschließlich Windows 10)|  
|**Wechselmedien**|Ermöglicht die Verwendung von Wechselmedien auf dem Gerät, z. B. SD-Karten.<br /><br /> (ausschließlich Windows 10)|  
|**Kamera**|Ermöglicht die Verwendung der Gerätekamera.<br /><br /> (ausschließlich Windows 10)|  
|**NFC (Near Field Communication)**|Ermöglicht auf dem Gerät die Kommunikation über NFC.<br /><br /> (ausschließlich Windows 10)|  
|**Diebstahlschutzmodus**|Steuert, ob der Windows 10-Diebstahlschutzmodus aktiviert ist.<br /><br /> (ausschließlich Windows 10)|  
|**USB-Verbindung zulassen**|Verbindung von Geräten zu diesem Gerät über eine USB-Verbindung.<br /><br /> (ausschließlich Windows 10)|
|**Profildatei**|Stellt ein VPN-Profil für Windows RT-Geräte bereit.<br /><br /> (ausschließlich Windows 8.1)|  
|**Profilname**|Stellt ein VPN-Profil für Windows RT-Geräte bereit.<br /><br /> (ausschließlich Windows 8.1)|  
|**Profil für alle Benutzer**|Stellt ein VPN-Profil für Windows RT-Geräte bereit.<br /><br /> (ausschließlich Windows 8.1)|  
  
###  <a name="peak-synchronization"></a>Hauptzeitsynchronisierung  
 Diese Einstellungen gelten nur für Geräte unter Windows 10 und höher.  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Angabe der Hauptzeit**|Geben Sie die Hauptzeit für die Synchronisierung von mobilen Geräten an.|  
|**Häufigkeit der Hauptzeitsynchronisierung**|Konfigurieren Sie, wie oft die Synchronisierung während der festgelegten Hauptzeiten durchgeführt wird.|  
|**Häufigkeit der Nebenzeitsynchronisierung**|Konfigurieren Sie, wie oft die Synchronisierung außerhalb der festgelegten Hauptzeiten durchgeführt wird.|  
  
###  <a name="roaming"></a>Roaming  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Geräteverwaltung beim Roaming**|Ermöglicht die Verwaltung des Geräts durch Configuration Manager beim Roaming.<br /><br /> (ausschließlich Windows 10)|  
|**Softwaredownload beim Roaming**|Ermöglicht das Herunterladen von Apps und Software beim Roaming.<br /><br /> (ausschließlich Windows 10)|  
|**E-Mail-Download beim Roaming**|Ermöglicht E-Mail-Downloads beim Roaming.<br /><br /> (ausschließlich Windows 10)|  
|**Datenroaming**|Ermöglicht beim Zugriff auf Daten das Roaming zwischen Netzwerken.| 
|**VPN über Mobilfunknetz**|Das Gerät kann während einer Verbindung zum Mobilfunknetz auf VPN-Verbindungen zugreifen.<br /><br /> (ausschließlich Windows 10)|
|**VPN-Roaming über Mobilfunknetz**|Das Gerät kann während des Roamings über ein Mobilfunknetz auf VPN-Verbindungen zugreifen.<br /><br /> (ausschließlich Windows 10)| 
  
###  <a name="encryption"></a>Verschlüsselung  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Speicherkartenverschlüsselung**|Erfordert eine Verschlüsselung, wenn Speicherkarten mit dem Gerät verwendet werden.<br /><br /> (ausschließlich Windows 10)|  
|**Dateiverschlüsselung auf Gerät**|Erfordert die Verschlüsselung der Dateien auf dem Gerät.|  
|**E-Mail-Signierung erforderlich**|Erfordert, dass E-Mails vor dem Senden signiert werden.|  
|**Signaturalgorithmus**|Wählt den Signaturalgorithmus für signierte E-Mails aus.|  
|**E-Mail-Verschlüsselung erforderlich**|Erfordert, dass E-Mails vor dem Senden verschlüsselt werden.|  
|**Verschlüsselungsalgorithmus**|Wählt den Algorithmus zum Verschlüsseln von E-Mails aus.|  
  
###  <a name="wireless-communications"></a>Funkkommunikation  
 Diese Einstellungen gelten nur für Geräte unter Windows 10 und höher.  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Drahtlosnetzwerkverbindung**|Aktivieren oder deaktivieren der WLAN-Funktion der Geräte.|  
|**WLAN-Tethering**|Ermöglicht Benutzern die Verwendung ihres Geräts als mobilen Hotspot.|  
|**Auslagern von Daten an Wi-Fi, wenn möglich**|Konfigurieren Sie diese Option, um wenn möglich die WLAN-Verbindung auf dem Gerät zu verwenden.|  
|**Berichterstellung für WLAN-Hotspots**|-|  
|**Manuelle WLAN-Konfiguration**|-|  
  
#### <a name="to-configure-a-wireless-network-connection"></a>So konfigurieren Sie eine Drahtlosnetzwerkverbindung  
  
1.  Klicken Sie auf der Seite **Einstellungen für die Funkkommunikation mit Mobilgeräten konfigurieren** auf **Hinzufügen**.  
  
2.  Geben Sie im Dialogfeld **Drahtlosnetzwerkverbindung** die folgenden Informationen zur Drahtlosverbindung ein, die auf mobilen Geräten bereitgestellt wird:  
  
|Einstellung|Weitere Informationen|  
|-------------|----------------------|  
|**Netzwerkname (SSID)**|Geben Sie den Namen des WLAN-Netzwerks ein.|  
|**Netzwerkverbindung**|Wählen Sie **Internet** oder **Arbeit**aus.|  
|**Authentifizierung**|Wählen Sie eine der folgenden Authentifizierungsmethoden für die Drahtlosverbindung aus:<br /><br /> - **Offen**<br /><br /> - **Freigegeben**<br /><br /> - **WPA**<br /><br /> - **WPA-PSK**<br /><br /> - **WPA2**<br /><br /> - **WPA2-PSK**|  
|**Datenverschlüsselung**|Wählen Sie die von dieser Verbindung verwendete Verschlüsselungsmethode aus. Die verfügbaren Werte variieren je nach ausgewählter **Authentifizierungsmethode** :<br /><br /> - **Deaktiviert**<br /><br /> - **WEP**<br /><br /> - **TKIP**<br /><br /> - **AES**|  
|**Schlüsselindex**|Wählen Sie einen Schlüsselindex von **1** bis **4** aus, der mit der Einstellung **WEP** der **Datenverschlüsselung**-verwendet wird.|  
|**Von diesem Netzwerk wird eine Verbindung zum Internet hergestellt**|Wählen Sie diese Option aus, wenn Sie Proxyeinstellungen angeben möchten, mit denen mobile Geräte über eine Drahtlosverbindung eine Verbindung mit dem Internet herstellen können.|  
|**Proxyservereinstellungen**|Geben Sie je nach Bedarf die Einstellungen **Server** und **Port** für **HTTP**, **WAP** und **Sockets**an.|  
|**802.1X-Netzwerkzugriff aktivieren**|Wählen Sie diese Option aus, wenn Sie die Verbindung sichern möchten, indem Sie einen EAP-Typ angeben.|  
|**EAP-Typ**|Wählen Sie den EAP-Typ aus:<br /><br /> - **PEAP**<br> - **Smartcard oder Zertifikat**|  
  
  
  
### <a name="certificates"></a>Zertifikate  
 Ermöglicht Ihnen das Importieren von Zertifikaten für die Installation auf mobilen Geräten.  
  
 Klicken Sie auf **Importieren**, und geben Sie dann folgende Werte an:  
  
-   **Zertifikatsdatei** : Klicken Sie auf "Durchsuchen", und wählen Sie dann die Zertifikatsdatei mit der Erweiterung **.cer** aus, die Sie importieren möchten.  
  
-   **Zielspeicher** : Wählen Sie mindestens einen Zielspeicher, dem das importierte Zertifikat auf dem mobilen Gerät hinzugefügt wird, aus den folgenden Optionen aus:  
  
    -   **Stamm**  
  
    -   **Zertifizierungsstelle**  
  
    -   **Normal**  
  
    -   **Privilegiert**  
  
    -   **SPC**  
  
    -   **Peer**  
  
-   **Rolle** : Wenn **SPC** (Software Publisher Certificate) als Zielspeicher ausgewählt ist, wählen Sie die Rolle, die dem Zertifikat zugeordnet ist, aus den folgenden Optionen aus:  
  
    -   **Mobilfunkanbieter**  
  
    -   **Verwalter**  
  
    -   **Benutzer authentifiziert**  
  
    -   **IT-Administrator**  
  
    -   **Benutzer nicht authentifiziert**  
  
    -   **Vertrauenswürdiger Bereitstellungsserver**  
  
### <a name="system-security"></a>Systemsicherheit  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Benutzerkontensteuerung**|Aktiviert oder deaktiviert die Windows-Benutzerkontensteuerung auf dem Gerät.|  
|**Netzwerkfirewall**|Aktiviert oder deaktiviert die Windows-Firewall.<br /><br /> (ausschließlich Windows 8.1)|  
|**Updates (Windows 8.1 und früher)**|Wählen Sie aus, wie Windows-Softwareupdates auf Computer heruntergeladen werden. Sie können z. B. Updates automatisch herunterladen, aber den Zeitpunkt der Installation vom Benutzer auswählen lassen.|  
|**Minimale Klassifizierung von Updates**|Wählen Sie aus, welche Klassifikation Updates mindestens aufweisen müssen, um auf Windows-Computer heruntergeladen zu werden: **Keine**, **Wichtig**oder **Empfohlen**.|  
|**Updates (Windows 10)**|Wählen Sie aus, wie Windows-Softwareupdates auf Computer heruntergeladen werden. Sie können z. B. Updates automatisch herunterladen, aber den Zeitpunkt der Installation vom Benutzer auswählen lassen.<br /><br /> (ausschließlich Windows 10)|  
|**Installationstag**|Wählen Sie den Tag aus, an dem Updates installiert werde sollen.<br /><br /> (ausschließlich Windows 10)|  
|**Installationszeit**|Wählen Sie die Uhrzeit aus, zu der Updates installiert werden sollen.<br /><br /> (ausschließlich Windows 10)|  
|**SmartScreen**|Aktivieren oder deaktivieren von Windows SmartScreen.|  
|**Virenschutz**|Stellt sicher, dass Antivirensoftware auf dem Gerät installiert ist.|  
|**Virenschutzsignaturen sind aktuell**|Stellt sicher, dass die Antivirensignaturdateien auf dem neuesten Stand sind.|  
|**Funktionen des Vorabreleases**|Ermöglicht Microsoft, Einstellungen und Features von Vorabversionen auf dem Gerät bereitzustellen.<br /><br /> (ausschließlich Windows 10)|  
|**Manuelle Installation von Stammzertifikaten**|(ausschließlich Windows 10)| 
|**Manuelle Aufhebung der Registrierung zulassen**|Ermöglicht dem Benutzer, die Verwaltung über eine MDM-Lösung aufzuheben.| 
  
###  <a name="windows-server-work-folders"></a>Arbeitsordner von Windows Server  
 Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**URL der Arbeitsordner**|Konfiguriert den Speicherort eines Windows Server-Arbeitsordners, mit dem Benutzer über ihr Gerät eine Verbindung herstellen können.|  
  
### <a name="allowed-and-blocked-apps-windows-phone-only"></a>Zulässige und blockierte Apps (nur Windows Phone)  
 Sie können eine Liste von Apps angeben, die von Intune verwaltet werden und die entweder in Ihrem Unternehmen als kompatibel oder als nicht kompatibel betrachtet werden. Windows Phone kann die Installation dieser Apps zulassen oder blockieren.  
  
 Es ist nicht möglich, kompatible und nicht kompatible Apps im selben Konfigurationselement anzugeben.  
  
#### <a name="to-specify-apps-that-are-allowed-or-blocked"></a>Apps angeben, die zugelassen oder blockiert werden  
  
Geben Sie auf der Seite **Liste zulässiger oder blockierter Apps** die folgenden Informationen an:  
  
|Einstellung|Weitere Informationen|  
    |-------------|----------------------|  
    |**Liste der blockierten Apps**|Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die Benutzer nicht installieren dürfen.|  
    |**Liste der zulässigen Apps**|Wählen Sie diese Option aus, wenn Sie eine Liste von Apps angeben möchten, die Benutzer installieren dürfen. Die Installation aller anderen Apps wird blockiert.|  
    |**Hinzufügen**|Fügt eine App zur ausgewählten Liste hinzu. Geben Sie einen Namen Ihrer Wahl sowie die URL zur App im App-Store und optional den Herausgeber der App an.<br /><br /> Zum Angeben der URL suchen Sie im Windows Store die App, die Sie verwenden möchten.<br /><br /> Öffnen Sie die Seite der App, und kopieren Sie die URL in die Zwischenablage. Sie können diese URL nun in der Liste kompatibler oder nicht kompatibler Apps verwenden.<br /><br /> **Beispiel:** Durchsuchen Sie den Store nach der App **Skype** . Die von Ihnen verwendete URL lautet **http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**.|  
    |**Bearbeiten**|Ermöglicht Ihnen das Bearbeiten von Name, Herausgeber und URL der ausgewählten App.|  
    |**Entfernen**|Löscht die ausgewählte App aus der Liste.|  
    |**Importierenieren**|Importiert eine Liste von Apps, die Sie in einer CSV-Datei angegeben haben. Verwenden Sie in der Datei das Format Anwendungsname, Herausgeber und App-URL.|  
  
### <a name="windows-10-team"></a>Windows 10 Team  
 Diese Einstellungen gelten nur für Geräte unter Windows 10 Team.  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Zulassen der automatischen Aktivierung des Bildschirms, wenn Sensoren eine Person im Raum erkennen**|Ermöglicht das automatische Aktivieren des Geräts, wenn der Sensor eine Person im Raum erkennt.|  
|**Erforderliche PIN für drahtlose Projektion**|Gibt an, ob Sie eine PIN eingeben müssen, bevor Sie die drahtlosen Projektionsfunktionen des Geräts verwenden können.|  
|**Wartungsfenster**|Konfiguriert das Fenster, in dem Updates am Gerät vorgenommen werden können. Sie können die Startzeit und Länge des Fensters (1 bis 5 Stunden) konfigurieren.|
|**Azure Operational Insights**|Azure Operational Insights, Teil der Microsoft Operations Manager-Suite, sammelt, speichert und analysiert Daten aus Protokolldateien von Windows 10 Team-Geräten.<br>Zum Herstellen einer Verbindung mit Azure Operational Insights geben Sie eine Arbeitsbereichs-ID und einen Arbeitsbereichsschlüssel ein.| 
|**Miracast-Funkprojektion**|Aktivieren Sie diese Option, wenn Sie dem Windows 10 Team-Gerät ermöglichen möchten, Miracast-fähige Geräte für die Projektion zu verwenden.<br>Wenn Sie diese Option aktivieren, wählen Sie unter **Miracast-Kanal wählen** den zum Projizieren von Inhalten verwendeten Miracast-Kanal aus.|
|**Besprechungsinformationen auf Willkommensbildschirm anzeigen**|Wenn Sie diese Option aktivieren, können Sie die Informationen auswählen, die auf der Kachel **Besprechungen** des Bildschirms **Willkommen** angezeigt werden. Sie können:<br><br>- **Nur Organisator und Zeit anzeigen**<br>- **Organisator, Zeit und Thema anzeigen (Thema bei privaten Besprechungen ausblenden)**|
|**URL zum Bild für den Sperrbildschirmhintergrund**|Verwenden Sie diese Einstellung, um auf dem Bildschirm **Willkommen** von Windows 10 Team-Geräten einen benutzerdefinierten Hintergrund aus der angegebenen URL anzuzeigen.<br>Das Bild muss im PNG-Format vorliegen, und die URL muss mit **https://** beginnen.| 
  
### <a name="windows-information-protection"></a>Windows Information Protection  

Mit dem Anstieg von Geräten im Besitz der Mitarbeiter im Unternehmen entsteht auch ein höheres Risiko unbeabsichtigter Datenpreisgabe durch Apps und Dienste, z.B. E-Mail, soziale Medien und die öffentliche Cloud, die sich außerhalb der Kontrolle des Unternehmens befinden. Wenn ein Mitarbeiter beispielsweise die aktuellsten technischen Zeichnungen von seinem privaten E-Mail-Konto versendet, Produktinformationen kopiert und in einen Tweet einfügt oder einen Verkaufsbericht, der sich in Bearbeitung befindet, im öffentlichen Cloudspeicher speichert.

Windows Information Protection (WIP) bietet hierbei einen Schutz gegen potenzielle Datenlecks, ohne dass die Benutzerfreundlichkeit für die Mitarbeiter darunter leidet. WIP schützt auch Unternehmens-Apps und -daten vor unbeabsichtigter Datenpreisgabe auf unternehmenseigenen und privaten Geräten, die Mitarbeiter mit zur Arbeit bringen, ohne dass Änderungen in Ihrer Umgebung oder anderen Apps nötig sind.

 Die Einstellungen der Configuration Manager WIP-Konfigurationselemente verwalten die Liste der von EDP geschützten Apps, Unternehmens-Netzwerkadressen, Schutzebenen und Verschlüsselungseinstellungen.

Weitere Informationen zum Konfigurieren des Unternehmensdatenschutzes mit Configuration Manager finden Sie unter [Schützen von Unternehmensdaten mit Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).


### <a name="microsoft-edge"></a>Microsoft Edge  
Diese Einstellungen gelten für Geräte unter Windows 10 und höher.  
  
|Name der Einstellung|Details|  
|------------------|-------------| 
|Microsoft Edge|Verwendung des Webbrowsers Microsoft Edge auf dem Gerät zulassen| 
|**Suchvorschläge in Adressleiste zulassen**|Ermöglicht der Suchmaschine, schon während der Eingabe von Suchausdrücken Websites vorzuschlagen.|  
|**Übertragung des Intranetdatenverkehrs an Internet Explorer zulassen**||  
|**Nicht verfolgen (Do not track) zulassen**|„Do Not Track“ teilt Websites mit, dass sie Ihren Besuch nicht verfolgen sollen.|  
|**SmartScreen aktivieren**|Verwenden Sie SmartScreen, um von den Benutzern heruntergeladene Dateien auf Schadsoftware zu überprüfen.|  
|**Popups zulassen**|Mit dieser Option werden Browser-Popups zugelassen oder deaktiviert.|  
|**Cookies zulassen**|Mit dieser Option werden Cookies zugelassen oder deaktiviert.|  
|**AutoAusfüllen zulassen**|Mit dieser Option wird das AutoAusfüllen-Feature des Edge-Browsers zugelassen.|  
|**Kennwort-Manager zulassen**|Mit dieser Option wird die Kennwort-Manager-Feature des Edge-Browsers zugelassen.|  
|**Speicherort der Standortliste für Enterprise-Modus**|Gibt an, wo Sie die Liste der Websites finden, die im Unternehmensmodus geöffnet werden. Benutzer können diese Liste nicht bearbeiten.|
|**Zugriff auf about:flags-Seite blockieren**|Verhindern, dass Benutzer in Edge Zugriff auf die Seite about:flags erhalten, die Entwicklereinstellungen und experimentellen Einstellungen enthält.|
|**Außerkraftsetzen von SmartScreen-Aufforderung verhindern**|Zulassen dass Benutzer Warnungen des SmartScreen-Filters umgehen, mit denen sie vor potenziell schädlichen Websites gewarnt werden.|
|**Außerkraftsetzen von SmartScreen-Aufforderung für Dateien verhindern**|Zulassen dass Benutzer Warnungen des SmartScreen-Filters umgehen, mit denen sie vor dem Download potenziell schädlicher Dateien gewarnt werden.|
|**WebRTC-LocalHost-IP-Adresse**|Blockieren Sie die Anzeige der localhost-IP-Adresse der Benutzer beim Telefonieren über das Protokoll WebRTC.|
|**Standardsuchmodul**|Geben Sie die standardmäßige Suchmaschine an. Die Benutzer können dies jedoch jederzeit ändern.|
|**OpenSearch-XML-URL**|Sie können eine OpenSearch XML-Datei verwenden, um einen Suchdienst für Microsoft Edge zu erstellen.<br>Weitere Informationen finden Sie im Artikel [OpenSearch](https://msdn.microsoft.com/library/windows/desktop/dd940337)|
|**Homepages (nur Desktop)**|Fügen Sie eine Liste der Seiten hinzu, die in Edge als Startseiten verwendet werden sollen (nur für Desktopcomputer).|  


### <a name="windows-defender"></a>Windows Defender
Diese Einstellungen gelten für Geräte unter Windows 10 und höher.
 
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Echtzeitüberwachung zulassen**|Ermöglicht die Echtzeitüberprüfung auf Schadsoftware, Spyware und andere unerwünschte Software.|
|**Verhaltensüberwachung zulassen**|Erlaubt Defender, Geräte auf bestimmte bekannte verdächtige Aktivitätsmuster zu überprüfen.|
|**Netzwerkinspektionssystem aktivieren**|Das Netzwerkinspektionssystem (NIS) trägt zum Schutz von Geräten vor netzwerkbasierten Angriffen bei, indem es Signaturen bekannter Sicherheitsrisiken aus dem Microsoft-Endpoint Protection-Center verwendet, um schädlichen Datenverkehr zu ermitteln und zu blockieren.|
|**Alle heruntergeladene Dateien überprüfen**|Steuert, ob Defender alle aus dem Internet heruntergeladenen Dateien überprüft.|
|**Skriptüberprüfung zulassen**|Ermöglicht Defender die Überprüfung von Skripts, die in Internet Explorer verwendet werden.|
|**Datei- und Programmaktivität überwachen**|Defender überwacht die Datei- und Programmaktivität auf Geräten.
|**Tage für Nachverfolgung behandelter Schadsoftware**|Ermöglicht Defender die Nachverfolgung behandelter Schadsoftware für die angegebene Anzahl von Tage, damit Sie zuvor Geräte betroffene Geräte manuell überprüfen können. Wenn Sie die Anzahl der Tage auf 0 festlegen, verbleibt die Schadsoftware im Quarantäneordner und wird nicht automatisch entfernt.|
|**Clientzugriff auf Benutzeroberfläche zulassen**|Steuert, ob die Benutzeroberfläche von Windows Defender für Benutzer ausgeblendet ist.<br>Wird diese Einstellung geändert, wird die Änderung mit dem nächsten Neustart des Benutzer-PCs wirksam.|
|**Systemüberprüfung planen**|Sie können eine vollständige oder schnelle Systemüberprüfung planen, die regelmäßig am ausgewählten Tag und zur angegebenen Uhrzeit stattfindet.|
|**Eine tägliche Schnellüberprüfung planen**|Ermöglicht Ihnen, eine Schnellüberprüfung zu planen, die täglich zur ausgewählten Uhrzeit erfolgt.
|**CPU-Nutzung während einer Überprüfung begrenzen**|Hiermit können Sie die CPU-Menge, die von den Überprüfungen genutzt werden darf, einschränken (von 1 bis 100).|
|**Archivdateien überprüfen**|Ermöglicht Defender das Überprüfen von Archivdateien wie ZIP- oder CAB-Dateien.|
|**E-Mail-Nachrichten überprüfen**|Ermöglicht Defender das Überprüfen von E-Mail-Nachrichten beim Eingang auf dem Gerät.|
|**Wechseldatenträger überprüfen**|Ermöglicht Defender das Überprüfen von Wechseldatenträgern wie z.B. USB-Sticks.|
|**Zugeordnete Laufwerke überprüfen**|Ermöglicht Defender das Überprüfen von Dateien auf zugeordneten Netzlaufwerken.<br>Wenn die Dateien auf dem Laufwerk schreibgeschützt sind, kann Defender eventuell gefundene Schadsoftware nicht entfernen.|
|**In freigegebenen Netzwerkordnern geöffnete Dateien überprüfen**|Ermöglicht Defender das Überprüfen von Dateien auf freigegebenen Netzlaufwerken (z.B. Dateien, auf die über einen UNC-Pfad zugegriffen wird.<br>Wenn die Dateien auf dem Laufwerk schreibgeschützt sind, kann Defender eventuell gefundene Schadsoftware nicht entfernen.|
|**Intervall zum Aktualisieren von Signaturen**|Gibt an, in welchem Intervall Defender nach neuen Signaturdateien suchen soll.
|**Cloudschutz zulassen**|Zulassen oder Blockieren, dass Microsoft Active Protection Service Informationen über Schadsoftwareaktivität von verwalteten Geräten empfängt. Diese Daten werden zur Verbesserung des Diensts für die Zukunft verwendet.|
|**Beim Senden von Beispielen beim Benutzer nachfragen**|Steuert, ob Dateien automatisch an Microsoft gesendet werden, wenn möglicherweise erst durch eine weitere Analyse festgestellt werden kann, ob sie schädlich sind.|
|**Erkennung potenziell unerwünschter Anwendungen**|Schützt registrierte Windows-Desktopgeräte vor dem Ausführen von Software, die von Windows Defender als potenziell unerwünscht eingestuft wird. Sie können sich vor dem Ausführen dieser Anwendungen schützen, oder den Überwachungsmodus verwenden, um bei der Installation einer potenziell unerwünschten Anwendung informiert zu werden.|
|**Datei- und Ordnerausschlüsse**|Fügt der Ausschlussliste eine oder mehrere Dateien und Ordner hinzu, z.B. „C:\Pfad“ oder „%ProgramFiles%\Pfad\Dateiname.exe“. Diese Dateien und Ordner werden in Echtzeitüberprüfungen oder geplanten Überprüfungen nicht berücksichtigt.|
|**Dateierweiterungsausschlüsse**|Fügen Sie der Ausschlussliste eine oder mehrere Dateierweiterungen hinzu, z.B. JPG oder TXT. Dateien mit diesen Erweiterungen werden in Echtzeitüberprüfungen oder geplanten Überprüfungen nicht berücksichtigt.|
|**Prozessausschlüsse**|Fügt der Ausschlussliste einen oder mehrere Prozesse vom Typ .exe, .com, oder .scr hinzu. Diese Prozesse werden in Echtzeitüberprüfungen oder geplanten Überprüfungen nicht berücksichtigt.|

  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationselemente für Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)