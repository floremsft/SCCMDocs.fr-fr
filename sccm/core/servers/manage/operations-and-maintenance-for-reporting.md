---
title: "Vorgänge und Wartungstasks für die Berichterstellung | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über das Verwalten von Berichten und Berichtsabonnements in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
caps.latest.revision: "5"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: df572cd0c64c82e25164430a53e1b893b3ba3cf5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="operations-and-maintenance-for-reporting-in-system-center-configuration-manager"></a>Vorgänge und Wartungstasks für die Berichterstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Es gibt mehrere Operationen, die Sie normalerweise ausführen, um Berichte und Berichtsabonnements zu verwalten, wenn die Infrastruktur vorhanden ist, die für die Berichterstellung in System Center Configuration Manager erforderlich ist.  

##  <a name="BKMK_ManageReports"></a> Verwalten von Configuration Manager-Berichten  
 In Configuration Manager sind über 400 vordefinierte Berichte verfügbar. Diese können Sie nutzen, um Informationen zu Benutzern, Hardware- und Softwareinventar, Softwareupdates, Anwendungen, Standortstatus und anderen Configuration Manager-Operationen in Ihrer Organisation zu erfassen, zu organisieren und darzustellen. Sie können die vordefinierten Berichte so verwenden, wie sie sind, oder sie nach Ihren Anforderungen ändern. Sie können auch benutzerdefinierte modell\- und SQL\-basierte Berichte nach Ihren Anforderungen erstellen. In den folgenden Abschnitten finden Sie Informationen zum Verwalten von Configuration Manager-Berichten.  

###  <a name="BKMK_RunReport"></a> Ausführen eines Configuration Manager-Berichts  
 Berichte in Configuration Manager in SQL Server Reporting Services gespeichert sind, und die Daten im Bericht gerendert werden aus der Configuration Manager-Datenbank abgerufen. Sie können Berichte in Configuration Manager-Konsole oder mithilfe des Berichts-Manager, die Sie in einem Webbrowser zugreifen zugreifen. Sie können Berichte auf jedem Computer öffnen, von dem aus Sie auf den Computer zugreifen können, auf dem SQL Server Reporting Services ausgeführt werden. Sie benötigen allerdings entsprechende Rechte, um die Berichte anzuzeigen. Wenn Sie einen Bericht ausführen, werden Titel, Beschreibung und Kategorie des Berichts in der Sprache des lokalen Betriebssystems angezeigt.  

> [!NOTE]  
>  In bestimmten anderen Sprachen als Englisch werden Zeichen in Berichten möglicherweise nicht richtig angezeigt.  In diesem Fall können die Berichte mithilfe des webbasierten Berichts-Managers oder über die Remoteadministratorkonsole angezeigt werden.  

> [!WARNING]  
>  Zum Ausführen von Berichten benötigen Sie das Recht **Lesen** für die Berechtigung **Standort** sowie die Berechtigung **Bericht ausführen** , die für bestimmte Objekte konfiguriert ist.  

> [!IMPORTANT]    
> Es muss eine bidirektionale Vertrauensstellung für Benutzer eingerichtet werden, die zu einer anderen Domäne als das Konto des Reporting Services-Punkts gehören, um erfolgreich Berichte auszuführen.

