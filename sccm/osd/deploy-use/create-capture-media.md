---
title: "Erstellen von Erfassungsmedien – Configuration Manager | Microsoft-Dokumentation"
description: Verwenden Sie den Assistenten zum Erstellen von Tasksequenzmedien, um Erfassungsmedien in Configuration Manager zum Erfassen eines Betriebssystemimages von einem Referenzcomputer zu erstellen.
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5acf800ff5aebd849e294393337755145a60cca5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>Erstellen von Erfassungsmedien mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe von Erfassungsmedien in Configuration Manager können Sie ein Betriebssystemimage von einem Referenzcomputer erfassen. Verwenden Sie Erfassungsmedien für das folgende Szenario:  

-   [Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="BKMK_CreateCaptureMedia"></a> Erstellen von Erfassungsmedien  
 Verwenden Sie Erfassungsmedien, um ein Betriebssystemabbild auf einem Referenzcomputer zu erfassen. Die Erfassungsmedien enthalten das Startabbild zum Starten des Referenzcomputers und die Tasksequenz zum Erfassen des Betriebssystemabbilds.

Sie erstellen vorab Erfassungsmedien mit dem Assistenten zum Erstellen von Tasksequenzmedien. Achten Sie vor der Ausführung des Assistenten darauf, dass die folgenden Bedingungen erfüllt sind:  

|Aufgabe|Beschreibung|  
|----------|-----------------|  
|Startabbild|Beachten Sie die folgenden Informationen zum Startabbild, das Sie in der Tasksequenz zum Erfassen des Betriebssystems verwenden:<br /><br /> - Die Architektur des Startimages muss für die Architektur des Zielcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Zielcomputer gestartet und ausgeführt werden. Bei einem x86-Zielcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.<br />- Achten Sie darauf, dass das Startimage die zur Bereitstellung des Zielcomputers erforderlichen Netzwerk- und Massenspeichertreiber enthält.|  
|Verteilen aller der Tasksequenz zugeordneten Inhalte|Sie müssen alle für die Tasksequenz erforderlichen Inhalte auf mindestens einen Verteilungspunkt verteilen. Dies schließt das Startabbild, Betriebssystemabbild und andere zugehörige Dateien ein. Die Informationen werden vom Assistenten beim Erstellen des eigenständigen Mediums vom Verteilungspunkt abgerufen. Sie benötigen **Lesezugriffsrechte** für die Inhaltsbibliothek am Verteilungspunkt.  Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).|  
|Vorbereiten des USB-Wechseldatenträgers|Für einen USB-Wechseldatenträger:<br /><br /> Bei Verwendung eines USB-Wechseldatenträgers muss das USB-Laufwerk mit dem Computer verbunden werden, auf dem der Assistent ausgeführt wird. Das USB-Laufwerk muss zudem für Windows als Wechselmedium erkennbar sein. Beim Erstellen der Medien wird vom Assistenten direkt auf das USB-Laufwerk geschrieben.|  
|Erstellen eines Ausgabeordners|Für einen CD/DVD-Satz:<br /><br /> Sie müssen für die vom Assistenten zum Erstellen von Tasksequenzmedien erstellten Ausgabedateien einen Ordner anlegen, bevor Sie den Assistenten ausführen, um Medien für einen CD- oder DVD-Satz zu erstellen. Die für einen CD- oder DVD-Satz erstellten Medien werden als ISO-Dateien direkt in den Ordner geschrieben.|  

 Wenden Sie das folgende Verfahren an, um vorab Erfassungsmedien zu erstellen.  

#### <a name="to-create-capture-media"></a>So erstellen Sie Erfassungsmedien  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Tasksequenzen**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Tasksequenzmedien erstellen** , um den Assistenten zum Erstellen von Tasksequenzmedien zu starten.  

4.  Wählen Sie auf der Seite **Medientyp wählen** die Option **Erfassungsmedien**aus, und klicken Sie auf **Weiter**.  

5.  Geben Sie auf der Seite **Medientyp** an, ob das Medium ein Speicherstick oder ein CD/DVD-Satz ist, und klicken Sie dann, um Folgendes zu konfigurieren:  

    -   Wenn Sie **USB-Speicherstick**auswählen, geben Sie das Laufwerk an, auf dem der Inhalt gespeichert wird.  

    -   Wenn Sie **CD/DVD-Satz**auswählen, geben Sie die Kapazität der Medien und Namen sowie Pfad der Ausgabedateien an. Die Ausgabedateien werden vom Assistenten an diesen Speicherort geschrieben. Beispiel: **\\\Servername\Ordner\Ausgabedatei.iso**  

         Wenn die Medienkapazität zu gering zum Speichern des gesamten Inhalts ist, werden mehrere Dateien erstellt, und Sie müssen den Inhalt auf mehreren CDs oder DVDs speichern. Falls mehrere Medien erforderlich sind, wird dem Namen jeder von Configuration Manager erstellten Ausgabedatei eine Sequenznummer hinzugefügt. Außerdem wird die Anwendung von Configuration Manager auf mehreren Medien gespeichert, wenn Sie eine Anwendung zusammen mit dem Betriebssystem bereitstellen und die Anwendung nicht auf ein einzelnes Medium passt. Wenn das eigenständige Medium ausgeführt wird, wird der Benutzer von Configuration Manager zum Angeben des nächsten Mediums aufgefordert, auf dem die Anwendung gespeichert ist.  

        > [!IMPORTANT]  
        >  Wenn Sie ein vorhandenes ISO-Abbild auswählen, wird dieses ISO-Abbild vom Assistenten zum Erstellen von Tasksequenzmedien auf dem Laufwerk oder der Freigabe gelöscht, sobald Sie mit der nächsten Seite des Assistenten fortfahren. Das vorhandene Abbild wird selbst dann gelöscht, wenn Sie den Assistenten anschließend abbrechen.  

     Klicken Sie auf **Weiter**.  

6.  Geben Sie auf der Seite **Startabbild** die folgenden Informationen an, und klicken Sie dann auf **Weiter**.  

    > [!IMPORTANT]  
    >  Die Architektur des angegebenen Startabbilds muss für die Architektur des Referenzcomputers geeignet sein. Beispielsweise kann ein x86- oder x64-Startabbild von einem x64-Referenzcomputer gestartet und ausgeführt werden. Bei einem x86-Referenzcomputer sind jedoch nur der Start und die Ausführung eines x86-Startabbilds möglich.  

    -   Geben Sie im Feld **Startabbild** das Startabbild zum Starten des Referenzcomputers an.  

    -   Geben Sie im Feld **Verteilungspunkt** den Verteilungspunkt an, auf dem das Startabbild sich befindet. Das Startabbild wird von dem Assistenten vom Verteilungspunkt abgerufen und auf das Medium geschrieben.  

        > [!NOTE]  
        >  Sie benötigen Lesezugriffsrechte für die Inhaltsbibliothek am Verteilungspunkt.  

7.  Schließen Sie den Assistenten ab.  
