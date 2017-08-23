---
title: Tasksequenz-Aktionsvariablen | Microsoft-Dokumentation
description: "Verwenden Sie Sequenzaktionsvariablen, z.B. Variablen zur Netzwerkeinstellung, um Konfigurationseinstellungen für einen einzelnen Schritt in einer Configuration Manager-Tasksequenz anzugeben."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6049ec2369e0a97b21ce6523ba8448335385ab9a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Tasksequenz-Aktionsvariablen in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit den Tasksequenzaktionsvariablen werden Konfigurationseinstellungen angegeben, die von einem einzelnen Schritt einer System Center Configuration Manager-Tasksequenz verwendet werden. Standardmäßig werden die von einem Tasksequenzschritt verwendeten Einstellungen initialisiert, bevor der Schritt ausgeführt wird. Sie sind nur während der Ausführung des zugehörigen Tasksequenzschritts verfügbar. Mit anderen Worten, die Einstellung der Tasksequenzvariablen wird der Tasksequenzumgebung vor der Ausführung des Tasksequenzschritts hinzufügt, und der Wert wird nach der Ausführung Tasksequenzschritts aus der Tasksequenzumgebung entfernt.  

## <a name="action-variable-example"></a>Beispiel für eine Aktionsvariable  
 Mit dem Tasksequenzschritt **Befehlszeile ausführen** können Sie beispielsweise ein Startverzeichnis für eine Befehlszeilenaktion angeben. Dieser Schritt umfasst die Eigenschaft **Starten in** , deren Standardwert in der Tasksequenzumgebung als Variable **WorkingDirectory** gespeichert wird. Die Umgebungsvariable **WorkingDirectory** wird initialisiert, bevor die Tasksequenzaktion **Befehlszeile ausführen** ausgeführt wird. Während des Schritts **Befehlszeile ausführen** kann über die Eigenschaft **Starten in** auf den Wert **WorkingDirectory** zugegriffen werden. Nach Abschluss des Tasksequenzschritts wird der Wert der Variablen **WorkingDirectory** aus der Tasksequenzumgebung entfernt. Falls die Sequenz einen weiteren Tasksequenzschritt **Befehlszeile ausführen** enthält, wird die neue Variable **WorkingDirectory** initialisiert und auf den Startwert für diese Tasksequenz festgelegt.  

 Der Standardwert für die Einstellung einer Tasksequenzaktion ist beim Ausführen des Tasksequenzschritts vorhanden. Dahingegen kann jeder von Ihnen neu festgelegte Wert von mehreren Schritten in der Sequenz verwendet werden. Wenn Sie eine der Methoden zum Erstellen von Tasksequenzvariablen zum Überschreiben eines integrierten Variablenwerts verwenden, bleibt der neue Wert in der Umgebung erhalten und überschreibt den Standardwert für weitere Schritte in der Tasksequenz. Wenn im vorherigen Beispiel als erster Schritt der Tasksequenz der Schritt **Tasksequenzvariable festlegen** hinzugefügt wird, und dieser die Umgebungsvariable **WorkingDirectory** auf den Wert **C:\\** festlegt, verwenden beide Schritte **Befehlszeile ausführen** in der Tasksequenz den neuen Startverzeichniswert.  

## <a name="action-variables-for-task-sequence-actions"></a>Aktionsvariablen für Tasksequenzaktionen  
 Configuration Manager-Tasksequenzvariablen sind nach der zugehörigen Tasksequenzaktion gruppiert. Weitere Informationen zu den Aktionsvariablen, die einer bestimmten Aktion zugeordnet sind, finden Sie unter den folgenden Links. Über die Tasksequenzvariablen wird die Funktionsweise der Tasksequenzaktion gesteuert. Von der Tasksequenzaktion werden die von Ihnen als Eingabevariablen gekennzeichneten Variablen gelesen und verwendet. Alternativ können Sie die Variablen mithilfe der Aktion „Tasksequenzvariable festlegen“ oder mithilfe des Objekts „TSEnvironment COM“ in der Laufzeit festlegen. Nur von der Tasksequenzaktion werden Variablen als Ausgabevariablen gekennzeichnet, die von später in der Tasksequenz liegenden Aktionen gelesen werden.  

> [!NOTE]  
>  Nicht alle Tasksequenzaktionen sind einem Satz Tasksequenzvariablen zugeordnet. Beispielsweise gibt es zwar Variablen, die der Aktion BitLocker aktivieren zugeordnet sind, aber der Aktion BitLocker deaktivieren sind keine Variablen zugeordnet.  

