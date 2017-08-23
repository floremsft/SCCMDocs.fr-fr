---
title: Erstellen von Exchange ActiveSync-E-Mail-Profilen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie E-Mail-Profile in System Center Configuration Manager erstellen und konfigurieren, die mit Microsoft Intune verwendet werden.
ms.custom: na
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: "4"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 7434c98f2217cf63fdcd250b91e772de72daaea9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Erstellen von Exchange ActiveSync-E-Mail-Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit Microsoft Intune und Exchange ActiveSync können Sie Geräte mit E-Mail-Profilen und -Einschränkungen einrichten. Dies ermöglicht Benutzern bei minimal erforderlicher eigener Einrichtung den Zugriff auf E-Mails im Unternehmen über ihre Geräte.  

 Sie können die folgenden Gerätetypen mit E-Mail-Profilen konfigurieren:  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- iPhones unter iOS 5, iOS 6, iOS 7 und iOS 8  
- iPads unter iOS 5, iOS 6, iOS 7 und iOS 8  
- Samsung KNOX Standard (4 und höher)
- Android for Work

Um E-Mail-Profile für Geräte bereitzustellen, müssen Sie die Geräte in Intune registrieren. Informationen zum Registrieren von Geräten finden Sie unter [Verwalten mobiler Geräte mit Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).

> [!NOTE]
> Intune stellt zwei Android for Work-E-Mail-Profile bereit: eines für die Gmail-E-Mail-App und eines für die Nine Work-E-Mail-App. Diese Apps sind im Google Play Store erhältlich und unterstützen Verbindungen mit Exchange. Stellen Sie auf den Geräten der Benutzer eine dieser E-Mail-Apps bereit, erstellen Sie das entsprechende Profil, und stellen Sie dieses bereit, um die E-Mail-Konnektivität zu aktivieren. E-Mail-Apps wie Nine Work sind möglicherweise nicht frei. Lesen Sie dazu die Details der App-Lizenzierung, oder wenden Sie sich mit Ihren Fragen an das App-Unternehmen.

 Zusätzlich zum Konfigurieren eines E-Mail-Kontos auf dem Gerät können Sie die Synchronisierungseinstellungen für Kontakte, Kalender und Aufgaben konfigurieren.  

 Wenn Sie ein E-Mail-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen einfügen. Dazu gehören Zertifikate für Identität, Verschlüsselung und Signatur, die mithilfe von System Center Configuration Manager-Zertifikatprofilen eingerichtet wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md).    

## <a name="create-an-exchange-activesync-email-profile"></a>Erstellen eines Exchange ActiveSync-E-Mail-Profils  

Zum Erstellen eines Profils verwenden Sie den Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen. 

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Kompatibilität** aus.  

2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, dann den **Zugriff auf Unternehmensressourcen**, und wählen Sie anschließend **E-Mail-Profile** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Exchange ActiveSync-E-Mail-Profil erstellen** aus, um den Assistenten zu starten.

4.  Konfigurieren Sie auf der Seite **Allgemein** des Assistenten die folgenden Informationen:

    - **Name**. Geben Sie einen aussagekräftigen Namen für das E-Mail-Profil ein.

    - **Beschreibung**. Wenn Sie möchten, können Sie eine Beschreibung des E-Mail-Profils eingeben, anhand derer Sie es in der Configuration Manager-Konsole erkennen können.

    - **Dieses Email Profil ist für Android for Work bestimmt**. Wählen Sie diese Option aus, wenn Sie dieses E-Mail-Profil nur für Android for Work-Geräte bereitstellen. Wenn Sie dieses Kontrollkästchen aktivieren, wird die Seite **Unterstützte Plattformen** des Assistenten nicht angezeigt. Nur Android for Work-E-Mail-Profile sind konfiguriert.

