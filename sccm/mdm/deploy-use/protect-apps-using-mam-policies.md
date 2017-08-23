---
title: "Schützen von Apps mithilfe Verwaltungsrichtlinien für mobile Anwendungen | Microsoft-Dokumentation"
description: "Ändern der Funktionalität von bereitgestellten Apps, damit sie den Kompatibilitäts- und Sicherheitsrichtlinien Ihres Unternehmens entsprechen."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28115475-e563-4e16-bf30-f4c9fe704754
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 50c137f159b0ef631f7173b8eec190182ce41cee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Schützen von Apps mithilfe von Verwaltungsrichtlinien für mobile Anwendungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit den Richtlinien für die Anwendungsverwaltung können Sie in System Center Configuration Manager die Funktionalität von Apps ändern, die Sie bereitstellen, um sie mit den Konformitäts- und Sicherheitsrichtlinien Ihres Unternehmens in Einklang zu bringen. Sie können z.B. Ausschneide-, Kopier- und Einfügevorgänge innerhalb einer eingeschränkten App einschränken oder eine App so konfigurieren, dass alle URLs in einem Managed Browser geöffnet werden. Anwendungsverwaltungsrichtlinien unterstützen Folgendes:  

-   Geräte unter Android 4 und höher  

-   Geräte unter iOS 7 und höher  

Ferner können Sie Verwaltungsrichtlinien für mobile Apps auch zum Schutz von Apps auf Geräten verwenden, die nicht von Intune verwaltet werden. Mit dieser neuen Funktion können Sie Verwaltungsrichtlinien für mobile Apps auf Apps anwenden, die eine Verbindung zu Office 365-Diensten herstellen. Diese Funktion wird nicht für Apps unterstützt, die die Verbindung zu lokalen Exchange- oder SharePoint-Diensten herstellen.  