###  <a name="BKMK_ApplyDataImage"></a> Variablen der Tasksequenzaktion „Datenabbild anwenden“  
 Mit den Variablen für diese Aktion wird angegeben, welches Abbild einer WIM-Datei auf den Zielcomputer angewendet wird und ob die Dateien auf der Zielpartition gelöscht werden sollen. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Apply Data Image Task Sequence Step (Tasksequenzschritt „Datenimage anwenden“)](task-sequence-steps.md#BKMK_ApplyDataImage).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (Eingabe)|Hiermit wird der Indexwert des Abbilds angegeben, das auf den Zielcomputer angewendet wird.|  
|OSDWipeDestinationPartition<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die auf der Zielpartition vorhandenen Dateien gelöscht werden sollen.<br /><br /> Gültige Werte:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**|  

###  <a name="BKMK_ApplyDriverPackage"></a> Variablen der Tasksequenzaktion „Treiberpaket anwenden“  
 Mit den Variablen für diese Aktion werden Informationen zur Installation von Massenspeichertreibern bereitgestellt, und es wird angegeben, ob nicht signierte Treiber installiert werden sollen. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Apply Driver Package (Treiberpaket anwenden)](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (Eingabe)|Hiermit wird die Inhalts-ID des Treibers für Massenspeichergeräte angegeben, der aus dem Treiberpaket installiert werden soll. Wenn dieser Wert nicht angegeben ist, wird kein Massenspeichertreiber installiert.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (Eingabe)|Hiermit wird die INF-Datei des zu installierenden Massenspeichertreibers angegeben.<br /><br /> <br /><br /> Diese Tasksequenzvariable ist erforderlich, wenn ein Wert für OSDApplyDriverBootCriticalContentUniqueID festgelegt ist.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (Eingabe)|Hiermit wird angegeben, ob ein Treiber für Massenspeichergeräte installiert wird (muss **SCSI**sein).<br /><br /> <br /><br /> Diese Tasksequenzvariable ist erforderlich, wenn ein Wert für OSDApplyDriverBootCriticalContentUniqueID festgelegt ist.|  
|OSDApplyDriverBootCriticalID<br /><br /> (Eingabe)|Hiermit wird die für den Start erforderliche ID des Treibers für Massenspeichergeräte angegeben, der installiert werden soll. Diese ID wird im Abschnitt**SCSI**der Gerätetreiberdatei „txtsetup.oem“ aufgeführt.<br /><br /> <br /><br /> Diese Tasksequenzvariable ist erforderlich, wenn ein Wert für OSDApplyDriverBootCriticalContentUniqueID festgelegt ist.|  
|OSDAllowUnsignedDriver<br /><br /> (Eingabe)|Hiermit wird angegeben, ob Windows so konfiguriert werden soll, dass die Installation nicht signierter Gerätetreiber zugelassen wird. Diese Tasksequenzvariable wird bei der Bereitstellung von Windows Vista und späteren Betriebssystemen nicht verwendet.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  

###  <a name="BKMK_ApplyNetworkSettings"></a> Variablen der Tasksequenzaktion „Netzwerkeinstellungen anwenden“  
 Mit den Variablen für diese Aktion werden Netzwerkeinstellungen für den Zielcomputer angegeben, darunter Einstellungen für die Netzwerkkarten des Computers, Domäneneinstellungen und Arbeitsgruppeneinstellungen. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Apply Network Settings Step (Schritt „Netzwerkeinstellungen anwenden“)](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (Eingabe)|Bei dieser Tasksequenzvariablen handelt es sich um die Arrayvariable. Die einzelnen Elemente im Array stellen die Einstellungen für eine einzelne Netzwerkkarte im Computer dar. Die für die jeweilige Karte definierten Einstellungen werden aufgerufen, indem der Name der Arrayvariablen mit dem nullbasierten Netzwerkkartenindex und dem Eigenschaftennamen kombiniert wird.<br /><br /> <br /><br /> Wenn mit dieser Tasksequenzaktion mehrere Netzwerkkarten konfiguriert werden, werden die Eigenschaften für die zweite Netzwerkkarte mithilfe ihres Indexes im Variablennamen definiert; beispielsweise OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList, OSDAdapter1EnableWINS usw.<br /><br /> <br /><br /> Die folgenden Variablennamen können beispielsweise verwendet werden, um die Eigenschaften für die erste Netzwerkkarte zu definieren, die von dieser Tasksequenzaktion konfiguriert wird:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP** – TRUE aktiviert Dynamic Host Configuration Protocol (DHCP) für die Karte.<br />    Diese Einstellung ist erforderlich. Mögliche Werte: True oder False.</li><li>**OSDAdapter0IPAddressList** – durch Kommas getrennte Liste der IP-Adressen für die Karte; diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf **false**festgelegt.<br />    Diese Einstellung ist erforderlich.</li><li>**OSDAdapter0SubnetMask** – durch Kommas getrennte Liste der Subnetzmasken; diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf **false**festgelegt.<br />    Diese Einstellung ist erforderlich.</li><li>**OSDAdapter0Gateways** – durch Kommas getrennte Liste der IT-Gatewayadressen; diese Eigenschaft wird ignoriert, es sei denn, **EnableDHCP** ist auf **false**festgelegt.<br />    Diese Einstellung ist erforderlich.</li><li>**OSDAdapter0DNSDomain** : DNS-Domäne (Domain Name System) für die Karte</li><li>**OSDAdapter0DNSServerList** – durch Kommas getrennte Liste der DNS-Server für die Karte<br />    Diese Einstellung ist erforderlich.</li><li>**OSDAdapter0EnableDNSRegistration** - **true** registriert die IP-Adresse für die Karte in DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration** - **true** registriert die IP-Adresse der Karte unter dem vollständigen DNS-Namen des Computers in DNS.</li><li>**OSDAdapter0EnableIPProtocolFiltering** - **true**aktiviert die IP-Protokollfilterung für die Karte.</li><li>**OSDAdapter0IPProtocolFilterList** – durch Kommas getrennte Liste der Protokolle, die über IP ausgeführt werden dürfen; diese Eigenschaft wird ignoriert, wenn **EnableIPProtocolFiltering** auf **false**festgelegt ist.</li><li>**OSDAdapter0EnableTCPFiltering** - **true** aktiviert TCP-Portfilterung für die Karte.</li><li>**OSDAdapter0TCPFilterPortList** – durch Kommas getrennte Liste der Ports, denen Zugriffsberechtigungen für TCP zu erteilen sind; diese Eigenschaft wird ignoriert, wenn **EnableTCPFiltering** auf **false**festgelegt ist.</li><li>**OSDAdapter0TcpipNetbiosOptions** – Optionen für NetBIOS über TCP/IP; Es sind folgende Werte möglich:<br /><br /> <ul><li>0: NetBIOS-Einstellungen von DHCP-Server verwenden</li><li>1: NetBIOS über TCP/IP aktivieren</li><li>2: NetBIOS über TCP/IP deaktivieren</li></ul></li><li>**OSDAdapter0EnableWINS** - **true** verwendet WINS für die Namensauflösung.</li><li>**OSDAdapter0WINSServerList** – durch Kommas getrennte Liste der WINS-Server-IP-Adressen; diese Eigenschaft wird ignoriert, es sei denn, **EnableWINS** ist auf **true**festgelegt.</li><li>**OSDAdapter0MacAddress** – Mithilfe der MAC-Adresse (Media Access Control) werden Einstellungen der physischen Netzwerkkarte zugeordnet.</li><li>**OSDAdapter0Name** – Name der Netzwerkverbindung, der in der Systemsteuerung unter „Netzwerkverbindungen“ angezeigt wird; der Name ist zwischen 0 und 255 Zeichen lang.</li><li>**OSDAdapter0Index** – Index der Netzwerkkarteneinstellungen im Array der Einstellungen.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (Eingabe)|Hiermit wird die Anzahl der Netzwerkkarten angegeben, die auf dem Zielcomputer installiert sind. Wenn der **OSDAdapterCount** -Wert festgelegt wird, müssen alle Konfigurationsoptionen für die einzelnen Adapter festgelegt werden. Wenn Sie z. B. den **OSDAdapterTCPIPNetbiosOptions** -Wert für einen bestimmten Adapter festlegen, müssen auch alle anderen Werte für diesen Adapter konfiguriert werden.<br /><br /> <br /><br /> Wenn dieser Wert nicht angegeben wird, werden alle **OSDAdapter** -Werte ignoriert.|  
|OSDDNSDomain<br /><br /> (Eingabe)|Hiermit wird der primäre DNS-Server angegeben, der vom Zielcomputer verwendet wird.|  
|OSDDomainName<br /><br /> (Eingabe)|Hiermit wird der Name der Windows-Domäne angegeben, der der Zielcomputer hinzugefügt wird. Der angegebene Wert muss ein gültiger Active Directory-Domänendienste-Domänenname sein.|  
|OSDDomainOUName<br /><br /> (Eingabe)|Hiermit wird der Name der Organisationseinheit, der der Zielcomputers hinzugefügt wird, im RFC 1779-Format angegeben. Wenn dieser Parameter angegeben wird, muss die Zeichenfolge einen vollständigen Pfad enthalten.<br /><br /> Beispiel:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der TCP/IP-Filter aktiviert wird.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDJoinAccount<br /><br /> (Eingabe)|Hiermit wird das Netzwerkkonto angegeben, über das der Zielcomputer einer Windows-Domäne hinzugefügt wird.|  
|OSDJoinPassword<br /><br /> (Eingabe)|Hiermit wird das Netzwerkkennwort angegeben, über das der Zielcomputer einer Windows-Domäne hinzugefügt wird.|  
|OSDNetworkJoinType<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der Zielcomputer einer Windows-Domäne oder einer Arbeitsgruppe hinzugefügt wird.<br /><br /> **0** bedeutet, dass der Zielcomputer einer Windows-Domäne hinzugefügt wird. **1** bedeutet, dass der Computer einer Arbeitsgruppe hinzugefügt wird.<br /><br /> Gültige Werte:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (Eingabe)|Hiermit wird die DNS-Suchreihenfolge für den Zielcomputer angegeben.|  
|OSDWorkgroupName<br /><br /> (Eingabe)|Hiermit wird der Name der Arbeitsgruppe angegeben, der der Zielcomputer hinzugefügt wird.<br /><br /> Sie müssen entweder diesen Wert oder den Wert **OSDDomainName** angeben. Der Name der Arbeitsgruppe darf maximal 32 Zeichen umfassen.<br /><br /> Beispiel:<br /><br /> **„Accounting“**|  

###  <a name="BKMK_ApplyOperatingSystem"></a> Variablen der Tasksequenzaktion „Betriebssystemabbild anwenden“  
 Mit den Variablen für diese Aktion werden Einstellungen für das Betriebssystem angegeben, das Sie auf dem Zielcomputer installieren möchten. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Apply Operating System Image (Betriebssystemimage anwenden)](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (Eingabe)|Gibt den Dateinamen der Antwortdatei für die Betriebssystembereitstellung an, die zum Bereitstellungspaket des Betriebssystems gehört.|  
|OSDImageIndex<br /><br /> (Eingabe)|Hiermit wird der Abbildindexwert der WIM-Datei angegeben, die auf den Zielcomputer angewendet wird.|  
|OSDInstallEditionIndex<br /><br /> (Eingabe)|Hiermit wird die Version von Windows Vista oder einem späteren Betriebssystem angegeben, die bzw. das installiert wird. Wenn keine Version festgelegt ist, bestimmt Windows Setup anhand des referenzierten Produktschlüssels, welche Version installiert werden soll.<br /><br /> Verwenden Sie den Wert null (0) nur, wenn Folgendes zutrifft:<br /><br /> Sie installieren ein Betriebssystem vor Windows Vista.<br />Sie installieren eine Volumenlizenzedition von Windows Vista oder höher, und es wird kein Product Key angegeben.<br /><br /> Gültige Werte:<br /><br /> **„0“** (Standard)|  
|OSDTargetSystemDrive (Ausgabe)|Hiermit wird der Laufwerksbuchstabe der Partition angegeben, die die Betriebssystemdateien enthält.|  

###  <a name="BKMK_ApplyWindowsSettings"></a> Variablen der Tasksequenzaktion „Windows-Einstellungen anwenden“  
 Mit den Variablen für diese Aktion werden Windows-Einstellungen für den Zielcomputer angegeben, darunter der Computername, der Windows Product Key, der registrierte Benutzer und die Organisation sowie das lokale Administratorkennwort. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Apply Windows Settings (Windows-Einstellungen anwenden)](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (Eingabe)|Hiermit wird der Name des Zielcomputers angegeben.<br /><br /> Beispiel:<br /><br /> **"%_SMSTSMachineName%"** (Standard)|  
|OSDProductKey<br /><br /> (Eingabe)|Gibt den Windows-Product Key an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.|  
|OSDRegisteredUserName<br /><br /> (Eingabe)|Gibt den registrierten Standardbenutzernamen im neuen Betriebssystem an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.|  
|OSDRegisteredOrgName<br /><br /> (Eingabe)|Gibt den registrierten Standardorganisationsnamen im neuen Betriebssystem an. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.|  
|OSDTimeZone<br /><br /> (Eingabe)|Hiermit wird die Standardeinstellung für die Zeitzone angegeben, die im neuen Betriebssystem verwendet wird.|  
|OSDServerLicenseMode<br /><br /> (Eingabe)|Hiermit wird der verwendete Windows Server-Lizenzmodus angegeben.<br /><br /> Gültige Werte:<br /><br /> **„PerSeat“**<br /><br /> **„PerServer“**|  
|OSDServerLicenseConnectionLimit<br /><br /> (Eingabe)|Gibt die Anzahl der maximal zulässigen Verbindungen an. Die angegebene Zahl muss zwischen 5 und 9999 liegen.|  
|OSDRandomAdminPassword<br /><br /> (Eingabe)|Gibt ein zufällig erstelltes Kennwort für das Administratorkonto im neuen Betriebssystem an. Wenn **true**festgelegt ist, wird das lokale Administratorkonto auf dem Bereitstellungszielcomputer deaktiviert. Wenn **false**festgelegt ist, wird das lokale Administratorkonto auf dem Bereitstellungszielcomputer aktiviert, und dem Kennwort des lokalen Administratorkontos wird der Wert der Variable **OSDLocalAdminPassword**zugewiesen.<br /><br /> Gültige Werte:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**|  
|OSDLocalAdminPassword<br /><br /> (Eingabe)|Gibt das lokale Administratorkennwort an. Dieser Wert wird ignoriert, wenn die Option **Lokales Administratorkennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren** aktiviert ist. Der angegebene Wert darf zwischen 1 und 255 Zeichen enthalten.|  

###  <a name="BKMK_AutoApplyDrivers"></a> Variablen der Tasksequenzaktion „Treiber automatisch anwenden“  
 Mit den Variablen für diese Aktion wird angegeben, welche Windows-Treiber auf dem Zielcomputer installiert werden und ob die Installation nicht signierter Treiber möglich ist. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Auto Apply Drivers (Treiber automatisch anwenden)](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (Eingabe)|Eine durch Kommas getrennte Liste der eindeutigen IDs der Treiberkatalogkategorie. Wenn diese Variable angegeben wird, werden bei der Tasksequenzaktion **Treiber automatisch anwenden** im Rahmen der Treiberinstallation nur Treiber berücksichtigt, die mindestens einer dieser Kategorien angehören. Dieser Wert ist optional und wird standardmäßig nicht festgelegt. Die verfügbaren Kategorie-IDs können durch Aufzählen der Liste der **SMS_CategoryInstance** -Objekte auf dem Standort abgerufen werden.|  
|OSDAllowUnsignedDriver<br /><br /> (Eingabe)|Hiermit wird angegeben, ob Windows so konfiguriert wird, dass die Installation nicht signierter Gerätetreiber zugelassen wird. Diese Tasksequenzvariable wird bei der Bereitstellung von Windows Vista und späteren Betriebssystemen nicht verwendet.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (Eingabe)|Hiermit wird die Vorgehensweise der Tasksequenzaktion für den Fall angegeben, dass der Treiberkatalog mehrere mit einem Hardwaregerät kompatible Gerätetreiber enthält Wenn **true**festgelegt ist, wird nur der optimale Gerätetreiber installiert.  Wenn **false**festgelegt ist, werden alle kompatiblen Gerätetreiber installiert, und der optimale Treiber wird vom Betriebssystem ausgewählt.<br /><br /> Gültige Werte:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**|  

###  <a name="BKMK_CaptureNetworkSettings"></a> Variablen der Tasksequenzaktion „Netzwerkeinstellungen erfassen“  
 Mit den Variablen für diese Aktion wird angegeben, ob die Konfigurationsinformationen für die Netzwerkkarteneinstellungen (TCP/IP, DNS und WINS) erfasst und die Informationen zur Arbeitsgruppen- oder Domänenmitgliedschaft im Rahmen der Betriebssystembereitstellung migriert werden. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Capture Network Settings (Netzwerkeinstellungen erfassen)](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die Konfigurationsinformationen für die Netzwerkkarteneinstellungen (TCP/IP, DNS und WINS) erfasst werden.<br /><br /> Beispiele:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**|  
|OSDMigrateNetworkMembership<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die Informationen zur Arbeitsgruppen- oder Domänenmitgliedschaft im Rahmen der Betriebssystembereitstellung migriert werden.<br /><br /> Beispiele:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**|  

###  <a name="BKMK_CaptureOperatingSystemImage"></a> Variablen der Tasksequenzaktion „Betriebssystemabbild erfassen“  
 Mit den Variablen für diese Aktion werden Informationen zu dem erfassten Betriebssystemabbild angegeben, darunter der Speicherort, der Ersteller und die Beschreibung des Abbilds. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Capture Operating System Image (Betriebssystemimage erfassen)](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (Eingabe)|Hiermit wird ein Windows-Kontoname mit der Berechtigung, das erfasste Abbild in einer Netzwerkfreigabe zu speichern, angegeben.|  
|OSDCaptureAccountPassword<br /><br /> (Eingabe)|Gibt das Kennwort für das Windows-Konto an, das zum Speichern des erfassten Abbilds in einem freigegebenen Netzwerkordner verwendet wird.|  
|OSDCaptureDestination<br /><br /> (Eingabe)|Hiermit wird der Speicherort angegeben, an dem das erfasste Betriebssystemabbild gespeichert wird. Die maximale Länge für den Verzeichnisnamen beträgt 255 Zeichen.|  
|OSDImageCreator<br /><br /> (Eingabe)|Dies ist ein optionaler Name des Benutzers, der das Abbild erstellt hat. Dieser Name wird in der WIM-Datei gespeichert. Die maximale Länge des Benutzernamens beträgt 255 Zeichen.|  
|OSDImageDescription<br /><br /> (Eingabe)|Dies ist eine optionale benutzerdefinierte Beschreibung des erfassten Betriebssystemabbilds. Diese Beschreibung wird in der WIM-Datei gespeichert. Die maximale Länge der Beschreibung beträgt 255 Zeichen.|  
|OSDImageVersion<br /><br /> (Eingabe)|Eine optionale benutzerdefinierte Versionsnummer, die dem erfassten Betriebssystemabbild zugewiesen wird. Diese Versionsnummer wird in der WIM-Datei gespeichert. Bei diesem Wert kann es sich um eine beliebige Zeichenkombination mit einer maximalen Länge von 32 Zeichen handeln.|  
|OSDTargetSystemRoot<br /><br /> (Eingabe)|Gibt den Pfad zum Windows-Verzeichnis des installierten Betriebssystems auf dem Referenzcomputer an. Es wird dann geprüft, ob das Betriebssystem die Erfassung durch Configuration Manager unterstützt.|  

###  <a name="BKMK_CaptureUserState"></a> Variablen der Tasksequenzaktion „Benutzerzustand erfassen“  
 Mit den Variablen für diese Aktion werden die vom Migrationstool für den Benutzerstatus (USMT) verwendeten Informationen angegeben, darunter der Ordner, in dem der Benutzerzustand gespeichert wird, Befehlszeilenoptionen für USMT sowie die Konfigurationsdateien, mit denen die Erfassung der Benutzerprofile gesteuert wird.  Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Capture User State (Benutzerzustand erfassen)](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (Eingabe)|Dies ist der UNC- oder lokale Pfadname des Ordners, in dem der Benutzerzustand gespeichert wird. Kein Standardwert.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (Eingabe)|Hiermit werden Befehlszeilenoptionen für USMT angegeben, die bei der Erfassung des Benutzerzustands verwendet, aber nicht in der Configuration Manager-Benutzeroberfläche verfügbar gemacht werden. Die zusätzlichen Optionen werden im Format einer Zeichenfolge angegeben, die der automatisch generierten USMT-Befehlszeile hinzugefügt wird.<br /><br /> <br /><br /> Die USMT-Optionen, die mit dieser Tasksequenzvariablen angegeben werden, werden vor dem Ausführen dieser Tasksequenz nicht auf Genauigkeit überprüft.|  
|OSDMigrateMode<br /><br /> (Eingabe)|Ermöglicht das Anpassen der Dateien, die mit USMT erfasst wurden. Wenn diese Variable auf „Einfach“ festgelegt ist, werden nur die USMT-Standardkonfigurationsdateien verwendet. Wenn diese Variable auf „Erweitert“ festgelegt ist, werden von der Tasksequenzvariablen OSDMigrateConfigFiles die von USMT verwendeten Konfigurationsdateien angegeben.<br /><br /> Gültige Werte:<br /><br /> **„Einfach“**<br /><br /> **„Erweitert“**|  
|OSDMigrateConfigFiles<br /><br /> (Eingabe)|Gibt die Konfigurationsdateien an, mit denen die Erfassung von Benutzerprofilen gesteuert wird. Diese Variable wird nur verwendet, wenn OSDMigrateMode auf „Erweitert“ festgelegt wurde. Dieser durch Kommas getrennte Listenwert wird festgelegt, um die Migration benutzerdefinierter Benutzerprofile auszuführen.<br /><br /> Beispiel: miguser.xml, migsys.xml, migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (Eingabe)|Ermöglicht, dass die Erfassung des Benutzerzustands fortgesetzt wird, wenn einige Dateien nicht erfasst werden können.<br /><br /> Gültige Werte:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (Eingabe)|Aktiviert die ausführliche Protokollierung für USMT.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (Eingabe)|Hiermit wird angegeben, ob verschlüsselte Dateien erfasst werden.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|_OSDMigrateUsmtPackageID<br /><br /> (Eingabe)|Gibt die Paket-ID des Configuration Manager-Pakets an, das die USMT-Dateien enthält. Diese Variable ist erforderlich.|  

###  <a name="BKMK_CaptureWindowsSettings"></a> Variablen der Tasksequenzaktion „Windows-Einstellungen erfassen“  
 Mit den Variablen für diese Aktion wird angegeben, ob bestimmte Windows-Einstellungen zum Zielcomputer migriert werden, darunter der Name des Computers, der registrierte Organisationsname sowie Informationen zur Zeitzone. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Capture Windows Settings (Windows-Einstellungen erfassen)](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der Computername migriert wird.<br /><br /> Gültige Werte:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**<br /><br /> Wenn der Wert TRUE lautet, wird die Variable OSDComputerName auf den NetBIOS-Namen des Computers festgelegt.|  
|OSDComputerName<br /><br /> (Ausgabe)|Auf den NetBIOS-Namen des Computers festlegen. Der Wert wird nur festgelegt, wenn die Variable OSDMigrateComputerName auf TRUE festgelegt ist.|  
|OSDMigrateRegistrationInfo<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die Informationen zum Computerbenutzer und zur Organisation migriert werden.<br /><br /> Gültige Werte:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**<br /><br /> Wenn der Wert TRUE lautet, wird die Variable OSDRegisteredOrgName auf den registrierten Organisationsnamen des Computers festgelegt.|  
|OSDRegisteredOrgName<br /><br /> (Ausgabe)|Auf den registrierten Organisationsnamen des Computers festlegen. Der Wert wird nur festgelegt, wenn die Variable OSDMigrateRegistrationInfo auf TRUE festgelegt ist.|  
|OSDMigrateTimeZone<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die Zeitzone des Computers migriert wird.<br /><br /> Gültige Werte:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**<br /><br /> Wenn der Wert TRUE zurückgegeben wird, wird die Variable „OSDTimeZone“ auf die Zeitzone des Computers festgelegt.|  
|OSDTimeZone<br /><br /> (Ausgabe)|Diese Variable wird auf die Zeitzone des Computers festgelegt. Der Wert wird nur festgelegt, wenn die Variable OSDMigrateTimeZone auf TRUE festgelegt ist.|  

###  <a name="BKMK_ConnecttoNetworkFolder"></a> Variablen der Tasksequenzaktion „Verbindung mit Netzwerkordner herstellen“  
 Mit den Variablen für diese Aktion werden Informationen zu einem Ordner im Netzwerk angegeben, darunter die Anmeldeinformationen (Konto und Kennwort), über die die Verbindung mit dem Netzwerkordner hergestellt wird, sowie der Laufwerksbuchstabe und der Pfad des Ordners. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Connect To Network Folder (Verbindung mit Netzwerkordner herstellen)](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (Eingabe)|Hiermit wird das Administratorkonto angegeben, über das eine Verbindung mit der Netzwerkfreigabe hergestellt wird.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (Eingabe)|Gibt den Laufwerkbuchstaben des Netzwerks an, mit dem eine Verbindung hergestellt werden soll. Dieser Wert ist optional. Wenn er nicht angegeben ist, wird die Netzwerkverbindung keinem Laufwerkbuchstaben zugeordnet. Wenn der Wert angegeben wird, muss er im Bereich von D: bis Z: liegen.  Sie dürfen außerdem X: nicht verwenden, da dieser Laufwerksbuchstabe während der Windows PE-Phase von Windows PE verwendet wird.<br /><br /> Beispiele:<br /><br /> **„D:“**<br /><br /> **„E:“**|  
|SMSConnectNetworkFolderPassword<br /><br /> (Eingabe)|Hiermit wird das Netzwerkkonto angegeben, über das eine Verbindung mit der Netzwerkfreigabe hergestellt wird.|  
|SMSConnectNetworkFolderPath<br /><br /> (Eingabe)|Gibt den Netzwerkpfad für die Verbindung an.<br /><br /> Beispiel:<br /><br /> **"\\Servername\Freigabename"**|  

###  <a name="BKMK_ConvertDisk"></a> Variablen der Tasksequenzaktion „In dynamischen Datenträger konvertieren“  
 Mit der Variablen für diese Aktion wird die Nummer des physischen Datenträgers angegeben, der von einem einfachen in einen dynamischen Datenträger konvertiert werden soll. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Convert Disk to Dynamic (In dynamischen Datenträger konvertieren)](task-sequence-steps.md#BKMK_ConvertDisktoDynamic).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDConvertDiskIndex<br /><br /> (Eingabe)|Hiermit wird die Nummer des physischen Datenträgers angegeben, der konvertiert wird.|  

###  <a name="BKMK_EnableBitLocker"></a> Variablen der Tasksequenzaktion „BitLocker aktivieren“  
 Mit den Variablen für diese Aktion werden das Wiederherstellungskennwort und der Systemstartschlüssel angegeben, mit denen BitLocker auf dem Zielcomputer aktiviert wird. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Enable BitLocker (Aktivieren von BitLocker)](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (Eingabe)|Von der Tasksequenzaktion **BitLocker aktivieren** wird kein zufälliges Wiederherstellungskennwort generiert, sondern der angegebene Wert als Wiederherstellungskennwort verwendet. Dieser Wert muss ein gültiges numerisches BitLocker-Wiederherstellungskennwort sein.|  
|OSDBitLockerStartupKey<br /><br /> (Eingabe)|Von der Tasksequenzaktion **BitLocker aktivieren** wird kein zufälliger Systemstartschlüssel für die Schlüsselverwaltungsoption **Nur Schlüssel zum Systemstart auf USB** generiert, sondern das Trusted Platform Module (TPM) als Systemstartschlüssel verwendet. Bei dem Wert muss es sich um einen gültigen, 256-Bit Base64-codierten BitLocker-Systemstartschlüssel handeln.|  

###  <a name="BKMK_FormatPartitionDisk"></a> Variablen der Tasksequenzaktion „Datenträger formatieren und partitionieren“  
 Mit den Variablen für diese Aktion werden Informationen zur Formatierung und Partitionierung eines physischen Datenträgers angegeben, darunter die Datenträgernummer und ein Array der Partitionseinstellungen. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Format and Partition Disk (Datenträger formatieren und partitionieren)](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (Eingabe)|Gibt die Anzahl der zu partitionierenden physischen Datenträger an.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (Eingabe)|Hiermit wird angegeben, ob die Cacheausrichtungsoptimierung deaktiviert werden soll, wenn die Festplatte für die Kompatibilität mit bestimmten BIOS-Typen partitioniert wird. Dies kann beim Bereitstellen der Betriebssysteme Windows XP- oder Windows Server 2003 erforderlich sein. Weitere Informationen hierzu finden Sie im [Artikel 931760](http://go.microsoft.com/fwlink/?LinkId=134081) und im [Artikel 931761](http://go.microsoft.com/fwlink/?LinkId=134082) der Microsoft Knowledge Base.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDGPTBootDisk<br /><br /> (Eingabe)|Hiermit wird angegeben, ob eine EFI-Partition auf einer GPT-Festplatte erstellt werden soll, damit diese als Startdatenträger für EFI-basierte Computer verwendet werden kann.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDPartitions<br /><br /> (Eingabe)|Gibt ein Array von Partitionseinstellungen an. Informationen zum Zugriff auf Arrayvariablen in der Tasksequenzumgebung finden Sie im Abschnitt über SDK.<br /><br /> Bei dieser Tasksequenzvariablen handelt es sich um die Arrayvariable. Die einzelnen Elemente im Array stellen die Einstellungen für eine einzelne Partition auf der Festplatte dar. Die Einstellungen, die für jede Partition definiert sind, können aufgerufen werden, indem der Name der Arrayvariablen mit der Null-basierten Nummer der Festplattenpartition und dem Eigenschaftennamen kombiniert wird.<br /><br /> Die folgenden Variablennamen können beispielsweise verwendet werden, um die Eigenschaften für die erste Partition zu definieren, die von dieser Tasksequenzaktion auf der Festplatte erstellt werden:<br /><br /> - **OSDPartitions0Type** – Hiermit wird die Größe der Partition angegeben. Dies ist eine erforderliche Eigenschaft. Gültige Werte lauten „**Primär**“, „**Erweitert**“, „**Logisch**“ und „**Versteckt**“.<br />-   **OSDPartitions0FileSystem** – Gibt den Typ des Dateisystems an, das zum Formatieren der Partition verwendet wird. Dabei handelt es sich um eine optionale Eigenschaft. Wenn kein Dateisystem angegeben ist, wird die Partition nicht formatiert. Gültige Werte sind „**FAT32**“ und „**NTFS**“.<br />-   **OSDPartitions0Bootable** : Hiermit wird angegeben, ob die Partition startbar ist. Dies ist eine erforderliche Eigenschaft. Wenn der Wert für MBR-Datenträger auf „**TRUE**“ festgelegt ist, werden diese Datenträger zur aktiven Partition gemacht.<br />-   **OSDPartitions0QuickFormat** : Hiermit wird der Typ des verwendeten Formats angegeben. Dies ist eine erforderliche Eigenschaft. Wenn dieser Wert auf „**TRUE**“ festgelegt ist, wird eine Schnellformatierung ausgeführt. Andernfalls erfolgt eine vollständige Formatierung.<br />-   **OSDPartitions0VolumeName** : Hiermit wird der Name angegeben, der dem Volume bei der Formatierung zugewiesen wird. Dies ist eine optionale Eigenschaft.<br />-   **OSDPartitions0Size** – Gibt die Größe der Partition an. Einheiten werden von der Variablen **OSDPartitions0SizeUnits** angegeben. Dies ist eine optionale Eigenschaft. Wenn diese Eigenschaft nicht angegeben wird, wird die Partition mit dem gesamten verbleibenden freien Speicherplatz erstellt.<br />-   **OSDPartitions0SizeUnits** – Gibt die Einheiten an, die verwendet werden, wenn die Tasksequenzvariable **OSDPartitions0Size** interpretiert wird. Dies ist eine optionale Eigenschaft. Gültige Werte sind „**MB**“ (Standard), „**GB**“ und „**Prozent**“.<br />-   **OSDPartitions0VolumeLetterVariable** – Bei der Erstellung von Partitionen wird für diese immer der nächste verfügbare Laufwerkbuchstabe in Windows PE verwendet. Geben Sie mit dieser optionalen Eigenschaft den Namen einer anderen Tasksequenzvariablen an, der verwendet wird, um den neuen Laufwerkbuchstaben zur weiteren Referenz zu speichern.<br /><br /> <br /><br /> Wenn mehrere Partitionen mit dieser Tasksequenzaktion definiert werden, können die Eigenschaften für die zweite Partition definiert werden, indem deren Index im Variablennamen verwendet wird; Beispiele: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**und **OSDPartitions1VolumeName** .|  
|OSDPartitionStyle<br /><br /> (Eingabe)|Gibt den bei der Partitionierung des Datenträgers zu verwendenden Partitionsstil an. "**MBR**" steht für den Partitionsstil "Master Boot Record" und "**GPT**" für den Stil "GUID-Partitionstabelle".<br /><br /> Gültige Werte:<br /><br /> **„GPT“**<br /><br /> **„MBR“**|  

###  <a name="BKMK_InstallSoftwareUpdates"></a> Variablen der Tasksequenzaktion „Softwareupdates installieren“  
 Mit der Variablen für diese Aktion wird angegeben, ob sämtliche Updates oder nur obligatorische Updates installiert werden sollen. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Install Software Updates (Softwareupdates installieren) ](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (Eingabe)|Hiermit wird angegeben, ob sämtliche Updates oder nur obligatorische Updates installiert werden sollen.<br /><br /> Gültige Werte:<br /><br /> **„Alle“**<br /><br /> **„Obligatorisch“**|  

###  <a name="BKMK_JoinDomainWorkgroup"></a> Variablen der Tasksequenzaktion „Einer Domäne oder Arbeitsgruppe beitreten“  
 Mit den Variablen für diese Aktion werden Informationen angegeben, die für den Beitritt des Zielcomputers zu einer Windows-Domäne oder Arbeitsgruppe erforderlich sind. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Join Domain or Workgroup (Einer Domäne oder Arbeitsgruppe beitreten)](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (Eingabe)|Hiermit wird das Konto angegeben, über das der Beitritt des Zielcomputers zur Windows-Domäne erfolgt. Diese Variable ist für den Beitritt zu einer Domäne erforderlich.|  
|OSDJoinDomainName<br /><br /> (Eingabe)|Hiermit wird der Name einer Windows-Domäne angegeben, der der Zielcomputer hinzugefügt wird. Der Name der Windows-Domäne muss zwischen 1 und 255 Zeichen enthalten.|  
|OSDJoinDomainOUName<br /><br /> (Eingabe)|Hiermit wird der Name der Organisationseinheit, der der Zielcomputers hinzugefügt wird, im RFC 1779-Format angegeben. Wenn dieser Parameter angegeben wird, muss die Zeichenfolge einen vollständigen Pfad enthalten. Der Organisationseinheitsname für die Windows-Domäne muss zwischen 0 und 32.767 Zeichen enthalten. Dieser Wert wird nicht festgelegt, wenn die Variable **OSDJoinType** den Wert „1“ (Arbeitsgruppe beitreten) hat.<br /><br /> Beispiel:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (Eingabe)|Hiermit wird das Netzwerkkennwort angegeben, über das der Beitritt des Zielcomputers zur Windows-Domäne erfolgt. Wenn die Variable nicht angegeben wird, wird ein Versuch mit einem leeren Kennwort unternommen. Dieser Wert ist erforderlich, wenn die Variable **OSDJoinType** den Wert**0**(Domäne beitreten) hat.|  
|OSDJoinSkipReboot<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der Neustart des Zielcomputers nach dessen Beitritt zur Domäne oder Arbeitsgruppe übersprungen werden soll.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“**|  
|OSDJoinType<br /><br /> (Eingabe)|Hiermit wird angegeben, ob der Zielcomputer einer Windows-Domäne oder einer Arbeitsgruppe hinzugefügt wird. Geben Sie**0**an, wenn der Zielcomputer einer Windows-Domäne hinzugefügt werden soll. Geben Sie**1**an, wenn der Zielcomputer einer Arbeitsgruppe hinzugefügt werden soll.<br /><br /> Gültige Werte:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (Eingabe)|Hiermit wird der Name einer Arbeitsgruppe angegeben, der der Zielcomputer hinzugefügt wird. Der Name der Arbeitsgruppe muss zwischen 1 und 32 Zeichen enthalten.<br /><br /> Beispiel:<br /><br /> **„Accounting“**|  

###  <a name="BKMK_PrepareWindowsCapture"></a> Variablen der Tasksequenzaktion „Windows für die Erfassung vorbereiten“  
 Mit den Variablen für diese Aktion werden Informationen angegeben, die zum Erfassen des Windows-Betriebssystems auf dem Zielcomputer erforderlich sind. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Prepare ConfigMgr Client for Capture (Prepare ConfigMgr Client for Capture)](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (Eingabe)|Hiermit wird angegeben, ob von Sysprep eine Treiberliste für Massenspeichergeräte erstellt wird. Diese Einstellung gilt nur für Windows XP and Windows Server 2003. Sie dient dazu, in der Datei sysprep.inf den Abschnitt [SysprepMassStorage] mit Informationen zu allen Massenspeichertreibern aufzufüllen, die von dem zu erfassenden Abbild unterstützt werden.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDKeepActivation<br /><br /> (Eingabe)|Hiermit wird angegeben, ob das Produktaktivierungskennzeichen von Sysprep zurückgesetzt wird.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDTargetSystemRoot<br /><br /> (Ausgabe)|Gibt den Pfad zum Windows-Verzeichnis des installierten Betriebssystems auf dem Referenzcomputer an. Es wird dann geprüft, ob das Betriebssystem die Erfassung durch Configuration Manager unterstützt.|  

###  <a name="BKMK_ReleaseStateStore"></a> Variablen der Tasksequenzaktion „Zustandsspeicher freigeben“  
 Mit den Variablen für diese Aktion werden Informationen angegeben, die zur Freigabe des gespeicherten Benutzerzustands verwendet werden. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Release State Store (Zustandsspeicher freigeben)](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (Eingabe)|Dies ist der UNC- oder lokale Pfadname des Speicherorts, von dem aus der Benutzerzustand wiederhergestellt wird. Dieser Wert wird von den Tasksequenzaktionen **Benutzerzustand erfassen** und **Benutzerzustand wiederherstellen** verwendet.|  

###  <a name="BKMK_RequestState"></a> Variablen der Tasksequenzaktion „Zustandsspeicher anfordern“  
 Mit den Variablen für diese Aktion werden Informationen für die Anforderung des gespeicherten Benutzerzustands angegeben. Hierzu gehört z. B. der Ordner auf dem Zustandsmigrationspunkt, in dem die Benutzerdaten gespeichert sind. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Release State Store (Zustandsspeicher freigeben)](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (Eingabe)|Hiermit wird angegeben, ob das Netzwerkzugriffskonto als Ausweichmöglichkeit verwendet wird, wenn über das Computerkonto keine Verbindung mit dem Zustandsmigrationspunkt hergestellt werden kann.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDStateSMPRetryCount<br /><br /> (Eingabe)|Hiermit wird angegeben, wie viele Wiederholungsversuche des Tasksequenzschritts zum Suchen eines Zustandsmigrationspunkts ausgeführt werden, bevor der Schritt mit einem Fehler abgebrochen wird. Die angegebene Anzahl muss zwischen 0 und 600 liegen.|  
|OSDStateSMPRetryTime<br /><br /> (Eingabe)|Hiermit wird angegeben, wie viele Sekunden zwischen den einzelnen Versuchen des Tasksequenzschritts gewartet werden soll. Die Anzahl der Sekunden darf maximal 30 Zeichen umfassen.|  
|OSDStateStorePath<br /><br /> (Ausgabe)|Dies ist der UNC-Pfad des Ordners auf dem Zustandsmigrationspunkt, in dem der Benutzerzustand gespeichert ist.|  

###  <a name="BKMK_RestartComputer"></a> Variablen der Tasksequenzaktion „Computer neu starten“  
 Mit den Variablen für diese Aktion werden Informationen für den Neustart des Zielcomputers angegeben. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Restart Computer (Computer neu starten)](task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (Eingabe)|Hiermit wird die Nachricht angegeben, die den Benutzern vor dem Neustart des Zielcomputers angezeigt wird. Wenn diese Variable nicht festgelegt ist, wird die Standardnachricht angezeigt. Die angegebene Meldung darf nicht länger als 512 Zeichen sein.<br /><br /> Beispiel:<br /><br /> „Dieser Computer wird neu gestartet. Speichern Sie Ihre Daten.“|  
|SMSRebootTimeout<br /><br /> (Eingabe)|Gibt die Anzeigedauer der Warnmeldung an den Benutzer in Sekunden an, bis der Computer neu gestartet wird. Geben Sie null Sekunden an, wenn keine Neustartmeldung angezeigt werden soll.<br /><br /> Beispiele:<br /><br /> **„0“** (Standard)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="BKMK_RestoreUserState"></a> Variablen für die Tasksequenzaktion „Benutzerzustand wiederherstellen“  
 Mit den Variablen für diese Aktion werden Informationen angegeben, mit deren Hilfe der Benutzerzustand des Zielcomputers wiederhergestellt wird. Hierzu gehören z. B. der Pfadname des Ordners, von dem aus der Benutzerzustand wiederhergestellt wird, und die Angabe, ob das lokale Computerkonto wiederhergestellt wird. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Restore User State (Benutzerzustand wiederherstellen)](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (Eingabe)|Dies ist der UNC-Pfadname oder der lokale Pfadname des Ordners, von dem aus der Benutzerzustand wiederhergestellt wird.|  
|OSDMigrateContinueOnRestore<br /><br /> (Eingabe)|Hiermit wird angegeben, dass die Wiederherstellung des Benutzerzustands fortgesetzt wird, auch wenn einige Dateien nicht wiederhergestellt werden können.<br /><br /> Gültige Werte:<br /><br /> **„true“** (Standard)<br /><br /> **„false“**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (Eingabe)|Aktiviert die ausführliche Protokollierung für USMT. Dieser Wert ist für die Aktion erforderlich. Er muss auf „true“ oder „false“ festgelegt sein.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDMigrateLocalAccounts<br /><br /> (Eingabe)|Hiermit wird angegeben, ob das lokale Computerkonto wiederhergestellt werden soll.<br /><br /> Gültige Werte:<br /><br /> **„true“**<br /><br /> **„false“** (Standard)|  
|OSDMigrateLocalAccountPassword<br /><br /> (Eingabe)|Wenn für die Variable **OSDMigrateLocalAccounts** der Wert TRUE festgelegt ist, muss diese Variable das Kennwort enthalten, das allen zu migrierenden lokalen Konten zugewiesen wird. Da allen migrierten lokalen Konten das gleiche Kennwort zugewiesen wird, wird dieses Kennwort als temporäres Kennwort betrachtet, das später mit einem anderen Verfahren als der Configuration Manager-Betriebssystembereitstellung geändert wird.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (Eingabe)|Hiermit werden zusätzliche Befehlszeilenoptionen für Windows-EasyTransfer (früher USMT) angegeben, die beim Wiederherstellen des Benutzerzustands verwendet werden. Die zusätzlichen Optionen werden im Format einer Zeichenfolge angegeben, die der automatisch generierten USMT-Befehlszeile hinzugefügt wird. Die USMT-Optionen, die mit dieser Tasksequenzvariablen angegeben werden, werden vor dem Ausführen dieser Tasksequenz nicht auf Genauigkeit überprüft.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (Eingabe)|Gibt die Paket-ID des Configuration Manager-Pakets an, das die USMT-Dateien enthält. Diese Variable ist erforderlich.|  

###  <a name="BKMK_RunCommand"></a> Variablen der Tasksequenzaktion „Befehlszeile ausführen“  
 Mit den Variablen für diese Aktion werden Informationen angegeben, die zum Ausführen eines Befehls über die Befehlszeile verwendet werden. Hierzu gehört z. B. das Arbeitsverzeichnis, von dem aus der Befehl ausgeführt wird. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Run Command Line (Befehlszeile ausführen)](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen|Beschreibung|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (Eingabe)|Unter einem 64-Bit-Betriebssystem wird das Programm in der Befehlszeile standardmäßig gesucht und mithilfe des Dateisystem-Redirectors von WOW64 ausgeführt, sodass die 32-Bit-Versionen der Betriebssystemprogramme und -DLLs gefunden werden. Wenn Sie für die Variable den Wert TRUE festlegen, wird die Verwendung des Dateisystem-Redirectors von WOW64 deaktiviert, sodass die nativen 64-Bit-Versionen der Betriebssystemprogramme und -DLLs gefunden werden. Unter einem 32-Bit-Betriebssystem hat diese Variable keine Auswirkungen.|  
|WorkingDirectory<br /><br /> (Eingabe)|Gibt das Startverzeichnis für eine Befehlszeilenaktion an. Der angegebene Verzeichnisname darf nicht länger als 255 Zeichen sein.<br /><br /> Beispiele:<br /><br /> -   **C:\\**<br />-   **„%SystemRoot%“**|  
|SMSTSRunCommandLineUserName<br /><br /> (Eingabe)|Hiermit wird das Konto angegeben, mit dem die Befehlszeile ausgeführt wird. Der Wert ist eine Zeichenfolge in der Form Benutzername oder Domäne\Benutzername.|  
|SMSTSRunCommandLinePassword<br /><br /> (Eingabe)|Hiermit wird das Kennwort für das mit der Variablen SMSTSRunCommandLineUserName angegebene Konto angegeben.|  

### <a name="set-dynamic-variables"></a>Dynamische Variablen festlegen  
 Die Variablen für diese Aktion werden automatisch festgelegt, wenn Sie den Tasksequenzschritt „Dynamische Variablen festlegen“ hinzufügen. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Set Dynamic Variables (Dynamische Variablen festlegen)](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Gibt den Hersteller des Computers an.|  
|_SMSTSModel|Gibt das Modell des Computers an.|  
|_SMSTSMacAddresses|Gibt die vom Computer verwendeten MAC-Adressen an.|  
|_SMSTSIPAddresses|Gibt die vom Computer verwendeten IP-Adressen an.|  
|_SMSTSSerialNumber|Gibt die Seriennummer des Computers an.|  
|_SMSTSAssetTag|Gibt das Bestandskennzeichen für den Computer an.|  
|_SMSTSUUID|Gibt die UUID des Computers an.|  
|_SMSTSDefaultGateways|Gibt die vom Computer verwendeten Standardgateways an.|  

###  <a name="BKMK_SetupWindows"></a> Variablen der Tasksequenzaktion „Windows und ConfigMgr einrichten“  
 Mit der Variablen für diese Aktion werden die Clientinstallationseigenschaften angegeben, die bei der Installation des Configuration Manager-Client verwendet werden. Weitere Informationen zu dem Tasksequenzschritt, der diesen Variablen zugeordnet ist, finden Sie unter [Setup Windows and ConfigMgr (Windows und ConfigMgr einrichten)](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (Eingabe)|Hiermit werden die Eigenschaften der Clientinstallation angegeben, die bei der Installation des Configuration Manager-Clients verwendet werden.|  

### <a name="upgrade-operating-system"></a>Betriebssystem aktualisieren  
 Die Variable für diese Aktion gibt zusätzliche Befehlszeilenoptionen an, die in der Configuration Manager-Konsole nicht verfügbar sind, und die zu Setup für ein Windows 10-Upgrade hinzugefügt werden. Weitere Informationen zu dem Tasksequenzschritt, der dieser Variable zugeordnet ist, finden Sie unter [Upgrade Operating System (Betriebssystem aktualisieren)](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Details  

|Name der Aktionsvariablen<br /><br /> (Eingabe)|Beschreibung|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (Eingabe)|Gibt die zusätzlichen Befehlszeilenoptionen an, die Setup während eines Windows 10-Upgrades hinzugefügt werden. Die Befehlszeilenoptionen werden nicht überprüft. Daher sollten Sie überprüfen, ob die von Ihnen eingegebene Option richtig ist.<br /><br /> Weitere Informationen finden Sie unter [Windows Setup-Befehlszeilenoptionen](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).|  
