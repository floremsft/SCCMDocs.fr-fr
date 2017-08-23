---
title: "Voraussetzungen für E-Mail-Profile | Microsoft-Dokumentation"
description: "Hier finden Sie Informationen zu E-Mail-Profilen in System Center Configuration Manager sowie zu den entsprechenden externen Abhängigkeiten und Abhängigkeiten innerhalb des Produkts."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 451317db1d7aab888c03d1a099b9ce25311e06d0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="email-profile-prerequisites"></a>Voraussetzungen für E-Mail-Profile

*Gilt für: System Center Configuration Manager (Current Branch)*

E-Mail-Profile in System Center Configuration Manager weisen externe Abhängigkeiten sowie Abhängigkeiten innerhalb des Produkts auf.  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Für die Verwaltung von E-Mail-Profilen sind spezielle Sicherheitsberechtigungen erforderlich.|Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um Einstellungen für den Zugriff auf Unternehmensressourcen wie z. B. E-Mail-Profile zu verwalten:<br /><br /> - So zeigen Sie Warnungen und Berichte für E-Mail-Profile an und verwalten sie: Berechtigung **Erstellen**, **Löschen**, **Ändern**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Warnungen**.<br /><br /> - So erstellen und verwalten Sie Zertifikatprofile: Berechtigung **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Zertifikatprofil**.<br /><br /> - So verwalten Sie Bereitstellungen von E-Mail-Profilen: **Konfigurationsrichtlinien bereitstellen**, **Warnung zu Clientstatus ändern**, **Lesen** und **Ressource lesen** für das Objekt **Sammlung**.<br /><br /> - So verwalten Sie alle Konfigurationsrichtlinien: Berechtigung **Erstellen**, **Löschen**, **Ändern**, **Lesen** und **Sicherheitsbereich festlegen** für das Objekt **Konfigurationsrichtlinie**.<br /><br /> - So führen Sie mit E-Mail-Profilen verknüpfte Abfragen aus: Berechtigung **Lesen** für das Objekt **Abfrage**.<br /><br /> - So zeigen Sie E-Mail-Profilinformationen in der System Center Configuration Manager-Konsole an: Berechtigung **Lesen** für das Objekt **Standort**.<br /><br /> - So zeigen Sie Statusmeldungen für E-Mail-Profile an: Berechtigung **Lesen** für das Objekt **Statusmeldungen**.<br /><br /> - So erstellen und verwalten Sie E-Mail-Profile: Berechtigung **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Profil zur Kommunikationsvermittlung**.<br /><br /> In der Sicherheitsrolle **Zugriffs-Manager für Unternehmensressourcen** sind diese Berechtigungen zum Verwalten der E-Mail-Profile in System Center Configuration Manager enthalten. Weitere Informationen finden Sie unter [Configure security in System Center Configuration Manager (Konfigurieren der Sicherheit in System Center Configuration Manager)](../../core/plan-design/security/configure-security.md).|  
|Mail-Attribut in Active Directory|Wenn Sie E-Mail-Adressen von Benutzern in einem E-Mail-Profil mithilfe der primären SMTP-Adresse des Benutzers generieren möchten, muss die System Center Configuration Manager-Benutzerermittlung so konfiguriert sein, dass sie das **mail**-Attribut von Active Directory ermitteln kann (dies ist standardmäßig konfiguriert).|  

## <a name="external-dependencies"></a>Externe Abhängigkeiten  

|Abhängigkeit|Weitere Informationen|  
|----------------|----------------------|  
|Mail-Attribut in Active Directory|Wenn Sie E-Mail-Adressen von Benutzern in einem E-Mail-Profil mithilfe der primären SMTP-Adresse des Benutzers generieren möchten, muss diese Adresse im **mail**-Attribut in Active Directory enthalten sein.<br /><br /> Weitere Informationen finden Sie in der Windows Server-Dokumentation.|
