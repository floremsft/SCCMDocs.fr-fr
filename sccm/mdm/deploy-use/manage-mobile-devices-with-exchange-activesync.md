---
title: "Verwalten von mobilen Geräten | Microsoft-Dokumentation"
description: "Verwalten Sie mobile Geräte mithilfe des Exchange Server-Connectors in Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
caps.latest.revision: "8"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 44958bc35586f5e57ab3fb59681bfb018d2bd5da
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-mobile-devices-with-system-center-configuration-manager-and-exchange"></a>Verwalten von mobilen Geräten mit System Center Configuration Manager und Exchange

*Gilt für: System Center Configuration Manager (Current Branch)*

Verwenden Sie den Exchange Server-Connector in System Center Configuration Manager, um mobile Geräte zu verwalten, die über das Exchange ActiveSync-Protokoll mit Exchange Server (lokal gehostet oder online) verbunden sind und nicht mithilfe von Configuration Manager registriert werden können. Sie können in der Configuration Manager-Konsole Exchange-Verwaltungsfunktionen für mobile Geräte konfigurieren, wie z.B. das Remotezurücksetzen von Geräten und Einstellungen zum Steuern mehrerer Exchange-Server.  

 ![configmgr&#45;with&#45;exchange](../../mdm/deploy-use/media/configmgr-with-exchange.png "configmgr-with-exchange")  

 Wenn Sie mobile Geräte mithilfe des Exchange Server-Connectors verwalten, wird der Configuration Manager-Client auf den mobilen Geräten nicht installiert. Aus diesem Grund sind einige Verwaltungsfunktionen eingeschränkt. Zum Beispiel können Sie keine Software auf diesen Geräten installieren oder sie mithilfe von Konfigurationselementen konfigurieren. Informationen dazu, welche unterschiedlichen Verwaltungsfunktionen von Configuration Manager Sie für mobile Geräte verwenden können, finden Sie unter [Wählen einer Geräteverwaltungslösung für System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

> [!IMPORTANT]  
>  Vergewissern Sie sich vor der Installation des Exchange Server-Connectors, dass die von Ihnen verwendete Microsoft Exchange-Version von Configuration Manager unterstützt wird. Weitere Informationen finden Sie unter „Exchange Server connector“ (Exchange Server-Connector) unter[Supported operating systems for sites and clients for System Center Configuration Manager (Unterstützte Betriebssysteme für Standorte und Clients für System Center Configuration Manager)](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

 Wenn Sie den Exchange Server-Connector verwenden, können Sie die mobilen Geräte mithilfe der in Configuration Manager konfigurierten Einstellungen verwalten statt über die Standardpostfachrichtlinien für Exchange ActiveSync. Definieren Sie die zu verwendenden Einstellungen in den folgenden Gruppeneinstellungen: **Allgemein**, **Kennwort**, **E-Mail-Verwaltung**, **Sicherheit**und **Anwendung**. Zum Beispiel können Sie in den **Kennwort** -Gruppeneinstellungen konfigurieren, ob für mobile Geräte ein Kennwort erforderlich ist, wie lang und komplex das Kennwort mindestens sein muss und ob eine Kennwortwiederherstellung zulässig ist.  

 Wenn Sie in der Gruppe mindestens eine Einstellung konfigurieren, werden alle Einstellungen in der Gruppe für mobile Geräte von Configuration Manager verwaltet. Wenn Sie in einer Gruppe keine Einstellung konfigurieren, werden die mobilen Geräte für diese Einstellungen weiterhin von Exchange verwaltet. Alle Exchange ActiveSync-Postfachrichtlinien, die auf dem Exchange Server konfiguriert und Benutzern zugewiesen wurden, behalten ihre Gültigkeit.  

 Sie können den Exchange Server-Connector auch dafür konfigurieren, die Exchange-Zugriffsregeln zu verwalten sowie mobile Geräte zuzulassen, zu blockieren oder unter Quarantäne zu stellen. Sie können ein Remotezurücksetzen für mobile Geräte mithilfe der Configuration Manager-Konsole ausführen, und Benutzer können ein Remotezurücksetzen für ihre mobilen Geräte mithilfe des Anwendungskatalogs ausführen.  

 Das mobile Gerät eines Benutzers wird automatisch im Anwendungskatalog angezeigt, wenn es vom Exchange Server-Connector verwaltet und der Exchange Server lokal gehostet wird. Wenn Sie den Exchange Server-Connector für Microsoft Exchange Online konfigurieren, müssen Sie die Affinität zwischen Benutzer und Gerät manuell konfigurieren, damit das mobile Gerät des Benutzers im Anwendungskatalog angezeigt wird. Weitere Informationen zum manuellen Konfigurieren der Affinität zwischen Benutzer und Gerät finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in System Center Configuration Manager](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

> [!TIP]  
>  Wenn Sie ein mobiles Gerät mithilfe des Exchange Server-Connectors verwalten und das mobile Gerät auf einen anderen Benutzer übertragen wird, löschen Sie das mobile Gerät aus der Configuration Manager-Konsole, bevor der neue Besitzer des mobilen Geräts sein Exchange-Konto auf dem übertragenen mobilen Gerät konfiguriert.  

## <a name="required-security-permissions"></a>Erforderliche Sicherheitsberechtigungen  
 Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um den Exchange Server-Connector konfigurieren zu können:  

-   Die Berechtigung **Ändern** für das Objekt **Standort** , um den Exchange Server-Connector hinzufügen, ändern und löschen zu können  

-   Die Berechtigung **ModifyConnectorPolicy** für das Objekt **Standort** , um die Einstellungen mobiler Geräte konfigurieren zu können  

 Die Sicherheitsrolle **Hauptadministrator** umfasst die für die Konfiguration des Exchange Server-Connectors erforderlichen Berechtigungen.  

 Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um mobile Geräte verwalten zu können:  

-   Die Berechtigung **Ressource löschen** für das Objekt **Sammlung** , um ein mobiles Gerät zurücksetzen zu können  

-   Die Berechtigung **Ressource ändern** für das Objekt **Sammlung** , um einen Befehl zum Zurücksetzen abbrechen zu können  

-   Berechtigung **Ressource ändern** für das Objekt **Sammlung** , um mobile Geräte zulassen und blockieren zu können  

 Die Sicherheitsrolle **Betriebsadministrator** umfasst die für die Verwaltung mobiler Geräte mithilfe des Exchange Server-Connectors erforderlichen Berechtigungen.  

 Weitere Informationen zum Konfigurieren von Sicherheitsberechtigungen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung für System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="installing-and-configuring-an-exchange-server-connector"></a>Installieren und Konfigurieren eines Exchange Server-Connectors  
 Gehen Sie wie folgt vor, um einen Exchange Server-Connector zum Verwalten mobiler Geräte zu installieren und zu konfigurieren. Von Configuration Manager wird nur jeweils ein Connector in einer Exchange-Organisation unterstützt. Nach Abschluss dieses Verfahrens können Sie die vom Connector ermittelten und verwalteten mobilen Geräte überwachen, wenn Sie die Sammlungen mit mobilen Geräten und die Berichte zu mobilen Geräten anzeigen.  

> [!NOTE]  
>  Von Configuration Manager werden automatisch Namen für die gefundenen mobilen Geräte im Format *Benutzername*_*Gerätetyp* generiert. Wenn ein Benutzer über mehrere mobile Geräte mit dem gleichen Gerätetyp verfügt, wird in der Configuration Manager-Konsole und in Berichten der gleiche Name für diese mobilen Geräte angezeigt.  

#### <a name="to-install-and-configure-an-exchange-server-connector"></a>So installieren und konfigurieren Sie einen Exchange Server-Connector  

1.  Entscheiden Sie, mit welchem Konto eine Verbindung mit dem Exchange-Clientzugriffsserver hergestellt wird, um die mobilen Geräte zu verwalten. Dabei kann es sich um das Computerkonto des Standortservers oder um ein Windows-Benutzerkonto handeln. Konfigurieren Sie dieses Konto anschließend für die Ausführung der folgenden Exchange Server-Cmdlets:  

    -   **Clear-ActiveSyncDevice**  

    -   **Get-ActiveSyncDevice**  

    -   **Get-ActiveSyncDeviceAccessRule**  

    -   **Get-ActiveSyncDeviceStatistics**  

    -   **Get-ActiveSyncMailboxPolicy**  

    -   **Get-ActiveSyncOrganizationSettings**  

    -   **Get-ExchangeServer**  

    -   **Get-Recipient**  

    -   **Set-ADServerSettings**  

    -   **Set-ActiveSyncDeviceAccessRule**  

    -   **Set-ActiveSyncMailboxPolicy**  

    -   **Set-CASMailbox**  

    -   **New-ActiveSyncDeviceAccessRule**  

    -   **New-ActiveSyncMailboxPolicy**  

    -   **Remove-ActiveSyncDevice**  

    > [!NOTE]  
    >  Diese Cmdlets sind in folgenden Exchange Server-Verwaltungsrollen enthalten: Empfängerverwaltung, Organisationsverwaltung (nur mit Leserechten versehen) und Serververwaltung. Weitere Informationen zu Verwaltungsrollengruppen in Exchange Server 2010 finden Sie unter [Grundlegendes zu Verwaltungsrollengruppen](http://go.microsoft.com/fwlink/p/?LinkId=212914).  

    > [!TIP]  
    >  Wenn Sie versuchen, den Exchange Server-Connector ohne erforderliche Cmdlets zu installieren oder zu verwenden, wird in der Protokolldatei „EasDisc.log“ auf dem Standortservercomputer unter der Angabe `Invoking cmdlet <cmdlet> failed` ein Fehler erfasst.  

2.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

3.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Hierarchiekonfiguration**, und klicken Sie dann auf **Exchange Server-Connector**.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Exchange Server-Server hinzufügen**.  

5.  Schließen Sie den Assistenten zum Hinzufügen von Exchange Server-Servern ab.  

    -   Wenn Sie eine lokale Instanz von Exchange Server verwenden und einen Clientzugriffsserver festlegen, können Sie einen Einzelserver oder ein Clientzugriffsserver-Array für jeden Active Directory-Standort angeben. Wenn der Server oder das Array offline sind, wird von Configuration Manager versucht, einen Clientzugriffsserver für die Verwendung zu ermitteln. Gelingt dies nicht, dann wird von Configuration Manager nachfolgend ein Postfachserver zur Herstellung einer Verbindung mit einem Clientzugriffsserver verwendet. Wiederholte Versuche werden in der Protokolldatei „EasDisc.log“ auf dem Standortservercomputer als Warnungen erfasst. Suchen Sie beispielsweise nach `Failed to open runspace for site <site_name>`.  

    -   Geben Sie als Konto für den Exchange Server-Connector das in Schritt 1 konfigurierte Konto an.  

    -   Wenn Sie mobile Geräte auch mithilfe von Configuration Manager registrieren, aktivieren Sie die Option **Externe Mobilgeräteverwaltung zulassen**, damit diese mobilen Geräte auch nach ihrer Registrierung über Configuration Manager weiterhin E-Mails von Exchange erhalten.  

    -   Auf der Seite **Konto** des Assistenten können Sie das Konto konfigurieren, das verwendet wird, um E-Mail-Benachrichtigungen an Clients zu senden, die vom bedingten Configuration Manager-Zugriff blockiert werden. Das angegebene Konto muss ein gültiges Postfach auf dem Exchange-Server haben.  

         Weitere Informationen finden Sie unter [Manage access to services in System Center Configuration Manager (Verwalten des Zugriffs auf Dienste in System Center Configuration Manager)](../../protect/deploy-use/manage-access-to-services.md).  

6.  Sie können die Installation des Exchange Server-Connectors mithilfe von Statusmeldungen und Protokolldateien überprüfen:  

    -   Bestätigen Sie, dass der Exchange Server-Connector vom Standortkomponenten-Manager erfolgreich installiert wurde, indem Sie nach der Status-ID **1015** für die Komponente **SMS_EXCHANGE_CONNECTOR** suchen. Falls der Connector von Configuration Manager nicht ordnungsgemäß installiert werden kann, weil beispielsweise der Computer des angegebenen Clientzugriffsservers offline ist, wird von Configuration Manager alle 60 Minuten ein erneuter Installationsversuch gestartet, bis entweder der Vorgang erfolgreich abgeschlossen werden konnte oder Sie den Exchange Server-Connector entfernen.  

    -   Suchen Sie auf dem Standortservercomputer die Protokolldatei „Sitecomp.log“ und darin die Angabe `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. Eine erfolgreiche Installation wird dann mit dem folgenden Text erfasst: `STATMSG: ID=1015`.  
