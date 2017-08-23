---
title: "Verwalten von Treibern – Configuration Manager | Microsoft-Dokumentation"
description: "Verwenden Sie den Configuration Manager-Treiberkatalog zum Importieren von Gerätetreibern und Gruppentreibern in Paketen und zum Verteilen dieser Pakete an Verteilungspunkte."
ms.custom: na
ms.date: 01/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 87ab9925717a307cbda3cea1f2e470ae012fa067
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-drivers-in-system-center-configuration-manager"></a>Verwalten von Treibern in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager stellt einen Treiberkatalog bereit, den Sie zum Verwalten der Windows-Gerätetreiber in Ihrer Configuration Manager-Umgebung verwenden können. Sie können den Treiberkatalog verwenden, um Gerätetreiber in Configuration Manager zu importieren, sie in Pakete zu gruppieren und um diese Pakete an Verteilungspunkte zu verteilen, wo Sie auf sie zugreifen können, wenn Sie ein Betriebssystem bereitstellen. Sie können Gerätetreiber verwenden, wenn Sie das vollständige Betriebssystem auf dem Zielcomputer installieren und wenn Sie Windows PE mithilfe eines Startabbilds installieren. Windows-Gerätetreiber bestehen aus einer INF-Datei (Setup Information File) sowie ggf. zusätzlichen Dateien, die für die Geräteunterstützung erforderlich sind. Wenn ein Betriebssystem bereitgestellt wird, werden die Hardware- und Plattforminformationen durch Configuration Manager aus der INF-Datei des Geräts abgerufen. Gehen Sie wie folgt vor, um Treiber in Ihrer Configuration Manager-Umgebung zu verwalten.

##  <a name="BKMK_DriverCategories"></a> Gerätetreiberkategorien  
 Wenn Sie Gerätetreiber importieren, können Sie sie einer Kategorie zuweisen. Mithilfe von Gerätetreiberkategorien können Sie ähnlich verwendete Gerätetreiber im Treiberkatalog gruppieren. Sie können z. B. alle Netzwerkkarten-Gerätetreiber einer bestimmten Kategorie zuweisen. Wenn Sie dann eine Tasksequenz erstellen, die den Schritt [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) enthält, können Sie eine bestimmte Kategorie von Gerätetreibern angeben. Configuration Manager überprüft anschließend die Hardware und wählt die anwendbaren Treiber aus dieser Kategorie aus, um sie zur Verwendung durch Windows Setup verfügbar zu machen.  

##  <a name="BKMK_ManagingDriverPackages"></a> Treiberpakete  
 Sie können zur Vereinfachung der Bereitstellung eines Betriebssystems ähnliche Gerätetreiber in Paketen zusammenfassen. Sie können z. B. ein Treiberpaket für jeden Computerhersteller in Ihrem Netzwerk erstellen. Sie können ein Treiberpaket erstellen, wenn Sie Treiber direkt über den Knoten **Treiberpakete** in den Treiberkatalog importieren. Wenn Sie das Treiberpaket erstellt haben, müssen Sie es an Verteilungspunkte verteilen, von denen aus die Treiber von Configuration Manager-Clientcomputern nach Bedarf installiert werden können. Beachten Sie Folgendes:  

-   Wenn Sie ein Treiberpaket erstellen, muss der Quellspeicherort des Pakets einen Verweis auf eine leere Netzwerkfreigabe enthalten, die nicht von einem anderen Treiberpaket verwendet wird, und für den SMS-Anbieter sind die Berechtigungen Lesen und Schreiben für diesen Speicherort erforderlich.  

-   Wenn Sie einem Treiberpaket Gerätetreiber hinzufügen, wird der Gerätetreiber von Configuration Manager an den Quellspeicherort des Treiberpakets kopiert. Sie können nur Gerätetreiber hinzufügen, die importiert und im Treiberkatalog für ein Treiberpaket aktiviert wurden.  

-   Um eine Teilmenge der Gerätetreiber von einem bestehenden Treiberpaket zu kopieren, erstellen Sie ein neues Treiberpaket, fügen die gewünschte Teilmenge der Gerätetreiber hinzu und verteilen das neue Paket an einen Verteilungspunkt.  

 Verwenden Sie zum Erstellen und Verwalten von Treiberpaketen die folgenden Abschnitte.  

