---
id: applications-monitoring-node-exporter-windows
title: Node Exporter Windows Metrics
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Vue d'ensemble

Ce pack permet la supervision d'un hôte Windows basée sur les métriques remontées par l'exporteur Prometheus, un agent logiciel qui collecte et expose des données de performance et de ressources système.

## Contenu du pack

### Modèles

Le connecteur de supervision **Node Exporter Windows Metrics** apporte un modèle d'hôte :

* **App-Monitoring-Node-Exporter-Windows-custom**

Le connecteur apporte les modèles de service suivants
(classés selon le modèle d'hôte auquel ils sont rattachés) :

<Tabs groupId="sync">
<TabItem value="App-Monitoring-Node-Exporter-Windows-custom" label="App-Monitoring-Node-Exporter-Windows-custom">

| Alias             | Modèle de service                                        | Description                                   | Découverte |
|:------------------|:---------------------------------------------------------|:----------------------------------------------|:----------:|
| Node-Cpu          | App-Monitoring-Node-Exporter-Windows-Cpu-custom          | Contrôle l'utilisation CPU du noeud           |            |
| Node-Memory       | App-Monitoring-Node-Exporter-Windows-Memory-custom       | Contrôle la consommation mémoire du noeud     |            |
| Node-Service-Name | App-Monitoring-Node-Exporter-Windows-Service-Name-custom | Contrôle l'état des services                  | X          |
| Node-Storage      | App-Monitoring-Node-Exporter-Windows-Storage-custom      | Contrôle la consommation du stockage du noeud | X          |
| Node-Traffic      | App-Monitoring-Node-Exporter-Windows-Traffic-custom      | Contrôle le trafic réseau par interface       | X          |

> Les services listés ci-dessus sont créés automatiquement lorsque le modèle d'hôte **App-Monitoring-Node-Exporter-Windows-custom** est utilisé.

> Si la case **Découverte** est cochée, cela signifie qu'une règle de découverte de service existe pour ce service.

</TabItem>
</Tabs>

### Règles de découverte

#### Découverte de services

| Nom de la règle                                     | Description                                                             |
|:----------------------------------------------------|:------------------------------------------------------------------------|
| App-Monitoring-Node-Exporter-Windows-Interface-Name | Découvre les interfaces réseaux et supervise le statut et l'utilisation |
| App-Monitoring-Node-Exporter-Windows-Service-Name   | Découvre les services et supervise leur utilisation système                        |
| App-Monitoring-Node-Exporter-Windows-Storage-Name   | Découvre les partitions de disque et supervise l'occupation de l'espace de stockage |

Rendez-vous sur la [documentation dédiée](/docs/monitoring/discovery/services-discovery)
pour en savoir plus sur la découverte automatique de services et sa [planification](/docs/monitoring/discovery/services-discovery/#règles-de-découverte).

### Métriques & statuts collectés

Voici le tableau des services pour ce connecteur, détaillant les métriques rattachées à chaque service.

<Tabs groupId="sync">
<TabItem value="Node-Cpu" label="Node-Cpu">

| Métrique                                              | Unité |
|:------------------------------------------------------|:------|
| cpu.utilization.percentage                            | %     |
| *node_cpu*#node.cpu.idle.utilization.percentage       | %     |
| *node_cpu*#node.cpu.dpc.utilization.percentage        | %     |
| *node_cpu*#node.cpu.interrupt.utilization.percentage  | %     |
| *node_cpu*#node.cpu.privileged.utilization.percentage | %     |
| *node_cpu*#node.cpu.user.utilization.percentage       | %     |

</TabItem>
<TabItem value="Node-Memory" label="Node-Memory">

| Métrique                | Unité |
|:------------------------|:------|
| node.memory.usage.bytes | B     |
| node.paging.usage.bytes | B     |

</TabItem>
<TabItem value="Node-Service-Name" label="Node-Service-Name">

| Métrique         | Unité |
|:-----------------|:------|
| *service*#status | N/A   |

</TabItem>
<TabItem value="Node-Storage" label="Node-Storage">

| Métrique                                  | Unité |
|:------------------------------------------|:------|
| *disk_name*#node.storage.space.free.bytes | B     |

</TabItem>
<TabItem value="Node-Traffic" label="Node-Traffic">

| Métrique                                 | Unité |
|:-----------------------------------------|:------|
| node.bandwidth.usage                     | %     |
| *traffic*#node.packets.in.count          | count |
| *traffic*#node.packets.out.count         | count |
| *traffic*#node.packets.in.error.count    | count |
| *traffic*#node.packets.out.error.count   | count |
| *traffic*#node.traffic.in.bitspersecond  | b/s   |
| *traffic*#node.traffic.out.bitspersecond | b/s   |

</TabItem>
</Tabs>

## Prérequis

Ce pack est basé sur l'exporteur "Prometheus community" pour les machines Windows : https://github.com/prometheus-community/windows_exporter#installation.

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
dnf install centreon-pack-applications-monitoring-node-exporter-windows
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-applications-monitoring-node-exporter-windows
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-pack-applications-monitoring-node-exporter-windows
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-applications-monitoring-node-exporter-windows
```

</TabItem>
</Tabs>

2. Quel que soit le type de la licence (*online* ou *offline*), installez le connecteur **Node Exporter Windows Metrics**
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
dnf install centreon-plugin-Applications-Monitoring-Nodeexporter-Windows
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Applications-Monitoring-Nodeexporter-Windows
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-plugin-applications-monitoring-nodeexporter-windows
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Applications-Monitoring-Nodeexporter-Windows
```

</TabItem>
</Tabs>

## Utiliser le connecteur de supervision

### Utiliser un modèle d'hôte issu du connecteur

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Complétez les champs **Nom**, **Alias** & **IP Address/DNS** correspondant à votre ressource.
3. Appliquez le modèle d'hôte **App-Monitoring-Node-Exporter-Windows-custom**. Une liste de macros apparaît. Les macros vous permettent de définir comment le connecteur se connectera à la ressource, ainsi que de personnaliser le comportement du connecteur.
4. Renseignez les macros désirées. Attention, certaines macros sont obligatoires.

| Macro             | Description                                                                                          | Valeur par défaut | Obligatoire |
|:------------------|:-----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| NODEEXPORTERPROTO | Specify https if needed (default: 'http')                                                            | http              |             |
| NODEEXPORTERURL   | URL to scrape metrics from (default: '/metrics')                                                     | /metrics          |             |
| NODEEXPORTERPORT  | Port used                                                                             | 9182              |             |
| EXTRAOPTIONS      | Any extra option you may want to add to every command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

5. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). L'hôte apparaît dans la liste des hôtes supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails de l'hôte : celle-ci montre les valeurs des macros.

### Utiliser un modèle de service issu du connecteur

1. Si vous avez utilisé un modèle d'hôte et coché la case **Créer aussi les services liés aux modèles**, les services associés au modèle ont été créés automatiquement, avec les modèles de services correspondants. Sinon, [créez les services désirés manuellement](/docs/monitoring/basic-objects/services) et appliquez-leur un modèle de service.
2. Renseignez les macros désirées (par exemple, ajustez les seuils d'alerte). Les macros indiquées ci-dessous comme requises (**Obligatoire**) doivent être renseignées.

<Tabs groupId="sync">
<TabItem value="Node-Cpu" label="Node-Cpu">

| Macro              | Description                                                                                        | Valeur par défaut | Obligatoire |
|:-------------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNINGAVERAGE     | Warning threshold                                                                                  |                   |             |
| CRITICALAVERAGE    | Critical threshold                                                                                 |                   |             |
| WARNINGDPC         | Warning threshold                                                                                  |                   |             |
| CRITICALDPC        | Critical threshold                                                                                 |                   |             |
| WARNINGIDLE        | Warning threshold                                                                                  |                   |             |
| CRITICALIDLE       | Critical threshold                                                                                 |                   |             |
| WARNINGINTERRUPT   | Warning threshold                                                                                  |                   |             |
| CRITICALINTERRUPT  | Critical threshold                                                                                 |                   |             |
| WARNINGPRIVILEGED  | Warning threshold                                                                                  |                   |             |
| CRITICALPRIVILEGED | Critical threshold                                                                                 |                   |             |
| WARNINGUSER        | Warning threshold                                                                                  |                   |             |
| CRITICALUSER       | Critical threshold                                                                                 |                   |             |
| EXTRAOPTIONS       | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

</TabItem>
<TabItem value="Node-Memory" label="Node-Memory">

| Macro          | Description                                                                                        | Valeur par défaut | Obligatoire |
|:---------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| UNITS          | Units of thresholds. Can be : '%', 'B' Default: '%'                                                | %                 |             |
| WARNINGPAGING  | Warning threshlod                                                                                  |                   |             |
| CRITICALPAGING | Critical threshlod                                                                                 |                   |             |
| WARNINGUSAGE   | Warning threshlod                                                                                  |                   |             |
| CRITICALUSAGE  | Critical threshlod                                                                                 |                   |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

</TabItem>
<TabItem value="Node-Service-Name" label="Node-Service-Name">

| Macro          | Description                                                                                                                                                                                    | Valeur par défaut                                    | Obligatoire |
|:---------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------|:-----------:|
| SERVICENAME    | Specify which service to monitor. Can be a regex.  Default: all services are monitored                                                                                                         | .*                                                   |             |
| CRITICALSTATUS | Define the conditions to match for the status to be CRITICAL (default: '%\{start_mode\} =~ /auto/ && %\{status\} !~ /^running$/'). You can use the following variables: %\{status\}, %\{start_mode\} | %\{start_mode\} =~ /auto/ && %\{status\} !~ /^running$/ |             |
| WARNINGSTATUS  | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{status\}, %\{start_mode\}                                                      |                                                      |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                                                             |                                                      |             |

</TabItem>
<TabItem value="Node-Storage" label="Node-Storage">

| Macro         | Description                                                                                        | Valeur par défaut | Obligatoire |
|:--------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| UNITS         | Units of thresholds. Can be : '%', 'B' Default: '%'                                                | %                 |             |
| DISKNAME      | Specify which disk to monitor. Can be a regex.  Default: all disks are monitored                   | .*                |             |
| WARNINGUSAGE  | Warning threshold                                                                                  |                   |             |
| CRITICALUSAGE | Critical threshold                                                                                 |                   |             |
| EXTRAOPTIONS  | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

</TabItem>
<TabItem value="Node-Traffic" label="Node-Traffic">

| Macro                  | Description                                                                                        | Valeur par défaut | Obligatoire |
|:-----------------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| INTERFACENAME          | Specify which interface to monitor. Can be a regex.          Default: all interfaces are monitored | .*                |             |
| WARNINGBANDWIDTHUSAGE  | Warning thresholds                                                                                 |                   |             |
| CRITICALBANDWIDTHUSAGE | Critical thresholds                                                                                |                   |             |
| WARNINGPACKETSIN       | Warning thresholds                                                                                 |                   |             |
| CRITICALPACKETSIN      | Critical thresholds                                                                                |                   |             |
| WARNINGPACKETSOUT      | Warning thresholds                                                                                 |                   |             |
| CRITICALPACKETSOUT     | Critical thresholds                                                                                |                   |             |
| WARNINGTRAFFICIN       | Warning thresholds                                                                                 |                   |             |
| CRITICALTRAFFICIN      | Critical thresholds                                                                                |                   |             |
| WARNINGTRAFFICOUT      | Warning thresholds                                                                                 |                   |             |
| CRITICALTRAFFICOUT     | Critical thresholds                                                                                |                   |             |
| EXTRAOPTIONS           | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

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
/usr/lib/centreon/plugins/centreon_monitoring_nodeexporter_windows.pl \
	--plugin=apps::monitoring::nodeexporter::windows::plugin \
	--mode=traffic \
	--hostname=10.0.0.1 \
	--urlpath='/metrics' \
	--port='9182' \
	--proto='http'  \
	--interface='.*' \
	--warning-traffic-in='' \
	--critical-traffic-in='' \
	--warning-traffic-out='' \
	--critical-traffic-out='' \
	--warning-packets-in='' \
	--critical-packets-in='' \
	--warning-packets-out='' \
	--critical-packets-out='' \
	--warning-bandwidth-usage='' \
	--critical-bandwidth-usage=''
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK: Average bandwidth usage : 86 % All interfaces are OK.  | 'node.bandwidth.usage'=86%;;;0;100'*traffic*#node.packets.in.count'=;;;0;'*traffic*#node.packets.out.count'=;;;0;'*traffic*#node.packets.in.error.count'=;;;0;'*traffic*#node.packets.out.error.count'=;;;0;'*traffic*#node.traffic.in.bitspersecond'=123b/s;;;0;'*traffic*#node.traffic.out.bitspersecond'=123b/s;;;0;
```

### Diagnostic des erreurs communes

Rendez-vous sur la [documentation dédiée](../getting-started/how-to-guides/troubleshooting-plugins.md)
pour le diagnostic des erreurs communes des plugins Centreon.

### Modes disponibles

Dans la plupart des cas, un mode correspond à un modèle de service. Le mode est renseigné dans la commande d'exécution
du connecteur. Dans l'interface de Centreon, il n'est pas nécessaire de les spécifier explicitement, leur utilisation est
implicite dès lors que vous utilisez un modèle de service. En revanche, vous devrez spécifier le mode correspondant à ce
modèle si vous voulez tester la commande d'exécution du connecteur dans votre terminal.

Tous les modes disponibles peuvent être affichés en ajoutant le paramètre
`--list-mode` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_monitoring_nodeexporter_windows.pl \
	--plugin=apps::monitoring::nodeexporter::windows::plugin \
	--list-mode
```

Le plugin apporte les modes suivants :

| Mode                                                                                                                                                | Modèle de service associé                                |
|:----------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------|
| cpu [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/windows/mode/cpu.pm)]                        | App-Monitoring-Node-Exporter-Windows-Cpu-custom          |
| list-interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/windows/mode/listinterfaces.pm)] | Used for service discovery                               |
| list-services [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/windows/mode/listservices.pm)]     | Used for service discovery                               |
| list-storages [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/windows/mode/liststorages.pm)]     | Used for service discovery                               |
| memory [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/windows/mode/memory.pm)]                  | App-Monitoring-Node-Exporter-Windows-Memory-custom       |
| services [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/windows/mode/services.pm)]              | App-Monitoring-Node-Exporter-Windows-Service-Name-custom |
| storage [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/windows/mode/storage.pm)]                | App-Monitoring-Node-Exporter-Windows-Storage-custom      |
| traffic [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/windows/mode/traffic.pm)]                | App-Monitoring-Node-Exporter-Windows-Traffic-custom      |

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
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource Default: 'UTF-8'.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --hostname                                 | Endpoint hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --port                                     | Port used (default: 80)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --proto                                    | Specify https if needed (default: 'http')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --urlpath                                  | URL to scrape metrics from (default: '/metrics').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --username                                 | Endpoint username.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --password                                 | Endpoint password.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --timeout                                  | Set HTTP timeout (default: 10).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
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
<TabItem value="Node-Cpu" label="Node-Cpu">

