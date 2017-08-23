1.  Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Softwareupdates**.  

2.  Wählen Sie das herunterzuladende Softwareupdate mit einer der folgenden Methoden aus:  

    -   Wählen Sie unter **Softwareupdategruppen**mindestens eine Softwareupdategruppe aus. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Updategruppe** auf **Download**.  

    -   Wählen Sie unter **Alle Softwareupdates**mindestens ein Softwareupdate aus. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Update** auf **Download**.  

        > [!NOTE]  
        >  Im Knoten **Alle Softwareupdates** zeigt Configuration Manager nur Softwareupdates an, die die Klassifizierungen **Kritisch** und **Sicherheit** aufweisen, und in den letzten 30 Tagen veröffentlicht wurden.  

        > [!TIP]  
        >  Klicken Sie auf **Kriterien hinzufügen** , um die im Knoten **Alle Softwareupdates** angezeigten Softwareupdates zu filtern. Speichern Sie Suchkriterien, die Sie häufig verwenden, und verwalten Sie die gespeicherten Suchvorgänge auf der Registerkarte **Suchen** .  

         Der Assistent zum Herunterladen von Softwareupdates ****  wird geöffnet.  

3.  Konfigurieren Sie auf der Seite **Bereitstellungspaket** die folgenden Einstellungen:  

    1.  **Bereitstellungspaket auswählen**: Wählen Sie diese Einstellung aus, um ein vorhandenes Bereitstellungspaket für die in der Bereitstellung enthaltenen Softwareupdates auszuwählen.  

        > [!NOTE]  
        >  Softwareupdates, die bereits in das ausgewählte Bereitstellungspaket heruntergeladen wurden, werden nicht erneut heruntergeladen.  

    2.  **Neues Bereitstellungspaket erstellen**: Wählen Sie diese Einstellung aus, um ein neues Bereitstellungspaket für die in der Bereitstellung enthaltenen Softwareupdates zu erstellen. Konfigurieren Sie die folgenden Einstellungen:  

        -   **Name**: Gibt den Namen des Bereitstellungspakets an. Das Paket muss einen eindeutigen Namen haben, der den Paketinhalt kurz beschreibt.  Er ist auf 50 Zeichen begrenzt.  

        -   **Beschreibung**: Gibt die Beschreibung des Bereitstellungspakets an. Die Paketbeschreibung enthält Informationen zum Paketinhalt und ist auf 127 Zeichen begrenzt.  

        -   **Paketquelle**: Gibt den Speicherort der Quelldateien der Softwareupdates an. Geben Sie für den Quellspeicherort einen Netzwerkpfad wie **\\\Server\Freigabename\Pfad**ein. Alternativ können Sie auf **Durchsuchen** klicken, um den Netzwerkpfad zu suchen. Sie müssen den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets erstellen, bevor Sie mit der nächsten Seite fortfahren.  

            > [!NOTE]  
            >  Der von Ihnen angegebene Quellspeicherort des Bereitstellungspakets kann von keinem anderen Softwarebereitstellungspaket verwendet werden.  

            > [!IMPORTANT]  
            >  Das Computerkonto für den SMS-Anbieter und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen über die NTFS-Berechtigung **Schreiben** für den Downloadort verfügen. Sie müssen den Zugriff auf den Downloadort beschränken, um das Risiko zu verringern, dass Angreifer die Quelldateien der Softwareupdates manipulieren.  

            > [!IMPORTANT]  
            >  Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt von der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.  

     Klicken Sie auf **Weiter**.  

