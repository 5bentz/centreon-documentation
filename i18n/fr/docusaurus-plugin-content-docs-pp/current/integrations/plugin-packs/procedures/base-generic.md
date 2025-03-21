---
id: base-generic
title: Base Pack
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Le pack Base-Generic est utilisé par tous les autres. Il fournit des modèles d'hôtes et de services actifs et passifs ainsi que le service Ping.

## Contenu du pack

### Modèles

Le connecteur de supervision **base-generic** apporte 4 modèles d'hôte :

* generic-active-host
* generic-passive-host
* generic-dummy-host
* Generic-Active-Cloud-Host

Le connecteur apporte les modèles de service suivants (classés selon le modèle d'hôte auquel ils sont rattachés) :

<Tabs groupId="sync">
<TabItem value="generic-active-host-custom" label="generic-active-host-custom">

| Alias  | Modèle de service                     | Description          |
|:---------------|:------------------------------------|:-----------------------------|
| Ping     | Base-Ping-LAN     | Check host response time                           |

</TabItem>
<TabItem value="generic-passive-host-custom" label="generic-passive-host-custom">
  
Ce modèle d'hôte n'est associé à aucun modèle de service.

</TabItem>
<TabItem value="generic-dummy-host-custom" label="generic-dummy-host-custom">

Ce modèle d'hôte n'est associé à aucun modèle de service.

</TabItem>
<TabItem value="Generic-Active-Cloud-Host-custom" label="Generic-Active-Cloud-Host-custom">

Ce modèle d'hôte n'est associé à aucun modèle de service.

</TabItem>
<TabItem value="Not attached to a host template" label="Not attached to a host template">

| Alias         | Modèle de service                           | Description                          |
|:----------------------|:------------------------------------------|:---------------------------------------------|
| generic-active-service | generic-active-service | Check service availability and status proactively |
| generic-passive-service     | generic-passive-service     | Check service status reactively based on received data|

</TabItem>
</Tabs>

### Métriques & statuts collectés

Voici le tableau des services pour ce connecteur, détaillant les métriques rattachées à chaque service.

<Tabs groupId="sync">
<TabItem value="Base-Ping-LAN" label="Base-Ping-LAN">

| Métrique                             | Unité |
|:-------------------------------------|:------|
| rta        | ms     |
| pl        | %     |
| rtmax        | ms     |
| rtmin        | ms     |

</TabItem>
</Tabs>

## Prérequis

Ce connecteur de supervision n'a aucun prérequis spécifique hormis le check ICMP de Nagios, qui est déjà installé par défaut sur les serveurs Centreon.

## Utiliser le connecteur de supervision

### Utiliser un modèle d'hôte issu du connecteur

<Tabs groupId="sync">
<TabItem value="generic-dummy-host" label="generic-dummy-host">

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Appliquez le modèle d'hôte **generic-dummy-host**. Une liste de macros apparaît. Les macros vous permettent de définir comment le connecteur se connectera à la ressource, ainsi que de personnaliser le comportement du connecteur.

| Macro               | Description                      |
|:------------------|:---------------------------------|
| DUMMYSTATUS   | Host state. Default is OK, do not modify it unless you know what you are doing                   |
| DUMMYOUTPUT   | Host check output. Default is 'This is a dummy check'. Customize it with your own if needed                |

</TabItem>
<TabItem value="generic-passive-host" label="generic-passive-host">

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Appliquez le modèle d'hôte **generic-passive-host**. Une liste de macros apparaît. Les macros vous permettent de définir comment le connecteur se connectera à la ressource, ainsi que de personnaliser le comportement du connecteur.

| Macro               | Description                      |
|:------------------|:---------------------------------|
| DUMMYSTATUS   | Host state. Default is OK, do not modify it unless you know what you are doing                   |
| DUMMYOUTPUT   | Host check output. Default is 'This is a dummy check'. Customize it with your own if needed                |

</TabItem>
</Tabs>

### Utiliser un modèle de service issu du connecteur

1. Si vous avez utilisé un modèle d'hôte et coché la case **Créer aussi les services liés aux modèles**, les services associés au modèle ont été créés automatiquement, avec les modèles de services correspondants. Sinon, [créez les services désirés manuellement](/docs/monitoring/basic-objects/services) et appliquez-leur un modèle de service.
2. Renseignez les macros désirées (par exemple, ajustez les seuils d'alerte).

<Tabs groupId="sync">
<TabItem value="Ping" label="Ping">

| Macro        | Description        | Valeur par défaut |
| :----------- | :----------------- | :------------ |
| PACKETNUMBER | Number of packets   | 5             |
| WARNING      | Warning threshold  | 200,20%       |
| CRITICAL     | Critical Threshold | 400,50%       |

</TabItem>
<TabItem value="generic-passive-service" label="generic-passive-service">

| Macro        | Description        | Valeur par défaut |
| :----------- | :----------------- | :------------ |
| DUMMYSTATUS | Service state. Default is OK, do not modify it unless you know what you are doing       | OK             |
| DUMMYOUTPUT      |  Service check output. Default is 'Service is OK'. Customize it with your own if needed  | Service is OK       |

</TabItem>
</Tabs>

## Comment puis-je tester le plugin et que signifient les options des commandes ?

Une fois le plugin installé, vous pouvez tester celui-ci directement en ligne
de commande depuis votre collecteur Centreon en vous connectant avec
l'utilisateur **centreon-engine** (`su - centreon-engine`). Vous pouvez tester
que le connecteur arrive bien à superviser une instance en utilisant une commande
telle que celle-ci (remplacez les valeurs d'exemple par les vôtres) :

```bash
/usr/lib/nagios/plugins/check_icmp -H 10.0.0.1 -n 5 -w 200,20% -c 400,50%
```

La commande devrait retourner un message de sortie similaire à :

```bash
Ping rta=0,032ms;200,000;400,000;0; pl=0%;20;50;; rtmax=0,047ms;;;; rtmin=0,023ms;;;;
```

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
| --filter-perfdata                          | Filter perfdata that match the regexp. Example: adding --filter-perfdata='avg' will remove all metrics that do not contain 'avg' from performance data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --filter-perfdata-adv                      | Filter perfdata based on a "if" condition using the following variables: label, value, unit, warning, critical, min, max. Variables must be written either %\{variable\} or %(variable). Eg: adding --filter-perfdata-adv='not (%(value) == 0 and %(max) eq "")' will remove all metrics whose value equals 0 and that don't have a maximum value.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --explode-perfdata-max                     | Create a new metric for each metric that comes with a maximum limit. The new metric will be named identically with a '\_max' suffix). Eg: it will split 'used\_prct'=26.93%;0:80;0:90;0;100 into 'used\_prct'=26.93%;0:80;0:90;0;100 'used\_prct\_max'=100%;;;;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --change-perfdata --extend-perfdata        | Change or extend perfdata. Syntax: --extend-perfdata=searchlabel,newlabel,target\[,\[newuom\],\[min\],\[m ax\]\]  Common examples:      Convert storage free perfdata into used:     --change-perfdata=free,used,invert()      Convert storage free perfdata into used:     --change-perfdata=used,free,invert()      Scale traffic values automatically:     --change-perfdata=traffic,,scale(auto)      Scale traffic values in Mbps:     --change-perfdata=traffic\_in,,scale(Mbps),mbps      Change traffic values in percent:     --change-perfdata=traffic\_in,,percent()                                                                                                                                                                                                                                                                                                                                                                          |
| --extend-perfdata-group                    | Add new aggregated metrics (min, max, average or sum) for groups of metrics defined by a regex match on the metrics' names. Syntax: --extend-perfdata-group=regex,namesofnewmetrics,calculation\[,\[ne wuom\],\[min\],\[max\]\] regex: regular expression namesofnewmetrics: how the new metrics' names are composed (can use $1, $2... for groups defined by () in regex). calculation: how the values of the new metrics should be calculated newuom (optional): unit of measure for the new metrics min (optional): lowest value the metrics can reach max (optional): highest value the metrics can reach  Common examples:      Sum wrong packets from all interfaces (with interface need     --units-errors=absolute):     --extend-perfdata-group=',packets\_wrong,sum(packets\_(discard     \|error)\_(in\|out))'      Sum traffic by interface:     --extend-perfdata-group='traffic\_in\_(.*),traffic\_$1,sum(traf     fic\_(in\|out)\_$1)'   |
| --change-short-output --change-long-output | Modify the short/long output that is returned by the plugin. Syntax: --change-short-output=pattern~replacement~modifier Most commonly used modifiers are i (case insensitive) and g (replace all occurrences). Eg: adding --change-short-output='OK~Up~gi' will replace all occurrences of 'OK', 'ok', 'Ok' or 'oK' with 'Up'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --change-exit                              | Replace an exit code with one of your choice. Eg: adding --change-exit=unknown=critical will result in a CRITICAL state instead of an UNKNOWN state.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --range-perfdata                           | Rewrite the ranges displayed in the perfdata. Accepted values: 0: nothing is changed. 1: if the lower value of the range is equal to 0, it is removed. 2: remove the thresholds from the perfdata.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --filter-uom                               | Mask the units when they don't match the given regular expression.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --opt-exit                                 | Replace the exit code in case of an execution error (i.e. wrong option provided, SSH connection refused, timeout, etc). Default: unknown.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-ignore-perfdata                   | Remove all the metrics from the service. The service will still have a status and an output.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --output-ignore-label                      | Remove the status label ("OK:", "WARNING:", "UNKNOWN:", CRITICAL:") from the beginning of the output. Eg: 'OK: Ram Total:...' will become 'Ram Total:...'                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-xml                               | Return the output in XML format (to send to an XML API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --output-json                              | Return the output in JSON format (to send to a JSON API).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --output-openmetrics                       | Return the output in OpenMetrics format (to send to a tool expecting this format).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --output-file                              | Write output in file (can be combined with json, xml and openmetrics options). E.g.: --output-file=/tmp/output.txt will write the output in /tmp/output.txt.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-format                             | Applies only to modes beginning with 'list-'. Returns the list of available macros to configure a service discovery rule (formatted in XML).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --disco-show                               | Applies only to modes beginning with 'list-'. Returns the list of discovered objects (formatted in XML) for service discovery.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --float-precision                          | Define the float precision for thresholds (default: 8).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource Default: 'UTF-8'.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
#### Options des modes

Les options disponibles pour chaque modèle de services sont listées ci-dessous :

<Tabs groupId="sync">
<TabItem value="Base-Ping-LAN" label="Base-Ping-LAN">

| Option              | Description                                                                                      |
|:--------------------|:-------------------------------------------------------------------------------------------------|
| -h, --help    | Print detailed help screen                                                                             |
| -V, --version    | Print version information                                                                           |
| -v, --verbose | Show details for command-line debugging (Nagios may truncate output)                                   |
| -s, --serverip=IPADDRESS     | IP address of DHCP server that we must hear from                                        |
| -r, --requestedip=IPADDRESS            | IP address that should be offered by at least one DHCP server                 |
| -t, --timeout=INTEGER            | Seconds to wait for DHCPOFFER before timeout occurs                                 |
| -i, --interface=STRING         | Interface to to use for listening (i.e. eth0)                                         |
| -m, --mac=STRING         | MAC address to use in the DHCP request                                                      |
| -u, --unicast            | Unicast testing: mimic a DHCP relay, requires -s                                            |

</TabItem>
</Tabs>
