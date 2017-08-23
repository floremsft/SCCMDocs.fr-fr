---
title: Verwenden von Clouddiensten mit Configuration Manager | Microsoft-Dokumentation
description: "Bereitstellen von Cloudressourcen für System Center Configuration Manager zur Ergänzung Ihrer lokalen Infrastruktur."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 52f7c63d155d5c34f0f12e13020767dec1867dab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>Verwenden von Clouddiensten mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager unterstützt mehrere cloudbasierte Optionen. Diese können Ihre lokale Infrastruktur ergänzen und Ihnen helfen, Geschäftsprobleme wie die folgenden zu lösen:  

-   Verwalten von BYOD (mithilfe von Intune für die Verwaltung mobiler Geräte)  

-   Bereitstellen von Inhaltsressourcen für isolierte Clients oder Ressourcen im Intranet, und zwar außerhalb der Unternehmensfirewall (mithilfe cloudbasierter Verteilungspunkte)  

-   Horizontales Skalieren von Infrastruktur, wenn physische Hardware nicht verfügbar oder nicht logisch zur Unterstützung Ihrer Anforderungen platziert ist (mithilfe virtueller Microsoft Azure-Computer)  

Wenngleich die Bereitstellung von Cloudressourcen nicht vor dem Bereitstellen von Configuration Manager erfolgt, kann es nützlich sein, diese Möglichkeiten zu kennen, bevor die Planung des Hierarchieentwurfs zu weit voranschreitet. Durch die Verwendung von Cloudressourcen können Sie ggf. Zeit und Geld sparen, da Sie Geschäftsprobleme lösen können, die mit lokaler Infrastruktur nicht gelöst werden können.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Cloudbasierte Ressourcen, die Sie mit Configuration Manager verwenden können  
 Da jede Option andere Anforderungen hat, untersuchen Sie sie eingehender, um sich mit den besonderen Voraussetzungen, Einschränkungen und möglichen Zusatzkosten basierend auf der Nutzung vertraut zu machen.  

