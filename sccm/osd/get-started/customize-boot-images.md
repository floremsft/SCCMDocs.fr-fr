---
title: "Anpassen von Startimages – Configuration Manager | Microsoft-Dokumentation"
description: "Hier lernen Sie mehrere Möglichkeiten kennen, Configuration Manager oder das Befehlszeilenwerkzeug der Imageverwaltung für die Bereitstellung (Deployment Image Servicing and Management, DISM) zu verwenden, um ein Startimage anzupassen."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: ab2ecb64c9c80b4effed79ba08769c99473db0c4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="customize-boot-images-with-system-center-configuration-manager"></a>Anpassen von Startimages mit System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Jede Version von Configuration Manager unterstützt eine bestimmte Version von Windows Assessment and Deployment Kit (Windows ADK). Sie können Startimages aus der Configuration Manager-Konsole bedienen oder anpassen, wenn diese auf einer Windows PE-Version aus der unterstützten Version von Windows ADK basieren. Andere Startabbilder müssen Sie mithilfe eines anderen Verfahrens anpassen, beispielsweise mit dem Befehlszeilenprogramm Deployment Image Servicing and Management (DISM), das Bestandteil von Windows AIK und Windows ADK ist.  

 Im Folgenden finden Sie die jeweils unterstützte Version von Windows ADK, die Windows PE-Version, auf der das Startimage basiert, das über die Configuration Manager-Konsole angepasst werden kann, und die Windows PE-Versionen, auf denen das Startimage basiert, das Sie mithilfe von DISM anpassen und anschließend zu Configuration Manager hinzufügen können.  

-   **Windows ADK-Version**  

     Windows ADK für Windows 10  

-   **Windows PE-Versionen für Startimages, die über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 10  

-   **Unterstützte Windows PE-Versionen für Startimages, die nicht über die Configuration Manager-Konsole angepasst werden können**  

     Windows PE 3.1<sup>1</sup> und Windows PE 5  

     <sup>1</sup> Sie können zu Configuration Manager nur dann ein Startimage hinzufügen, wenn es auf Windows PE 3.1 basiert. Installieren Sie die Ergänzung zu Windows AIK für Windows 7 SP1, um ein Upgrade von Windows AIK für Windows 7 (basierend auf Windows PE 3) mit der Ergänzung zu Windows AIK für Windows 7 SP1 (basierend auf Windows PE 3.1) durchzuführen. Sie können die Ergänzung zu Windows AIK für Windows 7 SP1 aus dem [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=5188)herunterladen.  

     Im Fall von Configuration Manager etwa können Sie Startimages aus Windows ADK für Windows 10 (das auf Windows PE 10 basiert) über die Configuration Manager-Konsole anpassen. Zwar werden auf Windows PE 5 basierende Startabbilder unterstützt, doch müssen Sie sie von einem anderen Computer aus anpassen und die mit dem Windows ADK für Windows 8 installierte DISM-Version verwenden. Danach können Sie das Startimage zur Configuration Manager-Konsole hinzufügen.  

 Mit den unter diesem Thema beschriebenen Verfahren wird gezeigt, wie die optionalen, für Configuration Manager erforderlichen Komponenten mithilfe der folgenden Windows PE-Pakete zum Startimage hinzugefügt werden:  

-   **WinPE-WMI**: Hiermit wird die Unterstützung für die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) hinzugefügt.  

-   **WinPE-Scripting**: Hiermit wird die Unterstützung für Windows Script Host (WSH) hinzugefügt.  

-   **WinPE-WDS-Tools**: Hiermit werden die Windows-Bereitstellungsdienste installiert.  

 Es gibt noch weitere Windows PE-Pakete, die Sie hinzufügen können. Die folgenden Ressourcen bieten weitere Informationen zu optionalen Komponenten, die Sie dem Startabbild hinzufügen können.  

-   Zu Windows PE 5 finden Sie Informationen im Thema [WinPE: Hinzufügen von Paketen (Referenz zu optionalen Komponenten)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)  

