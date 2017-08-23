---
title: Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems | Microsoft-Dokumentation
description: Eine Tasksequenz zum Erstellen und Erfassen erstellt einen Referenzcomputer, der spezifische Treiber und Softwareupdates zusammen mit dem Betriebssystem enthalten kann.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: e9320e40b8e5031ffa3da5e5149c7da718cc87d5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-capture-an-operating-system-in-system-center-configuration-manager"></a>Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn Sie zum Bereitstellen eines Betriebssystems auf einem Computer in System Center Configuration Manager eine Tasksequenz verwenden, installiert der Computer das Betriebssystemimage, das Sie in der Tasksequenz angeben. Um das Betriebssystemimage anzupassen, damit es bestimmte Treiber, Anwendungen, Softwareupdates usw. einbezieht, verwenden Sie eine Tasksequenz zum Erstellen und Erfassen, um einen Referenzcomputer zu erstellen und dann das Betriebssystemimage von diesem Referenzcomputer zu erfassen. Wenn Sie bereits über einen Referenzcomputer für die Erfassung verfügen, können Sie eine benutzerdefinierte Tasksequenz erstellen, um das Betriebssystem zu erfassen. Verwenden Sie die folgenden Abschnitte, um ein benutzerdefiniertes Betriebssystem zu erfassen.  

##  <a name="BKMK_BuildCaptureTS"></a> Verwenden einer Tasksequenz zum Erstellen und Erfassen eines Referenzcomputers  
 Die Tasksequenz für die Erstellung und Erfassung partitioniert und formatiert den Referenzcomputer, installiert das Betriebssystem sowie den Configuration Manager-Client, Anwendungen und Softwareupdates. Anschließend erfasst er das Betriebssystem vom Referenzcomputer. Die Pakete, die der Tasksequenz zugeordnet sind, z. B. Anwendungen, müssen auf Verteilungspunkten verfügbar sein, bevor Sie die Tasksequenz für die Erstellung und Erfassung erstellen.  

###  <a name="BKMK_CreatePackages"></a> Vorbereiten auf Betriebssystembereitstellungen  
 Es gibt eine Vielzahl von Szenarien zum Bereitstellen eines Betriebssystems auf Computern in Ihrer Umgebung. In den meisten Fällen erstellen Sie eine Tasksequenz und wählen **Bestehendes Abbildpaket installieren** im Tasksequenzerstellungs-Assistenten aus, um das Betriebssystem zu installieren, die Benutzereinstellungen zu migrieren, Softwareupdates anzuwenden und Anwendungen zu installieren. Bevor Sie eine Tasksequenz zum Installieren eines Betriebssystems erstellen, muss Folgendes vorhanden sein:  

-   **Erforderlich**  

    -   Das [Startimage](../get-started/manage-boot-images.md) muss in der Configuration Manager-Konsole verfügbar sein.  

    -   Ein [Betriebssystemimage](../get-started/manage-operating-system-images.md) muss in der Configuration Manager-Konsole verfügbar sein.  

