---
title: Verwalten von per Volumenlizenz erworbenen iOS-Apps | Microsoft-Dokumentation
description: "Sie können Lizenzen für Apps, die Sie über den iOS App Store erworben haben, bereitstellen, verwalten und nachverfolgen."
ms.custom: na
ms.date: 05/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: ce706e938f558406044f7890c80bb7156c3b262b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Verwalten von iOS-Apps, die über ein Volumenprogramm erworben wurden, mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*



 Der iOS App Store bietet die Möglichkeit, mehrere Lizenzen für eine App zu kaufen, die in Ihrem Unternehmen ausgeführt werden soll. Dadurch können Sie den Verwaltungsaufwand reduzieren, der durch das Nachverfolgen mehrerer App-Kopien entsteht, die Sie erworben haben.  

 System Center Configuration Manager unterstützt Sie nun bei der Bereitstellung und Verwaltung von iOS-Apps, die über das Programm erworben wurden, indem die Lizenzinformationen aus dem App Store importiert werden, und die Anzahl der Lizenzen, die verwendet werden, nachverfolgt wird.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Verwalten von Apps für iOS-Geräte, die über ein Volumenprogramm erworben wurden  
 Sie erwerben mehrere Lizenzen für iOS-Apps über das Programm „Volume Purchase Program“ (VPP) von Apple. Dies umfasst das Einrichten eines Apple VPP-Kontos auf der Apple-Website, und das Hochladen des Apple VPP-Tokens zu Configuration Manager. Dadurch haben Sie folgende Möglichkeiten:  

-   Sie können Ihre Volume Purchase-Informationen mit Configuration Manager synchronisieren. 
 
- Sie können Apps aus Apple Volume Purchase Program für Unternehmen und Apple Volume Purchase Program für Bildungseinrichtungen synchronisieren.

- Sie können mehrere Apple VPP-Tokens Configuration Manager zuordnen.

-   Erworbene Apps werden in der Configuration Manager-Konsole angezeigt.  

-   Sie können diese Apps bereitstellen und überwachen, und die Anzahl von Lizenzen für die verwendeten Apps nachverfolgen.  

-   Configuration Manager kann Sie dabei unterstützen, bei Bedarf Lizenzen durch Deinstallieren von Apps freizugeben, die per Volumenlizenz erworben bereitgestellt wurden.  

## <a name="before-you-start"></a>Vorbereitung  
 Bevor Sie beginnen, müssen Sie ein VPP-Token von Apple abrufen und es in Configuration Manager hochladen.  

-   Wenn Sie zuvor ein VPP-Token für ein anderes Produkt für die Verwaltung mobiler Geräte in Ihrem vorhandenen Apple VPP-Konto verwendet haben, müssen Sie für die Verwendung mit Configuration Manager ein neues erstellen.  
-   Jedes Token ist ein Jahr lang gültig.  
-   Standardmäßig wird Configuration Manager zweimal am Tag mit dem Apple VPP-Dienst synchronisiert, um sicherzustellen, dass Ihre Lizenzen mit Configuration Manager synchronisiert sind.  
      Dabei werden nur Änderungen an Ihren Lizenzen synchronisiert. Allerdings wird einmal pro Woche eine vollständige Synchronisierung ausgeführt.  
      Wenn Sie bei **Synchronisierung** auswählen, dass eine manuelle Synchronisierung ausgeführt werden soll, wird immer eine vollständige Synchronisierung ausgeführt.  
-   Wenn Sie eine Configuration Manager-Datenbank wiederherstellen müssen, sollten Sie im Anschluss daran eine manuelle Synchronisierung ausführen, um sicherzustellen, dass die synchronisierten Lizenzdaten auf dem aktuellen Stand sind.  
-   Darüber hinaus müssen Sie ein gültiges APNs-Zertifikat (Apple Push Notification Service) von Apple importieren, damit Sie iOS-Geräte verwalten und Apps bereitstellen können. Weitere Informationen finden Sie unter [Set up iOS hybrid device management (Einrichten der hybriden Verwaltung von iOS-Geräten)](enroll-hybrid-ios-mac.md).  
-   Configuration Manager unterstützt bis zu 3.000 VPP-Token.

Ab System Center Configuration Manager 1702 können Sie lizenzierte Apps für Geräte und Benutzer bereitstellen. Je nachdem, inwieweit die App Gerätelizenzierungen unterstützt, wird eine entsprechende Lizenz wie folgt beansprucht:

|||||
|-|-|-|-|
|Configuration Manager-Version|Unterstützt die App Gerätelizenzierung?|Typ der Bereitstellungssammlung|Beanspruchte Lizenz|
|Früher als 1702|Ja|Benutzer|Benutzerlizenz|
|Früher als 1702|Nein|Benutzer|Benutzerlizenz|
|Früher als 1702|Ja|Gerät|Benutzerlizenz|
|Früher als 1702|Nein|Gerät|Benutzerlizenz|
|1702 und höher|Ja|Benutzer|Benutzerlizenz|
|1702 und höher|Nein|Benutzer|Benutzerlizenz|
|1702 und höher|Ja|Gerät|Gerätelizenz|
|1702 und höher|Nein|Gerät|Benutzerlizenz|

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Schritt 1: Abrufen und Hochladen eines Apple VPP-Tokens  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Cloud Services** > **Apple Volume Purchase Program Tokens** (Apple Volume Purchase Program-Token) aus.   

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Apple Volume Purchase Program Tokens** (Apple Volume Purchase Program-Token) **Add Apple Volume Purchase Program Token** (Apple Volume Purchase Program-Token hinzufügen) aus.  

