---
title: Bereitstellen von Lookout for Work-Apps | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Lookout for Work-Apps.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 59f43c922d1d3bc64625733014b0def1e42c4d2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Konfigurieren und Bereitstellen von Lookout for Work-Apps

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieser Artikel beschreibt das Konfigurieren und Bereitstellen der Lookout for Work-App für Android und iOS-Geräte.

## <a name="android-google-play-store-app"></a>Android (Google Play Store-App)
1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen**.

2.  Geben Sie im Assistenten zum Bereitstellen von Software auf der Seite **Allgemein** die folgenden Informationen an:
  * Typ: Wählen Sie **App-Paket für Android in Google Play**
  * Speicherort: Kopieren Sie den Link der Lookout for Work-App aus dem Google Play Store, und fügen Sie ihn hier ein
  * Herausgeber: Lookout Mobile Security
  * Name: Lookout for Work
  * Beschreibung: Lookout bietet den besten Schutz vor mobilen Bedrohungen, damit Ihr Gerät sicher bleibt. Nach der Installation auf Ihrem Gerät schützt Lookout for Work Ihr Gerät vor Bedrohungen und warnt Sie und den Administrator Ihres Unternehmens, sobald welche gefunden werden.
  * Verwaltungskategorie: Verwalten von Computern

  Nach dem erfolgreichen Abschluss sehen Sie die Lookout for Work-App in der Liste der Programme.

3.  Wählen Sie auf der Registerkarte **Home** in der Gruppe **Bereitstellung** **Bereitstellen** aus, um die Lookout for Work App für Benutzer bereitzustellen.
>[!IMPORTANT]
>Sie müssen dieselben Benutzer auswählen, die der Option „Registrierungsverwaltung“ in der Lookout-MTP-Konsole hinzugefügt wurden.

  Wählen Sie die Option **Erforderliche Installation** aus, damit die Lookout-App auf dem Gerät des Benutzers installiert wird.

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (Enterprise-signierte Version der Lookout-App)

* **Schritt 1:** Stellen Sie sicher, dass **iOS-Verwaltung** auf Ihrem Gerät eingerichtet ist. Eine Anleitung zum Einrichten des Geräts für die iOS-Verwaltung finden Sie unter [Einrichten der iOS- und Mac-Geräteverwaltung]().

* **Schritt 2:** **Signieren** Sie die Lookout for Work iOS-App erneut. Lookout verteilt seine Lookout for Work iOS-App außerhalb des iOS App Store. **Bevor Sie die App verteilen**, müssen Sie die App mit Ihrem iOS Enterprise Developer Certificate neu signieren. Ausführliche Anweisungen zum erneuten Signieren der Lookout for Work iOS-Apps finden Sie unter [Lookout for Work iOS app re-signing process (Lookout for Work iOS-App-Re-Signing-Prozess)](https://personal.support.lookout.com/hc/en-us/articles/114094038714) auf der Lookout-Website.


* **Schritt 3:** Aktivieren Sie die Azure Active Directory-Authentifizierung für die iOS-Benutzer wie folgt:
  1.  Melden Sie sich im [Azure Active Directory-Verwaltungsportal](https://manage.windowsazure.com) an und navigieren Sie zur Anwendungsseite.
  2.  Fügen Sie die **Lookout for Work iOS-App** als eine **native Clientanwendung** hinzu.
  ![Screenshot des Dialogfelds Apps hinzufügen mit der Option native Clientanwendung](media/aad-add-app.png)

  3. Ersetzen Sie **com.lookout.enterprise.yourcompanyname** mit der Kundenbundle-ID, die Sie beim Unterzeichnen der IPA ausgewählt haben.
  4.  Hinzufügen von zusätzlichen Umleitungs-URI:  **&lt;companyportal://code/>** gefolgt von einer URL-codierten Version Ihrer ursprünglichen URI-Umleitung.
  5.  Fügen Sie **Delegierte Berechtigungen** zu Ihrer App hinzu.

  Weitere Informationen finden Sie unter [Konfigurieren einer nativen Clientanwendung](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).


* **Schritt 4:** Laden Sie die erneut signierte IPA-Datei wie im Thema [Erstellen von iOS-Anwendungen in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications) beschrieben hoch. Legen Sie die Mindestversion des Betriebssystems auf iOS 8.0 oder höher fest.


* **Schritt 5:** Erstellen Sie die Konfigurationsrichtlinie für verwaltete Anwendungen, wie im Thema [Configure iOS apps with mobile app configuration policies in System Center Configuration Manager (Konfigurieren von iOS-Apps mit den Konfigurationsrichtlinien für mobile Apps in System Center Configuration Manager)](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) beschrieben.


* **Schritt 6:** **Um die App für Benutzer bereitzustellen**, wählen Sie auf der Seite **Applikationen** die Lookout for Work-App aus. Wählen Sie auf der Registerkarte **Home** in der Gruppe **Bereitstellung** **Bereitstellen** aus.

  Sie müssen dieselben Benutzer auswählen, die der Option „Registrierungsverwaltung“ in der Lookout-Konsole hinzugefügt wurden.  
Wählen Sie die Option **Erforderliche Installation** aus, damit die Lookout-App auf dem Gerät des Benutzers installiert wird.

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>Was geschieht, wenn die bereitgestellte App auf dem Gerät geöffnet ist




Wenn der Benutzer Lookout for Work auf dem Gerät öffnet, wird er aufgefordert, die App zu aktivieren. Wählen Sie die Option „Bei Azure Active Directory anmelden“ aus. Eine ausführliche exemplarische Vorgehensweise für Endbenutzer finden Sie in den folgenden Themen:

* [Sie werden zur Installation von Lookout for Work auf Ihrem Android-Gerät aufgefordert](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [Sie müssen eine Bedrohung beheben, die Lookout for Work auf Ihrem Android-Gerät gefunden hat](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>Nächste Schritte
* [Aktivieren einer Regel zum Schutz vor Gerätebedrohungen in der Konformitätsrichtlinie](enable-device-threat-protection-rule-compliance-policy.md)
