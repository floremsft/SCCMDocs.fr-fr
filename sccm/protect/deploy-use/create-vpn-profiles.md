---
title: Erstellen von VPN-Profilen in System Center Configuration Manager | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie VPN-Profile in System Center Configuration Manager erstellen.
ms.custom: 
ms.date: 4/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: "15"
author: lleonard-msft
caps.handback.revision: "0"
ms.author: alleonar
ms.manager: angrobe
ms.openlocfilehash: 359fcfd9754fb5c81763bc44cac45376ea3ab0b8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Erstellen von VPN-Profilen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die für verschiedene Geräteplattformen verfügbaren Verbindungstypen werden unter [VPN-Profile in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md) beschrieben.  

Verteilen Sie die VPN-App für Drittanbieter-VPN-Verbindungen vor der Bereitstellung des VPN-Profils. Wenn Sie die App nicht bereitstellen, werden die Benutzer dazu aufgefordert, sobald sie versuchen, sich mit dem VPN zu verbinden. Weitere Informationen zum Bereitstellen von Apps finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

### <a name="create-a-vpn-profile"></a>Erstellen eines VPN-Profils   

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Assets and Compliance** (Bestand und Konformität) > **Compliance Settings** (Konformitätseinstellungen) > **Company Resource Access** (Zugriff auf Unternehmensressourcen) > **VPN-Profiles** (VPN-Profile) aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Create VPN Profile** (VPN-Profil erstellen) aus.  


1.  Schließen Sie die Seite **Allgemein** ab. Beachten Sie dabei Folgendes:  

    - Verwenden Sie im Namen des VPN-Profils keines der Zeichen \\/:*?&lt;>&#124; und auch keine Leerzeichen. Diese Zeichen werden vom Windows Server-VPN-Profil nicht unterstützt.  

     -   Wählen Sie **Import an existing VPN profile item from a file** (Vorhandenes VPN-Profilelement aus einer Datei importieren) aus, um Informationen eines VPN-Profils zu importieren, das in eine XML-Datei exportiert wurde (nur Windows 8.1 oder Windows RT).  

1.  Geben Sie auf der Seite **Verbindung** Folgendes an:  

    -   **Verbindungstyp**: Wählen Sie den VPN-Verbindungstyp aus. Sie können aus den Verbindungstypen in der folgenden Tabelle wählen.  

    -   **Server list** (Serverliste): Fügen Sie einen neuen Server zur Verwendung für die VPN-Verbindung hinzu. Abhängig vom Verbindungstyp können Sie einen oder mehrere VPN-Server hinzufügen und den Standardserver angeben.  

        > [!NOTE]  
        >  Von iOS-Geräten wird die Verwendung mehrerer VPN-Server nicht unterstützt. Wenn Sie mehrere VPN-Server konfigurieren und dann das VPN-Profil auf einem iOS-Gerät bereitstellen, wird nur der Standardserver verwendet.  

     Diese Tabelle bietet Optionen für die Verbindungstypen. Weitere Informationen finden Sie in der Dokumentation zum VPN-Server.

