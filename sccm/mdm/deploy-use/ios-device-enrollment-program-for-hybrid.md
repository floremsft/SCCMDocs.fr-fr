---
title: "Registrieren von iOS-Geräten mit dem Programm zur Geräteregistrierung (DEP) – Configuration Manager | Microsoft-Dokumentation"
description: "Aktivieren der Registrierung des iOS-Programms zur Geräteregistrierung (Device Enrollment Program, DEP) für Hybridbereitstellungen in Configuration Manager mit Intune."
ms.custom: na
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
caps.latest.revision: "9"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e76e46ce0d6ee0582d5161709ff114b936ac5660
ms.sourcegitcommit: db7b7ec347638efd05cdba474e8a8f8535516116
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2017
---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>Registrierung des iOS-Programms zur Geräteregistrierung (Device Enrollment Program, DEP) für Hybridbereitstellungen mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Unternehmen können iOS-Geräte mit dem Geräteregistrierungsprogramm von Apple kaufen und diese dann mithilfe von Microsoft Intune verwalten. Zum Verwalten von firmeneigenen iOS-Geräten mit dem Apple-Programm zur Geräteregistrierung (DEP) müssen Unternehmen die erforderlichen Schritte bei Apple durchlaufen, um am Programm teilnehmen und darüber Geräte beziehen zu können. Details zu diesem Prozess finden Sie unter:  [https://deploy.apple.com](https://deploy.apple.com)verwaltet werden können. Das Programm bietet den Vorteil, dass Geräte eingerichtet werden können, ohne dass jedes Gerät physisch über USB mit einem Computer verbunden werden muss.  

 Damit Sie firmeneigene iOS-Geräte mit dem DEP registrieren können, benötigen Sie ein DEP-Token von Apple. Mit diesem Token kann Intune Informationen zu DEP-Geräten synchronisieren, die Ihrem Unternehmen gehören. Zudem ermöglicht es Intune das Hochladen von Registrierungsprofilen bei Apple und das Zuweisen von Geräten zu diesen Profilen.  

## <a name="apple-dep-enrollment-for-ios-devices"></a>Apple DEP-Registrierung für iOS-Geräte  
 Die folgenden Verfahren beschreiben, wie iOS-Geräte angegeben werden, die über Apple DEP als von Intune verwaltete, unternehmenseigene Geräte gekauft wurden. Beim ersten Hochfahren des Geräts erhält es das DEP-Verwaltungsprofil, führt den Setup-Assistenten aus und registriert die Geräte für die Verwaltung.  

##  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Aktivieren der DEP-Registrierung in Configuration Manager mit Intune  

1.  **Beginnen der Verwaltung von iOS-Geräten mit Configuration Manager**   
    Bevor Sie Geräte des iOS-Programms zur Geräteregistrierung (DEP) registrieren können, müssen Sie die Schritte im Thema [Set up Hybrid mobile device management (Einrichten der hybriden Verwaltung mobiler Geräte)](../../mdm/deploy-use/setup-hybrid-mdm.md), einschließlich der [Schritte zur Unterstützung der iOS-Registrierung](../deploy-use/enroll-hybrid-ios-mac.md) durchführen.
2.  **Erstellen einer DEP-Tokenanforderung**   
    Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** die Option **Hierarchiekonfiguration**, erweitern Sie **Clouddienste**, und klicken Sie anschließend auf **Microsoft Intune-Abonnements**. Klicken Sie auf der Registerkarte **Startseite** auf die Option **DEP-Tokenanforderung erstellen** , klicken Sie auf **Durchsuchen** , um den Downloadpfad für die DEP-Tokenanforderung anzugeben, und klicken Sie anschließend auf **Herunterladen**. Speichern Sie die PEM-Datei der DEP-Tokenanforderung lokal. Mithilfe der PEM-Datei wird ein vertrauenswürdiges Token (P7M) beim Portal des Apple-Programms zur Geräteregistrierung angefordert.  
3.  **Abrufen eines Device Enrollment Program-Tokens**   
    Rufen Sie das [Portal des Programms zur Geräteregistrierung](https://deploy.apple.com) (https://deploy.apple.com) auf, und melden Sie sich mit Ihrer geschäftlichen Apple-ID an. Diese Apple-ID muss später verwendet werden, um das DEP-Token zu erneuern.  
    1.  Erweitern Sie in der [Portal des Programms zur Geräteregistrierung](https://deploy.apple.com)zu **Programm zur Geräteregistrierung** > **Server verwalten**, und klicken Sie anschließend auf **MDM-Server hinzufügen**verwaltet werden können.  
    2.  Geben Sie den **Namen des MDM-Servers**, und klicken Sie anschließend auf **Weiter**verwaltet werden können. Der Servername dient als Referenz zum Identifizieren des MDM-Servers. Dies ist nicht der Name oder die URL des Intune- oder Configuration Manager-Servers.  
    3.  Das Dialogfeld **<Servername\> hinzufügen** wird geöffnet. Klicken Sie auf **Datei auswählen…** um die im vorherigen Schritt erstellte PEM-Datei hochzuladen, und klicken Sie dann auf **Weiter**verwaltet werden können.  
    4.  Im Dialogfeld **<Servername\> hinzufügen** wird der Link **Ihr Servertoken** angezeigt. Laden Sie die Servertokendatei (verwaltet werden können.p7m) auf Ihren Computer herunter, und klicken Sie anschließend auf **Fertig**verwaltet werden können.  

     Diese Zertifikatdatei (.p7m) wird verwendet, um eine Vertrauensstellung zwischen dem Intune-Server und dem Server des Apple-Programms zur Geräteregistrierung herzustellen.  
4.  **Hinzufügen der DEP-Tokenanforderung zu Configuration Manager**   
    Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** die Option **Hierarchiekonfiguration**, und klicken Sie auf **Microsoft Intune-Abonnements**. Klicken Sie auf der Registerkarte **Startseite** auf **Plattformen konfigurieren** , und klicken Sie auf **iOS**. Wählen Sie **Programm zur Geräteregistrierung aktivieren**aus, navigieren Sie zur Zertifikatsdatei (.p7m), klicken Sie auf **Öffnen**&gt; **Hochladen**und anschließend auf **OK**.  

## <a name="add-a-corporate-device-enrollment-policy"></a>Hinzufügen einer Richtlinie für die Unternehmensgeräteregistrierung  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Bestand und Kompatibilität** die Option **Übersicht**, erweitern Sie **Alle Unternehmensgeräte**, erweitern Sie **iOS**, und klicken Sie anschließend auf **Registrierungsprofile**. Klicken Sie auf der Registerkarte **Startseite** auf **Profil erstellen** , um den Assistenten zum Erstellen von Profilen zu öffnen. Konfigurieren Sie die Einstellungen auf den folgenden Seiten:  
2. On the **Allgemein** die folgenden Informationen an, und klicken Sie anschließend auf **Weiter**verwaltet werden können.  
  -   **Name:** Name des Geräteregistrierungsprofils. (Für Benutzer nicht sichtbar)  
  -   **Beschreibung** : Beschreibung des Geräteanmeldungsprofils. (Für Benutzer nicht sichtbar)  
  -   **Benutzeraffinität:** Gibt an, wie Geräte registriert werden. Informationen finden Sie unter [User affinity for hybrid managed devices in Configuration Manager (Benutzeraffinität für hybridverwaltete Geräte in Configuration Manager)](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

      -  **Eingabeaufforderung für Benutzeraffinität:**Das Gerät muss während der ersten Setup einem Benutzer zugewiesen werden und kann dann berechtigt sein, im Namen dieses Benutzers auf Unternehmensdaten und E-Mails zuzugreifen.  Benutzeraffinität muss für von DEP verwaltete Geräte konfiguriert werden, die Benutzern gehören und das Unternehmensportal verwenden müssen (um beispielsweise Apps zu installieren).  
      > [!NOTE]
      > Für DEP mit Benutzeraffinität muss AD FS WS-Trust 1.3 Username/Mixed endpoint (AD FS WS-Trust 1.3 Benutzername/gemischter Endpunkt) aktiviert sein, damit ein Benutzertoken angefordert wird.

      -   **Keine Benutzeraffinität:**Das Gerät ist keinem Benutzer zugeordnet. Verwenden Sie diese Zuweisung für Geräte, die Aufgaben ohne den Zugriff auf lokale Benutzerdaten ausführen. Apps, die eine Benutzerzuweisung erfordern, funktionieren nicht.  
    ![Screenshot des DEP-Profilnamens, der Beschreibung und der Eingabeaufforderung „Benutzeraffinität“](../media/dep-general.png)

3. Geben Sie auf der Seite **Einstellungen des Programms zur Geräteregistrierung** die folgenden Informationen an, und klicken Sie anschließend auf **Weiter**.  
    -   **Department**: Diese Information erscheint, wenn Benutzer während der Aktivierung auf „About Configuration“ (Konfiguration) tippen.  
    -   **Telefonnummer des Supports**: Wird angezeigt, wenn der Benutzer während der Aktivierung auf die Schaltfläche **Benötigen Sie Hilfe?** tippt.
       ![Screenshot der Zuweisung des DEP-Profils für iOS-Geräte](../media/dep-settings.png)

    - **Vorbereitungsmodus**: Dieser Status wird während der Aktivierung festgelegt und kann nicht geändert werden, ohne das Gerät auf Werkseinstellungen zurückzusetzen:  
        -   **Nicht überwacht** – Eingeschränkte Verwaltungsfunktionen  
        -   **Überwacht** – Aktiviert mehr Verwaltungsoptionen und deaktiviert standardmäßig die Aktivierungssperre  
    - **Registrierungsprofil für das Gerät sperren**: Dieser Status wird während der Aktivierung festgelegt und kann nicht geändert werden, ohne das Gerät auf Werkseinstellungen zurückzusetzen.  
      -   **Deaktivieren** – Das Verwaltungsprofil kann aus dem Menü **Einstellungen** entfernt werden.  
      -   **Aktivieren** – (Erfordert **Preparation Mode** (Vorbereitungsmodus) = **Supervised** (Überwacht)) Deaktiviert iOS-Einstellungen, die die Entfernung des Verwaltungsprofils erlauben könnten.  

4.  Konfigurieren Sie auf der Seite **Setup-Assistent** die Einstellungen, die den iOS-Setup-Assistenten anpassen, der gestartet wird, wenn das Gerät erstmalig eingeschaltet wird, und klicken Sie anschließend auf **Weiter**. Zu diesen Einstellungen zählen:  
  -   **Kennung** – Aufforderung zur Eingabe der Kennung während der Aktivierung. Fordern Sie immer eine Kennung an, es sei denn, das Gerät wird gesichert oder der Zugriff wird auf andere Weise verwaltet (z.B. der Kioskmodus, der das Gerät auf eine App beschränkt).  
  -   **Standortdienste** – Falls aktiviert, fragt der Setup-Assistent ab, ob der Diensts aktiviert werden soll.  
  -   **Wiederherstellung** – Falls aktiviert, fordert der Setup-Assistent die iCloud-Sicherung während der Aktivierung auf  
  -   **Apple-ID** – Für den Download von Apps aus dem iOS App Store, einschließlich der Apps, die von Intune installiert werden, ist eine Apple-ID erforderlich. Wenn aktiviert, fordert iOS Benutzer auf, eine Apple-ID bereitzustellen, wenn Intune eine App ohne eine ID installieren möchte.  
  -   **Geschäftsbedingungen** – Wenn aktiviert, fordert der Setup-Assistent Benutzer auf, die Geschäftsbedingungen Apple während der Aktivierung zu akzeptieren  
  -   **Touch ID**: Falls aktiviert, fordert der Setup-Assistent zur Ausführung dieses Dienst während der Aktivierung auf.
  -   **Apple Pay**: Falls aktiviert, fordert der Setup-Assistent zur Ausführung dieses Dienst während der Aktivierung auf.
  -   **Zoom**: Falls aktiviert, fordert der Setup-Assistent zur Ausführung dieses Dienst während der Aktivierung auf.
  -   **Siri** – Falls aktiviert, fordert der Setup-Assistent zur Ausführung dieses Dienst während der Aktivierung auf  
  -   **Diagnosedaten an Apple senden** – Falls aktiviert, fordert der Setup-Assistent zur Ausführung dieses Dienst während der Aktivierung auf  
    ![Screenshot der Zuweisung des DEP-Profils für iOS-Geräte](../media/dep-setup-assistant.png)
5.  Geben Sie auf der Seite **Additional Management** (Zusatzverwaltung) an, ob eine USB-Verbindung für die Einstellungen der Zusatzverwaltung verwendet werden kann. Wenn Sie die Option **Require certificate**auswählen, müssen Sie ein Apple Configurator-Verwaltungszertifikat für die Verwendung dieses Profil importieren.  Legen Sie die Option auf **Nicht zulassen** fest, um die Synchronisierung von Dateien mit iTunes oder die Verwaltung über Apple Configurator zu verhindern. Microsoft empfiehlt Ihnen, die Einstellung **Nicht zulassen** zu verwenden, weitere Konfigurationen von Apple Configurator zu exportieren und die Bereitstellung als benutzerdefiniertes iOS-Konfigurationsprofil durchzuführen, anstatt diese Einstallung zu verwenden, um die manuelle Bereitstellung mit oder ohne einem Zertifikat zuzulassen.  

  -   **Nicht zulassen** – Hindert das Gerät daran, über USB zu kommunizieren (verhindert Kopplung)  
  -   **Zulassen** – Lässt zu, dass Geräte über eine USB-Verbindung mit jedem beliebigen PC oder Macintosh-Computer kommunizieren  
  -   **Zertifikat erfordern** – Lässt die Kopplung mit einem Mac mit einem Zertifikat zu, das in das Anmeldungsprofil importiert wurde  

## <a name="assign-dep-devices-for-management"></a>Zuweisen von DEP-Geräten zur Verwaltung

1. Rufen Sie das [Portal des Programms zur Geräteregistrierung](https://deploy.apple.com) (https://deploy.apple.com) auf, und melden Sie sich mit Ihrer geschäftlichen Apple-ID an.
2. Wechseln Sie zu **Bereitstellungsprogramm** > **Programm zur Geräteregistrierung** > **Geräte verwalten**verwaltet werden können. Geben Sie alle erforderlichen Informationen bei **Choose Devices**(Geräte wählen) an, fügen Sie Geräteinformationen hinzu, und geben Sie die Gerätedetails wie die **Seriennummer**und **Bestellnummer**an, oder laden Sie über **Upload CSV File**eine CSV-Datei hoch. Wählen Sie als Nächstes **Zu Server zuweisen** aus. Wählen Sie den in Schritt 3 angegebenen <*Servernamen*> aus, und klicken Sie dann auf **OK**.  

3.  **Synchronisieren von DEP-verwalteten Geräten**   
    Navigieren Sie im Arbeitsbereich **Bestand und Kompatibilität** zu **Alle unternehmenseigenen Geräte** > **Vorab deklarierte Geräte**. Klicken Sie auf der Registerkarte **Startseite** auf **DEP-Synchronisierung**. Eine Synchronisierungsanforderung wird an Apple gesendet. Nach Abschluss der Synchronisierung werden die DEP-verwalteten Geräte angezeigt.

    > [!NOTE]
    > In der Hybridkonfiguration wird der DEP-Synchronisierungsvorgang manuell durch Klicken auf **DEP-Synchronisierung** in der Configuration Manager-Konsole ausgelöst.

4.  **Zuweisen des DEP-Profils**<br>Navigieren Sie im Arbeitsbereich **Bestand und Kompatibilität** zu **Alle unternehmenseigenen Geräte** > **iOS** > **Registrierungsprofile**. Wählen Sie das DEP-Registrierungsprofil aus, und klicken Sie dann auf der Registerkarte **Startseite** auf **Geräten zuweisen**. Wählen Sie die Geräte aus, die dieses Registrierungsprofil verwenden sollen, klicken Sie auf **Hinzufügen**, und klicken Sie dann auf **OK**.   
     ![Screenshot der Zuweisung des DEP-Profils für iOS-Geräte](../media/dep-assign-profile.png)

## <a name="distribute-devices-to-users"></a>Verteilen von Geräten an Benutzer
Ihre firmeneigenen Geräte können jetzt an Benutzer verteilt werden. Das Dialogfeld **Registrierungsstatus** für verwaltete Geräte lautet **Nicht kontaktiert** , bis das Gerät eingeschaltet und der Setup-Assistent zum Registrieren des Geräts darauf ausgeführt wird. Wenn ein iOS-Gerät eingeschaltet wird, wird es für die Verwaltung durch Intune registriert.
