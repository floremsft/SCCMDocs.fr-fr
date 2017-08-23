---
title: "Funktionen in Technical Preview 1607 für Configuration Manager"
description: "Erfahren Sie mehr zu den Features, die in System Center Configuration Manager Technical Preview 1607 zur Verfügung stehen."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
caps.latest.revision: "11"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4717e0f8eef01501fb5b5790e855c476c1ca4590
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1607-for-system-center-configuration-manager"></a>Funktionen in Technical Preview 1607 für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Technical Preview)*

In diesem Artikel werden die Features erläutert, die in der Technical Preview für System Center Configuration Manager 1607 verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für System Center Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen, und zu erfahren, wie Sie Updates zwischen Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="dmp_edition"></a>Verbesserungen an der Richtlinie für Windows 10-Editionsupgrades

In dieser Release wurden die folgenden Verbesserungen an der Richtlinie vorgenommen:

* Sie können nun die Richtlinie für Editionsupgrades mit Windows 10-PCs, die den Configuration Manager-Client ausführen, zusätzlich zu Windows 10-PCs verwenden, die in Microsoft Intune registriert sind.
* Sie können von Windows 10 Professional auf beliebige Plattformen im Assistenten aktualisieren, die mit Ihrer Hardware kompatibel sind.

[Erfahren Sie mehr über die Richtlinie für Windows 10-Editionsupgrades.](/sccm/compliance/deploy-use/upgrade-windows-version)

### <a name="try-it-out"></a>Probieren Sie es aus!

1. Informationen zum Erstellen einer Richtlinie für Editionsupgrades finden Sie unter [Thema der vorhandenen Editionsupgraderichtlinie](/sccm/compliance/deploy-use/upgrade-windows-version).
2. Stellen Sie diese Richtlinie auf einem Windows 10-PC bereit, der den Configuration Manager-Client ausführt.
Sobald die Richtlinie einen entsprechenden Windows-PC erreicht, wird der PC innerhalb von zwei Stunden zum Installieren des Upgrades neu gestartet. Derzeit können Sie diesen Neustart nicht unterdrücken. Stellen Sie sicher, dass Sie jeden Benutzer informieren, dem Sie die Richtlinie bereitstellen, oder planen Sie die Ausführung der Richtlinie außerhalb der Arbeitsstunden der Benutzer.

### <a name="known-issue-with-this-release"></a>Bekannte Probleme in diesem Release
In den Configuration Manager-Clienteinstellungen finden Sie möglicherweise Einstellungen für **Editionsupgrades**. In diesem Release sind diese Einstellungen nicht funktionsfähig. Verwenden Sie die Hinweise weiter oben, um für Windows 10 ein Upgrade auf eine neuere Version durchzuführen.

## <a name="customizable-branding-for-software-center-dialogs"></a>Anpassbares Branding für Software Center-Dialogfelder

Benutzerdefiniertes Branding für das Softwarecenter wurde in Configuration Manager-Version 1602 eingeführt. In Technical Preview-Version 1607 ist dieses Branding jetzt auf alle zugehörigen Dialogfelder und Benachrichtigungen der Taskleiste ausgeweitet, um eine konsistentere Erfahrung für Softwarecenter-Benutzer zur Verfügung zu stellen.

### <a name="try-it-out"></a>Probieren Sie es aus!

Benutzerdefiniertes Branding für das Softwarecenter wird gemäß den folgenden Regeln angewendet:

1. Wenn die Standortserverrolle „Anwendungskatalog-Websitepunkt“ nicht installiert ist, zeigt das Softwarecenter den Organisationsnamen an, der in der **Computer-Agent**-Clienteinstellung **Im Softwarecenter angezeigter Organisationsname** angegeben ist. Eine Anleitung hierzu finden Sie unter [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md).

2. Wenn die Standortserverrolle „Anwendungskatalog-Websitepunkt“ installiert ist, zeigt Software Center den Organisationsnamen und die Farbe an, der bzw. die in den Eigenschaften der Standortserverrolle „Anwendungskatalog-Websitepunkt“ angegeben sind. Weitere Informationen finden Sie unter [Konfigurationsoptionen für den Anwendungskatalog-Websitepunkt](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Wenn ein Microsoft Intune-Abonnement konfiguriert und mit der Configuration Manager-Umgebung verbunden ist, zeigt das Softwarecenter den Organisationsnamen, die Farbe und das Unternehmenslogo entsprechend den Angaben in den Eigenschaften des Intune-Abonnements an. Weitere Informationen finden Sie unter [Configuring the Microsoft Intune subscription (Konfigurieren des Microsoft Intune-Abonnements)](/mdm/deploy-use/configure-intune-subscription).

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Verwenden derselben Netzwerkadapter für mehrere PXE-initiierte Bereitstellungen
In Technical Preview-Version 1607 können Sie bei der Verwendung eines Ethernet-Adapters für das Abbilden mehrere Geräte (z.B. ein USB-Ethernetadapter, den Sie auf mehreren Geräten verwenden) eine neue Einstellung aktivieren, mit der Sie Hardware-IDs für die Ethernet-Adapter eingeben können. Configuration Manager ignoriert die Hardware-IDs in der Liste für die Clientregistrierung, oder wenn er eine PXE-Installation ausführt.

Weitere Informationen zu diesem Problem finden Sie auf dem englischsprachigen [Blog des Configuration Manager OSD-Supportteams](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Aktivieren des Features zum Verwalten von doppelten Hardware-IDs  
1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Updates und Wartung** > **Features**.
2. Wählen Sie im Anzeigebereich **Doppelte Hardware-IDs verwalten** aus.
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Features** auf **Aktivieren**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Hinzufügen von Hardware-IDs, die Configuration Manager ignorieren soll  
1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Standortkonfiguration** > **Standorte**.
2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.
3. Klicken Sie auf die Registerkarte **Clientgenehmigung und in Konflikt stehende Datensätze**.
4. Klicken Sie im Abschnitt **Doppelte Hardware-IDs** auf **Hinzufügen**, um neue Hardware-IDs hinzuzufügen.