4.  Konfigurieren Sie auf der Seite **Allgemein** des **Assistenten zum Hinzufügen von Apple Volume Purchase Program-Token** folgende Optionen:   

    -   **Name**: Geben Sie einen Namen für dieses Token ein, der dann in der Configuration Manager-Konsole angezeigt wird.  

    -   **Token**: Klicken Sie auf **Durchsuchen**, und wählen Sie das VPP-Token aus, das Sie von der Apple-Website heruntergeladen haben.  

         Klicken Sie auf den Link **See Apple VPP account** (Siehe Apple VPP-Konto). Wenn Sie sich nicht bereits für das Volume Purchase Program für Unternehmen oder Bildungseinrichtungen registriert haben, registrieren Sie sich jetzt. Sobald Sie registriert sind, laden Sie das Apple VPP-Token für Ihr Konto herunter.  

    -   **Beschreibung**: Wenn Sie möchten, können Sie eine Beschreibung eingeben, anhand derer Sie dieses VPP-Token in der Configuration Manager-Konsole erkennen können.  

    -   **Zur Verbesserung der Suche und Filterung zugewiesene Kategorien**: Optional können Sie dem VPP-Token Kategorien zuweisen, um die Suche in der Configuration Manager-Konsole zu erleichtern.  
    -   **Apple ID**: Geben Sie die E-Mail-ID von Apple ein, die dem VPP-Token zugeordnet ist.
    -   **Tokentyp**: Wählen Sie den Typ des VPP-Tokens aus, den Sie verwenden möchten. Sie können zwischen den Tokentypen **Business** und **EDU** wählen.

5.  Wählen Sie **Weiter** aus, und schließen Sie den Assistenten ab.  

Über den Knoten **Apple Volume Purchase Program Tokens** (Apple Volume Purchase Program-Token) werden nun Informationen zum Apple VPP-Token angezeigt, einschließlich der letzten Aktualisierung, des Ablaufdatums und der letzten Synchronisierung.

Die von Apple gespeicherten Daten können jederzeit mit Configuration Manager vollständig synchronisiert werden. Wählen Sie hierzu auf der Registerkarte **Startseite** in der Gruppe **Synchronisieren** **Synchronisieren** aus.  

## <a name="step-2---deploy-a-volume-purchased-app"></a>Schritt 2: Bereitstellen einer im Rahmen des Volumenprogramms erworbenen App  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **License Information for Store Apps** (Lizenzinformationen für Store-Apps) aus.  

3.  Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.
Die Configuration Manager-Anwendung, die erstellt wird, enthält die App „Windows Store für Unternehmen“. Sie können diese Anwendung wie jede andere Configuration Manager-Anwendung bereitstellen und überwachen.

    > [!IMPORTANT]  
    > Wählen Sie als Bereitstellungszweck **Erforderlich** aus. Verfügbare Installationen werden derzeit nicht unterstützt.

 Wenn Sie die App bereitstellen, wird eine Lizenz je Benutzer verwendet, bei einer gerätebasierten Installation eine Lizenz je Gerät.  Wenn eine Gerätesammlung das Ziel einer App ist, die Gerätelizenzierung unterstützt, wird eine Gerätelizenz beansprucht.  Wenn eine Gerätesammlung das Ziel einer App ist, die Gerätelizenzierung nicht unterstützt, wird eine Benutzerlizenz beansprucht. 

 Wenn Sie eine App im Knoten **Lizenzinformationen für Store-Apps** erstellen, wird die App den Lizenzen des Tokens der von Ihnen ausgewählten App zugeordnet.  Es besteht z.B die Möglichkeit, dass Sie im Knoten zwei Versionen der gleichen App sehen. Dies liegt daran, dass jede Version der App einem anderen Apple VPP-Token zugeordnet ist.  Anschließend könnten Sie Apps von jedem Token erstellen und diese einzeln bereitstellen.

 Um eine Lizenz freizugeben, müssen Sie eine neue Bereitstellung für die App mit der Bereitstellungsaktion **Deinstallieren** erstellen. Sie können die Bereitstellungsaktion nicht in der ursprünglichen Bereitstellung ändern. Die Lizenz wird freigegeben, sobald die App deinstalliert ist.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Schritt 3: Überwachen von iOS VPP-Apps  
 Auf dem Knoten **License Information for Store Apps** (Lizenzinformationen für Store-Apps) im Arbeitsbereich **Softwarebibliothek** werden Informationen über per Volumenlizenz erworbene iOS-Apps angezeigt. Diese Informationen enthalten auch die Gesamtzahl der Lizenzen, die Sie für jede App besitzen, sowie die Anzahl, die bereitgestellt wurde. Zusätzlich wird angezeigt, welchem VPP-Token die App zugeordnet ist und welchen Typ sie aufweist.

 Zudem können Sie auch die Lizenzverwendung für alle von Ihnen erworbenen VPP-Apps mithilfe des Berichts **Apple Volume Purchase Program apps for iOS with license counts** (Apple Volume Purchase Program-Apps für iOS mit Lizenzanzahl) überwachen.  

 In diesem Bericht wird der Name jeder Anwendung zusammen mit der Gesamtzahl der erworbenen Lizenzen, der Anzahl der verfügbaren Lizenzen und weiteren Informationen angezeigt.  

 Informationen zum Ausführen von Configuration Manager-Berichten finden Sie unter [Reporting in System Center Configuration Manager (Berichterstellung in System Center Configuration Manager)](../../core/servers/manage/reporting.md).  
