---
title: "Geräteregistrierungsmethoden für die hybride Verwaltung mobiler Geräte | Microsoft-Dokumentation"
description: "Geräteregistrierungsmethoden für die hybride Verwaltung mobiler Geräte."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e09e639e939b846cdc162681f9d7bd4c39cd6fbf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="overview-of-device-enrollment-methods"></a>Übersicht über die Geräteregistrierungsmethoden

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachdem Sie Configuration Manager mit Intune erweitern, können Sie unternehmenseigene Geräte registrieren und verwalten oder Benutzern die Berechtigung zum Registrieren ihrer persönlichen Geräte erteilen. Mithilfe von Configuration Manager können Sie auch unternehmenseigene Geräte mit Intune verwalten.

In der folgenden Tabelle werden die Registrierungsmethoden zusammen mit den von ihnen unterstützten Funktionen dargestellt. Diese Funktionen beinhalten:
- **Zurücksetzen** – Zurücksetzen des Geräts auf Werkseinstellungen, wobei alle Daten entfernt werden. [Geräte abkoppeln](../deploy-use/wipe-lock-reset-devices.md)
- **Affinität** – Ordnet Geräte Benutzern zu. Für die Verwaltung mobiler Anwendungen (Mobile Application Management, MAM) und den bedingten Zugriff auf Unternehmensdaten erforderlich. [Benutzeraffinität](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Sperre** – Hindert Benutzer daran, das Gerät aus der Verwaltung zu entfernen. Für iOS-Geräte ist der überwachte Modus für die Sperre erforderlich. [Remotesperre](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**iOS-Registrierungsmethoden**

| **Methode** |  **Zurücksetzen** |  **Affinität**    |   **Sperren** | **Details** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Nein|    Ja |   Nein | [Mehr](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|   Nein |Nein |Nein  | [Mehr](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Ja |   Optional |  Optional|[Mehr](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB (Setup-Assistent)](#usb-sa)**| Ja |   Optional |  Nein| [Mehr](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows und Android-Registrierungsmethoden**

| **Methode** |  **Zurücksetzen** |  **Affinität**    |   **Sperren** | **Details**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Nein|    Ja |   Nein | [Mehr](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**|   Nein |Nein |Nein  |[Mehr](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Eine Reihe von Fragen, die Sie beim Ermitteln der richtigen Methode unterstützen, finden Sie unter [Auswählen der Registrierungsart von Geräten](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
BYOD-Benutzer („Bring your own device“) installieren die Unternehmensportal-App und registrieren ihr Gerät. Dies erlaubt Benutzern, Verbindungen mit dem Unternehmensnetzwerk herzustellen, und zur Domäne oder zu Azure Active Directory beizutreten. Das Aktivieren der BYOD-Registrierung ist eine Voraussetzung für viele COD-Szenarios der meisten Plattformen. Siehe [Einrichten der hybriden Verwaltung mobiler Geräte](../deploy-use/setup-hybrid-mdm.md). ([Zurück zur Tabelle](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Unternehmenseigene Geräte
Unternehmenseigene Geräte (Corporate-owned devices, COD) können mit der Configuration Manager-Konsole verwaltet werden. iOS-Geräte können direkt über die von Apple bereitgestellten Tools registriert werden. Alle Gerätetypen können von einem Administrator oder Manager die unter Verwendung des Geräteregistrierungs-Managers registriert werden. Geräte mit einer IMEI-Nummer können auch als firmeneigene Geräte identifiziert und gekennzeichnet werden, um COD-Szenarios zu unterstützen.

[Registrieren firmeneigener iOS-Geräte](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>Geräteregistrierungs-Manager (DEM)
Der Geräteregistrierungs-Manager ist ein besonderes Benutzerkonto, das zum Registrieren und Verwalten mehrerer firmeneigener Geräte verwendet wird. Manager können das Unternehmensportal installieren und viele benutzerlose Geräte registrieren. Erfahren Sie mehr über [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Zurück zur Tabelle](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP (Device Enrollment Program)
Mit der Apple DEP-Verwaltung (Device Enrollment Program, Programm zur Geräteregistrierung) können Sie Richtlinien erstellen und „drahtlos“ auf iOS-Geräten bereitstellen, die mit DEP erworben wurden und verwaltet werden. Das Gerät wird beim ersten Einschalten durch den Benutzer registriert und führt dann den iOS-Setup-Assistenten aus. Diese Methode unterstützt den iOS-Modus **Überwacht**, der wiederum Folgendes ermöglicht:
  - Gesperrte Registrierung
  - Bedingter Zugriff
  - Erkennung von Jailbreaks
  - Mobile Anwendungsverwaltung

Erfahren Sie mehr über das [Geräteregistrierungsprogramm](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Zurück zur Tabelle](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB (Setup-Assistent)
Über USB verbundene Registrierung mit Setup-Assistent. Der Administrator erstellt eine Richtlinie, und exportiert sie nach Apple Configurator. Über USB angeschlossene, unternehmenseigene Geräte werden mit der Richtlinie vorbereitet. Der Administrator muss jedes Gerät per Hand registrieren. Benutzer erhalten ihre Geräte und führen den Setup-Assistenten aus, um ihr Gerät zu registrieren. Diese Methode unterstützt den iOS-Modus **Überwacht**, der wiederum Folgendes ermöglicht:
  - Bedingter Zugriff
  - Erkennung von Jailbreaks
  - Mobile Anwendungsverwaltung

Erfahren Sie mehr über die [Setup Assistant enrollment with Apple Configurator (Registrierung über den Setup-Assistenten mit Apple Configurator)](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Zurück zur Tabelle](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Verwaltung mobiler Geräte mit Exchange ActiveSync und Configuration Manager
Mobile Geräte, die nicht registriert, aber mit Exchange ActiveSync (EAS) verbunden sind, können von Intune mit der MDM EAS-Richtlinie verwaltet werden. Intune verwendet Exchange Connector für die Kommunikation mit EAS, entweder lokal oder in der Cloud gehostet.

[Verwaltung mobiler Geräte mit Exchange ActiveSync und Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
