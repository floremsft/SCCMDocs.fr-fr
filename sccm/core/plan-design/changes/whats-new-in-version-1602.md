---
title: Neuerungen in Version 1602 von System Center Configuration Manager | Microsoft-Dokumentation
description: "Enthält Details zu Änderungen und neuen Funktionen, die in Version 1602 von System Center Configuration Manager eingeführt wurden."
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 9a548f43625a907173e7b967d26356bd80f1c5d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>Neuerungen in Version 1602 von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Das Update 1602 für System Center Configuration Manager ist nur als konsoleninternes Update für zuvor installierte Standorte verfügbar, die Version 1511 ausführen. 1511 ist die anfängliche Baselineversion, die Sie verwenden, um einen neuen Configuration Manager-Standort zu installieren.  


> [!TIP]  
>  Weitere Informationen:  
>   
>   -   [Installing new sites (Installieren von neuen Standorten)](/sccm/core/servers/deploy/install) (mithilfe einer Baseline-Version wie 1511)  
>   -   [Installing updates at sites (Installieren von Updates an Standorten)](/sccm/core/servers/manage/updates) (z.B. Update 1602)  

 Die folgenden Abschnitte enthalten Details zu Änderungen und neue Funktionen, die in Version 1602 von Configuration Manager eingeführt wurden.  

## <a name="site-infrastructure"></a>Infrastruktur von Standorten  

###  <a name="bkmk_UpgradeOS"></a> Direktes Upgrade des Betriebssystems von Standortservern, auf denen Windows Server 2008 R2 ausgeführt wird  
 Configuration Manager-Standorte, die Version 1602 oder höher ausführen, unterstützen das direkte Upgrade des Betriebssystems von Standortservern von Windows Server 2008 R2 auf Windows Server 2012 R2.  

> [!WARNING]  
>  Vor dem Upgrade auf Windows Server 2012 R2 müssen Sie WSUS 3.2 vom Server deinstallieren.  
>   
>  Informationen zu diesem wichtigen Schritt finden Sie im Abschnitt „Neue und geänderte Funktionalität“ in der [Übersicht über Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) in der Windows Server-Dokumentation.  

 Um einen Server upzugraden, verwenden Sie die Windows Server 2012 R2-Upgradeverfahren. Sie müssen nach dem Upgrade keine Configuration Manager-Standortserverwiederherstellung ausführen. Informationen zu Upgradeverfahren finden Sie unter [Upgradeoptionen für Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) in der Windows Server-Dokumentation.  

