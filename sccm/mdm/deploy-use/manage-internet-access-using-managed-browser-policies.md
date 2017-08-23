---
title: "Verwalten des Internetzugriffs mittels Richtlinien für verwaltete Browser | Microsoft-Dokumentation"
description: "Stellen Sie Intune Managed Browser bereit, um den Zugriff auf das Internet zu verwalten und einzuschränken."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
caps.latest.revision: "6"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: d2dd2c25a2714851ba1e71414cabcef38d3ce014
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Verwalten des Internetzugriffs mittels Richtlinien für verwaltete Browser mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager können Sie die Webbrowseranwendung Intune Managed Browser bereitstellen und der Anwendung eine Richtlinie für verwaltete Browser zuordnen. Die Richtlinie für verwaltete Browser konfiguriert die Liste „Zulassen“ oder „Blockieren“, um die Websites einzuschränken, die Benutzer des verwalteten Browsers besuchen können.  

 Da diese App eine verwaltete App ist, können Sie auch Richtlinien zur mobilen Anwendungsverwaltung anwenden, wie die Kontrolle über den Einsatz von „Ausschneiden“, „Kopieren“ und „Einfügen“. Dies verhindert Bildschirmaufnahmen und stellt zudem sicher, dass sich Links zu Inhalten nur in anderen verwalteten Apps öffnen. Weitere Informationen finden Sie unter [Schützen von Apps mit Verwaltungsrichtlinien für mobile Anwendungen](protect-apps-using-mam-policies.md).  

> [!IMPORTANT]  
>  Wenn Benutzer den verwalteten Browser selbst installieren, wird er durch keine von Ihnen angegebenen Richtlinien verwaltet. Um sicherzustellen, dass der Browser von Configuration Manager verwaltet wird, muss die App deinstalliert werden, bevor Sie sie als verwaltete Anwendung bereitstellen können.  

 Sie können Richtlinien für verwaltete Browser für die folgenden Gerätetypen erstellen:  

-   Geräte unter Android 4 und höher  

-   Geräte unter iOS 7 und höher  

> [!NOTE]  
>  Weitere Informationen zur Intune Managed Browser-App und wie Sie sie herunterladen können, finden Sie unter [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) für iOS und [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) für Android.  

## <a name="create-a-managed-browser-policy"></a>Erstellen einer Richtlinie für verwaltete Browser  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Richtlinien zur Anwendungsverwaltung** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Create Application Management Policy** (Anwendungsverwaltungsrichtlinie erstellen).  

4.  Geben Sie auf der Seite **Allgemein** den Namen und die Beschreibung für die Richtlinie ein, und wählen Sie anschließend **Weiter** aus.  

5.  Wählen Sie auf der Seite **Richtlinientyp** die Plattform aus, wählen Sie **Verwalteter Browser** als Richtlinientyp aus, und wählen Sie anschließend **Weiter**.  

     Wählen Sie auf der Seite **Verwalteter Browser** eine der folgenden Optionen aus:  

    -   **Der verwaltete Browser kann nur die unten aufgeführten URLs öffnen**: Geben Sie eine Liste mit URLs an, die der verwaltete Browser öffnen kann.  

    -   **Der verwaltete Browser kann die unten aufgeführten URLs nicht öffnen**: Geben Sie eine Liste mit URLs an, die der verwaltete Browser nicht öffnen kann.  

    > [!NOTE]  
    >  Eine Richtlinie für verwaltete Browser kann nicht sowohl zulässige als auch blockierte URLs enthalten.  

     Weitere Informationen zu den festlegbaren URL-Formaten finden Sie in diesem Artikel unter „URL-Format für zulässige und blockierte URLs“.  

    > [!NOTE]  
    >  Mit dem Richtlinientyp „Allgemein“ können Sie die Funktionalität von bereitgestellten Apps ändern, um sie an die Konformitäts- und Sicherheitsrichtlinien Ihres Unternehmens anzupassen. Sie können z. B. Ausschneide-, Kopier- und Einfügevorgänge innerhalb einer eingeschränkten App einschränken. Weitere Informationen zum Richtlinientyp „Allgemein“ finden Sie unter [Schützen von Apps mithilfe von Verwaltungsrichtlinien für mobile Anwendungen](protect-apps-using-mam-policies.md).  

6.  Beenden Sie den Assistenten.  

Die neue Richtlinie wird im Knoten **Anwendungsverwaltungsrichtlinien** des Arbeitsbereichs **Softwarebibliothek** angezeigt.  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Erstellen einer Softwarebereitstellung für die Managed Browser-App  
 Nachdem Sie die Richtlinie für verwaltete Browser erstellt haben, können Sie einen Softwarebereitstellungstyp für die Managed Browser-App erstellen. Sie müssen der Managed Browser-App eine Richtlinie „Allgemein“ und eine Richtlinie „Verwalteter Browser“ zuordnen.  

 Weitere Informationen finden Sie unter [Erstellen von Anwendungen](create-applications.md).  

