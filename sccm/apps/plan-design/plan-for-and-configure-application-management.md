---
title: Planen und Konfigurieren der Anwendungsverwaltung | Microsoft Docs
description: "Implementieren und konfigurieren Sie die erforderlichen Abhängigkeiten für die Bereitstellung von Anwendungen in System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: "13"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 46cc3fcfd9516cf1c124e24b50d0aac0cb0025dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Planen und Konfigurieren der Anwendungsverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Implementieren Sie anhand der Informationen in diesem Artikel die erforderlichen Abhängigkeiten für die Bereitstellung von Anwendungen in System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  

|Abhängigkeit|Weitere Informationen|  
|------------------|----------------------|  
|Auf den Standortsystemservern, auf denen der Anwendungskatalog-Websitepunkt, der Anwendungskatalog-Webdienstpunkt, der Verwaltungspunkt und der Verteilungspunkt ausgeführt werden, muss Internetinformationsdienste (IIS) installiert sein.|Weitere Informationen zu dieser Anforderung finden Sie unter [Unterstützte Konfigurationen](../../core/plan-design/configs/supported-configurations.md).|  
|Von Configuration Manager registrierte mobile Geräte|Verwenden Sie für die Codesignierung von Anwendungen zur Bereitstellung auf mobilen Geräten kein Zertifikat, das mithilfe einer Vorlage der Version 3 (**Windows Server 2008 Enterprise Edition**) generiert wurde. Bei Verwendung dieser Zertifikatvorlage wird ein Zertifikat generiert, das nicht mit Configuration Manager-Anwendungen für mobile Geräte kompatibel ist.<br /><br /> Wenn Sie Active Directory-Zertifikatdienste für die Codesignierung von Anwendungen für mobile Geräte nutzen, verwenden Sie keine Zertifikatvorlage der Version 3.|  
|Clients müssen für die Überwachung von Anmeldeereignissen konfiguriert sein, wenn Affinitäten zwischen Benutzern und Geräten automatisch erstellt werden sollen.|Der Configuration Manager-Client liest Anmeldeereignisse vom Typ **Success** (Erfolg) vom Sicherheitsereignisprotokoll des PCs, um automatisch Affinitäten zwischen Benutzen und Geräten zu bestimmen.  Diese Ereignisse werden durch die folgenden zwei Überwachungsrichtlinien aktiviert.<br>**Anmeldeversuche überwachen**<br>**Anmeldeereignisse überwachen**<br>Für die automatische Erstellung von Beziehungen zwischen Benutzern und Geräten müssen Sie sicherstellen, dass diese beiden Einstellungen auf Clientcomputern aktiviert sind. Sie können diese Einstellungen mithilfe von Windows-Gruppenrichtlinien konfigurieren.|  

## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager   

