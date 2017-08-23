---
title: Verwalten des E-Mail-Zugriffs | Microsoft-Dokumentation
description: Hier erfahren Sie, wie mit dem bedingten Zugriff in System Center Configuration Manager der Zugriff auf Exchange-E-Mail verwaltet wird.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
caps.latest.revision: "24"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: a5c2a8912cd2ef95a778b81d0b7f1f98315b8413
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-email-access-in-system-center-configuration-manager"></a>Verwalten des E-Mail-Zugriffs in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie den bedingten Zugriff von System Center Configuration Manager, um den Zugriff auf Exchange-E-Mail basierend auf den von Ihnen festgelegten Bedingungen zu verwalten.  

Sie können den Zugriff auf folgende Module verwalten:  

-   Microsoft Exchange lokal  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated

Sie können den Zugriff auf Exchange Online und Exchange On-Premises über den integrierten E-Mail-Client auf den folgenden Plattformen steuern:  

-   Android 4.0 und höher, Samsung KNOX Standard 4.0 und höher  

-   iOS 7.1 und höher  

-   Windows Phone 8.1 und höher  

-   E-Mail-Anwendung unter Windows 8.1 und höher

Office-Desktopanwendungen können auf PCs, auf denen Folgendes ausgeführt wird, auf Exchange Online zugreifen:  

-   Office-Desktop 2013 und höher mit aktivierter [moderner Authentifizierung](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) .  

-   Windows 7.0 oder Windows 8.1  

> [!NOTE]  
>  PCs müssen in eine Domäne eingebunden oder mit den in Intune festgelegten Richtlinien kompatibel sein.  


## <a name="device-requirements"></a>Geräteanforderungen
 Wenn Sie den bedingten Zugriff konfigurieren, bevor Benutzer ihre E-Mails abrufen können, muss das Gerät folgende Voraussetzungen erfüllen:  

-   Es muss bei Intune oder einem in die Domäne eingebundenen PC registriert sein.  

-   Das Gerät muss in Azure Active Directory registriert sein (dies erfolgt automatisch bei der Registrierung des Geräts in Intune – nur für Exchange Online). Darüber hinaus muss die Client-ID für Exchange ActiveSync bei Azure Active Directory registriert sein (gilt nicht für Windows- und Windows Phone-Geräten, die mit Exchange lokal verknüpft sind).  

     Für einen in die Domäne eingebundenen PC müssen Sie es für eine automatische Registrierung bei Azure Active Directory festlegen.  Im Abschnitt **Bedingter Zugriff für PCs** im Thema [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) ist der vollständige Satz von Anforderungen zum Aktivieren des bedingten Zugriff für PCs aufgelistet.  

-   Sie müssen mit allen für das Gerät bereitgestellten Kompatibilitätsrichtlinien von Configuration Manager kompatibel sein.  

 Wenn eine Bedingung für den bedingten Zugriff nicht erfüllt wird, erhält der Benutzer bei der Anmeldung eine der folgenden Meldungen:  

-   Wenn das Gerät nicht bei Intune oder in Azure Active Directory registriert ist, wird eine Meldung mit Anweisungen zum Installieren der Unternehmensportal-App, zum Registrieren des Geräts und (für Android und iOS-Geräte) zum Aktivieren des E-Mail-Zugriffs angezeigt. Bei Letzterem wird die Exchange ActiveSync-ID des Geräts mit dem Gerätedatensatz in Azure Active Directory verknüpft.  

-   Wenn das Gerät nicht kompatibel ist, wird eine Meldung angezeigt, die den Benutzer zum Intune-Webportal weiterleitet. Hier finden Sie Informationen über das Problem und dessen Lösung.  

**Für mobile Geräte:**

Sie können den Zugriff auf **Outlook Web Access (OWA)** auf Exchange Online verweigern, wenn der Zugriff von einem Browser von **iOS** - und **Android** -Geräten erfolgt.  Der Zugriff wird nur von unterstützten Browsern auf kompatiblen Geräten gewährt:

* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS und Android)

Nicht unterstützte Browser werden blockiert. Die OWA-Apps für iOS und Android werden nicht unterstützt.  Sie müssen über AD FS-Anspruchsregeln blockiert werden:
* Setup-ADFS beansprucht Regeln zum Blockieren von nicht moderner Authentifizierungsprotokolle. Detaillierte Anweisungen werden in Szenario 3 beschrieben: [Blockieren des gesamten Zugriffs auf Office 365 außer durch browserbasierte Anwendungen](https://technet.microsoft.com/library/dn592182.aspx).

 **Für PCs:**  

-   Wenn die Richtlinienanforderung für bedingten Zugriff das Zulassen von **In die Domäne eingebunden** oder **Kompatibel**vorsieht, wird eine Meldung mit Anweisungen zum Registrieren des Geräts angezeigt. Wenn der PC keine der Anforderungen erfüllt, wird der Benutzer aufgefordert, das Gerät bei Intune zu registrieren.  

-   Wenn die Richtlinienanforderung für bedingten Zugriff nur das Zulassen von in die Domäne eingebundenen Windows-Geräten vorsieht, wird das Gerät blockiert und die Meldung angezeigt, dass der IT-Administrator kontaktiert werden sollte.  

 Sie können den Zugriff auf Exchange-E-Mails auf den folgenden Plattformen über den geräteinternen Exchange ActiveSync-E-Mail-Client blockieren:  

-   Android 4.0 und höher, Samsung KNOX Standard 4.0 und höher  

-   iOS 7.1 und höher  

-   Windows Phone 8.1 und höher  

-   **E-Mail-Anwendung** unter Windows 8.1 und höher  

 Die Outlook-App für iOS und Android und Outlook Desktop 2013 und höher werden nur für Exchange Online unterstützt.  

 Damit der bedingte Zugriff unterstützt wird, ist der **lokale Exchange Connector** zwischen Configuration Manager und Exchange erforderlich.  

 Sie können eine Richtlinie für den bedingten Zugriff für Exchange lokal über die Configuration Manager-Konsole konfigurieren. Wenn Sie eine Richtlinie für den bedingten Zugriff für Exchange Online konfigurieren, können Sie den Vorgang in der Configuration Manager-Konsole starten, wodurch die Intune-Konsole gestartet wird, in der Sie den Vorgang abschließen können.  

## <a name="configure-conditional-access"></a>Konfigurieren des bedingten Zugriffs
### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Schritt 1: Bewerten der Auswirkungen der Richtlinie für bedingten Zugriff  
 Nachdem Sie den **lokale Exchange Connector**konfiguriert haben, können Sie mithilfe des Configuration Manager-Berichts **Geräteliste nach bedingtem Zugriffsstatus** die Geräte identifizieren, deren Exchange-Zugriff nach der Konfiguration der Richtlinie für den bedingten Zugriff blockiert wird. Dieser Bericht erfordert zusätzlich:  

-   Ein Abonnement für Intune  

-   Die Konfiguration und Bereitstellung eines Dienstverbindungspunkts  

 Wählen Sie in den Berichtsparametern die auszuwertende Intune-Gruppe sowie gegebenenfalls die Geräteplattformen aus, auf die Sie die Richtlinie beschränken möchten.  

 Weitere Informationen zum Ausführen von Berichten finden Sie unter [Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

 Überprüfen Sie nach der Ausführung des Berichts die folgenden vier Spalten auf blockierte Benutzer:  

-   **Verwaltungskanal** – Gibt an, ob das Gerät durch Intune und/oder Exchange ActiveSync verwaltet wird.  

-   **Bei AAD registriert** – Gibt an, ob das Gerät bei Azure Active Directory registriert ist (wird als Arbeitsbereichsverknüpfung bezeichnet).  

-   **Kompatibel** – Gibt an, ob das Gerät mit den von Ihnen bereitgestellten Kompatibilitätsrichtlinien kompatibel ist.  

-   **EAS-aktiviert** – Bei iOS- und Android-Geräten muss die Exchange ActiveSync-ID mit dem Geräteregistrierungsdatensatz in Azure Active Directory verknüpft sein. Dies erfolgt, wenn der Benutzer in der Quarantäne-E-Mail auf den Link zum **Aktivieren von E-Mails** klickt.  

    > [!NOTE]  
    >  Für Windows Phone-Geräte wird in dieser Spalte immer ein Wert angezeigt.  

 Bei Geräten, die Teil einer Zielgruppe oder Sammlung sind, ist der Zugriff auf Exchange blockiert, sofern die Spaltenwerte nicht mit den in der folgenden Tabelle aufgeführten Werten übereinstimmen:  

|Verwaltungskanal|Bei AAD registriert|Kompatibel|EAS-aktiviert|Resultierende Aktion|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Von Microsoft Intune und Exchange ActiveSync verwaltet**|Ja|Ja|**Ja** oder **Nein** wird angezeigt.|E-Mail-Zugriff erlaubt|  
|Beliebiger anderer Wert|Nein|Nein|Es wird kein Wert angezeigt.|E-Mail-Zugriff blockiert|  

 Sie können den Inhalt des Berichts exportieren und die Benutzer über die in der Spalte **E-Mail-Adresse** enthaltene Adresse informieren, dass sie blockiert werden.  

### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Schritt 2: Konfigurieren von Benutzergruppen oder Sammlungen für die Richtlinie für bedingten Zugriff  
 Je nach Art der Richtlinie weisen Sie unterschiedlichen Benutzergruppen oder -sammlungen spezielle Richtlinien für den bedingten Zugriff zu. Die Gruppen beinhalten die Benutzer, für die die Richtlinie gelten soll oder die davon ausgeschlossen sind. Bei Benutzern, für die eine Richtlinie gelten soll, muss jedes von ihnen verwendete Gerät die Richtlinie erfüllen, damit sie auf ihre E-Mails zugreifen können.  

-   **Richtlinie für Exchange Online** – Richtet sich an Azure Active Directory-Sicherheitsbenutzergruppen. Sie können diese Gruppen in der **Office 365 Admin Center**oder im **Intune-Kontenportal**konfigurieren.  

-   **Richtlinie für lokales Exchange** – Richtet sich an Configuration Manager-Benutzersammlungen. Diese können im Arbeitsbereich **Bestand und Kompatibilität** konfiguriert werden.  

 Sie können für jede Richtlinie zwei Arten von Gruppen angeben:  

-   **Zielgruppen** – Benutzergruppen oder Sammlungen, auf die die Richtlinie angewendet wird  

-   **Ausgenommene Gruppen** – Benutzergruppen oder Sammlungen, die von der Richtlinie ausgenommen sind (optional)  

 Benutzer, die in beiden Gruppen enthalten sind, werden von der Richtlinie ausgenommen.  

 Es werden nur die Gruppen oder Sammlungen, für die die Richtlinie für bedingten Zugriff gilt, für den Exchange-Zugriff ausgewertet.  

### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Schritt 3: Konfigurieren und Bereitstellen einer Kompatibilitätsrichtlinie  
 Wichtig ist, dass Sie für alle Geräte, auf die die Exchange-Richtlinie für bedingten Zugriff angewendet wird, eine Konformitätsrichtlinie erstellen und bereitstellen.  

 Ausführliche Informationen zum Konfigurieren der Kompatibilitätsrichtlinie finden Sie unter [Verwalten von Kompatibilitätsrichtlinien für Geräte in System Center Configuration Manager](device-compliance-policies.md).  

> [!IMPORTANT]  
>  Wenn Sie keine Konformitätsrichtlinie bereitgestellt haben und dann die Exchange-Richtlinie für bedingten Zugriff aktivieren, erhalten alle betreffenden Geräte Zugriff.  

 Fahren Sie mit **Schritt 4**fort.  

### <a name="step-4-configure-the-conditional-access-policy"></a>Schritt 4: Konfigurieren der Richtlinie für bedingten Zugriff  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Für Exchange Online (und Mandanten in der neuen Exchange Online Dedicated-Umgebung)

>[!NOTE]
>Richtlinien für den bedingten Zugriff können auch in der Azure AD-Verwaltungskonsole erstellt werden. Mithilfe der Azure AD-Verwaltungskonsole können neben den anderen Richtlinien für den bedingten Zugriff wie die Multi-Factor Authentication auch die Richtlinien für den bedingten Zugriff für Intune-Geräte (als Richtlinie für den gerätebasierten bedingten Zugriff in Azure AD bezeichnet) erstellt werden. Es können auch Richtlinien für den bedingten Zugriff für von Azure AD unterstützte Unternehmensanwendungen von Drittanbietern wie Salesforce und Box festgelegt werden. Weitere Informationen finden Sie unter [How to set Azure Active Directory device-based conditional access policy for access control to Azure Active Directory connected applications (Festlegen von Azure Active Directory-Richtlinien für den gerätebasierten bedingten Zugriff zur Zugriffssteuerung bei Anwendungen, die mit Azure Active Directory verbunden sind)](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).

 Bei Richtlinien für bedingten Zugriff wird für Exchange Online mithilfe des folgenden Ablaufs bewertet, ob Geräte Zugriff erhalten.  

 ![ConditionalAccess8&#45;1](media/ConditionalAccess8-1.png)  

 Für den E-Mail-Zugriff müssen Geräte die folgenden Voraussetzungen erfüllen:  

-   Es muss bei Intune registriert sein.  

-   PCs müssen entweder in die Domäne eingebunden oder registriert und mit den in Intune festgelegten Richtlinien kompatibel sein.  

-   Das Gerät muss in Azure Active Directory registriert sein (dies erfolgt automatisch bei der Registrierung des Geräts in Intune).  

     Für in die Domäne eingebundene PCs müssen Sie [das Gerät für eine automatische Registrierung](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) bei Azure Active Directory einrichten.  

-   Ihr E-Mail-Dienst muss aktiviert sein, damit die Exchange ActiveSync-ID des Geräts mit dem Gerätedatensatz in Azure Active Directory verknüpft wird (gilt nur für iOS- und Android-Geräte).  

-   Sie müssen mit allen bereitgestellten Kompatibilitätsrichtlinien kompatibel sein.  

 Der Gerätestatus wird in Azure Active Directory gespeichert. Die Anwendung gewährt oder blockiert den Zugriff auf E-Mails entsprechend den ausgewerteten Bedingungen.  

 Wenn eine Bedingung nicht erfüllt wird, erhält der Benutzer bei der Anmeldung eine der folgenden Meldungen:  

-   Wenn das Gerät nicht oder in Azure Active Directory registriert ist, wird eine Meldung mit Anweisungen zum Installieren der Unternehmensportal-App und zum Registrieren des Geräts angezeigt.  

-   Wenn das Gerät nicht kompatibel ist, wird eine Meldung angezeigt, die den Benutzer zum Intune-Unternehmensportal oder zur Unternehmensportal-App weiterleitet. Hier finden sie Informationen zum Problem und zu dessen Lösung.  

-   Für PCs:  

    -   Wenn die Richtlinie das Beitreten zu einer Domäne erfordert und der PC nicht in die Domäne eingebunden ist, wird die Meldung angezeigt, dass der IT-Administrator kontaktiert werden sollte.  

    -   Wenn die Richtlinie das Beitreten zu einer Domäne oder Kompatibilität erfordert und der PC keine der Anforderungen erfüllt, wird eine Meldung mit einer Anleitung zum Installieren der Unternehmensportal-App und zur Registrierung angezeigt.  

 Die Meldung wird für Exchange Online-Benutzer und Mandanten in der neuen Umgebung von Exchange Online Dedicated auf dem Gerät angezeigt. Auf Geräten, die Exchange lokal und ältere Exchange Online Dedicated-Umgebungen verwenden, wird sie zudem an den E-Mail-Posteingang gesendet.  

> [!NOTE]  
>  Mit den Regeln für den bedingten Zugriff von Configuration Manager werden in der Exchange Online-Verwaltungskonsole definierte Regeln überschrieben, zugelassen, blockiert und unter Quarantäne gestellt.  

> [!NOTE]  
>  Die Richtlinie für bedingten Zugriff muss in der Intune-Konsole konfiguriert werden. Die folgenden Schritte beginnen mit dem Zugriff auf die Intune-Konsole über den Configuration Manager. Wenn Sie dazu aufgefordert werden, melden Sie sich mit denselben Anmeldeinformationen an, die zum Einrichten des Dienstverbindungspunkts zwischen Configuration Manager und Intune verwendet wurden.  

##### <a name="to-enable-the-exchange-online-policy"></a>So aktivieren Sie die Exchange Online-Richtlinie  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie **Kompatibilitätseinstellungen**und **Bedingter Zugriff**, und klicken Sie dann auf **Exchange Online**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Links** auf **Richtlinie für bedingten Zugriff in der Intune-Konsole konfigurieren**. Sie müssen ggf. den Benutzernamen und das Kennwort des Kontos bereitstellen, das zum Verbinden von Configuration Manager mit einem beliebigen globalen Administrator für den Intune-Dienst verwendet wurde.  

     Die Intune-Verwaltungskonsole wird geöffnet.  

4.  Klicken Sie in der [Microsoft Intune-Verwaltungskonsole](https://manage.microsoft.com)auf **Richtlinie** > **Bedingter Zugriff** > **Exchange Online Richtlinie**.  

     ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5.  Aktivieren Sie auf der Seite **Exchange Online-Richtlinie** die Option **Bedingte Zugriffsrichtlinie für Exchange Online aktivieren**. Wenn Sie diese Option aktivieren, muss das Gerät kompatibel sein. Wenn diese Option nicht aktiviert ist, wird der bedingte Zugriff nicht angewendet.  

    > [!NOTE]  
    >  Wenn Sie keine Konformitätsrichtlinie bereitgestellt haben und dann die Exchange Online-Richtlinie aktivieren, werden alle Zielgeräte als konform gemeldet.  
    >   
    >  Unabhängig vom Kompatibilitätsstatus müssen alle Benutzer, denen die Richtlinie zugewiesen ist, ihre Geräte bei Intune registrieren.  

6.  Unter **Anwendungszugriff**können Sie für Outlook und andere Apps mit moderner Authentifizierung den Zugriff auf ausschließlich Geräte beschränken, die für jede Plattform kompatibel sind.  Windows-Geräte müssen entweder in die Domäne eingebunden oder in Intune registriert und kompatibel sein.  

    > [!TIP]  
    >  Die**moderne Authentifizierung** ermöglicht das ADAL-basierte (Active Directory Authentication Library) Anmelden für Office-Clients.  
    >   
    >  -   Die ADAL-basierte Authentifizierung ermöglicht Office-Clients die Einbindung in die browserbasierte Authentifizierung (auch als passive Authentifizierung bekannt).  Der Benutzer wird zur Authentifizierung zu einer Anmeldewebseite umgeleitet.  
    > -   Diese neue Anmeldemethode ermöglicht neue Szenarien, z. B. den bedingten Zugriff, auf Grundlage der **Gerätekompatibilität** und in Abhängigkeit davon, ob eine **mehrstufige Authentifizierung** erfolgt ist.  
    >   
    >  Dieser [Artikel](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) enthält ausführlichere Informationen zur Funktionsweise der modernen Authentifizierung.  

     Wenn Sie Exchange Online mit Configuration Manager und Intune verwenden, können Sie nicht nur mobile Geräte mit bedingtem Zugriff verwalten, sondern auch Desktopcomputer. PCs müssen entweder in die Domäne eingebunden oder in Intune registriert und kompatibel sein. Sie können die folgenden Anforderungen festlegen:  

    -   **Geräte müssen in eine Domäne eingebunden oder kompatibel sein.** PCs müssen entweder in die Domäne eingebunden oder mit den Richtlinien kompatibel sein. Wenn ein PC keine der Anforderungen erfüllt, wird der Benutzer aufgefordert, das Gerät bei Intune zu registrieren.  

    -   **Geräte müssen in eine Domäne eingebunden sein.** PCs müssen für den Zugriff auf Exchange Online in eine Domäne eingebunden sein. Wenn ein Computer in keine Domäne eingebunden ist, wird der E-Mail-Zugriff blockiert und der Benutzer aufgefordert, den IT-Administrator zu kontaktieren.  

    -   **Geräte müssen kompatibel sein.** PCs müssen bei Intune registriert und kompatibel sein. Wenn ein PC nicht registriert ist, wird eine Meldung mit Anweisungen zur Registrierung angezeigt.  

7.  Unter **Outlook Web Access (OWA)**können Sie Zugriff auf Exchange Online nur über die unterstützten Browser gewähren: Safari (iOS) und Chrome (Android). Der Zugriff über andere Browser wird blockiert. Die gleichen Plattformbeschränkungen, die Sie für den Anwendungszugriff für Outlook ausgewählt haben, gelten auch hier.

    Benutzer müssen auf **Android** -Geräten den Browserzugriff aktivieren.  Der Endbenutzer muss hierzu die Option „Browserzugriff aktivieren“ wie folgt auf dem registrierten Gerät aktivieren:
     1. Starten Sie die **Unternehmensportal-App**.
     2. Rufen Sie die Seite **Einstellungen** über die Schaltfläche mit den drei Punkten (…) oder über die physische Menütaste auf.
      3.    Drücken Sie die Schaltfläche **Browserzugriff aktivieren** .
      4.    Melden Sie sich im Chrome-Browser von Office 365 ab, und starten Sie Chrome erneut.

     Azure Active Directory führt ein TLS-Zertifikat (Transport Layer Security) auf dem Gerät aus, um auf **iOS und Android** -Plattformen das Gerät zu identifizieren, das für den Zugriff auf den Dienst verwendet wird.  Das Gerät zeigt das Zertifikat zusammen mit einer Aufforderung an den Endbenutzer an, der das Zertifikat auswählen muss, so wie in den folgenden Screenshots gezeigt. Der Endbenutzer muss dieses Zertifikat auswählen, bevor der Browser weiterhin verwendet werden kann.

     **iOS**

     ![Screenshot der Zertifikataufforderung auf einem iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Android**

    ![Screenshot der Zertifikataufforderung auf einem Android-Gerät](media/mdm-browser-ca-android-cert-prompt.png)

7.  Für**Exchange ActiveSync-E-Mail-Apps**können Sie E-Mails am Zugriff auf Exchange Online hindern, wenn das Gerät nicht kompatibel ist. Außerdem können Sie auswählen, ob der Zugriff auf E-Mail zugelassen oder blockiert wird, wenn Intune das Gerät nicht verwalten kann.  

8.  Wählen Sie unter **Zielgruppen**die Active Directory-Sicherheitsgruppen der Benutzer aus, auf die die Richtlinie angewendet wird.  

    > [!NOTE]  
    >  Für Benutzer in den Zielgruppen werden die Exchange-Regeln und -Richtlinien durch Intune-Richtlinien ersetzt.  
    >   
    >  Exchange erzwingt nur in den folgenden Situationen die Exchange-Regeln zum Zulassen, Blockieren und für die Quarantäne sowie Exchange-Richtlinien:  
    >   
    >  -   Der Benutzer ist nicht für Intune lizenziert.  
    > -   Der Benutzer ist für Intune lizenziert, gehört aber keiner Sicherheitsgruppe an, die in der Richtlinie für den bedingten Zugriff angegeben ist.  

9. Wählen Sie unter **Ausgenommene Gruppen**die Active Directory-Sicherheitsgruppen der Benutzer aus, die von dieser Richtlinie ausgenommen werden. Wenn ein Benutzer sowohl in den Zielgruppen als auch in den ausgenommenen Gruppen enthalten ist, wird er von der Richtlinie ausgenommen und hat Zugriff auf deren E-Mail.  

10. Wenn Sie fertig sind, klicken Sie auf **Speichern**.  

-   Die Richtlinie für bedingten Zugriff wird sofort wirksam und muss nicht explizit bereitgestellt werden.  

-   Nachdem ein Benutzer ein E-Mail-Konto erstellt hat, wird das Gerät sofort blockiert.  

-   Sobald ein blockierter Benutzer das Gerät bei Intune registriert (oder die Nichtkompatibilität behebt), wird der E-Mail-Zugriff innerhalb von 2 Minuten entsperrt.  

-   Wenn der Benutzer die Registrierung seines Geräts aufhebt, wird der E-Mail-Zugriff nach ca. 6 Stunden blockiert.  

### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Für Exchange lokal (und Mandanten in der älteren Exchange Online Dedicated-Umgebung)  
 Bei Richtlinien für bedingten Zugriff wird für Exchange lokal und Mandanten in der älteren Exchange Online Dedicated-Umgebung über den folgenden Ablauf bewertet, ob Geräten Zugriff erhalten.  

 ![ConditionalAccess8&#45;2](media/ConditionalAccess8-2.png)  

##### <a name="to-enable-the-exchange-on-premises-policy"></a>So aktivieren Sie die Richtlinie für lokales Exchange  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2.  Erweitern Sie **Kompatibilitätseinstellungen**und **Bedingter Zugriff**, und klicken Sie dann auf **Exchange lokal**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Exchange lokal** auf **Richtlinie für bedingten Zugriff konfigurieren**.  

4.  **Ab Version 1602 von Configuration Manager**können Sie auf der Seite **Allgemein** des **Assistenten zur Konfiguration der Richtlinie zum bedingten Zugriff**angeben, ob Sie die Exchange Active Sync-Standardregel außer Kraft setzen möchten. Aktivieren Sie diese Option, wenn Sie möchten, dass registrierte und kompatible Geräte stets Zugriff auf E-Mail haben, auch wenn die Standardregel auf Quarantäne oder Blockieren des Zugriffs festgelegt ist.  

    > [!NOTE]  
    >  Es gibt ein Problem mit der standardmäßigen Außerkraftsetzung für Android-Geräte. Wenn die Standardzugriffsregel des Exchange-Servers auf **Blockieren** festgelegt ist und die Exchange-Richtlinie für bedingten Zugriff mit der standardmäßigen Option zur Außerkraftsetzung der Regel aktiviert ist, wird die Blockierung der Android-Geräte der Zielbenutzer ggf. nicht aufgehoben, auch nachdem die Geräte bei Intune registriert wurden und kompatibel sind.  Zur Umgehung dieses Problem legen Sie die Exchange-Standardzugriffsregel auf **Quarantäne**fest. Das Gerät erhält nicht standardmäßig Zugriff auf Exchange. Der Administrator kann einen Bericht vom Exchange-Server mit der Liste der Geräte in Quarantäne abrufen.  

     Wenn Sie bei der Einrichtung des Exchange-Connectors kein Benachrichtigungs-E-Mail-Konto eingerichtet haben, wird eine Warnung auf dieser Seite angezeigt, und die Schaltfläche **Weiter** ist deaktiviert.  Bevor Sie fortfahren können, müssen Sie zunächst im Exchange-Connector die E-Mail-Benachrichtigungseinstellungen konfigurieren und dann zum **Assistenten zur Konfiguration der Richtlinie zum bedingten Zugriff** zurückkehren.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

     Klicken Sie auf **Weiter**.  

5.  Fügen Sie auf der Seite für **Zielsammlungen** mindestens eine Benutzersammlung hinzu. Für den Zugriff auf Exchange müssen Benutzer in diesen Sammlungen ihre Geräte bei Intune registrieren und zusätzlich die von Ihnen bereitgestellten Kompatibilitätsrichtlinien einhalten.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

     Klicken Sie auf **Weiter**.  

6.  Fügen Sie auf der Seite für **Ausgenommene Sammlungen** Benutzersammlungen hinzu, die von der Richtlinie für bedingten Zugriff ausgenommen werden sollen. Benutzer in diesen Gruppen müssen ihre Geräte nicht bei Intune registrieren und die bereitgestellten Kompatibilitätsrichtlinien nicht einhalten, um auf Exchange zuzugreifen.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

     Wenn ein Benutzer sowohl in der Zielliste als auch in der Ausnahmeliste enthalten ist, wird er aus der Richtlinie für den bedingten Zugriff ausgenommen.  

     Klicken Sie auf **Weiter**.  

7.  Konfigurieren Sie auf der Seite **Benutzerbenachrichtigung bearbeiten** die E-Mail, die Intune mit Anweisungen an Benutzer sendet, wie das Gerät entsperrt wird (und außerdem die von Exchange gesendete E-Mail).  

     Sie können die Standardnachricht bearbeiten und den Text mithilfe von HTML-Tags formatieren. Sie können auch eine E-Mail im Voraus an Ihre Mitarbeiter senden, in der diese über die bevorstehenden Änderungen informiert werden und Anleitungen für die Registrierung ihrer Geräte erhalten.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    >  Da die Benachrichtigungs-E-Mail von Intune mit den Lösungsanweisungen an das Exchange-Postfach des Benutzers gesendet wird, kann es vorkommen, dass das Gerät blockiert wird, bevor der Benutzer die E-Mail-Nachricht erhält. In diesem Fall besteht die Möglichkeit, die Nachricht über ein freigeschaltetes Gerät oder eine andere Exchange-Zugriffsmethode anzuzeigen.  

    > [!NOTE]  
    >  Damit die Benachrichtigungs-E-Mail in Exchange gesendet werden kann, müssen Sie das dafür verwendete Konto entsprechend konfigurieren. Dies geschieht, wenn Sie die Eigenschaften des Exchange Server-Connectors konfigurieren.  
    >   
    >  Weitere Informationen finden Sie unter [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

     Klicken Sie auf **Weiter**.  

8.  Überprüfen Sie auf der Seite  **Zusammenfassung** die Einstellungen, und schließen Sie dann den Assistenten ab.  

-   Die Richtlinie für bedingten Zugriff wird sofort wirksam und muss nicht explizit bereitgestellt werden.  

-   Nachdem ein Benutzer ein Exchange ActiveSync-Profil eingerichtet hat, kann es 1 bis 3 Stunden dauern, bis das Gerät blockiert wird (wenn es nicht von Intune verwaltet wird).  

-   Wenn ein blockierter Benutzer das Gerät anschließend bei Intune registriert (oder die Nichtkompatibilität behebt), wird der E-Mail-Zugriff innerhalb von zwei Minuten entsperrt.  

-   Wenn der Benutzer die Registrierung des Geräts bei Intune aufhebt, kann es 1 bis 3 Stunden dauern, bis das Gerät blockiert wird.  

### <a name="see-also"></a>Weitere Informationen:  
 [Verwalten des Zugriffs auf Dienste in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
