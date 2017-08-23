---
title: Erstellen von Sammlungen | Microsoft-Dokumentation
description: "Erstellen Sie Sammlungen in System Center Configuration Manager, um Benutzergruppen und Geräte leichter zu verwalten."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 44b4707b1a40624c51decf548d23ddd2164c5833
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Erstellen von Sammlungen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Bei Sammlungen handelt es sich um Gruppierungen von Benutzern und Geräten. Mithilfe von Sammlungen lassen sich zahlreiche Aufgaben ausführen, z.B. die Verwaltung von Anwendungen, die Bereitstellung von Konformitätseinstellungen und die Installation von Softwareupdates. Außerdem können Sammlungen zur Verwaltung von Clienteinstellungsgruppen verwendet werden. Möglich ist auch eine Verwendung von Sammlungen mit rollenbasierter Verwaltung zum Angeben der Ressourcen, auf die ein Administrator zugreifen kann. In Configuration Manager sind einige Sammlungen bereits integriert. Weitere Informationen finden Sie unter [Einführung in Sammlungen in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  Eine Sammlung kann nur Benutzer oder Geräte enthalten, aber nicht beide.  

 In der folgenden Tabelle werden Regeln aufgeführt, mit denen Sie die Mitglieder einer Sammlung in Configuration Manager konfigurieren können.  

|Typ der Mitgliedschaftsregel|Weitere Informationen|  
|--------------------------|----------------------|  
|Direktregel|Zur Auswahl der Benutzer oder Computer, die Sie zu einer Sammlung hinzufügen möchten. Diese Mitgliedschaft ändert sich nicht, es sei denn, Sie entfernen eine Ressource aus Configuration Manager. Die Ressourcen müssen von Configuration Manager ermittelt oder von Ihnen importiert worden sein, bevor Sie sie einer Direktregelsammlung hinzufügen können. Direktregelsammlungen bedeuten einen höheren Verwaltungsaufwand als Abfrageregelsammlungen, weil dieser Sammlungstyp manuell geändert werden muss.|  
|Abfrageregel|Aktualisieren Sie die Mitgliedschaft dynamisch auf Basis einer Abfrage, die von Configuration Manager nach einem Zeitplan ausgeführt wird. Sie können beispielsweise eine Sammlung von Benutzern erstellen, die Mitglieder der Organisationseinheit "Personal" in den Active Directory-Domänendiensten sind. Diese Sammlung wird automatisch aktualisiert, wenn neue Benutzer der Organisationseinheit „Personalwesen“ hinzugefügt bzw. daraus entfernt werden.<br /><br /> Weitere Informationen zu Abfragen, die Sie zum Erstellen von Sammlungen verwenden können, finden Sie unter [Erstellen von Abfragen in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Regel "Sammlungen einschließen"|Nehmen Sie die Mitglieder einer anderen Sammlung in eine Configuration Manager-Sammlung auf. Die Mitgliedschaft der aktuellen Sammlung wird nach einem Zeitplan aktualisiert, wenn sich die eingeschlossene Sammlung ändert.<br /><br /> Sie können einer Sammlung mehrere Regeln "Sammlungen einschließen" hinzufügen.<br /> |  
|Regel "Sammlungen ausschließen"|Mit der Regel „Sammlungen ausschließen“ können Sie die Mitglieder einer anderen Sammlung aus einer Configuration Manager-Sammlung ausschließen. Die Mitgliedschaft der aktuellen Sammlung wird nach einem Zeitplan aktualisiert, wenn sich die ausgeschlossene Sammlung ändert.<br /><br /> Sie können einer Sammlung mehrere Regeln "Sammlungen ausschließen" hinzufügen. Wenn eine Sammlung sowohl die Regel „Sammlungen einschließen“ als auch die Regel „Sammlungen ausschließen“ enthält und die Regeln in Konflikt stehen, hat die Regel „Sammlungen ausschließen“ Priorität.<br />              **Beispiel:** Sie erstellen eine Sammlung, die eine Regel "Sammlungen einschließen" und eine Regel "Sammlungen ausschließen" enthält. Die Regel "Sammlungen einschließen" bezieht sich auf eine Sammlung von Dell-Desktops. Die Regel "Sammlungen ausschließen" bezieht sich auf eine Sammlung von Computern mit weniger als 4 GB RAM. Die neue Sammlung enthält Dell-Desktops, die über mindestens 4 GB RAM verfügen.|  

 Die folgenden Prozeduren helfen Ihnen beim Erstellen von Sammlungen in Configuration Manager. Sie können auch Sammlungen importieren, die an diesem oder einem anderen Configuration Manager-Standort erstellt wurden. Informationen zum Exportieren und Importieren von Sammlungen finden Sie unter [Verwalten von Sammlungen in Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Informationen zum Erstellen von Sammlungen für Computer unter Linux und UNIX finden Sie unter [Verwalten von Clients für Linux- und UNIX-Server in System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="BKMK_1"></a> So erstellen Sie eine Gerätesammlung  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** > **Gerätesammlungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Gerätesammlung erstellen** aus.  

4.  Geben Sie auf der Seite **Allgemein** einen **Namen** und einen **Kommentar** ein. Wählen Sie anschließend in **Begrenzende Sammlung** zum Auswählen einer begrenzenden Sammlung **Durchsuchen** aus. In dieser Sammlung sind nur Mitglieder aus der begrenzenden Sammlung enthalten.  

5.  Wählen Sie auf der Seite **Mitgliedschaftsregeln** des **Assistenten zum Erstellen von Gerätesammlungen** in der Liste **Regel hinzufügen** den Typ der Mitgliedschaftsregel aus, den Sie für diese Sammlung verwenden möchten. Sie können für jede Sammlung mehrere Regeln konfigurieren.  

        
##### <a name="to-configure-a-direct-rule"></a>So konfigurieren Sie eine Direktregel  

1.  Geben Sie im **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft** auf der Seite **Ressourcen suchen**die folgenden Informationen an:  

-   **Ressourcenklasse**: Wählen Sie den Ressourcentyp aus, den Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie aus den Werten unter **Systemressource** Werte zur Suche nach Inventurdaten aus, die von Clientcomputern zurückgegeben wurden, oder wählen Sie **Unbekannter Computer** aus, um Werte auszuwählen, die von unbekannten Computern zurückgegeben wurden.  

-   **Attributname**: Wählen Sie das Attribut aus, das der ausgewählten Ressourcenklasse zugeordnet ist, nach der Sie suchen möchten. Wenn Sie Computer beispielsweise nach NetBIOS-Namen auswählen möchten, wählen Sie in der Liste **Ressourcenklasse** die Option **Systemressource** und in der Liste **Attributname** die Option **NetBIOS-Name** aus.  

-   **Als veraltet markierte Ressourcen ausschließen:** Wenn ein Clientcomputer als veraltet markiert wird, schließen Sie diesen Wert nicht in die Suchergebnisse ein.  

-   **Ressourcen ausschließen, für die der Configuration Manager-Client nicht installiert wurde**: Diese Ressourcen werden nicht in den Suchergebnissen angezeigt.  

-   **Wert** : Geben Sie einen Wert ein, für den Sie den ausgewählten Attributnamen suchen möchten. Sie können das Prozentzeichen **%** als Platzhalter verwenden. Um beispielsweise nach Computern zu suchen, deren NetBIOS-Name mit einem „M“ beginnt, geben Sie in dieses Feld **M%** ein.  

2.  Wählen Sie auf der Seite **Ressourcen auswählen** die Ressourcen aus, die Sie der Sammlung in der Liste **Ressourcen** hinzufügen möchten, und wählen Sie dann **Weiter** aus.  


##### <a name="to-configure-a-query-rule"></a>So konfigurieren Sie eine Abfrageregel  

1.  Geben Sie im Dialogfeld **Eigenschaften für Abfrageregel** die folgenden Informationen an:  

-   **Name**: Geben Sie einen eindeutigen Namen an.  

-   **Abfrageanweisung importieren**: Öffnet das Dialogfeld **Abfrage durchsuchen**, in dem Sie eine [Configuration Manager-Abfrage](../../../../core/servers/manage/create-queries.md) auswählen können, die als Abfrageregel für die Sammlung verwendet werden soll.   

-   **Ressourcenklasse**: Wählen Sie in der Liste den Ressourcentyp aus, den Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie aus den Werten unter **Systemressource** einen Wert zur Suche von Inventurdaten aus, die von Clientcomputern zurückgegeben wurden, oder wählen Sie **Unbekannter Computer** aus, um Werte auszuwählen, die von unbekannten Computern zurückgegeben wurden.  

-   **Abfrageanweisung bearbeiten:** Öffnet das Dialogfeld **Eigenschaften der Abfrageanweisung**, in dem Sie eine Abfrage erstellen können, die als Regel für die Sammlung verwendet werden soll. Weitere Informationen zu Abfragen finden Sie unter [Abfragen – Technische Referenz für System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

    
##### <a name="to-configure-an-include-collection-rule"></a>So konfigurieren Sie eine Regel "Sammlungen einschließen"  

Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie in die neue Sammlung einschließen möchten, und wählen Sie dann **Weiter** aus.  

##### <a name="to-configure-an-exclude-collection-rule"></a>So konfigurieren Sie eine Regel "Sammlungen ausschließen"  

Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie aus der neuen Sammlung ausschließen möchten, und wählen Sie dann **OK** aus.  

-   **Inkrementelle Updates für diese Sammlung verwenden**: Wählen Sie diese Option aus, um regelmäßig eine Überprüfung auf nur neue oder geänderte Ressourcen aus der vorherigen Sammlungsauswertung auszuführen und sie zu aktualisieren, unabhängig von einer vollständigen Sammlungsauswertung. Inkrementelle Updates erfolgen in Abständen von 10 Minuten.  

> [!IMPORTANT]  
>  Von Sammlungen, die mit Abfrageregeln erstellt wurden, in denen folgende Klassen verwendet werden, werden inkrementelle Updates nicht unterstützt:  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (nur für Benutzersammlungen)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (nur für Benutzersammlungen)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **Vollständiges Update für diese Sammlung planen**: Planen Sie eine reguläre, vollständige Auswertung der Sammlungsmitgliedschaft.  

6.  Schließen Sie den Assistenten ab, um die neue Sammlung zu erstellen. Die neue Sammlung wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Gerätesammlungen** angezeigt.  

> [!NOTE]  
>  Sie müssen die Configuration Manager-Konsole aktualisieren oder erneut laden, um die Sammlungsmitglieder anzuzeigen. Allerdings werden die Mitglieder erst nach dem ersten geplanten Update in der Sammlung angezeigt, oder nachdem Sie manuell **Mitgliedschaft aktualisieren** für die Sammlung ausgewählt haben. Es dauert möglicherweise ein paar Minuten, bis die Aktualisierung einer Sammlung abgeschlossen ist.  

##  <a name="BKMK_2"></a> So erstellen Sie eine Benutzersammlung  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** > **Benutzersammlungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Benutzersammlung erstellen** aus.  

4.  Geben Sie auf der Seite **Allgemein** des Assistenten einen **Namen** und einen **Kommentar** ein. Wählen Sie anschließend in **Begrenzende Sammlung** zum Auswählen einer begrenzenden Sammlung **Durchsuchen** aus. In dieser Sammlung sind nur Mitglieder aus der begrenzenden Sammlung enthalten.  

5.  Geben Sie auf der Seite **Mitgliedschaftsregeln** Folgendes ein:  

    -   Wählen Sie in der Liste **Regel hinzufügen** den Typ der Mitgliedschaftsregel aus, den Sie für diese Sammlung verwenden möchten. Sie können für jede Sammlung mehrere Regeln konfigurieren.  

##### <a name="to-configure-a-direct-rule"></a>So konfigurieren Sie eine Direktregel  

1.  Geben Sie im **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft** auf der Seite **Ressourcen suchen** Folgendes an:  

-   **Ressourcenklasse**: Wählen Sie den Ressourcentyp aus, den Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie Werte unter **Benutzerressource** aus, um Benutzerinformationen zu suchen, die von Configuration Manager gesammelt wurden, oder unter **Benutzergruppenressource**, um Benutzergruppeninformationen zu suchen, die von Configuration Manager gesammelt wurden.  

-   **Attributname**: Wählen Sie das Attribut aus, das der Ressourcenklasse zugeordnet ist, nach der Sie suchen möchten. Wenn Sie Benutzer beispielsweise nach dem Namen der Organisationseinheit auswählen möchten, wählen Sie in der Liste **Ressourcenklasse** die Option **Benutzerressource** und in der Liste **Attributname** die Option **Benutzer-Organisationseinheitsname** aus.  

-   **Wert:** Geben Sie einen Wert ein, nach dem Sie suchen möchten. Sie können das Prozentzeichen **%** als Platzhalter verwenden. Wenn Sie beispielsweise nach Benutzern in der Organisationseinheit „Contoso“ suchen, geben Sie **Contoso** in dieses Feld ein.  

2.  Wählen Sie auf der Seite **Ressourcen auswählen** die Ressourcen aus, die Sie der Sammlung in der Liste **Ressourcen** hinzufügen möchten.  

##### <a name="to-configure-a-query-rule"></a>So konfigurieren Sie eine Abfrageregel  

1.  Geben Sie im Dialogfeld **Eigenschaften für Abfrageregel** Folgendes an:  

-   **Name**: Einen eindeutigen Namen.  

-   **Abfrageanweisung importieren**: Öffnet das Dialogfeld **Abfrage durchsuchen**, in dem Sie eine [Configuration Manager-Abfrage](../../../../core/servers/manage/queries-technical-reference.md) auswählen können, die als Abfrageregel für die Sammlung verwendet werden soll.  

-   **Ressourcenklasse**: Wählen Sie den Ressourcentyp aus, den Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie Werte unter **Benutzerressource** aus, um Benutzerinformationen zu suchen, die von Configuration Manager gesammelt wurden, oder unter **Benutzergruppenressource**, um Benutzergruppeninformationen zu suchen, die von Configuration Manager gesammelt wurden.  

-   **Abfrageanweisung bearbeiten**: Öffnet das Dialogfeld **Eigenschaften der Abfrageanweisung**, in dem Sie eine [Abfrage erstellen](../../../../core/servers/manage/queries-technical-reference.md) können, die als Regel für die Sammlung verwendet werden soll.  

##### <a name="to-configure-an-include-collection-rule"></a>So konfigurieren Sie eine Regel "Sammlungen einschließen"  

Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie in die neue Sammlung einschließen möchten, und wählen Sie dann **Weiter** aus.  

##### <a name="to-configure-an-exclude-collection-rule"></a>So konfigurieren Sie eine Regel "Sammlungen ausschließen"  

Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie aus der neuen Sammlung ausschließen möchten, und wählen Sie dann **OK** aus.  


-   **Inkrementelle Updates für diese Sammlung verwenden**: Wählen Sie diese Option aus, um regelmäßig eine Überprüfung auf nur neue oder geänderte Ressourcen aus der vorherigen Sammlungsauswertung auszuführen und sie zu aktualisieren, unabhängig von einer vollständigen Sammlungsauswertung. Inkrementelle Updates erfolgen in Abständen von 10 Minuten.  

> [!IMPORTANT]  
>  Von Sammlungen, die mit Abfrageregeln erstellt wurden, in denen folgende Klassen verwendet werden, werden inkrementelle Updates nicht unterstützt:  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (nur für Benutzersammlungen)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (nur für Benutzersammlungen)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **Vollständiges Update für diese Sammlung planen**: Wählen Sie diese Option aus, um eine reguläre, vollständige Auswertung der Sammlungsmitgliedschaft zu planen.  

6.  Schließen Sie den Assistenten ab. Die neue Sammlung wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Benutzersammlungen** angezeigt.  

> [!NOTE]  
>  Sie müssen die Configuration Manager-Konsole aktualisieren oder erneut laden, um die Sammlungsmitglieder anzuzeigen. Allerdings werden die Mitglieder erst nach dem ersten geplanten Update oder nachdem Sie manuell **Mitgliedschaft aktualisieren** für die Sammlung ausgewählt haben in der Sammlung angezeigt. Es dauert möglicherweise ein paar Minuten, bis die Aktualisierung einer Sammlung abgeschlossen ist.  

##  <a name="BKMK_3"></a> So importieren Sie eine Sammlung  

1.  Wählen Sie in der Configuration Manager-Konsole **Bestand und Konformität** > **Benutzersammlungen** oder **Gerätesammlungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Sammlungen importieren** aus.  

4.  Wählen Sie im **Assistenten zum Importieren von Sammlungen** auf der Seite **Allgemein** **Weiter** aus.  

5.  Wählen Sie auf der Seite **MOF-Dateiname** **Durchsuchen** aus, und suchen Sie dann die MOF-Datei, die die zu importierenden Sammlungsinformationen enthält.  

    > [!NOTE]  
    >  Die zu importierende Datei muss von einem Standort exportiert worden sein, an dem dieselbe Configuration Manager-Version wie am Zielstandort ausgeführt wird. Weitere Informationen zum Exportieren von Sammlungen finden Sie unter [Verwalten von Sammlungen in Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Schließen Sie den Assistenten ab, um die Sammlung zu importieren. Die neue Sammlung wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Benutzersammlungen** oder **Gerätesammlungen** angezeigt. Aktualisieren Sie die Configuration Manager-Konsole, oder laden Sie sie erneut, um die Sammlungsmitglieder für die neu importierte Sammlung anzuzeigen.  
