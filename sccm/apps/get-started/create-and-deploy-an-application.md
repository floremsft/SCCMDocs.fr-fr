---
title: Erstellen und Bereitstellen einer Anwendung | Microsoft Docs
description: Informationen zum Erstellen und Bereitstellen einer Anwendung mit einer Line-of-Business-App, und wie Apps effektiv verwaltet werden.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: "15"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: bbbf278f5d31c51bfe061dd44e170f7ab1ca70ad
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>Erstellen und Bereitstellen einer Anwendung mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In diesem Thema legen Sie direkt los und erstellen eine Anwendung mit System Center Configuration Manager. In diesem Beispiel werden Sie eine Anwendung erstellen und bereitstellen, die eine branchenspezifische App für Windows-PCs enthält. Die App heißt **Contoso.msi** und muss auf allen PCs in Ihrem Unternehmen installiert werden, auf denen Windows 10 ausgeführt wird. Nebenbei lernen Sie viele Funktionen kennen, mit denen Sie Anwendungen effizient verwalten können.  

 Dieses Verfahren soll Ihnen einen Überblick über das Erstellen und Bereitstellen von Configuration Manager-Anwendungen geben. Es wird allerdings nicht auf alle Konfigurationsoptionen und auch nicht auf die Erstellung und Bereitstellung von Anwendungen für andere Plattformen eingegangen.  

 Spezifische Details für die einzelnen Plattformen finden Sie in den folgenden Themen:  

-   [Erstellen von Windows-Anwendungen](../../apps/get-started/creating-windows-applications.md)  
-   [Erstellen von iOS-Anwendungen](../../apps/get-started/creating-ios-applications.md)  
-   [Erstellen von Android-Anwendungen](../../apps/get-started/creating-android-applications.md)  
-   [Erstellen von Windows Phone-Anwendungen](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Erstellen von Anwendungen für Macintosh-Computer](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Erstellen von Linux- und UNIX-Serveranwendungen](../../apps/get-started/creating-linux-and-unix-server-applications.md)
-   [Erstellen von Windows Embedded-Anwendungen](../../apps/get-started/creating-windows-embedded-applications.md)


Wenn Sie bereits mit Configuration Manager-Anwendungen vertraut sind, können Sie dieses Thema überspringen. Vielleicht interessiert Sie auch das Thema zum [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md), in dem alle beim Erstellen und Bereitstellen von Anwendungen verfügbaren Optionen erläutert werden.  

## <a name="before-you-start"></a>Vorbereitung  

Die Informationen unter [Einführung in die Anwendungsverwaltung](/sccm/apps/understand/introduction-to-application-management) sollten Ihnen geläufig sein. So ist sichergestellt, dass Sie Ihren Standort für die Installation von Anwendungen vorbereitet haben und die in diesem Thema verwendete Terminologie kennen.  

 Vergewissern Sie sich außerdem, dass die Installationsdateien für die App **Contoso.msi** unter einem zugänglichen Pfad in Ihrem Netzwerk gespeichert sind.  

## <a name="create-the-configuration-manager-application"></a>Erstellen der Configuration Manager-Anwendung  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>So starten Sie den Assistenten zum Erstellen von Anwendungen und erstellen die Anwendung  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Anwendung erstellen** aus.  

