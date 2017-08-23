---
title: "Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk | Microsoft-Dokumentation"
description: "Verwenden Sie Multicast in Ihrer System Center Configuration Manager-Umgebung, damit mehrere Computer gleichzeitig das Betriebssystemimage herunterladen können."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 55266696aa7340fddda3a57ff90e20222ff665a5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Multicast ist eine Netzwerkoptimierungsmethode, die Sie in Ihrer System Center Configuration Manager-Umgebung verwenden können, wenn voraussichtlich mehrere Clients das gleiche Betriebssystemimage gleichzeitig herunterladen. In diesem Fall wird das Betriebssystemabbild vom Verteilungspunkt mithilfe von Multicast übertragen und kann von mehreren Computern gleichzeitig heruntergeladen werden, anstatt dass vom Verteilungspunkt über jeweils eine separate Verbindung Kopien der Daten an jeden Client gesendet werden.  

 Sie können in den folgenden Betriebssystembereitstellungsszenarien die Betriebssysteme mithilfe von Multicasting über das Netzwerk bereitstellen:  

-   [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

 Führen Sie die Schritte in einem der Szenarien für die Betriebssystembereitstellung aus, und verwenden Sie dann die folgenden Abschnitte, um Multicast zu unterstützen.  

##  <a name="BKMK_Configure"></a> Konfigurieren eines Verteilungspunkts zur Unterstützung von Multicast  
 Zum Verwenden von Multicast zum Bereitstellen von Betriebssystemen müssen Sie einen Verteilungspunkt konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Verteilungspunkten für die Multicastunterstützung](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Vorbereiten eines Betriebssystemabbilds für Multicastbereitstellungen  
 Informationen zum Konfigurieren des Pakets mit dem Betriebssystemimage zur Unterstützung von Multicast finden Sie unter [Vorbereiten des Betriebssystemimages für Multicastbereitstellungen](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Bereitstellen der Tasksequenz  
 Stellen Sie das Betriebssystem in einer Zielsammlung bereit. Weitere Informationen finden Sie unter [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
