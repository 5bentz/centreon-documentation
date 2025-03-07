---
id: hardware-devices-pexip-infinity-managementapi
title: Pexip Infinity ManagementAPI
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Vue d'ensemble

Pexip Infinity est une application d’entreprise dans le Cloud qui permet la compatibilité de vidéoconférence et de visoconférence d’entreprise 
à toutes les plates-formes de collaboration. Le logiciel fonctionne comme une passerelle entre les plates-formes et connecte de manière transparente 
les solutions de communication et de collaboration d’entreprise dans les salles de réunion virtuelles.

Pexip Infinity comprend une API de gestion qui permet à des tiers de contrôler, de configurer et d'obtenir des informations sur l'état de la plate-forme Pexip Infinity.

## Contenu du connecteur de supervision

### Objets supervisés

* Alarmes
* Conférences

### Métriques collectées

Vous pouvez vous renseigner en détails sur les métriques présentées ci-après sur la documentation officielle 
de Pexip Infinity ManagementAPI : https://docs.pexip.com/api_manage/management_intro.htm

<Tabs groupId="sync">
<TabItem value="Alarms" label="Alarms">

| Metric name                                | Description                         | Unit  |
| :----------------------------------------- | :-----------------------------------| :---- |
| status                                     | Alarms status                       |       |
| alerts.problems.current.count              | Number of  current alerts problems  | count |

</TabItem>
<TabItem value="Conferences" label="Conferences">

| Metric name                                 | Description                                                                            | Unit  |
| :------------------------------------------ | :------------------------------------------------------------------------------------- | :---- |
| conferences.total.count                     | Total number of conferences                                                            | count |
| participants.total.count                    | Total number of participants			                                               | count |
| participants.callquality.$state.count       | Number of states participants callquality ('good', 'ok', 'bad', 'terrible', 'unknown') | count |

</TabItem>
</Tabs>

## Prérequis

Tous les accès à l'API de gestion sont effectués via HTTPS.
Si vous n'utilisez pas de base de données LDAP pour l'authentification, l'accès se fait via les informations d'identification de l'utilisateur administrateur Web. 
Le nom d'utilisateur par défaut de ce compte est *admin*.
Si vous utilisez une base de données LDAP, il est recommandé de créer un compte spécifiquement à l'usage de l'API.

Plus d'informations sont disponible sur la documentation officielle de Pexip Infinity ManagementAPI : https://docs.pexip.com/admin/integrate_api.htm

## Installation

<Tabs groupId="sync">
<TabItem value="Online License" label="Online License">

1. Installer le Plugin sur tous les collecteurs Centreon supervisant des ressources Pexip Infinity ManagementAPI :

```bash
yum install centreon-plugin-Hardware-Devices-Pexip-Infinity-Managementapi.noarch
```

2. Sur l'interface Web de Centreon, installer le connecteur de supervision *Pexip Infinity ManagementAPI* depuis la page **Configuration > Gestionnaire de connecteurs de supervision**

</TabItem>
<TabItem value="Offline License" label="Offline License">

1. Installer le Plugin sur tous les collecteurs Centreon supervisant des ressources Pexip Infinity ManagementAPI :

```bash
yum install centreon-plugin-Hardware-Devices-Pexip-Infinity-Managementapi.noarch
```

2. Sur le serveur Central Centreon, installer le connecteur de supervision via le RPM:

```bash
yum install centreon-pack-hardware-devices-pexip-infinity-managementapi.noarch
```

3. Sur l'interface Web de Centreon, installer le connecteur de supervision *Pexip Infinity ManagementAPI* depuis la page **Configuration > Gestionnaire de connecteurs de supervision**

</TabItem>
</Tabs>

## Configuration

Ce connecteur de supervision est conçu de manière à avoir dans Centreon un hôte par environnement Pexip Infinity ManagementAPI
Lorsque vous ajoutez un hôte à Centreon, appliquez-lui le modèle *HW-Device-Pexip-Infinity-Managementapi-custom*.
Une fois celui-ci configuré, certaines macros doivent être renseignées:

