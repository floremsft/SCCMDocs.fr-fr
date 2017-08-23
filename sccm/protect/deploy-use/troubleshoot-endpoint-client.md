---
title: "Problembehandlung für Windows Defender oder den Endpoint Protection-Client | Microsoft-Dokumentation"
description: Erfahren Sie, wie Sie Fehler bei Windows Defender und Endpoint Protection beheben.
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1b096e71f5131214fb4e235e84d0b7f63e566831
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>Fehlerbehebung für Windows Defender oder Endpoint Protection-Client

*Gilt für: System Center Configuration Manager (Current Branch)*


Wenn bei Windows Defender oder Endpoint Protection Probleme auftreten, wenden Sie sich zwecks Unterstützung an den Sicherheitsadministrator. Sie können auch versuchen, die folgenden Probleme zu beheben:  

-   [Aktualisieren von Windows Defender oder Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [Starten von Windows Defender oder des Endpoint Protection-Diensts](#starting-windows-defender-or-endpoint-protection-service)  
-   [Internetverbindungsprobleme](#internet-connection-issues)  
-   [Erkannte Bedrohung kann nicht beseitigt werden](#detected-threat-cant-be-remediated)  
-   [Installieren des Endpoint Protection-Clients](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>Aktualisieren von Windows Defender oder Endpoint Protection  
 Windows Defender oder Endpoint Protection werden automatisch zusammen mit Microsoft Update verwendet, um zu gewährleisten, dass die Virus- und Spywaredefinitionen stets auf dem neuesten Stand sind.  

 **Symptome**  

 In diesem Artikel werden allgemeine Probleme mit automatischen Updates behandelt, einschließlich der folgenden Situationen:  

-   Es werden Fehlermeldungen mit dem Hinweis auf nicht erfolgreiche Updates angezeigt.  

-   Bei der Überprüfung auf Updates erhalten Sie eine Fehlermeldung mit dem Hinweis, dass die Definitionsupdates für Viren und Spyware nicht überprüft, heruntergeladen oder installiert werden können.  

-   Die Updates sind nicht erfolgreich, obwohl eine Verbindung mit dem Internet besteht.  

-   Updates werden nicht automatisch gemäß dem Zeitplan installiert.  

 **Ursache**  

 Meist sind Probleme mit Updates auf Probleme mit der Internetverbindung zurückzuführen. Wenn Sie jedoch sicher sind, dass eine Internetverbindung besteht, da Sie andere Websites besuchen können, ist das Problem unter Umständen auf Konflikte mit den Einstellungen in Windows Internet Explorer zurückzuführen.  

> [!IMPORTANT]  
>  Zum Ausführen dieser Schritte muss Internet Explorer beendet werden. Daher empfiehlt es sich, die Schritte auszudrucken, aufzuschreiben oder in eine andere Datei zu kopieren. Erstellen Sie anschließend ein Lesezeichen für dieses Thema, damit Sie es später problemlos wiederfinden.  

### <a name="step-1-reset-your-internet-explorer-settings"></a>Schritt 1: Zurücksetzen der Internet Explorer-Einstellungen  

1.  Beenden Sie alle geöffneten Programme, einschließlich Internet Explorer.  

    > [!NOTE]  
    >  Beim Zurücksetzen dieser Einstellungen in Internet Explorer werden die temporären Dateien, die Cookies, der Browserverlauf sowie die Onlinekennwörter gelöscht. Die Favoriten bleiben jedoch erhalten.  

2.  Klicken Sie auf **Start** , suchen Sie nach **inetcpl.cpl**, und drücken Sie dann die **EINGABETASTE.**  

3.  Klicken Sie im Dialogfeld **Internetoptionen** auf die Registerkarte **Erweitert** .  

4.  Klicken Sie unter **Internet Explorer-Einstellungen zurücksetzen**auf **Zurücksetzen**und anschließend erneut auf **Zurücksetzen** .  

5.  Warten Sie, bis die Einstellungen zurückgesetzt wurden, und klicken Sie anschließend auf **OK**.  

6.  Öffnen Sie Internet Explorer.  

7.  Öffnen Sie Microsoft Security Essentials, klicken Sie auf die Registerkarte **Aktualisieren** und anschließend auf **Aktualisieren**.  

8.  Sollte das Problem weiterhin bestehen, fahren Sie mit dem nächsten Schritt fort.  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>Schritt 2: Festlegen von Internet Explorer als Standardbrowser  

1.  Beenden Sie alle geöffneten Programme, einschließlich Internet Explorer.  

2.  Klicken Sie auf **Start** , suchen Sie nach **inetcpl.cpl**, und drücken Sie dann die **EINGABETASTE.**  

3.  Klicken Sie im Dialogfeld **Internetoptionen** auf die Registerkarte **Programme** .  

4.  Klicken Sie unter **Standardbrowser**auf **Als Standard**.  

5.  Klicken Sie auf **OK**.  

6.  Öffnen Sie Windows Defender oder Endpoint Protection. Klicken Sie zunächst auf die Registerkarte **Aktualisieren** und dann auf **Aktualisieren**.  

7.  Sollte das Problem weiterhin bestehen, fahren Sie mit dem nächsten Schritt fort.  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Schritt 3: Sicherstellen, dass Uhrzeit und Datum auf dem Computer richtig festgelegt sind  

1.  Öffnen Sie Windows Defender oder Endpoint Protection.  

2.  Wenn die angezeigte Fehlermeldung den Code 0x80072f8f enthält, wird der Fehler mit hoher Wahrscheinlichkeit durch eine fehlerhafte Einstellung für Datum oder Uhrzeit auf dem Computer verursacht.  

3.  Führen Sie zum Zurücksetzen der Datums- und Uhrzeiteinstellung des Computers die Schritte unter [Reparieren fehlerhafter Desktopverknüpfungen und Ausführen allgemeiner Systemwartungsaufgaben](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579) aus.  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>Schritt 4: Umbenennen des Softwareverteilungsordners auf dem Computer  

1. Beenden des Diensts „Automatische Updates“  

    1.  Klicken Sie auf **Start** , suchen Sie nach **services.msc**, und klicken Sie dann auf **OK**.  

    2.  Klicken Sie mit der rechten Maustaste auf den **Dienst „Automatische Updates“**, und klicken Sie anschließend auf **Beenden**.  

    3.  Minimieren Sie das Snap-In „Dienste“.  

2.  Benennen Sie das Verzeichnis **SoftwareDistribution** folgendermaßen um:  

    1.  Klicken Sie auf **Start** , suchen Sie nach  **cmd**, und klicken Sie dann auf **OK**.  

    2.  Geben Sie **cd %windir%**ein, und drücken Sie die **EINGABETASTE.**  

    3.  Geben Sie **ren SoftwareDistribution SDTemp**ein, und drücken Sie die **EINGABETASTE.**  

    4.  Geben Sie **exit**ein, und drücken Sie die **EINGABETASTE.**  

3.  Starten Sie den Dienst „Automatische Updates“ folgendermaßen:  

    1.  Maximieren Sie das Snap-In „Dienste“.  

    2.  Klicken Sie mit der rechten Maustaste auf den **Dienst „Automatische Updates“**, und klicken Sie anschließend auf **Starten**.  

    3.  Schließen Sie das Snap-In-Fenster „Dienste“.  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Schritt 5: Zurücksetzen des Antivirenaktualisierungsmoduls von Microsoft auf dem Computer  

1.  Klicken Sie auf **Start** , suchen Sie nach  **cmd**, und klicken Sie auf **OK**. Klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und wählen Sie dann **Als Administrator ausführen**aus.  

2.  Geben Sie in das Fenster **Eingabeaufforderung** die folgenden Befehle ein, und drücken Sie nach jedem Befehl die **EINGABETASTE.**  

     **Cd\\**  

     **Cd Programme\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **Beenden**  

3.  Starten Sie den Computer neu.  

4.  Öffnen Sie Windows Defender oder  
          Endpoint Protection, klicken Sie auf die Registerkarte **Aktualisieren**, und dann auf **Aktualisieren**.  

5.  Sollte das Problem weiterhin bestehen, fahren Sie mit dem nächsten Schritt fort.  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>Schritt 6: Manuelles Installieren der Virus- und Spyware-Definitionsupdates  

-   Wenn Sie mit einem 32-Bit-Windows-Betriebssystem arbeiten, laden Sie die neuesten Updates unter [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342) manuell herunter.  

-   Wenn Sie mit einem 64-Bit-Windows-Betriebssystem arbeiten, laden Sie die neuesten Updates unter [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341) manuell herunter.  

-   Klicken Sie auf **Ausführen**. Die neuesten Updates werden manuell auf dem Computer installiert.  


### <a name="step-7-contact-support"></a>Schritt 7: Kontaktieren des Supports  

-   Wenn das Problem mit diesen Schritten nicht behoben werden konnte, wenden Sie sich an den Support. Weitere Informationen finden Sie unter [Kundensupport](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174).  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>Starten von Windows Defender oder des Endpoint Protection-Diensts  
 **Symptom**  

 Eine Meldung mit dem folgenden Hinweis wird angezeigt:  **Windows Defender or Endpoint Protection isn't monitoring your computer because the program's service stopped (Der Computer wird nicht von Windows Defender oder Endpoint Protection überwacht, da der Dienst des Programms angehalten wurde). Sie sollten ihn jetzt neu starten.** 

 **Lösung**  

### <a name="step-1-restart-your-computer"></a>Schritt 1: Neustarten des Computers  

-   Schließen Sie alle Anwendungen, und starten Sie den Computer neu.  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>Schritt 2: Stellen Sie sicher, dass der Dienst „Windows Defender“ oder „Endpoint Protection“ auf „Automatisch“ festgelegt ist und gestartet wurde.  

1.  Klicken Sie auf **Start** , suchen Sie nach **services.msc**, und drücken Sie dann die **EINGABETASTE.**  

2.  Suchen Sie nach **Microsoft-Antischadsoftwaredienst**. Klicken Sie mit der rechten Maustaste darauf, und klicken Sie dann auf **Eigenschaften** , oder doppelklicken Sie auf den Dienst, um ihn zu öffnen.  

3.  Stellen Sie sicher, dass der**Starttyp**auf**Automatisch**festgelegt ist.  

4.  Klicken Sie auf die Schaltfläche **Starten** , um den Dienst zu starten. Wenn die Schaltfläche **Starten** nicht verfügbar ist, klicken Sie auf **Anhalten** , und klicken Sie dann auf **Starten** , um den Dienst erneut zu starten.  

5.  Stellen Sie sicher, dass Sie alle Fehler notieren, die bei diesem Vorgang eventuell auftreten, einen Fall online senden und die Fehlerinformationen einbinden.  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>Schritt 3: Entfernen aller eventuell vorhandener Internetsicherheitsprogramme  

1.  Klicken Sie auf **Start** , suchen Sie nach **appwiz.cpl**, und drücken Sie dann die **EINGABETASTE.**  

2.  Deinstallieren Sie in der Liste der installierten Programme sämtliche Drittanbieter-Internet-Sicherheitsprogramme.*  

3.  Starten Sie den Computer neu, und wiederholen Sie die Installation von Windows Defender oder  
          Endpoint Protection.  

> [!NOTE]  
>  Einige Internet-Sicherheitsanwendungen werden nicht vollständig deinstalliert. Möglicherweise müssen Sie ein Bereinigungsprogramm herunterladen und ausführen, damit frühere Sicherheitsanwendungen vollständig entfernt werden können.  

> [!CAUTION]  
>  Wenn Sie Ihre Internet-Sicherheitsprogramme entfernen, befinden sich der Computer in einem ungeschützten Zustand. Wenn bei der Installation von   
>       Endpoint Protection Probleme Auftreten, nachdem Sie die vorhandenen Internet-Sicherheitsprogramme entfernt haben, wenden Sie sich mittels einer Onlineabfrage an den Support für Windows Defender oder  
>       Endpoint Protection. Weitere Informationen finden Sie unter [Eine Anfrage online einreichen](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx).  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>Schritt 4: Deinstallieren und Neuinstallieren von Endpoint Protection  

1.  Klicken Sie auf **Start** , suchen Sie nach **appwiz.cpl**, und drücken Sie dann die **EINGABETASTE.**  

2.  Klicken Sie in der Liste mit den installierten Programmen auf **Endpoint Protection**, und deinstallieren Sie es.  

3.  Starten Sie bei Aufforderung den Computer neu, und wiederholen Sie die Installation von Endpoint Protection.  

##  <a name="internet-connection-issues"></a>Internetverbindungsprobleme  
 Damit der Computer von Windows Update mit den neuesten Updates versorgt werden kann, muss eine Verbindung mit dem Internet bestehen.  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>Schritt 1: Prüfen, ob der Computer mit dem Internet verbunden ist  

1.  Klicken Sie auf **Start**, suchen Sie nach **ncpa.cpl**, und drücken Sie dann die **EINGABETASTE.**  

2.  Klicken Sie mit der rechten Maustaste auf den Verbindungsnamen, und klicken Sie anschließend auf **Status**.  

3.  Wenn Ihr Computer mit dem Internet verbunden ist, wird unter Windows XP der Verbindungsstatus **Verbunden**, **Aktiviert**oder **Authentifizierung erfolgreich** angezeigt. Unter Windows Vista und Windows 7 wird der Status **IPv4** als **Internet**angezeigt.  

4.  Wenn Ihr Computer nicht mit dem Internet verbunden ist, klicken Sie mit der rechten Maustaste auf den Verbindungsnamen, und klicken Sie dann auf **Verbinden**, **Aktivieren**, **Authentifizieren**oder **Reparieren**.  

### <a name="step-3-restart-your-computer"></a>Schritt 3: Neustarten des Computers  

-   Schließen Sie alle geöffneten Programme, und starten Sie den Computer neu.  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>Schritt 4: Wenn Sie weiterhin keine Verbindung mit dem Internet herstellen können, Verbindungen überprüfen  

1.  Stellen Sie bei Verwendung einer DFÜ-Verbindung sicher, dass das Telefonkabel ordnungsgemäß an die Telefondose und an das Modem angeschlossen ist.  

2.  Wenn Sie ein Kabelmodem verwenden, stellen Sie sicher, dass das Kabel zum Modem ordnungsgemäß angeschlossen ist und die Verbindung vom Modem zum Computer ordnungsgemäß funktioniert.  

3.  Wenn Sie ein Kabelmodem oder einen DSL-Router verwenden, stellen Sie sicher, dass die Verbindungen zum Router und zum Computer ordnungsgemäß funktionieren. Trennen Sie die Verbindung mit dem Router oder Modem, und schalten Sie beide aus. Warten Sie einige Minuten, schließen Sie zuerst das Modem wieder an. Warten Sie einen Moment, schließen Sie dann den Router an, und starten Sie den Computer erneut.  

##  <a name="detected-threat-cant-be-remediated"></a>Erkannte Bedrohung kann nicht beseitigt werden  
 Wenn von Windows Defender oder  
      Endpoint Protection eine potenzielle Bedrohung in einer komprimierten Datei mit der Dateinamenerweiterung „.zip“ oder auf einer Netzwerkfreigabe ermittelt wird, wird versucht, die Bedrohung zu behandeln, indem das entsprechende Element unter Quarantäne gestellt oder entfernt wird.  

### <a name="remove-or-scan-the-file"></a>Entfernen oder scannen Sie die Datei.  

-   Wenn die Bedrohung in einer ZIP-Datei ermittelt wurde, navigieren Sie zu der ZIP-Datei. Entfernen Sie nun entweder die Datei, oder scannen Sie sie, indem Sie mit der rechten Maustaste darauf klicken und **Mit Windows Defender scannen** oder **Mit Endpoint Protection scannen**auswählen. Wenn von Windows Defender oder Endpoint Protection weitere Bedrohungen in der Datei ermittelt werden, werden Sie über diese informiert. Sie haben dann die Möglichkeit, eine geeignete Aktion auszuführen.  

-   Wenn sich die ermittelte Bedrohung in einer Netzwerkfreigabe befindet, navigieren Sie zu dieser Netzwerkfreigabe, und überprüfen Sie sie, indem Sie mit der rechten Maustaste auf die Datei klicken und **Mit Windows Defender scannen** oder **Mit Endpoint Protection scannen**auswählen. Wenn von Windows Defender oder Endpoint Protection weitere Bedrohungen in der Netzwerkfreigabe ermittelt werden, werden Sie über diese informiert. Sie haben dann die Möglichkeit, eine geeignete Aktion auszuführen.  

-   Wenn Sie unsicher über den Ursprung der Datei sind, empfiehlt sich als beste Lösung eine vollständige Überprüfung des Computers. Ein vollständiger Scan kann zwar einige Zeit in Anspruch nehmen, von Windows Defender oder Endpoint Protection kann hierbei jedoch die Quelle der Infektion gesucht und entfernt werden.  

##  <a name="install-the-endpoint-protection-client"></a>Installieren des Endpoint Protection-Clients  

> [!NOTE]  
>  Windows Defender wird auf Windows 10-PCs mit dem Betriebssystem installiert.  

 **Symptome**  

 Die Installation ist aus einem unbekannten Grund nicht erfolgreich, oder es wird eine Fehlermeldung mit einem Fehlercode angezeigt (beispielsweise 0x80070643, 0X8007064A, 0x8004FF2E, 0x8004FF01, 0x8004FF07, 0x80070002, 0x8007064C, 0x8004FF00, 0x80070001, 0x80070656, 0x8004FF40, 0xC0000156, 0x8004FF41 0x8004FF0B, 0x8004FF11, 0x80240022, 0x8004FF04, 0x80070660, 0x800106B5, 0x80070715, 0x80070005, 0x8004EE00, 0x8007003, 0x800B0100, 0x8007064E oder 0x8007007E).  

 Handelt es sich um einen Computer unter Windows XP Service Pack 2 (SP2), wird ggf. mindestens eine der folgenden Fehlermeldungen angezeigt:  

-   Der Installations-Assistent kann ein zum Abschließen der Installation erforderliches Rolluppaket für den Filter-Manager nicht finden.  

-   KB914882 – Setupfehler: Die Windows XP-Dateien können nicht aktualisiert werden, da die auf diesem System installierte Sprache nicht der Sprache des Updates entspricht.  

 **Ursache**  

 Endpoint Protection kann nicht auf einem Computer installiert werden, auf dem andere Sicherheitsprogramme ausgeführt werden. Manchmal kommt es vor, dass andere Sicherheitsprogramme nicht vollständig deinstalliert werden, obwohl sie zuvor entfernt wurden. Zum Installieren von Endpoint Protection muss eine Originalversion des Windows-Betriebssystems ausgeführt werden.  

 **Lösung**  

> [!IMPORTANT]  
>  Im Zuge der Behebung dieses Problems muss der Computer neu gestartet werden. Erstellen Sie ein Lesezeichen für diese Seite (indem Sie sie als Favorit markieren), damit Sie das Thema später leichter wiederfinden, oder drucken Sie die Seite aus.  

### <a name="step-1-remove-any-existing-security-programs"></a>Schritt 1: Entfernen aller vorhandenen Sicherheitsprogramme  
**Nur Endpoint Protection**

1.  Deinstallieren Sie alle vorhandenen Internetsicherheitsprogramme vollständig.  

2.  Starten Sie den Computer neu.  

3.  Installieren Sie Endpoint Protection erneut. Konnte das Problem dadurch nicht behoben werden, fahren Sie mit dem nächsten Schritt fort.  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>Schritt 2: Sicherstellen, dass der Windows-Installationsdienst ausgeführt wird  

1.  Klicken Sie auf **Start** , suchen Sie nach **services.msc**, und drücken Sie dann die **EINGABETASTE.**  

2.  Klicken Sie mit der rechten Maustaste auf **Windows Installer**, und klicken Sie dann auf **Starten**. Wenn die Option **Starten** nicht verfügbar ist, die Optionen **Anhalten** und **Neu starten** aber verfügbar sind, wurde der Dienst bereits gestartet.  

3.  Klicken Sie auf der Seite **Dienste** im Menü **Datei** auf **Beenden**.  

4.  Klicken Sie auf **Start**, und suchen Sie **Eingabeaufforderung**. Klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **Als Administrator ausführen**.  

5.  Geben Sie **MSIEXEC /REGSERVER**ein, und drücken Sie die **EINGABETASTE**.  

    > [!NOTE]  
    >  Sie erhalten keine Bestätigung dafür, dass der Befehl erfolgreich ausgeführt wurde.  

6.  Installieren Sie Endpoint Protection erneut. Konnte das Problem dadurch nicht behoben werden, fahren Sie mit dem nächsten Schritt fort.  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>Schritt 3: Starten von Windows im Modus „Benutzerdefinierter Systemstart“  

1.  Klicken Sie auf **Start** , suchen Sie nach **msconfig**, und drücken Sie dann die **EINGABETASTE.**  

2.  Klicken Sie auf der Registerkarte **Allgemein** auf **Benutzerdefinierter Systemstart**und deaktivieren Sie dann das Kontrollkästchen **Systemstartelemente laden** .  

3.  Aktivieren Sie auf der Registerkarte **Dienste** die Option **Alle Microsoft-Dienste ausblenden** , und deaktivieren Sie alle Kontrollkästchen für die Dienste, die in der Liste enthalten sind.  

4.  Klicken Sie auf **OK**und dann auf **Neu starten** , um den Computer erneut zu starten.  

5.  Versuchen Sie, Endpoint Protection erneut zu installieren.  



### <a name="see-also"></a>Weitere Informationen:  
 [Endpoint Protection client frequently asked questions (Endpoint Protection-Client – Häufig gestellte Fragen)](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Hilfe zu Endpoint Protection-Client](../../protect/deploy-use/endpoint-protection-client-help.md)
