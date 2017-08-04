---
title: Configurer la passerelle de gestion cloud | Microsoft Docs
description: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 05/01/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.translationtype: HT
ms.sourcegitcommit: afe0ecc4230733fa76e41bf08df5ccfb221da7c8
ms.openlocfilehash: df6e809aadd3d69275c137c92629ab8426bbdcb7
ms.contentlocale: fr-fr
ms.lasthandoff: 08/04/2017

---

# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurer la passerelle de gestion cloud pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Depuis la version 1610, le processus de configuration de la passerelle de gestion cloud dans Configuration Manager comprend les étapes suivantes :

## <a name="step-1-configure-required-certificates"></a>Étape 1 : configurer les certificats requis

## <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>Option 1 (recommandée) : utilisez le certificat d’authentification serveur provenant d’un fournisseur de certificats public et largement approuvé (comme VeriSign)

Lorsque vous utilisez cette méthode, les clients approuveront automatiquement le certificat, et vous n’avez pas besoin de créer vous-même un certificat SSL personnalisé.

1. Créez un enregistrement de nom canonique (CNAME) dans le service de nom de domaine (DNS) public de votre organisation afin de générer un alias pour le service de passerelle de gestion cloud avec un nom convivial qui sera utilisé dans le certificat public.
Par exemple, Contoso nomme son service de passerelle de gestion cloud **GraniteFalls** qui, dans Azure, sera **GraniteFalls.CloudApp.Net**. Dans l’espace de noms contoso.com du DNS public de Contoso, l’administrateur DNS crée un enregistrement CNAME pour **GraniteFalls.Contoso.com** pour le nom d’hôte réel, **GraniteFalls.CloudApp.net**.
2. Ensuite, demandez à un fournisseur public un certificat d’authentification serveur en utilisant le nom commun (CN) de l’alias CNAME.
Par exemple, Contoso utilise **GraniteFalls.Contoso.com** comme nom commun du certificat.
3. Créez le service de passerelle de gestion cloud dans la console Configuration Manager à l’aide de ce certificat.
    - Sur la page **Paramètres** de l’Assistant Création de la passerelle de gestion cloud, lorsque vous ajoutez le certificat de serveur pour ce service cloud (à partir du **fichier de certificat**), l’Assistant extrait le nom d’hôte du nom commun du certificat comme nom de service, puis l’ajoute à **cloudapp.net** (ou **usgovcloudapp.net** pour le cloud Azure US Government) en tant que nom de domaine complet du service pour créer le service dans Azure.
Par exemple, lors de la création de la passerelle de gestion cloud chez Contoso, le nom d’hôte **GraniteFalls** est extrait du nom commun du certificat afin de créer le service réel dans Azure en tant que **GraniteFalls.CloudApp.net**.

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>Option 2 : vous pouvez créer un certificat SSL personnalisé pour la passerelle de gestion cloud de la même façon que pour un point de distribution cloud

Vous pouvez créer un certificat SSL personnalisé pour la passerelle de gestion cloud de la même façon que vous le feriez pour un point de distribution cloud. Suivez les instructions pour le [déploiement du certificat de service pour les points de distribution cloud](/sccm/core/plan-design/network/example-deployment-of-pki-certificates), mais procédez différemment pour ce qui suit :

- Lorsque vous configurez le nouveau modèle de certificat, accordez les autorisations **Lecture** et **Inscription** au groupe de sécurité que vous configurez pour les serveurs Configuration Manager.
- Lors de la demande du certificat de serveur web personnalisé, donnez un nom de domaine complet au nom commun du certificat qui se termine par **cloudapp.net** pour utiliser la passerelle de gestion cloud sur le cloud public Azure ou par **usgovcloudapp.net** pour le cloud Secteur public Azure.


## <a name="step-2-export-the-client-certificates-root"></a>Étape 2 : Exporter la racine du certificat client

Le moyen le plus simple pour exporter la racine des certificats clients utilisés sur le réseau consiste à ouvrir un certificat client sur l’une des machines jointes au domaine qui en possède un, et de le copier.

