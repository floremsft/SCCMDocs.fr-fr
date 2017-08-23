---
title: Verwenden einer Tasksequenz zum Verwalten virtueller Festplatten | Microsoft-Dokumentation
description: "Erstellen Sie eine virtuelle Festplatte, fügen Sie Anwendungen und Softwareupdates hinzu, und veröffentlichen Sie die virtuelle Festplatte über die Configuration Manager-Konsole in System Center Virtual Machine Manager (VMM)."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
caps.latest.revision: "5"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: f77af4b8fcb193ed44511c0e5eea7290f55dbbf8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>Verwenden einer Tasksequenz zum Verwalten virtueller Festplatten in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager können Sie virtuelle Festplatten (Virtual Hard Disks, VHDs) verwalten und die erstellten virtuellen Festplatten über die Configuration Manager-Konsole in Ihr Datencenter integrieren. Die folgenden Aktionen sind möglich: Sie können eine virtuelle Festplatte erstellen und ändern, der virtuellen Festplatte Anwendungen und Softwareupdates hinzufügen und die virtuelle Festplatte über die Configuration Manager-Konsole in System Center Virtual Machine Manager (VMM) veröffentlichen.  

 In den folgenden Abschnitten erfahren Sie, wie Sie virtuelle Festplatten in Configuration Manager verwalten:

## <a name="prerequisites"></a>Voraussetzungen  
 Überprüfen Sie die folgenden Voraussetzungen, bevor Sie beginnen:  

-   Auf dem Computer, auf dem Sie virtuelle Festplatten verwalten, muss eines der folgenden Betriebssysteme ausgeführt werden:  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   Virtualisierung muss im BIOS aktiviert sein, und Hyper-V muss auf dem Computer installiert sein, auf dem Sie die Configuration Manager-Konsole für die Verwaltung von virtuellen Festplatten ausführen. Es hat sich zudem bewährt, die Hyper-V-Verwaltungstools zu installieren, um virtuelle Festplatten zu testen und Probleme damit zu behandeln. Beispiel: Die Hyper-V-Verwaltungstools müssen installiert sein, damit Sie die Datei smsts.log überwachen und so den Fortschritt der Tasksequenz in Hyper-V verfolgen können. Weitere Informationen zu Hyper-V-Anforderungen finden Sie unter [Hyper-V Installation Prerequisites (Voraussetzungen für die Hyper-V-Installation)](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!IMPORTANT]  
    >  Für den Prozess zum Erstellen einer virtuellen Festplatte werden Prozessorzeit und Arbeitsspeicher genutzt. Daher empfiehlt es sich, virtuelle Festplatten über eine Configuration Manager-Konsole zu verwalten, die nicht auf dem Standortserver installiert ist.  

-   Dem Standortserver muss die Zugriffsberechtigung **Schreiben** für den Ordner erteilt worden sein, der die VHD-Datei enthält, wenn Sie virtuelle Festplatten über einen Computer verwalten, der nicht der Standortserver ist.  

-   Stellen Sie sicher, dass Sie auf dem Computer, über den Sie die virtuellen Festplatten verwalten, über ausreichend Speicherplatz verfügen. Die Speicherplatzanforderungen der virtuellen Festplatte hängen vom Betriebssystem und den installierten Anwendungen ab.  

-   Stellen Sie sicher, dass Sie auf dem Computer, über den Sie die virtuellen Festplatten verwalten, über ausreichend Arbeitsspeicher verfügen. Während der Erstellung der virtuellen Festplatte werden vom virtuellen Computer 2 GB Arbeitsspeicher genutzt.  

-   Installieren Sie die System Center Virtual Machine Manager-Konsole (VMM) auf dem Computer, von dem Sie die virtuelle Festplatte in VMM hochladen. Sie können die VMM-Konsole auf einem separaten Computer installieren, über den Sie die virtuellen Festplatten verwalten. Dann muss Hyper-V nicht installiert sein, um die virtuelle Festplatte in VMM zu importieren.  

    > [!NOTE]  
    >  Wenn Sie die VMM-Konsole installieren, während die Configuration Manager-Konsole geöffnet ist, müssen Sie nach Abschluss der VMM-Konsoleninstallation die Configuration Manager-Konsole neu starten. Andernfalls kann von Configuration Manager keine Verbindung mit dem VMM-Verwaltungsserver hergestellt werden, um eine virtuelle Festplatte hochzuladen.  

