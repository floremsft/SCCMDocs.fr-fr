---
title: "Verwalten des Zugriffs auf Office 365-Dienste für verwaltete PCs | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie den bedingten Zugriff für PCs konfigurieren, die von System Center Configuration Manager verwaltet werden."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: "15"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: aede531a0406c3d30c9cca957896e002ed22ae51
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Verwalten des Zugriffs auf Office 365-Dienste für PCs, die von System Center Configuration Manager verwaltet werden

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1602 von Configuration Manager können Sie einen bedingten Zugriff für PCs konfigurieren, die von System Center Configuration Manager verwaltet werden.  

> [!IMPORTANT]  
> Dieses Vorabfeature ist in Update 1602, Update 1606 und Update 1610 verfügbar. Vorab veröffentlichte Features werden in das Produkt aufgenommen, um sie in einem frühen Stadium in einer Produktionsumgebung zu testen. Sie sollten nicht als für den Produktivbetrieb geeignet betrachtet werden. Weitere Informationen finden Sie unter [Use pre-release features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Verwenden von Vorabfeatures aus Updates).
> - Nach der Installation von Update 1602 wird der Featuretyp als endgültige Version angezeigt, obwohl es sich um eine Vorabversion handelt.
> - Wenn Sie anschließend von 1602 auf 1606 aktualisieren, wird der Featuretyp als endgültige Version angezeigt, obwohl es sich weiterhin um eine Vorabversion handelt.
> - Wenn Sie von Version 1511 direkt auf 1606 aktualisieren, wird der Featuretyp als Vorabversion angezeigt.

Informationen zum Konfigurieren des bedingten Zugriffs für bei Intune registrierte und mit Intune verwaltete Geräte oder zum Konfigurieren von PCs, die in die Domäne eingebunden sind und nicht auf Kompatibilität überprüft werden, finden Sie unter [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).

## <a name="supported-services"></a>Unterstützte Dienste  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>Unterstützte PCs  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>Unterstützte Windows Server-Versionen

-   2008 R2
-   2012
-   2012 R2
-   2016

    > [!IMPORTANT]
    > Bei Windows Server-Versionen, bei denen mehrere Benutzer gleichzeitig angemeldet sein können, müssen für alle angemeldeten Benutzer die gleichen Richtlinien für den bedingten Zugriff bereitgestellt werden.

## <a name="configure-conditional-access"></a>Konfigurieren des bedingten Zugriffs  
 Bevor Sie den bedingten Zugriff einrichten können, müssen Sie zunächst eine Kompatibilitätsrichtlinie erstellen und eine Richtlinie für bedingten Zugriff konfigurieren. Wenn Sie Richtlinien für bedingten Zugriff für PCs konfigurieren, können Sie verlangen, dass die PCs der Kompatibilitätsrichtlinie entsprechen müssen, damit sie auf Exchange Online- und SharePoint Online-Dienste zugreifen können.  

### <a name="prerequisites"></a>Voraussetzungen  

-   AD FS-Synchronisierung (Active Directory Federation Services, Active Directory-Verbunddienste) sowie ein Office 365-Abonnement Das Office 365-Abonnement wird zum Einrichten von Exchange Online und SharePoint Online benötigt.  

-   Microsoft Intune-Abonnement. Das Microsoft Intune-Abonnement muss in der Configuration Manager-Konsole konfiguriert werden. Das Intune-Abonnement wird zur Weiterleitung des Konformitätszustands des Geräts an Azure Active Directory und zur Benutzerlizenzierung verwendet.  

 Die PCs müssen folgende Anforderungen erfüllen:  

