---
title: "Erstellen von Konfigurationselementen für Android- und Samsung KNOX Standard-Geräte, die mit Intune verwaltet werden | Microsoft-Dokumentation"
description: "Verwenden Sie das Konfigurationselement von System Center Configuration Manager für Android- und Samsung KNOX Standard-Geräte, die Geräteeinstellungen zu verwalten."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
caps.latest.revision: "17"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: c9961c2e9866199571a1b39a7b185cb6bb96f998
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Erstellen von Konfigurationselementen für Android- und Samsung KNOX-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden

Verwenden Sie das System Center Configuration Manager Konfigurationselement für **Android und Samsung KNOX**, um Einstellungen für Android- und Samsung KNOX-Geräte zu verwalten, die in Microsoft Intune registriert sind oder lokal von Configuration Manager verwaltet werden.  

#### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>So erstellen Sie ein Konfigurationselement für Android und Samsung KNOX  

1. Wählen Sie in der Configuration Manager-Konsole **Bestand und Kompatibilität** aus.  

2. Erweitern Sie im Arbeitsbereich **Bestand und Konformität** die **Konformitätseinstellungen**, und wählen Sie dann **Konfigurationselemente** aus.  

3. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Konfigurationselement erstellen** aus.  

4. Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Konfigurationselementen einen Namen und optional eine Beschreibung für das Konfigurationselement an.  

5. Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben** den Typ **Android und Samsung KNOX** aus.  

6. Wählen Sie **Kategorien** aus, wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern.  

7. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die jeweilige Android- oder Samsung KNOX-Plattform zur Bewertung des Konfigurationselements aus.  

