---
title: Erstellen von Abfragen | Microsoft-Dokumentation
description: "Erfahren Sie, wie Sie in System Center Configuration Manager Abfragen erstellen und importieren. Enthält Beispiele für Abfragen und Tipps."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9f38d86ff6227bb6ea88c358a3d61242372d449e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Erstellen von Abfragen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Sie können dieses Thema verwenden, um in System Center Configuration Manager Abfragen zu erstellen oder zu importieren.  

##  <a name="BKMK_Create"></a> Erstellen von Abfragen  
 Mit diesem Verfahren können Sie Abfragen in Configuration Manager erstellen.  

#### <a name="to-create-a-query"></a>So erstellen Sie eine Abfrage  

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Überwachung** aus.  

2.  Wählen Sie im Arbeitsbereich **Überwachung** die Option **Abfragen** aus. Wählen Sie dann auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Abfrage erstellen** aus.  

3.  Geben Sie auf der Registerkarte **Allgemein** im **Abfrageerstellungs-Assistenten**einen eindeutigen Namen und optional einen Kommentar für die Abfrage an.  

4.  Wenn Sie eine vorhandene Abfrage als Grundlage für die neue Abfrage importieren möchten, wählen Sie **Abfrageanweisung importieren** aus. Wählen Sie im Dialogfeld **Abfrage durchsuchen** eine vorhandene Abfrage aus, die Sie importieren möchten, und wählen Sie dann **OK** aus.  

5.  Wählen Sie den Objekttyp, den die Abfrage zurückgeben soll, aus der Liste **Objekttyp** aus. In der folgenden Tabelle sind einige Beispiele für Objekttypen aufgeführt, nach denen Sie suchen können:  

    |Objekttyp|Beschreibung|  
    |-----------------|-----------------|  
    |**Systemressource**|Ermöglicht die Suche nach typischen Systemattributen wie NetBIOS-Name von Geräten, Clientversion, IP-Adresse des Clients und Active Directory-Domänendienstinformationen.|  
    |**Benutzerressource**|Ermöglicht die Suche nach typischen Benutzerinformationen wie Benutzernamen, Benutzergruppennamen und Sicherheitsgruppennamen.|  
    |**Bereitstellung**|Ermöglicht die Suche nach typischen Attributen einer Bereitstellung wie Bereitstellungsname, Zeitplan sowie Sammlung, der die Bereitstellung zugewiesen wurde.|  

6.  Wählen Sie **Abfrageanweisung bearbeiten** aus, um das Dialogfeld *Eigenschaften der &lt;Abfragename\>***-Anweisung** zu öffnen.  

