---
title: Auswerten von Configuration Manager | Microsoft-Dokumentation
description: "Richten Sie eine Laborumgebung ein, um System Center Configuration Manager für die Verwendung in Ihrer Organisation zu bewerten."
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: "25"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d7ea785ab1beee09b9adda735a87f89bc9481620
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Auswerten von System Center Configuration Manager durch Einrichtung Ihrer eigenen Laborumgebung

*Gilt für: System Center Configuration Manager (Current Branch)*

 Erfahren Sie mehr über die Einrichtung einer Laborumgebung, um System Center Configuration Manager für die Verwendung in Ihrer Organisation zu testen.  

 System Center Configuration Manager ist ein komplexes und leistungsstarkes Tool zum Verwalten Ihrer Benutzer, Geräte und Software. Es wird empfohlen, vor der vollständigen Bereitstellung von System Center Configuration Manager eine gründliche Bewertung durchzuführen, damit Sie über ein grundlegendes Verständnis hinaus die Möglichkeit haben, Ihr Wissen in praktischen Übungen anzuwenden.  

 Dieses Handbuch richtet sich in erster Linie an Administratoren, die die Verwendung von Configuration Manager in Unternehmensumgebungen bewerten:  

-   Administratoren, die eine Lösung zur vollständigen Verwaltung von PCs, Servern und mobilen Geräten möchten  

-   Administratoren in Hochsicherheitsbranchen, die für ihre lokale Geräteverwaltung hohe Sicherheitsanforderungen haben und gleichzeitig die Flexibilität cloudbasierter Geräteverwaltung benötigen  

-   Administratoren, die die Skalierung der eigenen lokalen Serverarchitektur verwalten möchten  

## <a name="what-this-lab-does"></a>Wozu diese Laborumgebung dient  
 Das Hauptziel der Erstellung dieser Testumgebung besteht darin, Ihnen allgemeine Kenntnisse für den Einstieg in die Arbeit mit Configuration Manager zu vermitteln, und Ihr Verständnis von Configuration Manager zu erweitern. Sie werden Schritt für Schritt durch eine beschleunigte Assembly des aktuellen Release von Configuration Manager mit zwei Servern gehen:  

-   Ein Server hostet Active Directory, den Domänencontroller und den DNS-Server.  

-   Ein zweiter Server hostet Configuration Manager und alle zugehörigen SQL Server-Komponenten.  

Clientcomputer werden in Hyper-V installiert. Die Laborumgebung selbst kann auch als vollständig virtualisiertes System auf einem einzigen Server ausgeführt werden.  

## <a name="what-this-lab-does-not-do"></a>Wozu diese Laborumgebung nicht dient  
 In dieser Laborumgebung werden nicht alle Configuration Manager-Szenarios behandelt. Sie ist nicht darauf ausgelegt, sofort in eine aktive Umgebung migriert zu werden.  

 Wenn Sie diese Laborumgebung einrichten, verfügen Sie über eine funktionierende Umgebung, in der Sie arbeiten können. Diese Umgebung wird jedoch nicht hinsichtlich Faktoren wie Systemleistung, Verwaltung von Festplattenspeicherplatz und SQL Server-Speicher optimiert.  

##  <a name="BKMK_EvalRec"></a> Empfohlene Literatur vor dem Erstellen der Laborumgebung  
 In der [Dokumentation für System Center Configuration Manager](http://docs.microsoft.com/sccm/) steht Ihnen eine Fülle von Inhalten zur Verfügung. Es wird empfohlen, dass Sie vor dem Erstellen der Laborumgebung folgende Themen aus dieser Bibliothek lesen:  

-   Erfahren Sie mehr zu wichtigen Konzepten der Configuration Manager-Konsole, Endbenutzerportalen und Beispielszenarios in der [Einführung zu System Center Configuration Manager](../../core/understand/introduction.md).  

-   Erfahren Sie mehr über die primären Verwaltungsfunktionen von Configuration Manager in [Features und Funktionen von System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Untermauern Sie Ihre Kenntnisse mit den [Grundlagen von System Center Configuration Manager](../../core/understand/fundamentals.md).  

-   Informationen zur Bedeutung von Sicherheitsrollen finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Erfahren Sie etwas über Content Management unter [Konzepte für Content Management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   [Erfahren Sie, wie Clients Standortressourcen und Dienste für System Center Configuration Manager suchen](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md), um tägliche Vorgänge in der gesamten Bereitstellung erfolgreich zu unterstützen.  