> [!NOTE]  
>  Der Berichts-Manager ist ein webbasiertes Zugriffs- und Verwaltungstool für Berichte. Sie können ihn zum Verwalten einer einzelnen Berichtsserverinstanz an einem Remotestandort mithilfe einer HTTP-Verbindung verwenden. Sie können den Berichts-Manager für Betriebstasks einsetzen, beispielsweise um Berichte anzuzeigen, Berichtseigenschaften zu ändern und zugeordnete Berichtsabonnements zu verwalten. In diesem Thema finden Sie die Schritte zum Anzeigen eines Berichts und zum Ändern der Berichtseigenschaften im Berichts-Manager. Weitere Informationen zu den anderen Optionen vom Berichts-Manager finden Sie unter [Berichts-Manager](http://go.microsoft.com/fwlink/p/?LinkId=224916) in der SQL Server 2008-Onlinedokumentation.  

 Verwenden Sie die folgenden Verfahren, um Configuration Manager-Berichten auszuführen.  

##### <a name="to-run-a-report-in-the-configuration-manager-console"></a>Ausführen eines Berichts in der Configuration Manager-Konsole  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Berichterstattung**, und klicken Sie dann auf **Berichte** , um die verfügbaren Berichte aufzulisten.  

    > [!IMPORTANT]  
    >  In dieser Version von Configuration Manager werden in Berichten des Typs **Gesamter Inhalt** nur Pakete, nicht aber Anwendungen angezeigt.  

    > [!TIP]  
    >  Wenn keine Berichte aufgelistet werden, vergewissern Sie sich, dass der Reporting Services-Punkt installiert und konfiguriert ist. Weitere Informationen finden Sie unter [Konfigurieren von Berichten](configuring-reporting.md).  

3.  Wählen Sie den Bericht aus, der ausgeführt werden soll, und klicken Sie dann auf der Registerkarte **Startseite** im Bereich **Berichtsgruppe** auf **Ausführen** , um den Bericht zu öffnen.  

4.  Wenn Parameter erforderlich sind, geben Sie die Parameter an, und klicken Sie dann auf **Bericht anzeigen**.  

#### <a name="to-run-a-report-in-a-web-browser"></a>So führen Sie einen Bericht in einem Webbrowser aus  

1.  Geben Sie die URL des Berichts-Managers in Ihren Webbrowser ein, beispielsweise **http:\/\/Server1\/Reports**. Sie können die URL des Berichts-Managers bestimmen, auf die **URL des Berichts-Managers** Seite in Configuration Manager für Reporting Services.  

2.  Klicken Sie im Berichts-Manager auf den Berichtsordner für Configuration Manager, z.B. **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Wenn keine Berichte aufgelistet werden, vergewissern Sie sich, dass der Reporting Services-Punkt installiert und konfiguriert ist. Weitere Informationen finden Sie unter [Konfigurieren von Berichten](configuring-reporting.md).  

3.  Klicken Sie auf die Berichtskategorie des Berichts, den Sie ausführen möchten, und dann auf den Link zum Bericht. Der Bericht wird im Berichts-Manager geöffnet.  

4.  Wenn Parameter erforderlich sind, geben Sie die Parameter an, und klicken Sie dann auf **Bericht anzeigen**.  

###  <a name="BKMK_ModifyReportProperties"></a> Ändern der Eigenschaften eines Configuration Manager-Berichts  
 In der Configuration Manager-Konsole können Sie die Eigenschaften eines Berichts anzeigen, beispielsweise Namen und Beschreibung des Berichts. Zum Ändern der Eigenschaften verwenden Sie jedoch den Berichts-Manager. Wenden Sie das folgende Verfahren an, um die Eigenschaften eines Configuration Manager-Berichts zu ändern.  

#### <a name="to-modify-report-properties-in-report-manager"></a>So ändern Sie Berichtseigenschaften im Berichts-Manager  

1.  Geben Sie die URL des Berichts-Managers in Ihren Webbrowser ein, beispielsweise **http:\/\/Server1\/Reports**. Sie können die URL des Berichts-Managers bestimmen, auf die **URL des Berichts-Managers** Seite in Configuration Manager für Reporting Services.  

2.  Klicken Sie im Berichts-Manager auf den Berichtsordner für Configuration Manager, z.B. **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Wenn keine Berichte aufgelistet werden, vergewissern Sie sich, dass der Reporting Services-Punkt installiert und konfiguriert ist. Weitere Informationen finden Sie unter [Konfigurieren von Berichten](configuring-reporting.md)  

3.  Klicken Sie auf die Berichtskategorie des Berichts, dessen Eigenschaften Sie ändern möchten, und dann auf den Link zum Bericht. Der Bericht wird im Berichts-Manager geöffnet.  

4.  Klicken Sie auf die Registerkarte **Eigenschaften** . Sie können den Namen und die Beschreibung des Berichts ändern.  

5.  Wenn Sie fertig sind, klicken Sie auf **Übernehmen**. Die Berichtseigenschaften werden auf dem Berichtsserver gespeichert, und die aktualisierten Eigenschaften des Berichts werden von der Configuration Manager-Konsole abgerufen.  

###  <a name="BKMK_EditReport"></a> Bearbeiten eines Configuration Manager-Berichts  
 Sie können einen vorhandenen Configuration Manager-Bericht in Berichts-Generator ändern, wenn nicht die gewünschten Informationen enthalten sind oder Sie ein anderes Layout bzw. einen anderen Entwurf wünschen.  

> [!NOTE]  
>  Auf Wunsch können Sie außerdem einen bestehenden Bericht klonen, indem Sie ihn zur Bearbeitung öffnen und dann auf **Speichern unter** klicken, um ihn als neuen Bericht zu speichern.  

> [!IMPORTANT]  
>  Für das Benutzerkonto sind für die spezifischen Objekte, die dem Bericht zugeordnet sind und die Sie ändern möchten, die Berechtigungen **Ändern** für den Standort und **Bericht ändern** erforderlich.  

> [!IMPORTANT]  
>  Wenn bei Configuration Manager ein Upgrade auf eine neuere Version ausgeführt wird, werden die vordefinierten Berichte von neuen Berichten überschrieben. Sie müssen geänderte vordefinierte Berichte sichern, bevor Sie die neue Version installieren, und sie nach dem Upgrade in Reporting Services wiederherstellen. Wenn Sie an einem Bericht erhebliche Änderungen ausführen möchten, erwägen Sie stattdessen das Erstellen eines neuen Berichts. Neue Berichte, die Sie erstellt haben, werden bei einem Upgrade des Standorts nicht überschrieben.  

 Wenden Sie das folgende Verfahren an, um die Eigenschaften eines Configuration Manager-Berichts zu ändern.  

#### <a name="to-edit-report-properties"></a>So bearbeiten Sie Berichtseigenschaften  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Berichterstattung**, und klicken Sie dann auf **Berichte** , um die verfügbaren Berichte aufzulisten.  

3.  Wählen Sie den Bericht aus, den Sie ändern möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Berichtsgruppe** auf **Bearbeiten**. Geben Sie Ihr Benutzerkonto und Ihr Kennwort ein, wenn Sie dazu aufgefordert werden, und klicken Sie dann auf **OK**. Wenn Report Builder auf dem Computer nicht installiert ist, werden Sie zur Installation aufgefordert. Klicken Sie auf **Ausführen** , um Report Builder zu installieren. Report Builder ist zum Erstellen und Ändern von Berichten erforderlich.  

4.  Ändern Sie in Report Builder die entsprechenden Berichtseinstellungen, und klicken Sie dann auf **Speichern** , um den Bericht auf dem Berichtsserver zu speichern.  

###  <a name="BKMK_CreateModelBasedReport"></a> Erstellen eines modellbasierten Berichts  
 Mit einem modellbasierten Bericht können Sie die Objekte, die Sie in den Bericht einschließen möchten, interaktiv auswählen. Weitere Informationen zum Erstellen von Berichtsmodellen finden Sie unter [Erstellen benutzerdefinierter Berichtsmodelle für System Center Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

> [!IMPORTANT]  
>  Zum Erstellen eines neuen Berichts muss das Benutzerkonto über die Berechtigung **Ändern** für den Standort verfügen. Benutzer können einen Bericht nur in Ordnern erstellen, für die diese über die Berechtigung **Bericht ändern** verfügen.  

 Gehen Sie wie folgt vor, um einen modellbasierten Configuration Manager-Bericht zu erstellen.  

#### <a name="to-create-a-model-based-report"></a>So erstellen Sie einen modellbasierten Bericht  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Berichterstattung** , und klicken Sie auf **Berichte**.  

3.  Klicken Sie auf der Registerkarte **Startseite** im Bereich **Erstellen** auf **Bericht erstellen** , um den **** Assistenten zum Erstellen von Berichten zu öffnen.  

4.  Konfigurieren Sie auf der Seite **Informationen** die folgenden Einstellungen:  

    -   **Typ**: Wählen Sie **Modellbasierter Bericht** aus, um in Berichts-Generator einen Bericht mithilfe eines Reporting Services-Modells zu erstellen.  

    -   **Name**: Geben Sie einen Namen für den Bericht an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung für den Bericht an.  

    -   **Server**: Zeigt den Namen des Berichtsservers an, auf dem Sie diesen Bericht erstellen.  

    -   **Pfad**: Klicken Sie auf **Durchsuchen** , um einen Ordner anzugeben, in dem der Bericht gespeichert werden soll.  

     Klicken Sie auf **Weiter**.  

5.  Wählen Sie auf der Seite **Modellauswahl** ein verfügbares Modell zum Erstellen des Berichts aus der Liste aus. Wenn Sie das Berichtsmodell auswählen, werden im Bereich **Vorschau** die SQL Server-Ansichten und Entitäten angezeigt, die durch das ausgewählte Berichtsmodell verfügbar sind.  

6.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen. Klicken Sie auf **Zurück**, um die Einstellungen zu ändern, oder auf **Weiter**, um den Bericht in Configuration Manager zu erstellen.  

7.  Klicken Sie auf der Seite **Bestätigung** auf **Schließen** , um den Assistenten zu schließen, und öffnen Sie dann Report Builder, um die Berichtseinstellungen zu konfigurieren. Geben Sie Ihr Benutzerkonto und Ihr Kennwort ein, wenn Sie dazu aufgefordert werden, und klicken Sie dann auf **OK**. Wenn Report Builder auf dem Computer nicht installiert ist, werden Sie zur Installation aufgefordert. Klicken Sie auf **Ausführen** , um Report Builder zu installieren. Report Builder ist zum Erstellen und Ändern von Berichten erforderlich.  

8.  In Microsoft Report Builder können Sie das Berichtslayout erstellen, Daten in den verfügbaren SQL Server-Ansichten auswählen, Parameter zum Bericht hinzufügen etc. Weitere Informationen zum Erstellen eines neuen Berichts mit Report Builder finden Sie in der Hilfe zu Report Builder.  

9. Klicken Sie auf **Ausführen** , um den Bericht auszuführen. Überprüfen Sie, ob die erwarteten Informationen im Bericht enthalten sind. Klicken Sie auf **Entwurf** , um zur Entwurfansicht zurückzukehren und den Bericht erforderlichenfalls zu ändern.  

10. Klicken Sie auf **Speichern** , um den Bericht auf dem Berichtsserver zu speichern. Sie können den neuen Bericht im Arbeitsbereich **Überwachung** im Knoten **Berichte** ausführen und ändern.  

###  <a name="BKMK_CreateSQLBasedReport"></a> Erstellen eines SQL\-basierten Berichts  
 Mit einem SQL\-basierten Bericht können Sie Daten auf Basis einer SQL-Anweisung für Berichte abrufen.  

> [!IMPORTANT]  
>  Wenn Sie eine SQL-Anweisung für einen benutzerdefinierten Bericht erstellen, sollten Sie nicht direkt auf SQL Server-Tabellen verweisen. Verweisen Sie stattdessen auf SQL Server-Berichtsansichten \(Ansichten, die mit „v\_“ beginnen\) der Standortdatenbank. Sie können auch auf öffentliche gespeicherte Prozeduren \(gespeicherte Prozeduren, deren Name mit „sp\_“ beginnt\) der Standortdatenbank verweisen.  

> [!IMPORTANT]  
>  Zum Erstellen eines neuen Berichts muss das Benutzerkonto über die Berechtigung **Ändern** für den Standort verfügen. Benutzer können einen Bericht nur in Ordnern erstellen, für die diese über die Berechtigung **Bericht ändern** verfügen.  

 Gehen Sie wie folgt vor, um einen SQL\-basierten Configuration Manager-Bericht zu erstellen.  

#### <a name="to-create-a-sql-based-report"></a>So erstellen Sie einen SQL\-basierten Bericht  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Berichterstattung**, und klicken Sie dann auf **Berichte**.  

3.  Klicken Sie auf der Registerkarte **Startseite** im Bereich **Erstellen** auf **Bericht erstellen** , um den **** Assistenten zum Erstellen von Berichten zu öffnen.  

4.  Konfigurieren Sie auf der Seite **Informationen** die folgenden Einstellungen:  

    -   **Typ**: Wählen Sie **SQL\-basierter Bericht** aus, um in Berichts-Generator einen Bericht mithilfe einer SQL-Anweisung zu erstellen.  

    -   **Name**: Geben Sie einen Namen für den Bericht an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung für den Bericht an.  

    -   **Server**: Zeigt den Namen des Berichtsservers an, auf dem Sie diesen Bericht erstellen.  

    -   **Pfad**: Klicken Sie auf **Durchsuchen** , um einen Ordner anzugeben, in dem der Bericht gespeichert werden soll.  

     Klicken Sie auf **Weiter**.  

5.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen. Klicken Sie auf **Zurück**, um die Einstellungen zu ändern, oder auf **Weiter**, um den Bericht in Configuration Manager zu erstellen.  

6.  Klicken Sie auf der Seite **Bestätigung** auf **Schließen** , um den Assistenten zu schließen, und öffnen Sie dann Report Builder, um die Berichtseinstellungen zu konfigurieren. Geben Sie Ihr Benutzerkonto und Ihr Kennwort ein, wenn Sie dazu aufgefordert werden, und klicken Sie dann auf **OK**. Wenn Report Builder auf dem Computer nicht installiert ist, werden Sie zur Installation aufgefordert. Klicken Sie auf **Ausführen** , um Report Builder zu installieren. Report Builder ist zum Erstellen und Ändern von Berichten erforderlich.  

7.  Stellen Sie in Microsoft Report Builder die SQL-Anweisung für den Bericht bereit oder erstellen Sie die SQL-Anweisung mithilfe der Spalten in den SQL Server-Ansichten; fügen Sie Parameter zum Bericht hinzu etc.  

8.  Klicken Sie auf **Ausführen** , um den Bericht auszuführen. Überprüfen Sie, ob die erwarteten Informationen im Bericht enthalten sind. Klicken Sie auf **Entwurf** , um zur Entwurfansicht zurückzukehren und den Bericht erforderlichenfalls zu ändern.  

9. Klicken Sie auf **Speichern** , um den Bericht auf dem Berichtsserver zu speichern. Sie können den neuen Bericht im Arbeitsbereich **Überwachung** im Knoten **Berichte** ausführen.  

##  <a name="BKMK_ManageReportSubscriptions"></a> Verwalten von Berichtsabonnements  
 Mithilfe von Berichtsabonnements in SQL Server Reporting Services können Sie die automatische Übermittlung von angegebenen Berichten per E-Mail oder an eine Dateifreigabe in geplanten Zeitintervallen konfigurieren. Verwenden Sie den **Assistenten zum Erstellen von Abonnements** in System Center 2012 Configuration Manager, um Berichtsabonnements zu konfigurieren.  

###  <a name="BKMK_ReportSubscriptionFileShare"></a> Erstellen eines Berichtsabonnements zum Übermitteln eines Berichts an eine Dateifreigabe  
 Wenn Sie ein Berichtsabonnement zum Übermitteln eines Berichts an eine Dateifreigabe erstellen, wird der Bericht im angegebenen Format auf die angegebene Dateifreigabe kopiert. Sie können die Übermittlung von nur einem Bericht auf einmal abonnieren bzw. anfordern.  

 Im Gegensatz zu Berichten, die von einem Berichtsserver gehostet und verwaltet werden, handelt es sich bei Berichten, die an eine Dateifreigabe übermittelt werden, um statische Dateien. Bei Berichten, die als Dateien im Dateisystem gespeichert werden, können interaktive Funktionen, die für den Bericht definiert wurden, nicht verwendet werden. Interaktive Funktionen werden als statische Elemente dargestellt. Wenn im Bericht Diagramme enthalten sind, wird die Standardpräsentation verwendet. Wenn im Bericht auf einen anderen Bericht verwiesen wird, wird der Link als statischer Text gerendert. Wenn interaktive Funktionen in einem übermittelten Bericht erhalten bleiben sollen, übermitteln Sie den Bericht stattdessen per E-Mail. Weitere Informationen zum Übermitteln per E-Mail finden Sie im Abschnitt [Erstellen eines Berichtsabonnements zum Übermitteln eines Berichts per E-Mail](#BKMK_ReportSubscriptionEmail) weiter unten im Thema.  

 Wenn Sie ein Abonnement erstellen, von dem die Dateifreigabeübermittlung verwendet wird, müssen Sie einen vorhandenen Ordner als Zielordner angeben. Vom Berichtsserver werden keine Ordner im Dateisystem erstellt. Über eine Netzwerkverbindung muss ein Zugriff auf den angegebenen Ordner möglich sein. Wenn Sie den Zielordner in einem Abonnement angeben, verwenden Sie einen UNC-Pfad. Schließen Sie keinen umgekehrten Schrägstrich am Ende des Ordnerpfads ein. So könnte beispielsweise ein gültiger UNC-Pfad für den Zielordner aussehen: \\\\&lt;Servername\>\\reportfiles\\operations\\2011.  

 Berichte können in verschiedenen Dateiformaten wie MHTML oder Excel gerendert werden. Um den Bericht in einem bestimmten Dateiformat zu speichern, wählen Sie dieses Renderformat, wenn Sie das Abonnement erstellen. Wenn Sie beispielsweise Excel auswählen, wird der Bericht als Microsoft Excel-Datei gespeichert. Sie können zwar jedes unterstützte Renderformat auswählen, doch einige Formate sind zum Rendern besser geeignet als andere.  

 Gehen Sie wie folgt vor, um ein Berichtsabonnement zur Übermittlung eines Berichts an eine Dateifreigabe zu erstellen.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>So erstellen Sie ein Berichtsabonnement zur Übermittlung eines Berichts an eine Dateifreigabe  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Erweitern Sie im Arbeitsbereich **Überwachung** den Knoten **Berichterstattung** , und klicken Sie dann auf **Berichte** , um die verfügbaren Berichte aufzulisten. Sie können einen Berichtsordner auswählen, um nur die Berichte aufzulisten, die dem Ordner zugeordnet sind.  

3.  Wählen Sie den Bericht aus, der dem Abonnement hinzugefügt werden soll, und klicken Sie dann auf der Registerkarte **Startseite** im Bereich **Berichtsgruppe** auf **Abonnement erstellen** , um den **** Assistenten zum Erstellen von Abonnements zu öffnen.  

4.  Konfigurieren Sie auf der Seite **Abonnementübermittlung** die folgenden Einstellungen:  

    -   Bericht übermittelt von: Wählen Sie **Windows-Dateifreigabe** aus, um den Bericht an eine Dateifreigabe zu übermitteln.  

    -   **Dateiname**: Geben Sie den Dateinamen des Berichts an. Standardmäßig ist bei der Berichtsdatei keine Dateinamenerweiterung enthalten. Wählen Sie die Option **Dateierweiterung beim Erstellen hinzufügen** aus, um diesem Bericht automatisch eine Dateinamenerweiterung anhand des Renderformats hinzuzufügen.  

    -   **Pfad**:Geben Sie einen UNC-Pfad zu einem vorhandenen Ordner an, in den Sie diesen Bericht übermitteln möchten \(z.B. \\\\&lt;Servername\>\\&lt;Serverfreigabe\>\\&lt;Berichtsordner\>\).  

        > [!NOTE]  
        >  Für den weiter unten auf dieser Seite angegebenen Benutzernamen müssen Zugriffsrechte für diese Serverfreigabe und Schreibzugriff für den Zielordner vorliegen.  

    -   **Renderformat**: Wählen Sie eines der folgenden Formate für die Berichtsdatei:  

        -   **XML-Datei mit Berichtsdaten**: Der Bericht wird im XML-Format (Extensible Markup Language) gespeichert.  

        -   **CSV \(Komma-getrennt\)**: Der Bericht wird im \-CSV-Format\- (Comma Separated Value, kommagetrennte Werte) gespeichert.  

        -   **TIFF-Datei**: Der Bericht wird im TIFF-Format (Tagged Image File Format) gespeichert.  

        -   **Acrobat-Datei \(PDF\)**: Der Bericht wird im PDF-Format (Acrobat Portable Document Format) gespeichert.  

        -   **HTML 4.0**: Der Bericht wird als Webseite gespeichert, die nur in Browsern mit Unterstützung für HTML 4.0 angezeigt werden kann. Internet Explorer 5 und höhere Versionen unterstützen HTML 4.0.  

            > [!NOTE]  
            >  Wenn in Ihrem Bericht Bilder enthalten sind, werden diese mit der HTML 4.0-Datei nicht gespeichert.  

        -   **MHTML \(Webarchiv\)**: Der Bericht wird im MIME HTML-Format \(mhtml\) gespeichert, das in vielen Webbrowsern angezeigt werden kann.  

        -   **RPL-Renderer**: Speichert den Bericht im Berichtsseitenlayout-Format \(RPL\).  

        -   **Excel**: Der Bericht wird als Microsoft Excel-Arbeitsblatt gespeichert.  

        -   **Word**: Der Bericht wird als Microsoft Word-Dokument gespeichert.  

    -   **Benutzername**: Geben Sie ein Windows-Benutzerkonto mit Berechtigungen für den Zugriff auf die Zielserverfreigabe und den Zielordner an. Für das Benutzerkonto müssen Zugriffsrechte für diese Serverfreigabe und Schreibzugriff für den Zielordner vorliegen.  

    -   **Kennwort**: Geben Sie das Kennwort für das Windows-Benutzerkonto an. Geben Sie im Feld **Kennwort bestätigen** das Kennwort erneut ein.  

    -   Wählen Sie eine der folgenden Optionen aus, um zu konfigurieren, wie vorgegangen werden soll, wenn eine Datei mit dem gleichen Namen bereits im Zielordner vorhanden ist.  

        -   **Vorhandene Datei mit einer neueren Version überschreiben**: Wenn die Berichtsdatei bereits vorhanden ist, wird sie von der neuen Version überschrieben.  

        -   **Vorhandene Datei nicht überschreiben**: Wenn die Berichtsdatei bereits vorhanden ist, wird keine Aktion ausgeführt.  

        -   **Dateinamen inkrementieren, wenn neuere Versionen hinzugefügt werden**: Wenn die Berichtsdatei bereits vorhanden ist, wird dem Dateinamen des neuen Berichts eine Nummer hinzufügt, um ihn von anderen Versionen zu unterscheiden.  

    -   **Beschreibung**: Hier wird die Beschreibung für das Berichtsabonnement angegeben.  

     Klicken Sie auf **Weiter**.  

5.  Wählen Sie auf der Seite **Abonnementzeitplan** eine der folgenden Optionen für den Übermittlungszeitplan des Berichtsabonnements aus:  

    -   **Freigegebenen Zeitplan verwenden**: Ein freigegebener Zeitplan ist ein zuvor festgelegter Zeitplan, der von anderen Berichtsabonnements verwendet werden kann. Aktivieren Sie dieses Kontrollkästchen, und wählen Sie dann in der Liste einen freigegebenen Zeitplan aus, falls Zeitpläne angegeben wurden.  

    -   **Neuen Zeitplan erstellen**: Konfigurieren Sie den Zeitplan, nach dem dieser Bericht ausgeführt werden soll, mit Intervall sowie Anfangs- und Enddatum für das Abonnement.  

6.  Geben Sie auf der Seite **Abonnementparameter** die Parameter für die unbeaufsichtigte Ausführung dieses Berichts an. Wenn keine Parameter für den Bericht vorhanden sind, wird diese Seite nicht angezeigt.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen für das Berichtsabonnement. Klicken Sie auf **Zurück** , um die Einstellungen zu ändern, oder auf **Weiter** , um das Berichtsabonnement zu erstellen.  

8.  Klicken Sie auf der Seite **Abschluss des Vorgangs** zum Beenden des Assistenten auf **Schließen** . Überprüfen Sie, ob das Berichtsabonnement erfolgreich erstellt wurde. Sie können Berichtsabonnements im Arbeitsbereich **Überwachung** unter **Berichterstattung** im Knoten **Berichte** anzeigen und ändern.  

###  <a name="BKMK_ReportSubscriptionEmail"></a> Erstellen eines Berichtsabonnements zum Übermitteln eines Berichts per E-Mail  
 Wenn Sie ein Berichtsabonnement für die Übermittlung eines Berichts per E-Mail erstellen, wird eine E-Mail mit dem Bericht als Anlage an die konfigurierten Empfänger gesendet. Dabei werden die E-Mail-Adressen nicht überprüft, und es werden auch keine E-Mail-Adressen von einem E-Mail-Server abgerufen. Sie müssen im Voraus wissen, welche E-Mail-Adressen Sie verwenden möchten. Standardmäßig können Sie Berichte an beliebige E-Mail-Konten innerhalb oder außerhalb Ihres Unternehmens senden. Sie können eine oder beide der folgenden E-Mail-Übermittlungsoptionen auswählen:  

-   Senden Sie eine Benachrichtigung und einen Hyperlink zum generierten Bericht.  

-   Senden Sie einen eingebetteten oder angehängten Bericht. Ob der Bericht eingebettet oder angehängt wird, ist abhängig vom Renderformat und vom Browser. Wenn Ihr Browser HTML 4.0 und MHTML unterstützt und Sie das Renderformat MHTML \(Webarchiv\) auswählen, wird der Bericht in den Text der Nachricht eingebettet. Bei allen anderen Renderformaten \(CSV, PDF, Word usw.\) werden Berichte als Anlagen übermittelt. Die Größe der Anlage oder Nachricht wird von Reporting Services vor dem Senden des Berichts nicht überprüft. Wenn der Grenzwert des Mailservers für die maximal zulässige Größe durch die Anlage oder die Nachricht überschritten wird, wird der Bericht nicht übermittelt.  

> [!IMPORTANT]  
>  Sie müssen die E-Mail-Einstellungen in Reporting Services so konfigurieren, dass die Übermittlungsoption **E-Mail** verfügbar ist. Weitere Informationen zum Konfigurieren der E-Mail-Einstellungen in Reporting Services finden Sie unter [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung](http://go.microsoft.com/fwlink/p/?LinkId=226668) in der Onlinedokumentation zu SQL Server.  

 Gehen Sie wie folgt vor, um ein Berichtsabonnement zur Übermittlung eines Berichts per E-Mail zu erstellen.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-by-email"></a>So erstellen Sie ein Berichtsabonnement zur Übermittlung eines Berichts per E-Mail  

-   Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

-   Erweitern Sie im Arbeitsbereich **Überwachung** den Knoten **Berichterstattung** , und klicken Sie dann auf **Berichte** , um die verfügbaren Berichte aufzulisten. Sie können einen Berichtsordner auswählen, um nur die Berichte aufzulisten, die dem Ordner zugeordnet sind.  

-   Wählen Sie den Bericht aus, der dem Abonnement hinzugefügt werden soll, und klicken Sie dann auf der Registerkarte **Startseite** im Bereich **Berichtsgruppe** auf **Abonnement erstellen** , um den **** Assistenten zum Erstellen von Abonnements zu öffnen.  

-   Konfigurieren Sie auf der Seite **Abonnementübermittlung** die folgenden Einstellungen:  

    -   **Bericht übermittelt von**: Wählen Sie **E\-Mail** aus, um den Bericht als Anlage einer E-Mail-Nachricht zu übermitteln.  

    -   **Bis**: Geben Sie eine gültige E-Mail-Adresse an, an die dieser Bericht gesendet werden soll.  

        > [!NOTE]  
        >  Sie können mehrere E-Mail-Empfänger eingeben, indem Sie die E-Mail-Adressen durch ein Semikolon trennen.  

    -   **Cc**: Geben Sie optional eine E-Mail-Adresse an, an die eine Kopie dieses Berichts gesendet werden soll.  

    -   **Bcc**: Geben Sie optional eine E-Mail-Adresse an, an die dieser Bericht per Blindkopie gesendet werden soll.  

    -   **Antwort an**: Geben Sie die Antwortadresse an, falls der Empfänger auf die E-Mail-Nachricht antworten möchte.  

    -   **Betreff**: Geben Sie eine Betreffzeile für die Abonnement-E-Mail an.  

    -   **Priorität**: Wählen Sie die Priorität für diese E-Mail aus. Wählen Sie **Niedrig**, **Normal**oder **Hoch**aus. Anhand der Einstellung der Priorität wird von Microsoft Exchange ein Kennzeichen festgelegt, das die Wichtigkeit der E-Mail-Nachricht anzeigt.  

    -   **Comment**: Geben Sie Text an, der dem Textteil der Abonnement-E-Mail hinzugefügt wird.  

    -   **Beschreibung**: Geben Sie eine Beschreibung für dieses Berichtsabonnement an.  

    -   **Link einschließen**: Bei Auswahl dieser Option wird eine URL zum abonnierten Bericht in den Textteil der E-Mail-Nachricht eingeschlossen.  

    -   **Bericht einschließen**: Geben Sie an, dass der Bericht an die E\-Mail-Nachricht angehängt wird. Das Format, in dem der Bericht angehängt wird, wird über die Liste **Renderformat** angegeben.  

    -   **Renderformat**: Wählen Sie eines der folgenden Formate für den angehängten Bericht aus:  

        -   **XML-Datei mit Berichtsdaten**: Der Bericht wird im XML-Format (Extensible Markup Language) gespeichert.  

        -   **CSV \(Komma-getrennt\)**: Der Bericht wird im \-CSV-Format\- (Comma Separated Value, kommagetrennte Werte) gespeichert.  

        -   **TIFF-Datei**: Der Bericht wird im TIFF-Format (Tagged Image File Format) gespeichert.  

        -   **Acrobat-Datei \(PDF\)**: Der Bericht wird im PDF-Format (Acrobat Portable Document Format) gespeichert.  

        -   **MHTML \(Webarchiv\)**: Der Bericht wird im MIME HTML-Format \(mhtml\) gespeichert, das in vielen Webbrowsern angezeigt werden kann.  

        -   **Excel**: Der Bericht wird als Microsoft Excel-Arbeitsblatt gespeichert.  

        -   **Word**: Der Bericht wird als Microsoft Word-Dokument gespeichert.  

-   Wählen Sie auf der Seite **Abonnementzeitplan** eine der folgenden Optionen für den Übermittlungszeitplan des Berichtsabonnements aus:  

    -   **Freigegebenen Zeitplan verwenden**: Ein freigegebener Zeitplan ist ein zuvor festgelegter Zeitplan, der von anderen Berichtsabonnements verwendet werden kann. Aktivieren Sie dieses Kontrollkästchen, und wählen Sie dann in der Liste einen freigegebenen Zeitplan aus, falls Zeitpläne angegeben wurden.  

    -   **Neuen Zeitplan erstellen**: Konfigurieren Sie den Zeitplan, nach dem dieser Bericht ausgeführt wird, mit Intervall sowie Anfangs- und Enddatum für das Abonnement.  

-   Geben Sie auf der Seite **Abonnementparameter** die Parameter für die unbeaufsichtigte Ausführung dieses Berichts an. Wenn keine Parameter für den Bericht vorhanden sind, wird diese Seite nicht angezeigt.  

-   Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen für das Berichtsabonnement. Klicken Sie auf **Zurück** , um die Einstellungen zu ändern, oder auf **Weiter** , um das Berichtsabonnement zu erstellen.  

-   Klicken Sie auf der Seite **Abschluss des Vorgangs** zum Beenden des Assistenten auf **Schließen** . Überprüfen Sie, ob das Berichtsabonnement erfolgreich erstellt wurde. Sie können Berichtsabonnements im Arbeitsbereich **Überwachung** unter **Berichterstattung** im Knoten **Berichte** anzeigen und ändern.  