###  <a name="CreatingDriverPackages"></a> Erstellen eines Treiberpakets  
 Gehen Sie wie folgt vor, um ein neues Treiberpaket zu erstellen.  

> [!IMPORTANT]  
>  Zum Erstellen eines Treiberpakets benötigen Sie einen leeren Netzwerkordner, der von keinem anderen Treiberpaket verwendet wird. In der Regel müssen Sie einen neuen Ordner erstellen, bevor Sie dieses Verfahren starten.  

> [!NOTE]  
>  Wenn Sie Tasksequenzen verwenden, um Treiber zu installieren, erstellen Sie Treiberpakete mit weniger als 500 Gerätetreibern.  

 Gehen Sie wie folgt vor, um ein Treiberpaket zu erstellen.  

#### <a name="to-create-a-driver-package"></a>So erstellen Sie ein Treiberpaket  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Treiberpakete**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Treiberpaket erstellen**.  

4.  Geben Sie im Feld **Name** einen beschreibenden Namen für das Treiberpaket an.  

5.  Geben Sie im Feld **Kommentar** eine optionale Beschreibung für das Treiberpaket ein. Achten Sie darauf, dass die Beschreibung Informationen zum Inhalt oder Zweck des Treiberpakets enthält.  

6.  Geben Sie im Feld **Pfad** einen leeren Quellordner für das Treiberpaket an. Geben Sie den Pfad zum Quellordner im UNC-Format (Universal Naming Convention) ein. Von jedem Treiberpaket muss ein eindeutiger Ordner verwendet werden.  

    > [!IMPORTANT]  
    >  Das Standortserverkonto muss über die Berechtigungen **Lesen** und **Schreiben** für den angegebenen Quellordner verfügen.  

 Das neue Treiberpaket enthält keine Treiber. Der nächste Schritt besteht darin, dem Paket Treiber hinzuzufügen.  

 Wenn der Knoten **Treiberpakete** mehrere Pakete enthält, können Sie dem Knoten Ordner hinzufügen, um die Pakete in logische Gruppen zu unterteilen.  

###  <a name="BKMK_PackageActions"></a> Zusätzliche Aktionen für Treiberpakete  
 Sie können zusätzliche Aktionen zur Verwaltung von Treiberpaketen ausführen, wenn Sie im Knoten **Treiberpakete** mindestens ein Treiberpaket auswählen. Diese Aktionen umfassen Folgendes:  

|Aktion|Beschreibung|  
|------------|-----------------|  
|**Datei für vorab bereitgestellten Inhalt erstellen**|Hiermit werden Dateien erstellt, die zum manuellen Importieren von Inhalt und der zugeordneten Metadaten verwendet werden können. Verwenden Sie vorab bereitgestellten Inhalt, wenn die Bandbreite zwischen dem Standortserver und den Verteilungspunkten, auf denen das Treiberpaket gespeichert wird, eingeschränkt ist.|  
|**Löschen**|Hiermit wird das Treiberpaket aus dem Knoten **Treiberpakete** entfernt.|  
|**Treiberpakete**|Hiermit wird das Treiberpaket an Verteilungspunkte, Verteilungspunktgruppen sowie an Verteilungspunktgruppen, die Sammlungen zugeordnet sind, verteilt.|  
|**Zugriffskonten verwalten**|Hiermit werden Zugriffskonten für das Treiberpaket hinzugefügt, geändert oder entfernt.<br /><br /> Weitere Informationen zu Paketzugriffskonten finden Sie unter [Technische Referenz für Konten in Configuration Manager](../../core/plan-design/hierarchy/accounts.md).|  
|**Verschieben**|Hiermit wird das Treiberpaket im Knoten **Treiberpakete** in einen anderen Ordner verschoben.|  
|**Verteilungspunkte aktualisieren**|Hiermit wird an allen Verteilungspunkten, auf denen das Gerätetreiberpaket gespeichert wird, ein Update des Pakets ausgeführt. Bei dieser Aktion wird nur der Inhalt kopiert, der sich seit seiner letzten Verteilung geändert hat.|  
|**Eigenschaften**|Hiermit wird das Dialogfeld **Eigenschaften** geöffnet, in dem Sie den Inhalt und die Eigenschaften des Gerätetreibers prüfen und ändern können. Beispielsweise können Sie den Namen und die Beschreibung des Gerätetreibers ändern, den Gerätetreiber aktivieren sowie angeben, auf welchen Plattformen der Gerätetreiber ausgeführt werden kann.|  

