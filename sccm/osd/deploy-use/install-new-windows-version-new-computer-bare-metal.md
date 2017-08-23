---
title: "Installieren von Windows auf einem neuen Computer – Configuration Manager | Microsoft-Dokumentation"
description: "Verwenden Sie Configuration Manager, um mithilfe von PXE, OEM oder einem eigenständigen Medium ein Betriebssystem auf einem neuen Computer (Bare-Metal-Computer) zu installieren."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
caps.latest.revision: "8"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 584dad7d8b05a2da9f7a66b73028ae99ff1a594f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-system-center-configuration-manager"></a>Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal) mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält die allgemeinen Schritte für System Center Configuration Manager, um ein Betriebssystem auf einem neuen Computer zu installieren. In diesem Szenario können Sie aus vielen unterschiedlichen Bereitstellungsmethoden auswählen, z. B. PXE, OEM oder eigenständige Medien. Wenn Sie nicht sicher sind, ob dies das richtige Szenario der Betriebssystembereitstellung für Sie ist, ziehen Sie [Szenarien für die Bereitstellung von Unternehmensbetriebssystemen](scenarios-to-deploy-enterprise-operating-systems.md) zurate.  

Verwenden Sie die folgenden Abschnitte, um einen vorhandenen Computer mit einer neuen Version von Windows zu aktualisieren.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Planen und Implementieren von Anforderungen an die Infrastruktur**  

     Vor der Bereitstellung von Betriebssystemen müssen verschiedene Anforderungen an die Infrastruktur erfüllt sein, z. B. Windows ADK, Windows Deployment Services (WDS), unterstützte Festplattenkonfigurationen usw. Weitere Informationen finden Sie unter [Infrastructure requirements for operating system deployment (Anforderungen an die Infrastruktur für die Betriebssystembereitstellung)](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

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

##  <a name="BKMK_Deploy"></a> Bereitstellen  

-   Verwenden Sie eine der folgenden Bereitstellungsmethoden, um das Betriebssystem bereitzustellen:  

    -   [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Verwenden eigenständiger Medien zum Bereitstellen von Windows ohne Verwendung des Netzwerks](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Verwenden startbarer Medien zum Bereitstellen von Windows über das Netzwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Überwachen der Tasksequenzbereitstellung**  

     Weitere Informationen zum Überwachen der Tasksequenzbereitstellung zum Installieren des Betriebssystems finden Sie unter [Überwachen von Betriebssystembereitstellungen](monitor-operating-system-deployments.md).  