|Abhängigkeit|Weitere Informationen|  
|------------------|----------------------|  
|Verwaltungspunkt|Von Clients wird eine Verbindung mit einem Verwaltungspunkt hergestellt, um eine Clientrichtlinie herunterzuladen, nach Inhalten zu suchen und eine Verbindung mit dem Anwendungskatalog herzustellen.<br /><br /> Ohne Zugriff auf einen Verwaltungspunkt ist Clients die Verwendung des Anwendungskatalogs nicht möglich.|  
|Verteilungspunkt|Damit Anwendungen auf Clients bereitgestellt werden können, muss in der Hierarchie mindestens ein Verteilungspunkt vorhanden sein. Standardmäßig wird auf dem Standortserver während einer Standardinstallation eine Verteilungspunkt-Standortrolle aktiviert. Anzahl und Standort von Verteilungspunkten richten sich nach den jeweiligen Anforderungen Ihres Unternehmens.<br /><br /> Weitere Informationen zum Installieren von Verteilungspunkten und zum Verwalten von Inhalten finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Clienteinstellungen|Mit vielen Clienteinstellungen wird gesteuert, wie Anwendungen auf dem Client installiert werden und wie die Benutzeroberfläche auf dem Client aussieht. Diese Clienteinstellungen umfassen Folgendes:<br /><br /><ul><li>Computer-Agent</li><li>Computerneustart</li><li>Softwarebereitstellung</li><li>Affinität zwischen Benutzer und Gerät</li></ul> Weitere Informationen zu diesen Clienteinstellungen finden Sie unter [Informationen zu Clienteinstellungen](../../core/clients/deploy/about-client-settings.md).<br /><br /> Informationen zum Konfigurieren von Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md).|  
|Für den Anwendungskatalog:<br /><br /> Ermittelte Benutzerkonten|Benutzer müssen zunächst von Configuration Manager ermittelt werden, bevor sie Anwendungen anzeigen und aus dem Anwendungskatalog anfordern können. Weitere Informationen finden Sie unter [Run discovery (Ausführen der Ermittlung)](/sccm/core/servers/deploy/configure/run-discovery).|  
|App-V 4.6 SP1-Client oder höher zum Ausführen von virtuellen Anwendungen|Zum Erstellen von virtuellen Anwendungen in Configuration Manager muss auf Clientcomputern der App-V 4.6 SP1-Client oder höher installiert sein.<br /><br /> Sie müssen den App-V-Client außerdem mit dem im Knowledge Base-Artikel [2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) beschriebenen Hotfix aktualisieren, bevor Sie virtuelle Anwendungen bereitstellen können.|  
|Anwendungskatalog-Webdienstpunkt|Der Anwendungskatalog-Webdienstpunkt ist eine Standortsystemrolle, über die der Anwendungskatalog-Website von der Softwarebibliothek Informationen zu verfügbarer Software bereitgestellt werden.<br /><br /> Weitere Informationen zum Konfigurieren dieser Standortsystemrolle finden Sie unter [Konfigurieren von Softwarecenter und Anwendungskatalog (nur Windows-PCs)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) in diesem Artikel.|  
|Anwendungskatalog-Websitepunkt|Der Anwendungskatalog-Websitepunkt ist eine Standortsystemrolle, über die Benutzern eine Liste der verfügbaren Software bereitgestellt wird.<br /><br /> Weitere Informationen zum Konfigurieren dieser Standortsystemrolle finden Sie unter [Konfigurieren von Softwarecenter und Anwendungskatalog (nur Windows-PCs)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) in diesem Artikel.|  
|Reporting Services-Punkt|Zur Verwendung der Configuration Manager-Berichte für die Anwendungsverwaltung müssen Sie einen Reporting Services-Punkt installieren und konfigurieren.<br /><br /> Weitere Informationen finden Sie unter [Berichterstellung in System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Sicherheitsberechtigungen für die Anwendungsverwaltung|Zum Verwalten von Anwendungen müssen Sie über folgende Sicherheitsberechtigungen verfügen:<br /><br /> In der Sicherheitsrolle **Anwendungsautor** sind die obigen erforderlichen Berechtigungen zum Erstellen, Ändern und Außerkraftsetzen von Anwendungen in Configuration Manager enthalten.<br /><br /> **So stellen Sie Anwendungen bereit:**<br /><br /> In der Sicherheitsrolle **Anwendungsbereitstellungs-Manager** sind die obigen erforderlichen Berechtigungen zum Bereitstellen von Anwendungen in Configuration Manager enthalten.<br /><br /> In der Sicherheitsrolle **Anwendungsadministrator** sind alle Berechtigungen der Sicherheitsrollen **Anwendungsautor** und **Anwendungsbereitstellungs-Manager** enthalten.<br /><br /> Weitere Informationen finden Sie unter [Configure role-based administration (Konfigurieren der rollenbasierten Verwaltung)](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Konfigurieren von Softwarecenter und Anwendungskatalog (nur Windows-PCs)  

 In System Center Configuration Manager gibt es für Benutzer jetzt zwei Optionen zum Ändern von Einstellungen sowie zum Suchen und Installieren von Anwendungen:  

-   **Das neue Softwarecenter:** Das neue Softwarecenter weist einen modernen Look auf. Apps, die bisher nur im von Silverlight abhängigen Anwendungskatalog angezeigt wurden (für Benutzer verfügbare Apps), werden jetzt im Softwarecenter auf der Registerkarte **Anwendungen** angezeigt. Auf den Anwendungskatalog kann weiterhin über den Link auf der Registerkarte **Installationsstatus** im Softwarecenter zugegriffen werden.  

     Sie können Clients für die Verwendung des neuen Softwarecenters konfigurieren, indem Sie die Clienteinstellung **Computer-Agent** > **Neues Softwarecenter verwenden**.  

    > [!IMPORTANT]  
    >  Obwohl Sie keine Verbindung mit dem Anwendungskatalog mehr herstellen müssen, müssen Sie weiterhin den Anwendungskatalog-Websitepunkt und den Anwendungskatalog-Webdienstpunkt wie im nächsten Abschnitt angegeben konfigurieren.  

-   **Das bisherige Softwarecenter und der Anwendungskatalog** – Standardmäßig verbinden sich Benutzer weiter mit der vorherigen Version des Softwarecenters und dem Anwendungskatalog (Silverlight-fähiger Webbrowser erforderlich), um verfügbare Anwendungen zu durchsuchen.  

 Unabhängig von der verwendeten Version wird das Softwarecenter automatisch installiert, wenn Sie den Configuration Manager-Client auf Windows-PCs installieren.  

    > [!TIP]  
    >  Die Version des Softwarecenters, die Benutzern angezeigt wird, basiert auf Configuration Manager-Clienteinstellungen. Dadurch können Sie flexibel steuern, welche Version basierend auf benutzerdefinierten Clienteinstellungen verwendet wird, die Sie in einer Sammlung bereitstellen. 

    > [!IMPORTANT]
    > In den kommenden Monaten wird die vorherige Version des Softwarecenters entfernt, und sie wird Ihnen nicht länger zur Verfügung stehen.
    > Sie können Clients für die Verwendung des neuen Softwarecenters konfigurieren, indem Sie die Clienteinstellung **Computer-Agent** > **Neues Softwarecenter verwenden**. 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Schritte zum Installieren und Konfigurieren von Anwendungskatalog und Softwarecenter  

> [!IMPORTANT]  
>  Vergewissern Sie sich, dass alle zuvor angegebenen Voraussetzungen erfüllt sind, bevor Sie diese Schritte ausführen.  

|Schritte|Details|Weitere Informationen|  
|-----------|-------------|----------------------|  
|**Schritt 1:** Wenn Sie planen, HTTPS-Verbindungen zu verwenden, muss zuvor ein Webserverzertifikat auf den Standortsystemservern bereitgestellt werden.|Stellen Sie ein Webserverzertifikat auf den Standortsystemservern bereit, auf denen der Anwendungskatalog-Websitepunkt und der Anwendungskatalog-Webdienstpunkt ausgeführt werden sollen.<br /><br /> Wenn darüber hinaus Clients den Anwendungskatalog über das Internet verwenden sollen, stellen Sie ein Webserverzertifikat auf mindestens einem Verwaltungspunkt-Standortsystemserver bereit, und konfigurieren Sie ihn für Clientverbindungen über das Internet.|Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Schritt 2:** Wenn Sie planen, ein PKI-Clientzertifikat für Verbindungen mit Verwaltungspunkten zu verwenden, stellen Sie ein Clientauthentifizierungszertifikat auf den Clientcomputern bereit.|Obwohl für die Verbindung von Clients mit dem Anwendungskatalog kein PKI-Clientzertifikat verwendet werden muss, ist eine Verbindung mit einem Verwaltungspunkt erforderlich, damit sie den Anwendungskatalog verwenden zu können. In folgenden Situationen müssen Sie ein Clientauthentifizierungszertifikat auf Clientcomputern bereitstellen:<br /><br /><ul><li>Von allen Verwaltungspunkten im Intranet werden nur HTTPS-Clientverbindungen akzeptiert.</li><li>Die Verbindung von Clients mit dem Anwendungskatalog wird über das Internet hergestellt.</li></ul>|Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Schritt 3:** Installieren und konfigurieren Sie den Anwendungskatalog-Webdienstpunkt und die Anwendungskatalog-Website.|Sie müssen beide Standortsystemrollen an demselben Standort installieren. Die Installation auf demselben Standortsystemserver oder in derselben Active Directory-Gesamtstruktur ist nicht erforderlich. Allerdings muss der Anwendungskatalog-Webdienstpunkt sich in der gleichen Gesamtstruktur befinden wie die Standortdatenbank.|Weitere Informationen zur Platzierung der Standortsystemrolle finden Sie unter [Planen für Standortsystemserver und Standortsystemrollen](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Informationen zum Konfigurieren des Anwendungskatalog-Webdienstpunkts und des Anwendungskatalog-Websitepunkts finden Sie unter **Schritt 3: Installieren und Konfigurieren der Standortsystemrollen für den Anwendungskatalog**.|  
|**Schritt 4:** Konfigurieren Sie die Clienteinstellungen für Anwendungskatalog und Softwarecenter.|Konfigurieren Sie die Clientstandardeinstellungen, wenn alle Benutzer über die gleichen Einstellungen verfügen sollen. Andernfalls können Sie auch benutzerdefinierte Clienteinstellungen für bestimmte Sammlungen konfigurieren.|Weitere Informationen zu Clienteinstellungen finden Sie unter [Informationen zu Clienteinstellungen](../../core/clients/deploy/about-client-settings.md).<br /><br /> Weitere Informationen zum Konfigurieren dieser Clienteinstellungen finden Sie unter **Schritt 4: Konfigurieren der Clienteinstellungen für Anwendungskatalog und Softwarecenter**.|  
|**Schritt 5:** Überprüfen Sie, ob der Anwendungskatalog betriebsbereit ist.|Sie können den Anwendungskatalog direkt über einen Browser oder über das Softwarecenter verwenden.|Informationen hierzu finden Sie unter **Schritt 5: Überprüfen Sie, ob der Anwendungskatalog betriebsbereit ist**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Ergänzende Verfahren zum Installieren und Konfigurieren von Anwendungskatalog und Softwarecenter  
 Verwenden Sie die folgenden Informationen, wenn die Schritte in der vorstehenden Tabelle zusätzliche Verfahren erfordern.  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>Schritt 3: Installieren und Konfigurieren der Standortsystemrollen für den Anwendungskatalog  
 Mit diesen Verfahren werden die Standortsystemrollen für den Anwendungskatalog konfiguriert. Wählen Sie je nachdem, ob Sie einen neuen Standortsystemserver installieren oder einen vorhandenen Standortsystemserver verwenden, eines der beiden folgenden Verfahren aus:  

> [!NOTE]  
>  Der Anwendungskatalog kann auf einem sekundären Standort oder einem Standort der zentralen Verwaltung nicht installiert werden.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>So installieren und konfigurieren Sie die Anwendungskatalog-Standortsysteme: neuer Standortsystemserver  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Standortkonfiguration** > **Server und Standortsystemrollen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Standortsystemserver erstellen** aus.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und wählen Sie dann **Weiter** aus.  

    > [!TIP]  
    >  Wenn Clientcomputer den Anwendungskatalog über das Internet verwenden sollen, geben Sie den Internet-FQDN (vollqualifizierter Domänenname) an.  

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen die Rollen **Anwendungskatalog-Webdienstpunkt** und **Anwendungskatalog-Websitepunkt** und dann **Weiter** aus.  

6.  Beenden Sie den Assistenten.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>So installieren und konfigurieren Sie die Anwendungskatalog-Standortsysteme: bestehender Standortsystemserver  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Standortkonfiguration** > **Server und Standortsystemrollen** und anschließend den Server aus, den Sie für den Anwendungskatalog verwenden möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Server** die Option **Standortsystemrollen hinzufügen**.  

4.  Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und wählen Sie dann **Weiter** aus.  

    > [!TIP]  
    >  Wenn Clientcomputer den Anwendungskatalog über das Internet verwenden sollen, geben Sie den Internet-FQDN (vollqualifizierter Domänenname) an.  

5.  Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen die Rollen **Anwendungskatalog-Webdienstpunkt** und **Anwendungskatalog-Websitepunkt** und dann **Weiter** aus.  

6.  Beenden Sie den Assistenten.  

7. Überprüfen Sie die Installation dieser Standortsystemrollen mithilfe von Statusmeldungen und Protokolldateien:  

    Statusmeldungen: Verwenden Sie die Komponenten **SMS_PORTALWEB_CONTROL_MANAGER** und **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Zum Beispiel wird durch die Status-ID **1015** für **SMS_PORTALWEB_CONTROL_MANAGER** bestätigt, dass der Anwendungskatalog-Websitepunkt von Standortkomponenten-Manager erfolgreich installiert wurde.  

    Protokolldateien: Suchen Sie nach **SMSAWEBSVCSetup.log** und **SMSPORTALWEBSetup.log**.  

    Suchen Sie nach den Protokolldateien **awebsvcMSI.log** und **portlwebMSI.log**, um weitere Informationen zu erhalten.  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>Schritt 4: Konfigurieren der Clienteinstellungen für Anwendungskatalog und Softwarecenter  
 Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für Anwendungskatalog und Softwarecenter konfiguriert, die für alle Geräte in der Hierarchie gelten. Wenn Sie diese Einstellungen nur auf einige Geräte anwenden möchten, können Sie eine benutzerdefinierte Clienteinstellung erstellen und diese für eine Sammlung mit den Geräten bereitstellen, auf die Sie diese Einstellungen anwenden möchten. Weitere Informationen zum Erstellen von benutzerdefinierten Geräteeinstellungen finden Sie im Abschnitt [Erstellen und Bereitstellen von benutzerdefinierten Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings) im Artikel [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

4.  Überprüfen und konfigurieren Sie die Einstellungen, die sich auf Benutzerbenachrichtigungen, Anwendungskatalog und Softwarecenter beziehen. Beispiel:  

    1.  Gruppe**Computer-Agent** :  

        -   **Websitepunkt des Standardanwendungskatalogs**  

        -   **Standardanwendungskatalog-Website zur Internet Explorer-Zone der vertrauenswürdigen Sites hinzufügen**  

        -   **Im Softwarecenter angezeigter Organisationsname**  

            > [!TIP]  
            >  Zum Angeben des im Anwendungskatalog angezeigten Organisationsnamens und zum Konfigurieren des Websitedesigns verwenden Sie in den Websiteeigenschaften des Anwendungskatalogs die Registerkarte **Anpassung**.  

        -   **Neues Softwarecenter verwenden:** Legen Sie diese Einstellung auf **Ja** fest, wenn Sie das neue Softwarecenter verwenden möchten. Es ermöglicht Benutzern das Suchen und Installieren verfügbarer Apps, ohne dass auf den Anwendungskatalog zugegriffen werden muss (der einen Silverlight-fähigen Browser erfordert).  

        -   **Berechtigungen installieren**  

        -   **Benachrichtigung für neue Bereitstellungen anzeigen**  

    2.  Gruppe**Energieverwaltung** :  

        -   **Benutzern das Ausschließen ihres Geräts aus der Energieverwaltung gestatten**  

    3.  Gruppe**Remotetools** :  

        -   **Benutzer können Richtlinien- oder Benachrichtigungseinstellungen im Softwarecenter ändern**  

    4.  Gruppe**Affinität zwischen Benutzer und Gerät** :  

        -   **Benutzern das Festlegen primärer Geräte gestatten**  

    > [!NOTE]  
    >  Weitere Informationen zu den Clienteinstellungen finden Sie unter [Informationen zu Clienteinstellungen in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Wählen Sie **OK** aus, um das Dialogfeld **Clientstandardeinstellungen** zu schließen.  

 Die Clientcomputer werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [How to manage Clients (Verwalten von Clients)](../../core/clients/manage/manage-clients.md).

#### <a name="how-to-customize-software-center-branding"></a>Anpassen des Brandings für das Softwarecenter

Benutzerdefiniertes Branding für das Softwarecenter wird gemäß den folgenden Regeln angewendet:

1. Wenn die Standortserverrolle „Anwendungskatalog-Websitepunkt“ nicht installiert ist, wird im Softwarecenter der Organisationsname angezeigt, der in der **Computer-Agent**-Clienteinstellung **Im Softwarecenter angezeigter Organisationsname** angegeben ist. Eine Anleitung hierzu finden Sie unter [Konfigurieren von Clienteinstellungen](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/configure-client-settings).
2. Wenn die Standortserverrolle „Anwendungskatalog-Websitepunkt“ installiert ist, zeigt Software Center den Organisationsnamen und die Farbe an, der bzw. die in den Eigenschaften der Standortserverrolle „Anwendungskatalog-Websitepunkt“ angegeben sind. Weitere Informationen finden Sie unter [Konfigurationsoptionen für den Anwendungskatalog-Websitepunkt](https://docs.microsoft.com/en-us/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).
3. Wenn ein Microsoft Intune-Abonnement konfiguriert und mit Configuration Manager verbunden wurde, werden im Softwarecenter der Organisationsname, die Farbe und das Unternehmenslogo entsprechend den Angaben in den Eigenschaften des Intune-Abonnements angezeigt. Weitere Informationen finden Sie unter [Configuring the Microsoft Intune subscription](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).

> [!IMPORTANT]  
>  Das Branding des Softwarecenters wird alle 14 Tage mit dem Intune-Dienst synchronisiert. Änderungen, die Sie in Intune vornehmen, können daher verzögert in Configuration Manager angezeigt werden.

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Schritt 5: Überprüfen Sie, ob der Anwendungskatalog betriebsbereit ist.  
 Verwenden Sie die folgenden Verfahren, um zu überprüfen, ob der Anwendungskatalog betriebsbereit ist. Sie können den Anwendungskatalog direkt über einen Browser oder über das Softwarecenter verwenden.  

> [!NOTE]  
>  Für den Anwendungskatalog ist Microsoft Silverlight erforderlich, das automatisch als Configuration Manager-Clientvoraussetzung installiert wird. Wenn Sie den Anwendungskatalog direkt über einen Browser auf einem Computer verwenden, auf dem der Configuration Manager-Client nicht installiert ist, müssen Sie zunächst überprüfen, ob Microsoft Silverlight auf dem Computer installiert ist.  

> [!TIP]  
>  Fehlende Voraussetzungen sind einer der häufigsten Gründe dafür, dass der Anwendungskatalog nach der Installation nicht ordnungsgemäß funktioniert. Stellen Sie sicher, dass die Standortsystemrollen-Voraussetzungen für die Standortsystemrollen des Anwendungskatalogs erfüllt sind. Lesen Sie hierzu den Artikel [Unterstützte Konfigurationen](../../core/plan-design/configs/supported-configurations.md).  

> [!NOTE]  
>  Wenn Sie über ein Domänenadministratorkonto angemeldet sind, werden keine Benachrichtigungen des Configuration Manager-Clients angezeigt (z.B. Benachrichtigungen über die Verfügbarkeit neuer Software).  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>So verwenden Sie den Anwendungskatalog direkt über einen Browser  

-   Geben Sie im Browser die Adresse der Anwendungskatalog-Website ein, und überprüfen Sie, ob die Webseite mit den folgenden drei Registerkarten angezeigt wird: **Anwendungskatalog**, **Eigene Anwendungsanforderungen** und **Eigene Geräte**.  

     Wählen Sie in der folgenden Liste die entsprechende Adresse für den Anwendungskatalog aus, wobei &lt;Server&gt; der Computername, der Intranet-FQDN oder der Internet-FQDN ist, und verwenden Sie sie:  

    -   HTTPS-Clientverbindungen und Standardeinstellungen für die Standortsystemrolle: **https://&lt;Server&gt;/CMApplicationCatalog**  

    -   HTTP-Clientverbindungen und Standardeinstellungen für die Standortsystemrolle: **http://&lt;Server&gt;/CMApplicationCatalog**  

    -   HTTPS-Clientverbindungen und benutzerdefinierte Einstellungen für die Standortsystemrolle: **https://&lt;Server&gt;:&lt;Port&gt;/&lt;Webanwendungsname&gt;**  

    -   HTTP-Clientverbindungen und benutzerdefinierte Einstellungen für die Standortsystemrolle: **http://&lt;Server&gt;:&lt;Port&gt;/&lt;Webanwendungsname&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>So verwenden Sie den Anwendungskatalog über das Softwarecenter (gilt nicht für die neue Version des Softwarecenters)  

1.  Wählen Sie auf dem Clientcomputer die Optionen **Start** > **Alle Programme** > **Microsoft System Center 2012** > **Configuration Manager** > **Softwarecenter** aus.  

2.  Wenn Sie für das Softwarecenter bereits einen Organisationsnamen als Clienteinstellung konfiguriert haben, überprüfen Sie, ob dieser ordnungsgemäß angezeigt wird.  

3.  Wählen Sie **Zusätzliche Anwendungen im Anwendungskatalog suchen** aus, und überprüfen Sie, ob die Seite mit den folgenden drei Registerkarten angezeigt wird: **Anwendungskatalog**, **Eigene Anwendungsanforderungen** und **Eigene Geräte**.  

> [!WARNING]  
>  Nach der Installation der Standortsystemrollen für den Anwendungskatalog wird beim Auswählen des Links **Zusätzliche Anwendungen im Anwendungskatalog suchen** im Softwarecenter nicht sofort der Anwendungskatalog angezeigt. Der Anwendungskatalog steht erst nach dem nächsten Herunterladen der Clientrichtlinie durch den Client oder bis zu 25 Stunden nach der Installation der Standortsystemrollen für den Anwendungskatalog zur Verfügung.  