-   Zu Windows PE 3.1 finden Sie Informationen im Thema [Add a Package to a Windows PE Image (Hinzufügen eines Pakets zu einem Windows PE-Abbild)](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) in der Windows 7-TechNet-Dokumentationsbibliothek.  

> [!NOTE]
>Wenn Sie von einem benutzerdefinierten Startimage mit von Ihnen hinzugefügten Tools aus in WinPE starten, können Sie eine Eingabeaufforderung von WinPE aus öffnen und den Dateinamen eines Tools eingeben, um es auszuführen. Der Speicherort dieser Tools wird automatisch der Pfadvariable hinzugefügt. Die Befehlszeile kann nur hinzugefügt werden, wenn die Einstellung **Befehlsunterstützung aktivieren (nur Test)** auf der Registerkarte **Anpassung** der Startimageeigenschaften aktiviert wird.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Anpassen eines Startimages, das Windows PE 5 verwendet  
 Um ein Startabbild anzupassen, das Windows PE 5 verwendet, müssen Sie das Windows ADK installieren und dann mithilfe des Befehlszeilenprogramms DISM das Startabbild bereitstellen, zusätzliche Komponenten und Treiber hinzufügen und die Änderungen im Startabbild ausführen. Gehen Sie wie folgt vor, um das Startabbild anzupassen.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>So passen Sie ein Startabbild an, das Windows PE 5 verwendet  

1.  Installieren Sie das Windows ADK auf einem Computer, auf dem keine andere Windows AIK- oder Windows ADK-Version installiert ist und auf dem keine Configuration Manager-Komponenten installiert sind.  

2.  Laden Sie das Windows ADK für Windows 8.1 aus dem [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=39982)herunter.  

3.  Kopieren Sie das Startimage (wimpe.wim) aus dem Windows ADK-Installationsordner (z.B. „<*Installationspfad*>\Windows Kits\\<Version*>\Assessment and Deployment Kit\Windows Preinstallation Environment*\\<*x86 oder amd64*>\\<*Gebietsschema*>“) in einen Zielordner auf dem Computer, von dem aus Sie das Startimage anpassen. In dieser Vorgehensweise wird C:\WinPEWAIK als Zielordnername verwendet.  

