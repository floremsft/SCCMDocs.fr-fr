---
title: Bereitstellen von Softwareupdates | Microsoft-Dokumentation
description: "Wählen Sie die Softwareupdates in der Configuration Manager-Konsole aus, um den Bereitstellungsprozess manuell zu starten oder Updates manuell bereitzustellen."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 70a0ad1da03a7ca88df206fec683ab1df2b531e1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_SUMDeploy"></a> Bereitstellen von Softwareupdates  

*Gilt für: System Center Configuration Manager (Current Branch)*

In der Softwareupdate-Bereitstellungsphase werden Softwareupdates bereitgestellt. Unabhängig davon, wie Sie Softwareupdates bereitstellen, werden die Updates in der Regel zu einer Softwareupdategruppe hinzugefügt. Die Softwareupdates werden auf Verteilungspunkte heruntergeladen, und die Updategruppe wird für Clients bereitgestellt. Beim Erstellen der Bereitstellung wird eine zugehörige Softwareupdaterichtlinie an Clientcomputer gesendet. Dann werden die Inhaltsdateien für das Softwareupdate von einem Verteilungspunkt in den lokalen Cache auf Clientcomputer heruntergeladen. Die Softwareupdates sind damit für die Installation auf dem Client verfügbar. Von Clients, die sich im Internet befinden, wird Inhalt von Microsoft Update heruntergeladen.  

> [!NOTE]  
>  Sie können einen Client im Intranet zum Herunterladen von Softwareupdates von Microsoft Update für den Fall konfigurieren, dass ein Verteilungspunkt nicht verfügbar ist.  