##  <a name="BKMK_CreateVHDSteps"></a> Schritte zum Erstellen einer virtuellen Festplatte  
 Zum Erstellen einer virtuellen Festplatte müssen Sie eine Tasksequenz erstellen, die die Schritte zum Erstellen der virtuellen Festplatte enthält, und diese Tasksequenz dann im Assistenten zum Erstellen virtueller Festplatten verwenden, um die virtuelle Festplatte zu erstellen. In den folgenden Abschnitten sind die Schritte zum Erstellen der virtuellen Festplatte angegeben.  

###  <a name="BKMK_CreateTS"></a> Erstellen einer Tasksequenz für die virtuelle Festplatte  
 Sie müssen eine Tasksequenz erstellen, die die Schritte zum Erstellen der virtuellen Festplatte enthält. Der Tasksequenzerstellungs-Assistent weist die Option **Bestehendes Abbildpaket auf einer virtuellen Festplatte installieren** auf, mit der die Schritte zur Erstellen der virtuellen Festplatte erstellt werden. Der Assistent fügt z. B. die folgenden erforderlichen Schritte hinzu: Neustarten in Windows PE, Formatieren und Partitionieren des Datenträgers, Anwenden des Betriebssystems und Herunterfahren des Computers. Die virtuelle Festplatte kann unter einem vollständigen Betriebssystems nicht erstellt werden. Zudem muss in Configuration Manager gewartet werden, bis der virtuelle Computer heruntergefahren wurde, bevor das Paket abgeschlossen werden kann. Standardmäßig wird der virtuelle Computer vom Assistenten nach 5 Minuten heruntergefahren. Nach dem Erstellen der Tasksequenz können Sie bei Bedarf zusätzliche Schritte hinzufügen.  

> [!IMPORTANT]  
>  Im folgenden Verfahren wird die Tasksequenz mit der Option **Bestehendes Abbildpaket auf einer virtuellen Festplatte installieren** erstellt, mit der die erforderlichen Schritte zum erfolgreichen Erstellen der virtuellen Festplatte aufgenommen werden. Wenn Sie eine vorhandene Tasksequenz auswählen oder eine Tasksequenz manuell erstellen, müssen Sie am Ende der Tasksequenz den Schritt zum Herunterfahren des Computers hinzufügen. Ohne diesen Schritt wird der temporäre virtuelle Computer nicht gelöscht, und die Erstellung der virtuellen Festplatte wird nicht abgeschlossen. Allerdings wird vom Assistenten ein erfolgreicher Abschluss angegeben.  

 Verwenden Sie das folgende Verfahren, um die Tasksequenz zum Erstellen der virtuellen Festplatte zu erstellen:  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>So erstellen Sie die Tasksequenz zum Erstellen der virtuellen Festplatte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Klicken Sie auf der Seite **Neue Tasksequenz erstellen** auf **Bestehendes Abbildpaket auf einer virtuellen Festplatte installieren**und dann auf **Weiter**.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Tasksequenzname**: Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der Tasksequenz an.  

    -   **Startabbild**: Geben Sie das Startabbild an, von dem das Betriebssystem auf dem Zielcomputer installiert wird. Weitere Informationen finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

6.  Geben Sie auf der Seite **Windows installieren** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Abbildpaket**: Geben Sie das Paket an, welches das zu installierende Betriebssystemabbild enthält.  

    -   **Abbild**: Wenn das Betriebssystemabbildpaket mehrere Abbilder enthält, geben Sie den Indes des zu installierenden Betriebssystemabbilds an.  

    -   **Product key**: Geben Sie den Product Key für das zu installierende Windows-Betriebssystem an. Sie können codierte Volumenlizenzschlüssel und standardmäßige Product Keys angeben. Wenn Sie einen nicht codierten Product Key verwenden, muss jede Gruppe aus 5 Zeichen mit einen Bindestrich (-) getrennt werden. Beispiel: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Serverlizenzierungsmodus**: Geben Sie an, ob die Serverlizenz **Pro Arbeitsplatz**oder **Pro Server**bzw. dass keine Lizenz angegeben ist. Wenn die Serverlizenz **Pro Server**gilt, geben Sie auch die maximale Anzahl von Serververbindungen an.  

    -   Geben Sie an, wie das Administratorkonto verarbeitet werden soll, das bei der Bereitstellung des Betriebssystemabbilds verwendet wird.  

        -   **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren (empfohlen)**: Verwenden Sie diese Einstellung, damit der Assistent ein zufälliges Kennwort für das lokale Administratorkonto erstellt und das Konto deaktiviert, wenn das Betriebssystemabbild bereitgestellt wurde.  

        -   **Konto aktivieren und lokales Administratorkennwort angeben**: Verwenden Sie diese Einstellung, um ein bestimmtes Kennwort für das lokale Administratorkonto auf allen Computern zu verwenden, auf denen das Betriebssystemabbild bereitgestellt wird.  