-   Informationen zu cloudbasierten Verteilungspunkten finden Sie unter [Installieren von cloudbasierten Verteilungspunkten](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   Weitere Informationen zu Azure finden Sie unter [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) in der MSDN Library.  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Virtuelle Azure-Computer (für cloudbasierte Infrastruktur)  
 Configuration Manager unterstützt das Verwenden von Computern, die in virtuellen Computern in Azure ausgeführt werden, genau wie lokale Computer, die innerhalb des physischen Unternehmensnetzwerks ausgeführt werden. Sie können virtuelle Microsoft Azure-Computer in den folgenden Szenarien nutzen:  

-   **Szenario 1:** Sie können Configuration Manager auf einem virtuellen Computer ausführen, und zum Verwalten von auf anderen virtuellen Computern installierten Clients verwenden.  

-   **Szenario 2:** Sie können Configuration Manager auf einem virtuellen Computer ausführen, und zum Verwalten von Clients verwenden, die nicht in Azure ausgeführt werden.  

-   **Szenario 3:** Sie können verschiedene Configuration Manager-Standortsystemrollen auf virtuellen Computern ausführen, während Sie andere Rollen im physischen Unternehmensnetzwerk (mit der entsprechenden Netzwerkkonnektivität für die Kommunikation) ausführen.  

Für die Installation von Configuration Manager in Azure gelten die gleichen Anforderungen für Netzwerke, Betriebssysteme und Hardware wie für die Installation von Configuration Manager in Ihrem physischen Unternehmensnetzwerk.  

Ein Azure-Abonnement ist erforderlich, um virtuelle Azure-Computer zu verwenden. Die Gebühren fallen basierend auf der Anzahl verwendeter virtueller Computer, ihrer Konfiguration und der Nutzung cloudbasierter Ressourcen an.  

Darüber hinaus gelten für Configuration Manager-Standorte und -Clients, die auf virtuellen Azure-Computern ausgeführt werden, dieselben Lizenzanforderungen wie für lokale Installationen.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Azure-Dienste (für cloudbasierte Verteilungspunkte)  
 Sie können einen Azure-Dienst zum Hosten eines Configuration Manager-Verteilungspunkts verwenden, der als cloudbasierter Verteilungspunkt bezeichnet wird. Sie können einen [cloudbasierten Verteilungspunkt mit System Center Configuration Manager verwenden](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md), und gleichzeitig lokale Verteilungspunkte und in virtuellen Azure-Computern bereitgestellte Verteilungspunkte nutzen.  

 Dies unterscheidet sich von der Verwendung eines virtuellen Azure-Computers, auf dem Sie eine Standortsystemrolle bereitstellen. Cloudbasierte Verteilungspunkte:  

-   Werden als Dienst in Azure, nicht auf einem virtuellen Computer ausgeführt.  

-   Werden automatisch skaliert, um zunehmende Inhaltsanforderungen von Clients zu erfüllen.  

-   Unterstützen Clients im Internet und Intranet.  

Ein Azure-Abonnement ist erforderlich, um mit Azure Verteilungspunkte zu hosten. Die Gebühren fallen basierend auf der Menge der Daten an, die in den und aus dem Dienst übertragen werden.  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (zur Verwaltung mobiler Geräte)  
 Sie können Ihr Microsoft Intune-Abonnement mit Configuration Manager integrieren, um die Verwaltung von Geräten mit dem Intune-Dienst zu ermöglichen. Diese Integration:  

-   Wird als Hybridkonfiguration bezeichnet und erweitert Configuration Manager (oder Intune je nach Sichtweise) so, dass eine große Vielfalt von Geräten unterstützt wird.  

-   Erfordert die Standortsystemrolle „Microsoft Intune-Connector“.  

-   Erfordert, dass Sie über ein separates Intune-Abonnement mit genügend Lizenzen für die Geräte verfügen, die Sie mit Intune verwalten.  

Obwohl Azure von Intune verwendet wird, ist es nicht erforderlich, Azure unabhängig zu konfigurieren. Zudem fallen keine zusätzlichen Gebühren an, die über die des Intune-Abonnements hinausgehen.  

### <a name="additional-configuration-manager-capabilities"></a>Zusätzliche Configuration Manager-Funktionen  
 Einige Configuration Manager-Funktionen können sich mit cloudbasierten Diensten wie den folgenden verbinden:  

-   Windows Server Update Services (WSUS)  

-   Die Configuration Manager-Dienstcloud zum Herunterladen von Updates für Configuration Manager.  

Diese zusätzlichen Funktionen erfordern kein Azure-Abonnement. Sie müssen keine bestimmten Verbindungen, Zertifikate oder Dienste in der Cloud einrichten. Stattdessen werden Sie von Configuration Manager automatisch für Sie verwaltet. Sie müssen lediglich sicherstellen, dass die betreffenden Standortsysteme und -geräte Zugriff auf die internetbasierten URLs haben.  

##  <a name="BKMK_CloudSec"></a> Sicherheit für cloudbasierte Dienste  
 Configuration Manager nutzt Zertifikate zum Bereitstellen des Zugriffs auf Ihre Inhalte in Azure und zum Verwalten der von Ihnen verwendeten Dienste. Die Daten, die Sie in Azure speichern, werden von Configuration Manager verschlüsselt. Über die von Azure bereitgestellten Sicherheitsfunktionen hinaus werden jedoch von Configuration Manager keine zusätzlichen Sicherheits- oder Datenschutzfunktionen bereitgestellt.  

 Weitere Informationen finden Sie in den Details zu den verschiedenen cloudbasierten Ressourcenszenarios. Sie können auch die folgenden Themen zur Sicherheit von Azure lesen:  

-   [Windows Azure: Verstehen der Sicherheitskontoverwaltung in Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Azure Security Overview (Azure-Sicherheitsübersicht)](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Get Past the Security Crossroads in Your Cloud Migration (Treffen von Sicherheitsentscheidungen bei der Cloudmigration)](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Datensicherheit in Azure, Teil 1 von 2](http://go.microsoft.com/fwlink/p/?LinkId=262974)  