##  <a name="BKMK_DeviceDrivers"></a> Gerätetreiber  
 Sie können Gerätetreiber auf Zielcomputern installieren, ohne sie in das Betriebssystemabbild einzuschließen, das bereitgestellt wird. In Configuration Manager ist ein Treiberkatalog enthalten, der Verweise zu allen Gerätetreibern enthält, die Sie in Configuration Manager importieren. Der Treiberkatalog befindet sich im Arbeitsbereich **Softwarebibliothek** . Er besteht aus zwei Knoten: **Treiber** und **Treiberpakete**. Im Knoten **Treiber** sind alle Treiber aufgelistet, die Sie in den Treiberkatalog importiert haben. Verwenden Sie diesen Knoten, um Details zu jedem importierten Treiber zu ermitteln, die Treiber im Treiberpaket oder Startabbild zu ändern, einen Treiber zu aktivieren oder deaktivieren usw.  

###  <a name="BKMK_ImportDrivers"></a> Importieren von Gerätetreibern in den Gerätekatalog  
 Bei der Bereitstellung eines Betriebssystems müssen Sie Gerätetreiber in den Treiberkatalog importieren, bevor Sie sie verwenden können. Sie können die Verwaltung Ihrer Gerätetreiber vereinfachen, indem Sie nur die Gerätetreiber importieren, die Sie im Rahmen der Betriebssystembereitstellung installieren möchten. Sie können aber auch mehrere Versionen der Gerätetreiber im Treiberkatalog speichern, um auf einfache Art Upgrades bei vorhandenen Gerätetreibern auszuführen, wenn sich die Hardwaregeräteanforderungen in Ihrem Netzwerk ändern.  

 Im Rahmen des Importvorgangs für den Gerätetreiber werden von Configuration Manager Informationen gelesen, die dem Gerät zugeordnet sind, darunter Anbieter, Klasse, Version, Signatur sowie unterstützte Hardware und Plattformen. Der Treiber wird standardmäßig nach dem ersten Hardwaregerät benannt, das von ihm unterstützt wird. Sie können den Gerätetreiber aber zu einem späteren Zeitpunkt umbenennen. Die Liste der unterstützten Plattformen beruht auf den Informationen in der INF-Datei des Treibers. Diese Informationen sind jedoch nicht immer vollständig. Überprüfen Sie daher nach dem Import eines Treibers in den Treiberkatalog manuell, ob der Gerätetreiber unterstützt wird.  

 Nachdem Sie Gerätetreiber in den Katalog importiert haben, können Sie die Gerätetreiber zudem Treiberpaketen oder Startabbildpaketen hinzufügen.  

> [!IMPORTANT]  
>  Es ist nicht möglich, Gerätetreiber direkt in einen Unterordner des Knotens **Treiber** zu importieren. Zum Importieren eines Gerätetreibers in einen Unterordner importieren Sie den Gerätetreiber zuerst in den Knoten **Treiber** , und verschieben Sie den Treiber dann in den Unterordner.  

 Gehen Sie wie folgt vor, um Windows-Gerätetreiber zu importieren.  

#### <a name="to-import-windows-device-drivers-into-the-driver-catalog"></a>So importieren Sie Windows-Gerätetreiber in den Treiberkatalog  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Treiber**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Treiber importieren** , um den **** Treiberimport-Assistenten zu starten.  

