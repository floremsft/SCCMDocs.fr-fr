---
title: "Planungsüberlegungen für das Automatisieren von Tasks | Microsoft-Dokumentation"
description: Planen Sie Ihre automatisierten Tasks in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
caps.latest.revision: "13"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 830f715b688cc9929a179da94eba9c81de8db11a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2017
---
# <a name="planning-considerations-for-automating-tasks-in-system-center-configuration-manager"></a>Planungsüberlegungen für das Automatisieren von Tasks in System Center Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

In Ihrer System Center Configuration Manager-Umgebung können Sie Tasksequenzen zum Automatisieren von Tasks erstellen. Dieses Tasks reichen von der Erfassung eines Betriebssystems auf einem Referenzcomputer bis zur Bereitstellung des Betriebssystems auf mehreren Zielcomputern. Die Aktionen der Tasksequenz werden in den einzelnen Schritten der Sequenz definiert. Bei der Ausführung der Tasksequenz werden die Aktionen der einzelnen Schritte auf Befehlszeilenebene im Kontext des lokalen Systemkontos ohne Benutzereingriff ausgeführt. Die folgenden Abschnitte helfen Ihnen bei der Planung der Automatisierung von Tasks in Configuration Manager.

##  <a name="BKMK_TSStepsActions"></a> Tasksequenzschritte und -aktionen  
 Schritte sind die Grundkomponenten einer Tasksequenz. Sie können Befehle enthalten, mit denen das Betriebssystem eines Referenzcomputers konfiguriert und erfasst wird oder mit denen das Betriebssystem, Treiber, der Configuration Manager-Client und Software auf dem Zielcomputer installiert werden. Die Befehle eines Tasksequenzschritts werden von den Aktionen des Schritts definiert. Es gibt zwei Arten von Aktionen. Eine Aktion, die Sie mit einer Befehlszeilen-Zeichenfolge definieren, wird als benutzerdefinierte Aktion bezeichnet. Eine von Configuration Manager vordefinierte Aktion wird als integrierte Aktion bezeichnet. Von einer Tasksequenz kann eine beliebige Kombination aus benutzerdefinierten und integrierten Aktionen ausgeführt werden.  

 Tasksequenzschritte können auch Bedingungen umfassen, mit denen das Verhalten des Schritts wie beispielsweise das Beenden oder Fortsetzen der Tasksequenz bei einem Fehler gesteuert wird. Bedingungen werden einem Schritt als Teil einer Tasksequenzvariablen hinzugefügt. Beispielsweise können Sie mit der Variablen **SMSTSLastActionRetCode** die Bedingung des vorherigen Schritts testen. Variablen können einem einzelnen Schritt oder eine Gruppe von Schritten hinzugefügt werden.  

 Tasksequenzschritte werden nacheinander verarbeitet. Dies gilt auch für die Aktion des Schritts sowie für die dem Schritt zugeordneten Bedingungen. Wenn die Verarbeitung eines Tasksequenzschritts von Configuration Manager gestartet wird, wird der nächste Schritt erst nach Abschluss der vorherigen Aktion gestartet. Eine Tasksequenz gilt als abgeschlossen, wenn alle zugehörigen Schritte abgeschlossen wurden oder wenn die Ausführung der Tasksequenz aufgrund eines fehlerhaften Schritts von Configuration Manager beendet wird, bevor alle Schritte abgeschlossen wurden. Wenn beispielsweise ein referenziertes Image oder Paket auf einem Verteilungspunkt nicht von einem Tasksequenzschritt gefunden werden kann, enthält die Tasksequenz einen fehlerhaften Verweis. Die Ausführung der Tasksequenz wird an diesem Punkt von Configuration Manager beendet, es sei denn, für den fehlerhaften Schritt wurde die Bedingung „Bei Fehler fortsetzen“ definiert.  

> [!IMPORTANT]  
>  Eine Tasksequenz kann standardmäßig nicht weiter ausgeführt werden, nachdem bei einem Schritt oder einer Aktion ein Fehler aufgetreten ist. Wenn die Tasksequenz auch dann fortgesetzt werden soll, wenn in einem Schritt ein Fehler auftritt, bearbeiten Sie die Tasksequenz, klicken Sie auf die Registerkarte **Optionen** , und wählen Sie anschließend **Bei Fehler fortsetzen**.  

 Weitere Informationen zu den Schritten, die einer Tasksequenz hinzugefügt werden können, finden Sie unter [Tasksequenzschritte](../understand/task-sequence-steps.md).  

##  <a name="BKMK_TSGroups"></a> Tasksequenzgruppen  
 Bei **Gruppen** handelt es sich um mehrere Schritte einer Tasksequenz. Eine Tasksequenzgruppe setzt sich aus einem Namen, einer optionalen Beschreibung und optionalen Bedingungen zusammen, die als Einheit ausgewertet werden, bevor diese Tasksequenz mit dem nächsten Schritt fortgesetzt wird. Gruppen können ineinander geschachtelt werden, und eine Gruppe kann sowohl Schritte als auch Untergruppen enthalten. Gruppen sind zum Kombinieren mehrerer Schritte nützlich, für die eine gemeinsame Bedingung gilt.  

> [!IMPORTANT]  
>  Eine Tasksequenzgruppe kann standardmäßig nicht weiter ausgeführt werden, wenn bei einem Schritt oder einer eingebetteten Gruppe innerhalb der Gruppe ein Fehler auftritt. Wenn die Tasksequenz nach einem Fehler bei einem Schritt oder einer eingebetteten Gruppe fortgesetzt werden soll, bearbeiten Sie die Tasksequenz, klicken Sie auf die Registerkarte **Optionen** , und wählen Sie anschließend **Bei Fehler fortsetzen**.  

 In der folgenden Tabelle wird die Wirkung der Option **Bei Fehler fortsetzen** bei gruppierten Schritten veranschaulicht.  

 In diesem Beispiel gibt es zwei Gruppen von Tasksequenzen, die jeweils drei Tasksequenzschritte enthalten.  