> [!NOTE]  
>  Im Gegensatz zu anderen Bereitstellungstypen werden alle Softwareupdates unabhängig von der auf dem Client festgelegten maximalen Cachegröße in den Clientcache heruntergeladen. Weitere Informationen zu den Einstellungen des Clientcaches finden Sie unter [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Wenn Sie eine erforderliche Softwareupdatebereitstellung konfigurieren, werden die Softwareupdates automatisch am geplanten Stichtag installiert. Alternativ kann der Benutzer die Softwareupdateinstallation auf dem Clientcomputer auch vor dem Stichtag einplanen oder initiieren. Nach dem Installationsversuch werden von den Clientcomputern Zustandsmeldungen zurück an den Standortserver gesendet, aus denen hervorgeht, ob die Softwareupdateinstallation erfolgreich war. Weitere Informationen zu Softwareupdatebereitstellungen  finden Sie unter [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Die Bereitstellung von Softwareupdates in einer Umgebung erfolgt entweder manuell oder automatisch. In der Regel beginnen Sie damit, dass Sie Softwareupdates manuell bereitstellen, um eine Baseline für die Clientcomputer zu erstellen. Die Verwaltung der Softwareupdates auf Clients erfolgt dann durch die automatische Bereitstellung.  

## <a name="BKMK_ManualDeployment"></a> Manuelles Bereitstellen von Softwareupdates
Sie können Softwareupdates in der Configuration Manager-Konsole auswählen und den Bereitstellungsprozess manuell starten. Mit dieser Bereitstellungsmethode sorgen Sie in der Regel dafür, dass die aktuell erforderlichen Softwareupdates auf den Clientcomputern vorhanden sind, bevor Sie automatische Bereitstellungsregeln zur Verwaltung der laufenden monatlichen Softwareupdatebereitstellungen erstellen. Diese Methode dient auch dazu, Out-of-Band-Anforderungen für Softwareupdates bereitzustellen. Der allgemeine Workflow für die manuelle Bereitstellung von Softwareupdates umfasst die folgenden Schritte:  

1. Filtern Sie Softwareupdates mit bestimmten Anforderungen heraus. Beispielsweise könnten Sie anhand geeigneter Kriterien angeben, dass alle Softwareupdates abgerufen werden sollen, die auf mehr als 50 Clientcomputern benötigt werden und deren Klassifizierung Sicherheit oder Kritisch lautet.  
2. Erstellen Sie eine Softwareupdategruppe, die die Softwareupdates enthält.  
3. Laden Sie den Inhalt für die Softwareupdates in der Softwareupdategruppe herunter.  
4. Stellen Sie die Softwareupdategruppe manuell bereit.

Ausführliche Schritte finden Sie unter [Manuelles Bereitstellen von Softwareupdates](manually-deploy-software-updates.md).

## <a name="automatically-deploy-software-updates"></a>Automatisches Bereitstellen von Softwareupdates
Die automatische Bereitstellung von Softwareupdates wird mithilfe einer automatischen Bereitstellungsregel (ADR) konfiguriert. Diese Bereitstellungsmethode eignet sich insbesondere für monatliche Softwareupdates (in der Regel bekannt als „Patch-Dienstag“) und für die Verwaltung von Definitionsupdates. Bei der Ausführung der Regel werden Softwareupdates aus der Softwareupdategruppe entfernt (bei Verwendung einer vorhandenen Updategruppe), Softwareupdates, die einem angegebenen Kriterium entsprechen (z.B. alle im letzten Monat veröffentlichten Sicherheitsupdates), zu einer Softwareupdategruppe hinzugefügt, die Inhaltsdateien für die Softwareupdates heruntergeladen und auf Verteilungspunkte kopiert und die Softwareupdates für Clients in der Zielsammlung bereitgestellt. Die folgende Liste bietet den allgemeinen Workflow, um Softwareupdates automatisch bereitzustellen:  

1.  Erstellen Sie eine automatische Bereitstellungsregel, die Bereitstellungseinstellungen angibt.
2.  Die Softwareupdates werden einer Softwareupdategruppe hinzugefügt.  
3.  Die Softwareupdategruppe wird auf den Clientcomputern in der Zielsammlung bereitgestellt, sofern diese angegeben ist.  

Sie müssen eine Bereitstellungsstrategie für Ihre Umgebung auswählen. Beispielsweise könnten Sie eine automatische Bereitstellungsregel erstellen und eine Sammlung mit Testclients als Ziel angeben. Nachdem Sie sich vergewissert haben, dass die Softwareupdates in der Testgruppe installiert werden, können Sie eine neue Bereitstellung zur Regel hinzufügen oder in der vorhandenen Bereitstellung eine andere Zielsammlung angeben, die mehr Clients enthält. Die von den automatischen Bereitstellungsregeln erstellten Softwareupdateobjekte sind interaktiv.  

-   Die mithilfe einer automatischen Bereitstellungsregel bereitgestellten Softwareupdates werden neuen Clients, die der Zielsammlung hinzugefügt werden, automatisch bereitgestellt.  
-   Neue Softwareupdates, die einer Softwareupdategruppe hinzugefügt werden, werden den Clients in der Zielsammlung automatisch bereitgestellt.  
-   Sie können Bereitstellungen für die automatische Bereitstellungsregel jederzeit aktivieren oder deaktivieren.  

Nach der Erstellung einer automatischen Bereitstellungsregel können Sie zusätzliche Bereitstellungen zur Regel hinzufügen. Dies hilft Ihnen dabei, die Komplexität der Bereitstellung verschiedener Updates für verschiedene Sammlungen zu verwalten. Jede neue Bereitstellung verfügt über sämtliche Funktionen und die Bereitstellungsüberwachungsumgebung, und in jeder neu hinzugefügten Bereitstellung:  

-   Werden die gleiche Upgradegruppe und das gleiche Upgradepaket verwendet, die bzw. das bei der ersten Ausführung der ADR erstellt wurde.  
-   Kann eine andere Sammlung angegeben werden.  
-   Werden eindeutige Bereitstellungseigenschaften unterstützt, einschließlich:  
   -   Aktivierungszeitpunkt  
   -   Stichtag  
   -   Endbenutzeroberfläche ein- oder ausblenden  
   -   Warnungen für diese Bereitstellung trennen  

Ausführliche Schritte finden Sie unter [Automatisches Bereitstellen von Softwareupdates](automatically-deploy-software-updates.md).

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->