7.  Geben Sie auf der Seite **Netzwerkeinstellungen konfigurieren** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Einer Arbeitsgruppe beitreten**: Geben Sie an, ob der Zielcomputer einer Arbeitsgruppe hinzugefügt werden soll.  

    -   **Einer Domäne beitreten**: Geben Sie an, ob der Zielcomputer einer Domäne hinzugefügt werden soll. Geben Sie unter **Domäne**den Namen der Domäne an.  

        > [!IMPORTANT]  
        >  Domänen in der lokalen Gesamtstruktur können Sie suchen, doch bei Domänen in remoten Gesamtstrukturen müssen Sie den Domänennamen angeben.  

         Sie können auch eine Organisationseinheit angeben. Dies ist eine optionale Einstellung, mit welcher der LDAP X.500-definierte Name der Organisationseinheit angegeben wird, in der das Computerkonto erstellt werden soll, sofern das Konto noch nicht vorhanden ist.  

    -   **Konto**: Geben Sie Benutzernamen und Kennwort für das Konto an, das die Berechtigungen hat, um der angegebenen Domäne beizutreten. Beispiel: *Domäne\Benutzer* oder *%Variable%*.  

8.  Geben Sie auf der Seite **Configuration Manager installieren** das Configuration Manager-Clientpaket an, das auf dem Zielcomputer installiert werden sollen, und klicken Sie auf **Weiter**.  

9. Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen, und klicken Sie dann auf **Weiter**. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

10. Schließen Sie den Assistenten ab.  

###  <a name="BKMK_CreateVHD"></a> Erstellen einer virtuellen Festplatte  
 Nachdem Sie eine Tasksequenz für die virtuelle Festplatte erstellt haben, erstellen Sie die virtuelle Festplatte mithilfe des Assistenten zum Erstellen virtueller Festplatten.  

> [!IMPORTANT]  
>  Stellen Sie vor der Ausführung dieses Verfahrens sicher, dass Sie die am Anfang dieses Themas aufgeführten Voraussetzungen erfüllen.  

 Verwenden Sie das folgende Verfahren, um eine virtuelle Festplatte zu erstellen.  

#### <a name="to-create-a-vhd"></a>So erstellen Sie eine virtuelle Festplatte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Virtuelle Festplatten**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Virtuelle Festplatte erstellen** , um den Assistenten zum Erstellen virtueller Festplatten zu starten.  

    > [!NOTE]  
    >  Hyper-V muss auf dem Computer installiert sein, auf dem die Configuration Manager-Konsole ausgeführt wird, über die Sie virtuelle Festplatten verwalten. Andernfalls ist die Option **Virtuelle Festplatte erstellen** nicht aktiviert. Weitere Informationen zu Hyper-V-Anforderungen finden Sie unter [Hyper-V Installation Prerequisites (Voraussetzungen für die Hyper-V-Installation)](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!TIP]  
    >  Erstellen Sie einen neuen Ordner, oder wählen Sie unter dem Knoten **Virtuelle Festplatten** einen vorhandenen Ordner aus, und klicken Sie in dem Ordner auf **Virtuelle Festplatte erstellen** , um die virtuellen Festplatten zu organisieren.  

4.  Geben Sie auf der Seite **Allgemein** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Name**: Geben Sie einen eindeutigen Namen für die virtuelle Festplatte an.  

    -   **Version**: Geben Sie eine Versionsnummer für die virtuelle Festplatte an. Dies ist eine optionale Einstellung.  

    -   **Kommentar**: Geben Sie eine Beschreibung für die virtuelle Festplatte an.  

    -   **Pfad**: Geben Sie den Pfad und den Dateinamen für die Erstellung der VHD-Datei durch den Assistenten an.  

         Sie müssen einen gültigen Netzwerkpfad im UNC-Format eingeben. Beispiel: **\\\Servername\\<Freigabename\>\\<Dateiname\>.vhd**.  

        > [!WARNING]  
        >  Configuration Manager muss die Zugriffsberechtigung **Schreiben** für den angegebenen Pfad erteilt worden sein, damit die virtuelle Festplatte erstellt werden kann. Wenn von Configuration Manager nicht auf den Pfad zugegriffen werden kann, wird der entsprechende Fehler in der Datei „distmgr.log“ auf dem Standortserver protokolliert.  