8. Wählen Sie auf der Seite **Geräteeinstellungen** des Assistenten die Einstellungsgruppe aus, die Sie konfigurieren möchten. Informieren Sie sich in diesem Thema unter [Referenz zu Einstellungen des Konfigurationselements für Android und Samsung KNOX](#BKMK_setref) über die Details, und klicken Sie dann auf **Weiter**.  

    > [!TIP]  
    >  Ist die gewünschte Einstellung nicht aufgeführt, aktivieren Sie das Kontrollkästchen **Zusätzliche Einstellungen konfigurieren, die in den Standardeinstellungsgruppen nicht enthalten sind**.  

9. Konfigurieren Sie auf jeder Einstellungsseite die erforderlichen Einstellungen. Legen Sie außerdem fest, ob sie korrigiert werden sollen, wenn sie auf Geräten nicht kompatibel sind (sofern unterstützt).  

10. Sie können für jede Einstellungsgruppe auch den Schweregrad konfigurieren, der gemeldet wird, wenn die Inkompatibilität eines Konfigurationselements festgestellt wird:  

    - **Keiner**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  

    - **Information**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  

    - **Warnung**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  

    - **Kritisch**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  

    - **Kritisch mit Ereignis**. Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  

11. Überprüfen Sie auf der Seite **Plattformanwendbarkeit** des Assistenten alle Einstellungen, die mit den zuvor ausgewählten unterstützten Plattformen nicht kompatibel sind. Sie können zurückkehren und diese Einstellungen entfernen oder den Vorgang fortsetzen.  

    > [!TIP]  
    >  Nicht unterstützte Einstellungen werden nicht auf Kompatibilität überprüft.  

12. Beenden Sie den Assistenten.  

 Sie können das neue Konfigurationselement im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Konfigurationselemente** anzeigen.  

## <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Referenz zu Einstellungen des Konfigurationselements für Android und Samsung KNOX  

### <a name="password"></a>Kennwort  
Diese Einstellungen gelten für Android- und Samsung KNOX-Geräte.  

|Einstellung|Details|  
|-------------|-------------|  
|**Kennworteinstellungen auf Geräten erforderlich**|Auf unterstützten Geräten ein Kennwort erfordern.|  
|**Minimale Kennwortlänge (Zeichen)**|Legt die Mindestlänge für das Kennwort fest.|  
|**Kennwortablauf in Tagen**|Legt fest, nach wie vielen Tagen ein Kennwort spätestens geändert werden muss.|  
|**Anzahl der gespeicherten Kennwörter**|Verhindert die Wiederverwendung zuvor verwendeter Kennwörter.|  
|**Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts**|Setzt das Gerät zurück, wenn diese Anzahl von Anmeldeversuchen fehlschlägt.|  
|**Leerlaufzeit vor dem Sperren des Geräts**|Legt die Zeitspanne fest, nach der das Gerät bei Nichtverwendung gesperrt wird.|
|**Kennwortqualität**|Legt den erforderlichen Grad der Kennwortkomplexität fest und bestimmt, ob biometrische Geräte zulässig sind.|  
|**Zulassen von Smart Lock und anderen Vertrauens-Agents**|Damit können Sie das Smart Lock-Feature auf kompatiblen Android-Geräten steuern. Diese Telefonfunktion ermöglicht Ihnen das Deaktivieren oder Umgehen des Kennworts für den Gerätesperrbildschirm, wenn sich das Gerät an einem vertrauenswürdigen Standort befindet, z.B. wenn es mit einem bestimmten Bluetooth-Gerät verbunden ist oder sich in der Nähe eines NFC-Tags befindet. Mit dieser Einstellung können Sie verhindern, dass Benutzer Smart Lock konfigurieren.|
|**Fingerabdruck zum Entsperren (KNOX 5.0+)**|Ermöglicht das Entsperren kompatibler Geräte mittels Fingerabdruck.|

### <a name="device"></a>Gerät   

|Einstellung|Details|  
|------------------|-------------|  
|**Sprachwahlverfahren**|Aktiviert oder deaktiviert das Feature „Sprachwahlverfahren“ auf dem Gerät.|
|**Sprach-Assistent**|Ermöglicht die Verwendung von Sprach-Assistent-Software auf dem Gerät.|
|**Bildschirmaufnahme**|Ermöglicht dem Benutzer, den Bildschirminhalt als Image zu erfassen.|
|**Übermittlung von Diagnosedaten**|Erlaubt dem Gerät, Diagnoseinformationen an Google zu senden.|
|**Geolocation**|Erlaubt dem Gerät die Verwendung von Standortinformationen.|
|**Kopieren und Einfügen**|Erlaubt die Verwendung der Funktionen zum Kopieren und Einfügen auf dem Gerät.|
|**Zurücksetzen auf Werkseinstellungen**|Ermöglicht dem Benutzer das Zurücksetzen des Geräts auf die Werkseinstellungen.|  |
|**Freigabe der Zwischenablage zwischen Anwendungen**|Ermöglicht dem Benutzer die Verwendung der Zwischenablage zum Kopieren und Einfügen zwischen Apps.|  |
|**Bluetooth**|Ermöglicht die Verwendung von Bluetooth auf dem Gerät.|

### <a name="store"></a>Speicher

|Einstellung|Details|  
|------------------|-------------|  
|**Anwendungsstore**|Erlaubt dem Benutzer den Zugriff auf Google Play Store auf dem Gerät.|

### <a name="browser"></a>Browser

|Einstellung|Details|  
|------------------|-------------|  
|**Webbrowser zulassen**|Ermöglicht die Verwendung des Standardwebbrowsers des Geräts.|
|**Automatisch ausfüllen**|Erlaubt die Verwendung der AutoAusfüllen-Funktion des Webbrowsers.|
|**Active Scripting**|Ermöglicht dem Webbrowser des Geräts die Verwendung von Active Scripting.|
|**Popupblocker**|Ermöglicht die Verwendung des Popupblockers im Webbrowser.|
|**Cookies**|Ermöglicht dem Webbrowser des Geräts die Verwendung von Cookies.|

### <a name="cloud"></a>Cloud  

|Einstellung|Details|  
|-------------|-------------|  
|**Google-Sicherung**|Erlaubt die Verwendung der Google-Sicherung.|  
|**Automatische Synchronisierung mit Google-Konto**|Ermöglicht die automatische Synchronisierung der Einstellungen von Google-Konten.|  

### <a name="security"></a>Sicherheit  

|Einstellung|Details|  
|-------------|-------------|  
|**SMS- und MMS-Nachrichten**|Ermöglicht die Verwendung von SMS- und MMS-Nachrichten auf dem Gerät.|
|**Wechselmedien**|Ermöglicht dem Gerät die Verwendung von Wechselmedien, z.B. SD-Karten.|
|**Kamera**|Ermöglicht die Verwendung der Gerätekamera.<br /><br /> Gilt für Android- und Samsung KNOX-Geräte.|
|**NFC (Near Field Communication)**|Erlaubt Aufgaben, die NFC (Near Field Communication) verwenden, wenn dies vom Gerät unterstützt wird.|
|**YouTube**|Ermöglicht die Verwendung der YouTube-App auf dem Gerät.<br /><br /> Gilt nur für Samsung KNOX-Geräte.|  
|**Ausschalten**|Ermöglicht das Ausschalten des Geräts.<br /><br /> Gilt nur für Samsung KNOX-Geräte.|  

### <a name="roaming"></a>Roaming

|Einstellung|Details|  
|-------------|-------------|  
|Sprachroaming|Lässt Sprachroaming über das Mobilfunknetz zu.|
|Datenroaming|Lässt Datenroaming über das Mobilfunknetz zu.|


### <a name="encryption"></a>Verschlüsselung  
 Diese Einstellungen gelten für Android- und Samsung KNOX-Geräte.  

|Einstellung|Details|  
|-------------|-------------|  
|**Speicherkartenverschlüsselung**|Erfordert die Verschlüsselung der Speicherkarte des Geräts.|
|**Dateiverschlüsselung auf Gerät**|Erfordert die Verschlüsselung von Dateien auf dem mobilen Gerät.|  

### <a name="wireless-communications"></a>Funkkommunikation

|Einstellung|Details|  
|-------------|-------------|  
|**Drahtlosnetzwerkverbindung**|Ermöglicht die Verwendung der WLAN-Funktionen des Geräts.|
|**WLAN-Tethering**|Ermöglicht die Verwendung von WLAN-Tethering auf dem Gerät.|


### <a name="compliant-and-noncompliant-apps-android"></a>Kompatible und nicht kompatible Apps (Android)  
Sie können eine Liste von Android-Apps angeben, die in Ihrem Unternehmen kompatibel oder nicht kompatibel sind. Anschließend können Sie mithilfe von Berichten Geräte, auf denen nicht kompatible Apps installiert sind, und dazugehörige Benutzer bestimmen.  

Es ist nicht möglich, kompatible und nicht kompatible Apps im selben Konfigurationselement anzugeben.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>So geben Sie eine Liste mit kompatiblen bzw. nicht kompatiblen Apps an  

Geben Sie auf der Seite **Kompatible und nicht kompatible Apps (Android)** die folgenden Informationen ein:  

|Einstellung|Weitere Informationen|  
|-------------|----------------------|  
|**Liste nicht kompatibler Apps**|Legt eine Liste von Apps fest, die als nicht kompatibel gemeldet werden, wenn sie von Benutzern installiert werden.|  
|**Liste kompatibler Apps**|Legt eine Liste von Apps fest, die Benutzer installieren dürfen. Alle anderen installierten Apps werden als nicht kompatibel gemeldet.|  
|**Hinzufügen**|Fügt eine App zur ausgewählten Liste hinzu. Geben Sie einen Namen Ihrer Wahl und optional den Herausgeber der App an. Geben Sie zudem die URL zur App im App-Store an.<br /><br /> Zum Angeben der URL suchen Sie im [Bereich „Apps“ von Google Play](https://play.google.com/store/apps) die App, die Sie verwenden möchten.<br /><br /> Öffnen Sie die Seite der App, und kopieren Sie die URL in die Zwischenablage. Jetzt können Sie diese als URL in der Liste mit kompatiblen oder nicht kompatiblen Apps verwenden.<br /><br /> **Beispiel:** Suchen Sie in Google Play nach **Microsoft Office Mobile**. Die URL, die Sie verwenden, ist **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
|**Bearbeiten**|Ermöglicht Ihnen das Bearbeiten von Name, Herausgeber und URL der ausgewählten App.|  
|**Entfernen**|Löscht die ausgewählte App aus der Liste.|  
|**Importieren**|Importiert eine Liste von Apps, die Sie in einer CSV-Datei angegeben haben. Verwenden Sie in der Datei das Format, den Anwendungsnamen, den Herausgeber und die App-URL.|  

## <a name="android-for-work-configuration-items"></a>Konfigurationselemente für Android for Work
Android for Work hat zwei Einstellungsgruppen für Konfigurationselemente:

- **Kennwort**. Identisch mit den Einstellungen für „klassisches“ Android.

- **Work-Profil**. Ermöglicht die folgenden Android for Work-Einstellungen:
  - **Ermöglicht die Datenfreigabe zwischen Arbeits- und persönlichen Profilen**
  - **Arbeitsprofilbenachrichtigungen bei gesperrtem Gerät ausblenden** (Android 6.0 und höher)
  - **Standard-App-Berechtigungsrichtlinie einrichten** (Android 6.0 und höher)

Um ein Konfigurationselement im Android-Arbeitsprofil zu erstellen, wählen Sie **Android for Work** auf der Seite **Allgemein** aus, und konfigurieren Sie die Einstellungen für jede der Einstellungsgruppen, indem Sie das Konfigurationselement in die Baseline einfügen und wie gewohnt bereitstellen. Diese Einstellungen gelten nur für Geräte, die als „Android for Work“ registriert sind, und nicht für die Geräte, die nur als „Android“ registriert wurden.

### <a name="kiosk-mode-samsung-knox-only"></a>Kioskmodus (nur Samsung KNOX)  
Mithilfe des Kioskmodus können Sie ein Gerät sperren, damit nur bestimmte Features verwendet werden können. Beispielsweise können Sie festlegen, dass auf einem Gerät nur eine von Ihnen angegebene verwaltete App ausgeführt werden kann, oder Sie können die Lautstärkeregler eines Geräts deaktivieren. Diese Einstellung können beispielsweise für ein Demomodell eines Geräts verwendet werden. oder für ein Gerät nützlich sein, das nur eine bestimmte Funktion ausführen soll, wie z.B. ein Point-of-Sale-Gerät.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>So konfigurieren Sie den Kioskmodus für ein Samsung KNOX-Gerät  

1. Geben Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Kioskmoduseinstellungen für Samsung KNOX-Geräte konfigurieren** die folgenden Informationen an:  

   |Einstellung|Weitere Informationen|  
   |-------------|----------------------|  
   |**App auswählen**|Klicken Sie auf **Durchsuchen**, um eine Configuration Manager-Android-Anwendung (mit der Erweiterung **.apk**) auszuwählen, die beim Betrieb des Geräts im Kioskmodus ausgeführt werden darf. Andere Apps dürfen auf dem Gerät nicht ausgeführt werden.|  
   |**Lautstärkeregler**|Aktiviert oder deaktiviert die Verwendung der Lautstärkeregler am Gerät.|  
   |**Schaltfläche für Standby und Aktivieren**|Aktiviert oder deaktiviert die Taste für Standby/Aktivierung des Bildschirms am Gerät.|  

2. Klicken Sie danach auf **Weiter**.  

## <a name="reports-for-monitoring"></a>Berichte für die Überwachung
Sie können einen der folgenden Berichte verwenden, um kompatible und nicht kompatible Apps zu überwachen:  

- **Liste der nicht kompatiblen Apps und Geräte für einen angegebenen Benutzer**. Zeigt Informationen zu Benutzern und Geräten an, die Apps installiert haben, die mit einer von Ihnen angegebenen Richtlinie nicht konform sind.  

- **Zusammenfassung der Benutzer mit nicht kompatiblen Apps**. Zeigt Informationen zu Benutzern an, die Apps installiert haben, die mit einer von Ihnen angegebenen Richtlinie nicht konform sind.  

Weitere Informationen zur Verwendung von Berichten finden Sie unter [Berichterstattung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="see-also"></a>Weitere Informationen:  
[Konfigurationselemente für Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
