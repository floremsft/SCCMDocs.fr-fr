---
title: Konfigurieren von Standorten | Microsoft-Dokumentation
description: "Stellen Sie anhand dieser Prüfliste sicher, dass Sie die am häufigsten verwendeten Konfigurationen berücksichtigen, die Standorte und Hierarchien betreffen."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: "15"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 862f420c063cb44c419d4904fbb4696efb739758
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Konfigurieren von Standorten und Hierarchien für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Nachdem Sie Ihren ersten System Center Configuration Manager-Standort installiert und Ihrer Hierarchie weitere Standorte hinzugefügt haben, nutzen Sie die folgende Prüfliste, um sicherzustellen, dass Sie die gängigsten Konfigurationen berücksichtigen, die sich sowohl auf Standorte als auch auf Hierarchien auswirken.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Prüfliste für gängige Konfigurationen neuer und zusätzlicher Standorte  
Beachten Sie die folgenden Hinweise zur Konfiguration, die für die meisten Bereitstellungen gelten:

-   Einige dieser Optionen, wie z.B. die Active Directory-Gesamtstrukturermittlung, Grenzen und Begrenzungsgruppen, bauen aufeinander auf.  

-   Bei verschiedenen Konfigurationen können Sie, zumindest vorübergehend, die Standardwerte ohne Änderungen verwenden.  

-   Andere Konfigurationen, wie z. B. Begrenzungsgruppen und Verteilungspunktgruppen, müssen Sie dagegen konfigurieren, bevor Sie sie verwenden können.  

|Aktion|Details|  
|------------|-------------|  
|Konfigurieren der rollenbasierten Verwaltung|Trennen Sie administrative Zuständigkeiten, um zu steuern, welche Administratoren verschiedene Objekte und Daten in Ihrer Configuration Manager-Umgebung anzeigen und verwalten können.<br /><br /> Konfigurationen der rollenbasierten Verwaltung werden von allen Standorten der Hierarchie gemeinsam genutzt.   <br/><br/>Weitere Informationen finden Sie unter [Configure role-based administration for System Center Configuration Manager (Konfigurieren der rollenbasierten Verwaltung)](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Veröffentlichen von Standortdaten in Active Directory-Domänendienste (AD DS)|Erleichtern Sie Clients das Auffinden von Diensten und das effiziente Verwenden von Standortressourcen.<br /><br /> Sie müssen [das Active Directory-Schema für System Center Configuration Manager zunächst erweitern](../../../../core/plan-design/network/extend-the-active-directory-schema.md) und anschließend jeden Standort einzeln konfigurieren, um [Standortdaten für System Center Configuration Manager zu veröffentlichen](../../../../core/servers/deploy/configure/publish-site-data.md).|  
|Konfigurieren eines Dienstverbindungspunkts|Planen Sie die Installation und Konfiguration des Dienstverbindungspunkts auf der obersten Ebene Ihrer Hierarchie. Weitere Informationen finden Sie unter [Informationen zum Dienstverbindungspunkt in System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Hinzufügen von Standortsystemrollen|Installieren und konfigurieren Sie für einzelne Standorte zusätzliche Standortsystemrollen.  Weitere Informationen finden Sie unter [Hinzufügen von Standortsystemrollen für System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Konfigurieren von Grenzen und Begrenzungsgruppen für Standorte|Geben Sie Grenzen zum Definieren der Netzwerkadressen in Ihrem Intranet an, die Geräte enthalten können, die Sie verwalten möchten. Konfigurieren Sie dann Begrenzungsgruppen, sodass Clients an diesen Netzwerkadressen Configuration Manager-Ressourcen finden können. Weitere Informationen hierzu finden Sie unter [Definieren von Standortgrenzen und Begrenzungsgruppen für Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Konfigurieren von Verteilungspunktgruppen|Konfigurieren Sie logische Gruppen von Verteilungspunkten, um das Verwalten von Bereitstellungen zu vereinfachen. Weitere Informationen hierzu finden Sie im Artikel [Installieren und Konfigurieren von Verteilungspunkten für System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) im Abschnitt [Verwalten von Verteilungspunktgruppen](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).|  
|Ausführen der Ermittlung|Führen Sie die Ermittlung aus, um Ressourcen in Ihrem Netzwerk zu finden, z.B. Netzwerkinfrastruktur, Geräte und Benutzer.<br /><br /> Weitere Informationen finden Sie unter [Ausführen der Ermittlung für System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Hinzufügen von Redundanz und Kapazität für Administratoren Ihrer Infrastruktur|Installieren Sie zusätzliche SMS-Anbieter und Configuration Manager-Konsolen, um Administratoren mehr Kapazität für das Verwalten Ihrer Infrastruktur zu bieten:<br /><br /> **Installieren Sie zusätzliche SMS-Anbieter**, um Redundanz für Kontaktpunkte zur Verwaltung des Standorts und der Hierarchie bereitzustellen. Weiter Informationen hierzu finden Sie im Artikel [Ändern Ihrer System Center Configuration Manager-Infrastruktur](../../../../core/servers/manage/modify-your-infrastructure.md) unter [Verwalten des SMS-Anbieters](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).<br /><br /> **Installieren Sie zusätzliche Configuration Manager-Konsolen** , um weiteren Administratoren Zugriff zu bieten. Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Konsolen](../../../../core/servers/deploy/install/install-consoles.md).|  
|Konfigurieren von Standortkomponenten|Konfigurieren Sie an jedem Standort Standortkomponenten, um das Verhalten von Standortsystemrollen und die Statusberichterstattung des Standorts zu ändern. Weitere Informationen finden Sie unter [Standortkomponenten für System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Erstellen benutzerdefinierter Sammlungen|Erstellen Sie anhand ermittelter Informationen zu Geräten und Benutzern benutzerdefinierte Sammlungen von Objekten zum Vereinfachen künftiger Verwaltungsaufgaben. Weitere Informationen finden Sie unter [Erstellen von Sammlungen in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Konfigurieren von Einstellungen zum Verwalten risikoreicher Bereitstellungen|Sie können Einstellungen an einem Standort konfigurieren, über die Administratoren gewarnt werden, wenn sie eine Bereitstellung mit risikoreicher Tasksequenz erstellen.  Weitere Informationen finden Sie unter [Einstellungen zum Verwalten risikoreicher Bereitstellungen für System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Konfigurieren von Datenbankreplikaten für Verwaltungspunkte|Konfigurieren Sie ein Datenbankreplikat zum Verringern der CPU-Last des Standortdatenbankservers mithilfe von Verwaltungspunkten, die Anforderungen von Clients erfüllen. Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte für System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Konfigurieren einer SQL Server-AlwaysOn-Verfügbarkeitsgruppe zum Hosten der Standortdatenbank|Ab Version 1602 konfigurieren Sie Verfügbarkeitsgruppen als Lösung für hohe Verfügbarkeit und Notfallwiederherstellung zum Hosten der Standortdatenbank an primären Standorten und am Standort der zentralen Verwaltung. Weitere Informationen finden Sie unter [SQL Server Always On für eine hoch verfügbare Standortdatenbank für System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).|  
|Ändern der Replikation zwischen Standorten|Lesen Sie den Artikel [Datenübertragungen zwischen Standorten in System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md), um mehr über die folgenden Themen zu erfahren:<br /><br /> Konfigurieren der [dateibasierten Replikation](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) zwischen sekundären Standorten<br /><br /> Konfigurieren von [Datenbankreplikationslinks](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Konfigurieren von [verteilten Ansichten](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  
