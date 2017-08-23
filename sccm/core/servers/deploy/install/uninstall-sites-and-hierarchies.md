---
title: Deinstallieren von Standorten | Microsoft-Dokumentation
description: Verwenden Sie diese Informationen als Leitfaden, wenn Sie einen System Center Configuration Manager-Standort deinstallieren.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6ad06753dc0e1d0958f7131afbf3ecb75eecb2e3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Deinstallieren von Standorten und Hierarchien für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie die folgenden Informationen als Leitfaden, wenn Sie einen System Center Configuration Manager-Standort deinstallieren müssen.  

Um eine Hierarchie mit mehreren Standorten aufzuheben, müssen die Standorte in einer bestimmten Reihenfolge entfernt werden. Beim Deinstallieren von Standorten beginnen Sie am unteren Ende der Hierarchie und arbeiten sich zum oberen Ende vor:  

1.  Entfernen Sie die mit den primären Standorten verbundenen sekundären Standorte.  
2.  Entfernen Sie die primären Standorte.
3.  Nachdem alle primären Standorte entfernt wurden, können Sie den Standort der zentralen Verwaltung deinstallieren.  


##  <a name="BKMK_RemoveSecondarysite"></a> Entfernen eines sekundären Standorts aus einer Hierarchie  
Sekundäre Standorte können nicht verschoben bzw. an einem neuen übergeordneten primären Standort erneut zugewiesen werden. Damit ein sekundärer Standort aus einer Hierarchie entfernt werden kann, muss er am direkten übergeordneten Standort gelöscht werden. Verwenden Sie den Assistenten zum Löschen sekundärer Standorte aus der Configuration Manager-Konsole, um einen sekundären Standort zu entfernen. Wenn Sie einen sekundären Standort entfernen, müssen Sie auswählen, ob er gelöscht oder deinstalliert werden soll:  

-   **Sekundären Standort deinstallieren**. Mit dieser Option können Sie einen funktionsfähigen sekundären Standort entfernen, auf den über das Netzwerk zugegriffen werden kann. Mit dieser Option wird Configuration Manager vom sekundären Standortserver deinstalliert. Anschließend werden alle Informationen über den Standort und seine Ressourcen aus der Configuration Manager-Standorthierarchie gelöscht. Wenn SQL Server Express von Configuration Manager als Teil der Installation des sekundären Standorts installiert wurde, wird SQL Server Express von Configuration Manager beim Deinstallieren des sekundären Standorts deinstalliert. Falls SQL Server Express vor der Installation des sekundären Standorts installiert wurde, wird SQL Server Express von Configuration Manager nicht deinstalliert.  

