---
title: Installieren von cloudbasierten Verteilungspunkten | Microsoft-Dokumentation
description: "Erfahren Sie, was Sie tun müssen, um mit der Verwendung von cloudbasierten Verteilungspunkten in Microsoft Azure zu beginnen."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 39b35cccf78bba4e69a7de0ca3a5a8dc516201e3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Installieren von cloudbasierten Verteilungspunkte in Microsoft Azure für System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können in Microsoft Azure cloudbasierte Verteilungspunkte von System Center Configuration Manager installieren. Wenn Sie keine Erfahrung mit cloudbasierten Verteilungspunkten haben, lesen Sie das Thema [Verwenden eines cloudbasierten Verteilungspunkts](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md), bevor Sie fortfahren.

 Bevor Sie mit der Installation beginnen, stellen Sie sicher, dass Sie über die erforderlichen Zertifikatdateien verfügen:  

-   Ein Microsoft Azure-Verwaltungszertifikat, das in eine CER-Datei und in eine PFX-Datei exportiert wird  

-   Ein Dienstzertifikat für cloudbasierte Verteilungspunkte von Configuration Manager, das in eine PFX-Datei exportiert wird.  

    > [!TIP]
    >   Weitere Informationen zu diesen Zertifikaten bietet der Abschnitt zu cloudbasierten Verteilungspunkten des Themas [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Eine Beispielbereitstellung des Dienstzertifikats für cloudbasierte Verteilungspunkte finden Sie im Abschnitt „Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte“ im Thema [Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für System Center Configuration Manager: Windows Server 2008-Zertifizierungsstelle](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  


 Nach der Installation des cloudbasierten Verteilungspunkts wird von Azure automatisch eine GUID für den Dienst generiert, die an das DNS-Suffix von **cloudapp.net** angehängt wird. Mit dieser GUID müssen Sie einen DNS-Datensatz mit einem DNS-Alias (CNAME-Datensatz) konfigurieren. So können Sie den im Dienstzertifikat für cloudbasierte Verteilungspunkte von Configuration Manager definierten Dienstnamen der automatisch generierten GUID zuordnen.  

 Wenn Sie einen Proxywebserver verwenden, müssen Sie möglicherweise Proxyeinstellungen konfigurieren, um die Kommunikation mit dem Clouddienst zu ermöglichen, von dem der Verteilungspunkt gehostet wird.  

##  <a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Einrichten von Azure und Installieren von cloudbasierten Verteilungspunkten  
 Gehen Sie wie folgt vor, um Azure zur Unterstützung von Verteilungspunkten einzurichten. Installieren Sie anschließend den cloudbasierten Verteilungspunkt in Configuration Manager.  

### <a name="to-set-up-a-cloud-service-in-azure-for-a-distribution-point"></a>So richten Sie einen Clouddienst in Azure für einen Verteilungspunkt ein  

1.  Öffnen Sie einen Webbrowser zum Azure-Portal unter https://manage.windowsazure.com, und öffnen Sie Ihr Konto.  

2.  Klicken Sie auf **Gehostete Dienste, Speicherkonten & CDN**, und wählen Sie dann **Verwaltungszertifikate** aus.  

3.  Klicken Sie mit der rechten Maustaste auf Ihr Abonnement, und wählen Sie anschließend **Zertifikat hinzufügen**aus.  

4.  Geben Sie unter **Zertifikatdatei** die CER-Datei an, die das exportierte Azure-Verwaltungszertifikat enthält, das für diesen Clouddienst verwendet werden soll. Klicken Sie dann auf **OK**.  

Das Verwaltungszertifikat wird in Azure geladen, und Sie können nun einen cloudbasierten Verteilungspunkt installieren.  

### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>So installieren Sie einen cloudbasierten Verteilungspunkt für Configuration Manager  

1.  Führen Sie die Schritte aus dem vorhergehenden Verfahren aus, um einen Clouddienst in Azure mit einem Verwaltungszertifikat einzurichten.  

2.  Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Cloud Services**, und wählen Sie dann **Cloudverteilungspunkte** aus. Klicken Sie auf der Registerkarte **Startseite** auf **Cloudverteilungspunkt erstellen**.  

3.  Richten Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Cloudverteilungspunkten Folgendes ein:  

    -   Geben Sie die **Abonnement-ID** für Ihr Azure-Konto an.  

        > [!TIP]  
        >  Sie können Ihre Azure-Abonnement-ID im Azure-Portal finden.  

    -   Geben Sie das **Verwaltungszertifikat**an. Klicken Sie auf **Durchsuchen**, um die PFX-Datei anzugeben, die das exportierte Azure-Verwaltungszertifikat enthält, und geben Sie dann das Kennwort für das Zertifikat ein. Optional können Sie eine Version 1 der PUBLISHSETTINGS-Datei aus dem Azure SDK 1.7 angeben.  

4.  Klicken Sie auf **Weiter**. Der Configuration Manager stellt eine Verbindung zu Azure her, um das Verwaltungszertifikat zu überprüfen.  

5.  Führen Sie auf der Seite **Einstellungen** die folgenden Schritte aus, und klicken Sie dann auf **Weiter**:  

    -   Wählen Sie unter **Region** die Azure-Region aus, in der Sie den Clouddienst erstellen möchten, von dem dieser Verteilungspunkt gehostet wird.  

    -   Geben Sie unter **Zertifikatdatei** die PFX-Datei an, die das exportierte Dienstzertifikat für cloudbasierte Verteilungspunkte von Configuration Manager enthält. Geben Sie dann das Kennwort ein.  

        > [!NOTE]  
        >  Das Feld **Dienst-FQDN** wird automatisch mit dem Namen des Zertifikatantragstellers aufgefüllt. Es muss in der Regel nicht bearbeitet werden. Die Ausnahme ist, wenn Sie ein Platzhalterzertifikat in einer Testumgebung verwenden. Beispielsweise können Sie in diesem Fall möglicherweise nicht den Hostnamen angeben, damit mehrere Computer mit dem gleichen DNS-Suffix das Zertifikat verwenden können. In diesem Szenario enthält der Zertifikatantragsteller einen ähnlichen Wert wie **CN=\*.contoso.com**, und von Configuration Manager wird eine Meldung darüber angezeigt, dass der korrekte FQDN angegeben werden muss. Klicken Sie auf **OK** , um die Meldung zu schließen. Geben Sie anschließend einen bestimmten Namen vor dem DNS-Suffix ein, damit der FQDN vollständig ist. Fügen Sie beispielsweise **clouddp1** hinzu, um den vollständigen Dienst-FQDN von **clouddp1.contoso.com**anzugeben. Der FQDN des Diensts muss in Ihrer Domäne eindeutig sein und darf keinem der Domäne angehörenden Gerät entsprechen.  
        >   
        >  Platzhalterzertifikate werden nur in Testumgebungen unterstützt.  

6.  Richten Sie auf der Seite **Warnungen** Speicher- und Übertragungsquoten ein, und geben Sie an, bei welchem Prozentsatz dieser Quoten von Configuration Manager Warnungen generiert werden sollen. Klicken Sie anschließend auf **Weiter**.  

7.  Schließen Sie den Assistenten ab.  

Mit dem Assistenten wird ein neuer gehosteter Dienst für den cloudbasierten Verteilungspunkt erstellt. Wenn Sie den Assistenten geschlossen haben, können Sie den Installationsfortschritt des cloudbasierten Verteilungspunkts in der Configuration Manager-Konsole überwachen. Sie können auch die **CloudMgr.log**-Datei auf dem primären Standortserver überwachen. Es ist möglich, die Bereitstellung des Clouddiensts im Azure-Portal zu überwachen.  

> [!NOTE]  
>  Die Bereitstellung eines neuen Verteilungspunkts in Azure kann bis zu 30 Minuten dauern. Bis zur Bereitstellung des Speicherkontos wird in der Datei **CloudMgr.log** wiederholt die Meldung angezeigt, **dass auf die Überprüfung gewartet wird, ob ein Container vorhanden ist, und dass die Überprüfung in 10 Sekunden wiederholt wird**. Anschließend wird der Dienst erstellt und konfiguriert.  

 Prüfen Sie mithilfe eines der folgenden Verfahren, ob die Installation des cloudbasierten Verteilungspunkts abgeschlossen ist:  

-   Im Azure-Portal wird unter **Bereitstellung** für den cloudbasierten Verteilungspunkt der Status **Bereit** angezeigt.  

-   In der Configuration Manager-Konsole wird im Arbeitsbereich **Verwaltung** im Knoten **Hierarchiekonfiguration**, **Cloud** für den cloudbasierten Verteilungspunkt der Status **Bereit** angezeigt.  

-   In Configuration Manager wird eine Statusmeldung mit der ID **9409** für die Komponente SMS_CLOUD_SERVICES_MANAGER angezeigt.  

##  <a name="BKMK_ConfigDNSforCloudDPs"></a> Einrichten der Namensauflösung für cloudbasierte Verteilungspunkte  
 Damit Clients auf den cloudbasierten Verteilungspunkt zugreifen können, muss auf diesen Clients der Name des cloudbasierten Verteilungspunkts in eine IP-Adresse aufgelöst werden können, die von Azure verwaltet wird. Dies erfolgt bei Clients in zwei Phasen:  

1.  Der mit dem Dienstzertifikat für cloudbasierte Verteilungspunkte von Configuration Manager definierte Dienstname wird dem Dienst-FQDN von Azure zugeordnet. Dieser FQDN enthält eine GUID und das DNS-Suffix von **cloudapp.net**. Die GUID wird nach der Installation des cloudbasierten Verteilungspunkts automatisch generiert. Den vollständigen FQDN können Sie im Azure-Portal anzeigen, indem Sie im Dashboard des Clouddiensts auf die **SITE-URL** verweisen. Die URL einer Website kann beispielsweise **http://d1594d4527614a09b934d470.cloudapp.net**lauten.  

2.  Damit wird die Dienst-FQDN von Azure in die von Azure zugewiesene IP-Adresse aufgelöst. Diese IP-Adresse kann auch im Dashboard des Clouddiensts des Azure-Portals ermittelt werden und trägt die Bezeichnung **ÖFFENTLICHE VIRTUELLE IP-ADRESSE**.  

DNS-Server im Internet müssen über einen DNS-Alias verfügen (CNAME-Eintrag), damit der Dienstname, den Sie mit dem Dienstzertifikat für cloudbasierte Verteilungspunkte von Configuration Manager angegeben haben (z.B. **clouddp1.contoso.com**), dem Dienst-FQDN von Azure zugeordnet wird (z.B. **d1594d4527614a09b934d470.cloudapp.net**). Von Clients kann dann unter Verwendung der DNS-Server im Internet der Dienst-FQDN von Azure in die IP-Adresse aufgelöst werden.  

##  <a name="BKMK_ConfigProxyforCloud"></a> Einrichten von Proxyeinstellungen für primäre Standorte, von denen Clouddienste verwaltet werden  
 Wenn Sie Clouddienste mit Configuration Manager verwenden, muss an dem primären Standort, von dem der cloudbasierte Verteilungspunkt verwaltet wird, eine Verbindung zum Azure-Portal hergestellt werden können. Verwendet wird dazu das Konto **System** des primären Standortcomputers. Diese Verbindung wird über den Standardwebbrowser auf dem Computer des primären Standortservers hergestellt.  

 Auf dem primären Standortserver, von dem der cloudbasierte Verteilungspunkt verwaltet wird, müssen Sie möglicherweise Proxyeinstellungen einrichten, damit der primäre Standort Zugriff auf das Internet und Azure erhält.  

 Gehen Sie wie folgt vor, um Proxyeinstellungen für den primären Standortserver in der Configuration Manager-Konsole einzurichten.  

> [!TIP]  
>  Sie können auch den **Assistenten zum Hinzufügen von Standortsystemrollen** verwenden, um den Proxyserver beim Installieren neuer Standortsystemrollen auf dem primären Standortserver einzurichten.  

#### <a name="to-set-up-proxy-settings-for-the-primary-site-server"></a>So richten Sie Proxyeinstellungen für den primären Standortserver ein  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Standortkonfiguration**, und klicken Sie dann auf **Server und Standortsystemrollen**. Wählen Sie dann den primären Standortserver aus, von dem der cloudbasierte Verteilungspunkt verwaltet wird.  

3.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **Standortsystem**, und klicken Sie dann auf **Eigenschaften**.  

4.  Wählen Sie unter **Eigenschaften des Standortsystems** die Registerkarte **Proxy** aus, und richten Sie die Proxyeinstellungen für diesen primären Standortserver ein.  

5.  Klicken Sie auf **OK**, um die Einstellungen zu speichern.  