###  <a name="bkmk_AOAG"></a> SQL Server AlwaysOn-Verfügbarkeitsgruppen  
 Verwenden Sie SQL Server Always On-Verfügbarkeitsgruppen zum Hosten der Standortdatenbank an primären Standorten und am Standort der zentralen Verwaltung als Lösung für hohe Verfügbarkeit und Notfallwiederherstellung.  

 Weitere Informationen finden Sie unter [SQL Server Always On für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung  

### <a name="windows-10-servicing"></a>Windows 10-Wartung  
 Die folgenden Verbesserungen für die Wartung von Windows 10 wurden der Configuration Manager-Version 1602 hinzugefügt:  

-   Neue Filteroptionen sind für Wartungspläne verfügbar, mit denen Sie nach **Sprache**, **Erforderlich** und **Titel** filtern können. Nur Upgrades, die die angegebenen Kriterien erfüllen, werden der entsprechenden Bereitstellung hinzugefügt.  

-   Wenn Sie die Klassifizierung **Upgrades** für die Softwareupdatesynchronisierung verwenden, wird eine Warnung angezeigt. Diese Warnung teilt Ihnen mit, dass [Hotfix 3095113](https://support.microsoft.com/kb/3095113) für Windows Server Update Services 4.0 (WSUS) erforderlich ist, bevor Sie die Softwareupdates erfolgreich synchronisieren können, bzw. damit die Windows 10-Wartung ordnungsgemäß funktioniert. Über die Warnmeldung gelangen Sie zum dazugehörigen Knowledge Base-Artikel.  

-   Verfügbare Windows 10-Upgrades werden jetzt nur im Knoten **Windows 10-Wartung** \ **Alle Windows 10-Updates** der Configuration Manager-Konsole angezeigt. Diese Updates werden im Knoten **Softwareupdates** \ **Alle Softwareupdates** der Konsole nicht mehr angezeigt.  

-   Ein Wartungsplan wird als Bereitstellung mit hohem Risiko eingestuft. Im Fenster **Sammlung auswählen** werden nur die benutzerdefinierten Sammlungen angezeigt, die den in den Eigenschaften des Standorts konfigurierten Einstellungen zur Bereitstellungsüberprüfung entsprechen. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   Benutzer, die ein Windows 10-Upgradepaket starten, erhalten nun eine Meldung, dass sie ihr Betriebssystem upgraden.  

## <a name="application-management"></a>Anwendungsverwaltung  

### <a name="ios-app-configuration-policies"></a>Richtlinien zur Konfiguration von iOS-Apps  
 Verwenden Sie Konfigurationsrichtlinien für Configuration Manager-Apps, um Einstellungen anzugeben, die beim Ausführen einer iOS-App durch den Benutzer erforderlich sein können. Eine App kann beispielsweise anfordern, dass der Benutzer eine benutzerdefinierte Portnummer, Sprache, Sicherheitseinstellungen oder Brandingeinstellungen, wie z.B. ein Unternehmenslogo, angibt. Wenn diese Einstellungen nicht ordnungsgemäß eingegeben werden, kann dies zur erhöhten Belastung Ihres Helpdesks führen und zudem die Übernahme der neuen Apps verlangsamen.  

 Mit Konfigurationsrichtlinien für Apps können Sie diese Probleme beseitigen, da Sie diese Einstellungen für Benutzer in einer Richtlinie bereitstellen können, bevor die Benutzer die App ausführen. Die Einstellungen werden dann automatisch bereitgestellt, und der Benutzer muss keine weitere Aktion durchführen. Weitere Einzelheiten finden Sie unter [Configure iOS apps with app configuration policies in System Center Configuration Manager (Konfigurieren von iOS-Apps mit Konfigurationsrichtlinien für Apps in System Center Configuration Manager)](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

### <a name="manage-volume-purchased-ios-apps"></a>Manage volume-purchased iOS apps  
 Configuration Manager kann Ihnen bei der Bereitstellung und Verwaltung von Apps helfen, die Sie per Volumenlizenz über das Apple Volume-Purchase Program (VPP) gekauft haben. Configuration Manager importiert die Lizenzinformationen aus dem App Store und verfolgt, wie viele Lizenzen Sie verwendet haben.  

 Weitere Informationen finden Sie unter [Manage volume-purchased iOS apps with System Center Configuration Manager (Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden, mit System Center Configuration Manager)](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

### <a name="automatic-creation-of-office-mobile-apps"></a>Automatische Erstellung von mobilen Office-Apps  
 Beim Update auf Version 1602 von 1511 erstellt Configuration Manager automatisch die folgenden mobilen Microsoft Office-Apps für Android und iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (nur iOS)  

-   Microsoft Outlook  

Diese Apps werden im Knoten **Anwendungen** der Configuration Manager-Konsole angezeigt.  

 Weitere Informationen zum Bereitstellen von Anwendungen finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Softwareupdates  

### <a name="manage-office-365-client-updates"></a>Verwalten von Updates von Office 365-Clients  
 System Center Configuration Manager bietet die Möglichkeit zum Verwalten von Updates von Office 365-Clients mithilfe des Workflows zum Verwalten von Softwareupdates. Weitere Informationen finden Sie unter [Verwalten von Office 365 ProPlus-Updates mit System Center Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).  

## <a name="compliance-settings"></a>Kompatibilitätseinstellungen  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Konformitätseinstellungen für Geräte mit Windows 10 Team  
 Neue Einstellungen wurden dem **Windows 8.1 und Windows 10**-Konfigurationselement hinzugefügt. Mithilfe dieser Einstellungen können Sie Geräte steuern, auf denen Windows 10 Team ausgeführt wird, wie z.B. ein Surface Hub-Gerät.  

 Einzelheiten finden Sie unter [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client (Erstellen von Konfigurationselementen für Windows 8.1- und Windows 10-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden)](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Einstellungen für den Kioskmodus für Android Samsung KNOX Standard-Geräte  
 Über den Kioskmodus können Sie ein Gerät sperren, damit nur bestimmte Features funktionieren. Beispielsweise können Sie festlegen, dass auf einem Gerät nur eine von Ihnen angegebene verwaltete App ausgeführt werden kann, oder Sie können die Lautstärkeregler eines Geräts deaktivieren. Diese Einstellungen können für ein Demomodell eines Geräts oder ein Gerät nützlich sein, das nur eine bestimmte Funktion ausführen soll, wie z.B. ein Point-of-Sale-Gerät. In Configuration Manager können Sie jetzt Einstellungen für den Kioskmodus für Samsung KNOX Standard-Geräte angeben.  

 Einzelheiten finden Sie unter [Erstellen von Konfigurationselementen für Android- und Samsung KNOX Standard-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Bedingter Zugriff  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Bedingten Zugriffs für PCs, die von System Center Configuration Manager verwaltet werden  
 Vor diesem Release musste ein PC für die Einrichtung des bedingten Zugriffs entweder bei Intune registriert werden oder der Domäne beigetreten sein. Ab dem Update 1602 wird der bedingte Zugriff für PCs unterstützt, die von System Center Configuration Manager verwaltet werden. Für Ihre PCs, die von System Center Configuration Manager verwaltet werden, können Sie den Zugriff auf Exchange Online und SharePoint Online auf ausschließlich Geräte einschränken, die die von Ihnen festgelegten Konformitätsrichtlinien einhalten.  

 Weitere Informationen finden Sie unter [Manage access to O365 services for PCs managed by System Center Configuration Manager (Verwalten des Zugriffs auf Office 365-Dienste für PCs, die von System Center Configuration Manager verwalteten)](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

### <a name="restricting-access-based-on-the-health-of-devices"></a>Einschränken des auf der Integrität von Geräten basierenden Zugriffs  
 Sie können jetzt den Zugriff auf E-Mail- und Office 365-Dienste basierend auf der Integrität von Geräten gemäß der Meldung des Health Attestation-Diensts einschränken. Darüber hinaus werden Geräte, die von Intune verwaltet werden, in die Geräte-Integritätsberichte einbezogen.  

 Die Configuration Manager-Konsole verfügt über eine neue Konformitätsregel, mit der Sie angeben können, ob den Geräten basierend auf ihrem Integritätsstatus der Zugriff erlaubt oder nicht erlaubt werden soll. Details zum Health Attestation-Dienst und zur Meldung der Integrität von Geräten in Intune finden Sie unter [Integritätsnachweis für System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Neue Regeln für Kompatibilitätsrichtlinien  
 Neue Regeln für Konformitätsrichtlinien, wie z.B. automatische Updates und ein erforderliches Kennwort zum Entsperren von Geräten, wurden hinzugefügt, um höhere Sicherheitsanforderungen zu unterstützen.

 Weitere Informationen finden Sie unter [Device compliance policies in System Center Configuration Manager (Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager)](../../../protect/deploy-use/device-compliance-policies.md).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Sicherstellen, dass registrierte und konforme Geräte immer Zugriff auf lokales Exchange haben  
 Wenn Sie die folgende Option aktivieren, dürfen Geräte, die bei Intune registriert sind und mit den Konformitätsrichtlinien übereinstimmen, auf lokales Exchange zugreifen: **Außerkraftsetzung der Standardregel – Über Intune registrierten und konformen Geräten immer Zugriff auf Exchange gewähren**. Diese Regel ist verfügbar auf der Seite **Allgemein** des **Assistenten zur Konfiguration der Richtlinie zum bedingten Zugriff** für lokales Exchange.

 Diese Regel setzt die Standardregel außer Kraft, was bedeutet, dass registrierte und konforme Geräte weiterhin auf lokales Exchange zugreifen können, selbst wenn Sie die Standardregel so festlegen, dass der Zugriff isoliert bzw. blockiert wird. Wählen Sie diese Einstellung, wenn registrierte und kompatible Geräte stets über lokales Exchange Zugriff auf E-Mail haben sollen.   

 Eine detaillierte exemplarische Vorgehensweise finden Sie unter [Manage email access in System Center Configuration Manager (Verwalten des E-Mail-Zugriffs in System Center Configuration Manager)](../../../protect/deploy-use/manage-email-access.md).  

## <a name="client-management"></a>Clientverwaltung  

### <a name="client-online-status"></a>Onlinestatus von Clients  
 Ein neuer Status für Clients ist für die Überwachung verfügbar, ob ein Computer online ist oder nicht. Ein Computer gilt als online, wenn er mit dem ihm zugewiesenen Verwaltungspunkt verbunden ist. Um anzugeben, dass der Computer online ist, sendet der Client Ping-ähnliche Nachrichten an den Verwaltungspunkt. Wenn der Verwaltungspunkt nach fünf Minuten keine Nachricht erhält, gilt der Client als offline.  

 Einzelheiten finden Sie unter [How to monitor clients in System Center Configuration Manager (Überwachen von Clients in System Center Configuration Manager)](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Aktualisieren von Computer- und Benutzerrichtlinien eines PCs über Software Center  
 Eine neue Option, **Richtlinie synchronisieren**, wurde im Softwarecenter zur Seite **Optionen** > **Computerwartung** hinzugefügt. Mit dieser Option können die Configuration Manager-Computer- und -Benutzerrichtlinie auf dem PC aktualisiert werden.  

### <a name="software-center-branding-changes"></a>Änderungen am Branding von Software Center  
 Sie können die im Softwarecenter angezeigte Farbe, den Organisationsnamen und das Symbol ändern. Diese Einstellungen werden entsprechend den folgenden Regeln angewendet:  

- Wenn die Standortserverrolle „Anwendungskatalog-Websitepunkt“ nicht installiert ist, zeigt das Softwarecenter den Organisationsnamen an, der in der **Computer-Agent**-Clienteinstellung **Im Softwarecenter angezeigter Organisationsname** angegeben ist.  

- Wenn die Standortserverrolle „Anwendungskatalog-Websitepunkt“ installiert ist, zeigt das Softwarecenter den Organisationsnamen und die Farbe an, der bzw. die in den Eigenschaften der Standortserverrolle „Anwendungskatalog-Websitepunkt“ angegeben sind.  

- Wenn ein Microsoft Intune-Abonnement konfiguriert und mit der Configuration Manager-Umgebung verbunden ist, zeigt das Softwarecenter den Organisationsnamen, die Farbe und das Unternehmenslogo entsprechend den Angaben in den Eigenschaften des Intune-Abonnements an.  

### <a name="health-attestation"></a>Integritätsnachweis  
 Administratoren können den Status des Windows 10-Nachweises zur Geräteintegrität in der Configuration Manager-Konsole anzeigen. Dies steht für Configuration Manager und Configuration Manager mit Microsoft Intune zur Verfügung. Mit dem Nachweis der Geräteintegrität kann der Administrator sicherstellen, dass Clientcomputer über die folgenden aktivierten vertrauenswürdigen BIOS-, TPM- und Startsoftwarekonfigurationen verfügen:  

-   Antischadsoftware-Frühstart  

-   BitLocker  

-   Sicherer Start  

-   Codeintegrität  

Einzelheiten finden Sie unter [Health attestation for System Center Configuration Manager (Integritätsnachweis für System Center Configuration Manager)](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Verbesserungen an den Antischadsoftware-Einstellungen für Endpoint Protection  
 In Version 1602 wurden die folgenden neuen Einstellungen zur Endpoint Protection-Richtlinie für Antischadsoftware für Windows Defender hinzugefügt:  

-   Echtzeitschutz: Potenziell unerwünschte Programme beim Herunterladen und vor der Installation blockieren.  

-   Überprüfungseinstellungen: Bei Ausführung einer vollständigen Überprüfung zugeordnete Netzlaufwerke überprüfen.  

-   Einstellungen für automatische Übermittlung von Beispieldateien:  

     Das Modul für Antischadsoftware kann das Senden von Dateibeispielen an Microsoft anfordern, damit diese eingehender analysiert werden. Standardmäßig erfolgt immer eine Aufforderung, bevor diese Beispiele gesendet werden. Administratoren können jetzt die folgenden Einstellungen verwalten, um dieses Verhalten zu konfigurieren:  

    -   Erweitert: Automatische Beispieldateiübermittlung aktivieren, um Microsoft bei der Erkennung von schädlichen Elementen zu unterstützen.  

    -   Erweitert: Benutzern das Ändern der Einstellungen für die automatische Beispieldateiübermittlung erlauben.  

    Darüber hinaus lässt die vorhandene Einstellung **Dateien und Ordner ausschließen** im Abschnitt „Ausschlusseinstellungen“ der Endpoint Protection-Richtlinie für Antischadsoftware nun den Ausschluss von Geräten zu.  

Einzelheiten finden Sie unter [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager (Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in System Center Configuration Manager)](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte  

### <a name="ios-activation-lock"></a>iOS-Aktivierungssperre  
 Configuration Manager kann Sie beim Verwalten der iOS-Aktivierungssperre unterstützen, einem Feature der App „Mein iPhone suchen“ für iOS 7.1 und höher. Die Aktivierungssperre wird automatisch aktiviert, wenn die iPhone-App „Mein iPhone suchen“ auf einem Gerät verwendet wird. Nach der Aktivierung müssen die Apple-ID und das Kennwort des Benutzers eingegeben werden, bevor folgende Vorgänge möglich sind:  

-   Deaktivieren Sie „Mein iPhone suchen“.  

-   Löschen Sie das Gerät.  

-   Reaktivieren Sie das Gerät.  

Configuration Manager kann den Status der Aktivierungssperre von überwachten und nicht überwachten Geräten anfordern, die iOS 7.1 und höher ausführen. Für überwachte Geräte kann Configuration Manager den Umgehungscode der Aktivierungssperre abrufen und ihn direkt auf das Gerät anwenden.  

 Einzelheiten finden Sie unter [Help protect iOS devices with Activation Lock bypass in System Center Configuration Manager (Unterstützen des Schutzes von iOS-Geräten durch Umgehung der Aktivierungssperre für System Center Configuration Manager)](/sccm/mdm/deploy-use/manage-ios-activation-lock).  

### <a name="monitor-terms-and-conditions-deployments"></a>Überwachen von Bereitstellungen von Geschäftsbedingungen  
 Sie können Bereitstellungen von Geschäftsbedingungen in der Configuration Manager-Konsole überwachen.  

 Wählen Sie die Bereitstellung der Geschäftsbedingungen in der Liste der Bereitstellungen aus. Der Zusammenfassungsbereich enthält die folgenden Statistiken:  

-   **Konform**: Benutzer haben die neueste Version der Geschäftsbedingungen akzeptiert.  

-   **Fehler**  

-   **Nicht konform**: Benutzer haben eine Version der Geschäftsbedingungen, aber nicht die neueste akzeptiert.  

-   **Unbekannt**: Benutzer haben die Geschäftsbedingungen nie akzeptiert, einschließlich derjenigen ohne registriertes Gerät.  