-   **Erforderlich (sofern verwendet)**  

    -   [Treiberpakete](../get-started/manage-drivers.md), die die erforderlichen Windows-Treiber zur Unterstützung von Hardware auf dem Referenzcomputer enthalten, müssen in der Configuration Manager-Konsole verfügbar sein. Weitere Informationen zu Tasksequenzschritten zum Verwalten von Treibern finden Sie unter [Verwenden von Tasksequenzen zum Installieren von Gerätetreibern](../get-started/manage-drivers.md#BKMK_TSDrivers).  

    -   [Softwareupdates](../../sum/get-started/synchronize-software-updates.md) müssen in der Configuration Manager-Konsole synchronisiert werden.  

    -   [Anwendungen](../../apps/deploy-use/create-applications.md) müssen zur Configuration Manager-Konsole hinzugefügt werden.  

###  <a name="BKMK_CreateBuildCaptureTS"></a> Erstellen einer Tasksequenz zum Erstellen und Erfassen  
 Gehen Sie wie folgt vor, um eine Tasksequenz zum Erstellen eines Referenzcomputers und zum Erfassen eines Betriebssystems zu verwenden.  

#### <a name="to-create-a-task-sequence-that-builds-and-captures-an-operating-system-image"></a>So erstellen Sie eine Tasksequenz zum Erstellen und Erfassen eines Betriebssystemabbilds  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Referenz-Betriebssystemabbild erstellen und erfassen**aus.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Tasksequenzname**: Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der Aufgabe an, die von der Tasksequenz erfüllt wird, beispielsweise eine Beschreibung des Betriebssystems, das von der Tasksequenz erstellt wird.  

    -   **Startabbild**: Geben Sie das Startabbild an, von dem das Betriebssystemabbild installiert wird.  

        > [!IMPORTANT]  
        >  Die Architektur des Startabbilds muss kompatibel mit der Hardwarearchitektur des Zielcomputers sein.  

6.  Geben Sie auf der Seite **Windows installieren** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Abbildpaket**: Geben Sie das Paket mit dem Betriebssystemabbild an, das die Dateien enthält, die zum Installieren des Betriebssystems erforderlich sind.  

    -   **Abbildindex**: Geben Sie das zu installierende Betriebssystem an. Wenn das Betriebssystemabbild mehrere Versionen enthält, wählen Sie die Version aus, die Sie installieren möchten.  

    -   **Product key**: Geben Sie den Product Key für das zu installierende Windows-Betriebssystem an. Sie können codierte Volumenlizenzschlüssel und standardmäßige Product Keys angeben. Wenn Sie einen nicht codierten Product Key verwenden, muss jede Gruppe aus 5 Zeichen mit einen Bindestrich (-) getrennt werden. Beispiel: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Serverlizenzierungsmodus**: Geben Sie an, ob die Serverlizenz **Pro Arbeitsplatz**oder **Pro Server**bzw. dass keine Lizenz angegeben ist. Wenn die Serverlizenz **Pro Server**gilt, geben Sie auch die maximale Anzahl von Serververbindungen an.  

    -   Geben Sie an, wie das Administratorkonto verarbeitet werden soll, das bei der Bereitstellung des Betriebssystems verwendet wird.  

        -   **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren**: Geben Sie an, ob Configuration Manager ein zufälliges Kennwort für das lokale Administratorkonto erstellen und das Konto deaktivieren soll, wenn das Betriebssystem bereitgestellt wurde.  

        -   **Konto aktivieren und lokales Administratorkennwort angeben**: Geben Sie an, ob während der Bereitstellung des Betriebssystems auf allen Computern das gleiche Kennwort für das lokale Administratorkonto verwendet werden soll.  

7.  Geben Sie auf der Seite **Netzwerkeinstellungen konfigurieren** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Einer Arbeitsgruppe beitreten**: Geben Sie an, ob der Zielcomputer einer Arbeitsgruppe hinzugefügt werden soll, wenn das Betriebssystem bereitgestellt wird.  

    -   **Einer Domäne beitreten**: Geben Sie an, ob der Zielcomputer einer Domäne hinzugefügt werden soll, wenn das Betriebssystem bereitgestellt wird. Geben Sie unter **Domäne**den Namen der Domäne an.  

        > [!IMPORTANT]  
        >  Domänen in der lokalen Gesamtstruktur können Sie suchen, doch bei Domänen in remoten Gesamtstrukturen müssen Sie den Domänennamen angeben.  

         Sie können auch eine Organisationseinheit angeben. Dies ist eine optionale Einstellung, mit welcher der LDAP X.500-definierte Name der Organisationseinheit angegeben wird, in der das Computerkonto erstellt werden soll, sofern das Konto noch nicht vorhanden ist.  

    -   **Konto**: Geben Sie Benutzernamen und Kennwort für das Konto an, das die Berechtigungen hat, um der angegebenen Domäne beizutreten. Beispiel: *Domäne\Benutzer* oder *%Variable%*.  

        > [!IMPORTANT]  
        >  Sie müssen die richtigen Domänenanmeldeinformationen eingeben, wenn Sie entweder die Domäneneinstellungen oder die Arbeitsgruppeneinstellungen migrieren möchten.  

8.  Geben Sie auf der Seite **Configuration Manager installieren** das Configuration Manager-Clientpaket an, das die Quelldateien zum Installieren des Configuration Manager-Clients enthält, sowie alle zusätzlichen Eigenschaften, die für die Installation erforderlich sind. Klicken Sie anschließend auf **Weiter**.  

     Weitere Informationen zu den Eigenschaften, die zur Installation eines Clients verwendet werden können, finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../core/clients/deploy/about-client-installation-properties.md).  

9. Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche Softwareupdates, alle Softwareupdates oder keine Softwareupdates installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur Softwareupdates installiert, die für Sammlungen bestimmt sind, in denen der Zielcomputer Mitglied ist.  

10. Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

11. Geben Sie auf der Seite **Systemvorbereitung** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Paket**: Geben Sie das Configuration Manager-Paket an, das die entsprechende Version von Sysprep zum Erfassen der Einstellungen des Referenzcomputers enthält.  

         Wenn Sie Windows Vista oder eine höhere Version als Betriebssystemversion verwenden, wird Sysprep automatisch auf dem Computer installiert, und es muss kein Paket angegeben werden.  

12. Geben Sie auf der Seite **Abbildeigenschaften** die folgenden Einstellungen für das Betriebssystemabbild an, und klicken Sie dann auf **Weiter**.  

    -   **Erstellt von**: Geben Sie den Namen des Benutzers an, der das Betriebssystemabbild erstellt hat.  

    -   **Version**: Geben Sie eine benutzerdefinierte Versionsnummer an, die dem Betriebssystemabbild zugeordnet ist.  

    -   **Beschreibung**: Geben Sie eine benutzerdefinierte Beschreibung des Betriebssystemabbilds an.  

13. Geben Sie auf der Seite **Abbild erfassen** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Pfad**: Geben Sie einen freigegebenen Netzwerkordner an, in dem die WIM-Ausgabedatei gespeichert ist. Diese Datei enthält das Betriebssystemabbild auf Basis der Einstellungen, die Sie mithilfe dieses Assistenten festlegen. Wenn Sie einen Ordner angeben, der eine vorhandene WIM-Datei enthält, wird die vorhandene Datei überschrieben.  

    -   **Konto**: Geben Sie ein Windows-Konto mit Berechtigungen für die Netzwerkfreigabe an, in der das Abbild gespeichert wird.  

14. Schließen Sie den Assistenten ab.  

15. Wenn Sie der Tasksequenz weitere Schritte hinzufügen möchten, wählen Sie die von Ihnen erstellte Tasksequenz aus, und klicken Sie dann auf **Bearbeiten**. Weitere Informationen zum Bearbeiten einer Tasksequenz finden Sie unter [Bearbeiten einer Tasksequenz](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Verwenden Sie eine der folgenden Methoden, um die Tasksequenz auf einem Referenzcomputer bereitzustellen:  

-   Wenn es sich beim Referenzcomputer um einen Configuration Manager-Client handelt, können Sie die Tasksequenz zum Erstellen und Erfassen für die Sammlung bereitstellen, die den Referenzcomputer enthält. Weitere Informationen zum Bereitstellen des Betriebssystemimages finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md).  

    > [!NOTE]  
    >  Wenn die Tasksequenz einen Schritt zur Laufwerkpartitionierung umfasst, wählen Sie bei der Bereitstellung der Tasksequenz nicht die Option **Programm herunterladen** aus.  

-   Wenn es sich beim Referenzcomputer nicht um einen Configuration Manager-Client handelt oder Sie die Tasksequenz auf dem Referenzcomputer manuell ausführen möchten, führen Sie den **Assistenten zum Erstellen von Tasksequenzmedien** aus, um startbare Medien zu erstellen. Informationen zum Erstellen von startbaren Medien finden Sie unter [Erstellen startbarer Medien](create-bootable-media.md).  

##  <a name="BKMK_CaptureExistingRefComputer"></a> Erfassen eines Betriebssystemabbilds von einem vorhandenen Referenzcomputer  
 Wenn Sie bereits über einen Referenzcomputer für die Erfassung verfügen, können Sie eine Tasksequenz erstellen, die das Betriebssystem vom Referenzcomputer erfasst. Sie verwenden den Tasksequenzschritt **Betriebssystemabbild erfassen** , um mindestens ein Abbild von einem Referenzcomputer zu erfassen und in einer Abbilddatei (WIM) auf der angegebenen Netzwerkfreigabe zu speichern. Der Referenzcomputer wird mithilfe eines Startabbilds in Windows PE gestartet. Jede Festplatte des Referenzcomputers wird in der WIM-Datei als separates Abbild erfasst. Wenn der Referenzcomputer über mehrere Laufwerke verfügt, enthält die erstellte WIM-Datei für jedes Volume ein separates Abbild. Es werden nur als NTFS oder FAT32 formatierte Volumes erfasst. Volumes in anderen Formaten sowie USB-Volumes werden nicht berücksichtigt.  

 Mit dem folgenden Verfahren können Sie ein Betriebssystemabbild von einem vorhandenen Referenzcomputer erfassen.  