| Option                 | Description                                                                                                                                                                                                                                   |
|:-----------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached            | Memcached server to use (only one server).                                                                                                                                                                                                    |
| --redis-server         | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                               |
| --redis-attribute      | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                       |
| --redis-db             | Set Redis database index.                                                                                                                                                                                                                     |
| --failback-file        | Failback on a local file if Redis connection fails.                                                                                                                                                                                           |
| --memexpiration        | Time to keep data in seconds (default: 86400).                                                                                                                                                                                                |
| --statefile-dir        | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                        |
| --statefile-suffix     | Define a suffix to customize the statefile name (default: '').                                                                                                                                                                                |
| --statefile-concat-cwd | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.   |
| --statefile-format     | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                         |
| --statefile-key        | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                  |
| --statefile-cipher     | Define the cipher algorithm to encrypt the cache (default: 'AES').                                                                                                                                                                            |
| --warning-*            | Warning threshold.  Can be: 'average', 'idle', 'dpc', 'user', 'interrupt', 'privileged'                                                                                                                                                       |
| --critical-*           | Critical threshold.  Can be: 'average', 'idle', 'dpc', 'user', 'interrupt', 'privileged'                                                                                                                                                      |

</TabItem>
<TabItem value="Node-Memory" label="Node-Memory">

