---
id: applications-pfsense-fauxapi
title: Pfsense Fauxapi
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Vue d'ensemble


## Contenu du pack

### Modèles

Le connecteur de supervision **pfSense Fauxapi** apporte un modèle d'hôte :

* **App-Pfsense-Fauxapi-custom**

Le connecteur apporte les modèles de service suivants
(classés selon le modèle d'hôte auquel ils sont rattachés) :

<Tabs groupId="sync">
<TabItem value="App-Pfsense-Fauxapi-custom" label="App-Pfsense-Fauxapi-custom">

| Alias        | Modèle de service                       | Description                                              |
|:-------------|:----------------------------------------|:---------------------------------------------------------|
| Backup-Files | App-Pfsense-Backup-Files-Fauxapi-custom | Contrôle les sauvegardes de fichiers Pfsense via Fauxapi |
| Gateways     | App-Pfsense-Gateways-Fauxapi-custom     | Contrôle les Gateways Pfsense via Fauxapi                |
| Rules        | App-Pfsense-Rules-Fauxapi-custom        | Contrôle les règles Pfsense via Fauxapi                  |
| System       | App-Pfsense-System-Fauxapi-custom       | Contrôle le status du système Pfsense via Fauxapi        |

> Les services listés ci-dessus sont créés automatiquement lorsque le modèle d'hôte **App-Pfsense-Fauxapi-custom** est utilisé.

</TabItem>
</Tabs>

### Métriques & statuts collectés

Voici le tableau des services pour ce connecteur, détaillant les métriques rattachées à chaque service.

<Tabs groupId="sync">
<TabItem value="Backup-Files" label="Backup-Files">

| Métrique                  | Unité |
|:--------------------------|:------|
| backups.total.count       | count |
| backups.time.last.seconds | ms    |

</TabItem>
<TabItem value="Gateways" label="Gateways">

| Métrique                                       | Unité |
|:-----------------------------------------------|:------|
| *gateways*#status                              | N/A   |
| *gateways*#gateway.packets.delay.milliseconds  | ms    |
| *gateways*#gateway.packets.loss.percentage     | %     |
| *gateways*#gateway.packets.stddev.milliseconds | ms    |

</TabItem>
<TabItem value="Rules" label="Rules">

| Métrique                           | Unité |
|:-----------------------------------|:------|
| rules.total.count                  | count |
| *rules*#rule.traffic.bitspersecond | b/s   |

</TabItem>
<TabItem value="System" label="System">

| Métrique                                | Unité |
|:----------------------------------------|:------|
| system.connections.tcp.usage.count      | count |
| system.connections.tcp.usage.percentage | %     |
| system.temperature.celsius              | C     |

</TabItem>
</Tabs>

## Prérequis

Un compte de service est requis pour interroger le Fauxapi Pfsense. Celui-ci doit avoir suffisamment de privilèges en lecture dans l'environnement.
Au niveau des droits API, votre fichier de configuration doit contenir au minimum :

* config_backup_list
* gateway_status
* rule_get
* system_stats

Plus d'informations sont disponible sur la documentation officielle de Pfsense Fauxpi documentation : https://github.com/ndejong/pfsense_fauxapi/blob/master/README.md

## Installer le connecteur de supervision

### Pack

1. Si la plateforme est configurée avec une licence *online*, l'installation d'un paquet
n'est pas requise pour voir apparaître le connecteur dans le menu **Configuration > Gestionnaire de connecteurs de supervision**.
Au contraire, si la plateforme utilise une licence *offline*, installez le paquet
sur le **serveur central** via la commande correspondant au gestionnaire de paquets
associé à sa distribution :

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-applications-pfsense-fauxapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-applications-pfsense-fauxapi
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-pack-applications-pfsense-fauxapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-applications-pfsense-fauxapi
```

</TabItem>
</Tabs>

2. Quel que soit le type de la licence (*online* ou *offline*), installez le connecteur **pfSense Fauxapi**
depuis l'interface web et le menu **Configuration > Gestionnaire de connecteurs de supervision**.

### Plugin

À partir de Centreon 22.04, il est possible de demander le déploiement automatique
du plugin lors de l'utilisation d'un connecteur. Si cette fonctionnalité est activée, et
que vous ne souhaitez pas découvrir des éléments pour la première fois, alors cette
étape n'est pas requise.

> Plus d'informations dans la section [Installer le plugin](/docs/monitoring/pluginpacks/#installer-le-plugin).

Utilisez les commandes ci-dessous en fonction du gestionnaire de paquets de votre système d'exploitation :

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Applications-Pfsense-Fauxapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Applications-Pfsense-Fauxapi
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-plugin-applications-pfsense-fauxapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Applications-Pfsense-Fauxapi
```

</TabItem>
</Tabs>

## Utiliser le connecteur de supervision

### Utiliser un modèle d'hôte issu du connecteur

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Complétez les champs **Nom**, **Alias** & **IP Address/DNS** correspondant à votre ressource.
3. Appliquez le modèle d'hôte **App-Pfsense-Fauxapi-custom**. Une liste de macros apparaît. Les macros vous permettent de définir comment le connecteur se connectera à la ressource, ainsi que de personnaliser le comportement du connecteur.
4. Renseignez les macros désirées. Attention, certaines macros sont obligatoires.

| Macro           | Description                                                                                          | Valeur par défaut | Obligatoire |
|:----------------|:-----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| APIPROTO        | Specify https if needed (default: 'https')                                                           | https             |             |
| APIPORT         | Port used (default: 443)                                                                             | 443               |             |
| APIKEY          | API key                                                                                              |                   | X           |
| APISECRET       | API secret                                                                                           |                   | X           |
| APIEXTRAOPTIONS | Any extra option you may want to add to every command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

5. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). L'hôte apparaît dans la liste des hôtes supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails de l'hôte : celle-ci montre les valeurs des macros.