7.  Geben Sie auf der Registerkarte **Allgemein** im Dialogfeld *Eigenschaften der &lt;Abfragename\>***-Anweisung** die Attribute, die von dieser Abfrage zurückgegeben werden, sowie die Anzeigeart an. Wählen Sie das Symbol **Neu** aus, um ein neues Attribut hinzuzufügen. Sie können auch **Abfragesprache anzeigen** auswählen, um die Abfrage direkt in der WMI-Abfragesprache (WMI Query Language, WQL) einzugeben oder zu ändern. Beispiele für WMI-Abfragen finden Sie im Abschnitt [Example WQL queries](#BKMK_Example) in diesem Thema.  

    > [!TIP]  
    > Die folgende MSDN-Referenzdokumentation enthält Informationen zum Erstellen eigener WQL-Abfragen:  
    >   
    > -   [WQL (SQL für WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [WHERE-Klausel](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [WQL-Operatoren](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Geben Sie auf der Registerkarte **Kriterien** im Dialogfeld *Eigenschaften der &lt;Abfragename\>***-Anweisung** Kriterien zum Optimieren der Abfrageergebnisse an. Sie könnten beispielsweise nur Ressourcen mit dem Standortcode **XYZ** in den Abfrageergebnissen zurückgeben lassen. Sie können mehrere Kriterien für eine Abfrage konfigurieren.  

    > [!IMPORTANT]  
    > Wenn Sie eine Abfrage ohne Kriterien erstellen, gibt diese alle Geräte in der Sammlung **Alle Systeme** aus.  

9. Auf der Registerkarte **Verknüpfungen** im Dialogfeld *Eigenschaften der &lt;Abfragename\>***-Anweisung** können Sie Daten aus zwei verschiedenen Attributen in Ihren Abfrageergebnissen kombinieren. Von Configuration Manager werden zwar automatisch Abfrageverknüpfungen erstellt, wenn verschiedene Attribute für die Abfrageergebnisse ausgewählt werden, doch die Registerkarte **Verknüpfungen** bietet erweiterte Optionen. Die folgende Tabelle enthält die Attributklassen, die von System Center 2012 Configuration Manager unterstützt werden:  

    |Verknüpfungstyp|Beschreibung|  
    |---------------|-----------------|  
    |Innerhalb|Zeigt nur übereinstimmende Ergebnisse an und wird immer von automatisch erstellten Verknüpfungen verwendet.|  
    |Links|Zeigt alle Ergebnisse für das Basisattribut und nur die übereinstimmenden Ergebnisse für das Verknüpfungsattribut an.|  
    |Rechts|Zeigt alle Ergebnisse für das Verknüpfungsattribut und lediglich die übereinstimmenden Ergebnisse für das Basisattribut an.|  
    |Vollständig|Zeigt alle Ergebnisse für das Basisattribut und für das Verknüpfungsattribut an.|  

     Weitere Informationen zum Verwenden von Verknüpfungsoperationen finden Sie in der SQL Server-Dokumentation.  

10. Wählen Sie **OK** aus, um das Dialogfeld *Eigenschaften der &lt;Abfragename\>***-Anweisung** zu schließen.  

11. Geben Sie auf der Registerkarte **Allgemein** des **Abfrageerstellungs-Assistenten** an, ob die Ergebnisse der Abfrage auf die Mitglieder einer Sammlung bzw. auf die Mitglieder einer angegebenen Sammlung begrenzt werden sollen oder ob bei jeder Ausführung der Abfrage nach einer Sammlung gefragt werden soll.  

12. Schließen Sie den Abfrageerstellungs-Assistenten ab. Die neue Abfrage wird im Knoten **Abfragen** des Arbeitsbereichs **Überwachung** angezeigt.  

##  <a name="BKMK_Import"></a> Importieren von Abfragen  
 Verwenden Sie dieses Verfahren, um eine Abfrage in Configuration Manager zu importieren. Informationen zum Exportieren von Abfragen finden Sie unter [Verwalten von Abfragen in Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### <a name="to-import-a-query"></a>So importieren Sie eine Abfrage  

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Überwachung** aus.  

2.  Wählen Sie im Arbeitsbereich **Überwachung** die Option **Abfragen** aus. Wählen Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Objekte importieren** aus.  

3.  Wählen Sie auf der Seite **MOF-Dateiname** des **Assistenten zum Importieren von Objekten** die Option **Durchsuchen** aus, um die MOF-Datei (Managed Object Format) mit der zu importierenden Abfrage auszuwählen.  

4.  Überprüfen Sie die Informationen zur Abfrage, die importiert werden soll, und schließen Sie den Assistenten ab. Die neue Abfrage wird im Knoten **Abfragen** des Arbeitsbereichs **Überwachung** angezeigt.  

##  <a name="BKMK_Example"></a> Example WQL queries

Dieser Abschnitt enthält Beispiele für WMI-Abfragen, die Sie in Ihrer Hierarchie verwenden oder für andere Zwecke ändern können. Um diese Abfragen zu verwenden, wählen Sie im Dialogfeld **Eigenschaften der Abfrageanweisung** die Option **Abfragesprache anzeigen**. Kopieren Sie anschließend die Abfrage in das Feld **Abfrageanweisung**.  

> [!TIP]  
> Verwenden Sie das Platzhalterzeichen `%`, um eine beliebige Zeichenfolge anzugeben. `%Visio%` gibt beispielsweise „Microsoft Office Visio 2010“ zurück.  

### <a name="computers-that-run-windows-7"></a>Computer, auf denen Windows 7 ausgeführt wird

Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und die Betriebssystemversion aller Computer mit Windows 7 zurückgegeben.  

> [!TIP]  
> Um Computer zurückzugeben, auf denen Windows Server 2008 R2 ausgeführt wird, ändern Sie `%Workstation 6.1%` in `%Server 6.1%`.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computer, auf denen ein bestimmtes Softwarepaket installiert ist  

Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und den Softwarepaketnamen aller Computer zurückzugeben, auf denen ein bestimmtes Softwarepaket installiert ist. In diesem Beispiel werden alle Computer angezeigt, auf denen eine Version von Microsoft Visio installiert ist. Ersetzen Sie `%Visio%` durch das Softwarepaket, nach dem Sie mit der Abfrage suchen möchten.  

> [!TIP]  
> Diese Abfrage sucht anhand der Namen, die in der Liste der Programme in der Windows-Systemsteuerung angezeigt werden, nach dem Softwarepaket.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit"></a>Computer in einer bestimmten Active Directory Domain Services-Organisationseinheit

Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und den Namen der Organisationseinheit (Organizational Unit, OU) aller Computer in einer bestimmten Organisationseinheit zurückzugeben. Ersetzen Sie den Text `OU Name` durch den Namen der Organisationseinheit, nach der Sie mit der Abfrage suchen möchten.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computer mit einem bestimmten NetBIOS-Namen

Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen aller Computer zurückzugeben, die mit einer bestimmten Zeichenfolge beginnen. In diesem Beispiel gibt die Abfrage alle Computer mit einem NetBIOS-Namen zurück, der mit `ABC` beginnt.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Geräte eines bestimmten Typs

Gerätetypen werden in der Configuration Manager-Datenbank unter der Ressourcenklasse **sms_r_system** und dem Attributnamen **AgentEdition** gespeichert. Verwenden Sie die folgende Abfrage, um nur die Geräte abzurufen, die mit der angegebenen Agent-Edition des Gerätetyps übereinstimmen:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Verwenden Sie einen der folgenden Werte für *&lt;Geräte-ID\>*:  

|Gerätetyp|Wert von „AgentEdition“|  
|-----------------|---------------------------|  
|Windows-Desktop oder -Laptop|0|  
|Windows-ARM-basiertes Gerät (mit Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Macintosh-Computer|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Intel-System auf einem Chip|12|  
|UNIX- und Linux-Server|13|  

 Wenn die Abfrage z. B. nur Macintosh-Computer zurückgeben soll, verwenden Sie die folgende Abfrage:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Weitere Informationen:  
 [Vorgänge und Wartungstasks für Abfragen in System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
