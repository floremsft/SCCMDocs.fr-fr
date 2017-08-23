---
title: Setup-Assistent | Microsoft-Dokumentation
ms.custom: na
ms.date: 7/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 678f1b35fe6f7649dacb766f7c671f4ec8ea1435
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>Verwenden des Setup-Assistenten zum Installieren von System Center Configuration Manager-Standorten

*Gilt für: System Center Configuration Manager (Current Branch)*


Verwenden Sie zum Installieren eines neuen System Center Configuration Manager-Standorts mit einer Benutzeroberfläche den Configuration Manager-Setup-Assistenten (setup.exe). Der Assistent unterstützt die Installation eines primären Standorts oder eines Standorts der zentralen Verwaltung. Verwenden Sie auch den Assistenten zum [Ausführen eines Upgrades für eine Evaluierungsinstallation](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md) von Configuration Manager auf eine vollständig lizenzierte Installation. Wenn Sie den Assistenten nicht verwenden möchten, können Sie stattdessen ein [Installationsskript](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) verwenden und eine unbeaufsichtigte Befehlszeileninstallation ausführen.

Installieren Sie einen sekundären Standort über die Configuration Manager-Konsole. Sekundäre Standorte unterstützen keine Installation per Skript über die Befehlszeile.

## <a name="bkmk_primary"></a> Installieren eines primären Standorts oder eines Standorts der zentralen Verwaltung
Verwenden Sie das folgende Verfahren,um einen Standort der zentralen Verwaltung oder einen primären Standort zu installieren oder ein Upgrade eines Evaluierungsstandorts auf einen vollständig lizenzierten Configuration Manager-Standort durchzuführen.   

