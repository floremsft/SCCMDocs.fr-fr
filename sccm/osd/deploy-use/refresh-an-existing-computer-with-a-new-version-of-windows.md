---
title: Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows | Microsoft-Dokumentation
description: "Zum Partitionieren und Formatieren (Zurücksetzen) eines vorhandenen Computers und zum Installieren eines neuen Betriebssystems auf dem Computer können verschiedene Methoden in Configuration Manager verwendet werden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
caps.latest.revision: "7"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b247cbb68ed63a8eb99715a248686d68a28c53e2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows-using-system-center-configuration-manager"></a>Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows unter Verwendung von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält die allgemeinen Schritte in System Center Configuration Manager zum Partitionieren und Formatieren (Zurücksetzen) eines vorhandenen Computers und zum Installieren eines neuen Betriebssystems auf dem Computer. In diesem Szenario können Sie aus vielen unterschiedlichen Bereitstellungsmethoden auswählen, z. B. PXE, startbare Medien oder Softwarecenter. Sie können auch einen Zustandsmigrationspunkt installieren, um Einstellungen zu speichern, und diese Einstellungen dann nach der Installation im neuen Betriebssystem wiederherstellen. Wenn Sie nicht sicher sind, ob dies das richtige Szenario der Betriebssystembereitstellung für Sie ist, ziehen Sie [Scenarios to deploy enterprise operating systems with System Center Configuration Manager (Szenarios für die Bereitstellung von Unternehmensbetriebssystemen)](scenarios-to-deploy-enterprise-operating-systems.md) zurate.  

 Verwenden Sie die folgenden Abschnitte, um einen vorhandenen Computer mit einer neuen Version von Windows zu aktualisieren.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Planen und Implementieren von Anforderungen an die Infrastruktur**  

     Vor der Bereitstellung von Betriebssystemen müssen verschiedene Anforderungen an die Infrastruktur erfüllt sein, z. B. Windows ADK, User State Migration Tool (USMT), Windows Deployment Services (WDS) unterstützte Festplattenkonfigurationen usw. Weitere Informationen finden Sie unter [Infrastructure requirements for operating system deployment (Anforderungen an die Infrastruktur für die Betriebssystembereitstellung)](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Installieren eines Zustandsmigrationspunkts (nur erforderlich, wenn Sie Einstellungen übertragen)**  

     Wenn Sie Einstellungen eines vorhandenen Computers erfassen und dann im neuen Betriebssystem wiederherstellen möchten, müssen Sie einen Zustandsmigrationspunkt installieren. Weitere Informationen finden Sie unter [Statusmigrationspunkt](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_Configure"></a> Konfigurieren  

1.  **Vorbereiten eines Startabbilds**  

     Ein Startabbild startet einen Computer in einer Windows PE-Umgebung (ein minimales Betriebssystem mit begrenzten Komponenten und Diensten), die dann ein vollständiges Windows-Betriebssystem auf dem Computer installieren kann.   Wenn Sie Betriebssysteme bereitstellen, müssen Sie das zu verwendende Startimage auswählen und das Image auf einen Verteilungspunkt verteilen. Bereiten Sie das Startimage unter Berücksichtigung folgender Informationen vor:  

    -   Weitere Informationen zu Startimages finden Sie unter [Manage boot images (Verwalten von Startimages)](../get-started/manage-boot-images.md).  

    -   Weitere Informationen zum Anpassen eines Startimages [Anpassen von Startimages mit System Center Configuration Manager](../get-started/customize-boot-images.md).  

    -   Verteilen Sie das Startabbild an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

2.  **Vorbereiten eines Betriebssystemabbilds**  

     Das Betriebssystemimage enthält die erforderlichen Dateien zum Installieren des Betriebssystems auf dem Zielcomputer. Bereiten Sie das Betriebssystemimage unter Berücksichtigung folgender Informationen vor:  

    -   Weitere Informationen zum Erstellen eines Betriebssystemimages finden Sie unter [Manage operating system images (Verwalten von Betriebssystemimages)](../get-started/manage-operating-system-images.md).  

    -   Verteilen Sie die Betriebssystemimages an Verteilungspunkte. Weitere Informationen finden Sie unter [Distribute content (Verteilen von Inhalt)](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

3.  **Erstellen einer Tasksequenz zum Bereitstellen von Betriebssystemen über das Netzwerk**  

     Verwenden Sie eine Tasksequenz, um die Installation des Betriebssystems über das Netzwerk zu automatisieren. Führen Sie die Schritte im Artikel [Erstellen einer Tasksequenz zum Installieren eines Betriebssystems](create-a-task-sequence-to-install-an-operating-system.md) aus, um die Tasksequenz zum Bereitstellen des Betriebssystems zu erstellen. Abhängig von der gewählten Bereitstellungsmethode sind möglicherweise zusätzliche Aspekte zur Tasksequenz zu berücksichtigen.  

    > [!NOTE]  
    >  In diesem Szenario werden die Festplatten auf dem Computer durch die Tasksequenz formatiert und partitioniert. Verwenden Sie den Zustandsmigrationspunkt, um Benutzereinstellungen zu erfassen, und wählen Sie auf der Seite **Zustandsmigration** des Assistenten zum Erstellen einer Tasksequenz die Option **Benutzereinstellungen und Dateien auf einem Zustandsmigrationspunkt speichern** aus. Wenn Sie die Benutzereinstellungen und Dateien lokal speichern, gehen diese beim Formatieren der Festplatte verloren und können von Configuration Manager nicht wiederhergestellt werden. Weitere Informationen finden Sie unter [Verwalten des Benutzerstatus](../get-started/manage-user-state.md).  

##  <a name="BKMK_Deploy"></a> Bereitstellen  

-   Verwenden Sie eine der folgenden Bereitstellungsmethoden, um das Betriebssystem bereitzustellen:  

    -   [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Verwenden des Softwarecenters zum Bereitstellen von Windows über das Netzwerk](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Überwachen der Tasksequenzbereitstellung**  

     Weitere Informationen zum Überwachen der Tasksequenzbereitstellung zum Installieren des Betriebssystems finden Sie unter [Überwachen von Betriebssystembereitstellungen](monitor-operating-system-deployments.md).  