5.  Geben Sie auf der Seite **Tasksequenz** die Tasksequenz aus dem vorherigen Abschnitt an, und klicken Sie dann auf **Weiter**.  

6.  Wählen Sie auf der Seite **Verteilungspunkte** mindestens einen Verteilungspunkt aus, der den für die Tasksequenz erforderlichen Inhalt enthält, und klicken Sie dann auf **Weiter**.  

7.  Klicken Sie auf der Seite **Anpassung** auf **Weiter**. Beim Vorgang zum Erstellen der virtuellen Festplatte werden alle auf diese Seite angegebenen Einstellungen ignoriert.  

8.  Überprüfen Sie die Einstellungen, und klicken Sie anschließend auf **Weiter**. Die virtuelle Festplatte wird vom Assistenten erstellt.  

    > [!TIP]  
    >  Die Dauer bis zum Abschluss des Prozesses zum Erstellen der virtuellen Festplatte kann variieren. Während der Prozess vom Assistenten bearbeitet wird, können Sie den Fortschritt in den folgenden Protokolldateien überwachen. Standardmäßig befinden sich die Protokolle auf dem Computer mit der Configuration Manager-Konsole unter %*ProgramFiles (x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: In dieses Protokoll werden vom Assistenten Informationen geschrieben, während die Tasksequenzmedien erstellt werden. Überprüfen Sie diese Protokolldatei, um den Fortschritt des Assistenten beim Erstellen der eigenständigen Medien zu überwachen.  
    > -   **DeployToVHD.log**: In dieses Protokoll werden vom Assistenten Informationen geschrieben, während die virtuelle Festplatte erstellt wird. Überprüfen Sie diese Protokolldatei, um den Fortschritt des Assistenten bei allen Schritten nach dem Erstellen der eigenständigen Medien zu überwachen.  
    >   
    >  Darüber hinaus können Sie beim Start der Betriebssysteminstallation den Hyper-V-Manager öffnen (sofern Sie die Hyper-V-Verwaltungstools auf dem Computer installiert haben) und eine Verbindung mit dem vom Assistenten erstellten temporären virtuellen Computer herstellen, um die Ausführung der Tasksequenz anzuzeigen. Über den virtuellen Computer können Sie in der Datei smsts.log den Fortschritt der Tasksequenz überwachen. Bei Problemen mit dem Abschluss eines Tasksequenzschritts können Sie diese Protokolldatei zur Problembehandlung verwenden. Vor der Formatierung der Festplatte befindet sich die Datei smsts.log unter X:\windows\temp\smstslog\smsts.log, nach der Formatierung befindet sie sich unter C:\\_SMSTaskSequence\Logs\Smstslog\. Nach Abschluss der Tasksequenzschritte wird der virtuelle Computer (standardmäßig) nach 5 Minuten heruntergefahren und gelöscht.  

 Nach dem Erstellen der virtuellen Festplatte in Configuration Manager befindet sich diese im Knoten **Virtuelle Festplatten** in der Configuration Manager-Konsole unter dem Knoten **Betriebssystembereitstellung** im Arbeitsbereich **Softwarebibliothek**.  

> [!NOTE]  
>  Die Größe der virtuellen Festplatte wird von Configuration Manager abgerufen, indem eine Verbindung mit dem Quellspeicherort der virtuellen Festplatte hergestellt wird. Wenn ein Zugriff auf die VHD-Datei durch Configuration Manager nicht möglich ist, wird in der Spalte **Größe (KB)** für die virtuelle Festplatte **0** angezeigt.  

##  <a name="BKMK_ModifyVHDSteps"></a> Schritte zum Ändern einer vorhandenen virtuellen Festplatte  
 Zum Ändern einer virtuellen Festplatte müssen Sie eine Tasksequenz mit den Schritten erstellen, die zum Ändern der virtuellen Festplatte erforderlich sind. Danach wählen Sie die Tasksequenz im Assistenten zum Ändern virtueller Festplatten aus. Die virtuelle Festplatte wird mit der virtuellen Maschine verbunden, die Tasksequenz wird in der virtuellen Festplatte ausgeführt, und die VHD-Datei wird nachfolgend aktualisiert. In den folgenden Abschnitten sind die Schritte zum Ändern der virtuellen Festplatte angegeben.  

###  <a name="BKMK_ModifyTS"></a> Erstellen einer Tasksequenz zum Ändern der virtuellen Festplatte  
 Zum Ändern einer vorhandenen virtuellen Festplatte müssen Sie diese zunächst als Tasksequenz erstellen. Wählen Sie nur die Schritte aus, die zum Ändern der Tasksequenz erforderlich sind. Wenn Sie der virtuellen Festplatte beispielsweise eine Anwendung hinzufügen möchten, erstellen Sie eine benutzerdefinierte Tasksequenz, und fügen Sie dann nur den Schritt zum Installieren der Anwendung hinzu.  

 Verwenden Sie das folgende Verfahren, um die Tasksequenz zum Ändern der virtuellen Festplatte zu erstellen:  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>So erstellen Sie eine benutzerdefinierte Tasksequenz zum Ändern der virtuellen Festplatte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenz erstellen** , um den Tasksequenzerstellungs-Assistenten zu starten.  

4.  Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Neue benutzerdefinierte Tasksequenz erstellen**aus, und klicken Sie dann auf **Weiter**.  

5.  Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    -   **Tasksequenzname**: Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    -   **Beschreibung**: Geben Sie eine Beschreibung der Tasksequenz an.  

    -   **Startabbild**: Geben Sie das Startabbild an, von dem das Betriebssystem auf dem Zielcomputer installiert wird. Weitere Informationen finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

6.  Schließen Sie den Assistenten ab.  

 Gehen Sie wie folgt vor, um der benutzerdefinierten Tasksequenz Tasksequenzschritte hinzuzufügen.  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>So fügen Sie der benutzerdefinierten Tasksequenz Tasksequenzschritte hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie **Betriebssysteme** im Arbeitsbereich **Softwarebibliothek**, klicken Sie auf **Tasksequenzen**, und wählen Sie dann die benutzerdefinierte Tasksequenz aus, die Sie mit dem vorherigen Verfahren erstellt haben.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Tasksequenz** auf **Bearbeiten** , um den Tasksequenz-Editor zu starten.  

4.  Fügen Sie Tasksequenzschritte hinzu, mit denen die virtuelle Festplatte geändert wird.  

5.  Klicken Sie auf **OK** , um den Tasksequenz-Editor zu beenden.  

###  <a name="BKMK_ModifyVHD"></a> Ändern einer virtuellen Festplatte  
 Nachdem Sie eine Tasksequenz für die virtuelle Festplatte erstellt haben, ändern Sie die virtuelle Festplatte mithilfe des Assistenten zum Ändern virtueller Festplatten.  

 Verwenden Sie das folgende Verfahren, um eine virtuelle Festplatte zu ändern.  

#### <a name="to-modify-a-vhd"></a>So ändern Sie eine virtuelle Festplatte  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie **Betriebssysteme** im Arbeitsbereich **Softwarebibliothek**, klicken Sie auf **Virtuelle Festplatten**, und wählen Sie dann die zu ändernde Festplatte aus.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Virtuelle Festplatte** auf **Virtuelle Festplatte ändern** , um den Assistenten zum Ändern virtueller Festplatten zu starten.  

    > [!NOTE]  
    >  Hyper-V muss auf dem Computer installiert sein, auf dem die Configuration Manager-Konsole ausgeführt wird, über die Sie virtuelle Festplatten verwalten. Andernfalls ist die Option **Virtuelle Festplatte ändern** nicht aktiviert. Weitere Informationen zu Hyper-V-Anforderungen finden Sie unter [Hyper-V Installation Prerequisites (Voraussetzungen für die Hyper-V-Installation)](http://technet.microsoft.com/library/cc731898.aspx).  

4.  Überprüfen Sie auf der Seite **Allgemein** die folgenden Einstellungen, und klicken Sie dann auf **Weiter**.  

    -   **Name**: Gibt einen eindeutigen Namen für die virtuelle Festplatte an.  

    -   **Version**: Gibt die Versionsnummer für die virtuelle Festplatte an. Dies ist eine optionale Einstellung.  

    -   **Kommentar**: Gibt die Beschreibung für die virtuelle Festplatte an.  

    -   **Pfad**: Gibt den Pfad und den Dateinamen für den Speicherort der VHD-Datei an. Diese Einstellung kann nicht geändert werden.  

        > [!WARNING]  
        >  Configuration Manager muss die Zugriffsberechtigung **Schreiben** für den angegebenen Pfad erteilt worden sein, damit die virtuelle Festplatte erstellt werden kann. Wenn von Configuration Manager nicht auf den Pfad zugegriffen werden kann, wird der entsprechende Fehler in der Datei „distmgr.log“ auf dem Standortserver protokolliert.  

5.  Geben Sie auf der Seite **Tasksequenz** die im vorherigen Abschnitt erstellte benutzerdefinierte Tasksequenz an, und klicken Sie dann auf **Weiter**.  

6.  Wählen Sie auf der Seite **Verteilungspunkte** mindestens einen Verteilungspunkt aus, der den für die Tasksequenz erforderlichen Inhalt enthält, und klicken Sie dann auf **Weiter**.  

7.  Klicken Sie auf der Seite **Anpassung** auf **Weiter**. Beim Vorgang zum Ändern der virtuellen Festplatte werden alle auf dieser Seite angegebenen Einstellungen ignoriert.  

8.  Überprüfen Sie die Einstellungen, und klicken Sie anschließend auf **Weiter**. Die geänderte virtuelle Festplatte wird vom Assistenten erstellt.  

    > [!TIP]  
    >  Die Dauer bis zum Abschluss des Vorgangs zum Ändern der virtuellen Festplatte kann variieren. Während der Prozess vom Assistenten bearbeitet wird, können Sie den Fortschritt in den folgenden Protokolldateien überwachen. Standardmäßig befinden sich die Protokolle auf dem Computer mit der Configuration Manager-Konsole unter %*ProgramFiles (x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: In dieses Protokoll werden vom Assistenten Informationen geschrieben, während die Tasksequenzmedien erstellt werden. Überprüfen Sie diese Protokolldatei, um den Fortschritt des Assistenten beim Erstellen der eigenständigen Medien zu überwachen.  
    > -   **DeployToVHD.log**: In dieses Protokoll werden vom Assistenten Informationen geschrieben, während die virtuelle Festplatte geändert wird. Überprüfen Sie diese Protokolldatei, um den Fortschritt des Assistenten bei allen Schritten nach dem Erstellen der eigenständigen Medien zu überwachen.  
    >   
    >  Darüber hinaus können Sie den Hyper-V-Manager öffnen (sofern Sie die Hyper-V-Verwaltungstools auf dem Computer installiert haben) und eine Verbindung mit dem vom Assistenten erstellten temporären virtuellen Computer herstellen, um die Ausführung der Tasksequenz anzuzeigen. Über den virtuellen Computer können Sie in der Datei smsts.log den Fortschritt der Tasksequenz überwachen. Bei Problemen mit dem Abschluss eines Tasksequenzschritts können Sie diese Protokolldatei zur Problembehandlung verwenden. Vor der Formatierung der Festplatte befindet sich die Datei smsts.log unter X:\windows\temp\smstslog\smsts.log, nach der Formatierung befindet sie sich unter C:\\_SMSTaskSequence\Logs\Smstslog\. Nach Abschluss der Tasksequenzschritte wird der virtuelle Computer (standardmäßig) nach 5 Minuten heruntergefahren und gelöscht.  

##  <a name="BKMK_ApplyUpdates"></a> Anwenden von Softwareupdates auf eine virtuelle Festplatte  
 Es werden regelmäßig neue Softwareupdates veröffentlicht, die für das Betriebssystem Ihrer virtuellen Festplatte gelten. Sie können relevante Softwareupdates nach einem festgelegten Zeitplan auf eine virtuelle Festplatte anwenden. Nach dem festgelegten Zeitplan werden von Configuration Manager die ausgewählten Softwareupdates auf die virtuelle Festplatte angewendet.  

 Die Informationen zur virtuellen Festplatte werden in der Standortdatenbank gespeichert. Dazu gehören beispielsweise die Softwareupdates, die während der Erstellung der virtuellen Festplatte angewendet wurden. Softwareupdates, die nach dem ursprünglichen Erstellen auf die virtuelle Festplatte angewendet wurden, werden ebenfalls in der Standortdatenbank gespeichert. Wenn Sie den Assistenten starten, um Softwareupdates auf die virtuelle Festplatte anzuwenden, wird vom Assistenten eine Liste mit den verfügbaren Softwareupdates abgerufen, die noch nicht auf die virtuelle Festplatte angewendet wurden und ausgewählt werden können.  

 Sie können die Einstellung **Bei Fehler fortsetzen** für Configuration Manager auswählen. Softwareupdates werden dann auch weiter angewendet, wenn beim Anwenden von einem oder mehreren ausgewählten Softwareupdates ein Fehler auftritt.  

> [!NOTE]  
>  Die Softwareupdates werden aus der Inhaltsbibliothek auf dem Standortserver kopiert.  

 Verwenden Sie das folgende Verfahren, um Softwareupdates auf eine virtuellen Festplatte anzuwenden.  

#### <a name="to-apply-software-updates-to-a-vhd"></a>So wenden Sie Softwareupdates auf eine virtuelle Festplatte an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Virtuelle Festplatten**.  

3.  Wählen Sie die virtuelle Festplatte aus, auf die Sie Softwareupdates anwenden möchten.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Virtuelle Festplatte** auf **Updates planen** , um den Assistenten zu starten.  

5.  Wählen Sie auf der Seite **Updates auswählen** die Softwareupdates aus, die auf die virtuelle Festplatte angewendet werden sollen, und klicken Sie dann auf **Weiter**.  

6.  Geben Sie auf der Seite **Zeitplan festlegen** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    1.  **Zeitplan**: Geben Sie den Zeitplan für die Anwendung der Softwareupdates auf die virtuelle Festplatte an.  

    2.  **Bei Fehler fortsetzen**: Aktivieren Sie diese Option, um anzugeben, dass Softwareupdates auch beim Auftreten eines Fehlers auf das Abbild angewendet werden sollen.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** die Informationen, und klicken Sie dann auf **Weiter**.  

8.  Überprüfen Sie auf der Seite **Abschluss des Vorgangs** , ob die Softwareupdates erfolgreich auf das Betriebssystemabbild angewendet wurden.  

##  <a name="BKMK_ImportToVMM"></a> Importieren der virtuellen Festplatte in System Center Virtual Machine Manager  
 System Center VMM ist eine Verwaltungslösung für virtualisierte Rechenzentren, mit der Sie Virtualisierungshosts, Netzwerk- und Speicherressourcen konfigurieren und verwalten können, um in von Ihnen erstellten privaten Clouds virtuelle Computer und Dienste zu erstellen und bereitzustellen. Nach der Erstellung einer virtuellen Festplatte in Configuration Manager können Sie die virtuelle Festplatte mit VMM importieren und verwalten.  

> [!TIP]  
>  Bevor Sie eine virtuelle Festplatte in VMM hochladen, überprüfen Sie, ob von der VMM-Konsole erfolgreich eine Verbindung mit dem VMM-Verwaltungsserver hergestellt werden kann.  

 Verwenden Sie das folgende Verfahren, um eine virtuelle Festplatte in VMM zu importieren.  

#### <a name="to-import-a-vhd-to-vmm"></a>So importieren Sie eine virtuelle Festplatte in VMM  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Virtuelle Festplatten**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Virtuelle Festplatte** auf **Zu Virtual Machine Manager hochladen** , um den Assistenten zu starten.  

4.  Konfigurieren Sie auf der Seite **Allgemein** die folgenden Einstellungen, und klicken Sie dann auf **Weiter**.  

    -   **VMM-Servername**: Geben Sie den FQDN des Computers an, auf dem der VMM-Verwaltungsserver installiert ist. Vom Assistenten wird eine Verbindung mit dem VMM-Verwaltungsserver hergestellt, um die Bibliotheksfreigaben für den Server herunterzuladen.  

    -   **VMM-Bibliotheksfreigabe**: Geben Sie in der Dropdownliste die VMM-Bibliotheksfreigabe an.  

    -   **Nicht verschlüsselte Übertragung verwenden**: Wählen Sie diese Einstellung aus, um die VHD-Datei unverschlüsselt an den VMM-Verwaltungsserver zu übertragen.  

5.  Überprüfen Sie auf der Seite Zusammenfassung die Einstellungen, und schließen Sie dann den Assistenten ab. Abhängig von der Größe der VHD-Datei und der Netzwerkbandbreite für die Verbindung mit dem VMM-Verwaltungsserver kann die Dauer für das Hochladen der virtuellen Festplatte variieren.  
