---
title: Verwalten von Bereitstellungen mit hohem Risiko | Microsoft-Dokumentation
description: "Erfahren Sie mehr über das Konfigurieren der Standorteinstellungen in System Center Configuration Manager, um Administratoren zu warnen, wenn sie eine risikoreiche Bereitstellung erstellen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8b5564f39f07a67a3c9278379ed59ca415603d21
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>Einstellungen zum Verwalten risikoreicher Bereitstellungen für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*


Mithilfe von System Center Configuration Manager können Sie Einstellungen an einem Standort konfigurieren, über die Administratoren gewarnt werden, wenn sie eine Bereitstellung mit risikoreicher Tasksequenz erstellen. Eine risikoreiche Bereitstellung ist z. B.:  

-   Eine Bereitstellung, die automatisch installiert wird  

-   Eine Bereitstellung mit potenziell unerwünschten Ergebnissen  

 Beispiel: Eine Tasksequenz, die als Zweck **Erforderlich** aufweist und ein Betriebssystem bereitstellt, wird als hohes Risiko betrachtet.  

 Um das Risiko einer unbeabsichtigten Bereitstellung mit hohem Risiko zu reduzieren, können Sie Größenbeschränkungen in Einstellungen zur Bereitstellungsüberprüfung konfigurieren:  

-   **Grenzwerte für Sammlungsgröße**: Mit dieser Einstellung werden beim Erstellen einer Bereitstellung die Sammlungen ausgeblendet, die mehr Clients als Ihr Grenzwert enthalten.  

    -   **Standardgröße**: Mit dieser Einstellung werden beim Erstellen einer Bereitstellung standardmäßig die Sammlungen ausgeblendet, die mehr Clients als Ihr Grenzwert enthalten. Sie können diese Sammlungen zwar weiterhin beim Erstellen der Bereitstellung anzeigen, doch sind sie standardmäßig ausgeblendet. Der Standardwert ist 100. Geben Sie den Wert 0 ein, um diese Einstellung zu ignorieren.  

    -   **Maximale Größe**: Mit dieser Einstellung werden beim Erstellen einer Bereitstellung immer die Sammlungen ausgeblendet, die mehr Clients als Ihr Grenzwert enthalten. Der Standardwert ist 0, wodurch diese Einstellung ignoriert wird. Der Wert **Maximale Größe** muss größer sein als der Wert **Standardgröße** .  

     Beispiel: Sie legen **Standardgröße** auf 100 und **Maximale Größe** auf 1000 fest. Wenn Sie eine Bereitstellung mit hohem Risiko erstellen, werden im Fenster **Sammlung auswählen** nur die Sammlungen angezeigt, die weniger als 100 Clients enthalten. Wenn Sie die Einstellung **Sammlungen mit einer Anzahl der Mitglieder, die größer als die minimale Größenkonfiguration (Wert) des Standorts ist, ausblenden** deaktivieren, werden im Fenster Sammlungen angezeigt, die weniger als 1000 Clients enthalten.  

-   **Sammlungen mit Standortsystemservern**: Hiermit werden Bereitstellungen blockiert oder eine Überprüfung vor dem Erstellen der Bereitstellung angefordert, wenn die Zielsammlung einen Computer mit einer Standortsystemrolle enthält. Wenn eine Bereitstellung blockiert wird, müssen Sie eine andere Sammlung auswählen, die den Kriterien der Bereitstellungsüberprüfung entspricht.  

> [!NOTE]  
>  Bereitstellungen mit hohem Risiko sind immer auf benutzerdefinierte Sammlungen, von Ihnen erstellte Sammlungen und die integrierte Sammlung **Unbekannte Computer** beschränkt. Beim Erstellen einer Bereitstellung mit hohem Risiko können Sie keine integrierte Sammlung auswählen, wie z. B. **Alle Systeme**.  

### <a name="to-configure-deployment-verification-for-a-site"></a>So konfigurieren Sie die Bereitstellungsüberprüfung für einen Standort  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** >**Standortkonfiguration** > **Standorte** und dann den zu konfigurierenden Standort aus.  

2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** und dann die Registerkarte **Bereitstellungsüberprüfung** aus.  

3.  Nachdem Sie die gewünschte Konfiguration festgelegt haben, wählen Sie **OK** aus, um die Konfiguration zu speichern.  

### <a name="see-also"></a>Weitere Informationen:  
 [Konfigurieren von Standorten und Hierarchien für System Center Configuration Manager](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)
