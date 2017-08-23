---
title: "Firewalls und Domänen | Microsoft-Dokumentation"
description: "Richten Sie Firewalls, Ports und Domänen zur Vorbereitung der System Center Configuration Manager-Kommunikation ein."
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4a2a8f96a900a2c4959ae3ff59232771ece95991
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Einrichten von Firewalls, Ports und Domänen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Planen Sie die Einrichtung von Infrastrukturkomponenten, z.B. Firewalls, um Ihr Netzwerk für die Unterstützung von System Center Configuration Manager vorzubereiten, damit die Kommunikation mit Configuration Manager gewährleistet ist.  

|Überlegung|Details|  
|-------------------|-------------|  
|Von verschiedenen Configuration Manager-Funktionen verwendete **Ports und Protokolle**. Einige Ports sind erforderlich, und andere **Domänen und Dienste** können angepasst werden.|Für einen Großteil der Configuration Manager-Kommunikation werden allgemeine Ports wie z.B. 80 für die HTTP- oder 443 für die HTTPS-Kommunikation verwendet. Allerdings [unterstützen einige Standortsystemrollen die Verwendung benutzerdefinierter Websites](/sccm/core/plan-design/network/websites-for-site-system-servers) und Ports.<br /><br /> Identifizieren Sie **vor der Bereitstellung von Configuration Manager** die Ports, die Sie verwenden möchten, und richten Sie die Firewalls entsprechend ein.<br /><br /> **Wenn Sie nach der Installation von Configuration Manager einen Port ändern müssen**, vergessen Sie nicht das Aktualisieren von Firewalls für Geräte und Netzwerk, und ändern Sie außerdem die Konfiguration des Ports in Configuration Manager.<br /><br /> Weitere Informationen finden Sie unter: </br>- [Konfigurieren von Clientkommunikationsports](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [In Configuration Manager verwendete Ports](../../../core/plan-design/hierarchy/ports.md) </br>- [Internetzugriffsanforderungen für den Dienstverbindungspunkt](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Domänen und Dienste**, die möglicherweise von Standortservern und Clients verwendet werden müssen.|Für Configuration Manager-Funktionen kann es erforderlich sein, dass Standortserver und Clients auf bestimmte Dienste und Domänen im Internet zugreifen können, wie z.B. „Windowsudpate.microsoft.com“ oder den Microsoft Intune-Dienst.<br /><br /> Wenn Sie Microsoft Intune zum Verwalten mobiler Geräte verwenden, müssen Sie auch den Zugriff auf [von Intune benötigte Ports und Domänen](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune) einrichten.|  
|**Proxyserver** für Standortsystemserver und die Clientkommunikation. Sie können separate Proxyserver für verschiedene Standortsystemserver und Clients angeben.|Da diese Konfigurationen bei der Installation einer Standortsystemrolle oder eines Clients erfolgen, müssen Sie lediglich mit den Proxyserverkonfigurationen vertraut sein, wenn Sie später Standortsystemrollen und Clients konfigurieren.<br /><br /> Wenn Sie nicht sicher sind, ob Sie in Ihrer Bereitstellung Proxyserver verwenden müssen, konsultieren Sie [Unterstützung von Proxyservern in System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md), um sich über Standortsystemrollen und Clientaktionen zu informieren, die einen Proxyserver verwenden können.|   
|  
