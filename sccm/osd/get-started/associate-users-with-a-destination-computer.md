---
title: Zuordnen von Benutzern zu einem Zielcomputer | Microsoft-Dokumentation
description: Konfigurieren Sie System Center Configuration Manager, um Benutzer beim Bereitstellen von Betriebssystemen zu Zielcomputern zuzuordnen.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c0331567b94a99b29cc73c16de17a9f3bc6b9e43
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>Zuordnen von Benutzern zu einem Zielcomputer in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn Sie System Center Configuration Manager verwenden, um ein Betriebssystem bereitzustellen, können Sie dem Zielcomputer, auf dem das Betriebssystem bereitgestellt wird, Benutzer zuordnen. Diese Konfiguration umfasst Folgendes:  

-   Ein einzelner Benutzer ist der primäre Benutzer des Zielcomputers.  

-   Mehrere Benutzer sind die primären Benutzer des Zielcomputers.  

 Von der Affinität zwischen Benutzer und Gerät wird die benutzerzentrierte Verwaltung unterstützt, wenn Sie Anwendungen bereitstellen. Wenn Sie dem Zielcomputer, auf dem ein Betriebssystem installiert werden soll, einen Benutzer zuordnen, können Sie diesem Benutzer zu einem späteren Zeitpunkt Anwendungen bereitstellen, die dann automatisch auf dem Zielcomputer installiert werden. Sie können zwar die Unterstützung für die Affinität zwischen Benutzer und Gerät konfigurieren, wenn Sie Betriebssysteme bereitstellen; sie können die Affinität zwischen Benutzer und Gerät jedoch nicht zum Bereitstellen von Betriebssystemen verwenden.  

 Weitere Informationen zur Affinität zwischen Benutzer und Gerät finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>Angeben eines Benutzers bei der Bereitstellung von Betriebssystemen  
 In der folgenden Tabelle sind die Aktionen aufgelistet, die Sie zur Integration der Affinität zwischen Benutzer und Gerät in Ihre Betriebssystembereitstellung ausführen können. Sie können die Affinität zwischen Benutzer und Gerät in PXE-Bereitstellungen, in Bereitstellungen mit startbaren Medien sowie in Bereitstellungen mit vorab bereitgestellten Medien integrieren.  

|Aktion|Weitere Informationen|  
|------------|----------------------|  
|Erstellen Sie eine Tasksequenz, welche die Variable **SMSTSAssignUsersMode** enthält.|Fügen Sie die Variable **SMSTSAssignUsersMode** dem Anfang Ihrer Tasksequenz hinzu, indem Sie den Tasksequenzschritt  [Set Task Sequence Variable](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) verwenden. Mit dieser Variable geben Sie an, wie die Benutzerinformationen von der Tasksequenz verarbeitet werden.<br /><br /> Legen Sie einen der folgenden Werte für die Variable fest:<br /><br /> <br /><br /> **Auto**: Es wird automatisch eine Beziehung zwischen Benutzer und Zielcomputer erstellt, und das Betriebssystem wird automatisch bereitgestellt.<br /><br /> **Ausstehend**: Von der Tasksequenz wird eine Beziehung zwischen dem Benutzer und dem Zielcomputer erstellt. Es wird jedoch auf die Genehmigung durch den Administrator gewartet, bevor das Betriebssystem bereitgestellt wird.<br /><br /> **Deaktiviert**: Während der Bereitstellung des Betriebssystems wird keine Beziehung zwischen einem Benutzer und dem Zielcomputer erstellt.<br /><br /> <br /><br /> Diese Variable kann auch bei einem Computer oder einer Sammlung festgelegt werden. Weitere Informationen zu integrierten Tasksequenzvariablen finden Sie unter [Integrierte Tasksequenzvariablen](../../osd/understand/task-sequence-built-in-variables.md).|  
|Erstellen eines Prestart-Befehls, von dem Benutzerinformationen gesammelt werden|Bei dem Prestart-Befehl kann es sich um ein Visual Basic-Skript (VB) mit Eingabefeld handeln oder um eine HTML-Anwendung (HTA), von der die eingegebenen Benutzerdaten überprüft werden.<br /><br /> Vom Prestart-Befehl muss die Variable **SMSTSUdaUsers** festgelegt werden, die beim Ausführen der Tasksequenz verwendet wird. Diese Variable kann auf einem Computer, einer Sammlung oder einer Tasksequenzvariable festgelegt werden. Verwenden Sie folgendes Format, wenn Sie mehrere Benutzer hinzufügen: *Domäne\Benutzer1, Domäne\Benutzer2, Domäne\Benutzer3*.|  
|Konfigurieren der Zuordnung von Benutzer und Zielcomputer durch Medien und Verteilungspunkte|Wenn Sie [einen Verteilungspunkt so konfigurieren, dass PXE-Startanforderungen von ihm akzeptiert werden](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) , und mithilfe des Assistenten zum Erstellen von Tasksequenzmedien [startbare Medien](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) oder [vorab bereitgestellte Medien](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) erstellen, können Sie angeben, wie die Zuordnung von Benutzern und Zielcomputern dort, wo das Betriebssystem bereitgestellt wird, durch den Verteilungspunkt oder die Medien unterstützt werden soll.<br /><br /> In der Unterstützungskonfiguration der Affinität zwischen Benutzer und Gerät ist keine Methode zur Überprüfung der Benutzeridentität enthalten. Dies kann wichtig sein, wenn ein Techniker bei der Bereitstellung des Computers diese Informationen anstelle des Benutzers eingibt. Sie können nicht nur festlegen, wie die Benutzerinformationen von der Tasksequenz verarbeitet werden, sondern mithilfe der Konfiguration dieser Optionen an Verteilungspunkts und Medien können Sie auch die Bereitstellungen begrenzen, die durch einen PXE-Start oder von einem bestimmten Mediumtyp gestartet werden.|  
