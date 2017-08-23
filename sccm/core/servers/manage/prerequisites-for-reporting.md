---
title: "Voraussetzungen für die Berichterstattung | Microsoft-Dokumentation"
description: "Hier finden Sie Informationen zu verschiedenen Abhängigkeiten, die sich auf die Nutzung der Berichterstellung in System Center Configuration Manager auswirken."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2e624eb2ea061a4eb7d92365410fada335640224
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Voraussetzungen für die Berichterstattung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die Berichterstellung in System Center Configuration Manager hat externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  
 In der folgenden Tabelle werden die externen Abhängigkeiten der Berichterstattung aufgelistet.  

|Voraussetzung|Weitere Informationen|  
|------------------|----------------------|  
|SQL Server Reporting Services|SQL Server Reporting Services muss zunächst installiert und konfiguriert werden, damit die Berichterstellung in Configuration Manager verwendet werden kann.<br /><br /> Informationen zum Planen und Bereitstellen von Reporting Services in Ihrer Umgebung finden Sie im Abschnitt [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) in der SQL Server 2008-Onlinedokumentation.|  
|Abhängigkeiten der Standortsystemrollen bei Computern, auf denen der Reporting Services-Punkt ausgeführt wird|[Unterstützte Konfigurationen für System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Interne Abhängigkeiten von Configuration Manager  
 In der folgenden Tabelle werden die Abhängigkeiten der Berichterstellung in Configuration Manager aufgelistet.  

|Voraussetzung|Weitere Informationen|  
|------------------|----------------------|  
|Reporting Services-Punkt|Die Standortsystemrolle des Reporting Services-Punkts muss konfiguriert werden, damit die Berichterstellung in Configuration Manager verwendet werden kann. Weitere Informationen zum Installieren und Konfigurieren eines Reporting Services-Punkts finden Sie unter [Configuring reporting in System Center Configuration Manager (Konfigurieren der Berichterstellung in System Center Configuration Manager)](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Unterstützte SQL Server-Versionen für den Reporting Services-Punkt  
 Die Reporting Services-Datenbank kann entweder auf der Standardinstanz oder auf einer benannten Instanz einer 64-Bit-SQL Server-Installation installiert werden. Die SQL Server-Instanz kann sich auf dem gleichen Computer wie der Standortsystemserver oder auf einem Remotecomputer befinden.  

 Die folgende Tabelle enthält eine Aufstellung der SQL Server-Versionen, die vom Reporting Services-Punkt unterstützt werden.  

|SQL Server-Version|Reporting Services-Punkt|  
|------------------------|------------------------------|  
|SQL Server 2008 SP2 (mindestens mit kumulativem Update 9)<br /><br /> - Standard<br />- Enterprise<br />- Datacenter|Ja|  
|SQL Server 2008 SP3 (mindestens mit kumulativem Update 4)<br /><br /> - Standard<br />- Enterprise<br />- Datacenter|Ja|  
|SQL Server 2008 R2 mit SP1 (mindestens mit kumulativem Update 6)<br /><br /> - Standard<br />- Enterprise<br />- Datacenter|Ja|  
|SQL Server 2008 R2 mit SP2<br /><br /> - Standard<br />- Enterprise<br />- Datacenter|Ja|  
|SQL Server Express 2008 R2 mit SP1 (mindestens mit kumulativem Update 4)|Nicht unterstützt|  
|SQL Server Express 2008 R2 mit SP2|Nicht unterstützt|  
|SQL Server 2012 (mindestens mit kumulativem Update 2)<br /><br /> - Standard<br />- Enterprise|Ja|  
|SQL Server 2012 mit SP1 (ohne kumulativem Update)<br /><br /> - Standard<br />- Enterprise|Ja|  
|SQL Server 2014<br /><br /> - Standard<br />- Enterprise|Ja|
|SQL Server 2016<br /><br /> - Standard<br />- Enterprise|Ja|
|SQL Server 2016 mit SP1<br /><br /> - Standard<br />- Enterprise|Ja|
## <a name="next-steps"></a>Nächste Schritte
[Vorgänge und Wartungstasks für die Berichterstellung](operations-and-maintenance-for-reporting.md)
