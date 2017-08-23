---
title: Erstellen von Tasksequenzmedien mit System Center Configuration Manager | Microsoft-Dokumentation
description: Erstellen von Tasksequenzmedien, z.B. einer CD, um ein Betriebssystem auf einem Zielcomputer in Ihrer Configuration Manager-Umgebung bereitzustellen.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: bd5448d70c2d465347de840cb197d4c33075c90a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-task-sequence-media-with-system-center-configuration-manager"></a>Erstellen von Tasksequenzmedien mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe von Medien können Sie ein Betriebssystemimage von einem Referenzcomputer erfassen oder ein Betriebssystem auf einem Zielcomputer in Ihrer System Center Configuration Manager-Umgebung bereitstellen. Sie können eine CD, einen DVD-Satz oder einen USB-Speicherstick als Medien erstellen.  

 Medien werden überwiegend zur Betriebssystembereitstellung auf Zielcomputern ohne Netzwerkverbindung verwendet, oder auf Zielcomputern, deren Verbindung mit dem Configuration Manager-Standort eine geringe Bandbreite aufweist. Mithilfe von Bereitstellungsmedien können jedoch auch Betriebssystembereitstellungen außerhalb eines vorhandenen Windows-Betriebssystems gestartet werden. Diese zweite Verwendungsmöglichkeit für Bereitstellungsmedien ist von Bedeutung, wenn auf dem Zielcomputer kein Betriebssystem oder ein nicht funktionsfähiges Betriebssystem vorhanden ist oder wenn der Administrator die Festplatte des Zielcomputers neu partitionieren möchte.  

 Zu den Bereitstellungsmedien gehören startbare Medien, eigenständige Medien und vorab bereitgestellte Medien. Der Inhalt der Bereitstellungsmedien ist unterschiedlich und hängt von dem verwendeten Medientyp ab. So enthalten eigenständige Medien z. B. die Tasksequenz, mit der das Betriebssystem bereitgestellt wird, während die Tasksequenzen bei anderen Medientypen vom Verwaltungspunkt abgerufen werden.  

> [!IMPORTANT]  
>  Sie müssen ein Administrator auf dem Computer sein, von dem aus Sie die Configuration Manager-Konsole ausführen, um Tasksequenzmedien zu erstellen. Wenn Sie kein Administrator sind, werden Sie zur Eingabe von Administratoranmeldeinformationen aufgefordert, wenn Sie den Assistenten zum Erstellen von Tasksequenzmedien starten.  

##  <a name="BKMK_PlanCaptureMedia"></a> Erfassungsmedien für Betriebssystemimages  
 Mithilfe von Erfassungsmedien können Sie ein Betriebssystemabbild von einem Referenzcomputer aufzeichnen. Die Erfassungsmedien enthalten das Startabbild zum Starten des Referenzcomputers und die Tasksequenz zum Erfassen des Betriebssystemabbilds. Informationen zum Erstellen von Erfassungsmedien finden Sie unter [Erstellen von Erfassungsmedien mit System Center Configuration Manager](create-capture-media.md).  

##  <a name="BKMK_PlanBootableMedia"></a> Betriebssystembereitstellungen mithilfe startbarer Medien  
 Startbare Medien enthalten nur das Startimage, optionale [Prestart-Befehle](../understand/prestart-commands-for-task-sequence-media.md) und die dazu benötigten Dateien sowie die Configuration Manager-Binärdateien. Beim Starten des Zielcomputers wird eine Verbindung mit dem Netzwerk hergestellt. Die Tasksequenzen, das Betriebssystemabbild sowie sämtlicher anderer erforderlicher Inhalt werden dann aus dem Netzwerk abgerufen. Da sich die Tasksequenz nicht auf den Medien befindet, brauchen Sie die Medien nicht neu zu erstellen, wenn Sie die Tasksequenz oder den Inhalt ändern.  

> [!IMPORTANT]  
>  Die Pakete auf startbaren Medien sind nicht verschlüsselt. Der Administrator muss den Paketinhalt mithilfe geeigneter Sicherheitsmaßnahmen vor dem Zugriff Unbefugter schützen, z. B. durch Hinzufügen eines Kennworts für die Medien.  

 Informationen zum Erstellen von startbaren Medien finden Sie unter [Erstellen von startbaren Medien](create-bootable-media.md).  

