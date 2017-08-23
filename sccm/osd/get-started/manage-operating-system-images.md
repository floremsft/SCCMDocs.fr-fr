---
title: Verwalten von Betriebssystemimages | Microsoft Docs
description: "Erfahren Sie in Configuration Manager mehr über Methoden, mit denen Sie Betriebssystemimages verwalten können, die in WIM-Dateien (Windows Imaging) gespeichert sind."
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
caps.latest.revision: "17"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6953c3834ca303b949f22436010a87b3da9688dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-operating-system-images-with-system-center-configuration-manager"></a>Verwalten von Betriebssystemimages mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Betriebssystemabbilder in Configuration Manager werden im WIM-Dateiformat (Windows Imaging) gespeichert. Sie stellen eine komprimierte Sammlung von Verweisdateien und -ordnern dar, die für die erfolgreiche Installation und Konfiguration eines Betriebssystems auf einem Computer erforderlich sind. Bei allen Szenarien für die Betriebssystembereitstellung müssen Sie ein Betriebssystemabbild auswählen.   Sie können das Standardabbild des Betriebssystems verwenden oder das Betriebssystemabbild von einem von Ihnen konfigurierten Referenzcomputer erstellen. Beim Erstellen des Referenzcomputers können Sie Betriebssystemdateien, Treiber, Unterstützungsdateien, Softwareupdates, Tools und andere Softwareanwendungen zum Betriebssystem hinzufügen, bevor es zum Erzeugen der Abbilddatei erfasst wird. Im Folgenden finden Sie Informationen zu den einzelnen Methoden.  

 **Standardimage**  

 Das Standardimage des Betriebssystems (install.wim) ist in den Installationsdateien des Windows-Betriebssystems enthalten. Dieses Abbild ist ein grundlegendes Betriebssystemabbild, das einen Standardsatz von Treibern enthält. Wenn Sie das Standardabbild des Betriebssystems verwenden, können Sie nach der Installation des Betriebssystems mithilfe von Tasksequenzschritten Apps installieren und andere Konfigurationen vornehmen.  Das Standardimage des Betriebssystems befindet sich in „<*Quellpfad des Betriebssystems*>\Sources\install.wim“.  

-   **Vorteile**  

    -   Das Image ist kleiner als ein erfasstes Image.  

    -   Das Installieren von Apps und Konfigurationen mithilfe von Tasksequenzschritten ist dynamischer. Sie können beispielsweise die zu installierenden Apps und die Konfigurationen in der Tasksequenz ändern und müssen kein neues Abbild des Betriebssystems erstellen.  

-   **Nachteile**  

    -   Die Installation des Betriebssystems kann länger dauern, da die App-Installation und andere Konfigurationen nach Abschluss der Betriebssysteminstallation erfolgen.  

 **Erfasstes Image**  

 Zum Erzeugen eines benutzerdefinierten Betriebssystemabbilds erstellen Sie einen Referenzcomputer mit dem gewünschten Betriebssystem, installieren Apps, konfigurieren Einstellungen usw. Dann erfassen Sie das Betriebssystemabbild auf dem Referenzcomputer, um die WIM-Datei zu erstellen. Sie können den Referenzcomputer manuell erstellen oder eine Tasksequenz zum Automatisieren einiger oder aller Erstellungsschritte verwenden.   
Die Schritte zum Erstellen eines benutzerdefinierten Betriebssystemimages finden Sie unter [Anpassen von Betriebssystemimages mit System Center Configuration Manager](customize-operating-system-images.md).  

-   **Vorteile**  

    -   Die Installation kann schneller als bei Verwendung des Standardbilds sein. Beispielsweise können Apps mit dem erfassten Betriebssystemabbild vorinstalliert werden, und Sie müssen später keine Apps mithilfe von Tasksequenzschritten installieren.  

-   **Nachteile**  

    -   Die Installation des Betriebssystems kann länger dauern, da die App-Installation und andere Konfigurationen nach Abschluss der Betriebssysteminstallation erfolgen.  


