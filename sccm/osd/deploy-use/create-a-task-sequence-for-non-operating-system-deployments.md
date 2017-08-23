---
title: "Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen | Microsoft-Dokumentation"
description: "Erstellen von Tasksequenzen, die nicht mit Systemen zur Betriebssystembereitstellung verknüpft sind, z.B. Verteilen von Software, Aktualisieren von Treibern, Bearbeiten von Benutzerzuständen, usw."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b4b04907f2cd48d81e864e46ca47c14a0b98a9f7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Erstellen einer Tasksequenz für Nicht-Betriebssystembereitstellungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Tasksequenzen in System Center Configuration Manager dienen zum Automatisieren einer Vielzahl von Aufgaben in Ihrer Umgebung. Diese Tasks wurden in erster Linie für die Bereitstellung von Betriebssystemen konzipiert und getestet.  Configuration Manager bietet viele weitere Features für den Einsatz als primäre Technologie in Szenarios wie [Anwendungsinstallation](../../apps/understand/introduction-to-application-management.md), [Installation von Softwareupdates](../../sum/understand/software-updates-introduction.md), [Konfiguration von Einstellungen](../../compliance/understand/ensure-device-compliance.md) oder benutzerdefinierte Automatisierung. Es gibt noch weitere Microsoft System Center-Automatisierungstechnologien wie [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) und [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) , die Sie auch in Erwägung ziehen sollten.  

Tasksequenzen sind ein mächtiges Werkzeug, weil sie flexibel sind und Ihnen dabei helfen, Clienteinstellungen zu konfigurieren, Software zu verteilen, Treiber zu aktualisieren, den Status von Benutzern zu bearbeiten und andere Tasks auszuführen, die nicht mit der Betriebssystembereitstellung in Zusammenhang stehen. Sie können eine benutzerdefinierte Tasksequenz erstellen, der Sie beliebig viele Tasks hinzufügen können. Für Bereitstellungen, bei denen kein Betriebssystem bereitgestellt wird, lassen sich in Configuration Manager benutzerdefinierte Tasksequenzen verwenden. Sollte eine Tasksequenz jedoch ungewollte oder inkonsistente Ergebnisse liefern, versuchen Sie den Vorgang zu vereinfachen. Dies erreichen Sie, indem Sie einfachere Schritte verwenden und die Aktionen auf mehrere Tasksequenzen aufteilen oder indem Sie das Erstellen und Testen der Tasksequenz in Phasen aufteilen.

 Folgende Schritte können in einer benutzerdefinierten Tasksequenz verwendet werden, die nicht für die Bereitstellung eines Betriebssystems gedacht ist:  

-   [Bereitschaft überprüfen](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Verbindung mit Netzwerkordner herstellen](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Paketinhalt herunterladen](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Anwendung installieren](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Paket installieren](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Softwareupdates installieren](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Computer neu starten](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [Befehlszeile ausführen](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [PowerShell-Skript ausführen](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Dynamische Variablen festlegen](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Tasksequenzvariable festlegen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Nächste Schritte
[Deploy the task sequence (Bereitstellen der Tasksequenz)](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)