### Utiliser un modèle de service issu du connecteur

1. Si vous avez utilisé un modèle d'hôte et coché la case **Créer aussi les services liés aux modèles**, les services associés au modèle ont été créés automatiquement, avec les modèles de services correspondants. Sinon, [créez les services désirés manuellement](/docs/monitoring/basic-objects/services) et appliquez-leur un modèle de service.
2. Renseignez les macros désirées (par exemple, ajustez les seuils d'alerte). Les macros indiquées ci-dessous comme requises (**Obligatoire**) doivent être renseignées.

<Tabs groupId="sync">
<TabItem value="Backup-Files" label="Backup-Files">

| Macro            | Description                                                                                        | Valeur par défaut | Obligatoire |
|:-----------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERCOUNTERS   | Only display some counters (regexp can be used). Example: --filter-counters='total'                |                   |             |
| WARNINGTIMELAST  | Thresholds                                                                                         |                   |             |
| CRITICALTIMELAST | Thresholds                                                                                         |                   |             |
| WARNINGTOTAL     | Thresholds                                                                                         |                   |             |
| CRITICALTOTAL    | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS     | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

</TabItem>
<TabItem value="Gateways" label="Gateways">

| Macro                 | Description                                                                                                                                                | Valeur par défaut    | Obligatoire |
|:----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------|:-----------:|
| FILTERCOUNTERS        | Only display some counters (regexp can be used). Example: --filter-counters='status'                                                                       |                      |             |
| FILTERNAME            | Filter gateway name (can be a regexp)                                                                                                                      |                      |             |
| WARNINGPACKETSDELAY   | Thresholds                                                                                                                                                 |                      |             |
| CRITICALPACKETSDELAY  | Thresholds                                                                                                                                                 |                      |             |
| WARNINGPACKETSLOSS    | Thresholds                                                                                                                                                 |                      |             |
| CRITICALPACKETSLOSS   | Thresholds                                                                                                                                                 |                      |             |
| WARNINGPACKETSSTDDEV  | Thresholds                                                                                                                                                 |                      |             |
| CRITICALPACKETSSTDDEV | Thresholds                                                                                                                                                 |                      |             |
| CRITICALSTATUS        | Define the conditions to match for the status to be CRITICAL (default: '%\{status\} !~ /none/i'). You can use the following variables: %\{status\}, %\{display\} | %\{status\} !~ /none/i |             |
| WARNINGSTATUS         | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{status\}, %\{display\}                      |                      |             |
| EXTRAOPTIONS          | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                         |                      |             |

</TabItem>
<TabItem value="Rules" label="Rules">

| Macro           | Description                                                                                        | Valeur par défaut | Obligatoire |
|:----------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERCOUNTERS  | Only display some counters (regexp can be used). Example: --filter-counters='traffic'              |                   |             |
| FILTERNAME      | Filter rule name (can be a regexp)                                                                 |                   |             |
| WARNINGTRAFFIC  | Thresholds                                                                                         |                   |             |
| CRITICALTRAFFIC | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS    | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

</TabItem>
<TabItem value="System" label="System">

| Macro                           | Description                                                                                        | Valeur par défaut | Obligatoire |
|:--------------------------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERCOUNTERS                  | Only display some counters (regexp can be used). Example: --filter-counters='temperature'          |                   |             |
| WARNINGCONNECTIONSTCPUSAGE      | Thresholds                                                                                         |                   |             |
| CRITICALCONNECTIONSTCPUSAGE     | Thresholds                                                                                         |                   |             |
| WARNINGCONNECTIONSTCPUSAGEPRCT  | Thresholds                                                                                         |                   |             |
| CRITICALCONNECTIONSTCPUSAGEPRCT | Thresholds                                                                                         |                   |             |
| WARNINGTEMPERATURE              | Thresholds                                                                                         |                   |             |
| CRITICALTEMPERATURE             | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS                    | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

</TabItem>
</Tabs>

3. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). Le service apparaît dans la liste des services supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails du service : celle-ci montre les valeurs des macros.

