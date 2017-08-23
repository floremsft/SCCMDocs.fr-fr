---
title: "Szenarien für die Bereitstellung von Unternehmensbetriebssystemen | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über Szenarios zur Bereitstellung von Unternehmensbetriebssystemen mit System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
caps.latest.revision: "11"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b1bea8b1b890f7c96a432835d28ad840a9b6873d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-system-center-configuration-manager"></a>Szenarien zur Bereitstellung von Unternehmensbetriebssystemen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die folgenden Szenarios für die Betriebssystembereitstellung sind in System Center Configuration Manager verfügbar:  

-   [Durchführen eines Upgrades von Windows auf die neueste Version](upgrade-windows-to-the-latest-version.md): In diesem Szenario wird das Betriebssystem auf Computern upgegradet, auf denen derzeit Windows 7, Windows 8, Windows 8.1 oder Windows 10 ausgeführt wird. Bei dem Upgradevorgang werden die Anwendungen, Einstellungen und Benutzerdaten auf dem Computer beibehalten. Es liegen keine externen Abhängigkeiten vor, wie z. B. Windows ADK, und dieser Vorgang ist schneller und weniger fehleranfällig als herkömmliche Betriebssystembereitstellungen.  

-   [Aktualisieren eines vorhandenen Computers auf eine neue Windows-Version](refresh-an-existing-computer-with-a-new-version-of-windows.md): In diesem Szenario wird ein vorhandener Computer partitioniert und formatiert (gelöscht) und ein neues Betriebssystem auf dem Computer installiert. Sie können Einstellungen und Benutzerdaten nach der Installation des Betriebssystems migrieren.  

-   [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare Metal)](install-new-windows-version-new-computer-bare-metal.md): In diesem Szenario wird ein Betriebssystem auf einem neuen Computer installiert. Dies ist eine Neuinstallation des Betriebssystems ohne Migration von Einstellungen oder Benutzerdaten.  

-   [Ersetzen eines vorhandenen Computers und Übertragen der Einstellungen](replace-an-existing-computer-and-transfer-settings.md): In diesem Szenario wird ein Betriebssystem auf einem neuen Computer installiert. Optional können Sie Einstellungen und Benutzerdaten vom alten Computer auf den neuen Computer migrieren.  

## <a name="things-to-consider-before-you-deploy-operating-system-images"></a>Zu berücksichtigende Aspekte vor der Bereitstellung von Betriebssystemabbildern  
 Es gibt bestimmte Aspekte, die vor der Bereitstellung eines Betriebssystems zu berücksichtigen sind.  

### <a name="operating-system-image-size"></a>Größe des Betriebssystemabbilds  
 Betriebssystemabbilder können sehr groß sein. Beispielsweise beträgt die Abbildgröße für Windows 7 mindestens 3 GB. Die Größe des Abbilds und die Anzahl der Computer, auf denen Sie das Betriebssystem gleichzeitig bereitstellen, haben Einfluss auf die Netzwerkleistung und die verfügbare Bandbreite. Stellen Sie sicher, dass Sie die Netzwerkleistung testen, um die Auswirkung besser einschätzen zu können, die die Abbildbereitstellung möglicherweise hat. Zudem erhalten Sie Informationen zum Zeitaufwand, der für das Abschließen der Bereitstellung erforderlich ist. Configuration Manager-Aktivitäten, die sich auf die Leistung des Netzwerks auswirken, umfassen die Verteilung des Images an einen Verteilungspunkt sowie die Verteilung des Images von einem Standort an einen anderen und das Herunterladen des Images auf den Configuration Manager-Client.  

 Sie müssen auch genügend Speicherplatz auf den Verteilungspunkten einplanen, auf denen die Betriebssystemabbilder gehostet werden.  

### <a name="client-cache-size"></a>Cachegröße des Clients  
 Wenn Inhalt von Configuration Manager-Clients heruntergeladen wird, wird automatisch der intelligente Hintergrundübertragungsdienst (Background Intelligent Transfer Service oder BITS) verwendet, sofern dieser verfügbar ist. Wenn Sie eine Tasksequenz bereitstellen, mit der ein Betriebssystem installiert wird, können Sie über eine Bereitstellungsoption festlegen, dass das vollständige Image von den Configuration Manager-Clients vor der Ausführung der Tasksequenz in einen lokalen Cache heruntergeladen wird.  

 Allgemein gilt: Wenn ein Betriebssystemimage (oder ein anderes Paket) von einem Configuration Manager-Client heruntergeladen werden muss und im Cache nicht genügend Platz verfügbar ist, werden die anderen Pakete im Cache vom Client überprüft, um zu bestimmen, ob durch das Löschen einiger oder aller ältesten Pakete genügend Speicherplatz für die Aufnahme des Images freigegeben wird. Wenn durch das Löschen von Paketen nicht genügend Speicherplatz freigegeben wird, wird das Abbild nicht vom Client heruntergeladen, und bei der Bereitstellung tritt ein Fehler auf. Das kann der Fall sein, wenn sich ein großes Paket im Cache befindet, das aufgrund der Konfiguration im Cache verbleiben muss. Falls durch das Löschen von Paketen genügend Speicherplatz im Cache freigegeben werden kann, wird der Löschvorgang vom Client ausgeführt, und das Abbild wird in den Cache heruntergeladen.  

 Der Standardcache auf Configuration Manager-Clients ist möglicherweise für die meisten Betriebssystemimage-Bereitstellungen nicht groß genug. Wenn Sie das vollständige Image in den Clientcache herunterladen möchten, müssen Sie die Größe des Configuration Manager-Clientcaches auf den Zielcomputern so anpassen, dass das bereitzustellende Image darin aufgenommen werden kann.  

 Weitere Informationen finden Sie unter [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

## <a name="task-sequence-deployments"></a>Tasksequenzbereitstellungen  
 Mit der von Ihnen erstellten Tasksequenz kann das Betriebssystemimage auf eine der folgenden Weisen auf einem Configuration Manager-Clientcomputer bereitgestellt werden:  

-   Laden Sie das Image und dessen Inhalt zunächst von einem Verteilungspunkt in den Configuration Manager-Clientcache herunter, und installieren Sie dann das Image samt Inhalt.  

-   Installieren Sie das Abbild und dessen Inhalt unmittelbar vom Verteilungspunkt aus.  

-   Installieren Sie das Abbild und dessen Inhalt im Bedarfsfall vom Verteilungspunkt aus.  

 Wenn Sie die Bereitstellung für die Tasksequenz erstellen, wird das Image standardmäßig zunächst in den Configuration Manager-Clientcache heruntergeladen und dann installiert. Wenn Sie sich entscheiden, das Image vor dem Ausführen in den Configuration Manager-Clientcache herunterzuladen, und die Tasksequenz einen Schritt zum Neupartitionieren des Festplattenlaufwerks enthält, tritt bei diesem Schritt ein Fehler auf, weil der Inhalt des Configuration Manager-Clientcaches beim Partitionieren der Festplatte gelöscht wird. Wenn die Festplatte von der Tasksequenz neu partitioniert werden muss, müssen Sie die Abbildinstallation vom Verteilungspunkt ausführen. Verwenden Sie dazu bei der Bereitstellung der Tasksequenz die Option **Programm vom Verteilungspunkt ausführen**  .  

 Weitere Informationen finden Sie unter [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