4.  Geben Sie auf der Seite **Treiber suchen** die folgenden Optionen an, und klicken Sie dann auf **Weiter**:  

    -   **Alle Treiber im folgenden Netzwerkpfad (UNC) importieren**: Geben Sie den Netzwerkpfad zu einem Gerätetreiberordner an, um alle Gerätetreiber zu importieren, die sich in einem bestimmten Ordner befinden. Beispiel:  **\\\Servername\Ordner**.  

        > [!NOTE]  
        >  Der Prozess zum Importieren aller Treiber kann eine Weile dauern, wenn viele Ordner und viele Treiberdateien (.inf) vorhanden sind.  

    -   **Bestimmten Treiber importieren**: Geben Sie den Netzwerkpfad (UNC) zur INF-Datei des Windows-Gerätetreibers oder zur Datei „Txtsetup.oem“ eines Massenspeichertreibers an, um einen bestimmten Treiber aus einem Ordner zu importieren.  

    -   **Option für doppelte Treiber angeben**: Geben Sie an, wie in Configuration Manager Treiberkategorien verwaltet werden sollen, wenn ein doppelter Gerätetreiber importiert wird.  

    > [!IMPORTANT]  
    >  Wenn Sie Treiber importieren, muss der Standortserver über die ****  Leseberechtigung für diesen Ordner verfügen. Andernfalls tritt beim Import ein Fehler auf.  

5.  Geben Sie auf der Seite **Treiberdetails** die folgenden Optionen an, und klicken Sie dann auf **Weiter**:  

    -   **Treiber ausblenden, die nicht in einer Speicher- oder Netzwerkklasse (für Startabbilder) enthalten sind**: Verwenden Sie diese Einstellung, um nur Speicher- und Netzwerktreiber anzuzeigen und andere Treiber, die in der Regel nicht für Startabbilder benötigt werden, z. B. Videotreiber oder Modemtreiber, auszublenden.  

    -   **Treiber ausblenden, die nicht digital signiert sind**: Verwenden Sie diese Einstellung, um Treiber auszublenden, die nicht digital signiert sind.  

    -   Wählen Sie in der Treiberliste die Treiber aus, die Sie in den Treiberkatalog importieren möchten.  

    -   **Diese Treiber aktivieren und Installation auf Computern zulassen**: Aktivieren Sie diese Einstellung, damit die Gerätetreiber auf Computern installiert werden können. Standardmäßig ist dieses Kontrollkästchen aktiviert.  

        > [!IMPORTANT]  
        >  Wenn ein Gerätetreiber ein Problem verursacht oder Sie die Installation eines Gerätetreibers anhalten möchten, können Sie den Gerätetreiber deaktivieren. Deaktivieren Sie dazu das Kontrollkästchen **Diese Treiber aktivieren und Installation auf Computern zulassen** . Sie können Treiber auch deaktivieren, nachdem sie importiert wurden.  

    -   Klicken Sie auf die Schaltfläche **Kategorien** , wenn Sie die Gerätetreiber zu Filterzwecken einer Verwaltungskategorie wie „Desktops“ oder „Notebooks“ zuweisen möchten. Wählen Sie dann eine vorhandene Kategorie aus, oder erstellen Sie eine neue Kategorie. Mit der Kategoriezuweisung können Sie auch konfigurieren, welche Gerätetreiber vom Tasksequenzschritt [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) auf die Bereitstellung angewendet werden.  

6.  Wählen Sie auf der Seite **Treiber zu Paketen hinzufügen** aus, ob die Treiber einem Paket hinzugefügt werden sollen, und klicken Sie auf **Weiter**. Berücksichtigen beim Hinzufügen von Treibern zu einem Paket Folgendes:  

    -   Wählen Sie die Treiberpakete aus, die zur Verteilung der Gerätetreiber verwendet werden.  

         Klicken Sie optional auf **Neues Paket** , um ein neues Treiberpaket zu erstellen. Wenn Sie ein neues Treiberpaket erstellen, müssen Sie eine Netzwerkfreigabe angeben, die nicht von anderen Treiberpaketen verwendet wird.  

    -   Wenn das Paket bereits an Verteilungspunkte verteilt wurde, klicken Sie im Dialogfeld auf **Ja** , um die Startabbilder auf Verteilungspunkten zu aktualisieren. Sie können Gerätetreiber erst verwenden, nachdem sie an Verteilungspunkte verteilt wurden. Wenn Sie auf **Nein**klicken, müssen Sie die Aktion **Verteilungspunkte aktualisieren** ausführen, bevor das Startabbild die aktualisierten Treiber enthält. Ist das Treiberpaket nie verteilt worden, müssen Sie am Knoten **Treiberpakete** auf **Inhalt verteilen** klicken.  

