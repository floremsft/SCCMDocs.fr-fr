---
title: Konfigurieren der Berichterstellung | Microsoft-Dokumentation
description: "Erfahren Sie mehr über das Einrichten der Berichterstellung in der Configuration Manager-Hierarchie, einschließlich Informationen zu SQL Server Reporting Services."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 7ae6bac23e585d6f61aff0f3155d050f1b537620
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="configuring-reporting-in-system-center-configuration-manager"></a>Konfigurieren der Berichterstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können in der System Center Configuration Manager-Konsole nur dann Berichte erstellen, ändern und ausführen, nachdem Sie einige Konfigurationstasks erledigt haben. In den folgenden Abschnitten wird erläutert, wie Sie die Berichterstellung in der Configuration Manager-Hierarchie konfigurieren:  

 Lesen Sie zunächst die folgenden Themen zur Berichterstellung in Configuration Manager, bevor Sie Reporting Services in der Hierarchie installieren und konfigurieren:  

-   [Einführung in die Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md)  

-   [Planen der Berichterstellung in System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services ist eine serverbasierte Berichterstattungsplattform, von der umfassende Berichterstattungsfunktionen für zahlreiche Datenquellen bereitgestellt werden. Die Kommunikation mit SQL Server Reporting Services erfolgt über den Reporting Services-Punkt in Configuration Manager. Im Rahmen dieser Kommunikation werden Configuration Manager-Berichte in einen bestimmten Berichtsordner kopiert und Einstellungen und Sicherheitseinstellungen für Reporting Services konfiguriert. Von Reporting Services wird eine Verbindung mit der Configuration Manager-Standortdatenbank hergestellt, um Daten abzurufen, die bei der Berichtausführung zurückgegeben werden.  

 Die Installation des Reporting Services-Punkts an einem Configuration Manager-Standort ist erst möglich, nachdem Sie SQL Server Reporting Services auf dem Standortsystem, von dem die Standortsystemrolle „Reporting Services-Punkt“ gehostet wird, installiert und konfiguriert haben. Informationen zum Installieren von Reporting Services finden Sie in der [TechNet-Bibliothek zu SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=266389).  

 Gehen Sie wie folgt vor, um zu überprüfen, ob SQL Server Reporting Services ordnungsgemäß installiert ist und ausgeführt wird.  

#### <a name="to-verify-that-sql-server-reporting-services-is-installed-and-running"></a>So überprüfen Sie, ob SQL Server Reporting Services installiert ist und ausgeführt wird  

1.  Klicken Sie auf dem Desktop nacheinander auf **Start**, **Alle Programme**, **Microsoft SQL Server 2008 R2**, **Konfigurationstools**und dann auf **Konfigurations-Manager für Reporting Services**.  

2.  Geben Sie im Dialogfeld **Konfigurationsverbindung für Reporting Services** den Namen des Servers an, auf dem SQL Server Reporting Services gehostet wird. Wählen Sie im Menü die SQL Server-Instanz aus, auf der Sie SQL Reporting Services installiert haben. Klicken Sie dann auf **Verbinden**. Der Konfigurations-Manager für Reporting Services wird geöffnet.  

3.  Überprüfen Sie auf der Seite **Berichtsserverstatus** , ob für **Berichtsdienststatus** die Einstellung **Gestartet**festgelegt wurde. Ist dies nicht der Fall, klicken Sie auf **Starten**.  

4.  Klicken Sie auf der Seite **Webdienst-URL** auf die URL unter **URLs für Berichtsserver-Webdienst** , um die Verbindung mit dem Berichtsordner zu testen. Gegebenenfalls wird das Dialogfeld **Windows-Sicherheit** angezeigt, und Sie werden zur Eingabe Ihrer Sicherheitsanmeldeinformationen aufgefordert. Standardmäßig wird Ihr Benutzerkonto angezeigt. Geben Sie Ihr Kennwort ein, und klicken Sie auf **OK**. Überprüfen Sie, ob die Webseite erfolgreich geöffnet wird. Schließen Sie das Browserfenster.  

5.  Überprüfen Sie auf der Seite **Datenbank** , ob für **Berichtsservermodus** die Einstellung **Systemeigen**festgelegt ist.  

6.  Klicken Sie auf der Seite **Berichts-Manager-URL** auf die URL unter **Identifikation der Berichts-Manager-Site** , um die Verbindung mit dem virtuellen Verzeichnis für den Berichts-Manager zu testen. Gegebenenfalls wird das Dialogfeld **Windows-Sicherheit** angezeigt, und Sie werden zur Eingabe Ihrer Sicherheitsanmeldeinformationen aufgefordert. Standardmäßig wird Ihr Benutzerkonto angezeigt. Geben Sie Ihr Kennwort ein, und klicken Sie auf **OK**. Überprüfen Sie, ob die Webseite erfolgreich geöffnet wird. Schließen Sie das Browserfenster.  

    > [!NOTE]  
    >  Der Reporting Services-Berichts-Manager ist für die Berichterstellung in Configuration Manager nicht erforderlich. Er ist jedoch erforderlich, wenn Sie mit dem Berichts-Manager Berichte in einem Internetbrowser ausführen oder Berichte verwalten möchten.  

7.  Klicken Sie auf **Beenden**, um Configuration Manager für Reporting Services zu schließen.  

##  <a name="BKMK_ReportBuilder3"></a> Konfigurieren der Berichterstellung zur Verwendung von Report Builder 3.0  

#### <a name="to-change-the-report-builder-manifest-name-to-report-builder-30"></a>So ändern Sie den Manifestnamen von Report Builder in Report Builder 3.0  

1.  Öffnen Sie auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, den Windows-Registrierungs-Editor.  

2.  Suchen Sie **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**.  

3.  Doppelklicken Sie auf den Schlüssel **ReportBuilderApplicationManifestName** , um den Wert zu bearbeiten.  

4.  Ändern Sie **ReportBuilder_2_0_0_0.application** in **ReportBuilder_3_0_0_0.application**. Klicken Sie dann auf **OK**.  

5.  Schließen Sie den Windows Registrierungs-Editor.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Installieren eines Reporting Services-Punkts  
 Damit an einem Standort Berichte verwaltet werden können, muss der Reporting Services-Punkt an diesem Standort installiert sein. Vom Reporting Services-Punkt werden Berichtsordner und Berichte nach SQL Server Reporting Services kopiert, die Sicherheitsrichtlinie für die Berichte und Ordner angewendet und Konfigurationseinstellungen in Reporting Services festgelegt. Sie müssen einen Reporting Services-Punkt konfigurieren, damit Berichte in der Configuration Manager-Konsole angezeigt werden und Sie die Berichte in Configuration Manager verwalten können. Der Reporting Services-Punkt ist eine Standortsystemrolle. Diese muss auf einem Server konfiguriert sein, auf dem Microsoft SQL Server Reporting Services installiert ist und ausgeführt wird. Weitere Informationen zu Voraussetzungen finden Sie unter [Voraussetzungen für die Berichterstellung in Configuration Manager](prerequisites-for-reporting.md).  

> [!IMPORTANT]  
>  Bedenken Sie bei der Auswahl eines Reporting Services-Punkts, dass die Benutzer, die auf Berichte zugreifen werden, sich im selben Sicherheitsbereich wie der Standort befinden müssen, an dem der Reporting Services-Punkt installiert ist.  

> [!NOTE]  
>  Lassen Sie die URL des Berichtsservers unverändert, nachdem Sie einen Reporting Services-Punkts in einem Standortsystem installiert haben. Angenommen, Sie erstellen den Reporting Services-Punkt und ändern dann im Configuration Manager für Reporting Services die URL des Berichtsservers. Da die alte URL weiterhin von Configuration Manager verwendet wird, ist es nicht möglich, Berichte über die Konsole auszuführen, zu bearbeiten oder zu erstellen. Falls Sie den URL-Berichtsserver ändern müssen, entfernen Sie zuerst den Reporting Services-Punkt. Ändern Sie dann die URL, und installieren Sie den Reporting Services-Punkt neu.  

> [!IMPORTANT]    
> Wenn Sie einen Reporting Services-Punkt installieren, müssen Sie das Konto eines Reporting Services-Punkts angeben. Wenn Benutzer aus einer anderen Domäne dann versuchen, einen Bericht auszuführen, kann der Bericht nur ausgeführt werden, sofern eine bidirektionale Vertrauensstellung zwischen den Domänen eingerichtet ist.

 Gehen Sie wie folgt vor, um den Reporting Services-Punkt zu installieren.  

#### <a name="to-install-the-reporting-services-point-on-a-site-system"></a>So installieren Sie den Reporting Services-Punkt in einem Standortsystem  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Server und Standortsystemrollen**.  

    > [!TIP]  
    >  Sollen nur die Standortsysteme aufgeführt werden, auf denen die Standortsystemrolle „Reporting Services-Punkt“ gehostet wird, klicken Sie mit der rechten Maustaste auf **Server und Standortsystemrollen** , und wählen Sie **Reporting Services-Punkt**aus.  

3.  Fügen Sie die Standortsystemrolle „Reporting Services-Punkt“ einem neuen oder vorhandenen Standortsystemserver wie folgt hinzu:  

    > [!NOTE]  
    >  Weitere Informationen zum Konfigurieren von Standortsystemen finden Sie unter [Hinzufügen von Standortsystemrollen für System Center Configuration Manager](../deploy/configure/add-site-system-roles.md).  

    -   **Neues Standortsystem**: Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Standortsystemserver erstellen**. Der ****  Assistent zum Erstellen von Standortsystemservern wird geöffnet.  

    -   **Vorhandenes Standortsystem**: Klicken Sie auf den Server, auf dem die Standortsystemrolle „Reporting Services-Punkt“ installiert werden soll. Wenn Sie auf einen Server klicken, wird im Ergebnisbereich eine Liste der Standortsystemrollen angezeigt, die bereits auf dem Server installiert sind.  

         Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen**. Der ****  Assistent zum Hinzufügen von Standortsystemrollen wird geöffnet.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an. Soll die Standortsystemrolle „Reporting Services-Punkt“ einem vorhandenen Standortsystemserver hinzugefügt werden, überprüfen Sie die Werte, die Sie zuvor konfiguriert haben.  

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen den Eintrag **Reporting Services-Punkt** aus. Klicken Sie dann auf **Weiter**.  

6.  Konfigurieren Sie auf der Seite **Reporting Services-Punkt** die folgenden Einstellungen:  

    -   **Name des Standortdatenbankservers**: Geben Sie den Namen des Servers an, auf dem die Configuration Manager-Standortdatenbank gehostet wird. Der vollqualifizierte Domänenname (FQDN) für den Server wird vom Assistenten in der Regel automatisch abgerufen. Zur Angabe einer Datenbankinstanz verwenden Sie das Format &lt;*Servername*>\&lt;*Instanzname*>.  

    -   **Datenbankname**: Geben Sie den Namen der Configuration Manager-Standortdatenbank an. Klicken Sie dann auf **Überprüfen**, um zu bestätigen, dass der Assistent auf die Standortdatenbank zugreifen kann.  

        > [!IMPORTANT]  
        >  Das Benutzerkonto, von dem der Reporting Services-Punkt erstellt wird, muss für die Standortdatenbank die Berechtigung **Lesen** haben. Wenn beim Verbindungstest ein Fehler auftritt, wird ein rotes Warnsymbol angezeigt. Bewegen Sie den Cursor auf dieses Symbol, um die Details zum Fehler zu lesen. Korrigieren Sie den Fehler, und klicken Sie dann erneut auf **Test** .  

    -   **Ordnername**: Geben Sie den Namen des Ordners an, der erstellt wird und in dem die Configuration Manager-Berichte von Reporting Services abgelegt werden.  

    -   **Reporting Services-Serverinstanz**: Wählen Sie in der Liste die SQL Server-Instanz für Reporting Services aus. Wird nur eine Instanz gefunden, so wird diese standardmäßig aufgeführt und ausgewählt. Werden keine Instanzen gefunden, überprüfen Sie, ob SQL Server Reporting Services installiert und konfiguriert ist. Überprüfen Sie ferner, ob der Dienst „SQL Server Reporting Services“ im Standortsystem gestartet wurde.  

        > [!IMPORTANT]  
        >  Von Configuration Manager wird im Kontext des aktuellen Benutzers eine Verbindung mit Windows Management Instrumentation (WMI) im ausgewählten Standortsystem hergestellt, um die SQL Server-Instanz für Reporting Services abzurufen. Der aktuelle Benutzer muss über die Berechtigung **Lesen** für WMI auf dem Standortsystem verfügen. Andernfalls können die Reporting Services-Instanzen nicht abgerufen werden.  

    -   **Konto des Reporting Services-Punkts**: Klicken Sie auf **Festlegen**. Wählen Sie dann ein Konto aus, über das von SQL Server Reporting Services auf dem Reporting Services-Punkt eine Verbindung mit der Configuration Manager-Standortdatenbank hergestellt wird, um die in einem Bericht angezeigten Daten abzurufen. Wählen Sie **Vorhandenes Konto** aus, um ein Windows-Benutzerkonto anzugeben, das zuvor als Configuration Manager-Konto konfiguriert wurde. Wählen Sie **Neues Konto** aus, um ein Windows-Benutzerkonto anzugeben, das derzeit nicht als Configuration Manager-Konto konfiguriert ist. Dem angegebenen Benutzer wird von Configuration Manager automatisch Zugriff auf die Standortdatenbank erteilt. Der Benutzer wird im Arbeitsbereich **Verwaltung** im Knoten **Sicherheit** mit dem Kontonamen **ConfigMgr Reporting Services-Punkt** im Unterordner **Konten** angezeigt.  

         Das Konto, über das Reporting Services ausgeführt werden, muss zur lokalen Sicherheitsgruppe **Windows-Autorisierungszugriffsgruppe**der Domäne gehören, und die Berechtigung **„tokenGroupsGlobalAndUniversal“ lesen** des Kontos muss auf **Zulassen**festgelegt sein. Es muss eine bidirektionale Vertrauensstellung für Benutzer eingerichtet werden, die zu einer anderen Domäne als das Konto des Reporting Services-Punkts gehören, um erfolgreich Berichte auszuführen.

         Das angegebene Windows-Benutzerkonto und das zugehörige Kennwort werden verschlüsselt und in der Reporting Services-Datenbank gespeichert. Die Daten werden von Reporting Services über dieses Konto und Kennwort aus der Standortdatenbank abgerufen und für Berichte verwendet.  

        > [!IMPORTANT]  
        >  Das angegebene Konto muss auf dem Computer, auf dem die Reporting Services-Datenbank gehostet wird, über die Berechtigung zur **Lokalen Anmeldung** verfügen.  

7.  Klicken Sie auf der Seite **Reporting Services-Punkt** auf **Weiter**.  

8.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen. Klicken Sie dann auf **Weiter** , um den Reporting Services-Punkt zu installieren.  

     Wenn der Assistent abgeschlossen wurde, werden Berichtsordner erstellt, und die Configuration Manager-Berichte werden in die angegebenen Berichtsordner kopiert.  

    > [!NOTE]  
    >  Wenn Berichtsordner erstellt und Berichte auf den Berichtsserver kopiert werden, wird von Configuration Manager die geeignete Sprache für die Objekte ermittelt. Wenn das zugeordnete Sprachpaket an dem Standort installiert ist, werden die Objekte von Configuration Manager in der Sprache des Betriebssystems erstellt, das am Standort auf dem Berichtsserver ausgeführt wird. Falls die Sprache nicht verfügbar ist, werden die Berichte in Englisch erstellt und angezeigt. Die Berichte werden auch in Englisch installiert, wenn Sie einen Reporting Services-Punkt an einem Standort ohne Sprachpakete installieren. Wenn Sie ein Sprachpaket nach der Installation des Reporting Services-Punkts installieren, müssen Sie den Reporting Services-Punkt deinstallieren und neu installieren, damit die Berichte in der Sprache des gewünschten Sprachpakets verfügbar sind. Weitere Informationen zu Sprachpaketen finden Sie unter [Sprachpakete in System Center Configuration Manager](../deploy/install/language-packs.md).  

###  <a name="BKMK_FileInstallationAndSecurity"></a> Dateiinstallation und Sicherheitsrechte für Berichtsordner  
 Zur Installation des Reporting Services-Punkts und zur Konfiguration von Reporting Services werden von Configuration Manager die folgenden Aktionen ausgeführt:  

> [!IMPORTANT]  
>  Die in der folgenden Listen genannten Aktionen werden mithilfe der Anmeldeinformationen des für den SMS_Executive-Dienst konfigurierten Kontos ausgeführt. Bei diesem Konto handelt es sich in der Regel um das lokale Systemkonto des Standortservers.  

-   Installation der Standortsystemrolle „Reporting Services-Punkt“  

-   Erstellen der Datenquelle in Reporting Services mithilfe der gespeicherten Anmeldeinformationen, die Sie im Assistenten festgelegt haben. Dabei handelt es sich um das Windows-Benutzerkonto und das dazugehörende Kennwort, über die von Reporting Services eine Verbindung mit der Standortdatenbank hergestellt wird, wenn Sie Berichte ausführen.  

-   Erstellen des Configuration Manager-Stammordners in Reporting Services  

-   Hinzufügen der Sicherheitsrollen **ConfigMgr-Berichtbenutzer** und **ConfigMgr-Berichtadministratoren** in Reporting Services  

-   Erstellen von Unterordnern und Bereitstellen von Configuration Manager-Berichten aus „%ProgramFiles%\SMS _SRSRP“ für Reporting Services  

-   Hinzufügen der Rolle **ConfigMgr-Berichtbenutzer** in Reporting Services zu den Stammordnern für alle Benutzerkonten in Configuration Manager, die über **Leseberechtigungen für den Standort** verfügen  

-   Hinzufügen der Rolle **ConfigMgr-Berichtadministratoren** in Reporting Services zu den Stammordnern für alle Benutzerkonten in Configuration Manager, die über **Berechtigungen zum Ändern des Standorts** verfügen  

-   Abrufen der Zuordnung zwischen Berichtordnern und den von Configuration Manager gesicherten Objekttypen (aus der Configuration Manager-Standortdatenbank)  

-   Konfigurieren der folgenden Rechte für bestimmte Berichtordner in Reporting Services für Administratoren in Configuration Manager:  

    -   Hinzufügen von Benutzern und Zuweisen der Rolle **ConfigMgr-Berichtbenutzer** zum zugeordneten Berichtordner für Administratoren, die über die Berechtigung **Bericht ausführen** für das Configuration Manager-Objekt verfügen  

    -   Hinzufügen von Benutzern und Zuweisen der Rolle **ConfigMgr-Berichtadministratoren** zum zugeordneten Berichtordner für Administratoren, die über die Berechtigung **Bericht ändern** für das Configuration Manager-Objekt verfügen  

     Von Configuration Manager wird eine Verbindung mit Reporting Services hergestellt. Dann werden die Berechtigungen der Benutzer für die Configuration Manager- und Reporting Services-Stammordner sowie für bestimmte Berichtordner festgelegt. Nach der Erstinstallation des Reporting Services-Punkts wird von Configuration Manager alle 10 Minuten eine Verbindung mit Reporting Services hergestellt, um zu überprüfen, ob es sich bei den für die Berichtsordner konfigurierten Benutzerrechten um die entsprechenden Rechte handelt, die für Configuration Manager-Benutzer festgelegt wurden. Wenn mit dem Reporting Services Berichts-Manager Benutzer hinzugefügt bzw. Benutzerrechte für den Berichtordner geändert werden, werden diese Änderungen mithilfe der in der Standortdatenbank gespeicherten rollenbasierten Zuweisungen von Configuration Manager überschrieben. Configuration Manager entfernt auch Benutzer, die nicht zur Berichterstellung in Configuration Manager berechtigt sind.  

##  <a name="BKMK_SecurityRoles"></a> Reporting Services-Sicherheitsrollen für Configuration Manager  
 Wenn von Configuration Manager der Reporting Services-Punkt installiert wird, werden in Reporting Services die folgenden Sicherheitsrollen hinzugefügt:  

-   **ConfigMgr-Berichtsbenutzer**: Benutzer, denen diese Sicherheitsrolle zugewiesen ist, können nur Configuration Manager-Berichte ausführen.  

-   **ConfigMgr-Berichtsadministratoren**: Benutzer, denen diese Sicherheitsrolle zugewiesen ist, können in Configuration Manager alle auf die Berichterstellung bezogenen Tasks ausführen.  

##  <a name="BKMK_VerifyReportingServicesPointInstallation"></a> Überprüfen der Installation des Reporting Services-Punkts  
 Nachdem Sie die Standortsystemrolle „Reporting Services-Punkt“ hinzugefügt haben, können Sie die Installation anhand bestimmter Statusmeldungen und Protokolldateieinträge überprüfen. Gehen Sie wie folgt vor, um zu überprüfen, ob der Reporting Services-Punkt erfolgreich installiert wurde.  

> [!WARNING]  
>  Sie können dieses Verfahren überspringen, wenn im Arbeitsbereich **Überwachung** der Configuration Manager-Konsole im Unterordner **Berichte** des Knotens **Berichterstellung** Berichte angezeigt werden.  

#### <a name="to-verify-the-reporting-services-point-installation"></a>So überprüfen Sie die Installation des Reporting Services-Punkts  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Eintrag **Systemstatus**, und klicken Sie dann auf **Komponentenstatus**.  

3.  Klicken Sie in der Komponentenliste auf **SMS_SRS_REPORTING_POINT** .  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Komponente** auf **Meldungen anzeigen**und dann auf **Alle**.  

5.  Geben Sie ein Datum und eine Uhrzeit für einen Zeitraum vor der Installation des Reporting Services-Punkts an, und klicken Sie dann auf **OK**.  

6.  Überprüfen Sie, ob Statusmeldungs-ID 1015 aufgelistet ist, die darauf hinweist, dass der Reporting Services-Punkt erfolgreich installiert wurde. Sie können auch die Datei „Srsrp.log“ öffnen, die sich unter &lt;*ConfigMgr-Installationspfad*>\Logs befindet, und nach **Die Installation war erfolgreich** suchen.  

     Navigieren Sie in Windows-Explorer zu &lt;*ConfigMgr-Installationspfad*>\Logs.  

7.  Öffnen Sie Srsrp.log, und sehen Sie die Protokolldatei ab dem Zeitpunkt der erfolgreichen Installation des Reporting Services-Punkts schrittweise durch. Überprüfen Sie, ob die Berichtsordner erstellt, die Berichte bereitgestellt und die Sicherheitsrichtlinie für jeden Ordner bestätigt wurden. Suchen Sie nach der letzten Zeile der Bestätigungen für die Sicherheitsrichtlinie nach dem Text **Integrität des SRS-Webdiensts erfolgreich überprüft auf Server** .  

##  <a name="BKMK_Certificate"></a> Konfigurieren eines selbstsignierten Zertifikats für Configuration Manager-Konsolencomputer  
 Es gibt zahlreiche Möglichkeiten, Berichte für SQL Server Reporting Services zu erstellen. Beim Erstellen oder Bearbeiten von Berichten in der Configuration Manager-Konsole wird der Berichts-Generator von Configuration Manager als Erstellungsumgebung geöffnet. Unabhängig von der Erstellungsmethode für Configuration Manager-Berichte ist ein selbstsigniertes Zertifikat für die Serverauthentifizierung beim Standortdatenbankserver erforderlich. Von Configuration Manager wird das Zertifikat automatisch auf dem Standortserver und auf den Computern mit dem SMS-Anbieter installiert. Daher können Sie Berichte mithilfe der Configuration Manager-Konsole erstellen und bearbeiten, wenn sie auf einem dieser Computer ausgeführt wird. Wenn Sie dagegen Berichte mithilfe einer Configuration Manager-Konsole erstellen oder ändern, die auf einem anderen Computer installiert ist, müssen Sie das Zertifikat vom Standortserver exportieren und anschließend dem Zertifikatspeicher **Vertrauenswürdige Personen** auf dem Computer hinzufügen, auf dem die Configuration Manager-Konsole ausgeführt wird.  

> [!NOTE]  
>  Weitere Informationen zu anderen Berichterstellungsumgebungen für SQL Server Reporting Services finden Sie unter [Vergleichen von Berichterstellungsumgebungen](http://go.microsoft.com/fwlink/p/?LinkId=242805) in der Onlinedokumentation zu SQL Server 2008.  

 Verwenden Sie das folgende Verfahren als Beispiel für das Übertragen einer Kopie des selbstsignierten Zertifikats vom Standortserver auf einen anderen Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, wenn auf beiden Computern Windows Server 2008 R2 ausgeführt wird. Wenn Sie dieses Verfahren nicht anwenden können, weil Sie über eine andere Betriebssystemversion verfügen, führen Sie das entsprechende Verfahren in der Dokumentation Ihres Betriebssystems aus.  

#### <a name="to-transfer-a-copy-of-self-signed-certificate-from-the-site-server-to-another-computer"></a>So übertragen Sie eine Kopie eines selbstsignierten Zertifikats vom Standortserver auf einen anderen Computer  

1.  Führen Sie die folgenden Schritte auf dem Standortserver aus, um das selbstsignierte Zertifikat zu exportieren:  

    1.  Klicken Sie auf **Start**, dann auf **Ausführen**, und geben Sie **mmc.exe**ein. Klicken Sie in der leeren Konsole auf **Datei**und anschließend auf **Snap-In hinzufügen/entfernen**.  

    2.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate**aus, und klicken Sie dann auf **Hinzufügen**.  

    3.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto**aus, und klicken Sie auf **Weiter**.  

    4.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Klicken Sie anschließend auf **Fertig stellen**.  

    5.  Klicken Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** auf **OK**.  

    6.  Erweitern Sie in der Konsole den Bereich **Zertifikate (Lokaler Computer)**, dann den Bereich **Vertrauenswürdige Personen**, und wählen Sie **Zertifikate**aus.  

    7.  Klicken Sie mit der rechten Maustaste auf das Zertifikat mit dem Anzeigenamen &lt;*FQDN des Standortservers*>, klicken Sie auf **Alle Tasks**, und wählen Sie anschließend **Exportieren** aus.  

    8.  Schließen Sie den ****  Assistenten zum Exportieren von Zertifikaten mit den Standardoptionen ab, und speichern Sie das Zertifikat mit der Dateinamenerweiterung **.cer** .  

2.  Führen Sie die folgenden Schritte auf dem Computer aus, auf dem die Configuration Manager-Konsole ausgeführt wird, um das selbstsignierte Zertifikat dem Zertifikatspeicher „Vertrauenswürdige Personen“ hinzuzufügen:  

    1.  Wiederholen Sie die Schritte 1.a bis 1.e um das MMC-Snap-In **Zertifikat** auf dem Verwaltungspunktcomputer zu konfigurieren.  

    2.  Erweitern Sie in der Konsole den Bereich **Zertifikate (Lokaler Computer)**, dann den Bereich **Vertrauenswürdige Personen**, klicken Sie mit der rechten Maustaste auf **Zertifikate**, wählen Sie **Alle Tasks**aus, und wählen Sie dann **Importieren** aus, um den **** Zertifikatimport-Assistenten zu starten.  

    3.  Wählen Sie auf der Seite **Importdatei** das in Schritt 1.h gespeicherte Zertifikat aus, und klicken Sie dann auf **Weiter**.  

    4.  Wählen Sie auf der Seite **Zertifikatspeicher** die Option **Alle Zertifikate in folgendem Speicher speichern**aus, legen Sie **Zertifikatspeicher** auf **Vertrauenswürdige Personen**fest, und klicken Sie dann auf **Weiter**.  

    5.  Klicken Sie auf **Fertig stellen** , um den Assistenten zu schließen und die Zertifikatkonfiguration für den Computer abzuschließen.  

##  <a name="BKMK_ModifyReportingServicesPoint"></a> Ändern der Einstellungen des Reporting Services-Punkts  
 Nach der Installation des Reporting Services-Punkts können Sie die Einstellungen für Standortdatenbankverbindung und Authentifizierung in den Eigenschaften des Reporting Services-Punkts konfigurieren. Gehen Sie wie folgt vor, um die Einstellungen des Reporting Services-Punkts zu ändern.  

#### <a name="to-modify-reporting-services-point-settings"></a>So ändern Sie die Einstellungen des Reporting Services-Punkts  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Server und Standortsystemrollen** , um die Standortsysteme aufzulisten.  

    > [!TIP]  
    >  Sollen nur die Standortsysteme aufgeführt werden, auf denen die Standortsystemrolle „Reporting Services-Punkt“ gehostet wird, klicken Sie mit der rechten Maustaste auf **Server und Standortsystemrollen** , und wählen Sie **Reporting Services-Punkt**aus.  

3.  Wählen Sie das Standortsystem aus, auf dem der Reporting Services-Punkt gehostet wird, dessen Einstellungen Sie ändern möchten, und wählen Sie dann in **Standortsystemrollen** die Option **Reporting Services-Punkt**aus.  

4.  Klicken Sie auf der Registerkarte **Standortrolle** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Im Dialogfeld **Eigenschaften des Reporting Services-Punkts** können Sie die folgenden Einstellungen ändern:  

    -   **Name des Standortdatenbankservers**: Geben Sie den Namen des Servers an, auf dem die Configuration Manager-Standortdatenbank gehostet wird. Der vollqualifizierte Domänenname (FQDN) für den Server wird vom Assistenten in der Regel automatisch abgerufen. Zur Angabe einer Datenbankinstanz verwenden Sie das Format &lt;*Servername*>\&lt;*Instanzname*>.  

    -   **Datenbankname**: Geben Sie den Namen der System Center 2012 Configuration Manager-Standortdatenbank an. Klicken Sie anschließend auf **Überprüfen**, um zu bestätigen, dass der Assistent auf die Standortdatenbank zugreifen kann.  

        > [!IMPORTANT]  
        >  Für das Benutzerkonto, von dem der Reporting Services-Punkt erstellt wird, muss die Berechtigung Lesen für die Standortdatenbank vorliegen. Wenn beim Verbindungstest ein Fehler auftritt, wird ein rotes Warnsymbol angezeigt. Bewegen Sie den Cursor auf dieses Symbol, um die Details zum Fehler zu lesen. Korrigieren Sie den Fehler, und klicken Sie dann erneut auf **Test** .  

    -   **Benutzerkonto**: Klicken Sie auf **Festlegen**. Wählen Sie anschließend ein Konto aus, über das von SQL Server Reporting Services auf dem Reporting Services-Punkt eine Verbindung mit der Configuration Manager-Standortdatenbank hergestellt wird, um die in einem Bericht angezeigten Daten abzurufen. Wählen Sie **Vorhandenes Konto** aus, um ein Windows-Benutzerkonto mit vorhandenen Configuration Manager-Rechten anzugeben. Wählen Sie **Neues Konto** aus, um ein Windows-Benutzerkonto anzugeben, für das derzeit keine Rechte in Configuration Manager vorhanden sind. Dem angegebenen Benutzerkonto wird von Configuration Manager automatisch Zugriff auf die Standortdatenbank erteilt. Das Konto wird im Arbeitsbereich **Verwaltung** im Knoten **Sicherheit** im Unterordner **Konten** als **ConfigMgr SRS-Berichterstattungspunkt** -Konto angezeigt.  

         Das angegebene Windows-Benutzerkonto und das zugehörige Kennwort werden verschlüsselt und in der Reporting Services-Datenbank gespeichert. Die Daten werden von Reporting Services über dieses Konto und Kennwort aus der Standortdatenbank abgerufen und für Berichte verwendet.  

        > [!IMPORTANT]  
        >  Befindet sich die Standortdatenbank auf einem Remotestandortsystem, muss das angegebene Konto auf dem Computer zur lokalen Anmeldung ****  berechtigt sein.  

6.  Klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld zu schließen.  

## <a name="upgrading-sql-server"></a>Ausführen eines Upgrades von SQL Server  
 Nach dem Ausführen eines Upgrades von SQL Server und der SQL Server Reporting Services-Anwendung, die als Datenquelle für einen Reporting Services-Punkt dient, treten möglicherweise Fehler auf, wenn Sie Berichte über die Configuration Manager-Konsole ausführen oder bearbeiten. Damit die Berichterstellung über die Configuration Manager-Konsole richtig funktioniert, müssen Sie die Standortsystemrolle des Reporting Services-Punkts für den Standort entfernen und neu installieren. Nach Abschluss des Upgrades können Sie Berichte jedoch weiterhin mit einem Internetbrowser ausführen und bearbeiten.  

##  <a name="BKMK_ConfigureReportOptions"></a> Konfigurieren von Berichtsoptionen  
 Verwenden Sie die Berichtsoptionen für einen Configuration Manager-Standort, um den Reporting Services-Punkt auszuwählen, der standardmäßig zur Verwaltung Ihrer Berichte verwendet wird. Zwar können auf einem Standort mehrere Reporting Services-Punkte vorhanden sein, die Verwaltung von Berichten kann jedoch nur über den Standardberichtsserver erfolgen, der in den Berichtsoptionen ausgewählt wurde. Gehen Sie wie folgt vor, um Berichtoptionen für Ihren Standort zu konfigurieren.  

#### <a name="to-configure-report-options"></a>So konfigurieren Sie Berichtsoptionen  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Berichterstattung**, und klicken Sie dann auf **Berichte**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Berichtsoptionen**.  

4.  Wählen Sie in der Liste den Standardberichtsserver aus, und klicken Sie dann auf **OK**. Wenn keine Reporting Services-Punkte aufgelistet sind, vergewissern Sie sich, dass der Reporting Services-Punkt auf dem Standort erfolgreich installiert und konfiguriert wurde.  

## <a name="next-steps"></a>Nächste Schritte
[Vorgänge und Wartungstasks für die Berichterstellung](operations-and-maintenance-for-reporting.md)
