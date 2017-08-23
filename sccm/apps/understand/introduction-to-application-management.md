---
title: "Einführung in die Anwendungsverwaltung | Microsoft Docs"
description: "Hier finden Sie die wichtigsten Informationen über das Verwalten und Bereitstellen von System Center Configuration Manager-Anwendungen."
ms.custom: na
ms.date: 12/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: "18"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 959a36413d06bb225f260bd44c1d3d59efd44e69
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>Einführung in die Anwendungsverwaltung in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Dieses Thema enthält die Grundlagen, die Sie vor der Arbeit mit System Center Configuration Manager-Anwendungen kennenlernen sollten.  

> [!TIP]  
>  Wenn Sie sich bereits mit der Verwaltung von Anwendungen in Configuration Manager auskennen, können Sie dieses Thema auch überspringen und zum Erstellen einer Beispielanwendung übergehen. Informationen hierzu finden Sie unter [Erstellen und Bereitstellen einer Anwendung mit System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Was ist eine Anwendung?  
 Obwohl der Begriff *Anwendung* in der Computertechnologie weit verbreitet ist, hat er in Configuration Manager eine andere Bedeutung. Stellen Sie sich eine Anwendung wie eine Schachtel vor. Diese Schachtel enthält mindestens einen Satz von Installationsdateien für ein Softwarepaket (als **Bereitstellungstyp** bezeichnet) und Anweisungen zum Bereitstellen der Software.  

 Bei der Bereitstellung der Anwendung für Geräte entscheiden **Anforderungen** , welcher Bereitstellungstyp auf dem Gerät installiert wird.  

 Eine Anwendung bietet viele weitere Möglichkeiten. Mehr zu diesen erfahren Sie bei der Lektüre dieses Leitfadens. In der folgenden Tabelle werden Konzepte vorgestellt, mit denen Sie sich vertraut machen sollten, bevor Sie sich eingehender mit dem Thema beschäftigen:  

|Konzept|Beschreibung|    
|-|-|  
|**Requirements**|In früheren Versionen von Configuration Manager wurde häufig eine Sammlung mit den Geräten erstellt, für die Sie eine Anwendung bereitstellen wollten. Obwohl Sie weiterhin eine Sammlung erstellen können, lassen sich mit Anforderungen detailliertere Kriterien für eine Anwendungsbereitstellung angeben.<br /><br /> Beispiel: Sie können angeben, dass eine Anwendung nur auf Geräten unter Windows 10 installiert werden darf. Dann können Sie die Anwendung auf Ihren Geräten bereitstellen. Allerdings wird sie nur auf Geräten mit Windows 10 installiert.<br /><br /> Durch Auswerten von Anforderungen wird von Configuration Manager bestimmt, ob eine Anwendung und deren Bereitstellungstypen installiert werden. Anschließend wird der für die Installation einer Anwendung richtige Bereitstellungstyp ermittelt. Die Anforderungsregeln werden entsprechend der Clienteinstellung **Erneute Auswertung für Bereitstellungen planen**standardmäßig alle sieben Tage erneut ausgewertet, um die Kompatibilität zu gewährleisten.<br /><br /> Weitere Informationen finden Sie unter [Erstellen und Bereitstellen einer Anwendung](../../apps/get-started/create-and-deploy-an-application.md).|  
|**Globale Bedingungen**|Obwohl Anforderungen mit einem bestimmten Bereitstellungstyp in einer einzelnen Anwendung verwendet werden, können Sie auch globale Bedingungen erstellen. Hierbei handelt es sich um eine Bibliothek mit vordefinierten Anforderungen, die Sie mit jeder Anwendung und jedem Anwendungstyp verwenden können.<br /><br /> Configuration Manager enthält eine Reihe integrierter globaler Bedingungen, und Sie können auch eigene erstellen.<br /><br /> Weitere Informationen finden Sie unter [Erstellen von globalen Bedingungen](../../apps/deploy-use/create-global-conditions.md).|  
|**Simulierte Bereitstellung**|Wertet die Anforderungen, die Erkennungsmethode und die Abhängigkeiten für eine Anwendung aus. Die Ergebnisse werden ausgegeben, ohne dass die Anwendung installiert wird.<br /><br /> Weitere Informationen finden Sie unter [Simulieren von Anwendungsbereitstellungen](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Bereitstellungsaktion**|Gibt an, ob Sie die bereitgestellte Anwendung installieren oder deinstallieren möchten (falls unterstützt).<br /><br /> Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md).|  
|**Bereitstellungszweck**|Gibt an, ob die Bereitstellungs-App **Erforderlich**oder **Verfügbar**ist.<br /><br /> **Erforderlich:** Die Anwendung wird gemäß dem eingerichteten Zeitplan automatisch bereitgestellt. Allerdings kann ein Benutzer den Bereitstellungsstatus der Anwendung (sofern dieser nicht ausgeblendet ist) nachverfolgen und die Anwendung vor Ablauf der Frist über das Softwarecenter installieren.<br /><br /> **Verfügbar** : Wenn die Anwendung für einen Benutzer bereitgestellt wird, ist sie für den Benutzer im Softwarecenter als veröffentlichte Anwendung sichtbar, und er kann sie bei Bedarf anfordern.<br /><br /> Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md).|  
|**Revisionen**|Wenn Sie an einer Anwendung oder an einem in einer Anwendung enthaltenen Bereitstellungstyp Änderungen vornehmen, wird in Configuration Manager eine neue Version der Anwendung erstellt. Sie können den Verlauf jeder Anwendungsrevision sowie deren Eigenschaften anzeigen, eine frühere Version einer Anwendung wiederherstellen oder eine alte Version löschen.<br /><br /> Weitere Informationen finden Sie unter [Aktualisieren und Außerkraftsetzen von Anwendungen](../../apps/deploy-use/update-and-retire-applications.md).|  
|**Erkennungsmethode**|Erkennungsmethoden werden verwendet, um zu ermitteln, ob eine bereitgestellte Anwendung bereits installiert ist. Wenn die Erkennungsmethode angibt, dass die Anwendung installiert ist, versucht Configuration Manager nicht, sie erneut zu installieren.<br /><br /> Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).|  
|**-Abhängigkeiten**|Mit Abhängigkeiten wird mindestens ein Bereitstellungstyp einer anderen Anwendung definiert, der installiert sein muss, bevor ein Bereitstellungstyp installiert wird. Sie können die abhängigen Bereitstellungstypen einrichten, die vor der Installation eines Bereitstellungstyps automatisch installiert werden.<br /><br /> Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).|  
|**Ablösung**|Configuration Manager ermöglicht es Ihnen, vorhandene Anwendungen mithilfe einer Ablösungsbeziehung zu aktualisieren oder zu ersetzen. Wenn Sie eine Anwendung ablösen, können Sie einen neuen Bereitstellungstyp als Ersatz für den Bereitstellungstyp der abgelösten Anwendung angeben. Sie können außerdem festlegen, ob vor dem Installieren der ablösenden Anwendung ein Upgrade der abzulösenden Anwendung ausgeführt oder die abzulösende Anwendung deinstalliert werden soll.<br /><br /> Weitere Informationen finden Sie unter [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).|  
|**Benutzerzentrierte Verwaltung**|Configuration Manager-Anwendungen unterstützen die benutzerorientierte Verwaltung, d.h., Sie können bestimmte Benutzer und Geräte einander zuordnen. Anstatt sich den Namen des Geräts eines Benutzers merken zu müssen, können Sie Apps für den Benutzer und das Gerät bereitstellen. Dank dieser Funktionalität können Sie dafür sorgen, dass die wichtigsten Apps stets auf jedem Gerät verfügbar sind, auf das ein bestimmter Benutzer zugreift. Beim Wechsel eines Benutzers zu einem neuen Computer können Sie auf dem Gerät automatisch die vom Benutzer verwendeten Apps installieren, bevor er sich anmeldet.<br /><br /> Weitere Informationen finden Sie unter [Verknüpfung von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).|  