|Tasksequenzgruppe oder -schritt|Einstellung „Bei Fehler fortsetzen“|  
|---------------------------------|-------------------------------|  
|**Tasksequenzgruppe 1**|**Bei Fehler fortsetzen** ausgewählt|  
|Tasksequenzschritt 1|**Bei Fehler fortsetzen** ausgewählt|  
|Tasksequenzschritt 2|Nicht festgelegt.|  
|Tasksequenzschritt 3|Nicht festgelegt.|  
|**Tasksequenzgruppe 2**|Nicht festgelegt.|  
|Tasksequenzschritt 4|Nicht festgelegt.|  
|Tasksequenzschritt 5|Nicht festgelegt.|  
|Tasksequenzschritt 6|Nicht festgelegt.|  

-   Tritt bei Tasksequenzschritt 1 ein Fehler auf, wird die Tasksequenz mit Tasksequenzschritt 2 fortgesetzt.  

-   Tritt bei Tasksequenzschritt 2 ein Fehler auf, wird die Tasksequenz nicht mit Tasksequenzschritt 3 fortgesetzt, sondern mit den Tasksequenzschritten 4 und 5, die sich in einer anderen Tasksequenzgruppe befinden.  

-   Tritt bei Tasksequenzschritt 4 ein Fehler auf, werden keine weiteren Schritte ausgeführt. Die Tasksequenz kann nicht ausgeführt werden, da die Einstellung **Bei Fehler fortsetzen** für die Tasksequenzgruppe 2 nicht konfiguriert wurde.  

 Sie müssen den Tasksequenzgruppen Namen zuweisen. Allerdings muss der Gruppenname nicht eindeutig sein. Sie können auch eine optionale Beschreibung für die Tasksequenzgruppe angeben.  

##  <a name="BKMK_TSVariables"></a> Tasksequenzvariablen  
 Tasksequenzvariablen sind Name-Wert-Paare, mit denen auf einem Configuration Manager-Clientcomputer Konfigurations- und Betriebssystembereitstellungseinstellungen für Tasks bereitgestellt werden, die zur Konfiguration von Computern, Betriebssystemen und Benutzerzuständen dienen. Mit Tasksequenzvariablen können die Schritte in einer Tasksequenz konfiguriert und angepasst werden.  

 Wenn Sie eine Tasksequenz ausführen, werden viele der Tasksequenzeinstellungen als Umgebungsvariablen gespeichert. Sie können die Werte integrierter Tasksequenzvariablen abrufen oder ändern sowie neue Tasksequenzvariablen erstellen, um die Art der Ausführung einer Tasksequenz auf einem Zielcomputer anzupassen.  

 Sie können mit Tasksequenzvariablen in der Tasksequenzumgebung folgende Aktionen ausführen:  

-   Konfigurieren von Einstellungen für eine Tasksequenzaktion  

-   Bereitstellen von Befehlszeilenargumenten für einen Tasksequenzschritt  

-   Auswerten einer Bedingung, von der bestimmt wird, ob ein Tasksequenzschritt oder eine Tasksequenzgruppe ausgeführt werden soll  

-   Angeben von Werten für benutzerdefinierte Skripts, die in einer Tasksequenz verwendet werden  

 Beispiel: Eine Tasksequenz enthält den Tasksequenzschritt **Einer Domäne oder Arbeitsgruppe beitreten**. Die Tasksequenz kann für verschiedene Sammlungen bereitgestellt werden, wobei die Sammlungsmitgliedschaft durch die Domänenmitgliedschaft bestimmt wird. In diesem Fall können Sie eine sammlungsspezifische Tasksequenzvariable für den Domänennamen jeder Sammlung festlegen und dann anhand dieser Tasksequenzvariablen den jeweiligen Domänennamen in der Tasksequenz angeben.  

###  <a name="BKMK_TSCreateVariables"></a> Erstellen von Tasksequenzvariablen  
 Sie können neue Tasksequenzvariablen hinzufügen, um die Schritte in einer Tasksequenz anzupassen und zu steuern. Zum Beispiel können Sie eine Tasksequenzvariable erstellen, um eine Einstellung für einen integrierten Tasksequenzschritt außer Kraft zu setzen. Sie können auch eine benutzerdefinierte Tasksequenzvariable erstellen, die in Bedingungen, Befehlszeilen oder benutzerdefinierten Schritten in der Tasksequenz verwendet werden kann. Wenn Sie eine Tasksequenzvariable erstellen, werden diese Tasksequenzvariable und der ihr zugeordnete Wert innerhalb der Tasksequenzumgebung beibehalten, auch wenn der Zielcomputer von der Sequenz neu gestartet wird. Die Variable und ihr Wert können innerhalb der Tasksequenz in verschiedenen Betriebssystemumgebungen verwendet werden. Sie können sie beispielsweise in einem vollständigen Windows-Betriebssystem und in der Windows PE-Umgebung einsetzen.  

 In der folgenden Tabelle werden die Methoden zum Erstellen einer Tasksequenzvariablen beschrieben und zusätzliche Informationen zur Verwendung aufgeführt.  