| Mandatory | Name            | Description                                                                |
| :-------- | :-------------- | :------------------------------------------------------------------------- |
| X         | APIPORT         | Port used (Default: 443)                                                   |
| X         | APIPROTO        | Specify https if needed (Default: 'https')                                 |
| X         | APIKUSERNAME    | Pexip Infinity ManagementAPI username                                      |
| X         | APIPASSWORD     | Pexip Infinity ManagementAPI password     	                               |
|           | APIEXTRAOPTIONS | Any extra option you may want to add to the command (eg. a --verbose flag) |

## FAQ

### Comment puis-je tester le Plugin et que signifient les options des commandes ?

Une fois le Plugin installé, vous pouvez tester celui-ci directement en ligne de commande depuis votre collecteur Centreon avec l'utilisateur *centreon-engine*
(Les paramètres tels que ```api-username``` ou ```api-password``` doivront être ajustés):

```bash
/usr/lib/centreon/plugins/centreon_pexip_infinity_managementapi.pl \
    --plugin=hardware::devices::pexip::infinity::managementapi::plugin \
    --mode=alarms \
    --hostname='mypexipinfnitapi.com' \
    --port='443' \
    --proto='https' \
    --api-username='myapiusername' \
    --api-password='myapipassword' \
    --filter-name='mycall1.centreon.com' \
    --warning-status='%\{level\} =~ /warning|minor/i' \
    --critical-status='%\{level\} =~ /critical|major|error/i' \
    --verbose
```

La commande ci-dessus contrôle le statut d'une alarme de l'application Pexip Infinity via Managementapi (```--mode=alarms```) nommée *mycall1.centreon.com* (```--filter-name='mycall1.centreon.com'```). 
Le Plugin utilise l'api-username (```--api-username='myapiusername'```), l'api-password (```--api-password='myapipassword'```)
et il se connecte à l'hôte _mypexipinfnitapi.com_ (```--hostname='mypexipinfnitapi.com'```) sur le port _443_ (```--port='443'```) utilisant le protocol _https_ (```--proto='https'```).

Cette commande déclenchera une alarme WARNING i le statut retourné de l'alarme est égale de */warning|minor/i* (```--warning-status='%{level} =~ /warning|minor/i'```)
et une alarme CRITICAL si l'alarme est égale de */critical|major|error/i* (```--critical-status='%{level} =~ /critical|major|error/i'```).

Toutes les options et leur utilisation peuvent être consultées avec le paramètre ```--help``` ajouté à la commande:

```bash
/usr/lib/centreon/plugins//centreon_pexip_infinity_managementapi.pl --plugin=hardware::devices::pexip::infinity::managementapi::plugin \
    --mode=alarms \
    --help
```

### J'obtiens le message d'erreur suivant: 

#### ```UNKNOWN: 500 Can't connect to mypexipinfnitapi.com:443 |```

Lors du déploiement de mes contrôles, j'obtiens le message suivant ```UNKNOWN: 500 Can't connect to mypexipinfnitapi.com:443 |```.
Cela signifie que Centreon n'a pas réussi à se connecter à Pexip Infinity ManagementAPI (*mypexipinfnitapi.com*).
La plupart du temps, il faut préciser le proxy à utiliser pour requêter l'URL *mypexipinfnitapi.com* en utilisant l'option ```--proxyurl='http://proxy.mycompany:8080'```.

#### ```UNKNOWN: 501 Protocol scheme 'connect' is not supported |``` 

Suite à la mise en place du proxy, j'obtiens le message suivant ```UNKNOWN: 501 Protocol scheme 'connect' is not supported |```
Cela signifie que le protocole de connexion au proxy n'est pas supporté par la libraire *LWP* utlisée par défaut par le Plugin Centreon.
Cette erreur peut être résolue en utilisant le backend HTTP *curl*. Pour ce faire, ajoutez l'option ```--http-backend='curl'``` à la commande.

#### ```UNKNOWN: Cannot load module 'Net::Curl::Easy'```

Ce message d'erreur indique qu'une librairie Perl est maquante pour utiliser le backend *curl*.

Pour corriger ce problème, installer la librairie Perl Net::Curl::Easy à l'aide de la commande suivante :

```bash
yum install perl-Net-Curl
```