## <a name="what-application-types-can-you-deploy"></a>Welche Anwendungstypen können bereitgestellt werden?  
 Configuration Manager unterstützt die Bereitstellung folgender App-Typen:  

- Windows Installer (MSI-Datei)
- Windows-App-Paket (*.appx, *.appxbundle)
- Windows-App-Paket (im Windows Store)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization 5
- Windows Mobile-CAB-Datei
- macOS  


Beim Verwalten von Geräten mit Microsoft Intune oder der lokalen Geräteverwaltung von Configuration Manager können Sie zusätzlich folgende App-Typen verwalten:

- Windows Phone-App-Paket (XAP-Datei)
- App-Paket für iOS (IPA-Datei)
- App-Paket für Android (APK-Datei)
- App-Paket für Android auf Google Play
- Windows Phone-App-Paket (in Windows Phone Store)
- Windows Installer über MDM
- Webanwendung



## <a name="state-based-applications"></a>Zustandsbasierte Anwendungen  
 Configuration Manager-Anwendungen verwenden eine zustandsbasierte Überwachung, mit deren Hilfe Sie den letzten Anwendungsbereitstellungszustand für Benutzer und Geräte nachverfolgen können. In den Zustandsmeldungen werden Informationen zu einzelnen Geräten angezeigt. Wenn beispielsweise eine Anwendung für eine Sammlung von Benutzern bereitgestellt wird, können Sie den Kompatibilitätszustand und den Zweck der Bereitstellung in der Configuration Manager-Konsole anzeigen. Sie können die Bereitstellung sämtlicher Software mithilfe des Arbeitsbereichs **Überwachung** in der Configuration Manager-Konsole überwachen. Softwarebereitstellungen umfassen Softwareupdates, Kompatibilitätseinstellungen, Anwendungen, Tasksequenzen sowie Pakete und Programme. Weitere Informationen finden Sie unter [Überwachen von Anwendungen](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Anwendungsbereitstellungen werden regelmäßig von Configuration Manager neu ausgewertet. Beispiel:  

-   Eine bereitgestellte Anwendung wird vom Endbenutzer deinstalliert. Im nächsten Auswertungszyklus wird von Configuration Manager festgestellt, dass die Anwendung nicht vorhanden ist, und sie wird erneut installiert.  

-   Eine Anwendung wurde nicht auf einem Gerät installiert, da es die Anforderungen nicht erfüllt. Später wird eine Änderung an dem Gerät vorgenommen, sodass es die Anforderungen erfüllt. Configuration Manager erkennt diese Änderung, und die Anwendung wird installiert.  


 Sie können das Intervall der erneuten Bewertung von Anwendungsbereitstellungen mithilfe der Clienteinstellung **Erneute Auswertung für Bereitstellungen planen** einrichten. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md).  

