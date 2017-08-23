---
title: "Registrieren von unternehmenseigenen Geräten – Configuration Manager | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über verschiedene Methoden für die Registrierung unternehmenseigener Geräte für Hybridbereitstellungen mit Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
caps.latest.revision: "13"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f0b503d8c9eba2dd1b6eb4c41ec40c001b727326
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Registrieren von unternehmenseigenen Geräten für Hybridbereitstellungen mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Organisations- oder unternehmenseigene Geräte (COD) können mit einer Vielzahl von Methoden verwaltet werden, die vom Gerät und der Erwerbsart abhängen.  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Registrieren von iOS-Geräten des Programms zur Geräteregistrierung  
 Stellt ein „drahtloses“ Registrierungsprofil für Geräte, die über das Geräteregistrierungsprogramm von Apple erworben wurden, bereit. Wenn der Benutzer den Setup-Assistenten auf dem Gerät ausführt, wird das Gerät in Intune registriert.  Die Registrierung von Geräten über DEP kann von Benutzern nicht rückgängig gemacht werden. Siehe [iOS-Registrierung im Programm zur Geräteregistrierung (Device Enrollment Program, DEP) für die Hybridbereitstellung mit Configuration Manager](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md).  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Registrieren von iOS-Geräten mit Apple Configurator  
 Bei dieser Methode muss der Administrator eine USB-Verbindung zwischen dem iOS-Gerät und einem Macintosh-Computer mit Apple Configurator herstellen, um die Registrierung vorzukonfigurieren. Die Geräte werden dann an ihre Benutzer übergeben, die den Setup-Assistenten ausführen, das Gerät mit ihren Geschäfts-, Uni- oder Schulanmeldeinformationen konfigurieren und den Registrierungsprozess abschließen. Siehe [iOS-Hybridregistrierung mithilfe von Apple Configurator mit Configuration Manager](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md).  

## <a name="device-enrollment-manager"></a>Geräteregistrierungsmanager  
 Mit Intune können Organisationen eine Vielzahl mobiler Geräte mit einem einzelnen Benutzerkonto, auch Geräteregistrierungsmanager genannt, verwalten. Nach dem Erstellen eines Geräteregistrierungsmanager-Kontos kann dieses Konto von einem Manager verwendet werden, um mehr als die fünf Standardgeräte, die für normale Benutzer standardmäßig zulässig sind, zu registrieren. Das Registrieren von Geräten mit einem Geräteregistrierungsmanager funktioniert nur bei Geräten, die nicht von einem bestimmten Benutzer verwendet werden. Diese Geräte sind z.B. gut für POS- oder -Dienstprogramm-Apps, aber schlecht für Benutzer, die Zugriff auf E-Mails oder Unternehmensressourcen benötigen. Siehe [Geräte mit dem Geräteregistrierungsmanager mit Configuration Manager registrieren](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md).  

## <a name="user-affinity-for-managed-devices"></a>Benutzeraffinität für verwaltete Geräte  
 Beim Konfigurieren von Profilen für unternehmenseigene Geräte kann der Administrator angeben, ob die verwalteten Geräte *Benutzeraffinität* unterstützen. Damit werden bestimmte Benutzer mit dem Gerät identifiziert. Auf mit **user affinity** konfigurierten Geräten kann die Unternehmensportal-App installiert und ausgeführt werden, um Apps herunterzuladen und Geräte zu verwalten. Siehe [Benutzeraffinität für hybridverwaltete Geräte in Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

## <a name="manage-devices-with-activation-lock"></a>Verwalten von Geräten mit Aktivierungssperre  
 Microsoft Intune kann Sie beim Verwalten der iOS-Aktivierungssperre unterstützen. Dies ist ein Feature der App „Mein iPhone suchen“ für iOS 7.1 und höher. Die Aktivierungssperre wird automatisch aktiviert, wenn die iPhone-App „Mein iPhone suchen“ auf einem Gerät verwendet wird. Siehe [iOS-Aktivierungssperre mit System Center Configuration Manager verwalten](../../mdm/deploy-use/manage-ios-activation-lock.md).

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Vorabdeklarieren von Geräten mit IMEI- oder iOS-Seriennummern

Sie können unternehmenseigene Geräte identifizieren, indem Sie deren IMEI-Nummern (International Station Mobile Equipment Identity) oder iOS-Seriennummern importieren. Sie können eine CSV-Datei (comma-separated values, durch Trennzeichen getrennte Datei) hochladen, die die IMEI-Nummern der Geräte enthält, oder Geräteinformationen manuell eingeben.  Siehe [Vorabdeklarieren von Geräten mit Hardware-ID-Nummern](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).