##  <a name="BKMK_AddOSImages"></a> Hinzufügen von Betriebssystemimages zu Configuration Manager  
 Bevor Sie ein Betriebssystemimage verwenden können, müssen Sie das Image zu einem Configuration Manager-Standort hinzufügen. Gehen Sie wie folgt vor, um ein Betriebssystemabbild zu einem Standort hinzuzufügen.  

#### <a name="to-add-an-operating-system-image-to-a-site"></a>So fügen Sie ein Betriebssystemabbild zu einem Standort hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Betriebssystemabbilder**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Betriebssystemabbild hinzufügen** , um den Assistenten zum Hinzufügen von Betriebssystemabbildern zu starten.  

4.  Geben Sie auf der Seite **Datenquelle** den Netzwerkpfad zum Betriebssystemabbild an. Geben Sie z. B.**\\\<Server>\<Pfad>\OS.WIM** ein.  

5.  Geben Sie auf der Seite **Allgemein** die folgenden Informationen an, und klicken Sie dann auf **Weiter**. Diese Informationen sind für Identifikationszwecke nützlich, wenn Sie dem gleichen Standort mehrere Betriebssystemabbilder hinzufügen möchten.  

    -   **Name**: Geben Sie den Namen des Abbilds an. Standardmäßig wird der Name des Abbilds aus der WIM-Datei übernommen.  

    -   **Version**: Geben Sie die Version des Abbilds an.  

    -   **Comment**: Geben Sie eine kurze Beschreibung des Abbilds an.  

6.  Schließen Sie den Assistenten ab.  

 Sie können nun das Betriebssystemabbild an Verteilungspunkte verteilen.  

