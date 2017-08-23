---
title: "Verwalten von Clients im Internet – Configuration Manager | Microsoft-Dokumentation"
description: "In diesem Artikel erhalten Sie Informationen über das Verwalten von Clients mithilfe des Cloudverwaltungsgateways und über die internetbasierte Clientverwaltung in Configuration Manager."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1b6752be448e1062c97a3225db4fa8af9f4832a6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Verwalten von Clients im Internet mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In der Regel sind in Configuration Manager die meisten verwalteten Computer und Server auf demselben internen privaten oder Unternehmensnetzwerk wie die Standortsystemserver, die Verwaltungsfunktionen ausführen. Allerdings können Sie Client-Computer außerhalb des Unternehmensnetzwerks verwalten, wenn sie mit dem Internet verbunden sind, ohne dass die Clients eine Verbindung über virtuelle private Netzwerke herstellen müssen, um die Standortsystemserver zu erreichen.

Configuration Manager bietet zwei Methoden, mit dem Internet verbundene Clients zu verwalten:

-   Cloudverwaltungsgateway

-   Internetbasierte Clientverwaltung

## <a name="cloud-management-gateway"></a>Cloudverwaltungsgateway

Ab Version 1610 bietet Configuration Manager das Cloudverwaltungsgateway. Diese neue Methode bietet eine Möglichkeit zur Verwaltung von internetbasierten Clients mit einer Kombination aus einem Cloud-Dienst, der für Microsoft Azure bereitgestellt wird, und einer neuen Standortsystemrolle, die mit diesem Dienst kommuniziert. Clients verwenden dann den Dienst, um mit Configuration Manager zu kommunizieren.

Vorteile:

-   Keine zusätzlichen Infrastrukturinvestitionen erforderlich.

-   Lokale Infrastruktur bleibt vom Internet getrennt.

-   Virtuelle Computer in der Cloud, auf denen der Dienst ausgeführt wird, werden vollständig von Azure verwaltet und erfordern keine Wartung.

-   Einfache Einrichtung und Konfiguration in der Configuration Manager-Konsole.

Nachteile:

-   Cloud-Abonnement-Kosten.

-   Verwaltungsdaten werden über Cloud-Dienst gesendet.

Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](plan-cloud-management-gateway.md).

## <a name="internet-based-client-management"></a>Internetbasierte Clientverwaltung

Diese Methode beruht auf Internet-bezogenen Standortsystemservern, mit denen Clients zu Verwaltungszwecken kommunizieren. Bei dieser Methode müssen Clients und Standortsystemserver für die internetbasierte Verwaltung konfiguriert werden.

Vorteile:

-   Keine Abhängigkeit von einem Cloud-Dienst.

-   Ohne zusätzliche Kosten eines Cloud-Abonnements.

-   Vollständige Kontrolle von Servern und Rollen, die den Dienst bereitstellen.

Nachteile:

-   Zusätzliche Infrastrukturinvestitionen erforderlich.

-   Gemeinkosten und Betriebskosten der zusätzlichen Infrastruktur.

-   Infrastruktur muss mit dem Internet verbunden sein.

Weitere Informationen finden Sie unter [Planen der internetbasierten Clientverwaltung](plan-internet-based-client-management.md).
