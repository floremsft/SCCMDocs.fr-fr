---
title: "Lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) | Microsoft-Dokumentation"
description: "Erfahren Sie mehr über die lokale Verwaltung mobiler Geräte – eine Geräteverwaltungslösung in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
caps.latest.revision: "8"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 7b96c4d4d87aa150eacc5d7d20710f5d2199e48a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>Lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Die lokale Verwaltung mobiler Geräte mit System Center Configuration Manager ist eine Geräteverwaltungslösung, die mit den integrierten Verwaltungsfunktionen von Gerätebetriebssystemen (basierend auf dem Standard OMA DM (Open Mobile Alliance Device Management)) arbeitet und die Configuration Manager-Infrastruktur eines Unternehmens zum Verwalten und Warten der Geräte nutzt. Für die lokale Verwaltung mobiler Geräte wird Microsoft Intune benötigt, um Verwaltungsfunktionen einzurichten. Dies ist allerdings nur für das Abonnement erforderlich und um gelegentlich Geräte bei Richtlinienänderungen einzuchecken. Die Funktionen werden nicht für die Verwaltung der Geräte verwendet oder um Daten über sie zu speichern.  

 ![Lokale Verwaltung – Konzepte](media/On-premises-conceptual.png)  

 Die lokale Verwaltung mobiler Geräte unterscheidet sich von Microsoft Intune, das auch mit den integrierten OMA DM-Funktionen arbeitet, wobei alle Verwaltungsfunktionen von Clouddiensten bereitgestellt werden.  Die lokale Verwaltung mobiler Geräte unterscheidet sich zudem von der von Configuration Manager angebotenen herkömmlichen clientbasierten Verwaltungslösung insofern, als mit einer vergleichbaren Unternehmensinfrastruktur gearbeitet wird, jedoch keine separat installierte Clientsoftware auf den verwalteten Computern und Geräten verwendet wird.  

 In der folgenden Tabelle sehen Sie die Vor- und Nachteile der lokalen Verwaltung mobiler Geräte im Vergleich mit einer herkömmlichen clientbasierten Verwaltung:  

|Vorteile|Nachteile|  
|----------------|-------------------|  
|**Vereinfachte Infrastruktur** : Weniger Standortsystemrollen sind erforderlich.<br /><br /> **Einfacher zu verwalten**: Da Verwaltungsfunktionalität in das Gerätebetriebssystem integriert ist, sind keine neuen Versionen der Clientsoftware erforderlich, wenn neue Verwaltungsfunktionen in das Configuration Manager-System eingeführt werden.<br /><br /> **Lokal** : Die gesamte Verwaltung und alle Daten bleiben lokal.|**Weniger Clientverwaltungsfunktionen** : Keine Orchestrierung, Softwaremessung, Integration von Drittanbietern, Tasksequenzen oder Softwarecenterunterstützung.<br /><br /> **Eingeschränkte Unterstützung für Geräte**: Derzeit werden bei der lokalen Verwaltung mobiler Geräte nur Geräte mit Windows 10 und Windows 10 Mobile unterstützt.|  

 Die folgenden Themen bieten Informationen zum Planen, Vorbereiten und Registrieren von mobilen Geräten für die lokale Verwaltung:  

-   [Planen der lokalen Verwaltung mobiler Geräte in System Center Configuration Manager](../plan-design/plan-on-premises-mdm.md)  

     Erfahren Sie, was bei der Einrichtung der Configuration Manager-Infrastruktur und Planung der Geräteregistrierung für die lokale Verwaltung mobiler Geräte berücksichtigt werden muss.  

-   [Vorbereitungsschritte für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Erfahren Sie, wie Sie das Configuration Manager-System für die lokale Verwaltung mobiler Geräte vorbereiten, indem Sie das Microsoft Intune-Abonnement und Zertifikate einrichten, die Standortsystemrollen installieren und die Geräteregistrierung einrichten.  

-   [Registrieren von Geräten für die lokale Verwaltung mobiler Geräte in System Center Configuration Manager](../deploy-use/enroll-devices-on-premises-mdm.md)  

     Erfahren Sie, wie die Registrierung erfolgt, wie Benutzer ihre eigenen Geräte registrieren können und wie die Massenregistrierung von Geräten mithilfe eines Registrierungspakets stattfindet.  
