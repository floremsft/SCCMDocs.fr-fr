---
title: Verwenden von Standortgrenzen und Begrenzungsgruppen | Microsoft-Dokumentation
description: "Verwenden Sie die Standortgrenzen und Begrenzungsgruppen zum Definieren von Netzwerkadressen und zugänglichen Standortsystemen für Geräte, die Sie verwalten."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fea1dece0768a2b7bcd3fcedc2288ea2d52e73d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definieren von Standortgrenzen und Begrenzungsgruppen für Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mithilfe von Grenzen für System Center Configuration Manager werden Netzwerkadressen in Ihrem Intranet definiert, die Geräte enthalten können, die Sie verwalten möchten. Begrenzungsgruppen sind logische Gruppen von Grenzen, die Sie konfigurieren.

 Eine Hierarchie kann eine beliebige Anzahl von Begrenzungsgruppen enthalten, und jede Begrenzungsgruppe kann eine beliebige Kombination der folgenden Grenztypen enthalten:  

-   IP-Subnetz,  
-   Active Directory-Standortname  
-   IPv6-Präfix  
-   IP-Adressbereich  

Clients im Intranet bewerten ihre aktuelle Adresse im Netzwerk und bestimmen anhand dieser Informationen Begrenzungsgruppen, zu denen sie gehören.  

 Clients nutzen Begrenzungsgruppen für folgende Zwecke:  
-   **Suchen eines zugewiesenen Standorts:** Mithilfe von Begrenzungsgruppen können Clients einen primären Standort für die Clientzuweisung finden (automatische Standortzuweisung).  
-   **Suchen bestimmter Standortsystemrollen, die Sie verwenden können:** Wenn Sie eine Begrenzungsgruppe bestimmten Standortsystemrollen zuordnen, bietet die Begrenzungsgruppe Clients eine Liste mit Standortsystemen, die während der Inhaltssuche und als bevorzugte Verwaltungspunkte verwendet werden sollen.  

Von Clients, die sich im Internet befinden oder nur für Internetverbindungen konfiguriert sind, werden keine Begrenzungsinformationen verwendet. Die automatische Standortzuweisung kann von diesen Clients nicht verwendet werden. Wenn der Verteilungspunkt für das Zulassen von Clientverbindungen aus dem Internet konfiguriert ist, werden Inhalte stets von einem beliebigen Verteilungspunkt im Standort heruntergeladen, der dem Client zugeordnet ist.  

**Erste Schritte:**
- Erstens, [define network locations as boundaries (Netzwerkorte als Grenzen definieren)](/sccm/core/servers/deploy/configure/boundaries).
- Fahren Sie anschließend mit [configuring boundary groups (Begrenzungsgruppen konfigurieren)](/sccm/core/servers/deploy/configure/boundary-groups) fort, um Clients in diesen Grenzen dem Standortsystemserver zuzuordnen.



##  <a name="BKMK_BoundaryBestPractices"></a> Empfohlene Methoden für Standortgrenzen und Begrenzungsgruppen  

-   **Verwenden Sie eine Kombination aus den wenigsten Grenzen, die Ihren Anforderungen entsprechen:**  
   In der Vergangenheit empfahlen wir die Verwendung von einigen Typen von Grenzen gegenüber anderen. Mit Änderungen zur Verbesserung der Leistung empfehlen wir Ihnen, die von Ihnen gewählten Grenzen oder Typen für Ihre Umgebung zu verwenden, sodass Sie die wenigsten möglichen Grenzen verwenden können, um Ihre Verwaltungsaufgaben zu vereinfachen.      

-   **Vermeiden Sie überlappende Grenzen bei der automatischen Standortzuweisung:**  
     Obwohl jede Begrenzungsgruppe sowohl Konfigurationen der Standortzuweisung als auch für die Inhaltssuche unterstützt, ist es eine bewährte Methode, einen getrennten Satz von Begrenzungsgruppen nur für die Standortzuweisung zu nutzen. Achten Sie also darauf, dass in einer Begrenzungsgruppe enthaltene Grenzen nicht gleichzeitig einer anderen Begrenzungsgruppe mit abweichender Standortzuweisung angehören. Der Grund ist wie folgt:  

    -   Eine einzelne Grenze kann zu mehreren Begrenzungsgruppen gehören.  

    -   Jede Begrenzungsgruppe kann für die Standortzuweisung einem anderen primären Standort zugeordnet werden.  

    -   Ein Client auf einer Grenze, die zu zwei verschiedenen Begrenzungsgruppen mit unterschiedlichen Standortzuweisungen gehört, wählt für den Beitritt zu einem Standort das Zufallsprinzip, wobei dies ggf. nicht der Standort ist, dem der Client beitreten möchte.  Diese Konfiguration wird als überlappende Grenzen bezeichnet.  

     Überlappende Grenzen sind kein Problem für die Inhaltssuche und stattdessen häufig eine gewünschte Konfiguration, um Clients zusätzliche Ressourcen oder Inhaltsorte zu bieten, die sie verwenden können.  
