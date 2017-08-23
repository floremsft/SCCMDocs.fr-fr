---
title: Erstellen von WLAN-Profilen | Microsoft-Dokumentation
description: "Hier erfahren Sie, wie Sie in System Center Configuration Manager mit WLAN-Profilen Funknetzwerkeinstellungen für Benutzer in Ihrer Organisation bereitstellen."
ms.custom: na
ms.date: 12/11/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: "13"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: f1ae976899de1fd3efcbde0c7268f071a5d0218b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-wi-fi-profiles"></a>Erstellen von WLAN-Profilen

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie WLAN-Profile in System Center Configuration Manager, um für Benutzer in Ihrer Organisation Einstellungen für Funknetzwerke bereitzustellen. Durch die Bereitstellung dieser Einstellungen erleichtern Sie den Benutzern das Herstellen einer WLAN-Verbindung.  

 Angenommen, Sie haben ein WLAN-Netzwerk installiert. Nun sollen alle iOS-Geräte mit diesem Netzwerk eine Verbindung herstellen können. Hierzu erstellen Sie ein WLAN-Profil mit den Einstellungen, die zum Herstellen einer Verbindung mit dem Drahtlosnetzwerk erforderlich sind. Stellen Sie dann das Profil für alle Benutzer bereit, die über iOS-Geräte in Ihrer Hierarchie verfügen. Benutzer von iOS-Geräten finden das Unternehmensnetzwerk in der Liste der Funknetzwerke und können leicht eine Verbindung mit diesem Netzwerk herstellen.  

 Sie können die folgenden Gerätetypen mit WLAN-Profilen konfigurieren:  

-   Geräte unter Windows 8.1 32-Bit  

-   Geräte unter Windows 8.1 64-Bit  

-   Geräte unter Windows RT 8.1  

-   Geräte unter Windows 10 Desktop oder Mobile  

[Erstellen von WLAN-Profilen für mobile Geräte](../../mdm/deploy-use/create-wifi-profiles.md) bietet Informationen zur Bereitstellung von Einstellungen für drahtlose Netzwerke in Configuration Manager mit WLAN-Profilen für Benutzer mobiler Geräte.

