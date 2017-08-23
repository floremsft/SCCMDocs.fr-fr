---
title: "Massenregistrierung von Geräten | Microsoft-Dokumentation | Lokale MDM"
description: "Automatische Massenregistrierung von Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
caps.latest.revision: "13"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: be9596537e9c80a6d78aa0685d33382bfd242afe
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Massenregistrierung von Geräten mit der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Die Massenregistrierung in System Center Configuration Manager mit der lokalen Verwaltung mobiler Geräte ist eine Methode zum Registrieren von Geräten, die im Vergleich zur Benutzerregistrierung in höherem Maße automatisiert ist. Bei der Benutzerregistrierung müssen Benutzer ihre Anmeldeinformationen zum Registrieren des Geräts eingeben.  Bei der Massenregistrierung wird ein Registrierungspaket zur Authentifizierung des Geräts während der Anmeldung verwendet. Das Paket (eine PPKG-Datei) enthält ein Zertifikatprofil und optional ein WLAN-Profil, zur Unterstützung der Registrierung Intranetkonnektivität auf dem Gerät erforderlich ist.  

> [!NOTE]  
>  Configuration Manager Current Branch unterstützt die Registrierung bei der lokalen Verwaltung mobiler Geräte für Geräte, auf denen folgende Betriebssysteme ausgeführt werden:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

In den folgenden Aufgaben wird erläutert, wie Sie eine Massenregistrierung von Computern und Geräten für die lokale Verwaltung mobiler Geräte vornehmen:  