|Erstellungsmethode|Verwendung|  
|-------------------|-----------|  
|Festlegen von Feldern in Tasksequenzschritten mithilfe des Tasksequenz-Editors|Bei dieser Methode geben Sie Standardwerte für den Tasksequenzschritt an. Variable und Wert sind nur verfügbar, wenn der Schritt in der Tasksequenz ausgeführt wird. Sie sind nicht Teil der Gesamtsequenzumgebung, und auf sie kann nicht über andere Tasksequenzschritte in der Tasksequenz zugegriffen werden.<br /><br /> Eine Liste der integrierten Variablen und der zugehörigen Aktionen finden Sie unter [Tasksequenz-Aktionsvariablen](../understand/task-sequence-action-variables.md).|  
|Hinzufügen eines festgelegten Tasksequenzvariablenschritts in einer Tasksequenz|Bei dieser Methode geben Sie die Tasksequenzvariable und ihren Wert in der Tasksequenzumgebung an, wenn der Tasksequenzschritt als Teil einer Tasksequenz ausgeführt wird. Alle darauf folgenden Tasksequenzschritte können auf die Umgebungsvariable und ihren Wert zugreifen.|  
|Definieren einer sammlungsspezifischen Variablen|Bei dieser Methode geben Sie Tasksequenzvariablen und Werte für eine Sammlung von Computern an. Der Zugriff auf die Tasksequenzvariable und deren Werte ist von allen für die Sammlung vorgesehenen Tasksequenzen aus möglich.|  
|Definieren einer computerspezifischen Variablen|Bei dieser Methode geben Sie Tasksequenzvariablen und Werte für einen bestimmten Computer an. Der Zugriff auf die Tasksequenzvariable und deren Werte ist von allen für den Computer vorgesehenen Tasksequenzen aus möglich.|  
|Hinzufügen einer Tasksequenzvariablen auf der Seite **Anpassung** des Tasksequenzmedien-Assistenten|Bei dieser Methode geben Sie Tasksequenzvariablen und Werte für die Tasksequenz an, die von dem Medium ausgeführt wird, das auf die Tasksequenzvariable und seinen Wert zugreifen kann.|  

 Um den Standardwert für eine integrierte Tasksequenzvariable außer Kraft zu setzen, müssen Sie eine Tasksequenzvariable mit dem gleichen Namen wie die integrierte Tasksequenzvariable definieren. Eine Liste der integrierten Tasksequenzvariablen mit den ihnen zugeordneten Aktionen und ihrer Verwendung finden Sie unter[Integrierte Tasksequenzvariablen](../understand/task-sequence-built-in-variables.md).  

 Zum Löschen einer Tasksequenzvariablen aus der Tasksequenzumgebung stehen Ihnen die gleichen Methoden wie zum Erstellen einer Tasksequenzvariablen zur Verfügung. Zum Löschen einer Variablen aus der Tasksequenzumgebung legen Sie den Wert der Tasksequenzvariablen auf eine leere Zeichenfolge fest.  

 Sie können die Methoden kombinieren, um eine Umgebungstasksequenz-Variable auf verschiedene Werte für die gleiche Sequenz festzulegen. In einem erweiterten Szenario können Sie z. B. die Standardwerte für Schritte in einer Sequenz mit dem Tasksequenz-Editor festlegen und dann einen benutzerdefinierten Variablenwert mithilfe der verschiedenen Erstellungsmethoden festlegen. In der folgenden Liste werden die Regeln beschrieben, von denen bestimmt wird, welcher Wert beim Erstellen einer Tasksequenzvariablen anhand mehrerer Methoden verwendet wird.  

1.  Mit dem Schritt **Tasksequenzvariable festlegen** werden alle anderen Erstellungsmethoden außer Kraft gesetzt.  

2.  Computerspezifische Variablen haben Vorrang vor sammlungsspezifischen Variablen. Wenn Sie für eine computerspezifische Variable den gleichen Namen wie für eine sammlungsspezifische Variable angeben, wird bei der Ausführung der bereitgestellten Tasksequenz durch den Zielcomputer der Wert der computerspezifischen Variablen verwendet.  

3.  Tasksequenzen können von Medien ausgeführt werden. Verwenden Sie die Medienvariablen anstelle der sammlungs- bzw. computerspezifischen Variablen. Wenn die Tasksequenz von einem Medium ausgeführt wird, treffen die computer- und sammlungsspezifischen Variablen nicht zu und werden nicht verwendet. Stattdessen werden mithilfe der im Tasksequenzmedien-Assistenten auf der Seite **Anpassung** definierten Tasksequenzvariablen Werte speziell für eine von einem Medium ausgeführte Tasksequenz festgelegt  

4.  Wenn in der Gesamtsequenzumgebung kein Tasksequenzvariablen-Wert festgelegt ist, verwenden integrierte Aktionen den im Tasksequenz-Editor festgelegten Standardwert für den Schritt.  

 Neben dem Außerkraftsetzen von Werten für integrierte Tasksequenzschritt-Einstellungen können Sie auch eine neue Umgebungsvariable zur Verwendung in einem Tasksequenzschritt, einem Skript, einer Befehlszeile oder einer Bedingung erstellen. Wenn Sie einen Namen für eine neue Tasksequenzvariable angeben, beachten Sie Folgendes:  

-   Der von Ihnen für die Tasksequenzvariable angegebene Name kann Buchstaben, Ziffern, das Unterstrichzeichen (_) und einen Bindestrich (-) enthalten.  

-   Für Tasksequenzvariablen-Namen gelten eine Mindestlänge von 1 Zeichen und eine maximale Länge von 256 Zeichen.  

-   Benutzerdefinierte Variablen müssen mit einem Buchstaben (A - Z oder a - z) beginnen.  

-   Benutzerdefinierte Variablennamen dürfen nicht mit einem Unterstrich beginnen. Nur schreibgeschützte Tasksequenzvariablen beginnen mit dem Unterstrich.  

    > [!NOTE]  
    >  Schreibgeschützte Tasksequenzvariablen können von Tasksequenzschritten in einer Tasksequenz gelesen, aber nicht festgelegt werden. Sie können z.B. eine schreibgeschützte Tasksequenzvariable als Teil der Befehlszeile für die Tasksequenzaktionsvariable **Befehlszeile ausführen** verwenden, eine schreibgeschützte Variable aber nicht mit der Aktionsvariablen **Tasksequenzvariable festlegen** definieren.  

-   Bei Tasksequenzvariablen-Namen wird die Groß-/Kleinschreibung nicht beachtet. OSDVAR und osdvar stellen beispielsweise die gleiche Tasksequenzvariable dar.  

-   Tasksequenzvariablen-Namen dürfen nicht mit einem Leerzeichen beginnen oder enden und keine Leerzeichen enthalten. Leerzeichen am Beginn oder Ende des Namens einer Tasksequenzvariablen werden ignoriert.  

 In der folgenden Tabelle finden Sie Beispiele für gültige bzw. ungültige benutzerdefinierte Tasksequenzvariablen.  

|Beispiele für gültige benutzerdefinierte Variablennamen|Beispiele für ungültige benutzerdefinierte Variablennamen|  
|-------------------------------------------------------|----------------------------------------------------------|  
|MeineVariable|1Variable<br /><br /> Benutzerdefinierte Tasksequenzvariablen dürfen nicht mit einer Ziffer beginnen.|  
|Meine_Variable|MyV@riable<br /><br /> Benutzerdefinierte Tasksequenzvariablen dürfen nicht das Zeichen @ enthalten.|  
|Meine_Variable_2|_MeineVariable<br /><br /> Benutzerdefinierte Tasksequenzvariablen dürfen nicht mit einem Unterstrich beginnen.|  

 Allgemeine Beschränkungen für Tasksequenzvariablen:  