7.  Wählen Sie auf der Seite **Treiber zu Startabbildern hinzufügen** , ob die Gerätetreiber vorhandenen Startabbildern hinzugefügt werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie ein Startabbild auswählen, beachten Sie Folgendes:  

    > [!NOTE]  
    >  Es wird empfohlen, den Startabbildern für die Bereitstellung von Betriebssystemen nur Massenspeicher- und Netzwerkgerätetreiber hinzuzufügen.  

    -   Klicken Sie im Dialogfeld auf **Ja** , um ein Update der  Startabbilder auf Verteilungspunkten auszuführen. Sie können Gerätetreiber erst verwenden, nachdem sie an Verteilungspunkte verteilt wurden. Wenn Sie auf **Nein**klicken, müssen Sie die Aktion **Verteilungspunkte aktualisieren** ausführen, bevor das Startabbild die aktualisierten Treiber enthält. Ist das Treiberpaket nie verteilt worden, müssen Sie am Knoten **Treiberpakete** auf **Inhalt verteilen** klicken.  

    -   Configuration Manager gibt eine Warnung aus, wenn die Architektur für einen oder mehrere Treiber nicht mit der Architektur der von Ihnen ausgewählten Startimages übereinstimmt. Wenn das der Fall ist, klicken Sie auf **OK** , und kehren Sie zur Seite **Treiberdetails** zurück, um die Treiber zu deaktivieren, die der Architektur des ausgewählten Startabbilds nicht entsprechen. Wenn Sie beispielsweise ein x64- und x86-Startabbild auswählen, müssen alle Treiber beide Architekturen unterstützen. Wenn Sie ein x64-Startabbild auswählen, müssen alle Treiber die x64-Architekturen unterstützen.  

        > [!NOTE]  
        >  -   Die Architektur basiert auf derjenigen, die in der INF-Datei vom Hersteller angegeben ist.  
        > -   Wenn für einen Treiber angegeben ist, dass er beide Architekturen unterstützt, können Sie ihn in jedes der Startabbilder importieren.  

    -   Configuration Manager gibt eine Warnung aus, wenn Sie Gerätetreiber hinzufügen, die keine Netzwerk- oder Speichertreiber für ein Startimage sind, da diese in den meisten Fällen nicht für das Startimage erforderlich sind. Klicken Sie auf **Ja** , um die Treiber zum Startabbild hinzuzufügen, oder auf **Nein** , um zurückzukehren und die Treiberauswahl zu ändern.  

    -   Configuration Manager gibt eine Warnung aus, wenn einer oder mehrere der ausgewählten Treiber nicht ordnungsgemäß digital signiert sind. Klicken Sie auf **Ja** , um fortzufahren, oder auf **Nein** , um zurückzukehren und die Treiberauswahl zu ändern.  

8.  Schließen Sie den Assistenten ab.  

###  <a name="BKMK_ModifyDriverPackage"></a> Verwalten von Gerätetreibern in einem Treiberpaket  
 Gehen Sie wie folgt vor, um Treiberpakete und Startabbilder zu ändern. Zum Hinzufügen oder Entfernen von Gerätetreibern suchen Sie die Treiber im Knoten **Treiber** , und bearbeiten Sie dann die Pakete oder Startabbilder, denen die ausgewählten Treiber zugeordnet sind.  

#### <a name="to-modify-the-device-drivers-in-a-driver-package"></a>So ändern Sie die Gerätetreiber in einem Treiberpaket  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Treiber**.  

3.  Wählen Sie im Knoten **Treiber** die Gerätetreiber aus, die Sie dem Treiberpaket hinzufügen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Treiber** auf **Bearbeiten**und dann auf **Treiberpakete**.  

