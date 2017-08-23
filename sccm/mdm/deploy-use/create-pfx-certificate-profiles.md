---
title: Erstellen von PFX-Zertifikatprofilen mit einer Zertifizierungsstelle | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie PFX-Dateien in System Center Configuration Manager verwenden, um benutzerspezifische Zertifikate zu generieren, die den verschlüsselten Datenaustausch unterstützen."
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 43d8b2217763681be69711fce93c020a65da1cd8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>Erstellen von PFX-Zertifikatprofilen mit einer Zertifizierungsstelle

*Gilt für: System Center Configuration Manager (Current Branch)*

Hier erfahren Sie, wie Sie ein Zertifikatprofil mit Anmeldeinformationen einer Zertifizierungsstelle verwenden.

Unter [Zertifikatprofile](../../protect/deploy-use/introduction-to-certificate-profiles.md) erhalten Sie allgemeine Informationen zum Erstellen und Konfigurieren von Zertifikatprofilen. In diesem Thema erfahren Sie Genaueres über Zertifikatprofile, die mit PFX-Zertifikatprofilen in Verbindung stehen.

## <a name="pfx-certificate-profiles"></a>PFX-Zertifikatprofile
Mit System Center Configuration Manager können Sie ein PFX-Zertifikatprofil mit Anmeldeinformationen erstellen, die von einer Zertifizierungsstelle ausgestellt wurden.  Ab Version 1706 können Sie Microsoft oder Entrust als Zertifizierungsstelle auswählen.  Bei der Bereitstellung von PFX-Dateien (Personal Information Exchange) auf Benutzergeräten werden benutzerspezifische Zertifikate zur Unterstützung des verschlüsselten Datenaustausches erstellt.

