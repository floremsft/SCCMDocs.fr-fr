---
title: "Assistent für Azure-Dienste | Microsoft-Dokumentation"
description: "Informationen zum Assistent für Azure-Dienste in System Center Configuration Manager"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Konfigurieren von Azure-Diensten zur Verwendung mit dem Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Ab der Current Branch-Version 1706 kommt der **Azure Services Wizard** (Assistent für Azure-Dienste) zum Einsatz, um die Konfiguration der von Ihnen verwendeten Azure-Dienste mit Configuration Manager zu vereinfachen.

Dieser Assistent bietet eine allgemeine Konfigurationserfahrung mithilfe einer **Azure-Web-App**, die Details zu Abonnements und Konfigurationen bereitstellt. Durch die Web-App müssen sie nicht jedes Mal dieselben Informationen erneut eingeben, wenn Sie mit Azure eine neue Komponente oder einen neuen Dienst für den Configuration Manager einrichten.

Die folgenden Azure-Dienste werden mithilfe des Assistenten zum Konfigurieren von Azure-Diensten konfiguriert:
-   **Cloud Management**  (Cloudverwaltung)  
    [Enable clients to authenticate by using Azure Active Directory (Authentifizieren von Clients mithilfe von Azure Active Directory ermöglichen)]() (Azure AD). Sie können ebenfalls die [Azure AD-Benutzerermittlung konfigurieren](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **OMSConnector**
     (OMS-Connector):[ Connect to Operations Manager Suite (Stellen Sie eine Verbindung mit der Operations Manager-Suite)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) her und synchronisieren Sie die Daten wie Sammlungen mit der OMS-Protokollanalyse.
-   **Upgrade Readiness (Upgradebereitschaft)**
    [Connect to Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) (Verbinden Sie sich mit Upgrade Readiness), um Daten zur Kompatibilität von Clientupgrades anzuzeigen.
-   **Windows Store for Business** Verbinden Sie sich mit dem Onlineshop [Windows Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business), um Apps für Ihre Organisation zu erhalten, die Sie mit dem Configuration Manager bereitstellen können.

Wenn Sie den Assistenten verwenden, um einen Dienst zu konfigurieren, sind einige gängige Aktionen verfügbar.
Dazu gehören:
-   Konfigurieren der Azure-Umgebung: Wählen Sie auf der **App**-Seite des Assistenten die **Azure-Umgebung**, die Sie verwenden. Lassen Sie den Inhalt jedes Dienstes anzeigen, um zu erfahren, ob dieser nur die öffentliche oder auch die private Azure-Cloud unterstützt.
-   Erstellen oder Importieren einer Server-App: Auf der **App**-Seite des Assistenten können Sie Azure-Web-Apps **Erstellen** und **Importieren**. Die verfügbaren Optionen sind abhängig vom Dienst, den Sie konfigurieren.  Darüber hinaus können einige Dienste eine zusätzliche App erfordern. Ein Dienst kann beispielsweise auch eine **Native Client App** (native Client-App) erfordern.


Weitere Informationen zu Azure-Web-Apps finden Sie unter [Authentication and authorization in Azure App Service (Authentifizierung und Autorisierung in Azure App Service)](/azure/app-service/app-service-authentication-overview), und [Web Apps overview (Überblick: Web-Apps)](/azure/app-service-web/app-service-web-overview)


## <a name="webapp"></a>Erstellen Sie die Azure-Web-App für die Verwendung mit Configuration Manager

Die Web-App für Azure-Dienste verbindet Ihren Configuration Manager-Standort mit Azure AD und ist eine Voraussetzung dafür, Azure-Dienste mit Ihrer Infrastruktur zu verwenden. Dazu ist Folgendes erforderlich:

1.  Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und klicken Sie dann auf **Azure-Dienste**.
2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Azure-Dienste** auf **Azure-Dienste konfigurieren**.
3.  Wählen Sie im Assistenten für Azure-Dienste auf der Seite **Azure-Dienste** die Option **Cloudverwaltung** aus, damit sich Clients in der Hierarchie mithilfe von Azure AD authentifizieren können.
4.  Geben Sie auf der Seite **Allgemein** des Assistenten einen Namen und eine Beschreibung für den Azure-Dienst ein.
5.  Wählen Sie auf der **App**-Seite des Assistenten in der Liste Ihre Azure-Umgebung aus, und klicken Sie auf **Durchsuchen**, um die *Web-App* und die *native Client-App* auszuwählen, die verwendet wird, um den Azure-Dienst zu konfigurieren.     
    **Web-App:** Mit „Durchsuchen“ wird das Server-App-Fenster geöffnet.    
      Wählen Sie im Fenster **Server-App** die Server-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**. Server-Apps sind Azure-Web-Apps, die Konfigurationen für Ihr Azure-Konto enthalten, einschließlich Ihrer Mandanten-ID, Client-ID und eines geheimen Schlüssels für Clients.
    Wenn Sie nicht über eine verfügbare App verfügen, verwenden Sie eine der folgenden:
        - **Erstellen**: Um eine neue Server-App zu erstellen, klicken Sie auf **Erstellen**. Geben Sie als nächstes einen Anzeigenamen für die App, die URL der Homepage, die URL der App-ID und eine Gültigkeitsdauer für den geheimen Schlüssel an. Standardmäßig ist die Gültigkeitsdauer des geheimen Schlüssels ein Jahr.

         Zum Fortsetzen des Vorgangs müssen Sie sich jetzt bei Azure anmelden, um dort die Erstellung der Web-App abzuschließen. Das Konto, das Sie verwenden, um sich bei Azure anzumelden, muss nicht dasselbe sein, auf dem der Assistent für Azure-Dienste ausgeführt wird. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager die Web-App in Azure für Sie, einschließlich der Client-ID und des geheimen Schlüssels für den Gebrauch mit der Web-App. Später können Sie diese im Azure-Portal anzeigen.

         Wenn Sie die Option „Erstellen“ verwenden, um eine Web-App zu konfigurieren, kann der Configuration Manager die Web-App für Sie in Azure AD erstellen.
        - **Importieren**: Um eine Web-App zu verwenden, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Stellen Sie einen Anzeigenamen für die App und den Mandanten bereit, und geben Sie dann die Mandanten-ID, Client-ID und den geheimen Schlüssel für die Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen überprüft haben, klicken Sie auf **OK**, um fortzufahren.

          Diese Option ist möglicherweise nicht für alle Dienste verfügbar, die Sie konfigurieren.

   **Native Client-App:** Mit „Durchsuchen“ wird das Client-App-Fenster geöffnet.  
     Wählen Sie im Fenster **Client-App** die Client-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.

     Wenn Sie nicht über eine verfügbare Client-App verfügen, verwenden Sie eine der folgenden:
     - **Erstellen**: Um eine neue Client-App zu erstellen, klicken Sie auf **Erstellen**. Geben Sie dann einen Anzeigenamen für die App und die Antwort-URL an.

          Zum Fortsetzen des Vorgangs müssen Sie sich jetzt bei Azure anmelden, um dort die Erstellung der Client-App abzuschließen. Das Konto, das Sie verwenden, um sich bei Azure anzumelden, muss nicht dasselbe sein, auf dem der Assistent für Azure-Dienste ausgeführt wird. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager daraufhin die native Client-App in Azure für Sie, einschließlich der Client-ID für den Gebrauch mit der Web-App. Später können Sie diese im Azure-Portal anzeigen.
          Wenn Sie die Option „Erstellen“ verwenden, um die App zu konfigurieren, kann der Configuration Manager die native Client-App für Sie in Azure AD erstellen.
     - **Importieren**: Um eine Client-App zu verwenden, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Geben Sie einen Anzeigenamen für die App und die Client-ID an. Klicken Sie dann auf **OK** , um den Vorgang fortzusetzen.
           Diese Option ist möglicherweise nicht für alle Dienste verfügbar, die Sie konfigurieren.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  Klicken Sie auf der Seite **Discovery** (Ermittlung) des Assistenten auf **Enable Azure Active Directory User Discovery** (Azure Active Directory-Benutzerermittlung aktivieren), und klicken Sie dann auf **Settings** (Einstellungen).
Konfigurieren Sie im Dialogfeld **Einstellungen der Azure AD-Benutzerermittlung** einen Zeitplan für die Ermittlung. Sie können auch die Deltaermittlung aktivieren, bei der nur eine Überprüfung auf neue oder geänderte Konten in Azure AD erfolgt. Erfahren Sie mir über die [Azure AD User Discovery (Azure AD-Benutzerermittlung](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).
 
 7. Schließen Sie den Assistenten ab.

An diesem Punkt haben Sie Ihren Configuration Manager-Standort mit Azure AD verbunden.

## <a name="view-the-configuration-of-an-azure-service"></a>Anzeigen der Konfiguration eines Azure-Diensts
Sie können die Eigenschaften eines Azure-Diensts anzeigen lassen, den Sie zur Verwendung konfiguriert haben.

Navigieren Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Azure-Dienste**. Wählen Sie anschließend den Dienst, den Sie anzeigen oder bearbeiten wollen, und klicken Sie dann auf **Properties** (Eigenschaften).