4.  Geben Sie auf der Seite **Verteilungspunkte** die Verteilungspunkte oder Verteilungspunktgruppen an, die die Softwareupdatedateien hosten. Klicken Sie dann auf **Weiter**. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurationen für Verteilungspunkte](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  Die Seite Verteilungspunkte ist nur verfügbar, wenn Sie ein neues Bereitstellungspaket für Softwareupdates erstellen.  

6.  Legen Sie auf der Seite **Verteilungseinstellungen** folgende Einstellungen fest:  

    -   **Verteilungspriorität**: Verwenden Sie diese Einstellung, um die Verteilungspriorität für das Bereitstellungspaket anzugeben. Die Verteilungspriorität gilt, wenn das Bereitstellungspaket an die Verteilungspunkte an untergeordneten Standorten gesendet wird. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: **Hoch**, **Mittel**oder **Niedrig**. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet. Standardmäßig werden Pakete mit der Priorität **Mittel** gesendet.  

    -   **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen**: Verwenden Sie diese Einstellung, um die bedarfsgesteuerte Inhaltsverteilung an bevorzugte Verteilungspunkte zu aktivieren. Wenn diese Einstellung aktiviert ist, wird vom Verwaltungspunkt ein Trigger erstellt. Mit diesem Trigger wird der Verteilungs-Manager zur Verteilung des Inhalts an alle bevorzugten Verteilungspunkte aufgefordert, wenn der Inhalt für das Paket von einem Client angefordert wird und der Inhalt auf keinem bevorzugten Verteilungspunkt verfügbar ist. Weitere Informationen zu bevorzugten Verteilungspunkten und bedarfsgesteuertem Inhalt finden Sie unter [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

    -   **Einstellungen für vorab bereitgestellten Verteilungspunkt**: Verwenden Sie diese Einstellung, um anzugeben, wie Sie Inhalte an vorab bereitgestellte Verteilungspunkte verteilen möchten. Wählen Sie eine der folgenden Optionen aus:  

        -   **Inhalt automatisch herunterladen, wenn Pakete Verteilungspunkten zugeordnet sind**: Verwenden Sie diese Einstellung, um die Einstellungen für die Vorabbereitstellung zu ignorieren und Inhalte an den Verteilungspunkt zu verteilen.  

        -   **Nur Inhaltsänderungen auf den Verteilungspunkt herunterladen**: Verwenden Sie diese Einstellung, um den ursprünglichen Inhalt am Verteilungspunkt vorab bereitzustellen und dann Inhaltsänderungen an den Verteilungspunkt zu verteilen.  

        -   **Den Inhalt dieses Pakets manuell an den Verteilungspunkt kopieren**: Verwenden Sie diese Einstellung, um Inhalte immer am Verteilungspunkt vorab bereitzustellen. Dies ist die Standardeinstellung.  

         Weitere Informationen zur Vorabbereitstellung von Inhalten für Verteilungspunkte finden Sie unter [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) (Verwenden von vorab bereitgestelltem Inhalt).  

     Klicken Sie auf **Weiter**.  

6.  Geben Sie auf der Seite **Downloadort** den Ort an, der von Configuration Manager zum Herunterladen der Quelldateien für Softwareupdates verwendet wird. Verwenden Sie ggf. die folgenden Optionen:  

    -   **Softwareupdates aus dem Internet herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates vom Speicherort im Internet herunterzuladen. Dies ist die Standardeinstellung.  

    -   **Softwareupdates von einem Pfad im lokalen Netzwerk herunterladen**: Wählen Sie diese Einstellung aus, um Softwareupdates aus einem lokalen Ordner oder aus einem freigegebenen Netzwerkordner herunterzuladen. Verwenden Sie diese Einstellung, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist.  

        > [!NOTE]  
        >  Wenn Sie diese Einstellung verwenden, laden Sie die Softwareupdates von einem beliebigen Computer mit Internetzugriff herunter. Kopieren Sie dann die Softwareupdates an einen Speicherort im lokalen Netzwerk, auf den vom Computer mit dem Assistenten zugegriffen werden kann.  

     Klicken Sie auf **Weiter**.  

7.  Geben Sie auf der Seite **Sprachauswahl** an, für welche Sprachen die ausgewählten Softwareupdates heruntergeladen werden. Klicken Sie dann auf **Weiter**. Configuration Manager lädt die Softwareupdates nur dann herunter, wenn sie in den ausgewählten Sprachen verfügbar sind. Softwareupdates, die nicht sprachspezifisch sind, werden immer heruntergeladen.  

8. Überprüfen Sie auf der Seite **Zusammenfassung** die im Assistenten ausgewählten Einstellungen. Klicken Sie dann auf **Weiter**, um die Softwareupdates herunterzuladen.  

9. Überprüfen Sie auf der Seite **Abschluss**, ob die Softwareupdates erfolgreich heruntergeladen wurden. Klicken Sie dann auf **Schließen**.  