-   [Erstellen eines Zertifikatprofils](#bkmk_createCert)  

-   [Erstellen eines WLAN-Profils](#CreateWifi)  

-   [Erstellen eines Anmeldungsprofils](#bkmk_createEnroll)  

-   [Erstellen einer Registrierungspaketdatei (PPKG-Datei)](#bkmk_createPpkg)  

-   [Verwenden des Pakets für die Massenregistrierung eines Geräts](#bkmk_getPpkg)  

-   [Überprüfen der Registrierung des Geräts](#bkmk_verifyEnroll)  

##  <a name="bkmk_createCert"></a> Erstellen eines Zertifikatprofils  
 Die Hauptkomponente des Registrierungspakets ist ein Zertifikatprofil, mit dem dem Gerät, das registriert wird, automatisch ein vertrauenswürdiges Stammzertifikat bereitgestellt wird.  Das Stammzertifikat wird für die vertrauenswürdige Kommunikation zwischen den Geräten und den erforderlichen Standortsystemrollen für die lokale Verwaltung mobiler Geräte benötigt. Ohne das Stammzertifikat wäre das Gerät in HTTPS-Verbindungen mit den Servern, auf denen der Anmeldungspunkt, der Anmeldungsproxypunkt, der Verteilungspunkt und die Standortsystemrollen des Geräteverwaltungspunkts gehostet werden, nicht vertrauenswürdig.  

 Bei der Vorbereitung des Systems für die lokale Verwaltung mobiler Geräte exportieren Sie ein Stammzertifikat, das Sie im Zertifikatprofil des Registrierungspakets verwenden können. Informationen zum Abrufen des vertrauenswürdigen Stammzertifikats finden Sie unter [Export the certificate with the same root as the web server certificate (Exportieren des Zertifikats mit dem Webserverzertifikat entsprechendem Stamm)](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

 Verwenden Sie das exportierte Stammzertifikat, um ein Profil zu erstellen. Anweisungen finden Sie unter [How to create certificate profiles in System Center Configuration Manager (Erstellen von Zertifikatprofilen in System Center Configuration Manager)](../../protect/deploy-use/create-certificate-profiles.md).  

##  <a name="CreateWifi"></a> Erstellen eines WLAN-Profils  
 Die andere Komponente des zur Massenregistrierung verwendeten Pakets ist ein WLAN Profil. Einige Geräte verfügen möglicherweise vor der Bereitstellung von Netzwerkeinstellungen nicht über die erforderliche Netzwerkkonnektivität, um die Registrierung zu unterstützen. Durch Hinzufügen eines WLAN-Profils zum Registrierungspaket wird dem Gerät ermöglicht, Netzwerkkonnektivität herzustellen.  

 Zum Erstellen eines WLAN-Profils in Configuration Manager, befolgen Sie die Anweisungen unter [How to create Wi-Fi profiles in System Center Configuration Manager (Erstellen von WLAN-Profilen in System Center Configuration Manager)](../../protect/deploy-use/create-wifi-profiles.md).  

> [!IMPORTANT]  
>Beachten Sie die folgenden zwei Probleme, wenn Sie ein WLAN-Profil für Massenregistrierung erstellen:
>
> - Current Branch von Configuration Manager unterstützt nur die folgenden WLAN-Sicherheitskonfigurationen für die lokale Verwaltung mobiler Geräte:  
>   
>   - Sicherheitstypen: **WPA2-Enterprise** oder **WPA2-Personal**  
>   - Verschlüsselungstypen: **AES** oder **TKIP**  
>   - EAP-Typen: **Smartcard- oder anderes Zertifikat** oder **PEAP**  
>
>
> - Obwohl Configuration Manager über eine Einstellung für Proxyserverinformationen im WLAN-Profil verfügt, wird kein Proxyserver bei der Registrierung des Geräts konfiguriert. Wenn Sie einen Proxyserver mit den registrierten Geräten einrichten müssen, können Sie die Einstellungen mithilfe von Konfigurationselementen bereitstellen, sobald die Geräte registriert sind. Andernfalls können Sie ein zweites Paket mithilfe von Windows Bildverarbeitungs- und Konfigurations-Designer (Windows ICD) erstellen, und zusammen mit dem Massenregistrierungsprogramm bereitstellen.

##  <a name="bkmk_createEnroll"></a> Erstellen eines Anmeldungsprofils  
 Das Anmeldungsprofil ermöglicht Ihnen, Einstellungen festzulegen, die für die Registrierung der Geräte erforderlich sind, z. B. ein Zertifikatprofil, das dem Gerät dynamisch ein vertrauenswürdiges Stammzertifikat bereitstellt, und ein WLAN-Profil, das bei Bedarf die Netzwerkeinstellungen bereitstellt.  

 Stellen Sie vor dem Erstellen eines Anmeldungsprofils sicher, dass Sie über ein Zertifikatprofil und (falls erforderlich) ein WLAN-Profil verfügen. Weitere Informationen finden Sie unter [Erstellen eines Zertifikatprofils](#bkmk_createCert) und [Erstellen eines WLAN-Profils](#CreateWifi).  

#### <a name="to-create-an-enrollment-profile"></a>So erstellen Sie ein Anmeldungsprofil:  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** >**Übersicht** >**Alle firmeneigenen Geräte** >**Windows** >**Anmeldungsprofile**.  

2.  Klicken Sie mit der rechten Maustaste auf **Anmeldungsprofil** , und klicken Sie dann auf **Profil erstellen**.  

3.  Geben Sie im Assistenten zum Erstellen des Anmeldungsprofils einen Namen für das Profil ein, vergewissern Sie sich, dass **Lokal** für **Verwaltungsautorität**ausgewählt ist, und klicken Sie dann auf **Weiter**.  

4.  Wählen Sie den Standortcode aus, und klicken Sie auf **Weiter**.  

5.  Wählen Sie **Nur Intranet**aus, wählen Sie Anmeldungsproxypunkte aus, die vom Gerät zum Initiieren der Registrierung verwendet werden, und klicken Sie dann auf **Weiter**.  

6.  Wählen Sie das Zertifikatprofil aus, das das vertrauenswürdige Stammzertifikat enthält (dies ist das Profil, das Sie in [Create a certificate profile](#bkmk_createCert)erstellt haben), und klicken Sie auf **Weiter**.  

7.  Wählen Sie das WLAN-Profil mit den erforderlichen Netzwerkeinstellungen aus, mit denen die Geräte die Verbindung mit dem Intranet herstellen können (dies ist das Profil, das Sie in [Create a Wi-Fi profile](#CreateWifi)erstellt haben), und klicken Sie auf **Weiter**.  

    > [!NOTE]  
    >  Wenn Sie für Ihr Registrierungspaket kein WLAN Profil verwenden, überspringen Sie diesen Schritt.  

8.  Bestätigen Sie die Einstellungen für das Registrierungspaket, und klicken Sie auf **Weiter**. Klicken Sie auf **Schließen** , um den Assistenten zu beenden.  

##  <a name="bkmk_createPpkg"></a> Erstellen einer Registrierungspaketdatei (PPKG-Datei)  
 Das Registrierungspaket ist die Datei, die Sie für die Massenregistrierung von Geräten für die lokale Verwaltung mobiler Geräte verwenden.  Diese Datei muss mit Configuration Manager erstellt werden. Mithilfe von Windows Bildverarbeitungs- und Konfigurations-Designer ( Windows ICD) können Sie ähnliche Pakettypen erstellen, aber nur in Configuration Manager erstellte Pakete können verwendet werden, um Geräte vom Anfang bis zum Ende für die lokale Verwaltung mobiler Geräte zu registrieren. Mit Windows ICD erstellte Pakete können nur den für die Registrierung erforderlichen Benutzerprinzipalnamen (UPN) bereitstellen, den eigentlichen Registrierungsvorgang aber nicht ausführen.  

 Zum Erstellen des Registrierungspakets muss das Windows Assessment and Deployment Toolkit (ADK) für Windows 10 verwendet werden.  Stellen Sie sicher, dass auf dem Server mit der Configuration Manager-Konsole Version 1511 von Windows ADK installiert ist. Weitere Informationen finden Sie unter [Herunterladen von Kits und Tools für Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)im Abschnitt über das ADK.  

> [!TIP]  
>  Wenn Sie ein Registrierungspaket von der Configuration Manager-Konsole entfernen, kann es nicht mehr zum Registrieren von Geräten verwendet werden. Sie können zur Verwaltung von Paketen die Pakete entfernen, die nicht mehr für die Massenregistrierung von Geräten verwendet werden sollen.  

#### <a name="to-create-an-enrollment-package-ppkg-file"></a>So erstellen Sie eine Registrierungspaketdatei (PPKG-Datei)  

1.  Klicken Sie mit der rechten Maustaste auf das soeben erstellte Profil (in [Erstellen eines Anmeldungsprofils](#bkmk_createEnroll)), und klicken Sie auf **Exportieren**.  

2.  Klicken Sie auf **Durchsuchen**, navigieren Sie zu dem Verzeichnis, in dem die PPKG-Datei gespeichert werden soll, geben Sie einen Namen für das Paket ein, und klicken Sie dann auf **Speichern**.  

3.  Wenn Sie das Paket durch ein Kennwort schützen möchten, aktivieren Sie das Kontrollkästchen neben **Paket verschlüsseln**, klicken Sie auf **Exportieren** , und warten Sie etwa 10 Sekunden, bis der Export abgeschlossen ist.  

    > [!NOTE]  
    >  Wenn Sie das Paket verschlüsselt haben, zeigt Configuration Manager eine Nachricht mit dem entschlüsselten Kennwort an. Stellen Sie sicher, dass Sie sich die Kennwortinformationen notieren, da Sie sie zur Bereitstellung des Pakets auf Geräten benötigen.  

4.  Klicken Sie auf **OK**.  

##  <a name="bkmk_getPpkg"></a> Verwenden des Pakets für die Massenregistrierung eines Geräts  
 Sie können das Paket verwenden, um Geräte vor oder nach der Bereitstellung des Geräts mithilfe des OOBE-Prozesses (Out-of-Box-Experience) zu registrieren.   Das Registrierungspaket kann auch als Teil eines OEM-Bereitstellungspakets (Originalgerätehersteller, Original Equipment Manufacturer) hinzugefügt werden.  

 Das Paket muss physisch auf dem Gerät bereitgestellt werden, um es für die Massenregistrierung verwenden zu können. Sie können das Registrierungspaket, je nach Ihren Anforderungen, auf verschiedene Arten an das Gerät übermitteln, zum Beispiel:  

-   Durch Kopieren aus dem Dateisystem  

-   Durch Anfügen an eine E-Mail  

-   Durch Kopieren über eine NFC-Verbindung (Near Field Communication)  

-   Durch Kopieren von einer Speicherkarte  

-   Durch Scannen eines Barcodes  

-   Durch Kopieren von einem verbundenen Gerät  

-   Durch Hinzufügen zu einem OEM-Bereitstellungspaket  

#### <a name="to-bulk-enroll-a-device"></a>So führen Sie die Massenregistrierung eines Geräts aus  

1.  Suchen Sie auf dem zu registrierenden Gerät (mit dem Datei-Explorer) das Registrierungspaket, und doppelklicken Sie auf die PPKG-Datei.  

2.  Klicken Sie in der Meldung „Benutzerkontensteuerung“ auf **Ja** .  

3.  Klicken Sie im Dialogfeld, in dem Sie gefragt werden, ob das Paket aus einer vertrauenswürdigen Quelle stammt, auf **Ja, hinzufügen**.  

     Der Registrierungsvorgang beginnt und dauert etwa 5 Minuten.  

4.  Öffnen Sie **Einstellungen**.  

5.  Klicken Sie auf  **Konten** > **Arbeitsplatzzugriff**erforderlichen Standortsystemrollen benötigt. Wenn die Registrierung erfolgreich war, wird unter **CompanyApps**ein Konto angezeigt.  

6.  Klicken Sie auf das Konto und dann auf **Synchronisieren**. Dadurch wird die Verwaltung mit gestartet.  

##  <a name="bkmk_verifyEnroll"></a> Überprüfen der Registrierung des Geräts  
 Sie können überprüfen, ob Geräte in der Configuration Manager-Konsole erfolgreich registriert wurden.  

-   Starten Sie hierzu die Configuration Manager-Konsole.  

-   Klicken Sie auf **Bestand und Kompatibilität** > **Übersicht** > **Geräte**erforderlichen Standortsystemrollen benötigt. Das registrierte Gerät wird in der Liste angezeigt.  