#### <a name="to-capture-an-operating-system-from-an-existing-reference-computer"></a>So erfassen Sie ein Betriebssystemabbild von einem vorhandenen Referenzcomputer  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Neue benutzerdefinierte Tasksequenz erstellen**aus.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** einen Namen für die Tasksequenz und eine Beschreibung der Tasksequenz an.  

6.  Geben Sie ein Startabbild für die Tasksequenz an. Dieses Startabbild wird zum Starten des Referenzcomputers mit Windows PE verwendet.  Weitere Informationen finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

7.  Schließen Sie den Assistenten ab.  

8.  Wählen Sie in **Tasksequenzen**die benutzerdefinierte Tasksequenz aus, und klicken Sie dann auf der Registerkarte **Start** der Gruppe **Tasksequenz** auf **Bearbeiten** , um den Tasksequenz-Editor zu öffnen.  

9. Verwenden Sie diesen Schritt nur, wenn der Configuration Manager-Client auf dem Referenzcomputer installiert ist.  

     Klicken Sie nacheinander auf **Hinzufügen**, **Images**, und [ConfigMgr-Client für Erfassung vorbereiten](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). In diesem Tasksequenzschritt wird der Configuration Manager-Client auf dem Referenzcomputer ausgewählt und im Rahmen des Imageerstellungsprozesses für die Erfassung vorbereitet.  

