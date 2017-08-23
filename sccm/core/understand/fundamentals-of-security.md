---
title: Grundlagen der Sicherheit | Microsoft-Dokumentation
description: "Erfahren Sie mehr über die Sicherheitsebenen für System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: df3198885259b1db4a1aadee0db6512a1a2d4911
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Grundlagen der Sicherheit für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sicherheit für System Center Configuration Manager besteht aus mehreren Ebenen. Die erste Ebene wird von Windows-Sicherheitsfunktionen für das Betriebssystem und das Netzwerk bereitgestellt und umfasst Folgendes:  

-   Dateifreigabe für die Übertragung von Dateien zwischen Configuration Manager-Komponenten  

-   Zugriffssteuerungslisten (ACLs) zum Schutz von Dateien und Registrierungsschlüsseln  

-   Internetprotokollsicherheit (IPsec), um sichere Kommunikation zu unterstützen  

-   Gruppenrichtlinie zum Festlegen von Sicherheitsrichtlinien  

-   Distributed Component Object Model-Berechtigungen (DCOM) für verteilte Anwendungen wie die Configuration Manager-Konsole  

-   Active Directory Domain Services für das Speichern von Sicherheitsprinzipalen  

-   Windows-Kontosicherheit einschließlich einiger Gruppen, die beim Configuration Manager-Setup erstellt werden  

Außerdem ermöglichen zusätzliche Sicherheitskomponenten wie Firewalls und Angriffserkennung einen umfassenden Schutz der gesamten Umgebung. Zertifikate, die über mit dem Industriestandard konforme Public Key-Infrastrukturimplementierungen (PKI) ausgestellt werden, ermöglichen Authentifizierung, Signatur und Verschlüsselung.  

Zusätzlich zu der durch die Server- und Netzwerkinfrastruktur von Windows bereitgestellten Sicherheit steuert Configuration Manager den Zugriff auf die Configuration Manager-Konsole und die zugehörigen Ressourcen auf unterschiedliche Weise. Standardmäßig haben nur lokale Administratoren Zugriffsrechte für die Dateien und Registrierungsschlüssel, die zum Ausführen der Configuration Manager-Konsole auf den Computern erforderlich sind, auf denen sie installiert ist.  

Die nächste Sicherheitsebene basiert auf dem Zugriff über die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), speziell über den SMS-Anbieter. Der SMS-Anbieter ist eine Configuration Manager-Komponente, die einem Benutzer Zugriff gewährt, damit dieser Informationen aus der Standortdatenbank abfragen kann. Der Zugriff auf den Anbieter ist standardmäßig auf Mitglieder der lokalen Gruppe „SMS-Administratoren“ beschränkt. Diese Gruppe enthält zunächst nur den Benutzer, der Configuration Manager installiert hat. Um anderen Konten die Berechtigung für den Zugriff auf das CIM-Repository (Common Information Model) und den SMS-Anbieter zu erteilen, fügen Sie die anderen Konten der Gruppe „SMS-Administratoren“ hinzu.  

Die letzte Sicherheitsebene basiert auf Berechtigungen für Objekte in der Standortdatenbank. Standardmäßig können mit dem lokalen Systemkonto und dem Benutzerkonto, das Sie für die Installation von Configuration Manager verwendet haben, alle Objekte in der Standortdatenbank verwaltet werden. Mithilfe der rollenbasierten Verwaltung können Sie weiteren Administratoren in der Configuration Manager-Konsole Berechtigungen erteilen bzw. verwehren.  



