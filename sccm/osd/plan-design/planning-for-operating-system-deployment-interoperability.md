---
title: "Planen der Interoperabilität der Betriebssystembereitstellung | Microsoft-Dokumentation"
description: "Grundlegendes zu Interoperabilitätsproblemen, wenn verschiedene System Center Configuration Manager-Standorte in einer einzelnen Hierarchie verschiedene Versionen verwenden."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
caps.latest.revision: "10"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 50a4b75b8c8c1cb6f7a8e696abad285f99080fcd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>Planen der Interoperabilität der Betriebssystembereitstellung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn verschiedene System Center Configuration Manager-Standorte in einer einzelnen Hierarchie verschiedene Versionen verwenden, sind einige Configuration Manager-Funktionen nicht verfügbar. Normalerweise sind Funktionen aus neueren Configuration Manager-Versionen für Standorte oder Clients mit einer niedrigeren Version nicht verfügbar. Weitere Informationen finden Sie unter [Interoperability between different versions of System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Berücksichtigen Sie Folgendes beim Upgrade des Standorts der obersten Ebene in Ihrer Hierarchie, wenn andere Standorte in Ihrer Hierarchie Configuration Manager in einer niedrigeren Version ausführen:  

-   Clientinstallationspaket  

    -   Für die Quelle des Standardclient-Installationspakets wird automatisch ein Upgrade durchgeführt, und alle Verteilungspunkte in der Hierarchie werden mit dem neuen Clientinstallationspaket aktualisiert, auch Verteilungspunkte an Standorten der Hierarchie, die eine niedrigere Version aufweisen.  

    -   Clients, auf denen die neue Version ausgeführt wird, können keinen Standorten zugeordnet werden, für die noch kein Upgrade auf die neue Version durchgeführt wurde. Die Zuordnung wird am Verwaltungspunkt gesperrt.  

-   Startabbilder  

    -   Wenn Sie für den Standort der obersten Ebene ein Upgrade auf die neueste Version von Configuration Manager durchführen, werden die Standardstartimages (x86 und x64) automatisch auf Windows ADK für Windows 10-basierte Startimages aktualisiert, die Windows PE 10 verwenden. Die Dateien, die den Standardstartimages zugeordnet sind, werden auf die neueste Configuration Manager-Version der Dateien aktualisiert. Benutzerdefinierte Startimages werden nicht automatisch aktualisiert. Sie müssen benutzerdefinierte Startimages, die ältere Versionen von Windows PE enthalten, manuell aktualisieren.  

    -   Vermeiden Sie die Verwendung eines dynamischen Mediums, wenn Ihre Standorthierarchie Standorte mit unterschiedlichen Versionen von Configuration Manager enthält. Verwenden Sie stattdessen ein standortbasiertes Medium, um einen bestimmten Verwaltungspunkt zu kontaktieren, bis alle Standorte auf dieselbe Version von Configuration Manager aktualisiert wurden.  

    -   Stellen Sie sicher, dass die neuesten Configuration Manager-Startimages die gewünschten Anpassungen enthalten, und aktualisieren Sie anschließend alle Verteilungspunkte an den Standorten mit der neuesten Version von Configuration Manager mit den neuen Startimages.  

-   Migrationsprogramm für den Benutzerzustand (USMT)  

    -   Wenn Sie den Standort auf oberster Ebene auf die neueste Version von Configuration Manager aktualisieren, wird das Standardpaket von USMT automatisch ebenfalls auf die neueste Version aktualisiert. Benutzerdefinierte USMT-Pakete werden nicht automatisch aktualisiert. Sie müssen diese Pakete manuell aktualisieren.  

-   Neue Tasksequenzschritte  

    -   Mit neuen Versionen von Configuration Manager werden regelmäßig neue Tasksequenzschritte eingeführt. Wenn Sie älteren Clients eine Tasksequenz mit einem neuen Schritt bereitstellen, schlägt der Tasksequenzschritt fehl. Bevor Sie eine Tasksequenz mit einem neuen Schritt bereitstellen, vergewissern Sie sich, dass die Clients in der Zielsammlung auf die neue Version aktualisiert wurden.  

-   Medien für die Betriebssystembereitstellung  

    -   Alle Medien (startbare, erfasste, vorab bereitgestellte und eigenständige) müssen mit dem neuen Configuration Manager-Clientpaket aktualisiert werden, wenn der Standort auf eine neue Version aktualisiert wird.  

-   Drittanbietererweiterungen für die Betriebssystembereitstellung  

    -   Wenn Sie über Erweiterungen zur Betriebssystembereitstellung von Drittanbietern verfügen und in einer gemischten Hierarchie arbeiten, d.h. mit verschiedenen Versionen von Configuration Manager-Standorten oder Configuration Manager-Clients, können Probleme mit der Erweiterung auftreten.  

 Während Sie aktive Upgrades für die Standorte in Ihrer Hierarchie durchführen, sollten Sie folgende Abschnitte zum Bereitstellen des Betriebssystems beachten.  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Neueste Version von Configuration Manager auf Standorten in einer gemischten Hierarchie  
 Wenn Sie für einen Standort ein Upgrade auf die neueste Version von Configuration Manager durchführen, starten Tasksequenzen, die sich auf das Standard-Clientinstallationspaket beziehen, automatisch die Bereitstellung der neuesten Clientversion von Configuration Manager. Tasksequenzen, die sich auf ein benutzerdefiniertes Clientinstallationspaket beziehen, stellen weiterhin die Version des Clients bereit, die in diesem benutzerdefinierten Paket enthalten ist (wahrscheinlich eine frühere Configuration Manager-Clientversion), und müssen aktualisiert werden, um Fehler bei der Tasksequenzbereitstellung zu vermeiden. Bei einer Tasksequenz, die für die Verwendung eines benutzerdefinierten Clientinstallationspakets konfiguriert ist, müssen Sie den Tasksequenzschritt aktualisieren, sodass die neueste Configuration Manager-Version des Clientinstallationspakets verwendet wird, oder das benutzerdefinierte Paket für die Verwendung der neuesten Configuration Manager-Clientinstallationsquelle aktualisieren.  

> [!IMPORTANT]  
>  Stellen Sie für Clients an einem älteren Configuration Manager-Standort keine Tasksequenz bereit, die sich auf das neueste Configuration Manager-Clientinstallationspaket bezieht. Wenn Clients, die einem älteren Configuration Manager-Standort zugewiesen sind, auf die neueste Configuration Manager-Clientversion aktualisiert werden, blockiert Configuration Manager die Zuweisung zum älteren Configuration Manager-Standort. Dadurch ist der Client keinem Standort mehr zugeordnet und wird nicht verwaltet, bis Sie ihn manuell zum neuesten Configuration Manager-Standort zuordnen oder die ältere Configuration Manager-Version des Clients erneut auf dem Computer installieren.  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Ältere Versionen von Configuration Manager in einer gemischten Hierarchie  
 Wenn Sie für Ihren Standort der zentralen Verwaltung ein Upgrade auf die neueste Version von Configuration Manager durchgeführt haben, müssen Sie den folgenden Schritt ausführen, um sicherzustellen, dass die Tasksequenzen der Betriebssystembereitstellung, die Sie für Clients bereitstellen, die einem älteren (noch nicht auf die neueste Version von Configuration Manager aktualisierten) Configuration Manager-Standort zugeordnet sind, diese Clients nicht in einem unverwalteten Zustand zurücklassen.  

-   Erstellen Sie eine Tasksequenz, die Sie nur für die Bereitstellung auf Clients an einem Configuration Manager-Standort verwenden. Dafür erstellen Sie in der Regel eine Kopie einer Tasksequenz, die Sie zur Bereitstellung auf Clients an der neuesten Version des Configuration Manager-Standorts verwenden, und ändern die Tasksequenz anschließend so, dass sie auf Clients an einem älteren Configuration Manager-Standort bereitgestellt werden kann. Konfigurieren Sie die Tasksequenz anschließend so, dass sie auf ein benutzerdefiniertes Clientinstallationspaket verweist, das die ältere Configuration Manager-Clientinstallationsquelle verwendet. Wenn Sie nicht bereits über ein benutzerdefiniertes Clientinstallationspaket verfügen, das auf die ältere Configuration Manager-Clientinstallationsquelle verweist, müssen Sie manuell eines erstellen.  
