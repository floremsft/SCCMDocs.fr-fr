---
title: "Grundlagen der Verwaltung von Geräten | Microsoft Docs"
description: "Erfahren Sie, wie Sie Geräte mit System Center Configuration Manager verwalten."
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: "6"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 45d84122a86da880268c93ecd994250df6b76c8a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Grundlagen der Verwaltung von Geräten mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager kann zwei große Gruppen von Geräten verwalten:

-   *Clients* sind Geräte wie Arbeitsstationen, Laptops, Server und mobile Geräte, auf denen die Configuration Manager-Clientsoftware installiert wird. Einige Verwaltungsfunktionen, z.B. Hardwareinventur, erfordern diese Clientsoftware.  

-   Zu *verwalteten Geräten* können *Clients* zählen, aber normalerweise handelt es sich um ein mobiles Gerät, auf dem die Configuration Manager-Clientsoftware nicht installiert ist. Auf dieser Art von Gerät erfolgt die Verwaltung mithilfe von Intune oder der in Configuration Manager integrierten lokalen Verwaltung mobiler Geräte.

Sie können Geräte außerdem nicht nur anhand des Clienttyps, sondern auch anhand des Benutzers gruppieren und identifizieren.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Verwalten von Geräten mit dem Configuration Manager-Client

Die Configuration Manager-Clientsoftware kann auf zwei Weisen zum Verwalten von Geräten verwendet werden. Bei der ersten wird das Gerät zunächst in Ihrem Netzwerk ermittelt. Anschließend wird die Clientsoftware auf diesem Gerät bereitgestellt. Bei der zweiten wird die Clientsoftware manuell auf einem neuen Computer installiert, der dann Ihrem Standort beitritt, wenn dieser Ihrem Netzwerk beitritt. Um Geräte zu ermitteln, auf denen die Clientsoftware nicht installiert ist, verwenden Sie eine oder mehrere der integrierten Ermittlungsmethoden. Nachdem ein Gerät erkannt wurde, können Sie die Clientsoftware mithilfe einer von mehreren Methoden installieren. Informationen zur Ermittlung finden Sie unter [Ausführen der Ermittlung für System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Nach der Ermittlung der Geräte, die die Ausführung der Configuration Manager-Clientsoftware unterstützen, können Sie die Software mithilfe einer von mehreren Methoden installieren. Nachdem die Software installiert und der Client einem primären Standort zugewiesen wurde, können Sie mit dem Verwalten des Geräts beginnen.  Es folgen gängige Installationsmethoden:

 - Clientpushinstallation

 - Auf einem Softwareupdate basierende Installation

 - Gruppenrichtlinie

 - Manuelle Installation auf einem Computer
 - Hinzufügen des Clients zu einem Betriebssystemimage, das Sie bereitstellen  


 Nachdem der Client installiert wurde, können Sie die Aufgaben bei der Verwaltung von Geräten mithilfe von Sammlungen vereinfachen. Sammlungen sind Gruppen von Geräten oder Benutzern, die Sie erstellen, damit Sie sie als Gruppe verwalten können. Beispielsweise kann es vorkommen, dass Sie eine mobile Geräteanwendung auf allen mobilen Geräten installieren möchten, die von Configuration Manager registriert wurden. In diesem Fall können Sie die Sammlung „Alle mobilen Geräte“ verwenden.  

 Weitere Informationen finden Sie in den folgenden Themen:  

-   [Wählen einer Geräteverwaltungslösung für System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Clientinstallationsmethoden in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Einführung in Sammlungen in System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Clienteinstellungen  
 Bei der Erstinstallation von Configuration Manager werden alle Clients in der Hierarchie mit den Clientstandardeinstellungen konfiguriert, die Sie ändern können. Die Clienteinstellungen umfassen diese Konfigurationsoptionen:

 -  Wie häufig die Geräte mit dem Standort kommunizieren

 -  Ob der Client für Softwareupdates und andere Verwaltungsvorgänge eingerichtet ist

 -  Ob Benutzer ihre mobilen Geräte so registrieren können, dass sie von Configuration Manager verwaltet werden  

Sie können benutzerdefinierte Clienteinstellungen erstellen und diese dann Sammlungen zuweisen.  Elemente der Sammlung sind so konfiguriert, dass sie die benutzerdefinierten Einstellungen haben. Sie können auch mehrere benutzerdefinierte Clienteinstellungen erstellen, die in der angegebenen (numerischen) Reihenfolge angewendet werden.  Bei Konflikten setzt die Einstellung mit der niedrigsten Reihenfolgennummer die anderen Einstellungen außer Kraft.  

Die folgende Abbildung zeigt ein Beispiel der Erstellung und Anwendung benutzerdefinierter Clienteinstellungen.  

 ![Clienteinstellungen](media/ClientSettings.gif)  

 Weitere Informationen zu Clienteinstellungen finden Sie unter  
                [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) und [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Verwalten von Geräten ohne Configuration Manager-Client  
 Configuration Manager unterstützt die Verwaltung einiger Geräte, auf denen die Clientsoftware nicht installiert ist und die nicht von Intune verwaltet werden. Weitere Informationen finden Sie unter [Verwalten mobiler Geräte mithilfe lokaler Infrastruktur in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) und [Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Benutzerbasierte Verwaltung  
 Configuration Manager unterstützt Sammlungen von Active Directory Domain Services-Benutzern. Wenn Sie eine Benutzersammlung verwenden, können Sie Software auf allen Computern installieren, die von Mitgliedern der Sammlung verwendet werden. Um sicherzustellen, dass die von Ihnen bereitgestellte Software nur auf den Geräten installiert wird, die als primäres Gerät eines Benutzers angegeben sind, richten Sie die Affinität zwischen Benutzer und Gerät ein. Ein Benutzer kann über ein oder mehrere primäre Geräte verfügen.  

 Eine der Möglichkeiten, mit denen Benutzer die Softwarebereitstellung auf ihren Geräten steuern können, ist die Verwendung der Clientbenutzeroberfläche **Softwarecenter**. Das **Softwarecenter** wird automatisch auf Clientcomputern installiert und über das **Startmenü** aufgerufen. Mithilfe des **Softwarecenters** können Benutzer ihre eigene Software verwalten und folgende Aufgaben ausführen:  

-   Installieren von Software  

-   Planen der automatischen Installation der Software außerhalb der Arbeitszeit  

-   Konfigurieren, wann die Installation von Software auf einem Gerät durch Configuration Manager zulässig ist  

-   Konfigurieren der Zugriffseinstellungen für die Remotesteuerung, wenn die Remotesteuerung in Configuration Manager eingerichtet ist  

-   Konfigurieren von Optionen für die Energieverwaltung, sofern diese von einem Administrator eingerichtet wurde  


 Über einen Link im **Softwarecenter** können Benutzer den **Anwendungskatalog** aufrufen und dort Software durchsuchen, installieren und anfordern. Der **Anwendungskatalog** dient außerdem zum Konfigurieren von Voreinstellungen und Zurücksetzen mobiler Geräte. Sofern eingerichtet, geben Sie ein primäres Gerät für die Affinität zwischen Benutzer und Gerät an.   

 Benutzer können auch in einer Intranet- oder Internetsitzung in einem Browser auf den **Anwendungskatalog** zugreifen.  
