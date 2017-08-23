---
title: Verwalten von Betriebssystem-Upgradepaketen | Microsoft Docs
description: "Erfahren Sie, wie Sie Betriebssystem-Upgradepakete in System Center Configuration Manager verwalten können."
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5fef04f26b12bced073332fd1f7b4e7c7bd7d398
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-operating-system-upgrade-packages-with-system-center-configuration-manager"></a>Verwalten von Betriebssystem-Upgradepaketen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ein Upgradepaket in Configuration Manager enthält die Quelldateien für Windows Setup, mit denen ein vorhandenes Betriebssystem auf einem Computer upgegradet wird. Verwenden Sie die folgenden Abschnitte zum Verwalten von Betriebssystem-Upgradepaketen in Configuration Manager.

##  <a name="BKMK_AddOSUpgradePkgs"></a> Hinzufügen von Betriebssystem-Upgradepaketen zu Configuration Manager  
 Bevor Sie ein Betriebssystem-Upgradepaket verwenden können, müssen Sie das Paket zu einem Configuration Manager-Standort hinzufügen. Gehen Sie wie folgt vor, um ein Betriebssystem-Upgradepaket zu einem Standort hinzuzufügen.  

#### <a name="to-add-an-operating-system-upgrade-package"></a>So fügen Sie ein Betriebssystem-Upgradepaket hinzu  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Betriebssystem-Upgradepakete**.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Betriebssystem-Upgradepaket hinzufügen** , um den Assistenten zum Hinzufügen von Betriebssystem-Upgradepaketen zu starten.  

4.  Geben Sie auf der Seite **Datenquelle** den Netzwerkpfad zu den Installationsquelldateien des Betriebssystem-Upgradepakets an. Geben Sie z.B. mit **\\\server\path** den UNC-Pfad zu den Installationsquelldateien an.  

    > [!NOTE]  
    >  Zu den Installationsquelldateien gehören „Setup.exe“ sowie andere Dateien und Ordner zum Installieren des Betriebssystems.  

    > [!IMPORTANT]  
    >  Schränken Sie den Zugriff auf die Installationsquelldateien ein, um unerwünschte Manipulationen zu verhindern.  

5.  Geben Sie auf der Seite **Allgemein** die folgenden Informationen an, und klicken Sie dann auf **Weiter**. Diese Informationen sind für Identifikationszwecke hilfreich, wenn Sie über mehrere Betriebssysteminstallationspakete verfügen.  

    -   **Name**: Geben Sie den Namen des Betriebssysteminstallationspakets an.  

    -   **Version**: Geben Sie die Version des Betriebssysteminstallationspakets an.  

    -   **Comment**: Geben Sie eine kurze Beschreibung des Betriebssysteminstallationspakets an.  

6.  Schließen Sie den Assistenten ab.  

 Das Betriebssysteminstallationspaket kann nun auf die Verteilungspunkte verteilt werden, auf die von Ihren Bereitstellungs-Tasksequenzen zugegriffen wird.  

##  <a name="BKMK_DistributeBootImages"></a> Verteilen von Betriebssystemabbildern an einen Verteilungspunkt  
 Betriebssystemabbilder werden genau wie anderer Inhalt an Verteilungspunkte verteilt. In den meisten Fällen müssen Sie das Betriebssystemabbild an mindestens einen Verteilungspunkt verteilen, bevor Sie das Betriebssystem bereitstellen. Die Schritte zum Verteilen von Betriebssystemabbildern finden Sie unter [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="BKMK_OSUpgradePkgApplyUpdates"></a> Anwenden von Softwareupdates auf ein Betriebssystem-Upgradepaket  
 Ab Configuration Manager Version 1602 können Sie neue Softwareupdates auf das Betriebssystemimage in Ihrem Betriebssystem-Upgradepaket anwenden. Vor dem Anwenden von Softwareupdates auf ein Upgradepaket müssen die Softwareupdateinfrastruktur vorhanden, Softwareupdates erfolgreich synchronisiert und die Softwareupdates aus der Inhaltsbibliothek auf den Standortserver heruntergeladen worden sein. Weitere Informationen finden Sie unter [Bereitstellen von Softwareupdates](../../sum/deploy-use/deploy-software-updates.md).  

 Sie können relevante Softwareupdates nach einem festgelegten Zeitplan auf ein Upgradepaket anwenden. Basierend auf dem von Ihnen festgelegten Zeitplan wendet Configuration Manager die ausgewählten Softwareupdates auf das Betriebssystem-Upgradepaket an und verteilt das aktualisierte Upgradepaket anschließend optional an Verteilungspunkte. Die Informationen zum Betriebssystem-Upgradepaket werden in der Standortdatenbank gespeichert. Dazu gehören beispielsweise die Softwareupdates, die während des Imports angewendet wurden. Softwareupdates, die nach dem ursprünglichen Hinzufügen auf das Upgradepaket angewendet wurden, werden ebenfalls in der Standortdatenbank gespeichert. Wenn Sie den Assistenten starten, um Softwareupdates auf das Betriebssystem-Upgradepaket anzuwenden, ruft der Assistent eine Liste mit den verfügbaren Softwareupdates ab, die noch nicht auf das Upgradepaket angewendet wurden und ausgewählt werden können. Configuration Manager kopiert die Softwareupdates aus der Inhaltsbibliothek auf dem Standortserver und wendet die Softwareupdates auf das Betriebssystem-Upgradepaket an.  

 Verwenden Sie das folgende Verfahren, um Softwareupdates auf ein Betriebssystem-Upgradepaket anzuwenden.  

#### <a name="to-apply-software-updates-to-an-operating-system-upgrade-package"></a>So wenden Sie Softwareupdates auf ein Betriebssystem-Upgradepaket an  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Betriebssystem-Upgradepakete**.  

3.  Wählen Sie das Betriebssystem-Upgradepaket aus, auf das Softwareupdates angewendet werden sollen.  

4.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Betriebssystem-Upgradepakete** auf **Updates planen** , um den Assistenten zu starten.  

5.  Wählen Sie auf der Seite **Updates auswählen** die Softwareupdates aus, die auf das Betriebssystemabbild angewendet werden sollen, und klicken Sie dann auf **Weiter**.  

6.  Geben Sie auf der Seite **Zeitplan festlegen** die folgenden Einstellungen an, und klicken Sie dann auf **Weiter**.  

    1.  **Zeitplan**: Geben Sie den Zeitplan dafür an, wann die Softwareupdates auf das Betriebssystemabbild angewendet werden sollen.  

    2.  **Bei Fehler fortsetzen**: Aktivieren Sie diese Option, um anzugeben, dass Softwareupdates auch beim Auftreten eines Fehlers auf das Abbild angewendet werden sollen.  

    3.  **Abbild an Verteilungspunkte verteilen**: Wählen Sie diese Option aus, um das Betriebssystemabbild auf Verteilungspunkten zu aktualisieren, nachdem die Softwareupdates angewendet wurden.  

7.  Überprüfen Sie auf der Seite **Zusammenfassung** die Informationen, und klicken Sie dann auf **Weiter**.  

8.  Überprüfen Sie auf der Seite **Abschluss des Vorgangs** , ob die Softwareupdates erfolgreich auf das Betriebssystemabbild angewendet wurden.  