-   Tasksequenzvariablen-Werte dürfen 4.000 Zeichen nicht überschreiten.  

-   Schreibgeschützte Tasksequenzvariablen können weder erstellt noch außer Kraft gesetzt werden. Die Namen von schreibgeschützten Variablen beginnen mit einem Unterstrich (_). Sie können auf den Wert von schreibgeschützten Tasksequenzvariablen in einer Tasksequenz zugreifen, die zugeordneten Werte aber nicht ändern.  

-   Bei Tasksequenzvariablenwerte muss ggf. je nach Einsatz des Werts auf die Schreibweise (Groß-/Kleinschreibung) geachtet werden. In den meisten Fällen ist Groß-/Kleinschreibung die Tasksequenzvariablenwerte nicht relevant. Bei anderen Werten, z. B. solchen, die ein Kennwort enthalten, ist die Schreibweise von Bedeutung.  

-   Es gibt keine Beschränkung der Anzahl an Tasksequenzvariablen, die erstellt werden können. Die Anzahl der Variablen wird jedoch durch die Größe der Tasksequenzumgebung beschränkt. Die Beschränkung der Gesamtgröße für die Tasksequenzumgebung beträgt 32 MB.  

###  <a name="BKMK_TSEnvironmentVariables"></a> Zugriff auf Umgebungsvariablen  
 Sie können den Umgebungsvariablenwert in Tasksequenzen verwenden, nachdem Sie die Tasksequenzvariable und ihren Wert mithilfe einer der Methoden aus dem vorherigen Abschnitt angegeben haben. Sie können auf Standardwerte für integrierte Tasksequenzvariablen zugreifen, einen neuen Wert für eine integrierte Variable angeben oder eine benutzerdefinierte Tasksequenzvariable in einer Befehlszeile oder einem Skript verwenden.  

 In der folgenden Tabelle werden die Tasksequenzvorgänge angegeben, die durch Zugreifen auf die Tasksequenz-Umgebungsvariablen ausgeführt werden können.  

|Tasksequenzvorgang|Verwendung|  
|-----------------------------|-----------|  
|Konfigurieren von Aktionseinstellungen|Sie können angeben, dass eine Tasksequenzschritt-Einstellung über einen Variablenwert bereitgestellt werden soll, wenn die Sequenz ausgeführt wird.<br /><br /> Zum Bereitstellen einer Einstellung für einen Tasksequenzschritt mithilfe einer Umgebungsvariablen für eine Tasksequenz bearbeiten Sie den Schritt im Tasksequenz-Editor, und geben Sie den Variablennamen als Feldwert an. Der Variablenname muss in Prozentzeichen (%) eingeschlossen werden, um zu verdeutlichen, dass es sich hier um eine Umgebungsvariable handelt.|  
|Bereitstellen von Befehlszeilenargumenten|Sie können einen Teil oder die gesamte benutzerdefinierte Befehlszeile mithilfe eines Umgebungsvariablenwerts angeben.<br /><br /> Um eine Befehlszeileneinstellung mithilfe einer Umgebungsvariablen anzugeben, verwenden Sie den Variablennamen als Teil des Felds  **Befehlszeile** im Tasksequenzschritt **Befehlszeile ausführen**. Der Variablenname muss in Prozentzeichen (%) eingeschlossen werden.<br /><br /> Beispielsweise wird in der folgenden Befehlszeile eine integrierte Umgebungsvariable verwendet, um den Computernamen in die Datei C:\File.txt zu schreiben.<br /><br /> <br /><br /> **Cmd /C %_SMSTSMachineName% > C:\File.txt**|  
|Auswerten einer Schrittbedingung|Sie können integrierte oder benutzerdefinierte Tasksequenz-Umgebungsvariablen auch als Teil eines Tasksequenzschritts oder einer Gruppenbedingung verwenden. Der Umgebungsvariablenwert wird vor der Ausführung des Tasksequenzschritts oder der Gruppe ausgewertet.<br /><br /> Gehen Sie wie folgt vor, um eine Bedingung hinzuzufügen, mit der ein Variablenwert ausgewertet wird:<br /><br /> 1.  Wählen Sie den Schritt oder die Gruppe aus, dem bzw. der Sie die Bedingung hinzufügen möchten.<br />2.  Wählen Sie auf der Registerkarte**Optionen** für den Schritt oder die Gruppe in der Dropdownliste **Bedingung hinzufügen** die Option **Tasksequenzvariable** aus.<br />3.  Geben Sie im Dialogfeld **Tasksequenzvariable** den Namen der Variablen, die getestete Bedingung und den Wert der Variablen an.|  
|Bereitstellen von Informationen für ein benutzerdefiniertes Skript|Tasksequenzvariablen können während der Ausführung der Tasksequenz mithilfe des COM-Objekts „Microsoft.SMS.TSEnvironment“ gelesen und geschrieben werden.<br /><br /> Im folgenden Beispiel sehen Sie eine Visual Basic-Skriptdatei, mit der die Tasksequenzvariable **_SMSTSLogPath** nach dem aktuellen Protokollpfad abgefragt wird. Das Skript legt außerdem eine benutzerdefinierte Variable fest.<br /><br /> <br /><br /> **dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")**<br /><br /> <br /><br /> **dim logPath**<br /><br /> <br /><br /> **' Sie können die Umgebung abfragen, um eine vorhandene Variable zu erhalten.**<br /><br /> **logPath = env("_SMSTSLogPath")**<br /><br /> <br /><br /> **' Sie können auch eine Variable in der OSD-Umgebung festlegen.**<br /><br /> **env("MyCustomVariable") = "varname"**<br /><br /> <br /><br /> Weitere Informationen zur Verwendung von Tasksequenzvariablen in Skripts finden Sie in der SDK-Dokumentation.|  

