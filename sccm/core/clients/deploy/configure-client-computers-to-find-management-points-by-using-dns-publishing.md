---
title: "Konfigurieren von Clients für die Suche nach Verwaltungspunkten mithilfe der DNS-Veröffentlichung | Microsoft-Dokumentation"
description: "Konfigurieren Sie Clientcomputer für die Suche nach Verwaltungspunkten mithilfe der DNS-Veröffentlichung in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d016ec3fe106b2d90b3c14b4f9296aed4d198644
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-computers-to-find-management-points-by-using-dns-publishing-in-system-center-configuration-manager"></a>Konfigurieren von Clientcomputern für die Suche nach Verwaltungspunkten mithilfe der DNS-Veröffentlichung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Clients in System Center Configuration Manager müssen kontinuierlich einen Verwaltungspunkt suchen, um die Standortzuordnung abzuschließen und anschließend ihre Verwaltung sicherzustellen. Active Directory-Domänendienste bieten Clients die sicherste Methode zum Suchen nach Verwaltungspunkten im Intranet. Wenn diese Dienstidentifizierungsmethode jedoch nicht verfügbar ist (z. B., wenn das Active Directory-Schema nicht erweitert wurde oder Clients sich in einer Arbeitsgruppe befinden), verwenden Sie stattdessen die DNS-Veröffentlichung.  

> [!NOTE]  
>  Beim Installieren des Clients für Linux und UNIX müssen Sie einen Verwaltungspunkt als ersten Kontaktpunkt angeben. Informationen zu Clientinstallationen für Linux und UNIX finden Sie unter [Bereitstellen von Clients auf UNIX- und Linux-Servern in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Bevor Sie die DNS-Veröffentlichung für Verwaltungspunkte verwenden, müssen Sie sicherstellen, dass bei den DNS-Servern im Intranet Ressourcendatensätze für die Dienstidentifizierung (SRV RR) und entsprechende Ressourcendatensätze für Hosts (A oder AAA) für die Verwaltungspunkte des Standorts vorhanden sind. Die Ressourcendatensätze für die Dienstidentifizierung können mithilfe von Configuration Manager automatisch oder manuell vom DNS-Administrator erstellt werden, der die Datensätze in DNS erstellt.  

 Weitere Informationen zur DNS-Veröffentlichung als Dienstidentifizierungsmethode für Configuration Manager-Clients finden Sie unter [Verstehen, wie Clients Standortressourcen und -dienste für System Center Configuration Manager finden](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 Standardmäßig durchsuchen Clients DNS nach Verwaltungspunkten in ihrer DNS-Domäne. Falls in der Domäne der Clients jedoch keine veröffentlichten Verwaltungspunkte vorliegen, müssen Sie Clients mit einem DNS-Suffix für Verwaltungspunkte manuell konfigurieren. Sie können ein derartiges DNS-Suffix auf Clients entweder während oder nach der Clientinstallation festlegen:  

-   Soll diese Konfiguration während der Clientinstallation vorgenommen werden, konfigurieren Sie die Eigenschaften der Datei „CCMSetup Client.msi“.  

-   Zum Festlegen eines Verwaltungspunktsuffixes auf Clients nach der Clientinstallation, konfigurieren Sie die **Configuration Manager-Eigenschaften**in der Systemsteuerung.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>So konfigurieren Sie Clients während der Clientinstallation für ein Verwaltungspunktsuffix  

-   Installieren Sie den Client mit der folgenden „CCMSetup Client.msi“-Eigenschaft:  

    -   **DNSSUFFIX=** *&lt;Verwaltungspunktdomäne\>*  

         Wenn der Standort über mehrere Verwaltungspunkte verfügt und diese sich in verschiedenen Domänen befinden, geben Sie nur eine Domäne an. Beim Herstellen einer Verbindung zwischen Clients und einem Verwaltungspunkt in dieser Domäne wird eine Liste der verfügbaren Verwaltungspunkte heruntergeladen. Darin sind auch die Verwaltungspunkte in den anderen Domänen enthalten.  

     Weitere Informationen zur Befehlszeileneigenschaft „CCMSetup“ finden Sie unter [Informationen zu Clientinstallationseigenschaften in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>So konfigurieren Sie Clients nach der Clientinstallation für ein Verwaltungspunktsuffix  

1.  Doppelklicken Sie in der Systemsteuerung des Clientcomputers unter **Configuration Manager**auf **Eigenschaften**.  

2.  Geben Sie auf der Registerkarte **Standort** das DNS-Suffix eines Verwaltungspunkts an, und klicken Sie dann auf **OK**.  

     Wenn der Standort über mehrere Verwaltungspunkte verfügt und diese sich in verschiedenen Domänen befinden, geben Sie nur eine Domäne an. Beim Herstellen einer Verbindung zwischen Clients und einem Verwaltungspunkt in dieser Domäne wird eine Liste der verfügbaren Verwaltungspunkte heruntergeladen. Darin sind auch die Verwaltungspunkte in den anderen Domänen enthalten.