4.  Geben Sie auf der Seite **Exchange ActiveSync** des Assistenten die folgenden Informationen an:  

    -   **Exchange ActiveSync-Host**. Geben Sie den Hostnamen des Exchange-Servers Ihres Unternehmens an, der die Exchange ActiveSync-Dienste hostet.  

    -   **Kontoname**. Geben Sie den Anzeigenamen für das E-Mail-Konto so an, wie er den Benutzern auf ihren Geräten angezeigt wird.  

    -   **Kontobenutzername**. Wählen Sie aus, wie der Benutzernamen des E-Mail-Kontos auf Clientgeräten konfiguriert wird. Sie können eine der folgenden Optionen aus der Dropdownliste auswählen:  

        -   **Benutzerprinzipalname**. Verwenden Sie den vollständigen Benutzerprinzipalnamen, um sich bei Exchange anzumelden.  

        -   **Kontoname**. Verwenden Sie den vollständigen Benutzerkontonamen von Active Directory.

        -   **Primäre SMTP-Adresse**. Verwenden Sie die primäre SMTP-Adresse des Benutzers zum Anmelden bei Exchange.  

    -   **E-Mail-Adresse**. Wählen Sie, wie die E-Mail-Adresse für den Benutzer auf jedem Clientgerät generiert wird. Sie können eine der folgenden Optionen aus der Dropdownliste auswählen:  

        -   **Primäre SMTP-Adresse**. Verwenden Sie die primäre SMTP-Adresse des Benutzers zum Anmelden bei Exchange.  

        -   **Benutzerprinzipalname**. Der vollständige Benutzerprinzipalname wird als E-Mail-Adresse verwendet.  

    -   **Kontodomäne**. Wählen Sie eine der folgenden Optionen aus:  

        -   **Von Active Directory abrufen**  

        -   **Benutzerdefiniert**  

         Dieses Feld ist nur anwendbar, wenn **sAMAccountName** in der Dropdownliste **Kontobenutzername** ausgewählt wird.  

    -   **Authentifizierungsmethode**. Wählen Sie eine der folgenden Authentifizierungsmethoden aus, die zum Authentifizieren der Verbindung mit Exchange ActiveSync verwendet wird:  

        -   **Zertifikate**. Ein Identitätszertifikat wird für die Authentifizierung der Exchange ActiveSync-Verbindung verwendet.  

        -   **Benutzername und Kennwort**. Der Gerätebenutzer muss ein Kennwort für die Verbindung mit Exchange ActiveSync angeben. (Der Benutzername ist als Teil des E-Mail-Profils konfiguriert.)  

    -   **Identitätszertifikat**. Wählen Sie **Auswählen** und dann ein Zertifikat für die Identität aus.  

         Als Identitätszertifikate lassen sich nur SCEP-Zertifikate und nicht PFX-Zertifikate verwenden.  Weitere Informationen erhalten Sie unter [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles) (Zertifikatprofile in System Center Configuration Manager).  

         Diese Option ist nur verfügbar, wenn Sie unter **Authentifizierungsmethode** die Option **Zertifikate** ausgewählt haben.  

    -   **S/MIME verwenden**. Ausgehende E-Mails werden mithilfe von S/MIME-Verschlüsselung gesendet. Diese Option steht nur für iOS-Geräte zur Verfügung. Wählen Sie aus den folgenden Optionen:

        -   **Signaturzertifikate**.  Klicken Sie auf **Auswählen** und wählen Sie dann ein Zertifikat für die Verschlüsselung aus.  

            Für das Profil kann entweder ein SCEP oder ein PFX-Zertifikat verwendet werden.  Wenn Sie jedoch sowohl die Signierung als auch die Verschlüsselung nutzen, müssen Sie für sowohl für die Signierung als auch für die Verschlüsselung PFX-Zertifikatprofile auswählen.**

        -   **Verschlüsselungszertifikate**. Wählen Sie **Auswählen** und dann ein Zertifikat für die Verschlüsselung aus. Sie können nur ein PFX-Zertifikat für die Verwendung als Verschlüsselungszertifikat auswählen.

        -   Um alle E-Mail auf iOS-Geräten zu verschlüsseln, aktivieren Sie das Kontrollkästchen **Verschlüsselung erforderlich**.    

         Sie müssen Zertifikatprofile erstellen, bevor Sie sie hier auswählen können.  Weitere Informationen erhalten Sie unter [Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles) (Zertifikatprofile in System Center Configuration Manager).  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Konfigurieren der Synchronisierungseinstellungen für das Exchange ActiveSync-E-Mail-Profil  

