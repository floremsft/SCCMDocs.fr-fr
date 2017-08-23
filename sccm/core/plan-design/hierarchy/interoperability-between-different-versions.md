---
title: "Interoperabilität zwischen den Configuration Manager-Versionen | Microsoft-Dokumentation"
description: "Hier erfahren Sie, wie Konflikte zwischen verschiedenen System Center Configuration Manager-Hierarchien im selben Netzwerk vermieden werden können."
ms.custom: na
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 28593d271603ff9775425327996d844d7ed358cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilität zwischen verschiedenen Versionen von System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können mehrere unabhängiger Hierarchien von System Center Configuration Manager im selben Netzwerk installieren und betreiben. Da unterschiedliche Hierarchien von Configuration Manager außerhalb des Migrationsprozesses nicht zusammenarbeiten, erfordert jede Hierarchie entsprechende Konfigurationen, um Konflikte zu vermeiden. Außerdem können Sie bestimmte Konfigurationen vornehmen, damit von Ihnen verwaltete Ressourcen jeweils mit den Standortsystemen der richtigen Hierarchie interagieren können.  

 Die folgenden Abschnitte enthalten Informationen zur Verwendung unterschiedlicher Versionen von Configuration Manager in einem Netzwerk:  

-   [Interoperabilität zwischen System Center Configuration Manager und früheren Produktversionen](#BKMK_SupConfigInterop)  

-   [Interoperabilität für die Configuration Manager-Konsole](#BKMK_ConsoleInterop)  

-   [Configuration Manager-Einschränkungen in einer Hierarchie mit unterschiedlichen Versionen](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interoperabilität zwischen System Center Configuration Manager und früheren Produktversionen  
 Standorte mit unterschiedlichen Versionen in einer Hierarchie können nicht parallel verwendet werden, außer während des Upgrades von System Center 2012 Configuration Manager auf System Center Configuration Manager oder von einer System Center Configuration Manager-Version auf eine neuere Version (mit konsoleninternen Updates).   

 Da Sie einen Standort und eine Hierarchie von System Center Configuration Manager zusammen mit einem vorhandenen Standort oder einer vorhandenen Hierarchie von System Center 2012 Configuration Manager bereitstellen können, sollten Sie Vorkehrungen treffen, die verhindern, dass Clients einer Version versuchen, einem Standort der anderen Version beizutreten.

Wenn beispielsweise mindestens zwei Configuration Manager-Hierarchien überlappende Grenzen aufweisen, die dieselben Netzwerkadressen beinhalten (Informationen hierzu finden Sie unter [overlapping boundaries (überlappende Grenzen)](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries)), sollten Sie jeden neuen Client einem bestimmten Standort zuweisen, anstatt die automatische Standortzuweisung zu verwenden. Weitere Informationen zur automatischen Standortzuweisung in System Center 2012 Configuration Manager finden Sie unter [How to assign clients to a site in System Center Configuration Manager (Zuweisen von Clients zu einem Standort in System Center Configuration Manager)](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Darüber hinaus können Sie weder die Installation eines Clients von System Center 2012 Configuration Manager auf einem Computer, auf dem eine Standortsystemrolle von System Center Configuration Manager gehostet wird, noch die Installation eines System Center Configuration Manager-Clients auf einem Computer vornehmen, auf dem eine Standortsystemrolle von System Center 2012 Configuration Manager gehostet wird.  

 Ganz ähnlich werden die folgenden Clients und die folgende VPN-Verbindung (Virtual Private Network) nicht unterstützt:  

-   System Center 2012 Configuration Manager oder frühere Computerclientversionen  

-   System Center 2012 Configuration Manager oder frühere Geräteverwaltungsclients  

-   Windows CE Platform Builder-Geräteverwaltungsclient (alle Versionen)  

-   VPN-Verbindung für System Center Mobile Device Manager  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Überlegungen zur Clientstandortzuweisung  
 System Center Configuration Manager-Clients können nur einem einzigen primären Standort zugewiesen werden. Wenn Clients während der Clientinstallation mithilfe der automatischen Standortzuweisung zugewiesen werden und mehrere Begrenzungsgruppen mit unterschiedlichen zugewiesenen Standorten die gleiche Grenze enthalten, erfolgt die tatsächliche Standortzuweisung des Clients nicht deterministisch.  

 Wenn sich die Grenzen mehrerer Configuration Manager-Standorte und -Hierarchien überlappen, werden Clients möglicherweise nicht dem von Ihnen erwarteten Standort oder sogar gar keinem Standort zugewiesen.  

 System Center Configuration Manager-Clients prüfen die Version des Configuration Manager-Standorts, bevor die Standortzuweisung durchgeführt wird. Dabei können sie einer früheren Version nur zugewiesen werden, wenn keine Grenzen überlappen. System Center 2012 Configuration Manager-Clients werden jedoch unter Umständen fälschlicherweise einem System Center Configuration Manager-Standort zugewiesen.  

 Um zu verhindern, dass Clients irrtümlich einem falschen Standort zugewiesen werden, wenn zwei Hierarchien überlappende Grenzen haben, empfehlen wir Ihnen, die Configuration Manager-Clientinstallationsparameter so zu konfigurieren, dass Clients einem bestimmten Standort zugewiesen werden.  

##  <a name="bkmk_mixed"></a> Configuration Manager-Einschränkungen in einer Hierarchie mit unterschiedlichen Versionen  
 Wenn Sie für einen System Center Configuration Manager-Standort ein Upgrade durchführen, gibt es Zeiten, zu denen verschiedene Standorte verschiedene Versionsstände haben. Beispielsweise könnten Sie für einen Standort der zentralen Verwaltung ein Upgrade auf eine neue Version durchführen, aber aufgrund von Standortwartungsfenstern kann es passieren, dass das Upgrade für mindestens einen primären Standort erst zu einem späteren Zeitpunkt durchgeführt werden kann.  

 Wenn in verschiedenen Standorten einer einzelnen Hierarchie unterschiedliche Versionen ausgeführt werden, sind einige Funktionen möglicherweise nicht verfügbar. Dies kann sich darauf auswirken, wie Sie Configuration Manager-Objekte in der Configuration Manager-Konsole verwalten und welche Funktionen für Clients verfügbar sind. Normalerweise sind Funktionen aus neueren Configuration Manager-Versionen für Standorte oder Clients mit einer niedrigeren Service Pack-Version nicht verfügbar.  

### <a name="limitations-when-upgrading--configuration-manager"></a>Einschränkungen beim Durchführen eines Upgrades von Configuration Manager  

|Objekt|Details|  
|------------|-------------|  
|Netzwerkzugriffskonto|**Beim Upgraden von System Center 2012 Configuration Manager auf System Center Configuration Manager:** Wenn Sie eine Configuration Manager-Konsole verwenden, die mit einem Standort der zentralen Verwaltung verbunden ist, die auf System Center Configuration Manager aktualisiert wurde, um Details von Netzwerkzugriffskonten anzuzeigen, werden in der Konsole keine Informationen zu Konten angezeigt, die in einem primären Standort konfiguriert sind, an dem System Center 2012 Configuration Manager ausgeführt wird. Nachdem der primäre Standort auf dieselbe Version wie der Standort der zentralen Verwaltung aktualisiert wurde, werden die Details in der Konsole angezeigt.<br /><br /> **Beim Upgraden zwischen System Center Configuration Manager-Versionen:** Wenn Sie eine Configuration Manager-Konsole verwenden, die mit einem auf eine neue System Center Configuration Manager-Version aktualisierten Standort der zentralen Verwaltung verbunden ist, um Details von Netzwerkzugriffskonten anzuzeigen, werden in der Konsole keine Informationen zu Konten angezeigt, die in einem primären Standort konfiguriert sind, an dem eine frühere Version ausgeführt wird. Nachdem der primäre Standort auf dieselbe Version wie der Standort der zentralen Verwaltung aktualisiert wurde, werden die Details in der Konsole angezeigt.|  
|Startabbilder für die Betriebssystembereitstellung|**Beim Upgraden von System Center 2012 Configuration Manager auf System Center Configuration Manager:** Wenn für den Standort der obersten Ebene einer Hierarchie ein Upgrade auf System Center Configuration Manager durchgeführt wird, werden die Standardstartimages automatisch auf Windows Assessment und Deployment Kit 10 (Windows ADK)-basierte Startimages aktualisiert. Verwenden Sie diese Startimages nur für Bereitstellungen für Clients an System Center Configuration Manager-Standorten. Weitere Informationen finden Sie unter [Planen der Interoperabilität der Betriebssystembereitstellung in System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).<br /><br /> **Beim Upgraden zwischen System Center Configuration Manager-Versionen:** Solange neue Versionen von System Center Configuration Manager nicht die aktuelle Windows ADK-Version aktualisieren, gibt es keine Auswirkungen auf die Startimages.|  
|Neue Tasksequenzschritte|Wenn Sie eine Tasksequenz mit einem Schritt erstellen, der in einer Version von Configuration Manager eingeführt wurde und in einer früheren Version nicht verfügbar ist, können die folgenden Problemen auftreten:<br /><br /> – Es tritt ein Fehler auf, wenn Sie versuchen, die Tasksequenz von einem Standort aus zu bearbeiten, auf dem eine vorherige Version von Configuration Manager ausgeführt wird.<br /><br /> – Die Tasksequenz kann nicht auf einem Computer ausgeführt werden, auf dem eine vorherige Version des Configuration Manager-Clients ausgeführt wird.|  
|Kommunikation von Clients mit Verwaltungspunkten mit niedrigeren Versionen|Ein Configuration Manager-Client, der mit einem Verwaltungspunkt eines Standorts mit einer niedrigeren Version als der Version des Clients kommuniziert, kann nur die Funktionen nutzen, die von der niedrigeren Version von Configuration Manager unterstützt werden. Wenn Sie beispielsweise Inhalte eines Configuration Manager-Standorts, der vor kurzem aktualisiert wurde, auf einem Client bereitstellen, der mit einem Verwaltungspunkt kommuniziert, der noch nicht auf diese Version aktualisiert wurde, kann dieser Client die neuen Funktionen der neuesten Version nicht verwenden.|  

##  <a name="BKMK_ConsoleInterop"></a> Interoperabilität für die Configuration Manager-Konsole  
 Die folgende Tabelle enthält Informationen zur Verwendung der Configuration Manager-Konsole in einer Umgebung mit gemischten Configuration Manager-Versionen.  

|Interoperabilitätsumgebung|Weitere Informationen|  
|----------------------------------|----------------------|  
|Eine Umgebung mit System Center 2012 Configuration Manager und System Center Configuration Manager|Zum Verwalten eines Configuration Manager-Standorts muss auf der Konsole und am Standort, mit dem die Konsole verbunden ist, dieselbe Configuration Manager-Version ausgeführt werden. So kann beispielsweise nicht eine System Center 2012 Configuration Manager-Konsole zum Verwalten eines System Center Configuration Manager-Standorts und umgekehrt verwendet werden.<br /><br /> Die parallele Installation der System Center 2012 Configuration Manager-Konsole und der System Center Configuration Manager-Konsole auf einem Computer wird nicht unterstützt.|  
|Eine Umgebung mit mehreren Versionen von System Center Configuration Manager|Von System Center Configuration Manager wird die Installation von mehreren Configuration Manager-Konsolen auf einem Computer nicht unterstützt. Wenn Sie mehrere, zu unterschiedlichen System Center Configuration Manager-Versionen gehörende Konsolen verwenden möchten, müssen Sie diese auf unterschiedlichen Computern installieren.<br /><br /> Bei laufender Aktualisierung von Standorten in einer Hierarchie auf eine neue Version können Sie eine Konsole mit einem Standort verbinden, auf dem eine neuere Version ausgeführt wird, und Informationen zu anderen Standorten in dieser Hierarchie anzeigen. Diese Konfiguration wird aber nicht empfohlen, weil die Möglichkeit besteht, dass Unterschiede zwischen der Konsolenversion und der Configuration Manager-Standortversion zu Datenproblemen führen und einige Funktionen, die in der neuesten Produktversion verfügbar sind, in der Konsole nicht zur Verfügung stehen. <br /></br /> Das Verwalten eines Standorts bei Verwendung einer Konsole mit einer Version, die nicht mit der Standortversion übereinstimmt, wird nicht unterstützt. Dies kann dazu führen, dass Daten verloren gehen und dass Ihre Website gefährdet wird. Es wird z.B. nicht unterstützt, eine Konsole der Version 1610 zu verwenden, um einen Standort zu verwalten, der Version 1606 ausführt. |