5.  Zum Hinzufügen eines Gerätetreibers aktivieren Sie das Kontrollkästchen für die Treiberpakete, denen Sie den Gerätetreiber hinzufügen möchten. Zum Entfernen eines Gerätetreibers deaktivieren Sie das Kontrollkästchen für die Treiberpakete, aus denen Sie den Gerätetreiber entfernen möchten.  

     Wenn Sie Gerätetreiber hinzufügen, die Treiberpaketen zugeordnet sind, können Sie optional ein neues Paket erstellen, indem Sie auf **Neues Paket**klicken. Hierdurch wird das Dialogfeld **Treiberpaket erstellen** geöffnet.  

6.  Wenn das Paket bereits an Verteilungspunkte verteilt wurde, klicken Sie im Dialogfeld auf **Ja** , um die Startabbilder auf Verteilungspunkten zu aktualisieren. Sie können Gerätetreiber erst verwenden, nachdem sie an Verteilungspunkte verteilt wurden. Wenn Sie auf **Nein**klicken, müssen Sie die Aktion **Verteilungspunkte aktualisieren** ausführen, bevor das Startabbild die aktualisierten Treiber enthält. Ist das Treiberpaket nie verteilt worden, müssen Sie am Knoten **Treiberpakete** auf **Inhalt verteilen** klicken. Bevor die Treiber zur Verfügung stehen, müssen Sie das Treiberpaket auf Verteilungspunkten aktualisieren.  

     Klicken Sie auf **OK**.  

###  <a name="BKMK_ManageDriversBootImage"></a> Verwalten von Gerätetreibern in einem Startabbild  
 Sie können Startabbildern Windows-Gerätetreiber hinzufügen, die in den Treiberkatalog importiert wurden. Verwenden Sie die folgenden Richtlinien, wenn Sie einem Startabbild Gerätetreiber hinzufügen:  

-   Fügen Sie Startabbildern nur Gerätetreiber für Massenspeichergeräte und Netzwerkadapter hinzu, da andere Treibertypen nicht grundsätzlich erforderlich sind. Durch Treiber, die nicht erforderlich sind, wird die Größe des Startabbilds unnötig erhöht.  

-   Fügen Sie Startabbildern nur Gerätetreiber für Windows 10 hinzu, da die erforderliche Version von Windows PE auf Windows 10 basiert.  

-   Vergewissern Sie sich, dass Sie die richtigen Gerätetreiber für die Startabbildarchitektur verwenden.  Fügen Sie einem x64-Startabbild keinen x86-Gerätetreiber hinzu.  

 Gehen Sie wie folgt vor, um Gerätetreiber in einem Startabbild hinzuzufügen oder zu entfernen.  

#### <a name="to-modify-the--device-drivers-associated-with-a-boot-image"></a>So ändern Sie Gerätetreiber, die einem Startabbild zugeordnet sind  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Treiber**.  

3.  Wählen Sie im Knoten **Treiber** die Gerätetreiber aus, die Sie dem Treiberpaket hinzufügen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Treiber** auf **Bearbeiten**und dann auf **Startabbilder**.  

5.  Zum Hinzufügen eines Gerätetreibers aktivieren Sie das Kontrollkästchen für das Startabbild, dem Sie den Gerätetreiber hinzufügen möchten. Zum Entfernen eines Gerätetreibers aktivieren Sie das Kontrollkästchen für das Startabbild, aus dem Sie den Gerätetreiber entfernen möchten.  