Geben Sie auf der Seite **Synchronisierungseinstellungen konfigurieren** des Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen die folgenden Informationen an:  

-   **Zeitplan**. Wählen Sie den Zeitplan aus, nach dem Geräte mit Daten vom Exchange-Server synchronisiert werden. Diese Option steht nur für Windows Phone-Geräte zur Verfügung. Wählen Sie aus:  

    -   **Nicht konfiguriert**. Es wird kein Synchronisierungszeitplan erzwungen. Dies ermöglicht es Benutzern, ihren eigenen Synchronisierungszeitplan zu konfigurieren.  

    -   **Bei Eintreffen von Nachrichten**. Daten wie E-Mails und Kalendereinträge werden bei ihrer Ankunft automatisch synchronisiert.  

    -   **15 Minuten**. Daten wie E-Mails und Kalendereinträge werden alle 15 Minuten automatisch synchronisiert.  

    -   **30 Minuten**. Daten wie E-Mails und Kalendereinträge werden alle 30 Minuten automatisch synchronisiert.  

    -   **60 Minuten**. Daten wie E-Mails und Kalendereinträge werden alle 60 Minuten automatisch synchronisiert.  

    -   **Manuell**. Der Gerätebenutzer muss die Synchronisierung manuell starten.  

-   **Anzahl der Tage für die E-Mail-Synchronisierung**. Wählen Sie in der Dropdownliste die Anzahl der Tage aus, für die E-Mails synchronisiert werden sollen. Wählen Sie einen der folgenden Werte aus:  

    -   **Nicht konfiguriert**. Die Einstellung wird nicht erzwungen. Damit können Benutzer konfigurieren, wie viele E-Mails auf ihr Gerät heruntergeladen werden.  

    -   **Unbegrenzt**. Alle verfügbaren E-Mail-Nachrichten werden synchronisiert.  

    -   **1 Tag**  

    -   **3 Tage**  

    -   **1 Woche**  

    -   **2 Wochen**  

    -   **1 Monat**  

-   **Verschieben von Nachrichten in andere E-Mail-Konten zulassen**. Wählen Sie diese Option aus, damit Benutzer E-Mail-Nachrichten zwischen verschiedenen Konten verschieben können, die auf ihrem Gerät konfiguriert sind. Diese Option steht nur für iOS-Geräte zur Verfügung.  

-   **E-Mail-Versand aus Anwendungen von Drittanbietern zulassen.** Wählen Sie diese Option aus, um Benutzern das Senden von E-Mails von bestimmten nicht standardmäßigen E-Mail-Anwendungen von Drittanbietern zu ermöglichen. Diese Option steht nur für iOS-Geräte zur Verfügung.  

-   **Zuletzt verwendete E-Mail-Adressen synchronisieren**. Wählen Sie diese Option aus, um die Liste der E-Mail-Adressen zu synchronisieren, die zuletzt auf dem Gerät verwendet wurden. Diese Option steht nur für iOS-Geräte zur Verfügung.  

-   **SSL verwenden**. Wählen Sie diese Option aus, um die SSL-Kommunikation (Secure Sockets Layer) beim Senden von E-Mails, beim Empfangen von E-Mails und für die Kommunikation mit dem Exchange-Server zu verwenden.  

-   **Zu synchronisierender Inhaltstyp**. Wählen Sie die Inhaltstypen aus, die auf Geräten synchronisiert werden sollen. Diese Option steht nur für Windows Phone-Geräte zur Verfügung. Wählen Sie aus:  

    -   **E-Mail**  

    -   **Kontakte**  

    -   **Kalender**  

    -   **Aufgaben**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Angeben der unterstützten Plattformen für das Exchange ActiveSync-E-Mail-Profil  

1.  Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten zum Erstellen von Exchange ActiveSync-E-Mail-Profilen die Betriebssysteme aus, unter denen das E-Mail-Profil installiert wird. Alternativ Wählen Sie **Alle auswählen** aus, um das E-Mail-Profil unter allen verfügbaren Betriebssystemen zu installieren.  

2.  Beenden Sie den Assistenten.

Informationen zum Bereitstellen von Exchange ActiveSync-E-Mail-Profilen finden Sie unter [Bereitstellen von E-Mail-Profilen in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  
