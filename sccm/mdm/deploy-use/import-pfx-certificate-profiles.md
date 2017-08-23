---
title: Erstellen von PFX-Zertifikatprofilen durch Importieren von Zertifikatdetails | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie PFX-Dateien in System Center Configuration Manager verwenden, um benutzerspezifische Zertifikate zu generieren, die den verschlüsselten Datenaustausch unterstützen."
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: c8346d04c7cd9761291824f5d30f09fab9acbcf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>Erstellen von PFX-Zertifikatprofilen durch Importieren von Zertifikatdetails

*Gilt für: System Center Configuration Manager (Current Branch)*


Hier erfahren Sie, wie Sie ein Zertifikatprofil erstellen, indem Sie die Anmeldeinformationen aus externen Zertifikaten importieren.  

Unter [Zertifikatprofile](../../protect/deploy-use/introduction-to-certificate-profiles.md) erhalten Sie allgemeine Informationen zum Erstellen und Konfigurieren von Zertifikatprofilen. In diesem Thema erfahren Sie Genaueres über Zertifikatprofile, die mit PFX-Zertifikatprofilen in Verbindung stehen.

-  Configuration Manager unterstützt diverse Zertifikatspeicher für verschiedene Geräte und Betriebssysteme.  Dazu gehören:

 -   iOS und MacOS/OSX
 -   Android und Android for Work
 -   Windows 10, einschließlich Windows 10 Mobile

Weitere Informationen erhalten Sie unter [Voraussetzungen für Zertifikatprofile in System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>PFX-Zertifikatprofile
System Center Configuration Manager ermöglicht Ihnen den Import und die anschließende Bereitstellung von PFX-Dateien (Personal Information Exchange) für Benutzergeräte. PFX-Dateien können zum Generieren benutzerspezifischer Zertifikate zur Unterstützung eines verschlüsselten Datenaustausches verwendet werden.

> [!TIP]  
>  Unter [Erstellen und Bereitstellen von PFX-Zertifikatprofilen in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)finden Sie eine schrittweise exemplarische Vorgehensweise für diesen Vorgang.  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Erstellen, importieren und bereitstellen eines PFX-Zertifikatprofils (Personal Information Exchange)  

### <a name="get-started"></a>Erste Schritte

1.  Klicken Sie in der System Center Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  
2.  Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, den **Zugriff auf Unternehmensressourcen**, und klicken Sie dann auf **Zertifikatprofile**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Zertifikatprofil erstellen**.

4.  Geben Sie auf der Seite **Allgemein** des ****  Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

    -   **Name**: Geben Sie einen eindeutigen Namen für das Zertifikatprofil ein. Sie können maximal 256 Zeichen verwenden.  

    -   **Beschreibung**: Geben Sie eine Beschreibung mit einem Überblick über das Zertifikatprofil sowie weitere relevante Informationen ein, die der Identifikation des Profils in der System Center Configuration Manager-Konsole dienen. Sie können maximal 256 Zeichen verwenden.  

    -   **Geben Sie den Typ des Zertifikatprofils an, das Sie erstellen möchten**: Wählen Sie bei PFX-Zertifikaten eine der folgenden Optionen aus:  

        -   **Personal Information Exchange PKCS #12 (PFX)-Einstellungen – Import**: Erstellt ein Zertifikatprofil, indem programmatisch Informationen aus existierenden Zertifikaten importiert werden.  

        -   **Personal Information Exchange PKCS #12 (PFX)-Einstellungen - Erstellen**: Erstellt ein Zertifikatprofil mithilfe von Anmeldeinformationen, die von einer Zertifizierungsstelle bereitgestellt werden.  Weitere Informationen erhalten Sie unter [How to create PFX certificate profiles using a certificate authority](../../mdm/deploy-use/create-pfx-certificate-profiles.md) Erstellen von PFX-Zertifikatprofilen mithilfe einer Zertifizierungsstelle.


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>Erstellen eines PFX-Zertifikatprofils für importierte Anmeldeinformationen

Beim Import eines PFX-Zertifikats verwenden Sie das Configuration Manager SDK, um ein PFX-Erstellungsskript bereitzustellen. 

Importierte Zertifikate werden später registrierten Geräten bereitgestellt.

1. Geben Sie auf der Seite **PFX-Zertifikat** des **Assistenten zum Erstellen von Zertifikatprofilen** die folgenden Informationen an:
    -   **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  
    -   **In Trusted Platform Module (TPM) installieren (andernfalls Fehler)** 
    -   **In Windows Hello for Business installieren (andernfalls Fehler)** 
    -   **In Softwareschlüsselspeicher-Anbieter installieren** 
2. Klicken Sie auf **Weiter**. 
3. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die unterstützten Geräteplattformen aus und klicken sie anschließend auf **Weiter**.

### <a name="finish-the-profile"></a>Fertigstellen des Profils

1.  Klicken Sie auf **Weiter**, überprüfen Sie die Seite **Zusammenfassung** , und schließen Sie dann den Assistenten.  
2.  Das Zertifikatprofil mit der PFX-Datei steht nun im Arbeitsbereich **Zertifikatprofile** bereit. 
3.  Um das Profil bereitzustellen, öffnen Sie im Arbeitsbereich **Bestand und Konformität** **Konformitätseinstellungen** > **Zugriff auf Unternehmensressourcen** > **Zertifikatprofile**, klicken Sie mit der rechten Maustaste auf das gewünschte Zertifikat und anschließend auf **Bereitstellen**. 

### <a name="deploy-a-create-pfx-script"></a>Bereitstellen eines PFX-Erstellungsskripts

Nutzen Sie das [Configuration Manager SDK](http://go.microsoft.com/fwlink/?LinkId=613525), um ein PFX-Erstellungsskript bereitzustellen. 

Mit dem PFX-Erstellungsskript, das in Configuration Manager 2012 SP2 hinzugefügt wurde, wird eine SMS_ClientPfxCertificate-Klasse zum SDK hinzugefügt. Diese Klasse enthält die folgenden Methoden:  

    -   `ImportForUser`  

    -   `DeleteForUser`  

Im folgende Beispiel werden Anmeldeinformationen in ein PFX-Zertifikatprofil importiert.

``` powershell
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  
```  

Aktualisieren Sie die folgenden Skriptvariablen, um diese Beispiel verwenden zu können:  

   -   **blob**\ – Das Base64-verschlüsselte PFX-Blob  
   -   **$Password** – Das Kennwort für die PFX-Datei  
   -   **$ProfileName** – der Name des PFX-Profils  
   -   **ComputerName** – der Name des Hostcomputers   

## <a name="see-also"></a>Weitere Informationen:
[Create a new certificate profile (Erstellen eines neuen Zertifikatprofils)](../../protect/deploy-use/create-certificate-profiles.md) begleitet Sie im Assistenten für das Erstellen eines Zertifikatprofils.

[How to create PFX certificate profiles by importing certificate details](../../mdm/deploy-use/create-pfx-certificate-profiles.md) (Erstellen von PFX-Zertifikatprofilen durch Importieren von Zertifikatdetails)

Unter [Deploy Wi-Fi, VPN, email, and certificate profiles](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) (Bereitstellen von Profilen in System Center Configuration Manager) wird beschrieben, wie Sie Zertifikatprofile bereitstellen.