10. Klicken Sie nacheinander auf **Hinzufügen**, **Images**, und [Windows für die Erfassung vorbereiten](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Mit dieser Tasksequenzaktion wird Sysprep ausgeführt. Der Computer wird anschließend über das für die Tasksequenz angegebene Windows PE-Startabbild neu gestartet. Damit diese Aktion erfolgreich abgeschlossen werden kann, darf der Referenzcomputer keiner Domäne angehören.  

11. Klicken Sie nacheinander auf **Hinzufügen**, **Images**, und [Erfassung des Betriebssystemimages](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  Dieser Tasksequenzschritt wird nur von Windows PE ausgeführt, um die Festplatten auf dem Referenzcomputer zu erfassen. Konfigurieren Sie die folgenden Einstellungen für den Tasksequenzschritt.  

    -   **Name** und **Beschreibung**: Sie können den Namen des Tasksequenzschritts optional ändern und eine Beschreibung bereitstellen.  

    -   **Ziel**: Geben Sie einen freigegebenen Netzwerkordner an, in dem die WIM-Ausgabedatei gespeichert ist. Diese Datei enthält das Betriebssystemabbild auf Basis der Einstellungen, die Sie mithilfe dieses Assistenten festlegen. Wenn Sie einen Ordner angeben, der eine vorhandene WIM-Datei enthält, wird die vorhandene Datei überschrieben.  

    -   **Beschreibung**, **Version**und **Erstellt von**: Stellen Sie optional Informationen zum zu erfassenden Abbild bereit.  

    -   **Konto für die Erfassung des Betriebssystemabbilds**: Geben Sie das Windows-Konto an, das über die Berechtigungen für die angegebene Netzwerkfreigabe verfügt. Klicken Sie auf **Festlegen** , um den Namen dieses Windows-Kontos anzugeben.  

     Klicken Sie auf **OK** , um den Tasksequenz-Editor zu schließen.  

 Verwenden Sie eine der folgenden Methoden, um die Tasksequenz auf einem Referenzcomputer bereitzustellen:  

-   Wenn es sich beim Referenzcomputer um einen Configuration Manager-Client handelt, können Sie die Tasksequenz für die Sammlung bereitstellen, die den Referenzcomputer enthält. Weitere Informationen zum Bereitstellen des Betriebssystemimages finden Sie unter [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md).  

-   Wenn es sich beim Referenzcomputer nicht um einen Configuration Manager-Client handelt oder Sie die Tasksequenz auf dem Referenzcomputer manuell ausführen möchten, führen Sie den **Assistenten zum Erstellen von Tasksequenzmedien** aus, um startbare Medien zu erstellen. Informationen zum Erstellen von startbaren Medien finden Sie unter [Erstellen startbarer Medien](create-bootable-media.md).  

##  <a name="BKMK_BuildandCaptureTSExample"></a> Tasksequenzbeispiel zum Erstellen und Erfassen eines Betriebssystemabbilds  
 Orientieren Sie sich an der folgenden Tabelle, während Sie eine Tasksequenz zum Erstellen und Erfassen eines Betriebssystemabbilds erstellen. Mithilfe dieser Tabelle können Sie die allgemeine Sequenz für Ihre Tasksequenzschritte festlegen und diese Tasksequenzschritte in logischen Gruppen organisieren. Die von Ihnen erstellte Tasksequenz kann von diesem Beispiel abweichen und eine andere Anzahl von Tasksequenzschritten und Tasksequenzgruppen enthalten.  

> [!IMPORTANT]  
>  Erstellen Sie diese Art von Tasksequenz stets mithilfe des Tasksequenzerstellungs-Assistenten.  

 Wenn Sie diese neue Tasksequenz über die Option **Neue Tasksequenz** erstellen, haben einige Tasksequenzschritte andere Namen, als wenn Sie diese Tasksequenzschritte manuell zu einer vorhandenen Tasksequenz hinzufügen. In der folgenden Tabelle sind die Namensunterschiede angezeigt:  

|Neuer Name des Tasksequenzschritts im Tasksequenzerstellungs-Assistenten|Name des entsprechenden Schritts im Tasksequenz-Editor|  
|------------------------------------------------------|-----------------------------------------------|  
|Neustart mit Windows PE|Neustart mit Windows PE oder Festplatte ausführen|  
|Festplatte 0 partitionieren|Datenträger formatieren und partitionieren|  
|Gerätetreiber anwenden|Treiber automatisch anwenden|  
|Updates installieren|Softwareupdates installieren|  
|Arbeitsgruppe beitreten|Einer Domäne oder Arbeitsgruppe beitreten|  
|ConfigMgr-Client vorbereiten|Prepare ConfigMgr Client for Capture|  
|Betriebssystem vorbereiten|Prepare Windows for Capture|  
|Referenzcomputer erfassen|Betriebssystemabbild erfassen|  

|Tasksequenzgruppe/-schritt|Reference|  
|-------------------------------|---------------|  
|Referenzcomputer erstellen – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine Tasksequenzgruppe. Mithilfe einer Tasksequenzgruppe können Sie ähnliche Tasksequenzschritte zur besseren Organisation und Fehlersteuerung gruppieren.<br /><br /> Diese Gruppe enthält die für das Erstellen eines Referenzcomputers erforderlichen Aktionen.|  
|Neustart mit Windows PE|Mithilfe dieses Tasksequenzschritts können Sie die Neustartoptionen für den Zielcomputer angeben. In diesem Schritt wird eine Meldung angezeigt, dass der Computer neu gestartet wird, um die Installation fortzusetzen.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSInWinPE** verwendet. Wenn der zugeordnete Wert **false** ist, wird der Tasksequenzschritt fortgesetzt.|  
|Festplatte 0 partitionieren|Mithilfe dieses Tasksequenzschritts können Sie die zum Formatieren der Festplatte auf dem Zielcomputer erforderlichen Aktionen angeben. Die standardmäßige Datenträgernummer ist **0**.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSClientCache** verwendet. Der Schritt wird ausgeführt, wenn kein Configuration Manager-Clientcache vorhanden ist.|  
|Betriebssystem anwenden|Mithilfe dieses Tasksequenzschritts können Sie ein angegebenes Betriebssystemabbild auf dem Zielcomputer installieren. In diesem Schritt werden alle in der WIM-Datei enthaltenen Volumeimages auf das entsprechende sequenzielle Datenträgervolume auf dem Bereitstellungszielcomputer angewendet, nachdem zuerst alle Dateien auf diesem Volume gelöscht wurden (mit Ausnahme Configuration Manager-spezifischer Steuerdateien).|  
|Windows-Einstellungen anwenden|Mithilfe dieses Tasksequenzschritts können Sie die Konfigurationsinformationen für die Windows-Einstellungen des Zielcomputers angeben.|  
|Netzwerkeinstellungen anwenden|Mithilfe dieses Tasksequenzschritts können Sie die Konfigurationsinformationen für das Netzwerk oder die Arbeitsgruppe des Zielcomputers angeben.|  
|Gerätetreiber anwenden|Mithilfe dieses Tasksequenzschritts können Sie geeigneten Gerätetreiber als Teil der Betriebssystembereitstellung auswählen und installieren. Sie können durch Auswahl von **Treiber aller Kategorien berücksichtigen** zulassen, dass alle vorhandenen Treiberkategorien von Windows Setup durchsucht werden, oder die von Windows Setup zu durchsuchenden Treiberkategorien durch Auswahl von **Nur Treiber in bestimmten Kategorien berücksichtigen**einschränken.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSMediaType** verwendet. Dieser Tasksequenzschritt wird ausgeführt, wenn der zugeordnete Wert nicht **FullMedia** ist.|  
|Windows und ConfigMgr einrichten|Mit diesem Tasksequenzschritt können Sie die Configuration Manager-Clientsoftware installieren. Mit dem Configuration Manager wird die GUID des Configuration Manager-Clients installiert und registriert. Sie können die erforderlichen Installationsparameter im Fenster **Installationseinstellungen** zuweisen.|  
|Updates installieren|Mithilfe dieses Tasksequenzschritts können Sie angeben, wie Softwareupdates auf dem Zielcomputer installiert werden. Der Zielcomputer wird erst beim Ausführen dieses Tasksequenzschritts hinsichtlich anwendbarer Softwareupdates ausgewertet. An diesem Punkt wird der Zielcomputer ähnlich wie jeder andere von Configuration Manager verwaltete Client hinsichtlich Softwareupdates ausgewertet.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSMediaType** verwendet. Dieser Tasksequenzschritt wird ausgeführt, wenn der zugeordnete Wert nicht **FullMedia** ist.|  
|Referenzcomputer erfassen – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine weitere Tasksequenzgruppe. Diese Gruppe enthält die für das Vorbereiten und Erfassen eines Referenzcomputers erforderlichen Schritte.|  
|Arbeitsgruppe beitreten|Mithilfe dieses Tasksequenzschritts können Sie die für den Beitritt des Zielcomputers in einer Arbeitsgruppe erforderlichen Informationen angeben.|  
|Prepare ConfigMgr Client for Capture|Mithilfe dieses Tasksequenzschritts können Sie den Configuration Manager-Client auf dem Referenzcomputer im Rahmen des Imageerstellungsprozesses für die Erfassung vorbereiten.|  
|Betriebssystem vorbereiten|Mit diesem Tasksequenzschritt geben Sie die Sysprep-Optionen an, mit denen die Windows-Einstellungen auf dem Referenzcomputer erfasst werden sollen. Dieser Tasksequenzschritt führt Sysprep aus und startet dann den Computer über das für die Tasksequenz angegebene Windows PE-Startabbild.|  
|Betriebssystemabbild erfassen|Geben Sie mithilfe dieses Tasksequenzschritts beim Speichern des Abbilds eine bestimmte vorhandene Netzwerkfreigabe sowie eine zu verwendende WIM-Datei an. Dieser Speicherort wird als Paketquellpfad verwendet, wenn mithilfe des **Assistenten zum Hinzufügen eines Betriebssystemabbilds**ein Betriebssystemabbildpaket hinzugefügt wird.|  

 Nachdem Sie ein Abbild von einem Referenzcomputer erfasst haben, dürfen Sie kein weiteres Betriebssystemabbild vom Referenzcomputer erfassen, da bei der ersten Konfiguration Registrierungseinträge erstellt werden. Erstellen Sie bei jedem Erfassen des Betriebssystemabbilds einen neuen Referenzcomputer. Wenn Sie den gleichen Referenzcomputer für das Erstellen zukünftiger Betriebssystemimages verwenden möchten, deinstallieren Sie zunächst den Configuration Manager-Client, und installieren Sie dann den Configuration Manager-Client erneut.  

## <a name="next-steps"></a>Nächste Schritte  
[Methoden zum Bereitstellen von Unternehmensbetriebssystemen](methods-to-deploy-enterprise-operating-systems.md)