6.  Deaktivieren Sie das Kontrollkästchen **Verteilungspunkte nach Abschluss aktualisieren** , wenn Sie kein Update der Verteilungspunkte, auf denen das Startabbild gespeichert wird, ausführen möchten. Standardmäßig wird ein Update der Verteilungspunkte ausgeführt, wenn ein Update des Startabbilds ausgeführt wird.  

     Klicken Sie auf **OK** , und beachten Sie Folgendes:  

    -   Klicken Sie im Dialogfeld auf **Ja** , um ein Update der  Startabbilder auf Verteilungspunkten auszuführen. Sie können Gerätetreiber erst verwenden, nachdem sie an Verteilungspunkte verteilt wurden. Wenn Sie auf **Nein**klicken, müssen Sie die Aktion **Verteilungspunkte aktualisieren** ausführen, bevor das Startabbild die aktualisierten Treiber enthält. Ist das Treiberpaket nie verteilt worden, müssen Sie am Knoten **Treiberpakete** auf **Inhalt verteilen** klicken.  

    -   Configuration Manager gibt eine Warnung aus, wenn die Architektur für einen oder mehrere Treiber nicht mit der Architektur der von Ihnen ausgewählten Startimages übereinstimmt. Wenn das der Fall ist, klicken Sie auf **OK** , und kehren Sie zur Seite **Treiberdetails** zurück, um die Treiber zu deaktivieren, die der Architektur des ausgewählten Startabbilds nicht entsprechen. Wenn Sie beispielsweise ein x64- und x86-Startabbild auswählen, müssen alle Treiber beide Architekturen unterstützen. Wenn Sie ein x64-Startabbild auswählen, müssen alle Treiber die x64-Architekturen unterstützen.  

        > [!NOTE]  
        >  -   Die Architektur basiert auf derjenigen, die in der INF-Datei vom Hersteller angegeben ist.  
        > -   Wenn für einen Treiber angegeben ist, dass er beide Architekturen unterstützt, können Sie ihn in jedes der Startabbilder importieren.  

    -   Configuration Manager gibt eine Warnung aus, wenn Sie Gerätetreiber hinzufügen, die keine Netzwerk- oder Speichertreiber für ein Startimage sind, da diese in den meisten Fällen nicht für das Startimage erforderlich sind. Klicken Sie auf **Ja** , um die Treiber zum Startabbild hinzuzufügen, oder auf **Nein** , um zurückzukehren und die Treiberauswahl zu ändern.  

    -   Configuration Manager gibt eine Warnung aus, wenn einer oder mehrere der ausgewählten Treiber nicht ordnungsgemäß digital signiert sind. Klicken Sie auf **Ja** , um fortzufahren, oder auf **Nein** , um zurückzukehren und die Treiberauswahl zu ändern.  

7.  Klicken Sie auf **OK**.  

###  <a name="BKMK_DriverActions"></a> Zusätzliche Aktionen für Gerätetreiber  
 Sie können zusätzliche Aktionen zur Verwaltung von Gerätetreibern ausführen, wenn Sie im Knoten **Treiber** mindestens einen Gerätetreiber auswählen. Diese Aktionen umfassen Folgendes:  

|Aktion|Beschreibung|  
|------------|-----------------|  
|**Kategorisieren**|Hiermit wird eine Verwaltungskategorie für die ausgewählten Gerätetreiber gelöscht, verwaltet oder festgelegt.|  
|**Löschen**|Hiermit wird der Gerätetreiber aus dem Knoten **Treiber** entfernt. Außerdem wird der Treiber aus den zugeordneten Verteilungspunkten entfernt|  
|**Deaktivieren**|Hiermit wird die Installation des Gerätetreibers verhindert. Sie können Gerätetreiber vorübergehend deaktivieren, damit sie nicht von Configuration Manager-Clientcomputern und Tasksequenzen installiert werden können, wenn Sie Betriebssysteme bereitstellen. **Hinweis:**  Die Aktion „Deaktivieren“ verhindert nur, dass Treiber mit dem Tasksequenzschritt „Treiber automatisch anwenden“ installiert werden.|  
|**Aktivieren**|Hiermit wird es den Configuration Manager-Clientcomputern und Tasksequenzen gestattet, den Gerätetreiber zu installieren, wenn das Betriebssystem bereitgestellt wird.|  
|**Verschieben**|Hiermit wird der Gerätetreiber im Knoten **Treiber** in einen anderen Ordner verschoben.|  
|**Eigenschaften**|Hiermit wird das Dialogfeld **Eigenschaften** geöffnet, in dem Sie die Eigenschaften des Gerätetreibers prüfen und ändern können. Beispielsweise können Sie den Namen und die Beschreibung des Gerätetreibers ändern, den Gerätetreiber aktivieren sowie angeben, auf welchen Plattformen der Gerätetreiber ausgeführt werden kann.|  

##  <a name="BKMK_TSDrivers"></a> Verwenden von Tasksequenzen zum Installieren von Gerätetreibern  
 Verwenden Sie Tasksequenzen, um die Art der Bereitstellung des Betriebssystems zu automatisieren. Von jedem Schritt in der Tasksequenz kann eine bestimmte Aktion ausgeführt werden, beispielsweise die Installation eines Gerätetreibers. Sie können die folgenden beiden Tasksequenzschritte verwenden, um Gerätetreiber zu installieren, während Sie Betriebssysteme bereitstellen:  