> [!NOTE] 
>
> Des certificats clients sont nécessaires sur chaque ordinateur que vous voulez gérer avec la passerelle de gestion cloud et sur le serveur de système de site qui héberge le point de connexion de la passerelle de gestion cloud. Si vous devez ajouter un certificat client à l’une quelconque de ces machines, consultez [Déploiement du certificat client pour les ordinateurs Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

1.  Dans la fenêtre Exécuter, tapez **mmc** et appuyez sur Entrée.

2.  Dans le menu Fichier, choisissez **Ajouter/supprimer un composant logiciel enfichable...**.

3.  Dans la boîte de dialogue Ajouter ou supprimer des composants logiciels enfichables, choisissez **Certificats** > **Ajouter &gt;**  > **Compte d’ordinateur** > **Suivant** > **Ordinateur Local** > **Terminer**. 

4.  Accédez à **Certificats** &gt; **Personnel** &gt;**Certificats**.

5.  Double-cliquez sur le certificat pour l’authentification du client sur l’ordinateur, choisissez l’onglet Chemin d’accès de certification et double-cliquez sur l’autorité racine (en haut du chemin).

6.  Sous l’onglet Détails, choisissez **Copier dans un fichier...** .

7.  Terminez l’Assistant Exportation de certificat en utilisant le format de certificat par défaut. Notez le nom et l’emplacement du certificat racine que vous créez. Vous en aurez besoin pour configurer la passerelle de gestion cloud dans une [étape ultérieure](#step-4-set-up-cloud-management-gateway).

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Étape 3 : Charger le certificat de gestion dans Azure

Un certificat de gestion Azure est nécessaire pour que Configuration Manager puisse accéder à l’API Azure et configurer la passerelle de gestion cloud. Pour plus d’informations et des instructions sur la manière de charger un certificat de gestion, consultez les articles suivants dans la documentation Azure :

- [Vue d’ensemble des certificats pour Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Téléchargement d’un certificat de gestion API dans Azure Management](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Veillez à copier l’ID d’abonnement associé au certificat de gestion. Vous en aurez besoin pour configurer la passerelle de gestion cloud dans la console Configuration Manager à l’[étape suivante](#step-4-set-up-cloud-management-gateway).

### <a name="subordinate-ca-certificates-and-azure"></a>Certificats d’autorité de certification subordonnée et Azure

Si votre certificat est émis par une autorité de certification subordonnée et que votre infrastructure PKI d’entreprise n’est pas sur Internet, procédez comme suit pour charger le certificat sur Azure. 

1. Dans votre portail Azure, après avoir configuré une passerelle de gestion cloud, recherchez le service de passerelle de gestion cloud et accédez à l’onglet **Certificat**. Chargez vos certificats d’autorité de certification subordonnée ici. Si vous avez plusieurs certificats d’autorité de certification subordonnée, vous devez les charger tous. 
2. Une fois que le certificat est chargé, enregistrez son empreinte numérique. 
3. Ajoutez l’empreinte numérique à la base de données de site à l’aide de ce script :
    
```

    DIM serviceCName
    DIM subCAThumbprints

    ' Verify arguments
    IF WScript.Arguments.Count <> 2 THEN
    WScript.StdOut.WriteLine "Usage: CScript UpdateSubCAThumbprints.vbs <ServiceCName> <SubCA cert thumbprints, separated by ;>"
    WScript.Quit 1
    END IF

    'Get arguments
    serviceCName = WScript.Arguments.Item(0)
    subCAThumbprints = WScript.Arguments.Item(1)

    'Find SMS Provider
    WScript.StdOut.WriteLine "Searching for SMS Provider for local site..."
    SET objSMSNamespace = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms")
    SET results = objSMSNamespace.ExecQuery("SELECT * From SMS_ProviderLocation WHERE ProviderForLocalSite = true")

    'Process the results
    FOR EACH var in results
    siteCode = var.SiteCode
    NEXT

    IF siteCode = "" THEN
    WScript.StdOut.WriteLine "Failed to locate SMS provider."
    WScript.Quit 1
    END IF

    WScript.StdOut.WriteLine "SiteCode = " & siteCode 

    ' Connect to the SMS namespace
    SET objWMIService = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms\site_" & siteCode)

    'Get instance of SMS_AzureService
    DIM query
    query = "SELECT * From SMS_AzureService WHERE ServiceType = 'CloudProxyService' AND ServiceCName = '" & serviceCName & "'"
    WScript.StdOut.WriteLine "Run WQL query: " &  query
    SET objInstances = objWMIService.ExecQuery(query)

    IF IsNull(objInstances) OR (objInstances.Count = 0) THEN
    WScript.StdOut.WriteLine "Failed to get Azure_Service instance."
    WScript.Quit 1
    END IF

    FOR EACH var IN objInstances
    SET azService = var
    NEXT

    WScript.StdOut.WriteLine "Update [SubCACertThumbprint] to " & subCAThumbprints

    'Update SubCA cert thumbprints
    azService.Properties_.item("SubCACertThumbprint") = subCAThumbprints

    'Save data back to provider
    azService.Put_

    WScript.StdOut.WriteLine "[SubCACertThumbprint] is updated successfully."
```


## <a name="step-4-set-up-cloud-management-gateway"></a>Étape 4 : Configurer la passerelle de gestion cloud

>[!NOTE]
>Dans la version 1610, la passerelle de gestion cloud est une fonctionnalité en préversion. Pour savoir comment l’activer, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

1. Dans la console Configuration Manager, accédez à **Administration** > **Services cloud** > **Passerelle de gestion cloud**.
2. Choisissez **Créer une passerelle de gestion cloud**.

3. Dans l’Assistant Création d’une passerelle de gestion cloud, entrez votre ID d’abonnement Azure (copié à partir du portail de gestion Azure) et accédez au fichier de certificat que vous avez chargé comme certificat de gestion Azure. Choisissez **Suivant** et attendez quelques instants que la console se connecte à Azure.

4. Remplissez les détails supplémentaires dans l’Assistant :

    - Spécifiez le nom du service qui s’exécutera dans Azure. Le nom du service doit être composé de 3 à 24 caractères alphanumériques.

    - Choisissez la région Azure où vous voulez que le service s’exécute.

    - Spécifiez le nombre de machines virtuelles que vous voulez utiliser pour le service. La valeur par défaut est 1, mais vous pouvez exécuter jusqu’à 16 machines virtuelles pour le service.

    >[!NOTE]
    >Si vous utilisez un proxy Internet pour le point de connexion de passerelle de gestion cloud, vous devez augmenter le nombre de ports sur le proxy du nombre de machines virtuelles que vous utilisez, en commençant au port 10124.

    - Spécifiez la clé privée (fichier .pfx) que vous avez exportée à partir du certificat SSL personnalisé.

    - Spécifiez le certificat racine exporté à partir du certificat client.

    -   Spécifiez le même nom de domaine complet de service que vous avez utilisé lorsque vous avez créé le nouveau modèle de certificat. Vous devez spécifier un des suffixes suivants pour le nom du service de nom de domaine complet, en fonction du cloud Azure que vous utilisez :

    Cloud Azure | Préfixe de nom de domaine complet
    --------------|-------------
    Cloud (commercial) public | .cloudapp.net    
    Cloud Secteur public | .usgovcloudapp.net

  - Décochez la case à côté de **Vérifier la révocation des certificats clients** (sauf si vous publiez publiquement les informations de votre liste de révocation de certificats).

  - Choisissez **Suivant** quand vous avez terminé.

5. Si vous voulez surveiller le trafic de la passerelle de gestion cloud avec un seuil de 14 jours, cochez la case pour activer l’alerte de seuil. Ensuite, spécifiez le seuil et le pourcentage auquel déclencher les différents niveaux d’alerte. Choisissez **Suivant** quand vous avez terminé.

6. Vérifiez les paramètres, puis choisissez **Suivant**. Configuration Manager commence à configurer le service. Une fois l’Assistant fermé, 5 à 15 minutes sont nécessaires pour approvisionner complètement le service dans Azure. Vérifiez la colonne **État** de la passerelle de gestion cloud nouvellement configurée pour déterminer quand le service est prêt.

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>Étape 5 : Configurer le site principal pour l’authentification de certification de client

1. Dans la console Configuration Manager, accédez à **Administration** > **Configuration de site** > **Sites**.

2. Sélectionnez le site principal pour les clients que vous voulez gérer via la passerelle de gestion cloud, puis cliquez sur **Propriétés**.

3. Sous l’onglet Communications des ordinateurs clients de la feuille de propriétés du site principal, cochez la case **Utiliser le certificat client PKI (fonctionnalité d’authentification du client) lorsqu’il est disponible**.

4. Veillez à décocher la case **Les clients vérifient la liste de révocation des certificats (CRL) pour les systèmes de site**. Cette option serait nécessaire seulement si vous publiiez publiquement votre liste de révocation de certificats.


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>Étape 6 : Ajouter le point de connexion de passerelle de gestion cloud

Le point de connexion de passerelle de gestion cloud est un nouveau rôle de système de site pour communiquer avec la passerelle de gestion cloud. Pour ajouter le point de connexion de passerelle de gestion cloud, suivez les instructions de la rubrique [Ajouter des rôles de système de site pour System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles).

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>Étape 7 : Configurer des rôles pour le trafic de la passerelle de gestion cloud

La dernière étape de la configuration de la passerelle de gestion cloud consiste à configurer les rôles de système de site pour qu’ils acceptent le trafic de la passerelle de gestion cloud. Pour la version d’évaluation technique 1606, seuls les rôles de point de gestion, de point de distribution et de point de mise à jour logicielle sont pris en charge pour la passerelle de gestion cloud. Vous devez configurer chaque rôle séparément.

1. Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Serveurs et rôles de système de site**.

2. Choisissez le serveur de système de site pour le rôle que vous voulez configurer pour le trafic de la passerelle de gestion cloud.

3. Choisissez le rôle puis **Propriétés**.

4. Dans la feuille de propriétés du rôle, sous Connexions client, choisissez **HTTPS**, cochez la case à côté de **Autoriser le trafic de la passerelle de gestion cloud de Configuration Manager**, puis cliquez sur **OK**. Répétez ces étapes pour les autres rôles.

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>Étape 8 : Configurer des clients pour la passerelle de gestion cloud

Une fois que la passerelle de gestion cloud et les rôles de système de site sont entièrement configurés et en cours d’exécution, les clients obtiennent l’emplacement du service de passerelle de gestion cloud automatiquement lors la demande d’emplacement suivante. Les clients doivent être sur le réseau d’entreprise pour recevoir l’emplacement du service de passerelle de gestion cloud. Le cycle d’interrogation pour les demandes d’emplacement est de 24 heures. Si vous ne souhaitez pas attendre la demande d’emplacement normalement planifiée, vous pouvez forcer la demande en redémarrant le service hôte de l’agent SMS (ccmexec.exe) sur l’ordinateur.

Avec l’emplacement du service de passerelle de gestion cloud configuré sur le client, il peut déterminer automatiquement si elle est sur l’intranet ou sur Internet. Si le client peut contacter le contrôleur de domaine ou le point de gestion local, il l’utilise pour communiquer avec Configuration Manager. Dans le cas contraire, il considère qu’elle est sur Internet et utilise l’emplacement du service de passerelle de gestion cloud pour communiquer.

>[!NOTE]
> Vous pouvez forcer le client à toujours utiliser la passerelle de gestion cloud, qu’elle soit sur l’intranet ou sur Internet. Pour ce faire, vous définissez la clé de Registre suivante sur l’ordinateur client : \
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

Pour vérifier que les clients peuvent contacter Configuration Manager, vous pouvez exécuter la commande PowerShell suivante sur l’ordinateur client :

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

Cette commande affiche les points de gestion que le client peut contacter, notamment le service de passerelle de gestion cloud.

## <a name="next-steps"></a>Étapes suivantes

[Surveiller les clients pour la passerelle de gestion cloud](monitor-clients-cloud-management-gateway.md)

