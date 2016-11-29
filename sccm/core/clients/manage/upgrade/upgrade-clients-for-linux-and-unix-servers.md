---
itle: Upgrade clients | Linux UNIX | System Center Configuration Manager
description: "Mettez à niveau un client sur un serveur Linux ou UNIX dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
caps.latest.revision: 6
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dda49b04914b53b56ed36a7bba8368d3c2387cde


---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Comment mettre à niveau les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez mettre à niveau la version du client pour Linux et UNIX vers une version plus récente du client sans désinstaller au préalable le client actuel. Pour cela, installez le nouveau package d’installation du client sur l’ordinateur en utilisant la propriété de ligne de commande **-keepdb** . Quand le client pour Linux et UNIX est installé, il remplace les données du client existantes par les nouveaux fichiers du client. Toutefois, la propriété de ligne de commande **-keepdb** demande au processus d’installation de conserver l’identificateur unique (GUID) du client, la base de données locale d’informations et le magasin de certificats. Ces informations sont ensuite utilisées par la nouvelle installation du client.  

 Par exemple, vous avez un ordinateur RHEL5 x64 qui exécute le client à partir de la version d’origine du client Configuration Manager pour Linux et UNIX. Pour mettre à niveau ce client vers la version du client disponible dans la mise à jour cumulative 1, vous exécutez manuellement le script **install** pour installer le package du client approprié à partir de la mise à jour cumulative 1, en ajoutant le commutateur de ligne de commande **-keepdb**. La ligne de commande que vous utilisez ressemble à ceci : **./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar**  

## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Comment utiliser un déploiement de logiciels pour mettre à niveau le client sur des serveurs Linux et UNIX  
 Vous pouvez utiliser un déploiement de logiciels pour mettre à niveau le client sur des serveurs Linux et UNIX vers une nouvelle version du client. Toutefois, le client System Center Configuration Manager ne peut pas exécuter directement le script d’installation pour installer le nouveau client, car l’installation d’un nouveau client doit d’abord désinstaller le client actuel. Sinon, le processus client Configuration Manager qui exécute le script d’installation se terminerait avant que l’installation du nouveau client ne commence. Pour pouvoir utiliser un déploiement de logiciels pour installer le nouveau client, vous devez planifier l’installation pour qu’elle commence plus tard et qu’elle soit exécutée par les fonctionnalités de planification intégrées du système d’exploitation.  

 Pour cela, utilisez un déploiement de logiciels pour d’abord copier les fichiers du nouveau package d’installation du client sur l’ordinateur client, puis déployez et exécutez un script destiné à planifier le processus d’installation du client. Le script utilise la commande **at** intégrée du système d’exploitation pour retarder son démarrage. Ensuite, quand le script s’exécute, son fonctionnement est géré par le système d’exploitation du client, et non par le client Configuration Manager sur l’ordinateur. Ainsi, la ligne de commande appelée par le script désinstalle d’abord le client Configuration Manager, puis installe le nouveau client, ce qui termine le processus de mise à niveau du client sur l’ordinateur UNIX ou Linux. Une fois la mise à niveau terminée, le client mis à niveau continue à être géré par Configuration Manager.  

 Utilisez la procédure suivante pour configurer un déploiement de logiciels destiné à mettre à niveau le client pour Linux et UNIX. Les étapes et exemples suivants mettent à niveau un ordinateur RHEL5 x64 qui exécute la version initiale du client vers la version du client disponible dans la mise à jour cumulative 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Pour utiliser un déploiement de logiciels destiné à mettre à niveau le client sur des serveurs Linux et UNIX  

1.  Copiez le fichier du nouveau package d’installation du client sur l’ordinateur qui exécute le client Configuration Manager que vous envisagez de mettre à niveau.  

     Par exemple, vous pouvez placer le package d’installation du client et le script d’installation de la mise à jour cumulative 1 dans l’emplacement suivant sur l’ordinateur client : **/tmp/PATCH**  

2.  Créez un script pour gérer la mise à niveau du client Configuration Manager, puis placez une copie de ce script dans le même dossier sur l’ordinateur client que les fichiers d’installation du client de l’étape 1.  

     Le script ne doit pas obligatoirement porter un nom spécifique, mais il doit contenir les lignes de commande nécessaires pour utiliser les fichiers d’installation du client à partir d’un dossier local sur l’ordinateur client et installer le package d’installation du client à l’aide de la propriété de ligne de commande **-keepdb** . Vous utilisez la propriété de ligne de commande **-keepdb** pour conserver l’identificateur unique du client actuel afin qu’il soit utilisé par le nouveau client que vous installez.  

     Par exemple, vous créez un script nommé **upgrade.sh** qui contient les lignes suivantes, puis vous le copiez dans le dossier **/tmp/PATCH** sur l’ordinateur client :  

    ```  
    #!/bin/sh  
    #  
    /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

    ```  

3.  Utilisez le déploiement de logiciels pour que chaque client utilise la commande **at** intégrée de l’ordinateur pour exécuter le script **upgrade.sh** avec un court délai avant l’exécution du script.  

     Par exemple, utilisez la ligne de commande suivante pour exécuter le script : **at -f /tmp/upgrade.sh -m now + 5 minutes**  

 Une fois que le client a correctement planifié l’exécution du script **upgrade.sh** , le client envoie un message d’état indiquant que le déploiement de logiciels s’est terminé avec succès. Toutefois, l’installation du client actuel est ensuite gérée par l’ordinateur, une fois le délai écoulé. Une fois la mise à niveau du client terminée, validez l’installation en consultant le fichier **/var/opt/microsoft/scxcm.log** sur l’ordinateur client. De plus, vous pouvez vérifier que le client est installé et qu’il communique avec le site en affichant les détails relatifs au client dans le nœud **Appareils** de l’espace de travail **Ressources et Conformité** dans la console Configuration Manager.  



<!--HONumber=Nov16_HO1-->