## <a name="security-and-privacy-for-the-managed-browser"></a>Sicherheit und Datenschutz für den verwalteten Browser  

-   Auf iOS-Geräten können Websites, deren Zertifikat abgelaufen oder nicht vertrauenswürdig ist, nicht geöffnet werden.  

-   Einstellungen, die Benutzer für den integrierten Browser auf ihren Geräten vornehmen, werden nicht vom verwalteten Browser verwendet. Der verwaltete Browser hat keinen Zugriff auf diese Einstellungen.  

-   Wenn Sie die Option **Einfache PIN für Zugriff anfordern** oder **Unternehmensanmeldeinformationen für Zugriff anfordern** in einer Richtlinie für die Verwaltung mobiler Anwendung einrichten, die mit dem verwalteten Browser verknüpft ist, kann ein Benutzer auf der Authentifizierungsseite auf „Hilfe“ klicken und anschließend beliebige Websites durchsuchen, selbst wenn diese in der Richtlinie für verwaltete Browser einer Sperrliste hinzugefügt wurden.  

-   Der verwaltete Browser kann nur den Zugriff auf Websites blockieren, wenn darauf direkt zugegriffen wird. Der Zugriff auf die Website kann nicht blockiert werden, wenn dafür Zwischendienste (z. B. ein Übersetzungsdienst) verwendet werden.  

## <a name="reference-information"></a>Referenzinformationen  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>URL-Format für zulässige und blockierte URLs  

Nachfolgend wird erläutert, welche Formate und Platzhalter Sie zum Festlegen von URLs in den Zulassungs- und Sperrlisten verwenden können.  

-   Sie können das Platzhaltersymbol '**\***"gemäß den Regeln in der nachfolgenden Liste mit zugelassenen Mustern verwenden.  

-   Stellen Sie sicher, dass Sie bei der Eingabe in die Liste allen URLs **http** oder **https** voranstellen.  

-   Sie können Portnummern in der Adresse angeben. Wenn Sie keine Portnummer angeben, werden folgende Werte verwendet:  

    -   Port 80 für http  

    -   Port 443 für https  

     Das Verwenden von Platzhaltern für die Portnummer wird nicht unterstützt: Beispiele: **http://www.contoso.com:\*** und **http://www.contoso.com: /\***  

-   In der folgenden Tabelle sind die zugelassenen Muster aufgeführt, die Sie zum Festlegen von URLs verwenden können:  

    |URL|Treffer|Stimmt nicht überein mit|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> Entspricht einer einzelnen Seite|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> Entspricht einer einzelnen Seite|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> Entspricht allen URLs, die mit www.contoso.com beginnen|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> Entspricht allen Unterdomänen unter "contoso.com"|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> Entspricht einem einzelnen Ordner|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> Entspricht einer einzelnen Seite mit einer Portnummer|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> Entspricht einer einzelnen, sicheren Seite|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> Entspricht einem einzelnen Ordner und allen Unterordnern|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   Es folgen Beispiele für einige der Eingaben, die Sie nicht festlegen können:  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*Schweine  

    -   www.contoso.com/page*  

    -   IP-Adressen  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com:*  

    -   http://www.contoso.com: / *  

> [!NOTE]  
>  *. microsoft.com ist immer zulässig.  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Lösen von Konflikten zwischen der Zulassungs- und Sperrliste  
 Wenn mehrere Richtlinien für verwaltete Browser für ein Gerät bereitgestellt werden und Einstellungen in Konflikt stehen, werden sowohl der Modus (zulassen oder blockieren) als auch die URL-Listen ausgewertet. Bei einem Konflikt gilt folgendes Verhalten:  

-   Wenn die Modi in jeder Richtlinie identisch sind, aber die URL-Listen voneinander abweichen, werden die URLs auf dem Gerät nicht erzwungen.  

-   Wenn die Modi in jeder Richtlinie voneinander abweichen, aber die URL-Listen identisch sind, werden die URLs auf dem Gerät nicht erzwungen.  

-   Wenn ein Gerät erstmals Richtlinien für verwaltete Browser empfängt und zwei Richtlinien in Konflikt stehen, werden die URLs auf dem Gerät nicht erzwungen. Sie können die Konflikte über den Knoten **Richtlinienkonflikte** des Arbeitsbereichs **Richtlinie** anzeigen.  

-   Wenn ein Gerät bereits ein Richtlinie für verwaltete Browser erhalten hat und eine zweite Richtlinie mit in Konflikt stehenden Einstellungen bereitgestellt wird, bleiben die ursprünglichen Einstellungen auf dem Gerät bestehen. Sie können die Konflikte über den Knoten **Richtlinienkonflikte** des Arbeitsbereichs **Richtlinie** anzeigen.  
