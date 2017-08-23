---
title: "Ausschließen von Clientupgrades | Windows |System Center Configuration Manager"
description: "Erfahren Sie, wie Sie Windows-Clients in System Center Configuration Manager von der Aktualisierung ausschließen."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: de5602179f3ac55b51133b8280a0143f1b0ff30e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>Ausschließen von Clientupgrades für Windows-Computer in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab Version 1610 können Sie eine Clientsammlung von der automatischen Installation aktualisierter Clientversionen ausschließen. Dies gilt sowohl für automatische Upgrades und als auch für andere Methoden, wie Upgrades auf der Basis von Softwareupdates, Registrierungsskripts und Gruppenrichtlinien. Sie können dies für eine Sammlung von Computern nutzen, bei der bei einem Upgrade des Clients größere Sorgfalt notwendig ist. Ein Client, der sich in einer ausgeschlossenen Sammlung befindet, ignoriert Anforderungen zur Installation von aktualisierter Clientsoftware.

## <a name="configure-exclusion-for-automatic-upgrades"></a>Konfigurieren des Ausschlusses automatischer Upgrades

1. Gehen Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und klicken Sie anschließend auf **Hierarchieeinstellungen**.

2. Klicken Sie auf die Registerkarte **Client Upgrade** (Clientupgrade).

3. Klicken Sie auf das Kontrollkästchen **Exclude specified clients from upgrade** (Angegebene Clients aus Upgrades ausschließen), und wählen Sie für die Ausschlusssammlung die Sammlung aus, die Sie ausschließen möchten. Sie können nur eine einzelne Sammlung für den Ausschluss auswählen.

4.  Klicken Sie auf **OK**, um die Konfiguration zu schließen und zu speichern. Nachdem die Clients Richtlinien aktualisiert haben, können Clients in der ausgeschlossenen Sammlung nicht mehr automatisch Updates der Clientsoftware installieren. Weitere Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer](upgrade-clients-for-windows-computers.md).

![Einstellungen für automatische Ausschlüsse aus Upgrades](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>Obwohl die Benutzeroberfläche angibt, dass Upgrades für Clients nicht mit einer beliebigen Methode durchgeführt werden können, gibt es zwei Methoden, die Sie verwenden können, um diese Einstellungen außer Kraft zu setzen. Die Clientpushinstallation und eine manuelle Clientinstallation können verwendet werden, um diese Konfiguration außer Kraft zu setzen. Weitere Details erfahren Sie im nächsten Abschnitt.

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>So führen Sie für einen Client in einer ausgeschlossenen Sammlung ein Upgrade durch

Solange eine Sammlung für den Ausschluss konfiguriert ist, können Mitglieder dieser Sammlung ihre Clientsoftware nur mit einer der beiden Methoden, die den Ausschluss außer Kraft setzen, upgegradet werden:
 - **Clientpushinstallation** – Sie können die Clientpushinstallation verwenden, um einen Client in einer ausgeschlossen Sammlung upzugraden. Dies ist zulässig, da es als Absicht des Administrators betrachtet wird und Ihnen ermöglicht, Clients upzugraden, ohne die gesamte Sammlung aus der Ausschlussliste zu entfernen.       

 - **Manuelle Clientinstallation** – Sie können Clients in einer ausgeschlossenen Sammlung unter Verwendung des Befehlszeilenschalters ***/ignoreskipupgrade*** mit ccmsetup manuell upgraden.

  Wenn Sie versuchen, einen Client, der Mitglied der ausgeschlossenen Sammlung ist, manuell upzugraden, und diesen Schalter nicht verwenden, wird der Client die neue Clientsoftware nicht installieren. Weitere Informationen finden Sie unter [Manuelles Installieren von Configuration Manager-Clients](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

Weitere Informationen zu Clientinstallationsmethoden finden Sie unter [Bereitstellen von Clients auf Windows-Computern in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).
