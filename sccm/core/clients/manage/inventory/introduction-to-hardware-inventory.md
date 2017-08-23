---
title: "Hardwareinventur – Configuration Manager | Microsoft-Dokumentation"
description: "Erhalten Sie eine Einführung in die Hardwareinventur in System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: c64f0b42bff25e8e91cf9101d6fbb538634eab15
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Einführung in die Hardwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sammeln Sie mit der Hardwareinventur in System Center Configuration Manager Informationen zur Hardwarekonfiguration der Clientgeräte in Ihrer Organisation. Zum Sammeln der Hardwareinventur muss in den Clienteinstellungen die Einstellung **Hardwareinventur auf Clients aktivieren** aktiviert sein.  

 Nachdem die Hardwareinventur aktiviert und ein Hardwareinventurzyklus vom Client ausgeführt wurde, sendet der Client die Informationen an einen Verwaltungspunkt am Standort des Clients. Der Verwaltungspunkt leitet diese Inventurinformationen an den Configuration Manager-Standortserver weiter, auf dem die Inventurinformationen in der Standortdatenbank gespeichert werden. Die Hardwareinventur wird auf Clients gemäß dem Zeitplan ausgeführt, den Sie in den Clienteinstellungen festlegen.  

 Sie können die von Configuration Manager gesammelten Hardwareinventurdaten unter Zuhilfenahme mehrerer Methoden anzeigen. Dazu gehören die folgenden:  

-   [Erstellen von Abfragen, bei denen Geräte zurückgegeben werden, die auf einer bestimmten Hardwarekonfiguration basieren](../../../../core/servers/manage/queries-technical-reference.md)  

-   [Erstellen von abfragebasierten Sammlungen, die auf einer bestimmten Hardwarekonfiguration basieren](../../../../core/clients/manage/collections/introduction-to-collections.md) Mitgliedschaften abfragebasierter Sammlungen werden automatisch nach einem Zeitplan aktualisiert. Für zahlreiche Tasks, zu denen auch die Softwarebereitstellung zählt, können Sie Sammlungen verwenden. .  

-   [Ausführen von Berichten, in denen spezifische Details zu Hardwarekonfigurationen in Ihrer Organisation angezeigt werden](../../../../core/servers/manage/reporting.md)   

-   Anzeigen von detaillierten Hardwareinventurinformationen, die von Clientgeräten gesammelt wurden, im [Ressourcen-Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).   

 Beim Ausführen der Hardwareinventur auf einem Clientgerät wird vom Client als Erstes immer das vollständige Inventar als Inventurdaten zurückgegeben. Alle nachfolgenden Inventurinformationen stellen lediglich das Deltainventar dar. Vom Standortserver werden die Deltainventurinformationen in der Reihenfolge verarbeitet, in der sie empfangen wurden. Falls Deltainformationen für einen Client fehlen, werden zusätzliche Deltainformationen vom Standortserver zurückgewiesen, und der Client erhält die Anweisung für einen vollständigen Inventurzyklus.  

 Configuration Manager bietet eingeschränkte Unterstützung für Dual-Boot-Computer. Eine Ermittlung von Dual-Boot-Computern ist zwar in Configuration Manager möglich, es werden jedoch nur die Inventurinformationen von dem Betriebssystem zurückgegeben, das zum Zeitpunkt der Ausführung des Inventurzyklus aktiv war.  

> [!NOTE]  
>  Informationen zur Verwendung der Hardwareinventur mit Clients, auf denen Linux und UNIX ausgeführt wird, finden Sie unter [Hardwareinventur für Linux und UNIX in System Center Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Erweitern der Konfigurations-Manager-Hardwareinventur  
 Neben der integrierten Hardwareinventur in Configuration Manager können Sie die Hardwareinventur auch durch eine der folgenden Methoden erweitern, um zusätzliche Informationen zu sammeln:  

- Sie können Inventurklassen für die Hardwareinventur über die Configuration Manager-Konsole aktivieren, deaktivieren, hinzufügen und entfernen.|  
- Verwenden Sie NOIDMIF-Dateien zum Sammeln von Informationen zu Clientgeräten, die nicht von Configuration Manager inventarisiert werden können. Möglicherweise möchten z. B. Gerät Asset Informationen sammeln, die nur als Etikett auf dem Gerät vorhanden ist. NOIDMIF-Inventur wird automatisch das Clientgerät, dem er entnommen wurde zugeordnet.  
- Verwenden Sie IDMIF-Dateien zum Sammeln von Informationen zu Assets, die keinem Configuration Manager-Client zugeordnet sind, z.B. Projektoren, Fotokopierer und Netzwerkdrucker.  

 Weitere Informationen zur Verwendung dieser Methoden zum Erweitern der Hardwareinventur für Configuration Manager finden Sie unter [Konfigurieren der Hardwareinventur in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
