---
title: Softwareinventur | Microsoft-Dokumentation
description: "Erhalten Sie eine Einführung in die Softwareinventur in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 969f2d28649853ddc95860fe72597d6d2c9a94e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Einführung in die Softwareinventur in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie verwenden die Softwareinventur, um Informationen zu Dateien auf Clientgeräten zu sammeln. Ferner können bei der Softwareinventur Dateien von Clientgeräten gesammelt und auf dem Standortserver gespeichert werden. Das Softwareinventar wird gesammelt, wenn in den Clienteinstellungen die Einstellung **Softwareinventur auf Clients aktivieren** aktiviert ist. Dort können Sie auch die Ausführung planen.  

Nachdem die Softwareinventur aktiviert und ein Softwareinventurzyklus von den Clients ausgeführt wurde, werden die vom einzelnen Client gesammelten Informationen an einen Verwaltungspunkt am Standort des Clients gesendet. Der Verwaltungspunkt leitet diese Inventurinformationen dann an den Configuration Manager-Standortserver weiter, auf dem die Informationen in der Standortdatenbank gespeichert werden.   

 Sie können die Softwareinventurdaten auf verschiedene Weise anzeigen:  

-   [Erstellen von Abfragen](../../../../core/servers/manage/queries-technical-reference.md), die Geräte mit angegebenen Dateien zurückgeben   

-   Erstellen von [abfragebasierten Sammlungen](../../../../core/clients/manage/collections/introduction-to-collections.md), die Geräte mit angegebenen Dateien enthalten   

-   [Ausführen von Berichten](../../../../core/servers/manage/reporting.md), die Details zu Dateien auf Geräten bereitstellen

-   Verwenden von [Ressourcen-Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md), um detaillierte Informationen zu den Dateien anzuzeigen, die von Clientgeräten inventarisiert und gesammelt wurden   

 Beim Ausführen der Softwareinventur auf einem Clientgerät enthält der erste Bericht ein vollständiges Inventar. Alle nachfolgenden Berichte enthalten lediglich Deltainventurinformationen. Vom Standortserver werden die Deltainformationen in der empfangenen Reihenfolge verarbeitet. Falls Deltainformationen für einen Client fehlen, werden weitere Deltainformationen vom Standortserver zurückgewiesen, und der Client erhält die Anweisung für eine vollständige Inventur.  

 Eine Ermittlung von Dual-Boot-Computern ist in Configuration Manager zwar möglich, es werden jedoch nur die Inventurinformationen von dem Betriebssystem zurückgegeben, das zum Zeitpunkt der Inventur aktiv war.  

**Mobile Geräte:** Unter [software inventory for mobile devices enrolled with Microsoft Intune (Softwareinventur für mobile Geräte, die mit Microsoft Intune registriert sind)](../../../../mdm/deploy-use/software-inventory-mobile-devices.md) finden Sie Informationen zum Sammeln von Inventur für auf mobilen Geräten installierte Apps.