4.  Wählen Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Anwendungen** die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen** aus. Dadurch werden einige Informationen aus der MSI-Installationsdatei extrahiert und vorab in den Assistenten eingefügt. Geben Sie dann die folgenden Informationen an:  

    -   **Typ:** Wählen Sie **Windows Installer (\*.msi-Datei)** aus.  

    -   **Speicherort:** Geben Sie den Speicherort der Installationsdatei **Contoso.msi** ein (oder wählen Sie **Durchsuchen** aus, um ihn auszuwählen). Beachten Sie, dass der Speicherort im Format *\\\Server\Freigabe\Datei* angegeben werden muss, damit die Installationsdateien in Configuration Manager gefunden werden.  

    Zum Schluss sollte ein Screenshot angezeigt werden, der etwa wie folgt aussieht:  

    ![App-Management-Assistent Allgemein](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  

5.  Wählen Sie **Weiter** aus. Auf der Seite **Informationen importieren** werden einige Informationen zur App und zugehörigen Dateien angezeigt, die in Configuration Manager importiert wurden. Wählen Sie abschließend erneut **Weiter** aus.  

6.  Auf der Seite **Allgemeine Informationen** können Sie weitere Informationen zur Anwendung angeben. Auf diese Weise kann die Anwendung leichter sortiert und in der Configuration Manager-Konsole gefunden werden.  

     Darüber hinaus können Sie im Feld **Installationsprogramm** die vollständige Befehlszeile angeben, die zur Installation der Anwendung auf PCs verwendet wird. Sie können das Feld bearbeiten, um eigene Eigenschaften hinzuzufügen (z.B. **/q** für eine unbeaufsichtigte Installation).  

    > [!TIP]  
    >  Einige Felder auf dieser Seite des Assistenten wurden während des Imports der Anwendungsinstallationsdateien möglicherweise automatisch ausgefüllt.  

     Zum Schluss sollte ein mit dem folgenden Screenshot vergleichbarer Bildschirm angezeigt werden:  

     ![App-Management-Assistent-Seite mit allgemeinen Informationen](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  

7.  Wählen Sie **Weiter** aus. Auf der Seite „Zusammenfassung“ können Sie die Anwendungseinstellungen bestätigen und den Assistenten dann abschließen.  

 Die Erstellung der App ist abgeschlossen. Sie finden die App, indem Sie im Arbeitsbereich **Softwarebibliothek** den Knoten **Anwendungsverwaltung** erweitern und dann die Option **Anwendungen** auswählen. In diesem Beispiel sehen Sie:  

 ![Endgültige App-Grafik](/sccm/apps/get-started/media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Überprüfen der Anwendungseigenschaften und des Bereitstellungstyps  

Nachdem Sie eine Anwendung erstellt haben, können Sie die Anwendungseinstellungen bei Bedarf optimieren. Um die Anwendungseigenschaften anzuzeigen, wählen Sie die App und dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

 Im Dialogfeld **<Contoso\> Anwendungseigenschaften** sind viele Elemente enthalten, die Sie konfigurieren können, um das Anwendungsverhalten zu optimieren. Details zu allen konfigurierbaren Einstellungen finden Sie unter [Anwendungen erstellen](../../apps/deploy-use/create-applications.md). Im Rahmen dieses Beispiels ändern Sie nur einige Eigenschaften des Bereitstellungstyps der Anwendung.  

 Wählen Sie die Registerkarte **Bereitstellungstypen** den Bereitstellungstyp **Contoso-Anwendung** und dann **Bearbeiten** aus.  

Ein mit dem folgenden vergleichbares Dialogfeld wird angezeigt:  

![App-Management-App-Eigenschaftenseite](/sccm/apps/get-started/media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Hinzufügen einer Anforderung zum Bereitstellungstyp  
 Mit Anforderungen werden Bedingungen angegeben, die erfüllt sein müssen, bevor eine Anwendung auf einem Gerät installiert wird.  Sie können integrierte Anforderungen auswählen oder eigene Anforderungen erstellen. In diesem Beispiel fügen Sie die Anforderung hinzu, dass die Anwendung nur auf PCs installiert wird, auf denen Windows 10 ausgeführt wird.  

1.  Wählen Sie auf der gerade geöffneten Eigenschaftenseite des Bereitstellungstyps die Registerkarte **Anforderungen** aus.  

2.  Wählen Sie **Hinzufügen** aus, um das Dialogfeld **Anforderung erstellen** zu öffnen.  

3.  Geben Sie im Dialogfeld **Anforderung erstellen** die folgenden Informationen an:  

    -   **Kategorie:** **Gerät**  

    -   **Bedingung:** **Betriebssystem**  

    -   **Regeltyp:** **Wert**  

    -   **Operator:** **Eine von**  

    -   Wählen Sie aus der Betriebssystemliste **Windows 10**aus.  

    Zum Schluss sieht das Dialogfeld etwa folgendermaßen aus:  

    ![Seite „App-Verwaltungsanforderungen“](/sccm/apps/get-started/media/App-management-requirements-page.png)  

4.  Wählen Sie **OK** aus, um alle geöffneten Eigenschaftenseiten zu schließen. Kehren Sie dann zur Liste **Anwendungen** in der Configuration Manager-Konsole zurück.  

> [!TIP]  
>  Mithilfe von Anforderungen können Sie die Anzahl der benötigten Configuration Manager-Sammlungen verringern. Da Sie gerade angegeben haben, dass die Anwendung nur auf Windows 10-Computern installiert werden kann, können Sie diese Anforderung später für eine Sammlung bereitstellen, die Computer enthält, auf denen viele verschiedene Betriebssysteme ausgeführt werden. Die Anwendung wird jedoch nur auf Windows 10-Computern installiert.  

## <a name="add-the-application-content-to-a-distribution-point"></a>Hinzufügen des Anwendungsinhalts zu einem Verteilungspunkt  

Zur Bereitstellung der Anwendung auf PCs müssen Sie als Nächstes sicherstellen, dass der Inhalt der Anwendung auf einen Verteilungspunkt kopiert wird. PCs greifen auf den Verteilungspunkt zu, um die Anwendung zu installieren.  

> [!TIP]  
>  Weitere Informationen zu Verteilungspunkten sowie zum Content Management in Configuration Manager finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Softwarebibliothek** aus.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Knoten **Anwendungen**. Wählen Sie dann in der Liste der Anwendungen die **Contoso-Anwendung** aus, die Sie erstellt haben.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** die Option **Inhalt verteilen** aus.  

4.  Überprüfen Sie auf der Seite **Allgemein** des **Assistenten für die Verteilung von Inhalt**, ob der Name der Anwendung richtig ist, und wählen Sie dann **Weiter** aus.  

5.  Überprüfen Sie auf der Seite **Inhalt** die Informationen, die auf den Verteilungspunkt kopiert werden, und wählen Sie dann **Weiter** aus.  

6.  Wählen Sie auf der Seite **Inhaltsziel** die Option **Hinzufügen** aus, um einen oder mehrere Verteilungspunkte oder Verteilungspunktgruppen auszuwählen, auf bzw. in denen der Anwendungsinhalt installiert werden soll.  

7.  Schließen Sie den Assistenten ab.  

Im Arbeitsbereich **Überwachung** können Sie unter **Verteilungsstatus** > **Inhaltsstatus** überprüfen, ob der Inhalt der Anwendung erfolgreich auf den Verteilungspunkt kopiert wurde.  

## <a name="deploy-the-application"></a>Bereitstellen der Anwendung  

Als Nächstes stellen Sie die Anwendung für eine Gerätesammlung in Ihrer Hierarchie bereit. In diesem Beispiel stellen Sie die Anwendung in der Gerätesammlung **Alle Systeme** bereit.  

> [!TIP]  
>  Denken Sie daran, dass die Anwendung aufgrund der zuvor ausgewählten Anforderungen nur auf Windows 10-Computern installiert wird.  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** aus.  

3.  Wählen Sie in der Liste der Anwendungen Ihre zuvor erstellte **Contoso-Anwendung** aus. Wählen Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** die Option **Bereitstellen** aus.  

4.  Wählen Sie auf der Seite **Allgemein** des **Assistenten zum Bereitstellen von Software** die Option **Durchsuchen** und dann die Gerätesammlung **Alle Systeme** aus.  

5.  Wählen Sie auf der Seite **Inhalt** den Verteilungspunkt aus, über den PCs die ausgewählte Anwendung installieren sollen.  

6.  Stellen Sie auf der Seite **Bereitstellungseinstellungen** sicher, dass die Bereitstellungsaktion auf **Installieren** und der Bereitstellungszweck auf **Erforderlich** festgelegt sind.  

    > [!TIP]  
    >  Indem Sie den Zweck der Bereitstellung auf **Erforderlich** festlegen, stellen Sie sicher, dass die Anwendung auf PCs installiert wird, die die definierten Anforderungen erfüllen. Wenn Sie diesen Wert auf **Verfügbar**festlegen, können Benutzer die Anwendung bei Bedarf über das Softwarecenter installieren.  

7.  Auf der Seite **Zeitplanung** können Sie konfigurieren, wann die Anwendung installiert wird. Wählen Sie für dieses Beispiel **So bald wie möglich nach der verfügbaren Zeit**aus.  

8.  Wählen Sie auf der Seite **Benutzerfreundlichkeit** die Option **Weiter** aus, um die Standardwerte zu übernehmen.  

9. Schließen Sie den Assistenten ab.  

Der nachfolgende Abschnitt **Die Anwendung überwachen** enthält Informationen zum Anzeigen des Status Ihrer Anwendungsbereitstellung.  

## <a name="monitor-the-application"></a>Die Anwendung überwachen  
 In diesem Abschnitt erhalten Sie eine Übersicht über den Bereitstellungsstatus der Anwendung, die Sie gerade bereitgestellt haben.  

### <a name="to-review-the-deployment-status"></a>So überprüfen den Bereitstellungsstatus  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Überwachung** > **Bereitstellungen** aus.  

3.  Wählen Sie in der Liste der Bereitstellungen die **Contoso-Anwendung**aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** die Option **Status anzeigen** aus.  

5.  Wählen Sie eine der folgenden Registerkarten aus, um weitere Statusinformationen zur Anwendungsbereitstellung anzuzeigen:  

    -   **Erfolg:** Die Anwendung wurde erfolgreich auf den angegebenen PCs installiert.  

    -   **In Bearbeitung:** Die Installation der Anwendung ist noch nicht abgeschlossen.  

    -   **Fehler:** Beim Installieren der Anwendung auf den angegebenen PCs ist ein Fehler aufgetreten. Weitere Informationen zum Fehler werden ebenfalls angezeigt.  

    -   **Anforderungen nicht erfüllt:** Es wurde nicht versucht, die Anwendung auf den angegebenen Geräten zu installieren, da sie nicht die konfigurierten Anforderungen erfüllt haben (in diesem Beispiel, weil auf diesen Geräten Windows 10 nicht ausgeführt wird).  

    -   **Unbekannt:** Der Status der Bereitstellung konnte in Configuration Manager nicht gemeldet werden. Kehren Sie später erneut zurück.  

> [!TIP]  
>  Es gibt einige Möglichkeiten zum Überwachen von Anwendungsbereitstellungen. Ausführliche Informationen finden Sie unter [Überwachen von Anwendungen](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

## <a name="end-user-experience"></a>Ablauf für Endbenutzer  

Benutzern von Windows 10-PCs, die mit Configuration Manager verwaltet werden, wird die Meldung angezeigt, dass sie die Anwendung „Contoso“ installieren müssen. Nachdem sie der Installation zugestimmt haben, wird die Anwendung installiert.  
