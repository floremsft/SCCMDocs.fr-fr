---
title: Aktualisieren von Windows auf die neueste Version | Microsoft-Dokumentation
description: "Erfahren Sie mehr über das Verwenden von Configuration Manager, um ein Upgrade eines Betriebssystems von Windows 7 oder höher auf Windows 10 durchzuführen."
ms.custom: na
ms.date: 02/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 026d61113a918e43ac4395ef092b1931f33f16d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Aktualisieren von Windows auf die neueste Version mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält die Schritte in System Center Configuration Manager, um auf einem Zielcomputer ein Betriebssystemupgrade von Windows 7 oder höher auf Windows 10 oder von Windows Server 2012 auf Windows Server 2016 durchzuführen. Sie können aus unterschiedlichen Bereitstellungsmethoden auswählen, z. B. eigenständige Medien oder Softwarecenter. Szenario für das direkte Upgrade:  

-   Aktualisiert das Betriebssystem auf Computern, auf denen derzeit eines der folgenden Betriebssysteme ausgeführt wird:
    - Windows 7, Windows 8 oder Windows 8.1. Sie können auch Upgrades von Windows 10-Build zu Windows 10-Build durchführen. Beispielsweise können Sie Windows 10 RTM auf Windows 10, Version 1511, aktualisieren.  
    - Windows Server 2012. Sie können auch Build-zu-Build-Upgrades von Windows 2016 durchführen. Details zu den unterstützten Upgradepfaden finden Sie unter [Unterstützte Upgradepfade](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Behält die Anwendungen, Einstellungen und Benutzerdaten auf dem Computer bei.  

-   Weist keine externen Abhängigkeiten auf, wie z. B. das Windows ADK.  

-   Ist schneller und stabiler als herkömmliche Betriebssystembereitstellungen.  

 Nutzen Sie die folgenden Abschnitte, um mithilfe einer Tasksequenz Betriebssysteme über das Netzwerk bereitzustellen.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Überprüfen Sie die für die Tasksequenz zum Durchführen eines Betriebssystemupgrades geltenden Einschränkungen.**  

     Überprüfen Sie die folgenden, für die Tasksequenz zum Durchführen eines Betriebssystemupgrades geltenden Anforderungen und Einschränkungen, und stellen Sie sicher, dass die Tasksequenz Ihren Anforderungen entspricht:  

    -   Fügen Sie nur Tasksequenzschritte hinzu, die sich auf die Kernaufgaben der Betriebssystembereitstellung und der Konfiguration der Computer nach der Installation des Images beziehen. Dazu zählen Schritte, die Pakete, Anwendungen oder Updates installieren, und Schritte, die Befehlszeilen oder PowerShell ausführen bzw. dynamische Variablen festlegen.  

    -   Überprüfen Sie vor dem Bereitstellen der Upgradetasksequenz die auf den Computern installierten Treiber und Anwendungen, um sicherzustellen, dass sie mit Windows 10 kompatibel sind.  

    -   Die folgenden Tasks sind mit dem direkten Upgrade nicht kompatibel und erfordern herkömmliche Betriebssystembereitstellungen:  

        -   Ändern der Domänenmitgliedschaft der Computer oder Aktualisieren lokaler Administratoren.  

        -   Implementieren einer grundlegenden Änderung auf dem Computer, z. B. die Datenträgerpartitionierung, einen Architekturwechsel von x86 zu x64, die Implementierung von UEFI oder das Ändern der Sprache des zugrunde liegenden Betriebssystems.  

        -   Sie haben benutzerdefinierte Anforderungen, z.B. die Verwendung eines benutzerdefinierten Basisimages mit Festplattenverschlüsselung eines <sup>Drittanbieters</sup>, oder Sie müssen WinPE-Offlinevorgänge durchführen.  

-   **Planen und Implementieren von Anforderungen an die Infrastruktur**  

     Die einzige Voraussetzung für das Upgradeszenario ist, dass ein Verteilungspunkt für das Betriebssystem-Aktualisierungspaket und alle anderen in der Tasksequenz enthaltenen Pakete verfügbar ist. Weitere Informationen finden Sie unter [Installieren oder Modifizieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

##  <a name="BKMK_Configure"></a> Konfigurieren  

1.  **Vorbereiten des Betriebssystem-Upgradepakets**  

     Das Windows 10-Upgradepaket enthält die erforderlichen Quelldateien zum Aktualisieren des Betriebssystems auf dem Zielcomputer. Das Upgradepaket muss die gleiche Edition, Architektur und Sprache wie die Clients aufweisen, die aktualisiert werden sollen.  Weitere Informationen finden Sie unter [Verwalten von Betriebssystem-Upgradepaketen](../get-started/manage-operating-system-upgrade-packages.md).  

2.  **Erstellen einer Tasksequenz zum Durchführen eines Betriebssystemupgrades**  

     Verwenden Sie die Schritte unter [Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](create-a-task-sequence-to-upgrade-an-operating-system.md), um das Upgrade des Betriebssystems zu automatisieren.  

    > [!IMPORTANT]
    > Wenn Sie eigenständige Medien verwenden, müssen Sie ein Startimage in die Tasksequenz einschließen, damit die Medien im Tasksequenzmedien-Assistenten zur Verfügung stehen.

    > [!NOTE]  
    > In der Regel verwenden Sie die Schritte unter [Erstellen einer Tasksequenz zum Durchführen eines Upgrades für ein Betriebssystem](create-a-task-sequence-to-upgrade-an-operating-system.md), um eine Tasksequenz zu erstellen, mit der das Upgrade eines Betriebssystems auf Windows 10 durchgeführt wird. Die Tasksequenz enthält den Schritt „Betriebssystem aktualisieren“ sowie weitere empfohlene Schritte und Gruppen für den End-to-End-Aktualisierungsprozess. Sie können jedoch eine benutzerdefinierte Tasksequenz erstellen und den Tasksequenzschritt [Betriebssystem aktualisieren](../understand/task-sequence-steps.md#BKMK_UpgradeOS) zum Aktualisieren des Betriebssystems hinzufügen. Dies ist der einzige Schritt, der zum Aktualisieren des Betriebssystems auf Windows 10 erforderlich ist. Wenn Sie diese Methode auswählen, fügen Sie nach dem Schritt „Betriebssystem aktualisieren“ außerdem den Schritt [Computer neu starten](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) hinzu, um das Upgrade abzuschließen. Stellen Sie sicher, dass die Einstellung **Aktuell installiertes Standardbetriebssystem** aktiviert ist, um den Computer mit dem installierten Betriebssystem und nicht mit Windows PE neu zu starten.  

##  <a name="BKMK_Deploy"></a> Bereitstellen  

-   Verwenden Sie eine der folgenden Bereitstellungsmethoden, um das Betriebssystem bereitzustellen:  

    -   [Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Überwachen der Tasksequenzbereitstellung**  

     Weitere Informationen zum Überwachen der Tasksequenzbereitstellung zum Durchführen eines Betriebssystemupgrades finden Sie unter [Überwachen von Betriebssystembereitstellungen](monitor-operating-system-deployments.md).  