-   Die[Voraussetzungen](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) für die automatische Geräteregistrierung bei Azure Active Directory müssen erfüllt sein.  

     Sie können PCs bei Azure Active Directory (Azure AD) über die Kompatibilitätsrichtlinie registrieren.  

    -   PCs unter Windows 8.1 und Windows 10 können Sie mithilfe einer Active Directory-Gruppenrichtlinie für die automatische Registrierung bei Azure AD konfigurieren.  

    -   Auf PCs unter Windows 7 müssen Sie das Geräteregistrierungs-Softwarepaket auf Ihren Windows 7-PC über System Center Configuration Manager bereitstellen. Weitere Informationen finden Sie unter dem Thema [Automatische Geräteregistrierung bei Azure Active Directory für in Domänen eingebundene Windows-Geräte](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   Auf dem PCs muss Office 2013 oder Office 2016 mit [aktivierter](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)moderner Authentifizierung verwendet werden.  

 Die nachfolgend beschriebenen Schritte gelten für Exchange Online und SharePoint Online.  

### <a name="step-1-configure-compliance-policy"></a>Schritt 1: Konfigurieren von Kompatibilitätsrichtlinien  
 Erstellen Sie in der Configuration Manager-Konsole eine Kompatibilitätsrichtlinie mit den folgenden Regeln:  

-   Registrierung in Azure Active Directory erforderlich: Diese Regel prüft, ob das Gerät des Benutzers in Azure AD eingebunden ist. Falls nicht, wird es automatisch in Azure AD registriert. Die automatische Registrierung wird nur unter Windows 8.1 unterstützt. Stellen Sie für Windows 7-PCs eine MSI-Datei bereit, um die automatische Registrierung durchzuführen. Weitere Informationen finden Sie unter [Automatische Geräteregistrierung bei Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   **Alle mit einem Stichtag älter als X Tage installierten benötigten Updates:** Diese Regel überprüft, ob das Gerät des Benutzers gemäß dem Stichtag und der Toleranzperiode, die Sie festgelegt haben, über alle erforderlichen Updates verfügt (entsprechend der Angabe in der Regel „Erforderliche automatische Updates“) und installiert automatisch alle ausstehenden Updates.  

-   **BitLocker-Laufwerkverschlüsselung erfordern:** Dies ist eine Prüfung, ob das primäre Laufwerk (z.B. C:\\) auf dem Gerät mit BitLocker verschlüsselt ist. Wenn die Bitlocker-Verschlüsselung auf dem primären Gerät nicht aktiviert ist, wird der Zugriff auf E-Mail- und SharePoint-Dienste blockiert.  

-   **Antischadsoftware erfordern:** Dies ist eine Prüfung, um herauszufinden, ob die Antischadsoftware (nur System Center Endpoint Protection oder Windows Defender) aktiviert ist und ausgeführt wird. Falls nicht, wird der Zugriff auf E-Mail- und SharePoint-Dienste blockiert.  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Schritt 2: Bewerten der Auswirkungen des bedingten Zugriffs  
 Führen Sie den „Bericht zur Kompatibilität mit bedingtem Zugriff“ aus. Sie finden ihn im Abschnitt „Überwachung“ unter „Berichte“ > „Kompatibilitäts- und Einstellungsverwaltung“. Dort wird der Kompatibilitätsstatus für alle Geräte angezeigt.  Für Geräte, die als nicht kompatibel gemeldet werden, wird der Zugriff auf Exchange Online und SharePoint Online blockiert.  

 ![CA&#95;compliance&#95;report](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Konfigurieren von Active Directory-Sicherheitsgruppen  
 Je nach Art der Richtlinie weisen Sie Benutzergruppen spezielle Richtlinien für bedingten Zugriff zu. Die Gruppen beinhalten die Benutzer, für die die Richtlinie gelten soll oder die davon ausgeschlossen sind. Bei Benutzern, für die eine Richtlinie gelten soll, muss jedes von ihnen verwendete Gerät die Richtlinie erfüllen, damit sie auf den Dienst zugreifen können.  

 Active Directory-Sicherheitsbenutzergruppen. Diese Benutzergruppen müssen mit Azure Active Directory synchronisiert werden. Sie können diese Gruppen auch im Office 365 Admin Center oder im Intune-Kontenportal konfigurieren.  

 Sie können für jede Richtlinie zwei Arten von Gruppen angeben :  

-   **Zielgruppen:** Benutzergruppen, auf die die Richtlinie angewendet wird Die gleiche Gruppe sollte sowohl für Konformität und die Richtlinie für bedingten Zugriff verwendet werden.  

-   **Ausgenommene Gruppen:** Benutzergruppen, die von der Richtlinie ausgenommen sind (optional)  
    Benutzer, die in beiden Gruppen enthalten sind, werden von der Richtlinie ausgenommen.  

     Es werden nur die Gruppen ausgewertet, für die die Richtlinie für bedingten Zugriff gilt.  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Schritt 3:  Erstellen einer Richtlinie für bedingten Zugriff für Exchange Online und SharePoint Online  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Zum Erstellen einer Richtlinie für Exchange Online wählen Sie die Option **Richtlinie für bedingten Zugriff für Exchange Online aktivieren**aus.  

     Zum Erstellen einer Richtlinie für SharePoint Online wählen Sie die Option **Richtlinie für bedingten Zugriff für SharePoint Online aktivieren**aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Links** auf **Richtlinie für bedingten Zugriff in der Intune-Konsole konfigurieren**. Sie müssen möglicherweise den Benutzernamen und das Kennwort des Kontos angeben, das zum Verbinden von Configuration Manager mit Intune verwendet wird.  

     Die Intune-Verwaltungskonsole wird geöffnet.  

4.  Für Exchange Online klicken Sie in der Microsoft Intune-Verwaltungskonsole auf **Richtlinie > Bedingter Zugriff > Exchange Online-Richtlinie**.  

     Für SharePoint Online klicken Sie in der Microsoft Intune-Verwaltungskonsole auf **Richtlinie> Bedingter Zugriff > SharePoint Online-Richtlinie**.  

5.  Legen Sie die Anforderung für Windows-PCs auf die Option**Geräte müssen kompatibel sein**fest.  

6.  Klicken Sie unter **Zielgruppen**auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, für die die Richtlinie gelten soll.  

    > [!NOTE]  
    >  Die gleiche Sicherheitsbenutzergruppe sollte für die Bereitstellung von Konformitätsrichtlinien und die Zielgruppe für bedingte Zugriffsrichtlinien verwendet werden.  

     Klicken Sie unter **Ausgenommene Gruppen**optional auf **Ändern** , um die Active Directory-Sicherheitsgruppen auszuwählen, die von dieser Richtlinie ausgenommen werden.  

7.  Klicken Sie auf **Speichern** , um die Richtlinie zu erstellen und zu speichern.  

 Endbenutzer, die aufgrund von Nichtkompatibilität blockiert werden, erhalten im System Center Configuration Manager-Softwarecenter Informationen zur Kompatibilität. Für sie wird eine erneute Richtlinienauswertung ausgelöst, nachdem Kompatibilitätsprobleme behoben wurden.  

<!---
##  <a name="bkmk_KnownIssues"></a> Known issues  
 You may see the following issues when using this feature:  

-   In this 1602 update,  the 5 day compliance is not enforced. Even if compliance check on the end-user's device has happened more than 5 days ago, users still can access Office 365 and SharePoint online.  

-   When a device is not compliant with the compliance policy, the reason is not automatically displayed. The end- user must go to the new Software Center to find the reason for non-compliance. The reason is displayed in the Device compliance section of the Software Center.  

-   Windows 10 users may see multiple access failures when trying to reach O365 and/or SharePoint online resources. Note that conditional access is not fully supported for Windows 10.  
--->
## <a name="see-also"></a>Weitere Informationen:

- [Schützen der Daten und Standortinfrastruktur mit System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Flussdiagramm der Problembehandlung beim bedingten Zugriff für Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)
