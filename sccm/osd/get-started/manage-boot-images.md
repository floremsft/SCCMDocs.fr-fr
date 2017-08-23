---
title: "Verwalten von Startimages – Configuration Manager | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie in Configuration Manager die Windows PE-Startimages verwalten, die Sie während der Bereitstellung von Betriebssystemen verwenden."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: "23"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: cc678c1133b1944f55bcad309cf9ede9f0660b57
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Verwalten von Startimages mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ein Startimage in Configuration Manager ist ein [Windows PE-Image (WinPE)](https://msdn.microsoft.com/library/windows/hardware/dn938389%28v=vs.85%29.aspx), das während einer Betriebssystembereitstellung verwendet wird. Startimages dienen zum Starten eines Computers in Windows PE, einem minimalen Betriebssystem mit begrenzten Komponenten und Diensten zur Vorbereitung des Zielcomputers für die Windows-Installation.  Gehen Sie wie in den folgenden Abschnitten beschrieben vor, um Startimages zu verwalten:

## <a name="BKMK_BootImageDefault"></a> Standardstartimages
Configuration Manager stellt zwei Standardstartimages bereit: ein Startimage zur Unterstützung von x86-Plattformen und eines zur Unterstützung von x64-Plattformen. Diese Images sind hier gespeichert: \\\\*Servername*>\SMS_<*Standortcode*>\osd\boot\\<*x64*> oder <*i386*>. Die Standardstartimages werden je nach der von Ihnen ausgeführten Aktion aktualisiert oder neu generiert.

Beachten Sie Folgendes für sämtliche Aktionen, die in den folgenden Abschnitten beschrieben werden:
- Die Quelltreiberobjekte müssen gültig sein, einschließlich der Treiberquelldateien, da die Treiber andernfalls nicht den Startimages im Speicherort hinzugefügt werden.
- Startimages, die nicht auf den standardmäßigen Startimages basieren, selbst wenn sie dieselbe Version von Windows PE verwenden, werden nicht angepasst.
- Sie müssen die angepassten Startimages neu auf Verteilungspunkten verteilen.
- Sie müssen alle Medien neu erstellen, die die geänderten Startimages verwenden.
- Wenn die benutzerdefinierten oder Standardstartimages nicht automatisch aktualisiert werden sollen, speichern Sie sie nicht am Standardspeicherort.

> [!NOTE]
> Das Ablaufprotokolltool von Configuration Manager wird allen Startimages hinzugefügt, die Sie der **Softwarebibliothek** hinzufügen. In Windows PE können Sie das Ablaufprotokolltool von Configuration Manager starten, indem Sie **CMTrace** in einer Befehlszeile eingeben.  

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Verwenden Sie Updates und Wartungen, um die neueste Version des Configuration Manager zu installieren.
Wenn Sie die Windows ADK-Version ab Version 1702 upgraden und dann Updates und Wartung zum Installieren der neuesten Version von Configuration Manager verwenden, generiert Configuration Manager ab dieser Version die Standardstartimages neu. Dies schließt die neue Windows PE-Version vom aktualisierten Windows ADK ein, die neue Version des Configuration Manager-Clients, Treiber, Anpassungen und so weiter. Benutzerdefinierte Startimages werden nicht geändert.

Vor Version 1702 aktualisiert Configuration Manager das vorhandene Startimage (boot.wim) mit den Clientkomponenten, Treibern, Anpassungen usw. Es wird jedoch nicht die neueste Windows PE-Version vom Windows ADK verwendet. Sie müssen das Startimage manuell anpassen, um die neueste Version des Windows ADK zu verwenden.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Aktualisieren von Configuration Manager 2012 auf Configuration Manager Current Branch (CB)
Wenn Sie Configuration Manager 2012 auf Configuration Manager CB mithilfe des Installationsprozesses upgraden, generiert Configuration Manager die Standardstartimages neu. Dies schließt die neue Windows PE-Version vom aktualisierten Windows ADK ein, die neue Version des Configuration Manager-Clients sowie alle Anpassungen bleiben unverändert. Benutzerdefinierte Startimages werden nicht geändert.

### <a name="update-distribution-points-with-the-boot-image"></a>Aktualisieren von Verteilungspunkten mithilfe des Startabbilds
Wenn Sie die Aktion **Update Distribution Points** (Verteilungspunkte aktualisieren) aus dem Knoten **Boot Images** (Startimages) in der Configuration Manager-Konsole verwenden, aktualisiert Configuration Manager die Standardstartimages mit den Clientkomponenten, den Treibern, den Anpassungen usw.    

Ab Version 1706 des Configuration Manager können Sie wahlweise die neueste Version von Windows PE in das Startimage laden (aus dem Installationsverzeichnis von Windows ADK). Die Seite **Allgemein** des Assistenten für die Aktualisierung von Verteilungspunkten enthält Informationen über die auf dem Standortserver installierte Windows ADK-Version, die Windows ADK-Version, von der aus Windows PE im Startimage verwendet wurde, und die Version des Configuration Manager-Clients. Anhand dieser Informationen können Sie entscheiden, ob Sie das Startimage erneut laden möchten. Darüber hinaus wurde eine neue Spalte hinzugefügt (**Clientversion**), die angezeigt wird, wenn Sie Startimages im Knoten **Startimages** anzeigen, damit Sie wissen, welche Version des Configuration Manager-Clients jedes Startimage verwendet.    

Benutzerdefinierte Startimages werden nicht geändert.

##  <a name="BKMK_BootImageCustom"></a> Anpassen eines Startimages  
 Sie können ein Startimage über die Configuration Manager-Konsole anpassen oder [ein Startimage ändern](#BKMK_ModifyBootImages), wenn das Image auf einer Windows PE-Version aus der unterstützten Version von Windows ADK basiert. Wenn ein Standort mit einer neuen Version aktualisiert wird und eine neue Version von Windows ADK installiert wird, werden benutzerdefinierte Startimages (die sich nicht im Standardspeicherort für Startimages befinden) nicht mit der neuen Version von Windows ADK aktualisiert. In diesem Fall können Sie die Startimages in der Configuration Manager-Konsole nicht mehr anpassen. Diese funktionieren jedoch weiterhin wie vor dem Upgrade.  

 Wenn ein Startimage auf einer anderen Version des an einem Standort installierten Windows ADK basiert, müssen Sie die Startimages mithilfe eines anderen Verfahrens anpassen, beispielsweise mit dem DISM-Befehlszeilenprogramm (Deployment Image Servicing and Management), das Bestandteil von Windows AIK und Windows ADK ist. Weitere Informationen zu Startimages finden Sie unter [Anpassen von Startimages](customize-boot-images.md).  

##  <a name="BKMK_AddBootImages"></a> Hinzufügen eines Startimages  

 Bei einer Standortinstallation fügt Configuration Manager automatisch Startimages hinzu, die auf einer WinPE-Version aus der unterstützten Version von Windows ADK basieren. Abhängig von der Configuration Manager-Version können Sie möglicherweise Startimages hinzufügen, die auf einer anderen WinPE-Version aus der unterstützten Version von Windows ADK basieren.  Es tritt ein Fehler auf, wenn Sie versuchen, ein Startabbild hinzuzufügen, das eine nicht unterstützte Version von WinPE enthält.  

 Im Folgenden finden Sie die jeweils unterstützte Version des Windows ADK, die Windows PE-Version, auf der das Startimage basiert, das über die Configuration Manager-Konsole angepasst werden kann, und die Windows PE-Versionen, auf denen das Startimage basiert, das Sie mithilfe von DISM anpassen und anschließend Configuration Manager hinzufügen können.  

-   **Windows ADK-Version**  

     Windows ADK für Windows 10  

-   **Windows PE-Versionen für Startimages, die über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 10  

-   **Unterstützte Windows PE-Versionen für Startimages, die nicht über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 3.1<sup>1</sup> und Windows PE 5  

     <sup>1</sup> Sie können zu Configuration Manager nur dann ein Startimage hinzufügen, wenn es auf Windows PE 3.1 basiert. Installieren Sie die Ergänzung zu Windows AIK für Windows 7 SP1, um ein Upgrade von Windows AIK für Windows 7 (basierend auf Windows PE 3) mit der Ergänzung zu Windows AIK für Windows 7 SP1 (basierend auf Windows PE 3.1) durchzuführen. Sie können die Ergänzung zu Windows AIK für Windows 7 SP1 aus dem [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=5188)herunterladen.  

     Im Fall von Configuration Manager etwa können Sie Startimages aus Windows ADK für Windows 10 (das auf Windows PE 10 basiert) über die Configuration Manager-Konsole anpassen. Zwar werden auf Windows PE 5 basierende Startabbilder unterstützt, doch müssen Sie sie von einem anderen Computer aus anpassen und die mit dem Windows ADK für Windows 8 installierte DISM-Version verwenden. Danach können Sie das Startimage der Configuration Manager-Konsole hinzufügen. Weitere Informationen und Vorgehensweisen zum Anpassen eines Startimages (Hinzufügen von optionalen Komponenten und Treibern), zum Aktivieren der Befehlsunterstützung für das Startimage, zum Hinzufügen des Startimages zur Configuration Manager-Konsole und zum Aktualisieren der Verteilungspunkte mit dem Startimage finden Sie unter [Anpassen von Startimages](customize-boot-images.md).

 Gehen Sie wie folgt vor, um ein Startabbild manuell hinzuzufügen.  

#### <a name="to-add-a-boot-image"></a>So fügen Sie ein Startabbild hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Startabbild hinzufügen** , um den Assistenten zum Hinzufügen von Startabbildern zu starten.  

4.  Geben Sie auf der Seite **Datenquelle** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie im Feld **Pfad** den Pfad der Startabbilddatei (WIM-Datei) an.  

         Der angegebene Pfad muss ein gültiger Netzwerkpfad im UNC-Format sein. Zum Beispiel: \\\\<*Servername*\\<*Freigabename*>\\<*Startimagename*>.wim.  

    -   Wählen Sie das Startabbild in der Dropdownliste **Startabbild** aus. Wenn die WIM-Datei mehrere Startabbilder enthält, wählen Sie das gewünschte Abbild aus.  

5.  Geben Sie auf der Seite **Allgemein**  die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

    -   Geben Sie im Feld **Name** einen eindeutigen Namen für das Startabbild an.  

    -   Geben Sie im Feld **Version** eine Versionsnummer für das Startabbild an.  

    -   Geben Sie im Feld **Kommentar** anhand einer kurzen Beschreibung an, wie das Startabbild verwendet werden soll.  

6.  Schließen Sie den Assistenten ab.  

 Das Startimage wird jetzt im Knoten **Startimage** der Configuration Manager-Konsole aufgeführt. Allerdings müssen Sie das Startabbild an Verteilungspunkte, Verteilungspunktgruppen oder Sammlungen, die Verteilungspunktgruppen zugeordnet sind, verteilen, damit Sie es zur Bereitstellung eines Betriebssystems verwenden können.  

> [!NOTE]  
>  Wenn Sie den Knoten **Startimage** in der Configuration Manager-Konsole auswählen, wird in der Spalte **Größe (KB)** die dekomprimierte Größe des jeweiligen Startimages angezeigt. Wenn ein Startimage hingegen von Configuration Manager über das Netzwerk gesendet wird, wird eine komprimierte Kopie des Images gesendet, die normalerweise eine wesentlich geringere Größe hat als in der Spalte **Größe (KB)** angegeben.  

##  <a name="BKMK_DistributeBootImages"></a> Verteilen von Startimages an einen Verteilungspunkt  
 Startabbilder werden genau wie anderer Inhalt an Verteilungspunkte verteilt. In den meisten Fällen müssen Sie das Startabbild an mindestens einen Verteilungspunkt verteilen, bevor Sie ein Betriebssystem bereitstellen und bevor Sie Medien erstellen.  

> [!NOTE]  
>  Wenn Sie PXE verwenden möchten, um ein Betriebssystem bereitzustellen, sollten Sie folgende Punkte beachten, bevor Sie das Startabbild verteilen:  
>   
>  -   Der Verteilungspunkt muss so konfiguriert sein, dass er PXE-Anforderungen akzeptiert.  
> -   Sie müssen sowohl ein x86- als auch ein x64-PXE-fähiges Startabbild an mindestens einen PXE-fähigen Verteilungspunkt verteilen.  
> -   Configuration Manager verteilt die Startimages an den Ordner **RemoteInstall** auf dem PXE-fähigen Verteilungspunkt.  
>   
>  Weitere Informationen zur Verwendung von PXE zum Bereitstellen von Betriebssystemen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Die Schritte zum Verteilen eines Startabbilds finden Sie unter [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a> Ändern eines Startimages  
 Sie können dem Abbild Gerätetreiber hinzufügen, Gerätetreiber aus dem Abbild entfernen oder die Eigenschaften des Startabbilds bearbeiten. Die Gerätetreiber, die Sie hinzufügen oder entfernen, können Treiber für Netzwerkkarten oder Massenspeichergeräte umfassen. Berücksichtigen Sie beim Ändern von Startabbildern die folgenden Faktoren:  

-   Sie müssen die Gerätetreiber in den Gerätetreiberkatalog importieren und dort aktivieren, bevor Sie sie dem Startabbild hinzufügen können.  

-   Wenn Sie ein Startabbild ändern, wird keines der zugewiesenen Pakete geändert, auf die das Startabbild verweist.  

-   Nachdem Sie Änderungen an einem Startabbild vorgenommen haben, müssen Sie das Startabbild auf den Verteilungspunkten **aktualisieren** , auf denen das Startabbild bereits vorhanden ist, sodass die neueste Version des Startabbilds verfügbar ist. Weitere Informationen finden Sie unter [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

 Gehen Sie wie folgt vor, um ein Startabbild zu ändern.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>So ändern Sie die Eigenschaften eines Startabbilds  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

3.  Wählen Sie das Startabbild aus, das Sie ändern möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** , um das Dialogfeld **Eigenschaften** für das Startabbild zu öffnen.  

5.  Legen Sie die folgenden Einstellungen fest, um das Verhalten des Startabbilds zu ändern:  

    -   Klicken Sie auf der Registerkarte **Abbilder** auf **Neu laden**, wenn Sie die Eigenschaften des Startabbilds mithilfe eines externen Tools geändert haben.  

    -   Fügen Sie auf der Registerkarte **Treiber** die Windows-Gerätetreiber hinzu, die zum Starten von WinPE erforderlich sind. Beachten Sie beim Hinzufügen von Gerätetreibern die folgenden Punkte:  

        -   Wählen Sie **Hide drivers that do not match the architecture of the boot image** (Treiber ausblenden, die nicht mit der Architektur des Startimages übereinstimmen) aus, damit nur Treiber für die Architektur des Startimages angezeigt werden. Die Architektur basiert auf derjenigen, die in der INF-Datei vom Hersteller angegeben ist.  

        -   Wählen Sie **Treiber ausblenden, die nicht in einer Speicher- oder Netzwerkklasse (für Startabbilder) enthalten sind** aus, um nur Speicher- und Netzwerktreiber anzuzeigen und andere Treiber, die in der Regel nicht für Startabbilder benötigt werden, z. B. Videotreiber oder Modemtreiber, auszublenden.  

        -   Wählen Sie **Treiber ausblenden, die nicht digital signiert sind** aus, um Treiber auszublenden, die nicht digital signiert sind.  

        -   Es wird empfohlen, dem Startabbild nur NIC- und Massenspeichertreiber hinzuzufügen, es sei denn, für WinPE sind andere Treiber erforderlich.  

        -   Da in WinPE bereits zahlreiche Treiber integriert sind, fügen Sie nur die NIC- und Massenspeichertreiber hinzu, die nicht mit WindPE bereitgestellt werden.  

        -   Stellen Sie sicher, dass die dem Startimage hinzugefügten Treiber der Architektur des Startimages entsprechen.  

        > [!NOTE]  
        >  Sie müssen Gerätetreiber in den Treiberkatalog importieren, bevor Sie sie einem Startabbild hinzufügen. Informationen zum Importieren von Gerätetreibern finden Sie unter [Verwalten von Treibern](manage-drivers.md).  

    -   Wählen Sie auf der Registerkarte **Anpassung** die folgenden Einstellungen aus:  

        -   Aktivieren Sie das Kontrollkästchen **Prestart-Befehl aktivieren** , um einen Befehl anzugeben, der vor der Tasksequenz ausgeführt werden soll. Wenn Prestart-Befehle aktiviert sind, können Sie angeben, welche Befehlszeile ausgeführt werden soll, ob zur Ausführung des Befehls unterstützende Dateien erforderlich sind und wie der Quellpfad dieser unterstützenden Dateien lautet.  

            > [!WARNING]  
            >  Sie müssen **cmd /c** am Anfang der Befehlszeile hinzufügen. Wenn Sie **cmd /c** nicht angeben, wird der Befehl nach der Ausführung nicht geschlossen. Die Bereitstellung wartet weiterhin auf den Abschluss des Befehls und startet keine weiteren konfigurierten Befehle oder Aktionen.  

            > [!TIP]  
            >  Während der Erstellung der Tasksequenzmedien werden die Paket-ID und die Prestart-Befehlszeile einschließlich des Wertes vorhandener Tasksequenzvariablen von der Tasksequenz in die Protokolldatei „CreateTSMedia.log“ auf dem Computer geschrieben, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können diese Protokolldatei überprüfen, um den Wert für die Tasksequenzvariablen zu überprüfen.  

        -   Geben Sie unter **Windows PE-Hintergrund** an, ob Sie den WinPE-Standardhintergrund oder einen benutzerdefinierten Hintergrund verwenden möchten.  

        -   Wählen Sie **Befehlsunterstützung aktivieren (nur Test)** aus, um während der Bereitstellung des Startabbilds über die Taste **F8** eine Eingabeaufforderung zu öffnen. Dies kann sich bei der Behandlung von Problemen, die beim Testen der Bereitstellung auftreten, als nützlich erweisen. Es wird davon abgeraten, diese Einstellung in einer Produktionsbereitstellung zu verwenden.  

        -   Konfigurieren Sie den temporären Speicherbereich für Windows PE. Dies ist temporärer Speicher (RAM), der von WinPE verwendet wird. Wenn eine Anwendung z. B. in WinPE ausgeführt wird und temporäre Dateien geschrieben werden müssen, werden die Dateien von WinPE an den temporären Speicherbereich im Arbeitsspeicher umgeleitet, um das Vorhandensein einer Festplatte zu simulieren. Standardmäßig werden von WinPE 32 MB beschreibbarer Arbeitsspeicher zugeordnet.  

    -   Führen Sie auf der Registerkarte **Datenquelle** für die folgenden Einstellungen ein Update aus:  

        -   Legen Sie **Abbildpfad** und **Abbildindex** fest, um die Quelldatei des Startabbilds zu ändern.  

        -   Wählen Sie **Verteilungspunkte entsprechend einem Zeitplan aktualisieren** aus, um einen Zeitplan dafür zu erstellen, wann das Startabbild aktualisiert wird.  

        -   Wählen Sie **Inhalt in Clientcache belassen** aus, wenn Sie nicht wünschen, dass der Inhalt dieses Pakets veraltet und aus dem Clientcache gelöscht wird, um Platz für anderen Inhalt zu schaffen.  

        -   Wählen Sie **Binäre differenzielle Replikation aktivieren** aus, um anzugeben, dass beim Update des Startabbildpakets am Verteilungspunkt nur geänderte Dateien verteilt werden. Durch diese Einstellung wird der Netzwerkdatenverkehr zwischen den Standorten auf ein Minimum reduziert, insbesondere wenn es sich um ein großes Startabbildpaket mit relativ geringen Änderungen handelt.  

        -   Wählen Sie **Dieses Startimage über den PXE-fähigen Verteilungspunkt bereitstellen** aus, wenn das Startimage in einer PXE-fähigen Bereitstellung verwendet wird.  

            > [!NOTE]  
            >  Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   Wählen Sie auf der Registerkarte **Datenzugriff** die folgenden Einstellungen aus:  

        -   Legen Sie **Einstellungen für die Paketfreigabe** fest, wenn der Inhalt dieses Pakets von Clients vom Netzwerk installiert werden soll.  

        -   Geben Sie unter **Einstellungen für die Paketaktualisierung** an, auf welche Weise Benutzer durch Configuration Manager vom Verteilungspunkt getrennt werden sollen. Über Configuration Manager kann möglicherweise kein Update ausgeführt werden, wenn Benutzer mit dem Verteilungspunkt verbunden sind.  

    -   Wählen Sie auf der Registerkarte **Verteilungseinstellungen** die folgenden Einstellungen aus:  

        -   Geben Sie in der Liste **Verteilungspriorität** an, welche Prioritätsstufe von Configuration Manager bei der Verteilung mehrerer Pakete an den gleichen Verteilungspunkt verwendet werden soll.  

        -   Wählen Sie **Den Inhalt für dieses Paket an bevorzugte Verteilungspunkte verteilen** aus, wenn sie eine bedarfsgesteuerte Inhaltsverteilung an bevorzugte Verteilungspunkte aktivieren möchten. Wenn diese Einstellung aktiviert ist und der von einem Client angeforderte Inhalt für das Paket auf keinem der bevorzugten Verteilungspunkte verfügbar ist, wird der Inhalt vom Verwaltungspunkt an alle bevorzugten Verteilungspunkte verteilt.  

        -   Geben Sie unter **Einstellungen für vorab bereitgestellten Verteilungspunkt** an, wie das Startabbild an Verteilungspunkte verteilt werden soll, die für vorab bereitgestellten Inhalt aktiviert sind.  

            > [!NOTE]  
            >  Weitere Informationen zu vorab bereitgestelltem Inhalt finden Sie unter [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   Wählen Sie auf der Registerkarte **Inhaltsorte** den Verteilungspunkt bzw. die Verteilungspunktgruppe aus, und führen Sie die folgenden Aktionen aus:  

        -   Klicken Sie auf **Neu verteilen** , um das Startabbild erneut an den ausgewählten Verteilungspunkt oder an die ausgewählte Verteilungspunktgruppe zu verteilen.  

        -   Klicken Sie auf **Überprüfen** , um die Integrität des Startabbildpakets am ausgewählten Verteilungspunkt bzw. in der ausgewählten Verteilungspunktgruppe zu überprüfen.  

    -   Geben Sie auf der Registerkarte **Optionale Komponenten** die Komponenten an, die Windows PE zur Verwendung mit Configuration Manager hinzugefügt werden. Weitere Informationen zu verfügbaren optionalen Komponenten finden Sie unter [WinPE: Hinzufügen von Paketen (Referenz zu optionalen Komponenten)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx).  

    -   Wählen Sie auf der Registerkarte **Sicherheit** einen Administrator aus, und ändern Sie die Vorgänge, die dieser Administrator ausführen kann.  

6.  Nachdem Sie die Eigenschaften konfiguriert haben, klicken Sie auf **OK**.  

##  <a name="BKMK_BootImagePXE"></a> Konfigurieren eines Startimages, das über einen PXE-fähigen Verteilungspunkt bereitgestellt werden soll  
 Bevor Sie ein Startimage für eine PXE-Betriebssystembereitstellung verwenden können, müssen Sie das Startimage für die Bereitstellung über einen PXE-fähigen Verteilungspunkt konfigurieren.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>So konfigurieren Sie ein Startimage, das über einen PXE-fähigen Verteilungspunkt bereitgestellt werden soll  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

3.  Wählen Sie das Startabbild aus, das Sie ändern möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften** , um das Dialogfeld **Eigenschaften** für das Startabbild zu öffnen.  

5.  Wählen Sie auf der Registerkarte **Datenquelle** die Option **Dieses Startimage über den PXE-fähigen Verteilungspunkt bereitstellen**aus.  

    > [!NOTE]  
    >  Weitere Informationen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  Nachdem Sie die Eigenschaften konfiguriert haben, klicken Sie auf **OK**.  

##  <a name="BKMK_BootImageLanguage"></a> Konfigurieren von mehreren Sprachen für die Startimagebereitstellung  
 Startabbilder sind sprachneutral. Daher können Sie unter WinPE ein Startabbild verwenden, für das die Tasksequenz in mehreren Sprachen angezeigt wird. Binden Sie dafür die entsprechende Sprachunterstützung aus den optionalen Komponenten von Windows PE ein, und legen Sie die erforderliche Tasksequenzvariable fest, um anzugeben, welche Sprache angezeigt werden kann. Die Sprache des bereitgestellten Betriebssystems ist unabhängig von der Sprache, die unter WinPE angezeigt wird. Dies gilt unabhängig von der Configuration Manager-Version. Die Sprache, die dem Benutzer angezeigt wird, wird wie folgt bestimmt:  

-   Wenn ein Benutzer die Tasksequenz unter einem vorhandenen Betriebssystem ausführt, wird von Configuration Manager automatisch die für den Benutzer konfigurierte Sprache verwendet. Wird die Tasksequenz automatisch als Folge eines obligatorischen Bereitstellungsstichtags ausgeführt, wird von Configuration Manager die Sprache des Betriebssystems verwendet.  

-   Für Betriebssystembereitstellungen, für die PXE oder Medien verwendet werden, können Sie den Wert für die Sprach-ID in der Variablen SMSTSLanguageFolder als Teil eines Prestart-Befehls festlegen. Wenn der Computer mit WinPE gestartet wird, werden Meldungen in der Sprache angezeigt, die Sie in der Variablen angegeben haben. Falls beim Zugreifen auf die Sprachressourcendatei im angegebenen Ordner ein Fehler auftritt oder falls Sie die Variable nicht festlegen, werden Meldungen in der WinPE-Sprache angezeigt.  

    > [!NOTE]  
    >  Wenn das Medium mit einem Kennwort geschützt ist, wird der Text, mit dem Benutzer zur Eingabe des Kennworts aufgefordert werden, immer in der WindPE-Sprache angezeigt.  

 Verwenden Sie das folgende Verfahren zum Festlegen der WinPE-Sprache für Betriebssystembereitstellungen, die per PXE oder Startmedium initiiert werden.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>So legen Sie die Windows PE-Sprache für Betriebssystembereitstellungen fest, die per PXE oder Startmedium initiiert werden  

1.  Vergewissern Sie sich vor dem Aktualisieren des Startabbilds, dass sich die richtige Tasksequenz-Ressourcendatei (tsres.dll) im entsprechenden Sprachordner auf dem Standortserver befindet. Die Ressourcendatei für Englisch befindet sich z.B. am folgenden Speicherort: <*ConfigMgr-Installationsordner*>\OSD\bin\x64\00000409\tsres.dll.  

2.  Legen Sie als Teil des Prestart-Befehls die Umgebungsvariable SMSTSLanguageFolder auf die gewünschte Sprach-ID fest. Die Sprach-ID muss im Dezimalformat angegeben werden (nicht hexadezimal). Wenn Sie die Sprach-ID auf Englisch festlegen möchten, geben Sie z. B. den Dezimalwert 1033 an, und nicht den Hexadezimalwert 00000409, der für den Ordnernamen verwendet wird.  