##  <a name="BKMK_PlanPrestagedMedia"></a> Betriebssystembereitstellungen mithilfe vorab bereitgestellter Medien  
 Mithilfe von vorab bereitgestellten Medien können Sie startbare Medien und ein Betriebssystemabbild vor Beginn des eigentlichen Bereitstellungsprozesses auf einer Festplatte vorab bereitstellen. Bei vorab bereitgestellten Medien handelt es sich um eine WIM-Datei (Windows Imaging Format), die vom Hersteller auf einem Computer ohne Betriebssystem oder im Staging Center eines Unternehmens ohne Verbindung zur Configuration Manager-Umgebung installiert werden kann.  

 Vorab bereitgestellte Medien enthalten das Startabbild, mit dem der Zielcomputer gestartet wird, und das Betriebssystemabbild, das auf den Zielcomputer angewendet wird. Sie können auch Anwendungen, Pakete und Treiberpakete als Teil der vorab bereitgestellten Medien angeben. Die Tasksequenz zur Bereitstellung des Betriebssystems ist nicht in den Medien enthalten. Beim Bereitstellen einer Tasksequenz mit Verwendung von vorab bereitgestellten Medien wird der lokale Tasksequenzcache vom Client zuerst auf gültige Inhalte geprüft. Falls keine Inhalte gefunden werden oder falls diese geändert wurden, werden die Inhalte vom Client vom Verteilungspunkt heruntergeladen.  

 Vorab bereitgestellte Medien werden auf die Festplatte eines neuen Computers angewendet, bevor dieser an den Endbenutzer ausgeliefert wird. Wenn der Computer nach der Anwendung der vorab bereitgestellte Medien zum ersten Mal gestartet wird, wird Windows PE gestartet und eine Verbindung zu einem Verwaltungspunkt herstellt. Dort wird nach der Tasksequenz gesucht, mit der Bereitstellungsvorgang für das Betriebssystem abgeschlossen wird.  

> [!IMPORTANT]  
>  Die Pakete auf vorab bereitgestellte Medien sind nicht verschlüsselt. Der Administrator muss den Paketinhalt mithilfe geeigneter Sicherheitsmaßnahmen vor dem Zugriff Unbefugter schützen, z. B. durch Hinzufügen eines Kennworts für die Medien.  

 Informationen zum Erstellen von vorab bereitgestellten Medien finden Sie unter [Erstellen von vorab bereitgestellten Medien](create-prestaged-media.md).  

##  <a name="BKMK_PlanStandaloneMedia"></a> Betriebssystembereitstellungen mithilfe eigenständiger Medien  
 Eigenständige Medien enthalten alles, was zur Bereitstellung des Betriebssystems erforderlich ist. Dazu gehören die Tasksequenz und sämtlicher anderer erforderlicher Inhalt. Da alle Komponenten, die zur Bereitstellung des Betriebssystems erforderlich sind, auf den eigenständigen Medien gespeichert sind, ist der Speicherplatzbedarf für eigenständige Medien wesentlich größer als für andere Medientypen.  

 Informationen zum Erstellen von eigenständigen Medien finden Sie unter [Erstellen von eigenständigen Medien](create-stand-alone-media.md).  

## <a name="media-considerations-when-using-site-systems-configured-for-https"></a>Überlegungen zu Medien bei Verwendung von Standortsystemen mit HTTPS-Konfiguration  
 Wenn der Verwaltungspunkt und die Verteilungspunkte für die Verwendung der HTTPS-Kommunikation konfiguriert sind, müssen Sie startbare Medien und vorab bereitgestellte Medien an einem primären Standort erstellen, und nicht am Standort der zentralen Verwaltung. Berücksichtigen Sie auch Folgendes, um besser bestimmen zu können, ob die Medien als dynamisch oder als standortbasiert konfiguriert werden müssen:  

-   Zum Konfigurieren der Medien als dynamische Medien müssen alle primären Standorte über die Stammzertifizierungsstelle des Standorts verfügen, über den Sie die Medien erstellt haben. Sie können die Stammzertifizierungsstelle in alle primären Standorte der Hierarchie importieren.  

-   Wenn primäre Standorte in Ihrer Configuration Manager-Hierarchie unterschiedliche Stammzertifizierungsstellen verwenden, müssen Sie an jedem Standort standortbasierte Medien verwenden.  