| &nbsp;&nbsp;Option&nbsp;&nbsp; | Weitere Informationen | &nbsp;&nbsp;Verbindung&nbsp;Typ&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**Bereich**     |Der Authentifizierungsbereich, den Sie verwenden möchten. Ein Authentifizierungsbereich ist eine Gruppe von Authentifizierungsressourcen, die vom Verbindungstyp „Pulse Secure“ verwendet werden.|Pulse Secure|    
|**Rolle**        |Die Benutzerrolle, die Zugriff auf diese Verbindung hat. |Pulse Secure|  
|**Anmeldegruppe oder Domäne** |Der Name der Anmeldegruppe oder Domäne, mit der Sie eine Verbindung herstellen möchten.|Dell SonicWALL Mobile Connect|  
|**Fingerabdruck**  |Eine Zeichenfolge wie z.B. „Contoso-Fingerabdruckcode“, anhand der überprüft wird, ob der VPN-Server vertrauenswürdig ist.<br /><br /> Mit einem Fingerabdruck kann wie folgt verfahren werden:<br /><br /> – Er kann an den Client gesendet werden, damit dieser weiß, dass alle Server vertrauenswürdig sind, die beim Verbinden den betreffenden Fingerabdruck vorweisen.<br /><br /> – Wenn das Gerät nicht über den Fingerabdruck verfügt, wird der Benutzer aufgefordert, dem VPN-Server zu vertrauen, mit dem eine Verbindung hergestellt wird, während der Fingerabdruck angezeigt wird (der Benutzer überprüft den Fingerabdruck manuell und wählt **Vertrauen** aus, um die Verbindung herzustellen).|Prüfpunkt für mobiles VPN|  
|**Gesamten Netzwerkdatenverkehr über die VPN-Verbindung senden** |Wenn diese Option nicht ausgewählt ist, können Sie zusätzliche Routen für die Verbindung angeben (für die Verbindungstypen **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** und **L2TP** ). Dies wird auch als getrenntes Tunneln oder VPN-Tunneln bezeichnet.<br /><br /> Nur Verbindungen mit dem Unternehmensnetzwerk werden über einen VPN-Tunnel gesendet. Beim Verbinden mit Ressourcen im Internet wird VPN-Tunneln nicht verwendet. |Alle|  
|**Verbindungsspezifisches DNS-Suffix** |Das verbindungsspezifische DNS-Suffix (Domain Name System) für die Verbindung.|– Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – PPTP<br /><br /> – L2TP|  
|**VPN beim Verbinden mit Unternehmens-WLAN-Netzwerk umgehen**  |Die VPN-Verbindung wird nicht verwendet, wenn das Gerät mit dem Unternehmens-WLAN verbunden ist.|– Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN<br /><br /> – Microsoft SSL (SSTP)<br /><br /> – Microsoft Automatic<br /><br /> – IKEv2<br /><br /> – L2TP|  
|**VPN beim Verbinden mit WLAN-Heimnetzwerk umgehen**  |Die VPN-Verbindung wird nicht verwendet, wenn das Gerät mit einem WLAN-Heimnetzwerk verbunden ist.|Alle|  
|**VPN pro App (iOS 7 und höher, Mac OS X 10.9 und höher)** |Ordnet diese VPN-Verbindung einer iOS-App zu, sodass die Verbindung geöffnet wird, wenn die Anwendung ausgeführt wird. Die Zuordnung des VPN-Profils zu einer App kann bei der Bereitstellung erfolgen.|– Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  
|**Benutzerdefiniertes XML (optional)** |Gibt benutzerdefinierte XML-Befehle zum Konfigurieren der VPN-Verbindung an.<br /><br /> Beispiele:<br /><br /> Für **Pulse Secure**:<br /><br /> **&lt;Pulse-Schema ><br /> &nbsp; &lt;IsSingleSignOnCredential > true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema >**<br /><br /> Für **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> Für **Dell SonicWALL Mobile Connect**:<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> Für **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> Weitere Informationen über das Schreiben von benutzerdefinierten XML-Befehlen finden Sie in der VPN-Dokumentation der einzelnen Hersteller.|– Cisco AnyConnect<br /><br /> – Pulse Secure<br /><br /> – F5 Edge Client<br /><br /> – Dell SonicWALL Mobile Connect<br /><br /> – Prüfpunkt für mobiles VPN|  

> [!NOTE]  
>  Informationen zum Erstellen von VPN-Profilen für mobile Geräte finden Sie unter [Erstellen von VPN-Profilen](../../mdm/deploy-use/create-vpn-profiles.md)  

Schließen Sie den Assistenten ab. Das neue VPN-Profil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **VPN-Profile** angezeigt.

### <a name="next-steps"></a>Nächste Schritte

- Verteilen Sie die VPN-App für Drittanbieter-VPN-Verbindungen vor der Bereitstellung des VPN-Profils. Wenn Sie die App nicht bereitstellen, werden die Benutzer dazu aufgefordert, sobald sie versuchen, sich mit dem VPN zu verbinden. Weitere Informationen zum Bereitstellen von Apps finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

- Stellen Sie die VPN-Profile wie in [Erstellen von VPN-Profilen in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) beschrieben bereit.  