###  <a name="BKMK_ComputerCollectionVariables"></a> Computer- und Sammlungsvariablen  
 Sie können Tasksequenzen so konfigurieren, dass sie auf mehreren Computern oder für mehrere Sammlungen gleichzeitig ausgeführt werden. Sie können eindeutige computer- oder sammlungsspezifische Informationen wie beispielsweise einen eindeutigen Product Key für das Betriebssystem angeben oder alle Mitglieder einer Sammlung einer bestimmten Domäne beitreten lassen.  

 Sie können Tasksequenzvariablen einem einzelnen Computer oder einer Sammlung zuweisen. Bei der Ausführung der Tasksequenz auf dem Zielcomputer oder für die Zielsammlung werden die angegebenen Werte auf den Zielcomputer bzw. die Zielsammlung angewendet.  

 Sie können Tasksequenzvariablen für einen einzelnen Computer oder eine Sammlung angeben. Bei der Ausführung der Tasksequenz auf dem Zielcomputer oder für die Zielsammlung werden die angegebenen Variablen der Umgebung hinzugefügt, und die Werte stehen allen Tasksequenzschritten der Tasksequenz zur Verfügung.  

> [!WARNING]  
>  Wenn Sie für eine sammlungsspezifische Variable und eine computerspezifische Variable den gleichen Variablennamen verwenden, hat der Wert der computerspezifischen Variablen Vorrang vor dem Wert der sammlungsspezifischen Variablen. Tasksequenzvariablen, die Sie Sammlungen zuweisen, haben Vorrang vor integrierten Tasksequenzvariablen.  

 Weitere Informationen zum Erstellen von Tasksequenzvariablen für Computer und Sammlungen finden Sie unter [Erstellen von Tasksequenzvariablen für Computer und Sammlungen](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTSVariables).  

###  <a name="BKMK_TSMediaVariables"></a> Tasksequenzmedien-Variablen  
 Sie können Tasksequenzvariablen für Tasksequenzen, die von Medien ausgeführt werden, angeben. Wenn Sie zur Bereitstellung des Betriebssystems Medien verwenden, fügen Sie die Tasksequenzvariablen hinzu und geben ihre Werte an, wenn Sie die Medien erstellen. Die Variablen und ihre Werte werden auf den Medien gespeichert.  

> [!NOTE]  
>  Tasksequenzen werden auf eigenständigen Medien gespeichert. Allerdings wird die Tasksequenz von allen anderen Medientypen, wie beispielsweise vorab bereitgestellten Medien, von einem Verwaltungspunkt abgerufen.  

 Sie können Tasksequenzvariablen auf der Seite **Anpassung** des Tasksequenzmedien-Assistenten angeben. Informationen zum Verwenden von Medien finden Sie unter [Erstellen von Tasksequenzmedien](../deploy-use/create-task-sequence-media.md).  

> [!TIP]  
>  Die Paket-ID und die Prestart-Befehlszeile einschließlich des Wertes vorhandener Tasksequenzvariablen werden von der Tasksequenz in die Protokolldatei „CreateTSMedia.log“ auf dem Computer geschrieben, auf dem die Configuration Manager-Konsole ausgeführt wird. Sie können diese Protokolldatei überprüfen, um den Wert für die Tasksequenzvariablen zu überprüfen.  

