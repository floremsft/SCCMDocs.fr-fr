---
title: Verwalten von Anwendungen in System Center Configuration Manager | Microsoft-Dokumentation
description: Verwalten Sie Anwendungen in System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: bc7bb99bc526ed0bbaaad15fc9af39fa8b7c3893
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>Verwalten von Anwendungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Beim Verwalten von Geräten mit Microsoft Intune oder der lokalen Geräteverwaltung von Configuration Manager können Sie folgende zusätzliche Anwendungstypen verwalten:
- Windows Phone-App-Paket (XAP-Datei)
- App-Paket für iOS (IPA-Datei)
- App-Paket für Android (APK-Datei)
- App-Paket für Android auf Google Play
- Windows Phone-App-Paket (in Windows Phone Store)
- Windows Installer über MDM
- Webanwendung

Dieser Abschnitt enthält ausführliche Informationen zum Erstellen und Verwalten von Anwendungen mithilfe von hybrider oder lokaler MDM-Software.

[Verwaltungstasks für System Center Configuration Manager-Anwendungen](../../apps/deploy-use/management-tasks-applications.md) bietet allgemeine Informationen zum Verwalten von System Center Configuration Manager-Anwendungen und Bereitstellungstypen.

## <a name="deploying-and-monitoring-apps"></a>Bereitstellen und Überwachen von Apps

Bereitstellen und Überwachen von Anwendungen in System Center Configuration Manager sind die gleichen Prozesse sowohl für mobile Geräte als auch für Geräte vor Ort wie Laptops und Desktopcomputer. Sie können für allgemeine Informationen zum Bereitstellen und Überwachen von Anwendungen die folgenden Themen lesen:

- [Bereitstellen von Anwendungen in System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Überwachen von Anwendungen in System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Hier sind einige Punkte, die bei der Bereitstellung und Überwachung von Anwendungen bei der Verwaltung mobiler Geräte beachtet werden müssen.

- MDM-registrierte Geräte unterstützen keine simulierten Bereitstellungen, Einstellungen für Benutzerfreundlichkeit oder Zeitplanung.

- Wenn Sie bereits eine iOS-App-Konfigurationsrichtlinie konfiguriert haben, können Sie die Bereitstellung dieser zuordnen. Weitere Informationen finden Sie unter [Einstellungen anwenden für iOS-Apps mit Konfigurationsrichtlinien](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Nächste Schritte

Nach einiger Zeit möchten Sie möglicherweise Änderungen an einer Anwendung vornehmen, eine Anwendung deinstallieren oder eine bereits bereitgestellte Anwendung durch eine neue Anwendung ersetzen. Weitere Informationen zu diesen Funktionen finden Sie unter [Aktualisieren und Deinstallieren von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md).