| Option            | Description                                          |
|:------------------|:-----------------------------------------------------|
| --units           | Units of thresholds. Can be : '%', 'B' Default: '%'  |
| --warning-usage   | Warning threshlod.                                   |
| --critical-usage  | Critical threshlod.                                  |
| --warning-paging  | Warning threshlod.                                   |
| --critical-paging | Critical threshlod.                                  |

</TabItem>
<TabItem value="Node-Service-Name" label="Node-Service-Name">

| Option            | Description                                                                                                                                                                                       |
|:------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --service         | Specify which service to monitor. Can be a regex.  Default: all services are monitored.                                                                                                           |
| --warning-status  | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{status\}, %\{start_mode\}                                                         |
| --critical-status | Define the conditions to match for the status to be CRITICAL (default: '%\{start_mode\} =~ /auto/ && %\{status\} !~ /^running$/'). You can use the following variables: %\{status\}, %\{start_mode\}    |

</TabItem>
<TabItem value="Node-Storage" label="Node-Storage">

| Option           | Description                                                                         |
|:-----------------|:------------------------------------------------------------------------------------|
| --storage        | Specify which disk to monitor. Can be a regex.  Default: all disks are monitored.   |
| --units          | Units of thresholds. Can be : '%', 'B' Default: '%'                                 |
| --warning-usage  | Warning threshold.                                                                  |
| --critical-usage | Critical threshold.                                                                 |