## Comment puis-je tester le plugin et que signifient les options des commandes ?

Une fois le plugin installé, vous pouvez tester celui-ci directement en ligne
de commande depuis votre collecteur Centreon en vous connectant avec
l'utilisateur **centreon-engine** (`su - centreon-engine`). Vous pouvez tester
que le connecteur arrive bien à superviser une ressource en utilisant une commande
telle que celle-ci (remplacez les valeurs d'exemple par les vôtres) :

```bash
/usr/lib/centreon/plugins/centreon_pfsense_fauxapi.pl \
	--plugin=apps::pfsense::fauxapi::plugin \
	--mode=rules \
	--hostname='10.0.0.1' \
	--port='443' \
	--proto='https' \
	--api-key='myapikey' \
	--api-secret='myapisecret'  \
	--filter-counters='' \
	--filter-name='' \
	--warning-traffic='' \
	--critical-traffic=''
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK: number of rules: 30 All rules are ok | 'rules.total.count'=30;;;0;'*rules*#rule.traffic.bitspersecond'=10b/s;;;0;
```

### Diagnostic des erreurs communes

Rendez-vous sur la [documentation dédiée](../getting-started/how-to-guides/troubleshooting-plugins.md#http-and-api-checks)
des plugins basés sur HTTP/API.

### Modes disponibles

Dans la plupart des cas, un mode correspond à un modèle de service. Le mode est renseigné dans la commande d'exécution
du connecteur. Dans l'interface de Centreon, il n'est pas nécessaire de les spécifier explicitement, leur utilisation est
implicite dès lors que vous utilisez un modèle de service. En revanche, vous devrez spécifier le mode correspondant à ce
modèle si vous voulez tester la commande d'exécution du connecteur dans votre terminal.

Tous les modes disponibles peuvent être affichés en ajoutant le paramètre
`--list-mode` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_pfsense_fauxapi.pl \
	--plugin=apps::pfsense::fauxapi::plugin \
	--list-mode
```

Le plugin apporte les modes suivants :

| Mode                                                                                                                          | Modèle de service associé               |
|:------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------|
| backup-files [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/pfsense/fauxapi/mode/backupfiles.pm)] | App-Pfsense-Backup-Files-Fauxapi-custom |
| gateways [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/pfsense/fauxapi/mode/gateways.pm)]        | App-Pfsense-Gateways-Fauxapi-custom     |
| rules [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/pfsense/fauxapi/mode/rules.pm)]              | App-Pfsense-Rules-Fauxapi-custom        |
| system [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/pfsense/fauxapi/mode/system.pm)]            | App-Pfsense-System-Fauxapi-custom       |

### Options disponibles

#### Options génériques

Les options génériques sont listées ci-dessous :

| Option                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|:-------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --mode                                     | Define the mode in which you want the plugin to be executed (see--list-mode).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --dyn-mode                                 | Specify a mode with the module's path (advanced).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --list-mode                                | List all available modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --mode-version                             | Check minimal version of mode. If not, unknown error.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --version                                  | Return the version of the plugin.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --custommode                               | When a plugin offers several ways (CLI, library, etc.) to get information the desired one must be defined with this option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --list-custommode                          | List all available custom modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --multiple                                 | Multiple custom mode objects. This may be required by some specific modes (advanced).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --pass-manager                             | Define the password manager you want to use. Supported managers are: environment, file, keepass, hashicorpvault and teampass.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --verbose                                  | Display extended status information (long output).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --debug                                    | Display debug messages.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --filter-perfdata                          | Filter perfdata that match the regexp. Example: adding --filter-perfdata='avg' will remove all metrics that do not contain 'avg' from performance data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --filter-perfdata-adv                      | Filter perfdata based on a "if" condition using the following variables: label, value, unit, warning, critical, min, max. Variables must be written either %\{variable\} or %(variable). Example: adding --filter-perfdata-adv='not (%(value) == 0 and %(max) eq "")' will remove all metrics whose value equals 0 and that don't have a maximum value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --explode-perfdata-max                     | Create a new metric for each metric that comes with a maximum limit. The new metric will be named identically with a '\_max' suffix). Example: it will split 'used\_prct'=26.93%;0:80;0:90;0;100 into 'used\_prct'=26.93%;0:80;0:90;0;100 'used\_prct\_max'=100%;;;;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --change-perfdata --extend-perfdata        | Change or extend perfdata. Syntax: --extend-perfdata=searchlabel,newlabel,target\[,\[newuom\],\[min\],\[m ax\]\]  Common examples:      Convert storage free perfdata into used:     --change-perfdata='free,used,invert()'      Convert storage free perfdata into used:     --change-perfdata='used,free,invert()'      Scale traffic values automatically:     --change-perfdata='traffic,,scale(auto)'      Scale traffic values in Mbps:     --change-perfdata='traffic\_in,,scale(Mbps),mbps'      Change traffic values in percent:     --change-perfdata='traffic\_in,,percent()'                                                                                                                                                                                                                                                                                                                                                                |
| --extend-perfdata-group                    | Add new aggregated metrics (min, max, average or sum) for groups of metrics defined by a regex match on the metrics' names. Syntax: --extend-perfdata-group=regex,namesofnewmetrics,calculation\[,\[ne wuom\],\[min\],\[max\]\] regex: regular expression namesofnewmetrics: how the new metrics' names are composed (can use $1, $2... for groups defined by () in regex). calculation: how the values of the new metrics should be calculated newuom (optional): unit of measure for the new metrics min (optional): lowest value the metrics can reach max (optional): highest value the metrics can reach  Common examples:      Sum wrong packets from all interfaces (with interface need     --units-errors=absolute):     --extend-perfdata-group=',packets\_wrong,sum(packets\_(discard     \|error)\_(in\|out))'      Sum traffic by interface:     --extend-perfdata-group='traffic\_in\_(.*),traffic\_$1,sum(traf     fic\_(in\|out)\_$1)'   |
| --change-short-output --change-long-output | Modify the short/long output that is returned by the plugin. Syntax: --change-short-output=pattern~replacement~modifier Most commonly used modifiers are i (case insensitive) and g (replace all occurrences). Example: adding --change-short-output='OK~Up~gi' will replace all occurrences of 'OK', 'ok', 'Ok' or 'oK' with 'Up'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --change-exit                              | Replace an exit code with one of your choice. Example: adding --change-exit=unknown=critical will result in a CRITICAL state instead of an UNKNOWN state.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --range-perfdata                           | Rewrite the ranges displayed in the perfdata. Accepted values: 0: nothing is changed. 1: if the lower value of the range is equal to 0, it is removed. 2: remove the thresholds from the perfdata.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --filter-uom                               | Mask the units when they don't match the given regular expression.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --opt-exit                                 | Replace the exit code in case of an execution error (i.e. wrong option provided, SSH connection refused, timeout, etc). Default: unknown.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-ignore-perfdata                   | Remove all the metrics from the service. The service will still have a status and an output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --output-ignore-label                      | Remove the status label ("OK:", "WARNING:", "UNKNOWN:", CRITICAL:") from the beginning of the output. Example: 'OK: Ram Total:...' will become 'Ram Total:...'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --output-xml                               | Return the output in XML format (to send to an XML API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --output-json                              | Return the output in JSON format (to send to a JSON API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-openmetrics                       | Return the output in OpenMetrics format (to send to a tool expecting this format).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --output-file                              | Write output in file (can be combined with json, xml and openmetrics options). E.g.: --output-file=/tmp/output.txt will write the output in /tmp/output.txt.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-format                             | Applies only to modes beginning with 'list-'. Returns the list of available macros to configure a service discovery rule (formatted in XML).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-show                               | Applies only to modes beginning with 'list-'. Returns the list of discovered objects (formatted in XML) for service discovery.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --float-precision                          | Define the float precision for thresholds (default: 8).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource Default: 'UTF-8'.      pfsense FauxAPI                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --hostname                                 | pfsense hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --port                                     | Port used (default: 443)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --proto                                    | Specify https if needed (default: 'https')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --api-key                                  | API key.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --api-secret                               | API secret.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --timeout                                  | Set timeout in seconds (default: 10).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --http-peer-addr                           | Set the address you want to connect to. Useful if hostname is only a vhost, to avoid IP resolution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --proxyurl                                 | Proxy URL. Example: http://my.proxy:3128                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --proxypac                                 | Proxy pac file (can be a URL or a local file).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --insecure                                 | Accept insecure SSL connections.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --http-backend                             | Perl library to use for HTTP transactions. Possible values are: lwp (default) and curl.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --ssl-opt                                  | Set SSL Options (--ssl-opt="SSL\_version =\> TLSv1" --ssl-opt="SSL\_verify\_mode =\> SSL\_VERIFY\_NONE").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --curl-opt                                 | Set CURL Options (--curl-opt="CURLOPT\_SSL\_VERIFYPEER =\> 0" --curl-opt="CURLOPT\_SSLVERSION =\> CURL\_SSLVERSION\_TLSv1\_1" ).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

#### Options des modes

Les options disponibles pour chaque modèle de services sont listées ci-dessous :

<Tabs groupId="sync">
<TabItem value="Backup-Files" label="Backup-Files">

| Option                   | Description                                                                           |
|:-------------------------|:--------------------------------------------------------------------------------------|
| --filter-counters        | Only display some counters (regexp can be used). Example: --filter-counters='total'   |
| --warning-* --critical-* | Thresholds. Can be: 'total', 'time-last'.                                             |

</TabItem>
<TabItem value="Gateways" label="Gateways">

| Option                   | Description                                                                                                                                                  |
|:-------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-counters        | Only display some counters (regexp can be used). Example: --filter-counters='status'                                                                         |
| --filter-name            | Filter gateway name (can be a regexp).                                                                                                                       |
| --unknown-status         | Define the conditions to match for the status to be UNKNOWN (default: ''). You can use the following variables: %\{status\}, %\{display\}                        |
| --warning-status         | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{status\}, %\{display\}                        |
| --critical-status        | Define the conditions to match for the status to be CRITICAL (default: '%\{status\} !~ /none/i'). You can use the following variables: %\{status\}, %\{display\}   |
| --warning-* --critical-* | Thresholds. Can be: 'packets-delay' (ms), 'packets-loss' (%), 'packets-stddev' (ms).                                                                         |

</TabItem>
<TabItem value="Rules" label="Rules">

| Option                   | Description                                                                                                                                                                                                                                   |
|:-------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached              | Memcached server to use (only one server).                                                                                                                                                                                                    |
| --redis-server           | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                               |
| --redis-attribute        | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                       |
| --redis-db               | Set Redis database index.                                                                                                                                                                                                                     |
| --failback-file          | Failback on a local file if Redis connection fails.                                                                                                                                                                                           |
| --memexpiration          | Time to keep data in seconds (default: 86400).                                                                                                                                                                                                |
| --statefile-dir          | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                        |
| --statefile-suffix       | Define a suffix to customize the statefile name (default: '').                                                                                                                                                                                |
| --statefile-concat-cwd   | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.   |
| --statefile-format       | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                         |
| --statefile-key          | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                  |
| --statefile-cipher       | Define the cipher algorithm to encrypt the cache (default: 'AES').                                                                                                                                                                            |
| --filter-counters        | Only display some counters (regexp can be used). Example: --filter-counters='traffic'                                                                                                                                                         |
| --filter-name            | Filter rule name (can be a regexp).                                                                                                                                                                                                           |
| --warning-* --critical-* | Thresholds. Can be: 'traffic' (b/s).                                                                                                                                                                                                          |

</TabItem>
<TabItem value="System" label="System">

| Option                   | Description                                                                                          |
|:-------------------------|:-----------------------------------------------------------------------------------------------------|
| --filter-counters        | Only display some counters (regexp can be used). Example: --filter-counters='temperature'            |
| --warning-* --critical-* | Thresholds. Can be: 'temperature' (C), 'connections-tcp-usage', 'connections-tcp-usage-prct' (%).    |

</TabItem>
</Tabs>

Pour un mode, la liste de toutes les options disponibles et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_pfsense_fauxapi.pl \
	--plugin=apps::pfsense::fauxapi::plugin \
	--mode=rules \
	--help
```
