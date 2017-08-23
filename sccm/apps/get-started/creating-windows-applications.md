---
title: Erstellen von Windows-Anwendungen | Microsoft Docs
description: "Erfahren Sie, was Sie beim Erstellen und Bereitstellen von Anwendungen für Windows-Geräte berücksichtigen müssen."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c80cc42f9ce6775067a89a9f5a63c1bf4a0c7ca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Erstellen von Windows-Anwendungen mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Zusätzlich zu den anderen System Center Configuration Manager-Anforderungen und -Verfahren zum Erstellen einer Anwendung müssen beim Erstellen und Bereitstellen von Anwendungen für Windows-Geräte auch die folgenden Aspekte berücksichtigt werden.  

## <a name="general-considerations"></a>Allgemeine Aspekte  
 Configuration Manager unterstützt die Bereitstellung folgender App-Dateitypen:  

|Gerätetyp|Unterstützte Dateitypen|  
|-----------------|---------------------|  
|Windows RT und Windows RT 8.1|*.appx, \*.appxbundle|  
|Windows 8.1 und höher, als mobiles Gerät registriert|*.appx, \*.appxbundle|  

 Die folgenden Bereitstellungsaktionen werden unterstützt:  

|Gerätetyp|Unterstützte Aktionen|  
|-----------------|-----------------------|  
|Windows 8.1 und höher|Verfügbar, Erforderlich, Deinstallieren|  
|Windows RT|Verfügbar, Erforderlich, Deinstallieren|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>Unterstützung für UWP-Apps (Universelle Windows-Plattform)  
 Windows 10-Geräte erfordern keinen Sideload-Schlüssel für die Installation von Branchen-Apps. Allerdings muss der Registrierungsschlüssel **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** den Wert 1 haben, um das Querladen zu aktivieren.  

 Wenn dieser Registrierungsschlüssel nicht konfiguriert ist, legt Configuration Manager diesen Wert automatisch auf **1** fest, wenn Sie zum ersten Mal eine App auf dem Gerät bereitstellen. Wenn Sie diesen Wert auf **0**festgelegt haben, kann Configuration Manager den Wert nicht automatisch ändern, und bei der Bereitstellung von branchenspezifischen Apps tritt ein Fehler auf.  

 UWP-Branchen-Apps (Universal Windows Platform) müssen mit einem codesignierten Zertifikat signiert sein, das auf jedem Gerät, auf dem die App bereitgestellt ist, als vertrauenswürdig eingestuft ist. Sie können Zertifikate aus einer internen PKI-Infrastruktur verwenden oder ein Zertifikat von einer öffentlichen Drittanbieter-Stammzertifizierungsstelle, das auf dem Gerät installiert ist.  

 Auf Windows 10 Mobile-Geräten können Sie ein nicht von Symantec stammendes Codesignaturzertifikat zum Signieren universeller **APPX** -Apps verwenden. Für **XAP** -apps sowie für **APPX** -Pakete, die für Windows Phone 8.1 erstellt wurden, die Sie auf Windows 10 Mobile-Geräten installieren möchten, müssen Sie ein Codesignaturzertifikat von Symantec verwenden.  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>Bereitstellen von Windows Installer-Apps auf registrierten Windows 10-PCs  
 Mit dem Installertyp **Windows Installer über MDM (\*.msi)** können Sie Windows Installer-basierte Apps auf registrierten Geräten unter Windows 10 erstellen und bereitstellen.  

 Folgendes muss berücksichtigt werden, wenn Sie diese Art Installationsprogramm verwenden:  

-   Sie können nur eine einzelne Datei mit der Erweiterung ".msi" hochladen.  

-   Produktcode und Produktversion der Datei werden zur Erkennung der App verwendet.  

-   Es wird das standardmäßige Verhalten bei Neustart der App verwendet. Dies wird nicht von Configuration Manager gesteuert.  

-   Pro Benutzer definierte MSI-Pakete werden für einen einzelnen Benutzer installiert.  

-   Pro Gerät definierte MSI-Pakete werden für alle Benutzer des Geräts installiert.  

-   App-Updates werden unterstützt, wenn jede Version den gleichen MSI-Produktcode aufweist.  