## <a name="get-started-creating-an-application"></a>Erste Schritte beim Erstellen einer Anwendung  
 Wenn Sie direkt mit dem Erstellen einer Anwendung beginnen möchten, finden Sie im Thema [Erstellen und Bereitstellen einer Anwendung](../../apps/get-started/create-and-deploy-an-application.md) eine exemplarische Vorgehensweise zum Erstellen einer einfachen Anwendung.  

 Wenn Sie mit den Grundlagen vertraut sind und ausführlichere Referenzinformationen zu allen verfügbaren Optionen wünschen, beginnen Sie mit [Erstellen von Anwendungen](/sccm/apps/deploy-use/create-applications).  

## <a name="software-center-and-the-application-catalog"></a>Softwarecenter und der Anwendungskatalog  
 In früheren Versionen von Configuration Manager diente das Softwarecenter zum Installieren und Planen von Softwareinstallationen, zum Konfigurieren von Remotesteuerungseinstellungen und zum Einrichten der Energieverwaltung. Benutzer konnten den Anwendungskatalog durchsuchen, um Software zu suchen und anzufordern, Voreinstellungen einrichten und ihre mobilen Geräte remote zurücksetzen.  

 Diese Einstellungen sind in System Center Configuration Manager weiterhin verfügbar. Es gibt jedoch eine neue Version von Softwarecenter, die Ihnen das Suchen nach Anwendungen ermöglicht. Dazu müssen Sie nicht den Anwendungskatalog verwenden, für den ein Silverlight-fähiger Webbrowser erforderlich ist. Allerdings sind die Standortsystemrollen "Anwendungskatalog-Websitepunkt" und "Anwendungskatalog-Webdienstpunkt" nach wie vor erforderlich, damit für Benutzer verfügbare Apps im Softwarecenter angezeigt werden.  

 Weitere Informationen finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung](../../apps/plan-design/plan-for-and-configure-application-management.md).  

## <a name="configuration-manager-packages-and-programs"></a>Configuration Manager-Pakete und -Programme  
 Configuration Manager unterstützt auch weiterhin Pakete und Programme, die in vorherigen Produktversionen verwendet wurden. Eine Bereitstellung mit Paketen und Programmen kann beim Bereitstellen der folgenden Objekte besser geeignet sein als eine Bereitstellung, die eine Anwendung verwendet:  

-   Skripts, mit denen keine Anwendungen auf einem Computer installiert werden, z. B. ein Skript zum Defragmentieren der Computerfestplatte  

-   „Einmal-Skripts“, die nicht ständig überwacht werden müssen  

-   Skripts, die mit regelmäßiger Wiederholung ausgeführt werden und keine globale Auswertung verwenden können

 Weitere Informationen finden Sie unter [Pakete und Programme](../../apps/deploy-use/packages-and-programs.md).  