##  <a name="BKMK_TSCreate"></a> Erstellen einer Tasksequenz  
 Sie erstellen Tasksequenzen mithilfe des Tasksequenzerstellungs-Assistenten. Mit dem Assistenten können integrierte Sequenzen zur Ausführung bestimmter Tasks oder benutzerdefinierte Tasksequenzen zur Ausführung vieler verschiedener Tasks erstellt werden.  

 Beispielsweise können Sie Tasksequenzen erstellen, mit denen ein Betriebssystemabbild eines Referenzcomputers erstellt und erfasst oder ein vorhandenes Betriebssystemabbild auf einem Zielcomputer installiert wird. Sie können auch eine benutzerdefinierte Tasksequenz erstellen, mit der ein benutzerdefinierter Task ausgeführt wird. Sie können benutzerdefinierte Tasksequenzen verwenden, um spezielle Betriebssystembereitstellungen durchzuführen.  

 Weitere Informationen zum Erstellen von Tasksequenzen finden Sie im Abschnitt [Erstellen von Tasksequenzen](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

##  <a name="BKMK_TSEdit"></a> Bearbeiten einer Tasksequenz  
 Sie bearbeiten die Tasksequenz mithilfe des **Tasksequenz-Editors**. Mit dem Editor kann die Tasksequenz wie folgt geändert werden:  

-   Sie können der Tasksequenz Schritte hinzufügen bzw. Schritte daraus entfernen.  

-   Sie können die Reihenfolge der Tasksequenzschritte ändern.  

-   Sie können Gruppen von Schritten hinzufügen oder entfernen.  

-   Sie können angeben, ob die Tasksequenz fortgesetzt wird, wenn ein Fehler auftritt.  

-   Sie können den Schritten und Gruppen einer Tasksequenz Bedingungen hinzufügen.  

> [!IMPORTANT]  
>  Enthält die Tasksequenz aufgrund der Bearbeitung nicht zugeordnete Referenzen auf ein Paket oder ein Programm, müssen Sie die Referenz korrigieren, das nicht referenzierte Programm aus der Tasksequenz löschen oder den fehlerhaften Tasksequenzschritt vorübergehend deaktivieren, bis die fehlerhafte Referenz korrigiert oder entfernt wird.  

 Weitere Informationen zum Bearbeiten einer Tasksequenz finden Sie unter [Bearbeiten einer Tasksequenz](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

##  <a name="BKMK_TSDeploy"></a> Bereitstellen einer Tasksequenz  
 Sie können eine Tasksequenz auf Zielcomputern bereitstellen, die sich in einer beliebigen Configuration Manager-Sammlung befinden. Dazu gehört auch die Sammlung **Alle unbekannten Computer** , die zur Bereitstellung von Betriebssystemen auf unbekannten Computern verwendet wird. Es ist jedoch nicht möglich, eine Tasksequenz für Benutzersammlungen bereitzustellen.  

> [!IMPORTANT]  
>  Stellen Sie keine Tasksequenzen bereit, mit denen Betriebssysteme in ungeeigneten Sammlungen wie beispielsweise **Alle Systeme** installiert werden. Achten Sie darauf, dass die Sammlung, für die Sie die Tasksequenz bereitstellen, nur die Computer enthält, auf denen das Betriebssystem installiert werden soll. Um die Bereitstellung eines unerwünschten Betriebssystems zu verhindern, können Sie Bereitstellungseinstellungen verwalten. Weitere Informationen finden Sie unter [Einstellungen zum Verwalten risikoreicher Bereitstellungen](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

 Die Tasksequenz wird von jedem Zielcomputer, der die Tasksequenz erhält, den in der Bereitstellung angegebenen Einstellungen entsprechend ausgeführt. Die Tasksequenzen selbst enthalten keine zugeordneten Dateien oder Programme. Alle Dateien, auf die von einer Tasksequenz verwiesen wird, müssen sich bereits auf dem Zielcomputer oder auf einem Verteilungspunkt befinden, die für Clients zugänglich sind. Darüber hinaus werden von der Tasksequenz die Pakete installiert, auf die von Programmen verwiesen wird, selbst wenn das Programm oder Paket bereits auf dem Zielcomputer installiert ist.  

> [!NOTE]  
>  Wenn von der Tasksequenz eine Anwendung installiert wird, wird die Anwendung im Gegensatz zu Paketen und Programmen nur installiert, wenn die Anforderungsregeln für die Anwendung erfüllt sind und die Anwendung nicht bereits installiert ist. Ob dies der Fall ist, wird von der Erkennungsmethode festgestellt, die für die Anwendung angegeben wurde.  

 Der Configuration Manager-Client führt beim Herunterladen einer Clientrichtlinie eine Tasksequenzbereitstellung aus. Informationen zum Initiieren dieser Aktion, anstatt auf den nächsten Abfragezyklus zu warten, finden Sie unter [Initiieren des Richtlinienabrufs für einen Configuration Manager-Client](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Sie können beim Bereitstellen von Tasksequenzen für Windows Embedded-Geräte mit aktivierten Schreibfiltern angeben, ob der Schreibfilter auf dem Gerät während der Bereitstellung deaktiviert und das Gerät nach der Bereitstellung neu gestartet werden soll. Wenn der Schreibfilter nicht deaktiviert ist, wird die Tasksequenz auf einem temporären Overlay bereitgestellt und ist nach dem Neustart des Geräts nicht verfügbar.  

> [!NOTE]  
>  Stellen Sie beim Bereitstellen einer Tasksequenz auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist. So können Sie verwalten, wann der Schreibfilter deaktiviert bzw. aktiviert ist und wann das Gerät neu gestartet wird.  
>   
>  Wenn Tasksequenzen von Clients außerhalb eines Wartungsfensters heruntergeladen werden, wird die Tasksequenz zweimal heruntergeladen. In diesem Fall wird von Clients die Tasksequenz heruntergeladen, die Schreibfilter werden deaktiviert, und der Computer wird neu gestartet. Anschließend wird die Tasksequenz erneut heruntergeladen, da die Tasksequenz auf das temporäre Overlay heruntergeladen wurde, das beim Neustarten des Geräts gelöscht wird.  

 Weitere Informationen zum Bereitstellen von Tasksequenzen finden Sie unter [Bereitstellen einer Tasksequenz](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_TSExportImport"></a> Exportieren und Importieren von Tasksequenzen  
 Configuration Manager erlaubt das Exportieren und Importieren von Tasksequenzen. Wenn Sie eine Tasksequenz exportieren, können Sie die Objekte einschließen, auf die von der Tasksequenz verwiesen wird. Dazu gehören ein Betriebssystemabbild, ein Startabbild, ein Client-Agent-Paket, ein Treiberpaket und Anwendungen mit Abhängigkeiten.  

> [!NOTE]  
>  Der Export- und Importprozess für Tasksequenzen stimmt weitgehend mit dem Export- und Importprozess für Anwendungen in Configuration Manager überein.  

 Weitere Informationen zum Exportieren und Importieren von Tasksequenzen finden Sie im Abschnitt [Exportieren und Importieren von Tasksequenzen](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

##  <a name="BKMK_TSRun"></a> Ausführen einer Tasksequenz  
 Tanksequenzen werden standardmäßig stets über das lokale Systemkonto ausgeführt. Mithilfe des Befehlszeilenschritts für die Tasksequenz kann diese auch unter einem anderen Konto ausgeführt werden. Beim Ausführen der Tasksequenz wird zunächst vom Configuration Manager-Client nach referenzierten Paketen gesucht, bevor die Schritte der Tasksequenz gestartet werden. Wenn ein referenziertes Paket nicht überprüft wird oder nicht auf einem Verteilungspunkt verfügbar ist, wird für den zugehörigen Tasksequenzschritt ein Fehler zurückgegeben.  

 Wenn eine verteilte Tasksequenz zum Herunterladen und Ausführen konfiguriert ist, werden alle abhängigen Programme und Anwendungen in den Configuration Manager-Clientcache heruntergeladen. Die erforderlichen Pakete und Anwendungen werden von Verteilungspunkten abgerufen. Wenn nicht genügend Configuration Manager-Clientcache vorhanden ist oder das Paket bzw. die Anwendung nicht gefunden werden kann, tritt ein Fehler in der Tasksequenz auf, und eine Statusmeldung wird generiert. Sie können außerdem angeben, dass der Inhalt nur im Bedarfsfall vom Client heruntergeladen wird, wenn Sie die Option **Inhalt vom Verteilungspunkt herunterladen und lokal ausführen**auswählen. Alternativ können Sie mithilfe der Option **Programm vom Verteilungspunkt ausführen** angeben, dass die Dateien direkt vom Verteilungspunkt aus auf den Client heruntergeladen werden, ohne zunächst im Cache zwischengespeichert zu werden. Die Option **Programm vom Verteilungspunkt ausführen** ist nur verfügbar, wenn in den **Paket**eigenschaften der referenzierten Pakete auf der Registerkarte**Datenzugriff** das Kontrollkästchen **Den Inhalt in diesem Paket in eine Paketfreigabe auf Verteilungspunkten kopieren** aktiviert ist.  

 Wenn ein abhängiges Paket oder eine abhängige Anwendung vom Client mit der Tasksequenz nicht gefunden werden kann und die Bereitstellung als **Verfügbar** konfiguriert ist, wird vom Client sofort eine Fehlermeldung ausgegeben. Ist die Bereitstellung jedoch als **Erforderlich**konfiguriert, wird vom Configuration Manager-Client für den Fall, dass der Inhalt noch nicht an einen für den Client zugänglichen Verteilungspunkt repliziert wurde, so lange gewartet und erneut versucht, den Inhalt herunterzuladen, bis der Stichtag erreicht ist.  

 Nachdem eine Tasksequenz erfolgreich abgeschlossen oder fehlerhaft beendet wurde, wird von Configuration Manager ein entsprechender Eintrag im Configuration Manager-Clientverlauf vorgenommen. Nachdem eine Tasksequenz auf einem Computer initiiert wurde, können Sie diese weder abbrechen noch beenden.  

> [!IMPORTANT]  
>  Falls für einen Schritt der Tasksequenz ein Neustart des Clientcomputers erforderlich ist, muss für den Client das Starten über eine formatierte Festplattenpartition möglich sein. Andernfalls tritt für die Tasksequenz unabhängig davon ein Fehler auf, ob eine von der Tasksequenz angegebene Fehlerbehandlung vorhanden ist.  

 Wenn ein Update für ein abhängiges Objekt einer Tasksequenz ausgeführt wird, z. B. für ein Softwareverteilungspaket, wird auch automatisch für alle Tasksequenzen, von denen auf dieses Paket verwiesen wird, ein Update ausgeführt. Auf diese Weise wird stets auf die neueste Version verwiesen, unabhängig davon, wie viele Updates bereitgestellt wurden.  

> [!NOTE]  
>  Alle Tasksequenzen werden vom Configuration Manager-Client auf mögliche Abhängigkeiten und auf die Verfügbarkeit solcher Abhängigkeiten auf einem Verteilungspunkt überprüft, bevor eine Tasksequenz ausgeführt wird. Falls vom Client ein gelöschtes Objekt gefunden wird, von dem die Tasksequenz abhängig ist, wird ein Fehler generiert, und die Tasksequenz wird nicht ausgeführt.  

###  <a name="BKMK_RunProgram"></a> Ausführen eines Programms vor der Tasksequenzausführung  
 Sie können ein Programm auswählen, das vor der Tasksequenz ausgeführt wird. Öffnen Sie das Dialogfeld **Eigenschaften** für die Tasksequenz, und legen Sie auf der Registerkarte **Erweitert** die folgenden Optionen fest, um ein Programm anzugeben, das zuerst ausgeführt werden soll:  

> [!IMPORTANT]  
>  Zum Ausführen eines Programms vor Beginn der Tasksequenz muss der gesamte Inhalt für die Tasksequenz und das Programm auf einer Paketfreigabe für das Paket verfügbar sein. Sie konfigurieren die Paketfreigabe unter den Eigenschaften des Pakets auf der Registerkarte **Datenzugriff** .  

-   **Ein anderes Programm zuerst ausführen**: Geben Sie an, dass ein anderes Programm vor der Tasksequenz ausgeführt werden soll.  

    > [!IMPORTANT]  
    >  Diese Einstellung gilt nur für Tasksequenzen, die in der Vollversion des Betriebssystems ausgeführt werden. Diese Einstellung wird von Configuration Manager ignoriert, wenn die Tasksequenz mithilfe von PXE- oder Startmedien gestartet wird.  

-   **Paket**: Geben Sie das Paket an, das das Programm enthält.  

-   **Programm**: Geben Sie das auszuführende Programm an.  

-   **Dieses Programm immer zuerst ausführen**: Geben Sie an, dass dieses Programm von Configuration Manager jedes Mal ausgeführt werden soll, wenn die Tasksequenz auf dem gleichen Client ausgeführt wird. Standardmäßig wird das Programm nach seiner erfolgreichen Ausführung auch bei einer erneuten Ausführung der Tasksequenz auf dem gleichen Client nicht erneut ausgeführt.  

 Wenn das ausgewählte Programm auf einem Client nicht ausgeführt werden kann, wird die Tasksequenz nicht ausgeführt.  

##  <a name="BKMK_TSMaintenanceWindow"></a> Verwenden eines Wartungsfensters, um anzugeben, wann eine Tasksequenz ausgeführt werden kann  
 Sie können den Zeitpunkt der Ausführung einer Tasksequenz angeben, indem Sie ein Wartungsfenster für die Sammlung definieren, in dem die Zielcomputer enthalten sind. Wartungsfenster werden mit einem Startdatum, einer Start- und Endzeit sowie einem Wiederholungsmuster konfiguriert. Beim Festlegen des Zeitplans für das Wartungsfenster können Sie auch angeben, dass das Wartungsfenster nur für Tasksequenzen gelten soll. Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
>  Wenn Sie ein Wartungsfenster zum Ausführen einer Tasksequenz konfigurieren, wird die Tasksequenz auch nach dem Schließen des Wartungsfensters weiter ausgeführt. Die Tasksequenz wird entweder erfolgreich abgeschlossen, oder es tritt ein Fehler auf.  

##  <a name="BKMK_TSNetworkAccessAccount"></a> Tasksequenzen und das Netzwerkzugriffskonto  
 Obwohl Tasksequenzen im Kontext des lokalen Systemkontos ausgeführt werden, müssen Sie das Netzwerkzugriffskonto in folgenden Situationen möglicherweise konfigurieren:  

-   Sie müssen das Netzwerkzugriffskonto ordnungsgemäß konfigurieren. Andernfalls tritt ein Fehler in der Tasksequenz auf, wenn von dieser versucht wird, zum Abschließen des Tasks auf Configuration Manager-Pakete auf Verteilungspunkten zuzugreifen. Weitere Informationen zum Netzwerkzugriffskonto finden Sie unter [Netzwerkzugriffskonto](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#a-namebkmknaaa-network-access-account).  

    > [!NOTE]  
    >  Das Netzwerkzugriffskonto wird niemals als Sicherheitskontext für das Ausführen von Programmen, das Installieren von Anwendungen oder Updates oder das Ausführen von Tasksequenzen verwendet. Es wird jedoch zum Zugriff auf die zugehörigen Ressourcen im Netzwerk genutzt.  

-   Bei der Initiierung einer Betriebssystembereitstellung über ein Startimage verwendet Configuration Manager die Windows PE-Umgebung, die kein vollständiges Betriebssystem darstellt. Die Windows PE-Umgebung verwendet einen automatisch generierten zufälligen Namen, der keiner Domäne angehört. Wenn Sie das Netzwerkzugriffskonto nicht ordnungsgemäß konfigurieren, verfügt der Computer möglicherweise nicht über die Berechtigungen, die zum Zugriff auf die für den Abschluss der Tasksequenz benötigten Configuration Manager-Pakete erforderlich sind.  

##  <a name="BKMK_TSCreateMedia"></a> Erstellen von Medien für Tasksequenzen  
 Sie können Tasksequenzen und die damit verbundene Dateien und Abhängigkeiten auf verschiedene Medientypen schreiben. Hierzu gehören z. B. das Schreiben auf Wechselmedien, wie CDs, DVDs oder USB-Speichersticks für Erfassungsmedien, eigenständige oder startbare Medien, oder das Schreiben in eine WIM-Datei für vorab bereitgestellte Medien.  

 Sie können die folgenden Medientypen erstellen:  

-   **Erfassungsmedien**. Mithilfe von Erfassungsmedien wird ein Betriebssystemimage erfasst, das außerhalb der Configuration Manager-Infrastruktur konfiguriert und erstellt wurde. Erfassungsmedien können benutzerdefinierte Programme enthalten, die vor einer Tasksequenz ausgeführt werden können. Vom benutzerdefinierten Programm kann mit dem Desktop interagiert werden. Benutzer können zur Werteingabe aufgefordert werden, und die von der Tasksequenz verwendeten Variablen können erstellt werden.  

     Weitere Informationen finden Sie unter [Erstellen von Erfassungsmedien](../deploy-use/create-capture-media.md).  

-   **Eigenständige Medien**. Eigenständige Medien enthalten die Tasksequenz und alle zugeordneten Objekte, die für die Ausführung der Tasksequenz erforderlich sind. Tasksequenzen auf eigenständigen Medien können ausgeführt werden, wenn Configuration Manager keine oder nur begrenzte Verbindungen mit dem Netzwerk aufweist. Eigenständige Medien können auf folgende Arten ausgeführt werden:  

    -   Wenn der Zielcomputer nicht gestartet ist, wird das der Tasksequenz zugeordnete Windows PE-Image vom eigenständigen Medium aus verwendet und die Tasksequenz wird gestartet.  

    -   Das eigenständige Medium kann auch manuell gestartet werden, sofern ein Benutzer am Netzwerk angemeldet ist und die Installation initiiert.  

    > [!IMPORTANT]  
    >  Die Schritte einer Tasksequenz auf eigenständigen Medien müssen ohne jeglichen Datenabruf aus dem Netzwerk ausgeführt werden können, anderenfalls tritt bei dem Tasksequenzschritt, von dem ein Datenabruf versucht wird, ein Fehler auf. So würde z. B. ein Fehler bei einem Tasksequenzschritt auftreten, für den ein Paketabruf durch einen Verteilungspunkt erforderlich ist. Wenn sich das erforderliche Paket jedoch auf dem eigenständigen Medium befindet, kann der Tasksequenzschritt erfolgreich ausgeführt werden.  

     Weitere Informationen finden Sie unter [Erstellen eigenständiger Medien](../deploy-use/create-stand-alone-media.md).  

-   **Startbare Medien**. Startbare Medien enthalten die zum Starten eines Zielcomputers erforderlichen Dateien, sodass vom Zielcomputer eine Verbindung mit der Configuration Manager-Infrastruktur hergestellt und auf Grundlage seiner Sammlungsmitgliedschaft bestimmt werden kann, welche Tasksequenzen auszuführen sind. Die Tasksequenz und die abhängigen Objekte sind nicht auf dem Medium enthalten, können jedoch vom Configuration Manager-Client über das Netzwerk abgerufen werden. Diese Methode empfiehlt sich bei Bereitstellungen auf neuen Computern, auf Bare-Metal-Computern oder auf Zielcomputern ohne Configuration Manager-Client.  

     Weitere Informationen finden Sie unter [Erstellen startbarer Medien](../deploy-use/create-bootable-media.md).  

-   **Vorab bereitgestellte Medien**. Mithilfe vorab bereitgestellter Medien wird ein Betriebssystemabbild auf einem nicht bereitgestellten Zielcomputer bereitgestellt. Bei vorab bereitgestellten Medien handelt es sich um im WIM-Format (Windows Imaging Format) gespeicherte Dateien, die vom Hersteller auf einem Bare-Metal-Computer oder im Staging Center eines Unternehmens ohne Verbindung zur Configuration Manager-Umgebung installiert werden können.  

     Weitere Informationen finden Sie unter [Erstellen vorab bereitgestellter Medien](../deploy-use/create-prestaged-media.md).  

 Wenn Sie Medien erstellen, geben Sie ein Kennwort für diese an, um den Zugriff auf die in den Medien enthaltenen Dateien zu steuern. Wenn Sie ein Kennwort angeben, muss ein Benutzer am Zielcomputer anwesend sein, um das Kennwort beim Ausführen der Tasksequenz einzugeben.  

 Wenn Sie eine Tasksequenz mithilfe eines Mediums ausführen, wird die angegebene Computerchiparchitektur auf dem Medium nicht erkannt, und es wird versucht, die Tasksequenz zu starten, selbst wenn die Architektur nicht mit der des Zielcomputers übereinstimmt. Stimmt die Chiparchitektur auf dem Medium nicht mit der auf dem Bereitstellungszielcomputer installierten Chiparchitektur überein, tritt bei der Installation ein Fehler auf.  

 Weitere Informationen zur Betriebssystembereitstellung mithilfe von Medien finden Sie unter [Erstellen von Tasksequenzmedien](../deploy-use/create-task-sequence-media.md).  