> [!IMPORTANT]  
>  Um Profile für Android-, iOS-, Windows Phone- und registrierte Windows 8.1-Geräte (und höher) bereitzustellen, müssen diese Geräte bei Microsoft Intune registriert werden. Informationen zum Registrieren von Geräten finden Sie unter [Enroll devices for management in Intune (Registrieren von Geräten für die Verwaltung in Intune)](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Wenn Sie ein WLAN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen einfügen. Dazu gehören Zertifikate für die Serverüberprüfung und die Clientauthentifizierung, die mithilfe von Configuration Manager-Zertifikatprofilen per Push übertragen wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="create-a-wi-fi-profile"></a>Erstellen eines WLAN-Profils  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** >  **Zugriff auf Unternehmensressourcen** > **WLAN-Profile** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **WLAN-Profil erstellen** aus.  

1.  Geben Sie auf der Seite **Allgemein** einen eindeutigen Namen und eine Beschreibung für das WLAN-Profil ein.  Wenn Sie eine Einstellungen aus einem anderen WLAN-Profil übernehmen möchten, wählen Sie **Vorhandenes WLAN-Profil aus einer Datei importieren** aus.  

    > [!IMPORTANT]  
    >  Stellen Sie sicher, dass das importierte WLAN-Profil gültigen XML-Code für ein WLAN-Profil enthält. Das Profil wird beim Importieren der Datei von Configuration Manager nicht überprüft.  

3.  Geben Sie unter **Schweregrad der Nichtkompatibilität für Berichte** den Schweregrad für Berichte an, falls festgestellt wird, dass das WLAN-Profil auf Clientgeräten nicht kompatibel ist (beispielsweise bei einem Fehler der Profilinstallation). Die folgenden Schweregrade sind verfügbar:  

    -   **Keine**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  

    -   **Information**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  

    -   **Warnung**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  

    -   **Kritisch**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  

    -   **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  

1.  Geben Sie auf der Seite **WLAN-Profil** den Namen an, der auf Geräten als Netzwerkname angezeigt wird.  

    > [!IMPORTANT]  
    >  Configuration Manager unterstützt weder den Apostroph (**‘**) noch das Komma (**,**) im Netzwerknamen.  

2.  Geben Sie die **SSID** unter Beachtung der Groß-/Kleinschreibung an.
3.  Wählen Sie die anderen entsprechenden Verbindungsoptionen aus, einschließlich   **Auch dann verbinden, wenn der Name (SSID) des Netzwerks nicht von diesem gesendet wird**, wenn die Möglichkeit besteht, dass die SSID ausgeblendet ist.  

4.  Wählen Sie auf der Seite **Sicherheitskonfiguration** das Sicherheitsprotokoll aus, das im Funknetzwerk verwendet wird, oder wählen Sie **Keine Authentifizierung (Offen)** aus, wenn das Netzwerk nicht gesichert ist.
    > [!IMPORTANT]  
    >  Wenn Sie für die lokale Verwaltung mobiler Geräte ein WLAN-Profil erstellen, unterstützt Current Branch von Configuration Manager nur die folgenden WLAN-Sicherheitskonfigurationen:  
    >   
    >  Sicherheitstypen: **WPA2-Enterprise** oder **WPA2-Personal**  
    > Verschlüsselungstypen: **AES** oder **TKIP**  
    > EAP-Typen: **Smartcard- oder anderes Zertifikat** oder **PEAP**  

    > Für Android-Geräte werden die Sicherheitstypen **WPA-Personal**, **WPA2-Personal** und **WEP** nicht unterstützt.  

2.  Wählen Sie die Verschlüsselungsmethode aus, die vom Funknetzwerk verwendet wird.  

3.  Wählen Sie den EAP-Typ aus, der zur Authentifizierung beim Funknetzwerk verwendet wird.  

     Nur für Windows Phone-Geräte: Die EAP-Typen **LEAP** und **EAP-FAST** werden nicht unterstützt.  

4.  Klicken Sie auf **Konfigurieren** , um Eigenschaften für den ausgewählten EAP-Typ anzugeben. Diese Option steht möglicherweise für einige ausgewählte EAP-Typen nicht zur Verfügung.  

    > [!IMPORTANT]  
    >  Wenn Sie auf **Konfigurieren**klicken, wird ein Windows-Dialogfeld geöffnet. Daher müssen Sie sicherstellen, dass die Konfiguration des ausgewählten EAP-Typs vom Betriebssystem des Computers unterstützt wird, auf dem die Configuration Manager-Konsole ausgeführt wird.  
    >   
    >  Wenn Sie für iOS-Geräte eine EAP-fremde Methode für die Authentifizierung gewählt haben, wird unabhängig von der ausgewählten Methode MS-CHAP v2 für die Verbindung verwendet.  

5.  Wenn Sie Benutzeranmeldeinformationen speichern möchten, damit Benutzer bei der Anmeldung keine Anmeldeinformationen eingeben müssen, wählen Sie **Benutzeranmeldeinformationen bei jeder Anmeldung speichern**aus.  

6. **Nur für iOS-Geräte:**  
 Konfigurieren Sie die Informationen für alle Zertifikate, die für die WLAN-Verbindung erforderlich sind. Sie müssen wie folgt das Clientzertifikat und entweder den Namen des vertrauenswürdigen Serverzertifikats oder das Stammzertifikat konfigurieren:  

    -   **Namen vertrauenswürdiger Serverzertifikate**: Wenn auf dem Server, mit dem das Gerät eine Verbindung herstellt, ein Serverauthentifizierungszertifikat für die Identifikation des Servers und zur Unterstützung bei der Absicherung des Kommunikationskanals verwendet wird, geben Sie den oder die Namen für den Antragstellernamen oder den alternativen Antragstellernamen dieses Zertifikats ein. Die Namen sind normalerweise die vollqualifizierten Domänennamen des Servers. Beispiel: Wenn für den Zertifikatantragsteller der allgemeine Name des Serverzertifikats „srv1.contoso.com“ lautet, geben Sie **srv1.contoso.com**ein. Wenn für das Serverzertifikat mehrere Namen als alternative Antragstellernamen angegeben sind, geben Sie die einzelnen Namen getrennt durch ein Semikolon ein.  

    > [!TIP]  
    >  Wenn das Clientzertifikat, das Sie für die EAP- oder Clientauthentifizierung für ein iOS-Gerät auswählen, zur Authentifizierung bei einem RADIUS-Server (Remote Authentication Dial-In User Service) wie etwa einem Server, auf dem ein Netzwerkrichtlinienserver ausgeführt wird, verwendet wird, müssen Sie als alternativen Antragstellername den Benutzerprinzipalnamen festlegen.  

    -   **Stammzertifikate für die Serverüberprüfung auswählen**: Wenn auf dem Server, mit dem das Gerät eine Verbindung herstellt, ein für das Gerät nicht vertrauenswürdiges Serverauthentifizierungszertifikat verwendet wird, wählen Sie das Zertifikatprofil aus, das das Stammzertifikat für das Serverzertifikat enthält, um auf dem Gerät eine Kette vertrauenswürdiger Zertifikate zu erstellen.  

    -   **Clientzertifikat für Clientauthentifizierung auswählen**: Wenn für den Server oder das Netzwerkgerät ein Clientzertifikat erforderlich ist, um das verbindende Gerät zu authentifizieren, wählen Sie das Zertifikatprofil aus, das das Clientauthentifizierungszertifikat enthält.  

    > [!NOTE]  
    >  Damit Sie das Stammzertifikat und das Clientzertifikat auswählen können, müssen Sie sie zuerst als Zertifikatprofil konfigurieren und bereitstellen. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

7.  Geben Sie auf der Seite **Erweiterte Einstellungen** erweiterte Einstellungen für das WLAN-Profil an. Dazu gehören der Authentifizierungsmodus, Optionen für einmaliges Anmelden und Einstellungen der FIPS-Kompatibilität (Federal Information Processing Standards). Weitere Informationen zu diesen Optionen finden Sie in der Windows-Dokumentation. Die verfügbaren erweiterten Einstellungen sind abhängig von den auf der Seite **Sicherheitskonfiguration** des Assistenten ausgewählten Optionen.  

1.  Aktivieren Sie auf der Seite **Proxyeinstellungen** das Kontrollkästchen **Proxyeinstellungen für dieses WLAN-Profil konfigurieren**, wenn für Ihr Funknetzwerk ein Proxyserver verwendet wird. Geben Sie dann die Konfigurationsinformationen an.  

2. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssysteme aus, unter denen das WLAN-Profil installiert wird. Alternativ klicken Sie auf **Alle auswählen** , um das WLAN-Profil unter allen verfügbaren Betriebssystemen zu installieren.  

### <a name="next-steps"></a>Nächste Schritte
 Weitere Informationen zum Bereitstellen des WLAN-Profils finden Sie unter [Bereitstellen von WLAN-Profilen in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