Machen Sie sich vor der Installation des Standorts mit den Details in den folgenden Artikeln vertraut:
 -  [Vorbereitung zur Installation von Standorten ](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [Voraussetzungen für die Installation von Standorten](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

Wenn Sie einen Standort der zentralen Verwaltung als Teil eines Standorterweiterungsszenarios installieren, lesen Sie den Abschnitt [Erweitern eines eigenständigen primären Standorts](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) dieses Themas, bevor Sie das folgende Verfahren anwenden.

### <a name="bkmk_installpri"></a> So installieren Sie einen primären Standort oder einen Standort der zentralen Verwaltung

1.  Führen Sie auf dem Computer, auf dem der Standort installiert werden soll, **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** aus, um den **Setup-Assistenten von System Center Configuration Manager** zu starten.  

    > [!NOTE]  
    > Wenn Sie einen Standort der zentralen Verwaltung installieren, um auf einem eigenständigen primären Standort zu erweitern, oder einen neuen untergeordneten primären Standort in einer vorhandenen Hierarchie installieren, benötigen Sie Installationsmedien (Quelldateien), die mit der Version des oder der vorhandenen Standorte übereinstimmen. Wenn Sie konsoleninterne Aktualisierungen installiert haben, die die Versionen der zuvor installierten Standorte geändert haben, verwenden Sie nicht die Originalinstallationsmedien. Verwenden Sie stattdessen Quelldateien aus dem [Ordner CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) eines aktualisierten Standorts. Configuration Manager erfordert die Verwendung von Quelldateien, die mit der Version des bestehenden Standorts übereinstimmen, mit dem der neue Standort eine Verbindung herstellt.  

2.  Wählen Sie auf der Seite **Vorbereitung** die Option **Weiter** aus.  

3.  Wählen Sie auf der Seite **Erste Schritte** den Typ des Standorts aus, den Sie installieren möchten:  

    -   **Standort der zentralen Verwaltung** als ersten Standort einer neuen Hierarchie oder beim Erweitern eines eigenständigen primären Standorts:  

        Wählen Sie **Standort der zentralen Verwaltung für Configuration Manager installieren** aus.  

         Bei einem späteren Schritt dieses Verfahrens haben Sie die Möglichkeit, einen Standort der zentralen Verwaltung als ersten Standort einer neuen Hierarchie oder zum Erweitern eines eigenständigen primären Standorts zu installieren.  

    -    **Primärer Standort** als eigenständiger primärer Standort, der der erste Standort einer neuen Hierarchie ist, oder als untergeordneter primärer Standort:  

        Wählen Sie **Primären Configuration Manager-Standort installieren** aus.  

        > [!TIP]  
        > Normalerweise wählen Sie nur die Option **Typische Installationsoptionen für einen eigenständigen primären Standort verwenden** aus, wenn Sie einen eigenständigen primären Standort in einer Testumgebung installieren möchten. Wenn Sie diese Option auswählen:  

        > -   konfiguriert Setup den Standort automatisch als eigenständigen primären Standort.  
        > -   wird ein Standardinstallationspfad verwendet.  
        > -   wird eine lokale Installation der Standardinstanz von SQL Server für die Standortdatenbank verwendet.  
        > -   werden ein Verwaltungspunkt und ein Verteilungspunkt auf dem Standortservercomputer installiert.  
        > -   Konfiguriert den Standort mit Englisch und der Anzeigesprache des Betriebssystems auf dem primären Standortserver, wenn diese einer der Sprachen entspricht, die Configuration Manager unterstützt.  

4.  Auf der Seite **Product Key**:
    - Wählen Sie, ob Configuration Manager als Evaluierungsversion oder als lizenzierte Version installiert werden soll.  

      -   Wenn Sie eine lizenzierte Version auswählen, geben Sie den Product Key ein und klicken Sie auf **Weiter**.  

      -   Wenn Sie eine Evaluierungsversion auswählen, klicken Sie auf **Weiter**. (Sie können später ein Upgrade einer Evaluierungsversion auf eine Vollversion durchführen.)  
    - Seit der Veröffentlichung von Version 1606 des Baselinemediums für System Center Configuration Manager im Oktober 2016 können Sie das Ablaufdatum Ihres Software Assurance-Vertrags angeben. Auf dieser Seite haben Sie die Möglichkeit, das **Ablaufdatum der Software Assurance** Ihres Lizenzvertrags als praktische Erinnerung an dieses Datum anzugeben. Wenn Sie das Datum nicht während des Setups eingeben, können Sie es später in der Configuration Manager-Konsole angeben.

      > [!NOTE]   
      > Microsoft überprüft das angegebene Ablaufdatum nicht und verwendet es auch nicht, um die Lizenz zu überprüfen. Stattdessen können Sie das Ablaufdatum angeben, um daran erinnert zu werden. Dies ist hilfreich, da Configuration Manager regelmäßig überprüft, ob neue Softwareupdates online angeboten werden, und Ihr Software Assurance-Lizenzstatus sollte aktuell sein, damit Sie von diesen zusätzlichen Updates profitieren können.    

      Weitere Informationen finden Sie unter [Lizenzierung und Branches für System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

5.  Lesen und akzeptieren Sie auf der Seite **Microsoft-Software-Lizenzbedingungen** die Lizenzbedingungen.  

6.  Lesen und akzeptieren Sie auf der Seite **Lizenzen für erforderliche Komponenten** die Lizenzbedingungen für die erforderliche Software. Die Software wird gegebenenfalls heruntergeladen und automatisch auf Standortsystemen oder Clients installiert. Die nächste Seite wird erst angezeigt, nachdem Sie alle Kontrollkästchen aktiviert haben.  

7.  Geben Sie auf der Seite **Download der Voraussetzungskomponenten** an, ob Setup die neuesten vorausgesetzten verteilbaren Dateien aus dem Internet herunterladen oder zuvor heruntergeladene Dateien verwenden muss:  

    -   Wenn Setup die Dateien zu diesem Zeitpunkt herunterladen soll, wählen Sie **Erforderliche Dateien herunterladen** aus, und geben Sie einen Speicherort für die Dateien an.  

    -   Falls Sie bereits Dateien mit dem [Setup-Downloadprogramm](../../../../core/servers/deploy/install/setup-downloader.md) heruntergeladen haben, wählen Sie **Bereits heruntergeladene Dateien verwenden** aus, und geben Sie den Downloadordner an.  

        > [!TIP]  
        > Wenn Sie bereits heruntergeladene Dateien verwenden, überprüfen Sie, ob der Downloadordner die neuesten Dateiversionen enthält.  

8.  Wählen Sie auf der Seite **Serversprachauswahl** die Sprachen aus, die für die Configuration Manager-Konsole sowie für Berichte verfügbar sind. (Englisch ist standardmäßig aktiviert und kann nicht entfernt werden.)  

9. Wählen Sie auf der Seite **Clientsprachauswahl** die Sprachen aus, die für Clientcomputer verfügbar sind. Geben Sie außerdem an, ob alle Clientsprachen für Clients für mobile Geräte aktiviert werden sollen. (Englisch ist standardmäßig aktiviert und kann nicht entfernt werden.)  

    > [!IMPORTANT]  
    > Wenn Sie einen Standort der zentralen Verwaltung verwenden, stellen Sie sicher, dass die Clientsprachen, die Sie am Standort der zentralen Verwaltung konfigurieren, alle Clientsprachen umfassen, die Sie an den einzelnen untergeordneten primären Standorten konfigurieren. Dies liegt daran, dass Clients, die über einen Verteilungspunkt installieren, Zugriff auf die Clientsprachen am Standort der obersten Ebene haben, während Clients, die über einen Verwaltungspunkt installieren, Zugriff auf die Clientsprachen von ihrem zugewiesenen primären Standort haben.  

10. Geben Sie auf der Seite **Standort- und Installationseinstellungen** für den neuen Standort, den Sie installieren, Folgendes an:  

    -   **Standortcode:** [Jeder Standortcode in einer Hierarchie muss eindeutig sein](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes) und drei alphanumerische Zeichen (A bis Z und 0 bis 9) umfassen. Da der Standortcode in Ordnernamen verwendet wird, dürfen keine für Windows reservierten Namen wie die folgenden für den Standort verwendet werden:    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        > Setup überprüft nicht, ob der angegebene Standortcode bereits verwendet wird oder ein reservierter Name ist.  

    -   **Standortname:** Jeder Standort benötigt diesen Anzeigenamen, mit dem Sie den Standort bestimmen können.  

    -   **Installationsordner**: Dies ist der Ordnerpfad zur Configuration Manager-Installation. Sie können den Speicherort nach der Installation des Standorts nicht mehr ändern. Der Pfad darf auch keine Unicode-Zeichen oder Leerzeichen enthalten.  

11. Verwenden Sie auf der Seite **Standortinstallation** die folgende Option entsprechend Ihrem Szenario:  

    -   **Ich installiere einen Standort der zentralen Verwaltung:**  

         Wählen Sie auf der Seite **Installation des Standorts der zentralen Verwaltung** die Option **Als ersten Standort in einer neuen Hierarchie installieren** aus, und klicken Sie auf **Weiter**, um fortzufahren.  

    -   **Ich erweitere einen eigenständigen primären Standort in eine Hierarchie mit einem Standort der zentralen Verwaltung:**  

         Wählen Sie auf der Seite **Installation des Standorts der zentralen Verwaltung** die Option **Vorhandenen eigenständigen primären Standort in eine Hierarchie erweitern** aus, geben Sie den FQDN des eigenständigen primären Standortservers an, und klicken Sie dann auf **Weiter**, um fortzufahren.  

         Die Medien, die Sie verwenden, um den neuen Standort der zentralen Verwaltung zu installieren, müssen mit der Version des primären Standorts übereinstimmen.  

    -   **Ich installiere einen eigenständigen primären Standort:**  

         Wählen Sie auf der Seite **Installation am primären Standort** die Option **Den primären Standort als eigenständigen Standort installieren** aus. Klicken Sie dann auf **Weiter**.  

    -   **Ich installiere einen untergeordneten primären Standort:**  

         Wählen Sie auf der Seite **Installation am primären Standort** die Option **Den primären Standort einer vorhandenen Hierarchie hinzufügen** aus, geben Sie den FQDN des Standorts der zentralen Verwaltung an, und klicken Sie dann auf **Weiter**.  

12. Geben Sie auf der Seite **Datenbankinformationen** die folgenden Informationen an:  

    -   **SQL Server-Name (FQDN):** Dieser Wert wird standardmäßig auf den Standortservercomputer festgelegt.

     Wenn Sie einen benutzerdefinierten Port verwenden, fügen Sie diesen Port zum FQDN des SQL Servers hinzu. Stellen Sie hierzu dem FQDN des Sequel Servers ein Komma nach gefolgt von der Portnummer.   Beispiel: Verwenden Sie für den Server *SQLServer1.fabrikam.com* Folgendes, um den Port *1551* anzugeben: **SQLServer1.fabrikam.com,1551**

    -   **Instanzname:** Ist standardmäßig leer. Verwendet die Standardinstanz von SQL auf dem Standortservercomputer.  

    -   **Datenbankname:** Dieser Wert ist standardmäßig auf CM_&lt;Standortcode\> festgelegt. Sie können einen anderen Namen angeben.  

    -   **Service Broker-Port:** Ist standardmäßig auf die Verwendung des standardmäßigen SQL Server Service Broker-Ports (SSB) 4022 festgelegt. SQL kommuniziert damit direkt mit der Standortdatenbank an anderen Standorten.  

13. Auf der zweiten Seite **Datenbankinformationen** können Sie vom Standard abweichende Speicherorte für die SQL Server-Datendatei und die SQL Server-Protokolldatei für die Standortdatenbank angeben:  

    -   Standardmäßige Dateispeicherorte für SQL Server werden bereitgestellt.  

    -   Die Option zur Angabe der vom Standard abweichenden Speicherorte ist nicht verfügbar, wenn Sie einen SQL Server-Cluster verwenden.  

    -   Von der Voraussetzungsprüfung wird nicht überprüft, ob für die vom Standard abweichenden Dateispeicherorte genügend Speicherplatz vorhanden ist.  

14. Geben Sie auf der Seite **SMS-Anbietereinstellungen** den vollqualifizierten Domänennamen (FQDN) des Servers an, auf dem der SMS-Anbieter installiert werden soll.  

    -   Standardmäßig wird der Standortserver angegeben.  

    -   Nach der Standortinstallation können Sie zusätzliche SMS-Anbieter konfigurieren.  

15. Geben Sie auf der Seite **Kommunikationseinstellungen für Clientcomputer** an, ob von allen Standortsystemen ausschließlich die HTTPS-Kommunikation mit Clients zugelassen werden soll oder ob die Kommunikationsmethode für jede Standortsystemrolle konfiguriert werden muss.  

    Wenn Sie die Option **Alle Standortsystemrollen lassen ausschließlich die HTTPS-Kommunikation mit Clients zu** auswählen, ist für den Clientcomputer ein gültiges PKI-Zertifikat zur Clientauthentifizierung erforderlich. Weitere Informationen zu den PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    > [!NOTE]  
    > Dieser Schritt ist nur nötig, wenn Sie einen primären Standort installieren. Wenn sie einen Standort der zentralen Verwaltung installieren, überspringen Sie diesen Schritt.  

16. Geben Sie auf der Seite **Standortsystemrollen** an, ob ein Verwaltungspunkt oder ein Verteilungspunkt installiert werden soll. Für jede gewählte Rolle, die von Setup installiert werden soll, gelten diese Voraussetzungen:  

    -   Sie müssen den **FQDN** des Computers eingeben, der die Rolle hostet, und die Clientverbindungsmethode wählen, die der Server unterstützt (HTTP oder HTTPS).  

    -   Falls Sie auf der vorherigen Seite die Option **Alle Standortsystemrollen lassen ausschließlich die HTTPS-Kommunikation mit Clients zu** ausgewählt haben, werden die Clientverbindungseinstellungen automatisch für HTTPS konfiguriert und können nur geändert werden, wenn Sie zur vorherigen Seite zurückkehren und die Einstellung ändern.  

    > [!NOTE]  
    > Dieser Schritt ist nur nötig, wenn Sie einen primären Standort installieren. Wenn sie einen Standort der zentralen Verwaltung installieren, überspringen Sie diesen Schritt.  

    > [!NOTE]  
    > Zum Installieren der Standortsystemrollen wird von Setup das **Standortsystem-Installationskonto**verwendet. Standardmäßig wird das Computerkonto des primären Standorts verwendet. Dieses Konto muss einem lokalen Administrator auf einem Remotecomputer gehören, um die Standortsystemrolle zu installieren. Wenn dieses Konto nicht über die erforderlichen Berechtigungen verfügt, deaktivieren Sie die Standortsystemrollen, und installieren Sie sie später über die Configuration Manager-Konsole, nachdem weitere Konten für die Verwendung als Standortsystem-Installationskonten konfiguriert wurden.  

17. Überprüfen Sie auf der Seite **Nutzungsdaten** die Informationen zu Daten, die von Microsoft gesammelt werden, und klicken Sie dann auf **Weiter**.  

18. Die Seite **Dienstverbindungspunkt einrichten** ist während des Setups nur in den folgenden Fällen verfügbar:  

    -   Wenn Sie einen eigenständigen primären Standort installieren.  

    -   Wenn Sie einen Standort der zentralen Verwaltung installieren.  

    > [!NOTE]  
    > Wenn Sie einen untergeordneten primären Standort installieren, überspringen Sie diesen Schritt (die Seite ist nicht verfügbar).  

     Wenn Sie einen Standort der zentralen Verwaltung als Teil eines Standorterweiterungsszenarios installieren und diese Rolle bereits an dem eigenständigen primären Standort installiert ist, müssen Sie diese Rolle am eigenständigen primären Standort deinstallieren. In einer Hierarchie ist nur eine Instanz dieser Rolle zulässig, und zwar nur für den obersten Standort der Hierarchie.  

     Nach Auswahl einer Konfiguration für den **Dienstverbindungspunkt** klicken Sie auf **Weiter**. (Nach Abschluss von Setup können Sie diese Konfiguration in der Configuration Manager-Konsole ändern.)  

19. Überprüfen Sie auf der Seite **Zusammenfassung der Einstellungen** die Einstellung, die Sie ausgewählt haben. Wenn Sie bereit sind, wählen Sie **Weiter** aus, um die Voraussetzungsprüfung zu starten.  

20. Auf der Seite **Voraussetzungsprüfung** werden etwaige Probleme aufgelistet.  

    -   Wenn bei der Voraussetzungsprüfung ein Problem festgestellt wird, klicken Sie in der Liste auf einen Eintrag, um Details zur Behebung des Problems anzuzeigen.  

    -   Sie müssen alle Elemente mit dem Status **Fehler** korrigieren, ehe Sie die Installation des Standorts fortsetzen können. Elemente mit dem Status **Warnung** sollten korrigiert werden, blockieren aber nicht die Installation des Standorts.  

    -   Nach dem Beheben von Problemen klicken Sie auf **Prüfung ausführen**, um die Voraussetzungsprüfung erneut auszuführen.  

     Wenn die Voraussetzungsprüfung ausgeführt wird und nicht der Status **Fehler** gemeldet wird, können Sie auf **Installation starten** klicken, um die Installation des Standorts zu starten.  

    > [!TIP]  
    > Zusätzlich zu dem im Assistenten aufgeführten Feedback finden Sie weitere Informationen zu Problemen mit den Voraussetzungen in der Datei **ConfigMgrPrereq.log**. Sie befindet sich auf dem Computer, auf dem die Installation erfolgt, im Stammverzeichnis des Systemlaufwerks. Eine Liste der Regeln und Beschreibungen zu den Installationsvoraussetzungen finden Sie unter [Liste der Voraussetzungsprüfungen für System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

21. Auf der Seite **Installation** wird der Installationsstatus von Setup angezeigt. Nach Abschluss der Installation des Hauptstandortservers können Sie den Installationsassistenten mit der Option **Schließen** beenden. Nachdem Sie den Assistenten geschlossen haben, werden die Installation und Erstkonfiguration des Standorts im Hintergrund fortgesetzt.  

    -   Bevor das Setup abgeschlossen ist, können Sie eine Configuration Manager-Konsole mit dem Standort verbinden. Diese Konsole stellt eine schreibgeschützte Verbindung her und ermöglicht Ihnen das Anzeigen, jedoch nicht das Bearbeiten von Objekten und Einstellungen.  

    -   Nach dem Abschluss von Setup können Sie eine Verbindung mit einer Konsole herstellen, über die Sie Objekte und Einstellungen bearbeiten können.  


## <a name="bkmk_expand"></a> Erweitern eines eigenständigen primären Standorts
Wenn Sie einen eigenständigen primären Standort als ersten Standort installiert haben, können Sie diesen Standort zu einem späteren Zeitpunkt in eine größere Hierarchie erweitern, indem Sie einen Standort der zentralen Verwaltung installieren.   

Wenn Sie einen eigenständigen primären Standort erweitern, installieren Sie einen neuen Standort der zentralen Verwaltung, der die Datenbank des vorhandenen eigenständigen primären Standorts als Referenz verwendet. Nach Installation des neuen Standorts der zentralen Verwaltung fungiert der eigenständige primäre Standort als untergeordneter primärer Standort.

-   Nur ein eigenständiger primärer Standort kann in eine neue Hierarchie erweitert werden.  

-   Nur ein einziger eigenständiger primärer Standort kann in eine bestimmte Hierarchie erweitert werden. Sie können über diese Option nicht zusätzliche eigenständige primäre Standorte derselben Hierarchie hinzufügen. Verwenden Sie stattdessen die Migration, um Daten aus einer Hierarchie in eine andere zu migrieren.  

-   Nachdem Sie einen eigenständigen Standort in eine Hierarchie mit einem Standort der zentralen Verwaltung erweitert haben, können Sie weitere untergeordnete primäre Standorte hinzufügen.  

-   Zum Entfernen eines primären Standorts aus einer Hierarchie mit einem Standort der zentralen Verwaltung müssen Sie den primären Standort deinstallieren.  

Um den Standort zu erweitern, verwenden Sie den Setup-Assistenten für System Center Configuration Manager, um einen neuen Standort der zentralen Verwaltung mit folgenden Einschränkungen zu installieren:  

-   Der Standort der zentralen Verwaltung muss mit derselben Version von Configuration Manager wie der eigenständige primäre Standort installiert werden.  

-   Wählen Sie auf der Seite **Erste Schritte** des Setup-Assistenten die Option zum Installieren eines Standorts der zentralen Verwaltung aus. In einer späteren Phase von Setup wählen Sie eine Option zum Erweitern eines vorhandenen eigenständigen primären Standorts aus.  

-   Wenn Sie die Seite **Clientsprachauswahl** für den neuen Standort der zentralen Verwaltung konfigurieren, müssen Sie dieselben Clientsprachen auswählen, die für den eigenständigen primären Standort konfiguriert sind, den Sie erweitern.  

-   Auf der Seite **Standortinstallation** wählen Sie die Option zum Erweitern des eigenständigen primären Standorts aus.  

Um einen eigenständigen primären Standort zu erweitern, sehen Sie sich zuerst die [Voraussetzungen zum erweitern eines Standorts](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) an, und verwenden Sie dann das Verfahren *[So installieren Sie einen primären Standort oder einen Standort der zentralen Verwaltung](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)* weiter oben in diesem Artikel.


## <a name="bkmk_secondary"></a> Installieren eines sekundären Standorts
 Sie installieren einen sekundären Standort mithilfe der Configuration Manager-Konsole.  

-   Wenn die verwendete Konsole nicht mit dem primären Standort verbunden ist, welcher der übergeordnete Standort des neuen sekundären Standorts sein wird, wird der Befehl zum Installieren des Standorts an den ordnungsgemäßen primären Standort repliziert.  

-   Stellen Sie vor dem Starten der Installation des Standorts sicher, dass Ihr Benutzerkonto über die erforderlichen Berechtigungen verfügt und dass der Computer, der den neuen sekundären Standort hostet, alle Voraussetzungen für sekundäre Standortserver erfüllt.  

-   Wenn Sie den sekundären Standort installieren, konfiguriert Configuration Manager den neuen Standort für das Verwenden der Clientkommunikationsports, die am übergeordneten primären Standort konfiguriert sind.  

### <a name="bkmk_installsecondary"></a> So installieren Sie einen sekundären Standort  


1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**. Wählen Sie den Standort aus, der der übergeordnete primäre Standort des neuen sekundären Standorts sein wird.  

2.  Klicken Sie zum Starten des **Assistenten zum Erstellen sekundärer Standorte** auf **Sekundären Standort erstellen**.  

3.  Überprüfen Sie auf der Seite **Bevor Sie beginnen**, ob der aufgeführte primäre Standort der Standort ist, der dem neuen sekundären Standort übergeordnet sein soll. Wählen Sie anschließend **Weiter** aus.  

4.  Geben Sie auf der Seite **Allgemein** Folgendes an:  

    -   **Standortcode:** Jeder Standortcode in einer Hierarchie muss eindeutig sein und drei alphanumerische Zeichen (A bis Z und 0 bis 9) umfassen. Da der Standortcode in Ordnernamen verwendet wird, dürfen keine für Windows reservierten Namen wie die folgenden für den Standort verwendet werden:  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       > Setup überprüft nicht, ob der angegebene Standortcode bereits verwendet wird oder ein reservierter Name ist.  

    -   **Standortservername**: Dies ist der FQDN des Servers, auf dem neue sekundäre Standort installiert wird.  

    -   **Standortname:** Jeder Standort benötigt diesen Anzeigenamen, mit dem Sie den Standort bestimmen können.  

    -   **Installationsordner**: Dies ist der Ordnerpfad zur Configuration Manager-Installation. Sie können den Speicherort nach der Installation des Standorts nicht mehr ändern. Der Pfad darf keine Unicode-Zeichen oder Leerzeichen enthalten.  

    > [!IMPORTANT]  
    > Nachdem Sie die Details auf dieser Seite angeben haben, können Sie auf **Zusammenfassung** klicken, um für die übrigen Optionen für den sekundären Standort die Standardeinstellungen zu verwenden und direkt zur Seite **Zusammenfassung** des Assistenten zu gelangen.  

    > -   Verwenden Sie diese Option nur, wenn Sie mit den Standardeinstellungen des Assistenten vertraut und dies die Einstellungen sind, die Sie verwenden möchten.  
    > -   Wenn Sie die Standardeinstellungen verwenden, werden Begrenzungsgruppen nicht dem Verteilungspunkt zugeordnet. Bis Sie Begrenzungsgruppen konfigurieren, die den sekundären Standortserver enthalten, werden Clients nicht den Verteilungspunkt, der auf diesem sekundären Standort installiert ist, als Quellspeicherort für Inhalt verwenden.  

5.  Wählen Sie auf der Seite **Installationsquelldateien** aus, wie der Computer des sekundären Standorts Quelldateien für die Installation des Standorts erhält.  

     Wenn Sie im Netzwerk oder auf einem Computer des sekundären Standorts gespeicherte Dateien verwenden:  

    -   Der Speicherort der Quelldateien muss einen Ordner namens **Redist** enthalten, der alle Dateien enthält, die zuvor mithilfe des Setup-Downloadprogramms heruntergeladen wurden.  

    -   Wenn Dateien aus **Redist** nicht verfügbar sind, kann Setup den sekundären Standort nicht installieren.  

    -   Das Computerkonto des Computers des sekundären Standorts muss über die Berechtigung **Lesen** für den Quelldateiordner und die Freigabe verfügen.  

6.  Geben Sie auf der Seite **SQL Server-Einstellungen** die zu verwendende Version von SQL Server an, und konfigurieren Sie dann die entsprechenden Einstellungen.  

    > [!NOTE]  
    > Die von Ihnen auf dieser Seite eingegebenen Informationen werden von Setup erst zu Beginn der Installation überprüft. Überprüfen Sie diese Einstellungen, und setzen Sie dann den Vorgang fort.  

     **Lokale Kopie von SQL Server Express auf dem Computer des sekundären Standorts installieren und konfigurieren**  

    -   **Port des SQL Server-Diensts**: Geben Sie den SQL Server-Dienstport an, der von SQL Server Express verwendet werden soll. Der Dienstport ist in der Regel zur Verwendung von TCP-Port 1433 konfiguriert, aber Sie können auch einen anderen Port konfigurieren.  

    -   **SQL Server Broker-Port**: Geben Sie den SSB-Port (SQL Server Service Broker) an, der von SQL Server Express verwendet werden soll. Der Service Broker ist in der Regel zur Verwendung von TCP-Port 4022 konfiguriert, aber Sie können auch einen anderen Port konfigurieren. Sie müssen einen gültigen Port angeben, der von keinem anderen Standort oder Dienst verwendet wird und nicht durch Firewalleinschränkungen blockiert ist.  

    > [!IMPORTANT]  
    > Wenn SQL Server Express von Configuration Manager installiert wird, erfolgt die Installation von SQL Server Express 2012 ohne Service Pack:  

    > -   Damit der sekundäre Standort unterstützt wird, müssen Sie nach der Installation für SQL Server Express 2012 ein Upgrade auf eine [unterstützte Version](/sccm/core/plan-design/configs/support-for-sql-server-versions#bkmk_SQLVersions) durchführen.
    > -   Wenn außerdem die Installation des neuen sekundären Standorts nicht abgeschlossen wird, sondern erst die Installation von SQL Server Express 2012 beendet wird, müssen Sie die SQL Server Express-Instanz aktualisieren, bevor die Installation des sekundären Standorts von Configuration Manager erfolgreich wiederholt werden kann.  

     **Vorhandene SQL Server-Instanz verwenden**  

    -   **SQL Server-FQDN**: Prüfen Sie den FQDN des Computers, der SQL Server ausführt. Zum Hosten der sekundären Standortdatenbank müssen Sie einen lokalen Server verwenden, der SQL Server ausführt. Diese Einstellung kann nicht geändert werden.  

    -   **SQL Server-Instanz**: Geben Sie die SQL Server-Instanz an, die als sekundäre Standortdatenbank verwendet werden soll. Lassen Sie diese Option leer, wenn Sie die Standardinstanz verwenden möchten.  

    -   **Name der ConfigMgr-Standortdatenbank**: Geben Sie den Namen der sekundären Standortdatenbank an.  

    -   **SQL Server Broker-Port**: Geben Sie den SSB-Port (SQL Server Service Broker) an, der von SQL Server verwendet werden soll. Sie müssen einen gültigen Port angeben, der von keinem anderen Standort oder Dienst verwendet wird und nicht durch Firewalleinschränkungen blockiert ist.  

    > [!TIP]  
    > Eine Liste der SQL Server-Versionen, die von System Center Configuration Manager unterstützt werden, finden Sie unter [Unterstützte Versionen von SQL Server](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

7.  Auf der Seite **Verteilungspunkt** konfigurieren Sie Einstellungen für den Verteilungspunkt, der auf dem sekundären Standortserver installiert wird.  

     **Erforderliche Einstellungen:**  

    -   **Legen Sie die Art der Kommunikation zwischen Clientgeräten und Verteilungspunkt fest**: Wählen Sie HTTP oder HTTPS.  

    -   **Erstellen Sie ein selbstsigniertes Zertifikat, oder importieren Sie ein PKI-Clientzertifikat**: Wählen Sie entweder ein selbstsigniertes Zertifikat (das auch anonyme Verbindungen von Configuration Manager-Clients mit der Inhaltsbibliothek zulässt), oder importieren Sie ein Zertifikat aus Ihrer PKI.  

         Das Zertifikat wird zum Authentifizieren des Verteilungspunkts bei einem Verwaltungspunkt verwendet, bevor Statusmeldungen vom Verteilungspunkt gesendet werden.  

         Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    **Optionale Einstellungen:**  

    -   **IIS installieren und konfigurieren, sofern dies für Configuration Manager erforderlich ist**: Wählen Sie diese Einstellung, damit Configuration Manager die Internetinformationsdienste (IIS) auf dem Server installiert und konfiguriert, sofern noch nicht erfolgt. IIS müssen auf allen Verteilungspunkten installiert werden.  

        > [!NOTE]  
        > Wenngleich diese Einstellung optional ist, muss IIS auf dem Server installiert sein, bevor ein Verteilungspunkt erfolgreich installiert werden kann.  

    -   **Aktivieren und Konfigurieren von BranchCache für diesen Verteilungspunkt**.  

    -   **Beschreibung**. Dies ist eine benutzerfreundliche Beschreibung des Verteilungspunkts, um ihn leichter zu erkennen.  

    -   **Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren**.  

8.  Legen Sie auf der Seite **Laufwerkseinstellungen** die Laufwerkseinstellungen für den Verteilungspunkt des sekundären Standorts fest.  

     Sie können bis zu zwei Laufwerke für die Inhaltsbibliothek und zwei Laufwerke für die Paketfreigabe konfigurieren. Configuration Manager kann jedoch zusätzliche Laufwerke verwenden, wenn die ersten beiden die konfigurierte Laufwerksspeicherreserve erreichen. Auf der Seite **Laufwerkseinstellungen** werden die Priorität der Laufwerke und der freie Speicherplatz, der auf jedem Laufwerk verbleiben muss, festgelegt.  

    -   **Laufwerksspeicherreserve (MB):** Hiermit geben Sie an, wie viel freier Speicher auf einem Laufwerk verbleiben muss. Wird der Wert erreicht, wählt Configuration Manager ein anderes Laufwerk aus, auf dem der Kopiervorgang fortgesetzt wird. Inhaltsdateien können sich über mehrere Laufwerke erstrecken.  

    -   **Inhaltsorte**: Geben Sie die Inhaltsorte für die Inhaltsbibliothek und die Paketfreigabe an. Configuration Manager kopiert solange Inhalte zum primären Inhaltsort, bis die Menge des freien Speicherplatzes den unter **Laufwerksspeicherreserve (MB)** angegebenen Wert erreicht.

     Die Inhaltsorte sind standardmäßig auf **Automatisch**festgelegt. Der primäre Inhaltsort wird auf das Laufwerk festgelegt, das bei der Installation über den meisten Speicherplatz verfügt. Der sekundäre Inhaltsort wird auf das Laufwerk festgelegt, das nach dem primären Laufwerk über den meisten freien Speicherplatz verfügt. Wenn vom primären und sekundären Laufwerk die Laufwerksspeicherreserve erreicht wird, wählt Configuration Manager ein anderes verfügbares Laufwerk mit dem meisten freien Speicherplatz aus und setzt den Kopiervorgang dort fort.  

9. Geben Sie auf der Seite **Inhaltsprüfung** an, ob die Integrität der Inhaltsdateien am Verteilungspunkt geprüft werden soll.  

    -   Wenn Sie die Inhaltsprüfung nach einem Zeitplan aktivieren, initiiert Configuration Manager den Vorgang zum festgesetzten Zeitpunkt, und am Verteilungspunkt werden alle Inhalte geprüft.  

    -   Sie können auch die **Priorität der Inhaltsprüfung**konfigurieren.  

    -   Zum Anzeigen der Ergebnisse der Inhaltsprüfung navigieren Sie in Configuration Manager zu **Überwachung** > **Verteilungsstatus** > **Inhaltsstatus**. Der Inhalt jedes Pakettyps (z. B. Anwendung, Softwareupdatepaket und Startabbild) wird angezeigt.  

10. Auf der Seite **Begrenzungsgruppen** können Sie die Begrenzungsgruppen verwalten, denen dieser Verteilungspunkt zugewiesen ist:  

    -   Bei der Inhaltsbereitstellung müssen sich die Clients in einer dem Verteilungspunkt zugeordneten Begrenzungsgruppe befinden, damit der Verteilungspunkt als Quellort für Inhalt verwendet werden kann.  

    -   Sie können das Kontrollkästchen **Fallbackquellpfad für Inhalt zulassen** aktivieren, um Clients außerhalb solcher Begrenzungsgruppen ein Ausweichen auf den Verteilungspunkt als Quellort für den Inhalt zu ermöglichen, wenn keine bevorzugten Verteilungspunkte verfügbar sind.  

     Weitere Informationen zu bevorzugten Verteilungspunkten finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen. Klicken Sie dann auf **Weiter**, um den sekundären Standort zu installieren. Wenn der Assistent die Seite **Abschluss** anzeigt, können Sie den Assistenten schließen. Die Installation des sekundären Standorts wird im Hintergrund fortgesetzt.  


### <a name="bkmk_verify"></a> So überprüfen Sie den Installationsstatus des sekundären Standorts  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.  

2.  Wählen Sie den sekundären Standortserver aus, den Sie installieren, und klicken Sie dann auf **Installationsstatus anzeigen**.  

    > [!TIP]  
    > Wenn Sie mehrere sekundäre Standorte gleichzeitig installieren, wird die Voraussetzungsprüfung immer nur für einen Standort ausgeführt. Erst wenn diese abgeschlossen ist, wird der nächste Standort geprüft.  