Informationen zum Import von Zertifikat-Anmeldeinformationen aus vorhandenen Zertifikatdateien finden Sie unter [How to create PFX certificate profiles by importing certificate details (Erstellen von PFX-Zertifikatprofilen durch Importieren von Zertifikatinformationen)](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Erstellen und Bereitstellen eines PFX-Zertifikatprofils (Personal Information Exchange)  

### <a name="get-started"></a>Erste Schritte

1.  Wählen Sie in der System Center Configuration Manager-Konsole **Bestand und Kompatibilität** aus.  
2.  Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** **Kompatibilitätseinstellungen**, &gt;Zugriff auf Unternehmensressourcen****  &gt; **Zertifikatprofile** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Zertifikatprofil erstellen** aus.

4.  Geben Sie auf der Seite **Allgemein** des ****  Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

    -   **Name**: Geben Sie einen eindeutigen Namen für das Zertifikatprofil ein. Sie können maximal 256 Zeichen verwenden.  

    -   **Beschreibung**: Geben Sie eine Beschreibung mit einem Überblick über das Zertifikatprofil sowie weitere relevante Informationen ein, die der Identifikation des Profils in der System Center Configuration Manager-Konsole dienen. Sie können maximal 256 Zeichen verwenden.  

    -   Wählen Sie in **Geben Sie den Typ des Zertifikatprofils an, das Sie erstellen möchten** zuerst **Privater Informationsaustausch - PKCS #12-Einstellungen (PFX) - Erstellen** und anschließend Ihre Zertifikatsstelle aus der Dropdownliste aus.  Ab Version 1706 können Sie **Microsoft** oder **Entrust** auswählen.

### <a name="select-supported-platforms"></a>Auswählen von unterstützten Plattformen

Auf der Seite „Unterstützte Plattformen“ werden die Betriebssysteme und Geräte identifiziert, die das Zertifikatprofil unterstützt.  

Zertifikatprofile können mehrere Betriebssysteme und Geräte unterstützen. Bestimmte Zusammenstellungen von Betriebssystemen oder Geräten erfordern jedoch unter Umständen unterschiedliche Einstellungen.  In diesen Fällen empfiehlt es sich, unterschiedliche Profile für verschiedene Einstellungen zu erstellen.  

Ab Version 1706 sind die folgenden Optionen verfügbar:

- Windows 10
    - Windows 10 (64-Bit)
    - Windows 10 (32-Bit)
    - Windows 10 Holographic Enterprise und höher
    - Windows 10 Holographic und höher
    - Windows 10 Team und höher
    - Windows 10 Mobile und höher
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> MacOS/OSX-Geräte werden derzeit nicht unterstützt.  

Wenn keine anderen Optionen ausgewählt sind, können Sie durch Aktivieren des Kontrollkästchens **Alles auswählen** alle verfügbare Optionen auswählen.  Wenn eine oder mehrere Optionen ausgewählt sind, wird durch Aktivieren des Kontrollkästchens **Alles auswählen** die vorhandene Auswahl gelöscht. 

1.  Wählen Sie eine oder mehrere Plattformen aus, die vom Zertifikatprofil unterstützt werden.

1.  Wählen Sie zum Fortfahren **Weiter** aus.  


### <a name="configure-certification-authorities"></a>Konfigurieren von Zertifizierungsstellen

Hier wählen Sie den Zertifikatregistrierungspunkt (CRP) aus, um die PFX-Zertifikate zu verarbeiten.  

1.  Wählen Sie aus der Liste **Primärer Standort** den Server mit der CRP-Rolle für die Zertifizierungsstelle aus.
1.  Wählen Sie aus der Liste **Zertifizierungsstellen** die relevante Zertifizierungsstelle aus, indem Sie ein Häkchen in der linken Spalte setzen.
1.  Wählen Sie zum Fortfahren **Weiter** aus.

Weitere Informationen finden Sie unter [Zertifikatinfrastruktur](../../protect/deploy-use/certificate-infrastructure.md).


### <a name="configure-certificate-settings-for-microsoft-ca"></a>Konfigurieren von Zertifikateinstellungen für Microsoft-Zertifizierungsstelle

Gehen Sie folgendermaßen vor, wenn Sie Microsoft als Zertifizierungsstelle zur Konfiguration Ihrer Zertifikateinstellungen verwenden:

1.  Wählen Sie die Zertifikatvorlage aus der Dropdownliste **Zertifikatvorlagenname** aus.

1.  Aktivieren Sie das Kontrollkästchen **Verwendung des Zertifikats**, um das Zertifikatprofil zum Signieren oder Verschlüsseln mit S/MIME zu verwenden.

    Wenn Sie diese Option mit Microsoft als Ihrer Zertifizierungsstelle verwenden, werden alle PFX-Zertifikate, die dem Zielbenutzer zugeordnet sind, an alle Geräte übermittelt, die vom Benutzer registriert werden.  Wenn dieses Kontrollkästchen deaktiviert ist, erhält jedes Gerät ein eindeutiges Zertifikat.  

1.  Legen Sie für **Format des Antragstellernamens** entweder die Option **Allgemeiner Name** oder **Vollständiger definierter Name** fest.  Wenn Sie nicht sicher sind, welche Option Sie auswählen sollten, wenden Sie sich an den Administrator der Zertifizierungsstelle.

1.  Wählen Sie für **Alternativer Antragstellername** je nach Zertifizierungsstelle entweder **E-Mail-Adresse** oder **Benutzerprinzipalname (UPN)** aus.

1.  Die Option **Erneuerungsschwellenwert** legt auf der Grundlage der verbleibenden Zeit in Prozent vor Ablauf eines Zertifikats fest, wann Zertifikate automatisch erneuert werden sollen.

1.  Geben Sie mit der Option **Gültigkeitsdauer des Zertifikats** den Zeitraum an, in dem das Zertifikats gültig ist.  Hierzu geben Sie eine Zahl (1-100) und einen Zeitraum (Jahre, Monate oder Tage) an.

1.  Die Option **Active Directory-Veröffentlichung** wird aktiviert, wenn durch den Zertifikatregistrierungspunkt Active Directory-Anmeldeinformationen angegeben werden.  Aktivieren Sie die Option, um das Zertifikatprofil in Active Directory zu veröffentlichen.

1.  Wenn Sie beim Angeben von unterstützten Plattformen eine oder mehrere Windows 10-Plattformen ausgewählt haben, gehen Sie folgendermaßen vor:

    1.  Legen Sie für **Windows-Zertifikatspeicher** die Option **Benutzer** fest.  Da durch die Option **Lokaler Computer** keine Zertifikate bereitgestellt werden, sollte diese nicht ausgewählt werden.
    1.  Wählen Sie eine der folgenden Optionen aus, um den **Schlüsselspeicheranbieter (KSP)** festzulegen:

        - **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  
        - **In Trusted Platform Module (TPM) installieren (andernfalls Fehler)** 
        - **In Windows Hello for Business installieren (andernfalls Fehler)** 
        - **In Softwareschlüsselspeicher-Anbieter installieren** 

1.  Wählen Sie abschließend **Weiter** oder **Zusammenfassung** aus.

### <a name="configure-certificate-settings-for-entrust-ca"></a>Konfigurieren von Zertifikateinstellungen für Entrust als Zertifizierungsstelle

Gehen Sie folgendermaßen vor, um Konfigurationseinstellungen mit Entrust als Zertifizierungsstelle vorzunehmen:

1.  Wählen Sie aus der Dropdownliste **Konfiguration der digitalen ID** das Konfigurationsprofil aus.  Die Optionen zur Konfiguration der digitalen ID werden vom Entrust-Administrator erstellt.

1.  Wenn die Option **Zertifikatverwendung** aktiviert wurde, wird das Zertifikatprofil zum Signieren oder Verschlüsseln mit S/MIME verwendet.

    Wenn Sie Entrust als Zertifizierungsstelle verwenden, werden alle PFX-Zertifikate, die dem Zielbenutzer zugeordnet sind, an alle Geräte übermittelt, die vom Benutzer registriert werden.    Wenn diese Option *nicht* aktiviert ist, erhält jedes Gerät ein eindeutiges Zertifikat.  Je nach Zertifizierungsstelle kann dieses Verhalten variieren. Weitere Informationen finden Sie im entsprechenden Abschnitt.

1.  Verwenden Sie die Schaltfläche **Format**, um Entrust-Tokens der Form **Format des Antragstellernamens** ConfigMgr-Feldern zuzuordnen.  

    Im Dialog **Certificate Name Formatting (Zertifikatsnamenformatierung)** werden alle Entrust-Variablen aufgeführt, die mit der Konfiguration der digitalen ID in Verbindung stehen.  Wählen Sie für jede Entrust-Variable die entsprechende LDAP-Variable aus der zugehörigen Dropdownliste.

1.  Klicken Sie auf die Schaltfläche **Format**, um Entrust-Tokens der Form **Alternativer Antragstellername** ConfigMgr-Feldern zuzuordnen.  

    Im Dialog **Certificate Name Formatting (Zertifikatsnamenformatierung)** werden alle Entrust-Variablen aufgeführt, die mit der Konfiguration der digitalen ID in Verbindung stehen.  Wählen Sie für jede Entrust-Variable die entsprechende LDAP-Variable aus der zugehörigen Dropdownliste.

1.  Die Option **Erneuerungsschwellenwert** legt auf der Grundlage der verbleibenden Zeit in Prozent vor Ablauf eines Zertifikats fest, wann Zertifikate automatisch erneuert werden sollen.

1.  Geben Sie mit der Option **Gültigkeitsdauer des Zertifikats** den Zeitraum an, in dem das Zertifikats gültig ist.  Hierzu geben Sie eine Zahl (1-100) und einen Zeitraum (Jahre, Monate oder Tage) an.

1.  Die Option **Active Directory-Veröffentlichung** wird aktiviert, wenn durch den Zertifikatregistrierungspunkt Active Directory-Anmeldeinformationen angegeben werden.  Aktivieren Sie die Option, um das Zertifikatprofil in Active Directory zu veröffentlichen.

1.  Wenn Sie beim Angeben von unterstützten Plattformen eine oder mehrere Windows 10-Plattformen ausgewählt haben, gehen Sie folgendermaßen vor:

    1.  Legen Sie für **Windows-Zertifikatspeicher** die Option **Benutzer** fest.  Da durch die Option **Lokaler Computer** keine Zertifikate bereitgestellt werden, sollte diese nicht ausgewählt werden.
    1.  Wählen Sie eine der folgenden Optionen aus, um den **Schlüsselspeicheranbieter (KSP)** festzulegen:

        - **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  
        - **In Trusted Platform Module (TPM) installieren (andernfalls Fehler)** 
        - **In Windows Hello for Business installieren (andernfalls Fehler)** 
        - **In Softwareschlüsselspeicher-Anbieter installieren** 

1.  Wählen Sie abschließend **Weiter** oder **Zusammenfassung** aus.


### <a name="finish-up"></a>Fertig stellen

1.  Überprüfen Sie auf der Seite „Zusammenfassung“ Ihre Auswahl.

1.  Wählen Sie anschließend **Weiter**, um das Profil zu erstellen.  

1.  Das Zertifikatprofil mit der PFX-Datei steht nun im Arbeitsbereich **Zertifikatprofile** bereit. 

1.  Gehen Sie folgendermaßen vor, um das Profil bereitzustellen:

    1. Öffnen Sie den Arbeitsbereich **Bestand und Kompatibilität**.
    1. Wählen Sie **Kompatibilitätseinstellungen** > **Zugriff auf Unternehmensressourcen** > **Zertifikatprofile** aus.
    1. Klicken Sie mit der rechten Maustaste auf das gewünschte Zertifikatprofil, und wählen Sie anschließend **Bereitstellen** aus. 


## <a name="see-also"></a>Weitere Informationen:
[Create a new certificate profile (Erstellen eines neuen Zertifikatprofils)](../../protect/deploy-use/create-certificate-profiles.md) begleitet Sie im Assistenten für das Erstellen eines Zertifikatprofils.

[How to create PFX certificate profiles by importing certificate details (Erstellen von PFX-Zertifikatprofilen durch Importieren von Zertifikatinformationen)](../../mdm/deploy-use/import-pfx-certificate-profiles.md)

Unter [Deploy Wi-Fi, VPN, email, and certificate profiles (Bereitstellen von WLAN-, VPN-, E-Mail- und Zertifikatprofilen)](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) wird beschrieben, wie Sie Zertifikatprofile bereitstellen.