</TabItem>
<TabItem value="Node-Traffic" label="Node-Traffic">

| Option                 | Description                                                                                                                                                                                                                                   |
|:-----------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached            | Memcached server to use (only one server).                                                                                                                                                                                                    |
| --redis-server         | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                               |
| --redis-attribute      | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                       |
| --redis-db             | Set Redis database index.                                                                                                                                                                                                                     |
| --failback-file        | Failback on a local file if Redis connection fails.                                                                                                                                                                                           |
| --memexpiration        | Time to keep data in seconds (default: 86400).                                                                                                                                                                                                |
| --statefile-dir        | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                        |
| --statefile-suffix     | Define a suffix to customize the statefile name (default: '').                                                                                                                                                                                |
| --statefile-concat-cwd | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.   |
| --statefile-format     | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                         |
| --statefile-key        | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                  |
| --statefile-cipher     | Define the cipher algorithm to encrypt the cache (default: 'AES').                                                                                                                                                                            |
| --interface            |         Specify which interface to monitor. Can be a regex.          Default: all interfaces are monitored.                                                                                                                                   |
| --warning-*            |         Warning thresholds.          Can be: 'traffic-in', 'traffic-out', 'packets-in', 'packets-out',         'bandwidth-usage'                                                                                                              |
| --critical-*           |         Critical thresholds.          Can be: 'traffic-in', 'traffic-out', 'packets-in', 'packets-out',         'bandwidth-usage'                                                                                                             |

</TabItem>
</Tabs>

Pour un mode, la liste de toutes les options disponibles et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_monitoring_nodeexporter_windows.pl \
	--plugin=apps::monitoring::nodeexporter::windows::plugin \
	--mode=traffic \
	--help
```
