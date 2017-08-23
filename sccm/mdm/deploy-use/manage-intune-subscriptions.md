---
title: Verwalten Ihres Intune-Abonnements, das System Center Configuration Manager zugeordnet ist | Microsoft-Dokumentation
description: Verwalten Ihres Intune-Abonnements, das System Center Configuration Manager zugeordnet ist.
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 2cb4d724c8b78657458a30c0bb020f67c6b62795
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Verwalten Ihres Intune-Abonnements, das System Center Configuration Manager zugeordnet ist

*Gilt für: System Center Configuration Manager (Current Branch)*

Wenn Sie Configuration Manager ein Microsoft Intune-Abonnement (Testabonnement oder kostenpflichtiges Abonnement) hinzufügen und dann zu einem anderen Intune-Abonnement wechseln müssen, müssen Sie sowohl das **Microsoft Intune-Abonnement** als auch den **Dienstverbindungspunkt** aus der Configuration Manager-Konsole löschen, bevor Sie ein neues Abonnement hinzufügen können.

> [!NOTE]
> Sie können jeweils nur ein Intune-Abonnement in der hybriden Verwaltung mobiler Geräte konfigurieren.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Löschen eines Intune-Abonnements aus Configuration Manager

> [!IMPORTANT]
>  Alle Inhalte, einschließlich Benutzerregistrierungen, Richtlinien und App-Bereitstellungen, die für Geräte konfiguriert sind, die vom Intune-Abonnement verwaltet werden, werden beim Löschen des Abonnements entfernt.

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Übersicht** > **Clouddienste** > **Microsoft Intune-Abonnements** aus.

2.  Klicken Sie mit der rechten Maustaste auf das aufgeführte **Microsoft Intune-Abonnement**, und klicken Sie anschließend auf **Löschen**.

3.   Klicken Sie im Assistenten auf **Microsoft Intune-Abonnement aus Configuration Manager entfernen**, klicken Sie auf **Weiter**, und klicken Sie anschließend erneut auf **Weiter**, um das Abonnement zu entfernen.


## <a name="how-to-remove-the-service-connection-point-role"></a>So entfernen Sie die Rolle „Dienstverbindungspunkt“

1.  Wechseln Sie zu **Verwaltung** > **Übersicht** > **-Standortkonfiguration** > **Server und Standortsystemrollen**.

2.  Wählen Sie den Server aus, auf dem die Rolle **Dienstverbindungspunkt** gehostet wird.

3.  Wählen Sie in der Liste **Standortsystemrollen** die Option **Dienstverbindungspunkt** aus, und klicken Sie anschließend im Menüband auf **Rolle entfernen**. Bestätigen Sie, dass Sie die Rolle entfernen möchten. Der Dienstverbindungspunkt wird gelöscht.

Sie können jetzt einen neuen Dienstverbindungspunkt erstellen, Configuration Manager ein neues Intune-Abonnement hinzufügen und Configuration Manager als MDM-Autorität festlegen.

## <a name="how-to-change-mdm-authority-to-intune"></a>So stellen Sie die MDM-Autorität auf Intune um
Ab Configuration Manager, Version 1610, und Microsoft Intune, Version 1705, können Sie Ihre MDM-Autorität ohne Unterstützung durch den Microsoft-Support und ohne Aufheben der Registrierung und erneutes Registrieren Ihrer vorhandenen verwalteten Geräte umstellen. Einzelheiten finden Sie unter [Umstellen der MDM-Autorität](/sccm/mdm/deploy-use/change-mdm-authority).