4.  Stellen Sie das Startabbild mithilfe von DISM in einem lokalen Windows PE-Ordner bereit. Geben Sie beispielsweise folgende Befehlszeile ein:  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     Hierbei ist C:\WinPEWAIK der Ordner, in dem das Startabbild enthalten ist, und C:\WinPEMount der bereitgestellte Ordner.  

    > [!NOTE]
    >  Weitere Informationen zu DISM finden Sie im Thema [DISM - Deployment Image Servicing and Management Technical Reference (Technische Referenz zur Abbildverwaltung für die Bereitstellung - DISM)](http://technet.microsoft.com/library/hh824821.aspx) in der Windows 8.1- und Windows 8-TechNet-Dokumentationsbibliothek.

5.  Nach dem Bereitstellen des Startabbilds fügen Sie diesem mit DISM optionale Komponenten hinzu. In Windows PE 5 befinden sich die optionalen 64-Bit-Komponenten im Verzeichnis „<*Installationspfad*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs“.  

    > [!NOTE]
    >  Bei diesem Verfahren wird der folgende Speicherort für die optionalen Komponenten verwendet: C:\Programme (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs. Je nach Windows ADK-Version und dafür ausgewählten Optionen kann sich der Pfad bei Ihnen unterscheiden.  

     Geben Sie Folgendes ein, um die optionalen Komponenten zu installieren:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<Gebietsschema\>* **\WinPE-SecureStartup_** *<Gebietsschema\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<Gebietsschema\>* **\WinPE-WMI_** *<Gebietsschema\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<Gebietsschema\>* **\WinPE-Scripting** *<Gebietsschema\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<Gebietsschema\>* **\WinPE-WDS-Tools_** *<Gebietsschema\>* **.cab"**  

     "C:\WinPEMount" ist der bereitgestellte Ordner und "locale" ist das Gebietsschema für die Komponenten. Für das Gebietsschema **en-us** geben Sie z. B. Folgendes ein:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

    > [!TIP]
    >  Weitere Informationen zu den optionalen Komponenten, die Sie dem Startabbild hinzufügen können, finden Sie im Thema [Windows PE Optional Components Reference (Referenz zu optionalen Komponenten in Windows PE)](http://technet.microsoft.com/library/hh824926.aspx) in der Windows 8.1- und Windows 8-TechNet-Dokumentationsbibliothek.  

6.  Fügen Sie mithilfe von DISM erforderlichenfalls bestimmte Treiber zum Startabbild hinzu. Geben Sie Folgendes ein, um Treiber zum Startabbild hinzuzufügen:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *path to driver .inf file* **>**  

     Hierbei ist C:\WinPEMount der bereitgestellte Ordner.  

7.  Geben Sie Folgendes ein, um die Bereitstellung der Startabbilddatei aufzuheben und die Änderungen auszuführen.  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     Hierbei ist C:\WinPEMount der bereitgestellte Ordner.  

8.  Fügen Sie das aktualisierte Startimage zu Configuration Manager hinzu, um es zur Verwendung in Ihren Tasksequenzen verfügbar zu machen. Gehen Sie wie folgt vor, um das aktualisierte Startabbild zu importieren:  

    1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

    2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

    3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Startabbild hinzufügen** , um den Assistenten zum Hinzufügen von Startabbildern zu starten.  

    4.  Geben Sie auf der Seite **Datenquelle** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

        -   Geben Sie im Feld **Pfad** den Pfad der aktualisierten Startabbilddatei an. Der angegebene Pfad muss ein gültiger Netzwerkpfad im UNC-Format sein. Beispiel: **\\\\<***Servername***>\\<***WinPEWAIK-Freigabe***>\winpe.wim**.  

        -   Wählen Sie das Startabbild in der Dropdownliste **Startabbild** aus. Wenn die WIM-Datei mehrere Startabbilder enthält, werden sämtliche Abbilder aufgeführt.  

    5.  Geben Sie auf der Seite **Allgemein** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

        -   Geben Sie im Feld **Name** einen eindeutigen Namen für das Startabbild an.  

        -   Geben Sie im Feld **Version** eine Versionsnummer für das Startabbild an.  

        -   Geben Sie im Feld **Kommentar** anhand einer kurzen Beschreibung an, wie das Startabbild verwendet werden soll.  

    6.  Schließen Sie den Assistenten ab.  

9. Sie können im Startabbild eine Befehlsshell aktivieren, um es in Windows PE zu debuggen und Probleme zu behandeln. Gehen Sie wie folgt vor, um die Befehlsshell zu aktivieren.  

    1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

    2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

    3.  Suchen Sie in der Liste nach dem neuen Startabbild, und ermitteln Sie die Paket-ID des Abbilds. Sie finden die Paket-ID in der Spalte **Abbild-ID** für das Startabbild.  

    4.  Geben Sie an der Eingabeaufforderung den Befehl **wbemtest** ein, um das Testprogramm für die Windows-Verwaltungsinstrumentation zu öffnen.  

    5.  Geben Sie **\\\\<***SMS-Anbietercomputer***>\root\sms\site_<***Standortcode***>** in **Namespace**ein, und klicken Sie auf **Verbinden**.  

    6.  Klicken Sie auf **Instanz öffnen**, geben Sie **sms_bootimagepackage.packageID="<Paket-ID\>"** ein, und klicken Sie auf **OK**. Geben Sie als Paket-ID den in Schritt 3 ermittelten Wert ein.  

    7.  Klicken Sie auf **Objekt aktualisieren**und dann im Bereich **Eigenschaften** auf **EnableLabShell** .  

    8.  Klicken Sie auf **Eigenschaft bearbeiten**, ändern Sie den Wert auf **TRUE**, und klicken Sie auf **Eigenschaft speichern**.  

    9. Klicken Sie auf **Objekt speichern**, und beenden Sie dann das Testprogramm für Windows-Verwaltungsinstrumentation.  

10. Sie müssen das Startabbild an Verteilungspunkte, Verteilungspunktgruppen oder mit Verteilungspunktgruppen verknüpften Sammlungen verteilen, um es in einer Tasksequenz verwenden zu können. Gehen Sie wie folgt vor, um das Startabbild zu verteilen.  

    1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

    2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

    3.  Klicken Sie auf das in Schritt 3 angegebene Startabbild.  

    4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Verteilungspunkte aktualisieren**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Passen Sie ein Startabbild an, das Windows PE 3.1 verwendet.  
 Zum Anpassen eines Startabbilds, das Windows PE 3.1 verwendet, müssen Sie nacheinander Windows AIK und die Ergänzung zu Windows AIK für Windows 7 SP1 installieren und dann mithilfe des Befehlszeilenprogramms DISM das Startabbild bereitstellen, zusätzliche Komponenten und Treiber hinzufügen und die Änderungen im Startabbild ausführen. Gehen Sie wie folgt vor, um das Startabbild anzupassen.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>So passen Sie ein Startabbild an, das Windows PE 3.1 verwendet  

1.  Installieren Sie das Windows A|K auf einem Computer, auf dem keine andere Windows AIK- oder Windows ADK-Version installiert ist und auf dem keine Configuration Manager-Komponenten installiert sind. Laden Sie Windows AIK im [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=5753)herunter.  

2.  Installieren Sie die Ergänzung zu Windows AIK für Windows 7 mit SP1 auf dem Computer aus Schritt 1. Laden Sie die Ergänzung zu Windows AIK für Windows 7 SP1 aus dem [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=5188)herunter.  

3.  Kopieren Sie das Startimage (wimpe.wim) aus dem Windows AIK-Installationsordner (z.B. „<*Installationspfad*>\Windows AIK\Tools\PETools\amd64\\“) in einen Ordner auf dem Computer, von dem aus Sie das Startimage anpassen. In dieser Vorgehensweise wird C:\WinPEWAIK als Ordnername verwendet.  

4.  Stellen Sie das Startabbild mithilfe von DISM in einem lokalen Windows PE-Ordner bereit. Geben Sie beispielsweise folgende Befehlszeile ein:  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     Hierbei ist C:\WinPEWAIK der Ordner, in dem das Startabbild enthalten ist, und C:\WinPEMount der bereitgestellte Ordner.  

    > [!NOTE]
    >  Weitere Informationen zu DISM finden Sie im Thema [Technische Referenz zur Imageverwaltung für die Bereitstellung](http://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx) in der TechNet-Dokumentationsbibliothek für Windows 7.  

5.  Nach dem Bereitstellen des Startabbilds fügen Sie diesem mit DISM optionale Komponenten hinzu. In Windows PE 3.1 beispielsweise befinden sich die optionalen Komponenten im Verzeichnis „<*Installationspfad*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\“.  

    > [!NOTE]
    >  Bei diesem Verfahren wird der folgende Speicherort für die optionalen Komponenten verwendet: C:\Programme\Windows AIK\Tools\PETools\amd64\WinPE_FPs. Je nach Windows AIK-Version und dafür ausgewählten Optionen kann sich der Pfad bei Ihnen unterscheiden.  

     Geben Sie Folgendes ein, um die optionalen Komponenten zu installieren:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<Gebietsschema\>* **\winpe-wmi_** *<Gebietsschema\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<Gebietsschema\>* **\winpe-scripting_** *<Gebietsschema\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<Gebietsschema\>* **\winpe-wds-tools_** *<Gebietsschema\>* **.cab"**  

     "C:\WinPEMount" ist der bereitgestellte Ordner und "locale" ist das Gebietsschema für die Komponenten. Für das Gebietsschema **en-us** geben Sie z. B. Folgendes ein:  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

    > [!TIP]
    >  Weitere Informationen zu den verschiedenen Paketen, die Sie dem Startimage hinzufügen können, finden Sie im Thema [Hinzufügen eines Pakets zu einem Windows PE-Image](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) in der TechNet-Dokumentationsbibliothek für Windows 7.  

6.  Fügen Sie mithilfe von DISM erforderlichenfalls bestimmte Treiber zum Startabbild hinzu. Geben Sie Folgendes ein, um Treiber zum Startabbild hinzuzufügen:  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *path to driver .inf file* **>**  

     Hierbei ist C:\WinPEMount der bereitgestellte Ordner.  

7.  Geben Sie Folgendes ein, um die Bereitstellung der Startabbilddatei aufzuheben und die Änderungen auszuführen.  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     Hierbei ist C:\WinPEMount der bereitgestellte Ordner.  

8.  Fügen Sie das aktualisierte Startimage zu Configuration Manager hinzu, um es zur Verwendung in Ihren Tasksequenzen verfügbar zu machen. Gehen Sie wie folgt vor, um das aktualisierte Startabbild zu importieren:  

    1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

    2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

    3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Startabbild hinzufügen** , um den Assistenten zum Hinzufügen von Startabbildern zu starten.  

    4.  Geben Sie auf der Seite **Datenquelle** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

        -   Geben Sie im Feld **Pfad** den Pfad der aktualisierten Startabbilddatei an. Der angegebene Pfad muss ein gültiger Netzwerkpfad im UNC-Format sein. Beispiel: **\\\\<***Servername***>\\<***WinPEWAIK-Freigabe***>\winpe.wim**.  

        -   Wählen Sie das Startabbild in der Dropdownliste **Startabbild** aus. Wenn die WIM-Datei mehrere Startabbilder enthält, werden sämtliche Abbilder aufgeführt.  

    5.  Geben Sie auf der Seite **Allgemein** die folgenden Optionen an, und klicken Sie dann auf **Weiter**.  

        -   Geben Sie im Feld **Name** einen eindeutigen Namen für das Startabbild an.  

        -   Geben Sie im Feld **Version** eine Versionsnummer für das Startabbild an.  

        -   Geben Sie im Feld **Kommentar** anhand einer kurzen Beschreibung an, wie das Startabbild verwendet werden soll.  

    6.  Schließen Sie den Assistenten ab.  

9. Sie können im Startabbild eine Befehlsshell aktivieren, um es in Windows PE zu debuggen und Probleme zu behandeln. Gehen Sie wie folgt vor, um die Befehlsshell zu aktivieren.  

    1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

    2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

    3.  Suchen Sie in der Liste nach dem neuen Startabbild, und ermitteln Sie die Paket-ID des Abbilds. Sie finden die Paket-ID in der Spalte **Abbild-ID** für das Startabbild.  

    4.  Geben Sie an der Eingabeaufforderung den Befehl **wbemtest** ein, um das Testprogramm für die Windows-Verwaltungsinstrumentation zu öffnen.  

    5.  Geben Sie **\\\\<***SMS-Anbietercomputer***>\root\sms\site_<***Standortcode***>** in **Namespace**ein, und klicken Sie auf **Verbinden**.  

    6.  Klicken Sie auf **Instanz öffnen**, geben Sie **sms_bootimagepackage.packageID="<Paket-ID\>"** ein, und klicken Sie auf **OK**. Geben Sie als Paket-ID den in Schritt 3 ermittelten Wert ein.  

    7.  Klicken Sie auf **Objekt aktualisieren**und dann im Bereich **Eigenschaften** auf **EnableLabShell** .  

    8.  Klicken Sie auf **Eigenschaft bearbeiten**, ändern Sie den Wert auf **TRUE**, und klicken Sie auf **Eigenschaft speichern**.  

    9. Klicken Sie auf **Objekt speichern**, und beenden Sie dann das Testprogramm für Windows-Verwaltungsinstrumentation.  

10. Sie müssen das Startabbild an Verteilungspunkte, Verteilungspunktgruppen oder mit Verteilungspunktgruppen verknüpften Sammlungen verteilen, um es in einer Tasksequenz verwenden zu können. Gehen Sie wie folgt vor, um das Startabbild zu verteilen.  

    1.  Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.  

    2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und klicken Sie dann auf **Startabbilder**.  

    3.  Klicken Sie auf das in Schritt 3 angegebene Startabbild.  

    4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Verteilungspunkte aktualisieren**.  
