---
title: "Hybride Mobilgeräteverwaltung (MDM) – Configuration Manager & Microsoft Intune | Microsoft-Dokumentation"
description: "Enthält Informationen zur hybriden Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: "34"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e54478a03807c939ffa64ff39a21ef6f9ea4ae2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Hybride Verwaltung mobiler Geräte (Mobile Device Management, MDM) mit System Center Configuration Manager und Microsoft Intune

*Gilt für: System Center Configuration Manager (Current Branch)*


Sie können iOS, Windows und Android-Geräte mit Configuration Manager und Microsoft Intune verwalten. Alle Verwaltungsaufgaben werden aus der Configuration Manager-Konsole heraus verarbeitet, in der Sie die restlichen Verwaltungstasks ausführen, die über das Internet nahtlos in den Microsoft Intune-Onlinedienst integriert sind.  Sie können Configuration Manager so verwenden, dass Benutzer auf sichere und verwaltete Weise auf Unternehmensressourcen auf ihren Geräten zugreifen können. Mithilfe der Geräteverwaltung schützen Sie Unternehmensdaten, und ermöglichen es den Benutzern gleichzeitig, ihre privaten oder im Besitz des Unternehmens befindlichen Geräte anzumelden, um auf Unternehmensdaten zuzugreifen. Verwaltungsfunktionen auf Geräten:

-   Abkoppeln und Zurücksetzen von Geräten
-   Konfigurieren von Kompatibilitätseinstellungen wie Kennwörter, Sicherheit, Roaming, Verschlüsselung und Funkkommunikation
-   Bereitstellen von Branchen-Apps (line-of-business, LOB) auf Geräten
-   Bereitstellen von Apps auf Geräten, die eine Verbindung mit Windows Store, Windows Phone Store, App Store oder Google Play herstellen
-   Erfassen der Hardwareinventur
-   Erfassen der Softwareinventur mithilfe integrierter Berichte

Informationen darüber, welche neuen Funktionen für die hybride Verwaltung mobiler Geräte verfügbar sind, finden Sie unter [What's new in hybrid mobile device management (Neuigkeiten in der hybriden Verwaltung mobiler Geräte)](../understand/whats-new-in-hybrid-mobile-device-management.md).

Im vorliegenden Dokument wird vorausgesetzt, dass Sie Computer mithilfe von Configuration Manager verwalten und beabsichtigen, die Configuration Manager-Konsole mit Intune zu erweitern, um mobile Geräte zu verwalten. Die Unterschiede zwischen Intune und der hybriden Verwaltung mobiler Geräte finden Sie unter [Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager (Auswahl zwischenMicrosoft Intune standalone und hybrider Verwaltung mobiler Geräte mit System Center Configuration Manager)](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Nach dem Erweitern von Configuration Manager mit Intune können Sie unternehmenseigene Geräte registrieren und verwalten, oder Benutzern die Berechtigung zum Registrieren ihrer persönlichen Geräte erteilen. Mithilfe von Configuration Manager können Sie auch unternehmenseigene Geräte mit Intune verwalten.

## <a name="hybrid-mdm-enrollment"></a>Hybrid-MDM-Registrierung
Um Geräte hybrid zu verwalten, müssen diese Geräte zuerst mit dem Dienst registriert werden. Auf welche Weise Geräte registriert werden, hängt von Gerätetyp, Besitz und benötigtem Verwaltungsniveau ab.
- Bei der BYOD-Registrierung (Bring Your Own Device, private Geräte der Mitarbeiter) können die Benutzer ihre privaten Smartphones, Tablets oder PCs selbst registrieren.
- Die COD-Registrierung (Corporate-Owned Device, Firmeneigene Geräte) ermöglicht Verwaltungsszenarios wie das Remotezurücksetzen, gemeinsam verwendete Geräte oder Benutzeraffinität für ein Gerät.
- Wenn Sie [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager) entweder lokal oder in der Cloud gehostet verwenden, können Sie eine einfache Intune-Verwaltung ohne Registrierung aktivieren. Auch Windows-PCs können mit [Intune-Clientsoftware](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune) verwaltet werden.
