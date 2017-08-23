---
title: 'Archiv: Neuheiten bei hybrider MDM | Microsoft-Dokumentation'
description: "Archiv der früheren Features der Verwaltung mobiler Geräte, die für Hybridbereitstellungen mit System Center Configuration Manager und Intune verfügbar sind"
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 0abd1cdcf44e778c91bacb8011efd711818ce2e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Frühere Hybridfeatures mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Artikel bietet Details zu früheren Features für die Verwaltung mobiler Geräte (MDM), die für Hybridbereitstellungen mit System Center Configuration Manager und Intune verfügbar sind.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Kompatibilität mit Configuration Manager-Versionen  

 Jeder Abschnitt dieses Artikels listet Hybridfeatures in drei verschiedenen Kategorien auf. Verwenden Sie die folgenden Anleitungen, um die Kompatibilität der Features in jeder Kategorie mit verschiedenen Versionen von Configuration Manager zu bestimmen:  

|Featurekategorien|
|-|  
|**Neuheiten in Microsoft Intune** – Im Allgemeinen sollten alle in dieser Kategorie aufgelisteten Features mit allen Configuration Manager-Releases, einschließlich Configuration Manager-Releases von System Center 2012 R2, zusammenarbeiten, da für diese Features nur der Intune-Dienst erforderlich ist, aber keine zusätzliche Funktionalität in Configuration Manager.<br /><br /> **Neuheiten in Configuration Manager Technical Preview** – Alle in dieser Kategorie aufgelisteten Features arbeiten nur mit dem angegebenen Technical Preview-Release zusammen. Um diese Features zu testen, müssen Sie die in der Featurebeschreibung angegebene Technical Preview-Version installieren. Weitere Informationen finden Sie unter [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Neuheiten in Configuration Manager (Current Branch)** – Alle in dieser Kategorie aufgelisteten Features arbeiten nur mit der angegebenen Version von Configuration Manager (Current Branch) zusammen, z.B. Version 1511 oder 1602. Wenn Sie eine ältere Version von Configuration Manager für die Hybridbereitstellung verwenden, müssen Sie ein Upgrade auf die in der Featurebeschreibung angegebene Configuration Manager-Version (Current Branch) ausführen. Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="december-2016"></a>Dezember 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Multi-Factor Authentication (MFA) für die Registrierung in das Azure-Portal verschoben**

  Bisher haben Sie MFA für Intune-Registrierungen entweder in der Intune-Konsole oder der Configuration Manager-Konsole festgelegt. Mit diesem aktualisierten Feature melden Sie sich nun beim [Microsoft Azure-Portal] (https://manage.windowsazure.com) mit Ihren Intune-Anmeldeinformationen an und konfigurieren die MFA-Einstellungen über Azure AD. Weitere Informationen finden Sie unter [Multi-factor authentication for Microsoft Intune] (https://aka.ms/mfa_ad) (Mehrstufige Authentifizierung für Microsoft Intune).

- **Unternehmensportal-App für Android jetzt in China verfügbar**

  Die Unternehmensportal-App für Android ist jetzt in China verfügbar. Da der Google Play Store in China nicht zur Verfügung steht, müssen Apps für Android-Geräte von chinesischen App-Marktplätzen abgerufen werden. Die Unternehmensportal-App für Android steht in den folgenden Stores zum Download zur Verfügung:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  In der Unternehmensportal-App für Android erfolgt die Kommunikation mit dem Microsoft Intune-Dienst über Google Play-Dienste. Da Google Play-Dienste in China noch nicht verfügbar sind, kann die Ausführung der folgenden Aufgaben bis zu 8 Stunden dauern.

  | Configuration Manager-Administratorkonsole | Intune-Unternehmensportal-App für Android | Intune-Unternehmensportalwebsite |
  |----|----|----|      
  | Abkoppeln/Zurücksetzen (Entfernen aller Daten)   | Entfernen eines Remotegeräts | Entfernen eines Geräts (lokal und remote) |
  | Abkoppeln/Zurücksetzen (Entfernen von Unternehmensdaten)   | Zurücksetzen eines Geräts | Zurücksetzen eines Geräts|
  | Neue oder aktualisierte App-Bereitstellungen | Installieren verfügbarer branchenspezifischer Apps | Zurücksetzen der Gerätekennung|
  | Remotesperre | | |
  | Zurücksetzen der Kennung | | |        


## <a name="november-2016"></a>November 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

- **Neues Microsoft Intune-Unternehmensportal für Windows 10-Geräte verfügbar**

  Microsoft hat eine neue [Unternehmensportal-App für Windows 10-Geräte](https://www.microsoft.com/store/apps/9wzdncrfj3pz) veröffentlicht. Diese App, die das neue universelle Windows 10-Format nutzt, bietet neben allen bereits in früheren Unternehmensportal-Apps bereitgestellten Funktionen eine aktualisierte Benutzeroberfläche, die auf allen Windows 10-Geräten (PCs und mobile Geräte) identisch ist.

  Die neue App nutzt Features der Plattform, z.B. einmaliges Anmelden (SSO) und die zertifikatbasierte Authentifizierung, auf Windows 10-Geräten. Die App ist als Upgrade für die vorhandenen Installationen des Unternehmensportals für Windows 8.1 und Windows Phone 8.1 im Windows Store verfügbar. Weitere Informationen finden Sie im [Blog des Intune-Supportteams](http://aka.ms/intunecp_universalapp).

  In der neuen Unternehmensportal-App werden auch alle Windows Store für Unternehmen-Anwendungen angezeigt, die in der Configuration Manager-Konsole als **Verfügbar** markiert sind.


### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Die folgenden Features, die zuvor in Configuration Manager Technical Preview-Releases verfügbar waren, stehen nun in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) Version 1610 zur Verfügung.

* [Zusätzliche Einstellungen und benutzerfreundlichere Konfigurationselemente](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Zusätzliche Einstellungen für DEP-Profile](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Kostenpflichtige Apps im Windows Store für Unternehmen](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Native connection types for Windows 10 VPN profiles (Native Verbindungstypen für Windows 10-VPN-Profile)](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Intune-Kompatibilitätsdiagramme](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Anforderung zur Richtliniensynchronisierung über die Konsole](/sccm/mdm/deploy-use/sync-intune-device)
* [Windows Defender-Konfigurationseinstellungen](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Die folgenden zusätzlichen Hybridfeatures sind auch in Version 1610 von Configuration Manager (Current Branch) enthalten:

- **Erhöhte Anzahl registrierter Geräte**

  Sie können jetzt für Benutzer die Registrierung von bis zu 15 Geräten festlegen. Die Beschränkung lag zuvor bei 5 Geräten pro Benutzer.


- **Zusätzliche Sicherheitsunterstützung**

  Zusätzlich zu „Hauptadministrator“ haben nun die folgenden integrierten Sicherheitsrollen vollen Zugriff auf Elemente im Knoten „Alle unternehmenseigenen Geräte“, einschließlich vorab deklarierter Geräte, iOS-Registrierungsprofilen und Windows-Registrierungsprofilen:

    - Asset-Manager
    - Zugriffs-Manager für Unternehmensressourcen

  Der Rolle „Analyst mit Leseberechtigung“ wird weiterhin der schreibgeschützte Zugriff auf diese Bereiche der Configuration Manager-Konsole gewährt.

- **Automatisch ausgelöster VPN-Zugriff über Windows Information Protection-Apps**

  Sie können Windows 10-VPN-Profilen eine primäre Windows Information Protection-Domäne hinzufügen, die bewirkt, dass alle zugeordneten Apps automatisch eine VPN-Verbindung auslösen, wenn sie auf dem Gerät ausgeführt werden. Diese Option ist nur verfügbar, wenn ein nativer Verbindungstyp ausgewählt wird.

- **Bedingter Zugriff für Windows 10-VPN-Profile**

    Sie können jetzt festlegen, dass in Azure Active Directory registrierte Windows 10-Geräte kompatibel sein müssen, damit sie VPN-Zugriff über in der Configuration Manager-Konsole erstellte Windows 10-VPN-Profile haben. Dies ist möglich über das neue Kontrollkästchen **Bedingten Zugriff für diese VPN-Verbindung aktivieren** auf der Seite „Authentifizierungsmethode“ im Assistenten zum Erstellen von VPN-Profilen und den VPN-Profileigenschaften für Windows 10-VPN-Profile. Diese Option ist nur verfügbar, wenn ein nativer Verbindungstyp ausgewählt wird.

    Wenn Sie den bedingten Zugriff für das Profil aktivieren, können Sie auch ein separates Zertifikat für die Einmalanmeldungsauthentifizierung angeben.

## <a name="october-2016"></a>Oktober 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

Die folgenden im Oktober 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Bedingter Zugriff für die Verwaltung der mobilen Anwendung**

  Sie können den Zugriff auf Exchange Online einschränken, sodass nur Apps, die Verwaltungsrichtlinien für mobile Anwendungen von Intune unterstützen, z.B. Outlook, Zugriff haben. [Die neuen Features](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) passen perfekt zu den Verwaltungsrichtlinien für mobile Apps (Mobile App Management, MAM) von Intune, da Sie den Zugriff auf integrierte Mailclients oder andere Apps, die nicht mit den MAM-Richtlinien von Intune konfiguriert wurden, blockieren können. Dadurch wird sichergestellt, dass Ihre Benutzer auf die Daten Ihrer Organisation mit Apps zugreifen, die mit Intune MAM geschützt werden können. Sie können Ihre ersten Schritte mit den Verwaltungsrichtlinien für mobile Apps von Intune über das Azure-Portal unternehmen. Suchen Sie den neuen Abschnitt „Bedingter Zugriff“ auf dem Blatt „Einstellungen“.

-   **Intune App Wrapping Tool für Android**

  Sie können mithilfe des Intune App Wrapping Tools Ihre Apps so einstellen, dass sie die MAM-Richtlinien von Intune verwenden.

- **Android Samsung KNOX Standard-Kompatibilität mit Intune**

  Bestimmte Modelle des Samsung Galaxy Ace-Telefons können nicht von Intune als Samsung KNOX Standard-Geräte verwaltet werden. Wenn Sie diese Geräte bei Intune registrieren, werden sie stattdessen als Android-Standardgeräte verwaltet.

  Folgende Modellnummern sind betroffen:

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  Sie und Ihre Endbenutzer müssen keine weiteren Maßnahmen ergreifen. Weitere Informationen finden Sie auf der Samsung KNOX-Website.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Neuheiten in Configuration Manager Technical Preview 1610

Die folgenden neuen Hybridfeatures wurden im Oktober 2016 Configuration Manager Technical Preview 1610 eingeführt.

- **Richtliniensynchronisierung über die Verwaltungskonsole anfordern**

  Sie können eine Richtliniensynchronisierung auf einem registrierten mobilen Gerät über die Configuration Manager-Konsole anfordern, anstatt die Synchronisierung in der Unternehmensportal-App auf dem Gerät selbst anzufordern. Diese neue Aktion namens **Send Sync Request** (Synchronisierungsanforderung senden) finden Sie im Menü „Remotegeräteaktionen“, das bei Auswahl eines mobilen Geräts im Knoten „Geräte“ im Menüband angezeigt wird.

- **Windows Defender-Konfigurationseinstellungen**

  Sie können Windows Defender-Clienteinstellungen auf Intune-registrierten Windows 10-Computern mithilfe von Konfigurationselementen in der Configuration Manager-Konsole konfigurieren. Der Assistent für Konfigurationselemente bietet eine neue Einstellungsgruppe namens **Windows Defender**. Beachten Sie, dass dies nur auf Windows 10 Version 1511 und höher unterstützt wird.


### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Im August 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.

## <a name="september-2016"></a>September 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

Die folgenden im September 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Hinzufügen von „Benachrichtigungen“ zum Unternehmensportal für Android**

  Ein neues Symbol „Benachrichtigungen“ wurde dem Unternehmensportal für Android auf der Startseite hinzugefügt. Wenn Sie auf dieses Symbol tippen, gelangen Sie auf die Seite „Benachrichtigungen“, auf der Ihre Benutzer alle Elemente sehen, denen in der Unternehmens-App Beachtung geschenkt werden muss. Dazu gehören die Nichtkompatibilität von Geräten, Registrierungsupdates und die Registrierungsaktivierung. Die iOS-Unternehmensportal-App verfügt bereits über diese benutzerfreundlichen Benachrichtigungen. Aufgrund der neuen Seite „Benachrichtigungen“ wird die Seite „Setup des Unternehmenszugriffs“ nicht jedes Mal angezeigt, wenn Benutzer das Unternehmensportal starten oder fortsetzen. Voraussetzung ist jedoch, dass das Gerät bereits registriert ist. Wenn Sie eigene Endbenutzeranleitungen erstellen, sollten Sie auch Ihre Dokumentation entsprechend aktualisieren. Aktualisierte Screenshots finden Sie [hier](https://aka.ms/androidcpupdate).

- **Änderungen bei der Unterstützung der iOS-Unternehmensportal-App**

  Alle Benutzer der Microsoft Intune-Unternehmensportal-App für iOS müssen jetzt die neueste Version verwenden. Neue Benutzer können nur die neueste Version herunterladen, und aktuelle Benutzer müssen ein entsprechendes Update durchführen. Da die neueste Version iOS 8.0 oder höher erfordert, können Geräte mit älteren iOS-Versionen das Unternehmensportal erst verwenden oder sich registrieren, wenn sie ihr Gerät auf iOS 8.0 oder höher aktualisieren und dann die Unternehmensportal-App auf die neueste Version aktualisieren. Registrierte Geräte, auf den Versionen vor iOS 8.0 ausgeführt werden, werden weiterhin in der Intune-Verwaltungskonsole verwaltet und aufgeführt.

- **Schaltfläche „Feedback“ der Windows Phone 8.1-Unternehmensportal-App hinzugefügt**

  Die Windows Phone 8.1-Unternehmensportal-App ermöglicht Endbenutzern, Feedback über die App mithilfe einer neuen Schaltfläche „Feedback senden“ zu senden. Um auf die Schaltfläche zuzugreifen, tippen Benutzer auf das Drei-Punkte-Menü unten rechts auf dem Bildschirm der Unternehmensportal-App und dann auf **Feedback senden**. Das gesammelte, anonymisierte Feedback hilft Microsoft, die Benutzerfreundlichkeit der Unternehmensportal-App zu verbessern.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Neuheiten in Configuration Manager Technical Preview 1609

Die folgenden neuen Hybridfeatures wurden im Oktober 2016 für Configuration Manager Technical Preview 1609 eingeführt.

- **Zusätzliche Einstellungen und benutzerfreundlichere Konfigurationselement-Einstellungen**

  Neue Einstellungen für Android, iOS und Windows wurden hinzugefügt und nur die Einstellungen, die für die Plattformen gelten, die Sie auf der Seite „Unterstützte Plattformen“ wählen, werden im Assistenten angezeigt. Weitere Informationen finden Sie unter [New compliance settings for configuration items in TP 1609 (Neue Kompatibilitätseinstellungen für Konfigurationselement ein TP 1609)](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Zusätzliche Einstellungen für DEP-Profile**

  TouchID, ApplePay und Zoom wurden als konfigurierbare Einstellungen in DEP-Profilen für iOS-Geräte hinzugefügt.

- **Kostenpflichtige Apps im Windows Store für Unternehmen**

  Sie können jetzt kostenpflichtige und kostenlose Apps zum Windows Store für Unternehmen hinzufügen und den Benutzern in Ihrer Organisation bereitstellen. Weitere Informationen finden Sie unter [Enhancements to Windows Store for Business in TP 1609 (Verbesserungen von Windows Store für Unternehmen in TP 1609)](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Native connection types for Windows 10 VPN profiles (Native Verbindungstypen für Windows 10-VPN-Profile)**

  Sie können jetzt Windows 10-VPN-Profile für MDM mit Microsoft Automatic-, IKEv2- und PPTP-Verbindungstypen in der Configuration Manager-Konsole erstellen, ohne OMA-URI zu verwenden.

- **Intune-Kompatibilitätsdiagramme**

  Sie können einen schnellen Überblick über die allgemeine Gerätekompatibilität und die wichtigsten Gründe für Nichtkompatibilität mithilfe der neuen Diagramme unter dem Arbeitsbereich „Überwachung“ abrufen. Weitere Informationen finden Sie unter [Intune compliance charts in TP 1609 (Intune Compliance-Diagramme in TP 1609)](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Die folgenden neuen Features vom September 2016 sind in Hybridbereitstellungen mit Microsoft Intune und Configuration Manager Version 1606 (Current Branch) verfügbar.

- **iOS 10-Unterstützung**

  Wenn Sie Profile oder Konfigurationselemente für alle iOS-Plattformen vorgesehen haben, werden diese auch auf iOS 10 übertragen. Wir haben auch ein Update für Configuration Manager Release 1606 veröffentlicht, das Ihnen ermöglicht, Profile und Konfigurationselemente für einzelne iOS-Plattformen, einschließlich iOS 10, zu planen. Sie können das Update mit der Configuration Manager-Administratorkonsole über **Verwaltung > Übersicht > Cloud-Dienste > Updates und Wartung** installieren. Weitere Informationen über das Update finden Sie unter [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="august-2016"></a>August 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

Die folgenden im August 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Android 7-Unterstützung in der Unternehmensportal-App**

  Die Intune-Unternehmensportal-App für Android bietet „Tag 0“-Unterstützung für das neue Betriebssystem Android 7.0 für mobile Geräte.

- **Google entfernt Funktion „Kennung remote zurücksetzen“ auf Android 7.0-Geräten**

  Google entfernt die für IT-Administratoren und Endbenutzer verfügbare Funktion, die Kennung von Android 7.0-Geräten remote zurückzusetzen. Bisher konnten IT-Administratoren die Kennung von Benutzern remote zurücksetzen, und die Endbenutzer konnten ihre Kennungen über die Unternehmensportal-Website zurücksetzen.

- **Richtlinien für zulässige und blockierte Apps für Samsung KNOX Standard-Geräte**

  Sie können nun eine benutzerdefinierte Richtlinie für Samsung KNOX Standard-Geräte konfigurieren, mit der Sie eines der folgenden Elemente erstellen können:

  - Eine Liste von Apps, deren Ausführung auf dem Gerät blockiert wurde. Auch wenn sie installiert ist, kann eine in der Liste der blockierten Geräte definierte App nicht auf dem Gerät aktiviert werden.
  - Eine Liste der Apps, die Benutzer des Geräts aus dem Google Play Store installieren dürfen. Keine anderen Apps können aus dem Store installiert werden.

  Diese Einstellungen können nur von Geräten verwendet werden, auf denen Samsung KNOX Standard ausgeführt wird. Einzelheiten finden Sie unter [Verwenden von benutzerdefinierten Richtlinien zum Zulassen und Blockieren von Apps für Samsung KNOX Standard-Geräte](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Feedback-Link vom Unternehmensportal zu Microsoft**

   Die Unternehmensportal-Website ermöglicht Endbenutzern auf einen neuen Link „Feedback“ am unteren Rand der Seite zu tippen, um Feedback zu ihren Erfahrungen mit der Site an Microsoft zu senden. Das gesammelte, anonymisierte Feedback hilft Microsoft, die Benutzerfreundlichkeit der Unternehmensportal-Website zu verbessern.

- **Mindestversion von Managed Browser für iOS auf 8.0 aktualisiert**

  Die Microsoft Intune Managed Browser-App für iOS wurde aktualisiert und unterstützt nun Geräte, auf denen iOS 8.0 oder höher ausgeführt wird. Obwohl IOS 7.1-Geräte weiterhin die vorhandene Managed Browser-App verwenden können, sollten Sie die Benutzer auffordern, auf iOS 8.0 oder höher zu aktualisieren und die neuen Managed Browser-Features im vollen Umfang zu nutzen.

### <a name="new-in-configuration-manager-technical-preview"></a>Neuheiten in Configuration Manager Technical Preview

Im August 2016 wurden keine neuen Hybridfeatures für Configuration Manager Technical Preview eingeführt.

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Im August 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.

## <a name="july-2016"></a>Juli 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune

Die folgenden im Juli 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Xamarin SDK für Intune-Apps ist verfügbar**

  Mit der Xamarin SDK-Komponente für Intune-Apps können Sie die Intune-Features für die Verwaltung mobiler Anwendungen in Ihren mit Xamarin erstellten mobilen iOS- und Android-Apps aktivieren. Sie finden die Komponente im [Xamarin Store](https://components.xamarin.com/view/Microsoft.Intune.MAM) oder auf der [Microsoft Intune-Github-Seite](https://github.com/msintuneappsdk).

- **Verbesserte Endbenutzererfahrung bei der Registrierung von Windows-Geräten**

  Wenn Sie den bedingten Zugriff verwenden, wurden die Registrierungsschritte für Windows 8.1, Windows 10 Desktop und Windows 10 Mobile auf der Unternehmensportal-Website geklärt. Benutzer sehen nun separate Schritte für die **Geräteregistrierung** und **Arbeitsplatzbereichsverknüpfung**, sodass sie den Status ihres Geräts besser verfolgen und den Prozess einfacher abschließen können, wenn ein Fehler bei der Arbeitsplatzverknüpfung auftritt. Separate Schritte sollen auch die Problembehandlung für IT-Administratoren zu vereinfachen. Wenn Endbenutzer versuchten, ein Gerät zu registrieren und alle Registrierungsschritte bis auf WPJ erfolgreich waren, wurde das registrierte Gerät bisher nicht in der Liste der für Benutzer zu identifizierenden Geräte angezeigt, was bei den Benutzern für Verwirrung sorgte.

 - **Vollständiges Zurücksetzen jetzt für Windows 10-Geräte verfügbar**

    Windows 10-PCs und Laptops, die als mobile Geräte registriert werden, können endgültig zurückgesetzt werden. Das Gerät wird dann auf seine Werkseinstellungen zurückgesetzt. Weitere Informationen finden Sie unter [How to protect your devices with remote wipe (Schützen von Geräten mithilfe von Remotezurücksetzung)](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Änderungen an Geräteregistrierungsmanager-Konten in der iOS-Unternehmensportal-App**

  Zum Verbessern von Leistung und Skalierung zeigt Intune nicht mehr alle Geräteregistrierungsmanager-Geräte (Device Enrollment Manager, DEM) im Bereich „Meine Geräte“ in der iOS-Unternehmensportal-App an. Nur das lokale Gerät wird angezeigt, auf dem die App ausgeführt wird, und auch nur dann, wenn es über die Unternehmensportal-App registriert wurde.

  Der DEM-Benutzer kann Aktionen auf dem lokalen Gerät ausführen, aber die Remoteverwaltung der anderen registrierten Geräte kann nur über die Intune-Verwaltungskonsole durchgeführt werden. Darüber hinaus verwirft Intune die Verwendung von DEM-Konten mit dem Apple-Programm zur Geräteregistrierung oder dem Apple Configurator Tool als veraltet. Die beiden Registrierungsmethoden unterstützen bereits die Registrierung ohne Benutzer für freigegebene iOS-Geräte.

  Verwenden Sie DEM-Konten nur, wenn die Registrierung ohne Benutzer für gemeinsam genutzte Geräte nicht verfügbar ist. Weitere Informationen finden Sie unter [Registrieren von firmeneigenen Geräten mit dem Geräteregistrierungs-Manager in Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Änderungen der Android-Unternehmensportal-App**

  Wenn Android-Endbenutzer von einer Fehlermeldung darüber informiert werden, dass ein erforderliches Zertifikat auf ihrem Gerät fehlt, können Sie auf die Schaltfläche „Problembehebung“ tippen und erhalten dann Anleitungen für die Installation des fehlenden Zertifikats. Wenn die Benutzer den Anleitungen folgen, aber eine weitere Fehlermeldung zu einem fehlenden Zertifikat angezeigt wird, sollten Sie sich an ihren IT-Administrator wenden und folgenden Link bereitstellen, der die Schritte enthält, mit denen IT-Administratoren das Zertifikatsproblem beheben können.

- **Installationen von quergeladenen Apps auf registrierte Android-Geräte beschränken**

  Android-Geräte können Apps nur noch dann über die Unternehmensportal-Website installieren, wenn die Geräte mithilfe der Intune-Unternehmensportal-App für Android in Intune registriert wurden.


### <a name="new-in-configuration-manager-technical-preview"></a>Neuheiten in Configuration Manager Technical Preview

Im Juli 2016 wurden keine neuen Hybridfeatures für Configuration Manager Technical Preview eingeführt.

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)

Die folgenden Features, die zuvor in Configuration Manager Technical Preview-Releases verfügbar waren, stehen nun in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) Release 1606 zur Verfügung.

* Suchen, Verwalten und Verteilen von Windows Store für Unternehmen-Apps für Windows 10-Geräte über die Configuration Manager-Konsole ([1604](#new-in-1604-technical-preview))
*   SmartLock-Einstellung für Android-Geräte ([1604](#new-in-1604-technical-preview))
*   Per App ausgelöstes VPN für Windows 10-Geräte ([1605](#new-in-1605-technical-preview))
*   Benutzerfreundlichere Remotegeräteaktionen ([1605](#new-in-1605-technical-preview))
*   Windows Store für Unternehmen-Apps ([1605](#new-in-1605-technical-preview))
*   Allgemeine Verbesserungen für per Volumenlizenz erworbene Apps ([1605](#new-in-1605-technical-preview))
*   Windows Information Protection (WIP) ([1605](#new-in-1605-technical-preview))
*   Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer ([1605](#new-in-1605-technical-preview))
*   Automatisches Kategorisieren von Geräten in Sammlungen ([1606](#new-in-1606-technical-preview))

Informationen zu den neuen Funktionen finden Sie in der Dokumentation für das angegebene Technical Preview-Release.

## <a name="june-2016"></a>Juni 2016

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune
Die folgenden im Juni 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **Intune-Dienstintegrität** Dienstintegritätsinformationen für Intune wurden an einen zentralen Speicherort mit anderen Microsoft-Diensten verschoben. Diese Informationen finden Sie jetzt im Office 365-Verwaltungsportal unter „Dienstintegrität“. Weitere Informationen finden Sie in diesem [Blogbeitrag](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Verbesserte Windows 10 Enterprise-Datenrichtlinienkonfiguration**

  Intune bietet nun verbesserte Benutzerfreundlichkeit beim Konfigurieren von Windows 10 Information Protection. Die Verbesserungen umfassen bessere Methoden zum Erstellen von App-Regeln, Angeben der Definition der Netzwerkgrenze und andere Windows Information Protection-Einstellungen. Weitere Informationen finden Sie unter [Create a Windows Information Protection (WIP) policy using Microsoft Intune (Erstellen einer Windows Information Protection-Richtlinie (WIP) mit Microsoft Intune)](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Cisco ISE-Netzwerk-Zugriffssteuerungsrichtlinie für Intune**

  Kunden, die Cisco Identity Service Engine (ISE) 2.1 und außerdem Microsoft Intune verwenden, können eine Netzwerkzugriffssteuerungsrichtlinie in ISE festlegen. Bei Verwendung dieser Richtlinie müssen Geräte, die über WLAN oder VPN eine Verbindung mit dem Netzwerk herstellen müssen, die folgenden Bedingungen erfüllen, bevor sie Zugriff erhalten:

  - Verwaltung durch Intune
  - Kompatibilität mit allen bereitgestellten Intune-Konformitätsrichtlinien

  Endbenutzer nicht konformer Geräte werden aufgefordert, sich zu registrieren und etwaige Kompatibilitätsprobleme zu beheben, um Zugriff zu erhalten.

- **Bedingter Zugriff für Browser**

  Sie können eine Richtlinie für bedingten Zugriff für Exchange Online und SharePoint Online festlegen, sodass nur von unterstützten Webbrowsern auf verwalteten und kompatiblen IOS- und Android-Geräten aus auf sie zugegriffen werden kann. Endbenutzer, die versuchen, sich bei Outlook Web Access- (OWA-) und SharePoint-Standorten mit IOS- und Android-Geräten anzumelden, werden aufgefordert, ihr Gerät bei Intune zu registrieren und alle Nichtkompatibilitätsprobleme zu beheben, bevor eine vollständige Anmeldung möglich ist. Weitere Informationen finden Sie unter

  * [Restrict email access to Exchange Online and new Exchange Online Dedicated with Intune (Beschränken des E-Mail-Zugriffs auf Exchange Online und das neue Exchange Online Dedicated mit Intune)](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restrict access to SharePoint Online with Microsoft Intune (Beschränken des Zugriffs auf SharePoint Online mit Microsoft Intune)](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online unterstützt den bedingten Zugriff**

  Sie können eine Richtlinie für bedingten Zugriff für Dynamics CRM Online festlegen, damit nur verwaltete und kompatible IOS- und Android-Geräte darauf zugreifen können. Endbenutzer, die sich bei der Dynamics CRM Mobile-App für iOS und Android anmelden möchten, werden aufgefordert, sich bei Intune zu registrieren und alle Nichtkompatibilitätsprobleme zu beheben, bevor die Anmeldung abgeschlossen werden kann. Weitere Informationen finden Sie unter [Restrict access to Dynamics CRM Online with Microsoft Intune (Beschränken des Zugriffs auf Dynamics CRM Online mit Microsoft Intune)](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Updates der Android-Unternehmensportal-App**

  Intune verfügt nun über die folgenden neuen Richtlinien, die sich auf Android Unternehmensportal-Benutzer auswirken:   

  Richtlinie  |Auswirkungen für Benutzer  
  ---------|---------
  Geräte müssen die Installation von Apps aus unbekannten Quellen verhindern (Android 4.0+)     |  Endbenutzer mit Geräten mit Android 4.0 oder höher sehen die Meldung „Die Installation von unbekannten Quellen muss deaktiviert sein“. Benutzer müssen auf ihren Geräten zu **Einstellungen > Sicherheit** wechseln und **Unbekannte Quellen** deaktivieren. Über einen Link in der Konformitätsmeldung erhalten Benutzer weitere Informationen über die Meldung und den Grund dafür, dass sie die Einstellung deaktivieren müssen.
  Geräte müssen die Installation von Apps aus unbekannten Quellen verhindern (Android 4.0+)  |    Endbenutzer mit Android 4.0 oder höher erhalten die Meldung „Gerät auf Sicherheitsbedrohungen überprüfen“. Benutzer müssen auf ihren Geräten zu **Einstellungen > Google > Sicherheit** wechseln und **Gerät auf Sicherheitsbedrohungen überprüfen** aktivieren. Über einen Link in der Konformitätsmeldung erhalten Benutzer weitere Informationen über die Nachricht und den Grund dafür, dass sie die Einstellung aktivieren müssen.     
  Das USB-Debuggen muss deaktiviert sein (Android 4.2+)  | Endbenutzer mit Geräten mit Android 4.2 oder höher sehen die Meldung „Das USB-Debuggen muss deaktiviert sein“. Benutzer müssen auf ihren Geräten zu **Einstellungen > Entwickleroptionen** wechseln und **USB-Debuggen** deaktivieren. Über einen Link in der Konformitätsmeldung erhalten Benutzer weitere Informationen über die Meldung und den Grund dafür, dass sie die Einstellung deaktivieren müssen.
  Niedrigste zulässige Android-Sicherheitspatchebene (Android 6.0+)  | Endbenutzer mit Android Version 6.0 oder höher erhalten die Meldung „Dieses Gerät weist nicht die mindestens erforderliche Ebene für Android-Sicherheitspatches auf“. Benutzer müssen die erforderlichen Sicherheitspatches installieren. Über einen Link in der Konformitätsmeldung erhalten Benutzer Informationen darüber, wie sie den erforderlichen Sicherheitspatch installieren und prüfen können, welchen Sicherheitspatch sie derzeit installiert haben.

- **Updates der iOS-Unternehmensportal-App**

  * Wenn Endbenutzer Branchen-Apps installieren, profitieren sie nun von einer verbesserten, benutzerfreundlichen App-Installation. Wenn die App-Installation lange dauert, können die Benutzer ihr Gerät manuell synchronisieren, um die Fortsetzung des Synchronisierungsprozesses zu erzwingen. Die Endbenutzeranweisungen finden Sie unter „Sync your iOS device manually (Manuelles Synchronisieren des iOS-Geräts)“.
  * Die Microsoft Windows Intune-Unternehmensportal-App für iOS wurde aktualisiert und unterstützt nun iOS-Version 8.0 und höher. Dieses Update bedeutet, dass Endbenutzer die Unternehmensportal-App nur installieren und neue Geräte in Intune nur registrieren können, wenn auf dem Gerät iOS Version 8.0 oder höher ausgeführt wird. Benutzer, die bereits Geräte registriert haben, auf denen eine nicht unterstützte Version von iOS ausgeführt wird, können weiterhin die auf ihrem Gerät vorhandene Unternehmensportal-App verwenden.


### <a name="new-in-1606-technical-preview"></a>Neuheiten in 1606 Technical Preview
Die folgenden neuen Features vom Juni 2016 sind in Hybridbereitstellungen mit Intune und Configuration Manager Technical Preview 1606 verfügbar.

- **Automatisches Kategorisieren von Geräten in Sammlungen**

  Sie können Gerätekategorien erstellen, mit denen Geräte automatisch in Gerätesammlungen platziert werden, wenn Sie Configuration Manager mit Intune verwenden. Benutzer müssen eine Gerätekategorie auswählen, wenn sie ein Gerät in Intune registrieren. Sie können außerdem die Kategorie eines Geräts in der Configuration Manager-Konsole ändern. Weitere Informationen finden Sie unter [Automatisches Kategorisieren von Geräten in Sammlungen](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) in [Funktionen in Technical Preview 1606 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > Diese Funktion wird vom Microsoft Intune-Release vom Juni 2016 unterstützt. Stellen Sie sicher, dass Sie auf dieses Release aktualisiert haben, bevor Sie die Verfahren ausprobieren.

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)
Im Juni 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.

##  <a name="may-2016"></a>Mai 2016  

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune  
 Die folgenden im Mai 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.

- **MAM SDK: Unterstützung der PIN-Längenkonfiguration**

  Sie können jetzt die Länge der PIN für MAM-Apps ähnlich wie bei einer Geräte-ID angeben. Hierfür müssen Endbenutzer die neuen Einschränkungen einhalten, die Sie festlegen. Der PIN-Bildschirm wird für die längere Eingabe geringfügig geändert. Weitere Informationen finden Sie unter [MAM policy settings for Android (MAM-Richtlinieneinstellungen für Android)](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) und [MAM policy settings for iOS (MAM-Richtlinieneinstellungen für iOS)](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype for Business für iOS und Android**

  Sie können jetzt [MAM ohne Registrierungsrichtlinien](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune) auf Skype for Business anwenden. Sobald sich die Benutzer angemeldet haben, werden die MAM-Richtlinien angewendet.  

- **Neue Apps für die Verwaltung mit MAM-Richtlinien verfügbar**

  Die Microsoft Word-, Excel- und PowerPoint-Apps für Android können mit MAM-Richtlinien auf Geräten verknüpft werden, die nicht bei Intune registriert sind. Eine vollständige Liste der unterstützten Apps finden Sie im Mobilanwendungskatalog von Microsoft Intune auf der Seite [Microsoft Intune-Anwendungspartner](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx).  

- **Android-Unternehmensportal-App: Popupbenachrichtigungen für Endbenutzer**

  Popupbenachrichtigungen von der Android-Unternehmensportal-App werden angezeigt, wenn Endbenutzer ihre Geräte über das Unternehmensportal registrieren oder entfernen.  

- **Unternehmensportal-Website: Geräte-ID-Banner bietet Endbenutzern weitere Informationen**

  Endbenutzer können das Gerät, das sie ausgewählt haben, bei Verwendung der Unternehmensportal-Website jetzt leichter finden. Wenn das falsche Gerät ausgewählt ist, können sie das korrekte Gerät auswählen, indem sie auf den Link **Hier tippen** im Banner der Startseite tippen.  


### <a name="new-in-1605-technical-preview"></a>Neuheiten in 1605 Technical Preview  
 Die folgenden neuen Features vom Mai 2016 sind in Hybridbereitstellungen mit Intune und Configuration Manager Technical Preview 1605 verfügbar. Diese Features setzen voraus, dass Sie die Configuration Manager-Konsole zum Konfigurieren und Verwalten verwenden.  

- **Per App ausgelöstes VPN für Windows 10-Geräte**

  Für Windows 10-Geräte, die mithilfe von Configuration Manager mit Intune verwaltet werden, können Sie eine Liste von Apps hinzufügen, die automatisch eine VPN-Verbindung öffnen, die Sie über die Configuration Manager-Verwaltungskonsole konfiguriert haben. Weitere Informationen finden Sie unter [Per App ausgelöstes VPN für Windows 10-Geräte](/sccm/core/get-started/capabilities-in-technical-preview-1605) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Benutzerfreundlichere Remotegeräteaktionen**

  Die Ausführung von Remotegeräteaktionen über die Configuration Manager-Konsole wurde benutzerfreundlicher gestaltet und verbessert.

  Häufig verwendete Aktionen, wie z.B. **Abkoppeln/Zurücksetzen**, **Kennung zurücksetzen**, **Remotesperre** und **Aktivierungssperre umgehen**, befinden sich nun im Menü **Remotegeräteaktionen**, auf das Sie über den Arbeitsbereich **Bestand und Kompatibilität** zugreifen.

  Weitere Informationen finden Sie unter [Benutzerfreundlichere Remotegeräteaktionen](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Store für Unternehmen-Apps**

  Im [Windows Store für Unternehmen](https://www.microsoft.com/en-us/business-store) können Sie Apps für Ihre Organisation finden und entweder einzeln oder per Volumenlizenz erwerben. Indem Sie den Store mit Configuration Manager verbinden, können Sie per Volumenlizenz erworbene Apps aus der Configuration Manager-Konsole verwalten. Weitere Informationen finden Sie unter [Windows Store für Unternehmen-Apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Allgemeine Verbesserungen für per Volumenlizenz erworbene Apps**

  Per Volumenlizenz erworbene Apps aus dem Windows Store für Unternehmen und dem iOS App-Store wurden in der gleichen Ansicht, **Lizenzinformationen für Store-Apps**, konsolidiert. Außerdem wurde die Art und Weise, wie Sie per Volumenlizenz erworbene Apps für iOS erstellen, verbessert. Weitere Informationen finden Sie unter [Allgemeine Verbesserungen für per Volumenlizenz erworbene Apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer**

  Sie können nun firmeneigene Geräte identifizieren, indem Sie deren IMEI-Nummern (International Station Mobile Equipment Identity) importieren. Sie können eine CSV-Datei (comma-separated values, durch Trennzeichen getrennte Datei) hochladen, die die IMEI-Nummern der Geräte enthält, oder Geräteinformationen manuell eingeben.  Sie können auch die Seriennummern für iOS-Geräte importieren.  Weitere Informationen finden Sie unter [Vorabdeklarieren von firmeneigenen Geräten mit IMEI- oder iOS-Seriennummer](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) in [Funktionen in Technical Preview 1605 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Information Protection (WIP)**

  Sie können Konfigurationselemente erstellen, mit denen Sie Ihre Windows Information Protection-Richtlinien (WIP) bereitstellen können und z.B. Ihre geschützten Apps und Ihre WIP-Schutzebene wählen und Unternehmensdaten im Netzwerk suchen können. Weitere Informationen zu WIP finden Sie in den folgenden Themen:  

  -   [Schützen von Unternehmensdaten mit Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Create and deploy a Windows Information Protection (WIP) policy using System Center Configuration Manager (Erstellen und Bereitstellen einer Windows Information Protection-Richtlinie (WIP) mithilfe von System Center Configuration Manager)](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)  
 Im Mai 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.  

##  <a name="april-2016"></a>April 2016  

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune  
 Die folgenden im April 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.  

- **MAM-Benutzerkompatibilität**

  Sie können nun den Status der Anwendungsverwaltungsrichtlinien für alle Benutzer in Ihrem Azure Active Directory-Mandanten (AAD) anzeigen.  Weitere Informationen finden Sie unter [Überwachen der Verwaltungsrichtlinien für mobile Apps mit Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in der Intune-Bibliothek.  

- **MAM-Steuerelemente, um die Synchronisierung von Kontakten zu verhindern (Android)**

  Eine neue Einstellung ist verfügbar, mit der Sie verhindern können, dass eine Anwendung Kontakte mit dem nativen Adressbuch auf Android-Geräten synchronisiert. Diese neue Einstellung wird anfänglich von der Outlook-Anwendung auf Android-Geräten unterstützt. Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Richtlinien zur Verwaltung mobiler Apps mit Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in der Intune-Bibliothek.  

- **Verbesserungen der Unternehmensportal-Website**

  Wenn Windows 10 Mobile- und Windows Phone 8.1-Benutzer Branchen-Apps installieren, sehen sie nun die folgenden neuen Status, die ihnen weitere Details über den Status ihrer Installation bieten:  

  -   **Warten auf Gerätesynchronisierung** – Der Benutzer hat auf „Installieren“ getippt, und das Gerät versucht nun, eine Synchronisierung mit der Intune-Infrastruktur auszuführen. Die Synchronisierung ist erforderlich, bevor die Installation abgeschlossen werden kann. Die Meldung „Warten auf Gerätesynchronisierung“ ist zudem ein Link, auf den der Benutzer tippen kann, um Anweisungen zur manuellen Synchronisierung mit Intune anzuzeigen, falls der Synchronisierungsprozess lange dauert oder angehalten wird.  

  -   **Wird heruntergeladen** – Die Downloadanforderung wird verarbeitet, und das Gerät lädt die App herunter und installiert sie.  

- **Verbesserungen der Android-Unternehmensportal-App**

  Benutzer, die ihre Geräte nicht in Intune registriert und nicht das richtige Zertifikat installiert haben, sind nicht in der Lage, sich bei der Android-Unternehmensportal-App anzumelden, und sehen die Meldung „Sie können sich nicht anmelden, da dem Gerät ein erforderliches Zertifikat fehlt“. Die Meldung enthält einen Link „Problembehebung“, auf den Benutzer tippen können, um Anweisungen für die Installation des Zertifikats anzuzeigen. Die Schritte, die die Endbenutzer zur Behebung dieses Problems durchführen, finden Sie unter [Your device is missing a required certificate (Dem Gerät fehlt ein erforderliches Zertifikat)](/intune/enduser/using-your-android-device-with-intune) in der Intune-Bibliothek.  

- **Verbesserungen der iOS-Unternehmensportal-App**

  Unterstützung wurde für die Aktion „Zum Aktualisieren ziehen“ hinzugefügt, die den Inhalt auf der Startseite aktualisieren soll. Dazu gehören aufgeführte Apps, aufgeführte Geräte und IT-Kontaktinformationen. Die Aktion „Zum Aktualisieren ziehen“ prüft Kompatibilitäts- oder Richtlinieninformationen nicht. Sie können diese Informationen prüfen, indem Sie die Kachel für das aktuelle Gerät auswählen und auf die Schaltfläche **Synchronisierung** tippen.  

- **Verbesserungen für die Windows 10 Mobile- und Windows Phone 8.1-Unternehmensportal-App**

  Wenn Endbenutzer Branchen-Apps installieren, profitieren sie nun von einer verbesserten, benutzerfreundlichen App-Installation. Wenn die App-Installation lange dauert, können die Benutzer ihr Gerät manuell synchronisieren, um die Fortsetzung des Synchronisierungsprozesses zu erzwingen. Die Endbenutzeranweisungen finden Sie unter [Sync your device manually to speed up app installations (Manuelles Synchronisieren des Geräts zum Beschleunigen von App-Installationen)](/intune/enduser/using-your-windows-device-with-intune) in der Intune-Bibliothek.  

###  <a name="new-in-1604-technical-preview"></a>Neuheiten in 1604 Technical Preview
 Die folgenden neuen Features vom April 2016 sind in Hybridbereitstellungen mit Intune und Configuration Manager Technical Preview 1604 verfügbar. Diese Features setzen voraus, dass Sie die Configuration Manager-Konsole zum Konfigurieren und Verwalten verwenden.  

- **Suchen, Verwalten und Verteilen von Windows Store für Unternehmen-Apps für Windows 10-Geräte über die Configuration Manager-Konsole**


  Unterstützung für Windows Store für Unternehmen ist in Configuration Manager Technical Preview 1604 verfügbar, damit Sie Apps für die von Ihnen verwalteten Windows 10-Geräte suchen, verwalten und verteilen können. Einzelheiten finden Sie unter [Verwalten von per Volumenlizenz aus dem Windows Store für Unternehmen erworbenen Apps](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) in [Funktionen in Technical Preview 1604 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **SmartLock-Einstellung für Android-Geräte**

  Eine neue Einstellung wurde dem Konfigurationselement „Android und Samsung KNOX Standard“ hinzugefügt. Mit dieser Einstellung können Sie das SmartLock-Feature auf kompatiblen Android-Geräten steuern.  Mit dieser Einstellung können Sie verhindern, dass Endbenutzer Smart Lock konfigurieren. Weitere Informationen finden Sie unter [SmartLock-Einstellung für Android-Geräte](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) in [Funktionen in Technical Preview 1604 für System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)  
 Im April 2016 wurden keine neuen Hybridfeatures für Configuration Manager (Current Branch) eingeführt.  

##  <a name="march-2016"></a>März 2016  

### <a name="new-in-microsoft-intune"></a>Neuheiten in Microsoft Intune  
 Die folgenden im März 2016 eingeführten Intune-Features werden in Hybridbereitstellungen unterstützt.  

- **MAM-Steuerelemente, um die Synchronisierung von Kontakten zu verhindern (iOS)**

  Eine neue Einstellung ist verfügbar, mit der Sie verhindern können, dass eine Anwendung Kontakte mit dem nativen Adressbuch auf iOS-Geräten synchronisiert. Diese neue Einstellung wird von der Outlook-Anwendung auf iOS-Geräten unterstützt. Weitere Einzelheiten zu diesen und anderen Einstellungen finden Sie unter [Create and deploy MAM policies (Erstellen und Bereitstellen von MAM-Richtlinien)](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in der Intune-Bibliothek.  

- **Skype for Business Online unterstützt den bedingten Zugriff**

  Sie können eine Richtlinie für bedingten Zugriff für Skype for Business Online festlegen, damit nur verwaltete und kompatible IOS- und Android-Geräte darauf zugreifen können.  Einzelheiten finden Sie unter [Manage access to Skype for Business Online (Verwalten des Zugriffs auf Skype for Business Online)](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) in der Intune-Bibliothek.  

- **Unterstützung für iOS 9.3**

  Am Montag, den 21. März, hat Apple die Verfügbarkeit von iOS 9.3 bekannt gegeben. Alle derzeit für die Verwaltung von iOS-Geräten verfügbaren Intune-Features werden auch weiterhin problemlos unterstützt, wenn die Benutzer ein Upgrade ihrer Geräte auf iOS 9.3 durchführen.  

- **Windows-App-Pakete direkt über die Unternehmensportal-Website verfügbar**

  Benutzer von Windows 8-, Windows 8.1- und Windows RT-PCs können jetzt Windows-App-Pakete (mit der Erweiterung „.appx“) direkt über die Unternehmensportal-Website installieren. Zuvor mussten Sie die Unternehmensportal-App bereitstellen, oder die Benutzer mussten die Unternehmensportal-App auf ihren Geräten installieren, um Apps zu installieren.  

- **Benutzer können ihr Gerät über die Unternehmensportal-Website remote sperren**

  Eine neue Option „Remotesperre“ wurde der Unternehmensportal-Website hinzugefügt, damit Benutzer ihr Gerät remote über das Portal sperren können, wenn es verloren ging oder gestohlen wurde.  

- **Profitieren Sie von der „Öffnen in“-Verwaltung für Geräte, die in einer Drittanbieter-MDM-Lösung angemeldet sind**

  Sie können über Ihren Drittanbieter der Verwaltung mobiler Geräte (MDM) von der „Öffnen in“-Verwaltung von iOS profitieren. Sie können die Einschränkungen in den Konfigurationsprofileinstellungen festlegen und die App mithilfe der MDM-Software bereitstellen. Wenn der Benutzer die verwaltete App installiert, werden die Einschränkungen angewendet. Lesen Sie die Details [Microsoft Intune-Richtlinien für die Verwaltung von mobilen Apps und iOS-Feature „Öffnen in“](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) in der Intune-Bibliothek.  

- **Microsoft-Apps, die MAM unterstützen**

  Die Liste der Microsoft-Apps, die Sie mit Verwaltungsrichtlinien für mobile Anwendungen von Intune verwenden können, wurde aktualisiert und enthält nun die neuesten Apps (nur für Geräte, die bei Intune registriert sind).  

- **Bereitstellen von Adobe Reader für Microsoft Intune auf Intune-verwalteten iOS-Geräten in Ihrem Unternehmen**

  Die Adobe Reader-App für iOS kann jetzt auf registrierten Geräten mit der Verwaltungsrichtlinie für mobile Anwendungen von Intune verwaltet werden.  

- Die Rights Management-Freigabe-App wird für Android unterstützt.

  IT-Administratoren können Verwaltungsrichtlinien für mobile Anwendungen bereitstellen, damit Endbenutzer Bilder, AV- und PDF-Dateien sicherer unabhängig davon anzeigen können, ob die IT die Geräte mit Intune verwaltet.  

- **Verbesserungen der Android- und iOS-Unternehmensportal-App**

  -   Wenn Ihre Benutzer eine App starten, die durch die Verwaltung mobiler Anwendungen (MAM) verwaltet wird, sehen sie eine Meldung, die sie darüber informiert, dass die App von ihrem Unternehmen verwaltet wird. Die Benutzer können nun auf eine Link „Weitere Informationen“ tippen, um weitere Informationen zur Bedeutung von „verwalteten Apps“ abzurufen. Sie können auch auf „Nicht mehr anzeigen“ tippen, damit die Meldung nicht mehr angezeigt wird, wenn sie die App starten.  

  -   Neue Bildschirme wurden hinzugefügt, um den Benutzer durch den Registrierungsprozess zu führen und darüber zu informieren, weshalb sich Benutzer registrieren sollten und was IT-Administratoren auf ihren registrierten Geräten sehen können und was nicht.  

  -   Registrierungsfehlermeldungen werden nun in der Unternehmensportal-App angezeigt.  

### <a name="new-in-configuration-manager-technical-preview"></a>Neuheiten in Configuration Manager Technical Preview  
 Im März 2016 wurden keine neuen Hybridfeatures für Configuration Manager Technical Preview eingeführt.  

### <a name="new-in-configuration-manager-current-branch"></a>Neuheiten in Configuration Manager (Current Branch)  
 Die folgenden neuen Features vom März 2016 sind in Hybridbereitstellungen mit Intune und Configuration Manager (Current Branch) Version 1602 verfügbar. Diese Features setzen voraus, dass Sie die Configuration Manager-Konsole zum Konfigurieren und Verwalten verwenden.  

- **Richtlinien zur Konfiguration von iOS-Apps**

  In Version 1602 von Configuration Manager (Current Branch) können Sie App-Konfigurationsrichtlinien verwenden, um Einstellungen anzugeben, die beim Ausführen einer iOS-App durch den Benutzer erforderlich sein können. Weitere Einzelheiten finden Sie unter [Configure iOS apps with app configuration policies in System Center Configuration Manager (Konfigurieren von iOS-Apps mit Konfigurationsrichtlinien für Apps in System Center Configuration Manager)](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Verwalten von per Volumenlizenz erworbenen iOS-Apps**

  In Version 1602 von Configuration Manager (Current Branch) können Sie Apps bereitstellen und verwalten, die über das Apple Volume-Purchase Program (VPP) erworben wurden, indem die Lizenzinformationen aus dem App Store importiert werden und nachverfolgt wird, wie viele Lizenzen Sie verwendet haben. Weitere Informationen finden Sie unter [Manage volume-purchased iOS apps with System Center Configuration Manager (Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden, mit System Center Configuration Manager)](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Automatische Erstellung von mobilen Office-Apps**

  Ab Version 1602 von Configuration Manager (Current Branch) werden die folgenden mobilen Microsoft Office-Apps für Android und iOS erstellt, wenn Sie ein Upgrade von Version 1511 durchführen:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (nur iOS)  
  -   Microsoft Outlook  

  Sie finden diese Apps im Knoten „Anwendungen“ der Configuration Manager-Konsole. Weitere Informationen zum Bereitstellen von Anwendungen finden Sie unter [Bereitstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Einstellungen für den Kioskmodus für Android Samsung KNOX Standard-Geräte**

  Über den Kioskmodus können Sie ein Gerät sperren, damit nur bestimmte Features funktionieren.  Ab Version 1602 von Configuration Manager (Current Branch) können Sie jetzt Einstellungen für den Kioskmodus für Samsung KNOX Standard-Geräte angeben. Einzelheiten finden Sie unter [Erstellen von Konfigurationselementen für Android- und Samsung KNOX Standard-Geräte, die ohne den System Center Configuration Manager-Client verwaltet werden](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **iOS-Aktivierungssperre**

  Ab Version 1602 von Configuration Manager (Current Branch) können Sie die iOS-Aktivierungssperre verwalten, ein Feature der App „Mein iPhone suchen“ für iOS 7.1 und höher. Die Aktivierungssperre wird automatisch aktiviert, wenn die iPhone-App „Mein iPhone suchen“ auf einem Gerät verwendet wird.  Einzelheiten finden Sie unter [Manage iOS Activation Lock Bypass with System Center Configuration Manager (Verwalten der iOS-Aktivierungssperre-Umgehung mit System Center Configuration Manager)](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  