-   **Sekundären Standort löschen**. Verwenden Sie diese Option, wenn eine der folgenden Aussagen zutrifft:  

    -   Bei der Installation eines sekundären Standorts ist ein Fehler aufgetreten  
    -   Nach der Deinstallation wird der sekundäre Standort weiterhin in der Configuration Manager-Konsole angezeigt

    Mit dieser Option werden alle Informationen über den Standort und die zugeordneten Ressourcen aus der Configuration Manager-Hierarchie gelöscht. Configuration Manager bleibt jedoch auf dem sekundären Standortserver installiert.  

    > [!NOTE]  
    >  Ein sekundärer Standort kann auch mit dem Hierarchieverwaltungstool und der Option **/DELSITE** gelöscht werden. Weitere Informationen finden Sie unter [Hierarchiewartungstool (Preinst.exe) für System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>So deinstallieren oder löschen Sie einen sekundären Standort  

1.  Überprüfen Sie, ob der Administrator, der die Installation ausführt, über die folgenden Sicherheitsrechte verfügt:  

    -   Administratorrechte auf dem sekundären Standortcomputer  
    -   Lokale Administratorrechte auf dem Datenbankserver des Remotestandorts für den primären Standort, sofern dieser ein Remotestandort ist  
    -   Sicherheitsrolle „Infrastrukturadministrator“ oder „Hauptadministrator“ am übergeordneten primären Standort  
    -   Systemadministratorrechte auf der Standortdatenbank des sekundären Standorts  

2.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  
3.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und wählen Sie **Standorte** aus.  
4.  Wählen Sie den sekundären Standortserver aus, der entfernt werden soll.  
5.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standort** auf **Löschen**.  
6.  Wählen Sie auf der Seite **Allgemein** aus, ob der sekundäre Standort deinstalliert oder gelöscht werden soll. Klicken Sie dann auf **Weiter**.  
7.  Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen, und klicken Sie dann auf **Weiter**.  
8.  Klicken Sie auf der Seite **Abschluss des Vorgangs** zum Beenden des Assistenten auf **Schließen**.  

##  <a name="BKMK_UninstallPrimary"></a> Deinstallieren eines primären Standorts  
Sie können das Configuration Manager-Setup ausführen, um einen primären Standort zu deinstallieren, dem kein sekundärer Standort zugeordnet ist. Beachten Sie vor der Deinstallation eines primären Standorts folgende Punkte:  

-   Wenn sich die Configuration Manager-Clients innerhalb der am Standort konfigurierten Grenzen befinden und der primäre Standort Teil einer Configuration Manager-Hierarchie ist, kann es sinnvoll sein, die Grenzen einem anderen primären Standort in der Hierarchie hinzuzufügen, bevor der primäre Standort deinstalliert wird.  
-   Ist der primäre Standortserver nicht mehr verfügbar, müssen Sie das Hierarchieverwaltungstool am Standort der zentralen Verwaltung verwenden, um den primären Standort aus der Standortdatenbank zu löschen. Weitere Informationen finden Sie unter [Hierarchiewartungstool (Preinst.exe) für System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Gehen Sie wie folgt vor, um einen primären Standort zu deinstallieren.  

#### <a name="to-uninstall-a-primary-site"></a>So deinstallieren Sie einen primären Standort  

1.  Überprüfen Sie, ob der Administrator, der die Installation ausführt, über die folgenden Sicherheitsrechte verfügt:  

    -   Lokale Administratorrechte auf dem Server des Standorts der zentralen Verwaltung  
    -   Lokale Administratorrechte auf dem Datenbankserver des Remotestandorts für den Standort der zentralen Verwaltung, sofern dieser ein Remotestandort ist
    -   Systemadministratorrechte auf der Standortdatenbank des Standorts der zentralen Verwaltung  
    -   Lokale Administratorrechte auf dem primären Standortcomputer  
    -   Lokale Administratorrechte auf dem Datenbankserver des Remotestandorts für den primären Standort, sofern dieser ein Remotestandort ist  
    -   Ein Benutzername, der der Sicherheitsrolle „Infrastrukturadministrator“ oder „Hauptadministrator“ am Standort der zentralen Verwaltung zugeordnet ist  

2.  Starten Sie das Configuration Manager-Setup auf dem primären Standortserver mithilfe eines der folgenden Verfahren:  

    -   Klicken Sie unter **Start** auf **Configuration Manager-Setup**.  
    -   Öffnen Sie die Datei „Setup.exe“ im Verzeichnis &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  
    -   Öffnen Sie die Datei „Setup.exe“ im Verzeichnis &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  Wählen Sie auf der Seite **Vorbereitung** die Option **Weiter**.  
4.  Wählen Sie auf der Seite **Erste Schritte** die Option **Configuration Manager-Standort deinstallieren**, und klicken Sie dann auf **Weiter**.  
5.  Geben Sie unter **Configuration Manager-Standort deinstallieren** an, ob die Standortdatenbank vom primären Standortserver und die Configuration Manager-Konsole entfernt werden sollen. Standardmäßig werden beide Komponenten entfernt.  

    > [!IMPORTANT]  
    >  Wenn dem primären Standort ein sekundärer Standort zugeordnet ist, müssen Sie den sekundären Standort entfernen, bevor Sie den primären Standort deinstallieren können.  

6.  Klicken Sie auf **Ja**, um zu bestätigen, dass der primäre Configuration Manager-Standort deinstalliert werden soll.  

##  <a name="BKMK_UninstallPrimaryDistViews"></a> Deinstallieren eines primären Standorts, der mit verteilten Ansichten konfiguriert ist  
 Sie müssen verteilte Ansichten in der Hierarchie deaktivieren, bevor Sie einen untergeordneten primären Standort deinstallieren, für dessen Replikationslink zum Standort der zentralen Verwaltung verteilte Ansichten aktiviert sind. Nutzen Sie die folgenden Informationen zum Deaktivieren von verteilten Ansichten, bevor Sie einen primären Standort deinstallieren.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>So deinstallieren Sie einen primären Standort, für den verteilte Ansichten konfiguriert wurden  

1.  Vor dem Deinstallieren primärer Standorte müssen Sie verteilte Ansichten für alle Links der Hierarchie zwischen dem Standort der zentralen Verwaltung und einem primären Standort deaktivieren.  
2.  Nachdem Sie verteilte Ansichten für die einzelnen Links deaktiviert haben, müssen Sie sicherstellen, dass für die Daten des primären Standorts eine Neuinitialisierung am Standort der zentralen Verwaltung ausgeführt wird. Sie können die Initialisierung der Daten überwachen, wenn Sie den Link in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** im Knoten **Datenbankreplikation** anzeigen.  
3.  Nachdem die Daten für den Standort der zentralen Verwaltung neu initialisiert wurden, können Sie den primären Standort deinstallieren. Informationen zum Deinstallieren eines primären Standorts finden Sie unter [Deinstallieren eines primären Standorts](#BKMK_UninstallPrimary).  
4.  Nach der vollständigen Deinstallation des primären Standorts können Sie verteilte Ansichten für Links zu primären Standorten neu konfigurieren.  

    > [!IMPORTANT]  
    >  Wenn Sie den primären Standort vor dem Deaktivieren der verteilten Ansichten eines Standorts oder vor der erfolgreichen Neuinitialisierung der Daten am Standort der zentralen Verwaltung deinstallieren, kann bei der Replikation der Daten zwischen primären Standorten und dem Standort der zentralen Verwaltung ein Fehler auftreten. In diesem Fall müssen Sie die verteilten Ansichten für jeden Link der Standorthierarchie deaktivieren. Nachdem die Daten für den Standort der zentralen Verwaltung neu initialisiert wurden, können Sie die verteilten Ansichten neu konfigurieren.  

##  <a name="BKMK_UninstallCAS"></a> Deinstallieren des Standorts der zentralen Verwaltung  
 Sie können das Configuration Manager-Setup ausführen, um einen Standort der zentralen Verwaltung ohne untergeordnete primäre Standorte zu deinstallieren. Wenden Sie das folgende Verfahren an, um den Standort der zentralen Verwaltung zu deinstallieren.  

#### <a name="to-uninstall-a-central-administration-site"></a>So deinstallieren Sie einen Standort der zentralen Verwaltung  

1.  Überprüfen Sie, ob der Administrator, der die Installation ausführt, über die folgenden Sicherheitsrechte verfügt:  

    -   Lokale Administratorrechte auf dem Server des Standorts der zentralen Verwaltung  
    -   Lokale Administratorrechte auf dem Standortdatenbankserver für den Standort der zentralen Verwaltung, sofern der Standortdatenbankserver nicht auf dem Standortserver installiert ist 

2.  Starten Sie das Configuration Manager-Setup auf dem Standortserver der zentralen Verwaltung mithilfe eines der folgenden Verfahren:  

    -   Klicken Sie unter **Start**auf **Configuration Manager-Setup**.  
    -   Öffnen Sie die Datei „Setup.exe“ im Verzeichnis &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  
    -   Öffnen Sie die Datei „Setup.exe“ im Verzeichnis &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  Wählen Sie auf der Seite **Vorbereitung** die Option **Weiter**.  
4.  Wählen Sie auf der Seite **Erste Schritte** die Option **Configuration Manager-Standort deinstallieren**, und klicken Sie dann auf **Weiter**.  
5.  Geben Sie unter **Configuration Manager-Standort deinstallieren** an, ob die Standortdatenbank vom Standortserver der zentralen Verwaltung und die Configuration Manager-Konsole entfernt werden sollen. Standardmäßig werden beide Komponenten entfernt.  

    > [!IMPORTANT]  
    >  Wenn dem Standort der zentralen Verwaltung ein primärer Standort zugeordnet ist, müssen Sie den primären Standort entfernen, bevor Sie den Standort der zentralen Verwaltung deinstallieren können.  

6.  Klicken Sie auf **Ja**, um zu bestätigen, dass der Configuration Manager-Standort der zentralen Verwaltung deinstalliert werden soll.  