## <a name="role-based-administration"></a>Rollenbasierte Verwaltung  
 In Configuration Manager wird die rollenbasierte Verwaltung verwendet, um Objekte wie Sammlungen, Bereitstellungen und Standorte zu sichern. Über dieses Verwaltungsmodell werden Sicherheitszugriffseinstellungen für alle Standorte und Standorteinstellungen hierarchieweit zentral definiert und verwaltet. Sicherheitsrollen werden Administratoren und Gruppenberechtigungen zugewiesen. Die Berechtigungen sind mit verschiedenen Configuration Manager-Objekttypen verbunden, wie z.B. den Berechtigungen, die zum Erstellen oder Ändern von Clienteinstellungen verwendet werden. Mithilfe von Sicherheitsbereichen werden bestimmte Instanzen von Objekten gruppiert, für deren Verwaltung ein Administrator verantwortlich ist, z.B. eine Anwendung zum Installieren von Microsoft Office. Durch die Kombination aus Sicherheitsrollen, Sicherheitsbereichen und Sammlungen wird definiert, welche Objekte ein Administrator anzeigen und verwalten kann. Von Configuration Manager werden einige Standardsicherheitsrollen für häufige Verwaltungsaufgaben installiert. Sie können jedoch auch eigene Sicherheitsrollen für ihre speziellen Geschäftsanforderungen erstellen.  

 Weitere Informationen finden Sie unter [Configure role-based administration for System Center Configuration Manager (Konfigurieren der rollenbasierten Verwaltung)](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="securing-client-endpoints"></a>Sichern von Clientendpunkten  
 Die Kommunikation zwischen Clients und Standortsystemrollen wird entweder mithilfe von selbstsignierten Zertifikaten oder mithilfe von PKI-Zertifikaten gesichert. Sie müssen ein PKI-Zertifikat für Computerclients, die Configuration Manager im Internet erkennt, und für Clients für mobile Geräte verwenden. Das PKI-Zertifikat verwendet HTTPS zum Schutz der Clientendpunkte. Die Standortsystemrollen, mit denen von Clients eine Verbindung hergestellt wird, können für Clientverbindungen über HTTPS oder HTTP konfiguriert werden. Die Kommunikation von Clientcomputern geschieht immer über die sicherste verfügbare Methode. Dabei wird nur dann im Intranet auf die weniger sichere HTTP-Kommunikation zurückgegriffen, wenn Sie über Standortsystemrollen verfügen, die HTTP-Kommunikation zulassen.  

 Weitere Informationen finden Sie unter [Technische Referenz für kryptografische Steuerelemente](../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

## <a name="configuration-manager-accounts-and-groups"></a>Konten und Gruppen in Configuration Manager  
 In Configuration Manager wird das lokale Systemkonto für den Großteil der Standortvorgänge verwendet. Für einige Verwaltungsaufgaben kann es erforderlich sein, zusätzliche Konten zu erstellen und zu verwalten. Beim Setup werden mehrere Standardgruppen und SQL Server-Rollen erstellt. Es kann erforderlich sein, diesen Standardgruppen und SQL Server-Rollen manuell Computer- oder Benutzerkonten hinzuzufügen.  

 Weitere Informationen finden Sie unter [In System Center Configuration Manager verwendete Konten](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Datenschutz  
 Zwar bieten Verwaltungsprodukte für Unternehmen zahlreiche Vorteile, da sie viele Clients effektiv verwalten können. Sie müssen sich jedoch der möglichen Auswirkungen dieser Software auf den Datenschutz der Benutzer in Ihrer Organisation bewusst sein. System Center Configuration Manager enthält zahlreiche Tools zum Sammeln von Daten und zum Überwachen von Geräten. Einige dieser Tools können Bedenken bezüglich des Datenschutzes auslösen.  

 Beim Installieren des Configuration Manager-Clients werden z.B. viele Verwaltungseinstellungen standardmäßig aktiviert. Dies führt dazu, dass von der Clientsoftware Informationen an den Configuration Manager-Standort gesendet werden. Clientinformationen werden in der Configuration Manager-Datenbank gespeichert und nicht an Microsoft gesendet. Berücksichtigen Sie beim Konfigurieren des System Center Configuration Manager Ihre Datenschutzanforderungen.  
