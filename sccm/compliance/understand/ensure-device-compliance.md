---
title: "Sicherstellen der Gerätekonformität | Microsoft-Dokumentation"
description: "Mithilfe von System Center Configuration Manager verwalten Sie die Konfiguration und die Kompatibilität von Geräten in Ihrer Organisation."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7568c9aa-b99e-4466-bfc8-0301aa376930
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f7ecfe550d2e28579ea873442b2a68dc1c7c5483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="ensure-device-compliance-with-system-center-configuration-manager"></a>Sicherstellen der Gerätekompatibilität mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Kompatibilitätseinstellungen in System Center Configuration Manager bieten Ihnen die Tools und Ressourcen, die Sie benötigen, um die Konfiguration und Kompatibilität von Geräten in Ihrer Organisation verwalten zu können. Damit können Sie die folgenden Geschäftsanforderungen umsetzen:  

-   Vergleichen der Konfiguration von Windows-PCs, Macintosh-Computern, Servern und mobilen Geräten, die Sie verwalten, mit bewährten Konfigurationen, die Sie erstellt oder von anderen Herstellern bekommen haben  

-   Erkennen von nicht autorisierten Gerätekonfigurationen  

-   Melden der Kompatibilität mit vorgeschriebenen Richtlinien und internen Sicherheitsrichtlinien  

-   Erkennen von Sicherheitsrisiken  

-   Bereitstellen von Informationen für den Helpdesk, damit mögliche Ursachen von gemeldeten Vorfällen und Problemen durch Identifizieren von nicht kompatiblen Konfigurationen erkannt werden können  

-   Automatisches Beheben von einigen nicht kompatiblen Einstellungen auf mobilen Geräten  

-   Beseitigen der Nichtkompatibilität durch Bereitstellen von Anwendungen, Paketen, Programmen oder Skripts für eine Sammlung, die automatisch mit Geräten aufgefüllt wird, von denen eine Nichtkompatibilität gemeldet wird  


## <a name="get-started"></a>Erste Schritte  
 Lernen Sie die Grundlagen von Kompatibilitätseinstellungen und die Aufgaben kennen, die Sie damit ausführen können.  

 [Erste Schritte mit Kompatibilitätseinstellungen](../../compliance/get-started/get-started-with-compliance-settings.md)  

## <a name="plan-and-design"></a>Planung und Entwurf  
 Stellen Sie vor Beginn der Arbeit mit Kompatibilitätseinstellungen sicher, dass die in diesem Thema beschriebenen Voraussetzungen erfüllt sind.  

 [Planen und Konfigurieren von Kompatibilitätseinstellungen](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

## <a name="common-tasks"></a>Gängige Tasks  
 In diesem Abschnitt finden Sie einige gängige Szenarios, mit denen gezeigt wird, wie Kompatibilitätseinstellungen in Configuration Manager verwendet werden.  

 [Allgemeine Tasks zur Verwaltung der Kompatibilität](../../compliance/plan-design/common-tasks-for-managing-compliance.md)  

## <a name="remote-connection-profiles"></a>Remoteverbindungsprofile  
 Dieser Konfigurationselementtyp ermöglicht Ihnen das Konfigurieren der PCs Ihrer Benutzer für das Herstellen von Remoteverbindungen mit Arbeitscomputern, wenn keine Verbindung mit der Domäne besteht oder ihre PCs über das Internet verbunden sind.  

 [Erstellen von Remoteverbindungsprofilen](/sccm/compliance/deploy-use/create-remote-connection-profiles)  

## <a name="user-data-and-profiles"></a>Benutzerdaten und Profile  
 Dieser Konfigurationselementtyp enthält Einstellungen, mit denen die Ordnerumleitung, Offlinedateien und Roamingprofile auf Windows 8-Computern für Benutzer in Ihrer Hierarchie verwaltet werden können.  

 [Erstellen von Konfigurationselementen für Benutzerdaten und -profile](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)  

## <a name="windows-edition-upgrade-policy"></a>Windows-Upgraderichtlinie für die Edition  
 Die Upgraderichtlinie für die Edition ermöglicht Ihnen ein automatisches Upgrade von Windows 10-Geräten auf eine neuere Version. Sie können einen Product Key für das Upgrade von Windows 10-Desktopversionen oder eine Lizenzdatei angeben, die zum Aktualisieren von Geräten mit Windows 10 Mobile und Windows 10 Holographic verwendet werden kann.  

 [Aktualisieren von Windows-Geräten mithilfe der Upgraderichtlinie für die Edition](/sccm/compliance/deploy-use/upgrade-windows-version)  
