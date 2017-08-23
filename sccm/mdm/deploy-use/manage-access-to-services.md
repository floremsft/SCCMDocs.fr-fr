---
title: Bedingter Zugriff | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie den bedingten Zugriff in System Center Configuration Manager verwenden, um Ihre E-Mails und andere Dienste zu schützen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: "26"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d6933a331bb229f7e378e8f0bfa511f6b0553ae9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Verwalten des Zugriffs auf Dienste in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Bedingter Zugriff in System Center Configuration Manager
Verwenden Sie den **bedingten Zugriff**, um E-Mails und andere Dienste auf den Geräten, die mit Microsoft Intune registriert sind, basierend auf den von Ihnen festgelegten Bedingungen zu schützen.  

 Informationen zum **bedingten Zugriff auf PCs, die mit System Center Configuration Manager** verwaltet und auf Kompatibilität bewertet werden, finden Sie unter [Verwalten des Zugriffs auf Office 365-Dienste für PCs, die von System Center Configuration Manager verwaltet werden](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 Ein typischer Ablauf für bedingten Zugriff könnte wie folgt aussehen:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Verwenden Sie den bedingten Zugriff zum Verwalten des Zugriffs auf folgende Dienste:  

-   Microsoft Exchange lokal  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype for Business Online

-   Dynamics CRM Online

 Um den bedingten Zugriff zu implementieren, konfigurieren Sie zwei Richtlinientypen in Configuration Manager:  

-   **Konformitätsrichtlinien** sind optionale Richtlinien, die Sie für Benutzersammlungen bereitstellen können. Mit diesen Richtlinien werden Einstellungen wie die folgenden ausgewertet:  

    -   Passwort  

    -   Verschlüsselung  

    -   Ob das Gerät per Jailbreak oder Rooting manipuliert wurde  

    -   Ob E-Mails auf dem Gerät von Configuration Manager oder einer Intune-Richtlinie verwaltet werden  

     **Wenn keine Kompatibilitätsrichtlinie für ein Gerät bereitgestellt wird, dann behandeln alle anwendbaren Richtlinien für den bedingten Zugriff das Gerät als kompatibel**.  

-   **Richtlinien für den bedingten Zugriff** werden für einen bestimmten Dienst konfiguriert und definieren Regeln wie z.B., welche Azure Active Directory-Sicherheitsbenutzergruppen oder Configuration Manager-Benutzersammlungen als Ziel dienen oder davon ausgeschlossen sind.  

     Sie konfigurieren die Richtlinie für den bedingten lokalen Exchange-Zugriff über die Configuration Manager-Konsole. Wenn Sie jedoch eine Exchange Online- oder SharePoint Online-Richtlinie konfigurieren, wird die Intune-Verwaltungskonsole geöffnet, in der Sie die Richtlinie konfigurieren.  

     Im Gegensatz zu anderen Intune- oder Configuration Manager-Richtlinien stellen Sie keine Richtlinien für den bedingten Zugriff bereit. Stattdessen konfigurieren Sie diese einmalig; anschließend gelten sie für alle Zielbenutzer.  

 Wenn Geräte die von Ihnen konfigurierten Bedingungen nicht erfüllen, erhält der Benutzer Anweisungen zum Registrieren des Geräts und zum Beheben des Problems, das die Konformität des Geräts verhindert.  

**Bevor** Sie den bedingten Zugriff verwenden können, müssen Sie sicherstellen, dass die jeweiligen **Anforderungen** erfüllt sind:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Anforderungen für Exchange Online (bei Verwendung der freigegebenen Umgebung mit mehreren Mandanten)
Bedingter Zugriff auf Exchange Online unterstützt Geräte, die Folgendes ausführen:
-   Windows 8.1 und höher (bei Registrierung mit Intune)
-   Windows 7.0 oder Windows 8.1 (bei Einbindung in eine Domäne)
-   Windows Phone 8.1 und höher
-   iOS 7.1 und höher
-   Android 4.0 und höher, Samsung KNOX Standard 4.0 und höher

 **Darüber hinaus gilt**:
-   Geräte erfordern eine Verknüpfung mit dem Arbeitsplatz, wodurch das Gerät beim Azure Active Directory Device Registration Service (AAD DRS) registriert wird.<br />     
- In eine Domäne eingebundene PCs müssen automatisch über eine Gruppenrichtlinie oder MSI bei Azure Active Directory registriert werden.

  Im Abschnitt **Bedingter Zugriff für PCs** in diesem Thema sind alle Anforderungen für die Aktivierung des bedingten Zugriffs für einen PC beschrieben.<br />     
  AAD DRS wird automatisch für Intune und Office 365-Kunden aktiviert. Kunden, die bereits den AD FS Device Registration Service bereitgestellt haben, sehen keine registrierten Geräte in ihrem lokalen Active Directory.
-   Sie müssen ein Office 365-Abonnement verwenden, das Exchange Online (z. B. E3) umfasst, und die Benutzer müssen für Exchange Online lizenziert sein.
-   Der optionale **Exchange Server-Connector** ist optional und verbindet Configuration Manager mit Microsoft Exchange Online. Er hilft bei der Überwachung von Geräteinformationen über die Configuration Manager-Konsole (Informationen dazu finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
Der Connector ist nicht zur Verwendung von Konformitätsrichtlinien oder Richtlinien für den bedingten Zugriff erforderlich, aber zum Ausführen von Berichten, mit deren Hilfe die Auswirkungen des bedingten Zugriffs bewertet werden.

## <a name="requirements-for-exchange-online-dedicated"></a>Anforderungen für Exchange Online Dedicated
Bedingter Zugriff auf Exchange Online Dedicated unterstützt Geräte, die Folgendes ausführen:
-   Windows 8 und höher (bei Registrierung mit Intune)
-   Windows 7.0 oder Windows 8.1 (bei Einbindung in eine Domäne)

  Bedingter Zugriff auf PCs, die in eine Domäne eingebunden sind, nur für Mandanten in der neuen Exchange Online Dedicated-Umgebung.
-   Windows Phone 8 und höher
-   Beliebige iOS-Geräte, die einen Exchange ActiveSync-E-Mail-Client (EAS) verwenden
-   Android 4 und höher
-   Für Mandanten in der **Exchange Online Dedicated-Legacyumgebung** gilt Folgendes:    

  Sie müssen den **Exchange Server-Connector** verwenden, der Configuration Manager mit Microsoft Exchange On-Premises verbindet. - Dies ermöglicht die Verwaltung mobiler Geräte und bedingten Zugriff (Informationen dazu finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
-   Für Mandanten in der **neuen Exchange Online Dedicated-Umgebung** gilt Folgendes:     
  Der optionale **Exchange Server-Connector** verbindet Configuration Manager mit Microsoft Exchange Online und hilft bei der Verwaltung von Geräteinformationen (Informationen dazu finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)). Der Connector ist nicht zur Verwendung von Konformitätsrichtlinien oder Richtlinien für den bedingten Zugriff erforderlich, aber zum Ausführen von Berichten, mit deren Hilfe die Auswirkungen des bedingten Zugriffs bewertet werden.  

## <a name="requirements-for-exchange-on-premises"></a>Anforderungen für lokales Exchange
Beim bedingten Zugriff auf Exchange lokal wird Folgendes unterstützt:
-   Windows 8 und höher (bei Registrierung mit Intune)
-   Windows Phone 8 und höher
-   Systemeigene E-Mail-App unter iOS
-   Systemeigene E-Mail-App unter Android 4 oder höher
-   Microsoft Outlook-App wird nicht unterstützt (Android und iOS).

**Darüber hinaus gilt**:

-  Es muss sich bei der Exchange-Version um Exchange 2010 oder höher handeln. Exchange Server-Clientzugriffsserver-Arrays werden unterstützt.

> [!TIP]
> Wenn sich Ihre Exchange-Umgebung in einer Clientzugriffsserver-Konfiguration befindet, müssen Sie den lokalen Exchange-Connector so konfigurieren, dass er auf einen der Clientzugriffsserver zeigt.
- Sie müssen den **Exchange Server-Connector** verwenden, der Configuration Manager mit lokalem Microsoft Exchange verbindet. Dies ermöglicht die Verwaltung mobiler Geräte und bedingten Zugriff (Informationen dazu finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
  - Stellen Sie sicher, dass Sie die neueste Version des **lokalen Exchange-Connectors**verwenden. Der lokale Exchange-Connector sollte über die Configuration Manager-Konsole konfiguriert werden. Eine ausführliche exemplarische Vorgehensweise finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Der Connector muss nur auf dem primären System Center Configuration Manager-Standort konfiguriert werden.</li><li>Dieser Connector unterstützt die Exchange-Clientzugriffsserver-Umgebung. <br />        Sie müssen den Connector so konfigurieren, dass er mit einem der Exchange-Clientzugriffsserver kommuniziert.

- Exchange ActiveSync kann mit zertifikatbasierter Authentifizierung oder Eingabe von Anmeldeinformationen konfiguriert werden


## <a name="requirements-for-skype-for-business-online"></a>Anforderungen für Skype for Business Online
Bedingter Zugriff auf SharePoint Online unterstützt Geräte, die Folgendes ausführen:
 -   iOS 7.1 und höher
 -   Android 4,0 und höher
 -   Samsung KNOX Standard 4.0 oder höher

**Darüber hinaus** müssen Sie die moderne Authentifizierung für Skype for Business Online aktivieren. Füllen Sie dieses [Anmeldeformular](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) aus, um sich für die moderne Authentifizierung zu registrieren.

Alle Ihre Endbenutzer müssen Skype for Business Online verwenden. Wenn Sie eine Bereitstellung sowohl mit Skype for Business Online als auch Skype for Business haben, wird die Richtlinie für bedingten Zugriff nicht für Endbenutzer angewendet, die zur lokalen Bereitstellung gehören.

## <a name="requirements-for-sharepoint-online"></a>Anforderungen für SharePoint Online
Bedingter Zugriff auf SharePoint Online unterstützt Geräte, die Folgendes ausführen:
 -   Windows 8.1 und höher (bei Registrierung mit Intune)
 -   Windows 7.0 oder Windows 8.1 (bei Einbindung in eine Domäne)
 -   Windows Phone 8.1 und höher
 -   iOS 7.1 und höher
 -   Android 4.0 und höher, Samsung KNOX Standard 4.0 und höher

 **Darüber hinaus gilt**:
 -   Geräte erfordern eine Verknüpfung mit dem Arbeitsplatz, wodurch das Gerät beim Azure Active Directory Device Registration Service (AAD DRS) registriert wird.

 In eine Domäne eingebundene PCs müssen automatisch über eine Gruppenrichtlinie oder MSI bei Azure Active Directory registriert werden. Im Abschnitt **Bedingter Zugriff für PCs** in diesem Thema sind alle Anforderungen für die Aktivierung des bedingten Zugriffs für einen PC beschrieben.

 AAD DRS wird automatisch für Intune und Office 365-Kunden aktiviert. Kunden, die bereits den AD FS Device Registration Service bereitgestellt haben, sehen keine registrierten Geräte in ihrem lokalen Active Directory.
 -   Es ist ein SharePoint Online-Abonnement erforderlich, und Benutzer müssen für SharePoint Online lizenziert sein.

 ### <a name="conditional-access-for-pcs"></a>Bedingter Zugriff für PCs

 Sie können den bedingten Zugriff für PCs einrichten, auf denen Office-Desktopanwendungen ausgeführt werden, um auf **Exchange Online** und **SharePoint Online** zuzugreifen. Dies gilt für PCs, die folgende Anforderungen erfüllen:
 -   Auf dem PC muss Windows 7.0 oder Windows 8.1 ausgeführt werden.
 -   Der PC muss entweder in eine Domäne eingebunden oder kompatibel sein.

 Damit der PC kompatibel ist, muss er bei Intune registriert sein und den Richtlinien entsprechen.

 Für in die Domäne eingebundene PCs müssen Sie [das Gerät für eine automatische Registrierung](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) bei Azure Active Directory einrichten.
 -   [Die moderne Authentifizierung von Office 365 muss aktiviert sein](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)und alle neuesten Office-Updates enthalten.<br />     Die moderne Authentifizierung ermöglicht Windows-Clients mit Office 2013 eine Active Directory Authentication Library (ADAL)-basierte Anmeldung und bietet größere Sicherheit wie **mehrstufige Authentifizierung**und **zertifikatbasierte Authentifizierung**.
 -   Setup-ADFS beansprucht Regeln zum Blockieren von nicht moderner Authentifizierungsprotokolle.  

## <a name="next-steps"></a>Nächste Schritte  
 Lesen Sie die folgenden Themen, um mehr über das Konfigurieren von Konformitätsrichtlinien und Richtlinien für den bedingten Zugriff für Ihr Szenario zu erfahren:  

-   [Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Verwalten des E-Mail-Zugriffs in System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Verwalten des SharePoint Online-Zugriffs in System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Verwalten des Zugriffs auf Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Weitere Informationen:  

 [Erste Schritte mit Kompatibilitätseinstellungen in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