##  <a name="BKMK_DistributeBootImages"></a> Verteilen von Betriebssystemimages an Verteilungspunkte  
 Betriebssystemabbilder werden genau wie anderer Inhalt an Verteilungspunkte verteilt. In den meisten Fällen müssen Sie das Betriebssystemabbild an mindestens einen Verteilungspunkt verteilen, bevor Sie das Betriebssystem bereitstellen. Die Schritte zum Verteilen von Betriebssystemabbildern finden Sie unter [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="BKMK_OSImagesApplyUpdates"></a>Anwenden von Softwareupdates auf ein Betriebssystemimage  
 Es werden regelmäßig neue Softwareupdates veröffentlicht, die für das Betriebssystem in Ihrem Betriebssystemabbild gelten. Vor dem Anwenden von Softwareupdates auf ein Image müssen die Softwareupdateinfrastruktur vorhanden, Softwareupdates erfolgreich synchronisiert und die Softwareupdates aus der Inhaltsbibliothek auf den Standortserver heruntergeladen worden sein. Weitere Informationen finden Sie unter [Bereitstellen von Softwareupdates](../../sum/deploy-use/deploy-software-updates.md).  

 Sie können relevante Softwareupdates nach einem festgelegten Zeitplan auf ein Abbild anwenden. Basierend auf dem von Ihnen festgelegten Zeitplan wendet Configuration Manager die ausgewählten Softwareupdates auf das Betriebssystemimage an und verteilt das aktualisierte Image dann optional an Verteilungspunkte. Die Informationen zum Betriebssystemabbild werden in der Standortdatenbank gespeichert. Dazu gehören beispielsweise die Softwareupdates, die während des Imports angewendet wurden. Softwareupdates, die nach dem ursprünglichen Hinzufügen auf das Abbild angewendet wurden, werden ebenfalls in der Standortdatenbank gespeichert. Wenn Sie den Assistenten starten, um Softwareupdates auf das Betriebssystemabbild anzuwenden, ruft der Assistent eine Liste mit den verfügbaren Softwareupdates ab, die noch nicht auf das Abbild angewendet wurden und ausgewählt werden können. Configuration Manager kopiert die Softwareupdates aus der Inhaltsbibliothek auf dem Standortserver und wendet die Softwareupdates auf das Betriebssystemimage an.  

 Verwenden Sie das folgende Verfahren, um Softwareupdates auf ein Betriebssystemabbild anzuwenden.  

#### <a name="to-apply-software-updates-to-an-operating-system-image"></a>So wenden Sie Softwareupdates auf ein Betriebssystemabbild an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Betriebssystemabbilder**.  

3.  Wählen Sie das Betriebssystemabbild aus, auf das Softwareupdates angewendet werden sollen.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Betriebssystemabbild** auf **Updates planen** , um den Assistenten zu starten.  

5.  Wählen Sie auf der Seite **Updates auswählen** die Softwareupdates aus, die auf das Betriebssystemabbild angewendet werden sollen, und klicken Sie dann auf **Weiter**.  

6.  Geben Sie auf der Seite **Zeitplan festlegen** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    1.  **Zeitplan**: Geben Sie den Zeitplan dafür an, wann die Softwareupdates auf das Betriebssystemabbild angewendet werden sollen.  

    2.  **Bei Fehler fortsetzen**: Aktivieren Sie diese Option, um anzugeben, dass Softwareupdates auch beim Auftreten eines Fehlers auf das Abbild angewendet werden sollen.  

    3.  **Abbild an Verteilungspunkte verteilen**: Wählen Sie diese Option aus, um das Betriebssystemabbild auf Verteilungspunkten zu aktualisieren, nachdem die Softwareupdates angewendet wurden.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** die Informationen, und klicken Sie dann auf **Weiter**.  

8.  Überprüfen Sie auf der Seite **Abschluss des Vorgangs** , ob die Softwareupdates erfolgreich auf das Betriebssystemabbild angewendet wurden.  

##  <a name="BKMK_OSImageMulticast"></a> Vorbereiten des Betriebssystemimages für Multicastbereitstellungen  
 Bei Verwendung von Multicastbereitstellungen können mehrere Computer gleichzeitig ein Betriebssystemabbild herunterladen. Das Abbild wird vom Verteilungspunkt per Multicast an Clients übertragen, anstatt dass der Verteilungspunkt eine Kopie des Abbilds über eine separate Verbindung an jeden Client sendet. Wenn Sie die Methode [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md) für die Betriebssystembereitstellung verwenden, müssen Sie das Imagepaket des Betriebssystems für die Multicastunterstützung konfigurieren, bevor Sie das Betriebssystemimage an einen multicastfähigen Verteilungspunkt verteilen. Gehen Sie wie folgt vor, um die Multicastoptionen für ein vorhandenes Abbildpaket des Betriebssystems festzulegen.  

#### <a name="to-modify-an-operating-system-image-package-to-use-multicast"></a>So ändern Sie das Abbildpaket des Betriebssystems für die Verwendung von Multicast  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Betriebssystemabbilder**.  

3.  Wählen Sie das Betriebssystemabbild aus, das Sie an den multicastfähigen Verteilungspunkt verteilen möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Wählen Sie die Registerkarte **Verteilungseinstellungen** aus, und konfigurieren Sie die folgenden Optionen:  

    -   **Dieses Paket darf per Multicast (nur WinPE) übertragen werden**: Sie müssen diese Option für Configuration Manager auswählen, damit Betriebssystemimages gleichzeitig bereitgestellt werden können.  

    -   **Multicastpakete verschlüsseln**: Geben Sie an, ob das Abbild vor der Übertragung an den Verteilungspunkt verschlüsselt werden soll. Verwenden Sie diese Option, wenn das Paket vertrauliche Informationen enthält. Wenn das Abbild nicht verschlüsselt wird, ist der Paketinhalt als Klartext im Netzwerk sichtbar und wird möglicherweise von unbefugten Benutzern gelesen.  

    -   **Dieses Paket nur per Multicast übertragen**: Geben Sie an, ob das Abbild vom Verteilungspunkt nur während einer Multicastsitzung bereitgestellt werden soll.  

         Bei Auswahl dieser Option **** müssen Sie auch **Inhalt lokal herunterladen, wenn dies für die Ausführung der Tasksequenz erforderlich ist** als Bereitstellungsoption für das Betriebssystemabbild angeben. Sie können die Bereitstellungsoptionen für das Abbild während der Bereitstellung des Betriebssystemabbilds oder zu einem späteren Zeitpunkt durch Bearbeitung der Bereitstellungseigenschaften angeben. Die Bereitstellungsoptionen finden Sie auf der Seite **Eigenschaften** des Bereitstellungsobjekts auf der Registerkarte **Verteilungspunkte** .  

6.  Klicken Sie auf **OK**.  