-   [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): Mit diesem Schritt werden Gerätetreiber automatisch als Teil einer Betriebssystembereitstellung ausgewählt und installiert. Sie können den Tasksequenzschritt so konfigurieren, dass nur der am besten passende Treiber für jedes ermittelte Hardwaregerät installiert wird. Sie können auch angeben, dass alle kompatiblen Treiber für jedes ermittelte Hardwaregerät installiert werden und der am besten passenden Treiber von Windows Setup ausgewählt werden soll. Zusätzlich können Sie eine Kategorie von Gerätetreibern angeben, um die für diesen Schritt verfügbaren Treiber zu begrenzen.  

-   [Apply Driver Package](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): Mit diesem Schritt können Sie alle Gerätetreiber in einem bestimmten Treiberpaket für Windows Setup zur Verfügung stellen. Die angegebenen Treiberpakete werden von Windows Setup nach den erforderlichen Gerätetreibern durchsucht. Beim Erstellen eigenständiger Medien müssen Sie diesen Schritt zum Installieren von Gerätetreibern ausführen.  

 Wenn Sie diese Tasksequenzschritte verwenden, können Sie auch angeben, wie die Gerätetreiber auf dem Computer, auf dem Sie das Betriebssystem bereitstellen, installiert werden sollen. Weitere Informationen finden Sie unter [Verwalten von Tasksequenzen zum Automatisieren von Aufgaben](../deploy-use/manage-task-sequences-to-automate-tasks.md).  

##  <a name="BKMK_InstallingDeviceDiriversTS"></a> Verwenden von Tasksequenzen zum Installieren von Gerätetreibern auf Computern  
 Gehen Sie wie folgt vor, um Gerätetreiber als Teil der Betriebssystembereitstellung zu installieren.  

#### <a name="use-a-task-sequence-to-install-device-drivers"></a>Verwenden einer Tasksequenz zum Installieren von Gerätetreibern  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Wählen Sie im Knoten **Tasksequenzen** die Tasksequenz aus, die Sie ändern möchten, um den Gerätetreiber zu installieren, und klicken Sie dann auf **Bearbeiten**.  

4.  Wechseln Sie zu dem Speicherort, an dem Sie die ****  Treiberschritte hinzufügen möchten, klicken Sie auf **Hinzufügen**, und wählen Sie dann **Treiber**aus.  

5.  Fügen Sie den Schritt **Treiber automatisch anwenden** hinzu, wenn von der Tasksequenz alle Gerätetreiber oder bestimmte angegebene Kategorien installiert werden sollen. Geben Sie auf der Registerkarte **Eigenschaften** die Optionen für den Schritt und ggf. auf der Registerkarte **Optionen** die Bedingungen für den Schritt an.  

     Fügen Sie den Schritt **Treiberpaket anwenden** hinzu, wenn nur die im angegebenen Paket enthaltenen Gerätetreiber von der Tasksequenz installiert werden sollen. Geben Sie auf der Registerkarte **Eigenschaften** die Optionen für den Schritt und ggf. auf der Registerkarte **Optionen** die Bedingungen für den Schritt an.  

    > [!IMPORTANT]  
    >  Für eine Problembehandlung der Tasksequenz können Sie auf der Registerkarte **Optionen** das Kontrollkästchen **Diesen Schritt deaktivieren** aktivieren, um den Schritt zu deaktivieren.  

6.  Klicken Sie auf **OK** , um die Tasksequenz zu speichern.  

 Weitere Informationen zum Erstellen einer Tasksequenz zum Installieren eines Betriebssystems finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).  

##  <a name="BKMK_DriverReports"></a> Berichte zur Treiberverwaltung  
 Sie können mehrere Berichte in der Berichtkategorie **Treiberverwaltung** verwenden, um allgemeine Informationen zu den Gerätetreibern im Treiberkatalog zu erhalten. Weitere Informationen zu Berichten finden Sie unter [Berichterstellung](../../core/servers/manage/reporting.md).
