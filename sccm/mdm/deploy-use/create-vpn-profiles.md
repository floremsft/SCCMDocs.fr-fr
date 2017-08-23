---
title: VPN-Profile in System Center Configuration Manager | Microsoft-Dokumentation
description: "VPN-Profile für mobile Geräte in System Center Configuration Manager."
ms.custom: na
ms.date: 07/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: "18"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: e4a53caab7d76b604a3fee7dcfc4dc48f22b0fb0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>VPN-Profile für mobile Geräte in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie VPN-Profile in System Center Configuration Manager, um Benutzern mobiler Geräte in Ihrer Organisation VPN-Einstellungen bereitzustellen. Wenn Sie diese Einstellungen bereitstellen, erleichtern Sie den Endbenutzern das Herstellen von Verbindungen mit Ressourcen im Unternehmensnetzwerk.  

 Ein Beispiel: Sie möchten alle Geräte, auf denen das iOS-Betriebssystem ausgeführt wird, mit den Einstellungen einrichten, die zum Herstellen einer Verbindung mit einer Dateifreigabe im Unternehmensnetzwerk erforderlich sind. Sie können ein VPN-Profil mit den zum Herstellen einer Verbindung mit dem Unternehmensnetzwerk erforderlichen Einstellungen erstellen und dieses Profil dann für alle Benutzer mit Geräten unter iOS in der Hierarchie bereitstellen. Benutzer von iOS-Geräten sehen die VPN-Verbindung in der Liste der verfügbaren Netzwerke und können sich mühelos mit diesem Netzwerk verbinden.  

 Wenn Sie ein VPN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen einrichten. Sie können z.B. Zertifikate für die Serverüberprüfung und Clientauthentifizierung angeben, die mithilfe von System Center Configuration Manager-Zertifikatprofilen bereitgestellt wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>VPN-Profile bei der Verwendung von Configuration Manager mit Intune

 Um Profile für Android-, iOS-, Windows Phone- und Windows 8.1-Geräte bereitzustellen, müssen diese Geräte bei Microsoft Intune registriert werden. Geräte auf anderen Plattformen können ebenfalls bei Intune registriert werden. Informationen zum Registrieren finden Sie unter [Verwalten von Geräten für die Verwaltung in Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Diese Tabelle zeigt, welcher Verbindungstyp für jede Geräteplattform unterstützt wird:  

 |Verbindungstyp|iOS und macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop und Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Ja|Ja|Nein|Nein|Nein|Nein|Ja (OMA-URI)|
 |Cisco (IPSec)|nur iOS|Nein|Nein|Nein|Nein|Nein|Nein|  
 |Pulse Secure|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
 |F5 Edge Client|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
 |Dell SonicWALL Mobile Connect|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
 |Prüfpunkt für mobiles VPN|Ja|Ja|Ja|Nein|Ja|Ja|Ja|  
 |Microsoft SSL (SSTP)|Nein|Nein|Ja|Ja|Ja|Nein|Nein|  
 |Microsoft Automatic|Nein|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  
 |IKEv2|Ja (Benutzerdefinierte Richtlinie)|Nein|Ja|Ja|Ja|Ja|Ja (OMA-URI)|  
 |PPTP|Ja|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  
 |L2TP|Ja|Nein|Ja|Ja|Ja|Nein|Ja (OMA-URI)|  

## <a name="create-vpn-profiles"></a>Erstellen von VPN-Profilen
Allgemeine Informationen zum Erstellen von VPN-Profilen finden Sie unter [Erstellen von VPN-Profilen in System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md).

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Bei der Verwendung von Configuration Manager mit Intune verfügbare Windows 10-VPN-Features  


> [!NOTE]  
> Der Name eines VPN-Profils mit Windows 10-VPN-Features darf keine Unicode- oder Sonderzeichen enthalten.


|Option|Weitere Informationen|Verbindungstyp|  
    |------------|----------------------|---------------------|  
    |**VPN beim Verbinden mit Unternehmens-WLAN-Netzwerk umgehen**|Die VPN-Verbindung wird nicht verwendet, wenn das Gerät mit dem Unternehmens-WLAN verbunden ist. Geben Sie den Namen des vertrauenswürdigen Netzwerks ein, das verwendet wird, um zu ermitteln, ob das Gerät mit dem Unternehmensnetzwerk verbunden ist.|Alle|  
    |**Regeln für den Netzwerkdatenverkehr**|Legen Sie die Protokolle, die lokalen und Remoteports sowie die Adressbereiche fest, die für die VPN-Verbindung aktiviert werden sollen.<br /><br /> **Hinweis:** Wenn Sie keine Regel für den Netzwerkdatenverkehr erstellen, werden alle Protokolle, Ports und Adressbereiche aktiviert. Nachdem Sie eine Regel erstellt haben, werden nur die in dieser oder weiteren Regeln festgelegten Protokolle, Ports und Adressbereiche von der VPN-Verbindung verwendet.|Alle|  
    |**Routen**|Die Routen, die die VPN-Verbindung verwenden. Beachten Sie, dass die Erstellung von mehr als 60 Routen Richtlinienfehler herbeiführen kann. |Alle|  
    |**DNS-Server**|Die DNS-Server, die von der VPN-Verbindung verwendet werden, nachdem die Verbindung hergestellt wurde.|Alle|  
    |**Apps, die automatisch eine Verbindung mit dem VPN herstellen**|Sie können Apps hinzufügen oder App-Listen importieren, die automatisch die VPN-Verbindung verwenden. Der App-Typ bestimmt den App-Bezeichner. Stellen Sie für eine Desktop-App den Dateipfad der App bereit. Stellen Sie für eine universelle App den Paketfamiliennamen (package family name; PFN) bereit. Informationen dazu, wie Sie den PFN einer App herausfinden, finden Sie unter [Find a package family name for per-app VPN (Suchen eines Paktefamiliennamens für Pro-App-VPN)](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |Alle|

> [!IMPORTANT]
> Es wird empfohlen, alle Listen der zugeordneten Apps zu sichern, die Sie für die Konfiguration des Pro-App-VPN kompilieren. Wenn ein nicht autorisierter Benutzer die Liste ändert und Sie die Liste in die Pro-App-VPN-Liste importieren, gewähren Sie möglicherweise VPN-Zugriff für Apps, die keinen Zugriff erhalten sollten. Eine Möglichkeit, die App-Listen zu sichern, besteht in der Verwendung einer Zugriffssteuerungsliste (access control list; ACL).


1.  Geben Sie auf der Seite **Authentifizierungsmethode** des Assistenten Folgendes an:  

    -   **Authentifizierungsmethode**: Wählen Sie die Authentifizierungsmethode für die VPN-Verbindung aus. Verfügbare Methoden hängen vom Verbindungstyp ab, wie in dieser Tabelle gezeigt.  

        |Authentifizierungsmethode|Unterstützte &nbsp;Verbindungstypen&nbsp;|  
        |---------------------------|--------------------------------|  
        |**Zertifikate**<br /><br /> **Hinweise:**<ul><li>Wenn für die Authentifizierung bei einem RADIUS-Server, wie z.B. einem Netzwerkrichtlinienserver, ein Clientzertifikat verwendet wird, muss der alternative Antragstellername im Zertifikat auf den Benutzerprinzipalnamen festgelegt werden.</li><li>Wählen Sie für Android-Bereitstellungen den EKU-Bezeichner und den Fingerabdruck-Hashwert des Zertifikatausstellers aus.  Andernfalls müssen Benutzer das entsprechende Zertifikat manuell auswählen.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Prüfpunkt für mobiles VPN</li></ul>|  
        |**Benutzername und Kennwort**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Prüfpunkt für mobiles VPN</li></ul>|  
        |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
        |**Microsoft-gesichertes EAP (PEAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Microsoft-gesichertes Kennwort (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Smartcard- oder anderes Zertifikat**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**RSA SecurID** (nur iOS)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Computerzertifikate verwenden**|<ul><li>IKEv2</li></ul>|  

         Je nach ausgewählten Optionen werden Sie möglicherweise aufgefordert, weitere Informationen wie beispielsweise die folgenden anzugeben:  

        -   **Benutzeranmeldeinformationen bei jeder Anmeldung speichern**: Benutzeranmeldeinformationen werden gespeichert, sodass die Benutzer diese nicht bei jeder Verbindungsherstellung eingeben müssen.  

        -   **Clientzertifikat für Clientauthentifizierung auswählen**: Wählen Sie das zuvor erstellte [SCEP-Clientzertifikat](create-pfx-certificate-profiles.md) aus, das zur Authentifizierung der VPN-Verbindung verwendet wird.   

            > [!NOTE]  
            >  Bei iOS-Geräten wird das von Ihnen ausgewählte SCEP-Profil in das VPN-Profil eingebettet. Bei anderen Plattformen wird eine Anwendbarkeitsregel hinzugefügt, um sicherzustellen, dass das VPN-Profil nicht installiert wird, wenn das Zertifikat nicht vorhanden oder nicht kompatibel ist.  
            >   
            >  Wenn das von Ihnen angegebene SCEP-Zertifikat nicht kompatibel ist oder nicht bereitgestellt wurde, wird das VPN-Profil nicht auf dem Gerät installiert.
            >  
            >  Geräte unter iOS unterstützen nur RSA SecurID und MSCHAP v2 als Authentifizierungsmethode, wenn der Verbindungstyp PPTP lautet. Um die Ausgabe von Fehlern zu vermeiden, stellen Sie auf Geräten unter IOS ein separates PPTP-VPN-Profil bereit.  

        - **Bedingter Zugriff**
            - Wählen Sie **Enable conditional access for this VPN connection** (Bedingten Zugriff für diese VPN-Verbindung aktivieren) aus, um sicherzustellen, dass Geräte, die eine Verbindung mit dem VPN herstellen, vor der Verbindung auf Konformität mit bedingtem Zugriff getestet werden. Weitere Informationen zu Kompatibilitätsrichtlinien finden Sie unter [Richtlinien zur Gerätekompatibilität in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md).
            - Wählen Sie **Einmaliges Anmelden (SSO) mit alternativem Zertifikat aktivieren** aus, um ein anderes Zertifikat als das Zertifikat für die VPN-Authentifizierung für die Gerätekompatibilität auszuwählen. Wenn Sie diese Option auswählen, geben Sie die **EKU** (durch Trennzeichen getrennte Liste) und den **Ausstellerhash** an, um das richtige Zertifikat auszuwählen, das der VPN-Client suchen soll.

         - Geben Sie unter **Windows Information Protection** die vom Unternehmen verwaltete Unternehmensidentität an. Dies ist normalerweise die primäre Domäne Ihres Unternehmens, z.B. *contoso.com*. Sie können mehrere Domänen angeben, die Ihrer Organisation gehören, indem Sie sie durch das Zeichen „|“ trennen. Beispiel: *contoso.com|newcontoso.com*.   
            Weitere Informationen zu Windows Information Protection finden Sie unter [Erstellen einer Windows Information Protection-Richtlinie (WIP) mit Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Konfigurieren des bedingten Zugriffs für VPN](media/vpn-conditional-access.png)

         Wenn der Vorgang von der Windows-Version, die Configuration Manager ausführt, _und_ der ausgewählten Autorisierungsmethode unterstützt wird, können Sie auf **Konfigurieren** klicken, um das Dialogfeld mit den Windows-Eigenschaften zu öffnen und die Eigenschaften der Authentifizierungsmethode zu konfigurieren.  Wenn **Konfigurieren** deaktiviert ist, verwenden Sie andere Möglichkeiten zum Konfigurieren der Eigenschaften der Authentifizierungsmethode.

2.  Aktivieren Sie auf der Seite **Proxyeinstellungen** des **Assistenten zum Erstellen von VPN-Profilen**das Kontrollkästchen **Proxyeinstellungen für dieses VPN-Profil konfigurieren**, wenn Ihre VPN-Verbindung einen Proxyserver verwendet. Geben Sie dann die Proxyserverinformationen an. Weitere Informationen finden Sie in der Windows Server-Dokumentation.  

    > [!NOTE]  
    >  Auf Windows 8.1-Computern zeigt das VPN-Profil die Proxyinformationen erst an, wenn Sie mit dem betreffenden Computer eine Verbindung zu dem VPN herstellen.  


3. Konfigurieren Sie weitere DNS-Einstellungen (falls erforderlich).  
 Auf der Seite **Automatische VPN-Verbindung konfigurieren** können Sie Folgendes konfigurieren:  

    -   **VPN bedarfsgesteuert aktivieren**: Verwenden Sie diese Option, wenn Sie weitere DNS-Einstellungen für Windows Phone 8.1-Geräte konfigurieren möchten. Diese Einstellung gilt nur für Windows Phone 8.1-Geräte und sollte nur auf VPN-Profilen aktiviert werden, die für Windows Phone 8.1-Geräte bereitgestellt werden.

    -   **DNS-Suffixliste** (nur Windows Phone 8.1-Geräte): Konfiguriert Domänen, die eine VPN-Verbindung herstellen. Fügen Sie für jede Domäne, die Sie angeben, das DNS-Suffix, die DNS-Serveradresse und eine der folgenden bedarfsgesteuerten Aktionen hinzu:  

        -   **Nie herstellen**: Es wird niemals eine VPN-Verbindung geöffnet.  

        -   **Bei Bedarf herstellen**: Es wird nur dann eine VPN-Verbindung geöffnet, wenn das Gerät eine Verbindung zu Ressourcen herstellen muss.  

        -   **Immer herstellen**: Die VPN-Verbindung wird immer geöffnet.  

    -   **Zusammenführen**: Kopiert alle von Ihnen konfigurierten DNS-Suffixe in die **Liste vertrauenswürdiger Netzwerke**.  

    -   **Liste vertrauenswürdiger Netzwerke** (nur Windows Phone 8.1-Geräte): Geben Sie in jeder Zeile ein DNS-Suffix an. Wenn sich das Gerät in einem vertrauenswürdigen Netzwerk befindet, wird die VPN-Verbindung nicht geöffnet.  

    -   **Suffixsuchliste** (nur Windows Phone 8.1-Geräte): Geben Sie in jeder Zeile ein DNS-Suffix an. Jedes DNS-Suffix wird beim Verbinden mit einer Website unter Verwendung eines Kurznamens gesucht.  

     Beispiel: Sie geben die DNS-Suffixe **domain1.contoso.com** und **domain2.contoso.com** an und besuchen dann die URL **http://mywebsite**. Die folgenden Adressen werden gesucht.  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Nur für Windows Phone 8.1-Geräte  
    >   
    >  Wenn die Option *Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden* ausgewählt ist *und* die VPN-Verbindung vollständiges Tunneln verwendet, wird die VPN-Verbindung automatisch mit dem ersten Geräteprofil geöffnet. Um eine Verbindung mit einem anderen Profil zu öffnen, legen Sie das gewünschte Profil als Standard fest.  
    >   
    >  Wenn die Option *Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden* *nicht* ausgewählt ist *und* die VPN-Verbindung getrenntes Tunneln verwendet, werden VPN-Verbindungen automatisch für konfigurierte Routen oder verbindungsspezifische DNS-Suffixe geöffnet.  


4. Wählen Sie auf der Seite **Unterstützte Plattformen** des **Assistenten zum Erstellen von VPN-Profilen** die Betriebssysteme aus, unter denen das VPN-Profil installiert wird, oder klicken Sie auf **Alle auswählen**, um das VPN-Profil unter allen verfügbaren Betriebssystemen zu installieren.  

5. Beenden Sie den Assistenten. Das neue VPN-Profil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **VPN-Profile** angezeigt.  


**Bereitstellen**: Weitere Informationen zum Bereitstellen von VPN-Profilen finden Sie unter [Bereitstellen von WLAN-, VPN-, E-Mail- und Zertifikatprofilen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

### <a name="next-steps"></a>Nächste Schritte  
 Die folgenden Themen helfen Ihnen beim Planen, Einrichten, Betreiben und Verwalten von VPN-Profilen in Configuration Manager.  

-   [Prerequisites for VPN profiles in System Center Configuration Manager (Voraussetzungen für VPN-Profile in System Center Configuration Manager)](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Security and privacy for VPN profiles in System Center Configuration Manager (Sicherheit und Datenschutz für VPN-Profile in System Center Configuration Manager)](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