Um diese neue Funktion zu verwenden, müssen Sie das Azure-Vorschauportal verwenden. Die folgenden Themen können Ihnen bei den ersten Schritten helfen:  
-   [Erste Schritte mit Verwaltungsrichtlinien für mobile Apps im Azure-Portal](https://technet.microsoft.com/library/mt627830.aspx)  
-   [Erstellen und Bereitstellen von Verwaltungsrichtlinien für mobile Apps mit Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

 Im Gegensatz zu Konfigurationselementen und -baselines in Configuration Manager wird eine Richtlinie für die Anwendungsverwaltung nicht direkt bereitgestellt. Stattdessen verknüpfen Sie die Richtlinie mit dem Anwendungsbereitstellungstyp, den Sie einschränken möchten. Wenn der App-Bereitstellungstyp bereitgestellt wird und auf Geräten installiert ist, werden die von Ihnen angegebenen Einstellungen wirksam.  

Zum Anwenden von Einschränkungen auf eine App muss die App das Microsoft Intune App Software Development Kit (SDK) enthalten. Es gibt zwei Möglichkeiten, um diesen App-Typ zu beziehen:  

-   **Verwenden einer richtlinienverwalteten App** (Android und iOS): Diese Apps verfügen über das integrierte App SDK. Um diesen App-Typ hinzuzufügen, geben Sie in einem App Store wie iTunes Store oder Google Play einen Link zur App an. Es ist keine weitere Bearbeitung für diesen App-Typ erforderlich. Eine Liste der richtlinienverwalteten Apps, die für IOS- und Android-Geräte verfügbar sind, finden Sie unter [Verwaltete Apps für Microsoft Intune-Verwaltungsrichtlinien für mobile Anwendungen](https://technet.microsoft.com/library/dn708489.aspx).  

-   **Verwenden einer „umschlossenen“ App** (Android und iOS): Diese Apps werden mit dem **Microsoft Intune App Wrapping Tool**neu gepackt, sodass sie das App SDK enthalten. Dieses Tool wird normalerweise verwendet, um Unternehmensanwendungen zu verarbeiten, die intern erstellt wurden. Es kann nicht verwendet werden, um Apps zu verarbeiten, die aus dem App Store heruntergeladen wurden. Weitere Informationen finden Sie in den folgenden Artikeln:
    - [Vorbereiten von iOS-Apps für die Verwaltung mobiler Anwendungen mit dem Intune App Wrapping Tool](https://technet.microsoft.com/library/dn878028.aspx)

    - [Vorbereiten von Android-Apps für die Verwaltung von mobilen Anwendungen mit dem Intune App Wrapping Tool](https://technet.microsoft.com/library/mt147413.aspx)  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Erstellen und Bereitstellen einer App mit einer Verwaltungsrichtlinie für mobile Anwendungen  

##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Schritt 1: Abrufen des Links zu einer richtlinienverwalteten App oder Erstellen einer umschlossenen App  

-   **So rufen Sie einen Link zu einer richtlinienverwalteten App ab**: Suchen Sie im App Store die URL der richtlinienverwalteten App, die Sie bereitstellen möchten, und notieren Sie sie.  

     Die URL der Microsoft Word für iPad-App ist beispielsweise **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  

-   **So erstellen Sie eine umschlossene App**: Verwenden Sie die Informationen in den Themen [Vorbereiten von iOS-Apps für die Verwaltung mobiler Anwendungen mit dem Intune App Wrapping Tool](https://technet.microsoft.com/library/dn878028.aspx) und [Vorbereiten von Android-Apps für die Verwaltung von mobilen Anwendungen mit dem Intune App Wrapping Tool](https://technet.microsoft.com/library/mt147413.aspx), um eine umschlossene App zu erstellen.  

     Das Tool erstellt eine verarbeitete App und eine zugehörige Manifestdatei. Sie verwenden diese Dateien beim Erstellen einer Configuration Manager-Anwendung, in der die App enthalten ist.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Schritt 2: Erstellen einer Configuration Manager-Anwendung, in der eine App enthalten ist  
 Die Vorgehensweise zum Erstellen der Configuration Manager-Anwendung hängt davon ab, ob Sie eine richtlinienverwaltete App (externer Link) verwenden oder eine App, die mit dem Microsoft Intune App Wrapping Tool für iOS (App-Paket für iOS) erstellt wurde. Verwenden Sie eines der folgenden Verfahren, um die Configuration Manager-Anwendung zu erstellen.  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Anwendung erstellen** aus, um den Assistenten zum **Erstellen von Anwendungen** zu öffnen.  

4.  Wählen Sie auf der Seite **Allgemein** die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen**aus.  

5.  Wählen Sie in der Dropdownliste **Typ** die Option **App package for iOS (\*.ipa file)** (iOS-App-Paketdatei (*.ipa)) aus.  

6.  Wählen Sie **Durchsuchen** aus, um das zu importierende App-Paket auszuwählen, und wählen Sie dann **Weiter** aus.  

7.  Geben Sie auf der Seite **Allgemeine Informationen** die Beschreibung und Kategorieinformationen ein, die Benutzern im Unternehmensportal angezeigt werden sollen.  

8.  Schließen Sie den Assistenten ab.  

 Die neue Anwendung wird im Knoten **Anwendungen** des Arbeitsbereichs **Softwarebibliothek** angezeigt.  

### <a name="create-an-application-that-contains-a-link-to-a-policy-managed-app"></a>Erstellen einer Anwendung mit einem Link zu einer richtlinienverwalteten App  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Anwendung erstellen** aus, um den Assistenten zum **Erstellen von Anwendungen** zu öffnen.  

4.  Wählen Sie auf der Seite **Allgemein** die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen**aus.  

5.  Wählen Sie in der Dropdownliste **Typ** eine der folgenden Optionen aus:  

    -   Für iOS: **App-Paket für iOS aus App Store**  

    -   Für Android: **App-Paket für Android in Google Play**  

6.  Geben Sie die URL für die App (aus Schritt 1) ein, und wählen Sie dann **Weiter** aus.  

7.  Geben Sie auf der Seite **Allgemeine Informationen** die Beschreibung und Kategorieinformationen ein, die Benutzern im Unternehmensportal angezeigt werden sollen.  

8.  Schließen Sie den Assistenten ab.  

 Die neue Anwendung wird im Knoten **Anwendungen** des Arbeitsbereichs **Softwarebibliothek** angezeigt.  

##  <a name="step-3-create-an-application-management-policy"></a>Schritt 3: Erstellen einer Anwendungsverwaltungsrichtlinie  
 Als Nächstes erstellen Sie eine Anwendungsverwaltungsrichtlinie, die Sie der Anwendung zuordnen. Sie können eine Richtlinie vom Typ "Allgemein" oder "Verwalteter Browser" erstellen.  

1)  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Richtlinien zur Anwendungsverwaltung** aus.  

2)  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Create Application Management Policy** (Anwendungsverwaltungsrichtlinie erstellen) aus.  

3)  Geben Sie auf der Seite **Allgemein** den Namen und die Beschreibung für die Richtlinie ein, und wählen Sie dann **Weiter** aus.  

4)  Wählen Sie auf der Seite **Richtlinientyp** die Plattform und den Richtlinientyp für diese Richtlinie aus, und wählen Sie dann **Weiter** aus. Die folgenden Richtlinientypen sind verfügbar:  

-   **Allgemein**: Mit dem Richtlinientyp „Allgemein“ können Sie die Funktionalität bereitgestellter Apps ändern, um sie an die Konformitäts- und Sicherheitsrichtlinien Ihres Unternehmens anzupassen. Sie können z. B. Ausschneide-, Kopier- und Einfügevorgänge innerhalb einer eingeschränkten App einschränken.  

-   **Managed Browser**: Mit der Richtlinie „Managed Browser“ können Sie festlegen, ob das Öffnen einer Liste von URLs durch den Managed Browser zugelassen oder blockiert werden soll. Mit dem Richtlinientyp "Verwalteter Browser" können Sie die Funktionalität der Intune Managed Browser-App ändern. Dies ist ein Webbrowser, mit dem Sie die von Benutzern ausführbaren Aktionen verwalten können. Legen Sie beispielsweise fest, welche Websites sie besuchen können und wie Links zu Inhalten innerhalb des Browsers geöffnet werden. Erfahren Sie mehr über die  [Intune Managed Browser-App für iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) und die [Intune Managed Browser-App für Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

5)  Konfigurieren Sie auf der Seite **iOS-Richtlinie** oder **Android-Richtlinie** die folgenden Werte nach Bedarf, und wählen Sie dann **Weiter** aus. Die Optionen unterscheiden sich je nach Gerätetyp, für den Sie die Richtlinie konfigurieren.  

|Wert|Weitere Informationen|  
|-----------|----------------------|  
|**Einschränken von anzuzeigenden Webinhalten in einem unternehmensverwalteten Browser**|Alle Links in der App können im Managed Browser geöffnet werden. Sie müssen diese App auf Geräten bereitstellen, damit diese Option funktioniert.|  
|**Verhindern von Android-Sicherungen** oder **Verhindern von iTunes- und iCloud-Sicherungen**|Deaktiviert die Sicherung von Informationen aus der App.|  
|**App Übertragung von Daten an andere Apps erlauben**|Gibt die Apps an, denen diese App Daten senden kann. Sie können auswählen, die Datenübertragung an beliebige Apps nicht zu erlauben, nur die Übertragung an andere eingeschränkte Apps zu erlauben oder die Übertragung an beliebige Apps zuzulassen.<br /><br /> Um für iOS-Geräte den Austausch von Dokumenten zwischen verwalteten und nicht verwalteten Apps zu verhindern, müssen Sie eine Sicherheitsrichtlinie für mobile Geräte konfigurieren und bereitstellen, die die Einstellung **Verwaltete Dokumente in anderen nicht verwalteten Apps zulassen**deaktiviert.<br /><br /> Bei Zulassung der Übertragung nur an andere eingeschränkte Apps werden die Intune PDF- und Image-Viewer (sofern bereitgestellt) verwendet, um den Inhalt der jeweiligen Typen zu öffnen.|  
|**App Empfang von Daten aus anderen Apps erlauben**|Gibt die Apps an, von denen diese App Daten empfangen kann. Sie können auswählen, die Datenübertragung von beliebigen Apps nicht zu erlauben, nur die Übertragung von anderen eingeschränkten Apps zu erlauben oder die Übertragung von beliebigen Apps zuzulassen.|  
|**"Speichern unter" verhindern**|Deaktiviert die Verwendung der Option **Speichern unter** in jeder App, die diese Richtlinie verwendet.|  
|**Beschränken von Ausschneiden, Kopieren und Einfügen mit anderen Apps**|Gibt an, wie Ausschneiden, Kopieren und Einfügen mit der App verwendet werden kann. Wählen Sie aus:<br /><br /> **Blockiert**: Ausschneiden, Kopieren und Einfügen zwischen dieser App und anderen Apps sind nicht zugelassen.<br /><br /> **Richtlinienverwaltete Apps**: Ausschneiden, Kopieren und Einfügen zwischen dieser App und anderen eingeschränkten Apps sind zugelassen.<br /><br /> **Richtlinienverwaltete Apps mit Einfügen**: Ermöglicht das Einfügen von aus dieser App ausgeschnittenen oder kopierten Daten nur in andere eingeschränkte Apps. Das Einfügen der aus beliebigen Apps ausgeschnittenen oder kopierten Daten in diese App wird zugelassen.<br /><br /> **Jede App**: Keine Einschränkungen beim Ausschneiden, Kopieren und Einfügen in diese oder aus dieser App.|  
|**Einfache PIN für Zugriff erforderlich**|Der Benutzer muss eine PIN eingeben, um die App zu verwenden. Benutzer werden aufgefordert, diese beim ersten Ausführen der App festzulegen.|  
|**Anzahl der Versuche vor dem Zurücksetzen der PIN**|Gibt die Anzahl der möglichen PIN-Eingabeversuche an, bevor der Benutzer die PIN zurücksetzen muss.|  
|**Unternehmensanmeldeinformationen für Zugriff erforderlich**|Erfordert, dass der Benutzer die Unternehmensanmeldeinformationen eingeben muss, bevor er auf die Anwendung zugreifen kann.|  
|**Gerätekonformität mit Unternehmensrichtlinien für Zugriff erforderlich**|Lässt die Verwendung der App nur dann zu, wenn das Gerät nicht per Jailbreak oder Rooting manipuliert wurde.|  
|**Überprüfen der Zugriffsanforderungen nach (Minuten)**|Gibt (im Feld **Timeout**) den Zeitraum an, bevor die Zugriffsanforderungen für die App nach dem Starten der App erneut geprüft werden müssen.<br /><br /> Wenn das Gerät offline ist, wird im Feld **Offlinetoleranzperiode** der Zeitraum angegeben, bevor die Zugriffsanforderungen für die App erneut geprüft werden.|  
|**App-Daten verschlüsseln**|Gibt an, dass alle mit dieser App verknüpften Daten verschlüsselt werden, einschließlich extern gespeicherter Daten (wie z.B. Daten auf SD-Karten).<br /><br /> **Verschlüsselung für iOS**<br /><br /> Bei Apps, die einer Configuration Manager-Verwaltungsrichtlinie für mobile Anwendungen zugeordnet sind, werden Daten im Ruhezustand mit vom Betriebssystem bereitgestellter Verschlüsselung auf Geräteebene verschlüsselt. Dies wird durch eine Geräte-PIN-Richtlinie aktiviert, die vom IT-Administrator festgelegt werden muss. Wenn eine PIN erforderlich ist, werden die Daten gemäß den Einstellungen in der Richtlinie für die Verwaltung mobiler Anwendungen verschlüsselt. Wie in der Apple-Dokumentation angegeben, [sind die von iOS 7 verwendeten Module FIPS 140-2-zertifiziert](http://support.apple.com/en-us/HT202739).<br /><br /> **Verschlüsselung für Android**<br /><br /> Bei Apps, die einer Configuration Manager-Verwaltungsrichtlinie für mobile Anwendungen zugeordnet sind, wird die Verschlüsselung von Microsoft bereitgestellt. Daten werden während der E/A-Dateivorgänge gemäß der Einstellung in der mobilen Anwendungsverwaltungsrichtlinie synchron verschlüsselt. Verwaltete Apps auf Android verwenden AES-128-Verschlüsselung im CBC-Modus mit den Plattform-Kryptografie-Bibliotheken. Die Verschlüsselungsmethode ist nicht FIPS 140-2-zertifiziert. Inhalt im Speicher des Geräts wird immer verschlüsselt.|  
    |**Blockieren von Bildschirmaufnahmen** (nur Android-Geräte)|Gibt an, dass die Screen Capture-Funktionen des Geräts blockiert werden, wenn Sie diese App verwenden.|  

6)  Wählen Sie auf der Seite **Managed Browser** aus, ob der Managed Browser nur URLs in der Liste öffnen darf oder ob das Öffnen der URLs in der Liste durch den Managed Browser blockiert ist. Wählen Sie dann **Weiter** aus.  
Weitere Informationen finden Sie unter [Manage Internet access using managed browser policies (Verwalten des Internetzugriffs mit Richtlinien für Managed Browser)](manage-internet-access-using-managed-browser-policies.md).  

7)  Schließen Sie den Assistenten ab.  

 Die neue Richtlinie wird im Knoten **Anwendungsverwaltungsrichtlinien** des Arbeitsbereichs **Softwarebibliothek** angezeigt.  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Schritt 4: Zuordnen der Anwendungsverwaltungsrichtlinie zu einem Bereitstellungstyp  

 Wenn ein Bereitstellungstyp für eine App erstellt wird, die eine Richtlinie für die Anwendungsverwaltung erfordert, erkennt Configuration Manager dies und fordert Sie auf, eine Richtlinie für die Anwendungsverwaltung zuzuordnen. Für den Managed Browser müssen Sie sowohl eine Richtlinie „Allgemein“ als auch eine Richtlinie „Managed Browser“ zuordnen. Weitere Informationen finden Sie unter [Erstellen von Anwendungen](create-applications.md).  

> [!IMPORTANT]  
>  Wenn die Anwendung bereits bereitgestellt ist, tritt bei der Bereitstellung für den neuen Bereitstellungstyp so lange ein Fehler auf, bis diese Zuordnung erfolgt ist. Sie können die Zuordnung unter **Eigenschaften** für die Anwendung auf der Registerkarte **Anwendungsverwaltung** vornehmen.  

> [!IMPORTANT]  
>  Für Geräte, die ältere Betriebssysteme als iOS 7.1 ausführen, werden verknüpfte Richtlinien nicht entfernt, wenn die App deinstalliert wird.  
>   
>  Wenn das Gerät über Configuration Manager registriert wird, werden die Richtlinien nicht aus den Apps entfernt. Apps, auf die Richtlinien angewendet wurden, behalten die Richtlinieneinstellungen auch dann bei, wenn die App deinstalliert und anschließend neu installiert wird.  

##  <a name="step-5-monitor-the-app-deployment"></a>Schritt 5: Überwachen der App-Bereitstellung  
 Nachdem Sie eine mit einer Verwaltungsrichtlinie für mobile Anwendungen verknüpfte App erstellt und bereitgestellt haben, können Sie die App überwachen und Richtlinienkonflikte lösen.  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Übersicht** > **Bereitstellungen** aus.  

3.  Wählen Sie die von Ihnen erstellte Bereitstellung aus. Wählen Sie anschließend auf der Registerkarte **Startseite** die Option **Eigenschaften** aus.  

4.  Klicken Sie im Detailbereich für die Bereitstellung unter **Zugehörige Objekte** auf **Application Management Policies** (Richtlinien zur Anwendungsverwaltung).  

 Weitere Informationen zum Überwachen von Anwendungen finden Sie unter [Überwachen von Anwendungen](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="learn-how-policy-conflicts-are-resolved"></a>Lösen von Richtlinienkonflikten  
 Wenn bei einer Verwaltungsrichtlinie für mobile Anwendungen bei der ersten Bereitstellung für den Benutzer oder das Gerät ein Konflikt auftritt, wird der jeweilige in Konflikt stehende Einstellungswert aus der Richtlinie entfernt, die für die App bereitgestellt wird. Die App verwendet dann einen vorgegebenen Konfliktwert.  

 Wenn bei einer späteren Bereitstellung ein Konflikt in der Verwaltungsrichtlinie für mobile Anwendungen für den Benutzer oder das Gerät auftritt, wird der jeweilige in Konflikt stehende Einstellungswert nicht in der Richtlinie für die App aktualisiert, und die App verwendet den vorhandenen Wert für diese Einstellung.  

 In Fällen, in denen das Gerät oder der Benutzer zwei in Konflikt stehende Richtlinien erhält, gilt Folgendes:  

-   Wenn bereits eine Richtlinie mit dem Gerät bereitgestellt wurde, werden die vorhandenen Richtlinieneinstellungen nicht überschrieben.  

-   Wenn keine Richtlinie für das Gerät bereitgestellt wurde und zwei widersprüchliche Einstellungen bereitgestellt werden, wird die in das Gerät integrierte Standardeinstellung verwendet.  

##  <a name="see-a-list-of-available-policy-managed-apps"></a>Liste verfügbarer richtlinienverwalteter Apps  
 Eine Liste der richtlinienverwalteten Apps, die für IOS- und Android-Geräte verfügbar sind, finden Sie unter [Microsoft Intune-Anwendungspartner](https://www.microsoft.com/cloud-platform/microsoft-intune-partners).  
