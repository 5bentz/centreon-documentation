---
id: network-fortinet-fortigate-restapi
title: Fortinet Fortigate Rest API
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Contenu du pack

### Modèles

Le connecteur de supervision **Fortinet Fortigate Rest API** apporte un modèle d'hôte :

* **Net-Fortinet-Fortigate-Restapi-custom**

Le connecteur apporte les modèles de service suivants
(classés selon le modèle d'hôte auquel ils sont rattachés) :

<Tabs groupId="sync">
<TabItem value="Net-Fortinet-Fortigate-Restapi-custom" label="Net-Fortinet-Fortigate-Restapi-custom">

| Alias    | Modèle de service                              | Description                              |
|:---------|:-----------------------------------------------|:-----------------------------------------|
| Health   | Net-Fortinet-Fortigate-Health-Restapi-custom   | Contrôle l'état de santé du firewall    |
| Licenses | Net-Fortinet-Fortigate-Licenses-Restapi-custom | Contrôle le statut des licences          |
| System   | Net-Fortinet-Fortigate-System-Restapi-custom   | Contrôle l'utilisation système des VDOM  |

> Les services listés ci-dessus sont créés automatiquement lorsque le modèle d'hôte **Net-Fortinet-Fortigate-Restapi-custom** est utilisé.

</TabItem>
<TabItem value="Non rattachés à un modèle d'hôte" label="Non rattachés à un modèle d'hôte">

| Alias | Modèle de service                        | Description                                            |
|:------|:-----------------------------------------|:-------------------------------------------------------|
| Ha    | Net-Fortinet-Fortigate-Ha-Restapi-custom | Contrôle l'utilisation système des membres du cluster  |

> Les services listés ci-dessus ne sont pas créés automatiquement lorsqu'un modèle d'hôte est appliqué. Pour les utiliser, [créez un service manuellement](/docs/monitoring/basic-objects/services) et appliquez le modèle de service souhaité.

</TabItem>
</Tabs>

### Métriques & statuts collectés

Voici le tableau des services pour ce connecteur, détaillant les métriques rattachées à chaque service.

<Tabs groupId="sync">
<TabItem value="Ha" label="Ha">

| Métrique                                        | Unité |
|:------------------------------------------------|:------|
| members.detected.count                          | count |
| *member_name*~member.cpu.utilization.percentage | %     |
| *member_name*~member.memory.usage.percentage    | %     |
| *member_name*~member.sessions.active.count      | count |

</TabItem>
<TabItem value="Health" label="Health">

| Métrique           | Unité |
|:-------------------|:------|
| *vdom_name*#health | N/A   |

</TabItem>
<TabItem value="Licenses" label="Licenses">

| Métrique                               | Unité |
|:---------------------------------------|:------|
| *license_name*#status                  | N/A   |
| *license_name*#license.expires.seconds | s     |

</TabItem>
<TabItem value="System" label="System">

| Métrique                               | Unité |
|:---------------------------------------|:------|
| *vdom_name*~cpu.utilization.percentage | %     |
| *vdom_name*~memory.usage.percentage    | %     |
| *vdom_name*~sessions.active.count      | count |

</TabItem>
</Tabs>

## Prérequis

Afin de contrôler votre équipement Fortinet Fortigate, l'API Rest doit être configurée (cf: https://docs.fortinet.com/document/fortigate/7.2.1/administration-guide/399023/rest-api-administrator).

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
dnf install centreon-pack-network-fortinet-fortigate-restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-network-fortinet-fortigate-restapi
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-pack-network-fortinet-fortigate-restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-network-fortinet-fortigate-restapi
```

</TabItem>
</Tabs>

2. Quel que soit le type de la licence (*online* ou *offline*), installez le connecteur **Fortinet Fortigate Rest API**
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
dnf install centreon-plugin-Network-Fortinet-Fortigate-Restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Network-Fortinet-Fortigate-Restapi
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-plugin-network-fortinet-fortigate-restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Network-Fortinet-Fortigate-Restapi
```

</TabItem>
</Tabs>

## Utiliser le connecteur de supervision

### Utiliser un modèle d'hôte issu du connecteur

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Complétez les champs **Nom**, **Alias** & **IP Address/DNS** correspondant à votre ressource.
3. Appliquez le modèle d'hôte **Net-Fortinet-Fortigate-Restapi-custom**. Une liste de macros apparaît. Les macros vous permettent de définir comment le connecteur se connectera à la ressource, ainsi que de personnaliser le comportement du connecteur.
4. Renseignez les macros désirées. Attention, certaines macros sont obligatoires.

| Macro           | Description                                                                                           | Valeur par défaut | Obligatoire |
|:----------------|:------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| APIACCESSTOKEN  | API token                                                                                             |                   | X           |
| APIPROTO        | Specify https if needed (Default: 'https')                                                            | https             |             |
| APIPORT         | Port used (Default: 443)                                                                              | 443               |             |
| APIEXTRAOPTIONS | Any extra option you may want to add to every command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

5. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). L'hôte apparaît dans la liste des hôtes supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails de l'hôte : celle-ci montre les valeurs des macros.

### Utiliser un modèle de service issu du connecteur

1. Si vous avez utilisé un modèle d'hôte et coché la case **Créer aussi les services liés aux modèles**, les services associés au modèle ont été créés automatiquement, avec les modèles de services correspondants. Sinon, [créez les services désirés manuellement](/docs/monitoring/basic-objects/services) et appliquez-leur un modèle de service.
2. Renseignez les macros désirées (par exemple, ajustez les seuils d'alerte). Les macros indiquées ci-dessous comme requises (**Obligatoire**) doivent être renseignées.

<Tabs groupId="sync">
<TabItem value="Ha" label="Ha">

| Macro                   | Description                                                                                         | Valeur par défaut | Obligatoire |
|:------------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERNAME              | Filter members by name                                                                              |                   |             |
| WARNINGCPUUTILIZATION   | Thresholds                                                                                          |                   |             |
| CRITICALCPUUTILIZATION  | Thresholds                                                                                          |                   |             |
| WARNINGMEMBERSDETECTED  | Thresholds                                                                                          |                   |             |
| CRITICALMEMBERSDETECTED | Thresholds                                                                                          |                   |             |
| WARNINGMEMORYUSAGE      | Thresholds                                                                                          |                   |             |
| CRITICALMEMORYUSAGE     | Thresholds                                                                                          |                   |             |
| WARNINGSESSIONSACTIVE   | Thresholds                                                                                          |                   |             |
| CRITICALSESSIONSACTIVE  | Thresholds                                                                                          |                   |             |
| EXTRAOPTIONS            | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) | --verbose         |             |

</TabItem>
<TabItem value="Health" label="Health">

| Macro          | Description                                                                                                                                                | Valeur par défaut       | Obligatoire |
|:---------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------|:-----------:|
| FILTERVDOM     | Filter vdom by name                                                                                                                                        |                         |             |
| CRITICALHEALTH | Define the conditions to match for the status to be CRITICAL (Default: '%\{status\} !~ /success/i'). You can use the following variables: %\{status\}, %\{name\} | %\{status\} !~ /success/i |             |
| WARNINGHEALTH  | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{status\}, %\{name\}                                       |                         |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                                        | --verbose               |             |

</TabItem>
<TabItem value="Licenses" label="Licenses">

| Macro           | Description                                                                                                                                                | Valeur par défaut       | Obligatoire |
|:----------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------|:-----------:|
| FILTERNAME      | Filter licenses by name (can be a regexp)                                                                                                                  |                         |             |
| UNIT            | Select the time unit for thresholds. May be 's' for seconds,'m' for minutes, 'h' for hours, 'd' for days, 'w' for weeks. Default is seconds              |                         |             |
| WARNINGEXPIRES  | Thresholds                                                                                                                                                 |                         |             |
| CRITICALEXPIRES | Thresholds                                                                                                                                                 |                         |             |
| CRITICALSTATUS  | Define the conditions to match for the status to be CRITICAL (Default: '%\{status\} =~ /expired/i'). You can use the following variables: %\{name\}, %\{status\} | %\{status\} =~ /expired/i |             |
| WARNINGSTATUS   | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{name\}, %\{status\}                                       |                         |             |
| EXTRAOPTIONS    | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                                        | --verbose               |             |

</TabItem>
<TabItem value="System" label="System">

| Macro                  | Description                                                                                         | Valeur par défaut | Obligatoire |
|:-----------------------|:----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERVDOM             | Filter vdom by name                                                                                 |                   |             |
| WARNINGCPUUTILIZATION  | Thresholds                                                                                          |                   |             |
| CRITICALCPUUTILIZATION | Thresholds                                                                                          |                   |             |
| WARNINGMEMORYUSAGE     | Thresholds                                                                                          |                   |             |
| CRITICALMEMORYUSAGE    | Thresholds                                                                                          |                   |             |
| WARNINGSESSIONSACTIVE  | Thresholds                                                                                          |                   |             |
| CRITICALSESSIONSACTIVE | Thresholds                                                                                          |                   |             |
| EXTRAOPTIONS           | Any extra option you may want to add to the command (E.g. a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) | --verbose         |             |

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
/usr/lib/centreon/plugins/centreon_fortinet_fortigate_restapi.pl \
	--plugin=network::fortinet::fortigate::restapi::plugin \
	--mode=system \
	--hostname='10.0.0.1' \
	--port='443' \
	--proto='https' \
	--access-token='xxxxxx'  \
	--filter-vdom='' \
	--warning-cpu-utilization='' \
	--critical-cpu-utilization='' \
	--warning-sessions-active='' \
	--critical-sessions-active='' \
	--warning-memory-usage='' \
	--critical-memory-usage='' \
	--verbose
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK: All vdom systems are ok | 'ABS#cpu.utilization.percentage'=0.00%;;;0;100 'ABS#memory.usage.percentage'=0.00%;;;0;100 'ABS#sessions.active.count'=155;;;0; 'ADV#cpu.utilization.percentage'=0.00%;;;0;100 'ADV#memory.usage.percentage'=1.00%;;;0;100 'ADV#sessions.active.count'=553;;;0; 'BGN#cpu.utilization.percentage'=0.00%;;;0;100 'BGN#memory.usage.percentage'=0.00%;;;0;100 'BGN#sessions.active.count'=244;;;0; 'LHE#cpu.utilization.percentage'=0.00%;;;0;100 'LHE#memory.usage.percentage'=0.00%;;;0;100 'LHE#sessions.active.count'=100;;;0; 'MED#cpu.utilization.percentage'=3.00%;;;0;100 'MED#memory.usage.percentage'=11.00%;;;0;100 'MED#sessions.active.count'=6280;;;0; 'MIC#cpu.utilization.percentage'=0.00%;;;0;100 'MIC#memory.usage.percentage'=5.00%;;;0;100 'MIC#sessions.active.count'=3244;;;0; 'MLC#cpu.utilization.percentage'=0.00%;;;0;100 'MLC#memory.usage.percentage'=0.00%;;;0;100 'MLC#sessions.active.count'=431;;;0; 'PRN#cpu.utilization.percentage'=0.00%;;;0;100 'PRN#memory.usage.percentage'=0.00%;;;0;100 'PRN#sessions.active.count'=0;;;0; 'SSTRN#cpu.utilization.percentage'=5.00%;;;0;100 'SSTRN#memory.usage.percentage'=12.00%;;;0;100 'SSTRN#sessions.active.count'=6559;;;0; 'root#cpu.utilization.percentage'=2.00%;;;0;100 'root#memory.usage.percentage'=4.00%;;;0;100 'root#sessions.active.count'=228;;;0;
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
/usr/lib/centreon/plugins/centreon_fortinet_fortigate_restapi.pl \
	--plugin=network::fortinet::fortigate::restapi::plugin \
	--list-mode
```

Le plugin apporte les modes suivants :

| Mode                                                                                                                                 | Modèle de service associé                      |
|:-------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------|
| ha [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/fortinet/fortigate/restapi/mode/ha.pm)]             | Net-Fortinet-Fortigate-Ha-Restapi-custom       |
| health [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/fortinet/fortigate/restapi/mode/health.pm)]     | Net-Fortinet-Fortigate-Health-Restapi-custom   |
| licenses [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/fortinet/fortigate/restapi/mode/licenses.pm)] | Net-Fortinet-Fortigate-Licenses-Restapi-custom |
| system [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/fortinet/fortigate/restapi/mode/system.pm)]     | Net-Fortinet-Fortigate-System-Restapi-custom   |

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
| --filter-perfdata                          | Filter perfdata that match the regexp. Eg: adding --filter-perfdata='avg' will remove all metrics that do not contain 'avg' from performance data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
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
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource Default: 'UTF-8'.      FortiOS Rest API                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --hostname                                 | Set hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --port                                     | Port used (Default: 443)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --proto                                    | Specify https if needed (Default: 'https')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --access-token                             | API token.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --timeout                                  | Set timeout in seconds (Default: 50).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --http-peer-addr                           | Set the address you want to connect to. Useful if hostname is only a vhost, to avoid IP resolution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --proxyurl                                 | Proxy URL. Eg: http://my.proxy:3128                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --proxypac                                 | Proxy pac file (can be a URL or a local file).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --insecure                                 | Accept insecure SSL connections.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --http-backend                             | Perl library to use for HTTP transactions. Possible values are: lwp (default) and curl.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --ssl-opt                                  | Set SSL Options (--ssl-opt="SSL\_version =\> TLSv1" --ssl-opt="SSL\_verify\_mode =\> SSL\_VERIFY\_NONE").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --curl-opt                                 | Set CURL Options (--curl-opt="CURLOPT\_SSL\_VERIFYPEER =\> 0" --curl-opt="CURLOPT\_SSLVERSION =\> CURL\_SSLVERSION\_TLSv1\_1" ).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

#### Options des modes

Les options disponibles pour chaque modèle de services sont listées ci-dessous :

<Tabs groupId="sync">
<TabItem value="Ha" label="Ha">

| Option                   | Description                                                                                              |
|:-------------------------|:---------------------------------------------------------------------------------------------------------|
| --filter-counters        | Only display some counters (regexp can be used). Example: --filter-counters='memory-usage'               |
| --filter-name            | Filter members by name.                                                                                  |
| --warning-* --critical-* | Thresholds. Can be: 'members-detected', 'cpu-utilization' (%), 'memory-usage' (%), 'sessions-active'.    |

</TabItem>
<TabItem value="Health" label="Health">

| Option            | Description                                                                                                                                                   |
|:------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-vdom     | Filter vdom by name.                                                                                                                                          |
| --unknown-health  | Define the conditions to match for the status to be UNKNOWN. You can use the following variables: %\{status\}, %\{name\}                                          |
| --warning-health  | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{status\}, %\{name\}                                          |
| --critical-health | Define the conditions to match for the status to be CRITICAL (Default: '%\{status\} !~ /success/i'). You can use the following variables: %\{status\}, %\{name\}    |

</TabItem>
<TabItem value="Licenses" label="Licenses">

| Option                   | Description                                                                                                                                                   |
|:-------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-name            | Filter licenses by name (can be a regexp).                                                                                                                    |
| --warning-status         | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{name\}, %\{status\}.                                         |
| --critical-status        | Define the conditions to match for the status to be CRITICAL (Default: '%\{status\} =~ /expired/i'). You can use the following variables: %\{name\}, %\{status\}.   |
| --unit                   | Select the unit for expires threshold. May be 's' for seconds,'m' for minutes, 'h' for hours, 'd' for days, 'w' for weeks. Default is seconds.                |
| --warning-* --critical-* | Thresholds. Can be: 'expires'.                                                                                                                                |

</TabItem>
<TabItem value="System" label="System">

| Option                   | Description                                                                                  |
|:-------------------------|:---------------------------------------------------------------------------------------------|
| --filter-counters        | Only display some counters (regexp can be used). Example: --filter-counters='memory-usage'   |
| --filter-vdom            | Filter vdom by name.                                                                         |
| --warning-* --critical-* | Thresholds. Can be: 'cpu-utilization' (%), 'memory-usage' (%), 'sessions-active'.            |

</TabItem>
</Tabs>

Pour un mode, la liste de toutes les options disponibles et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_fortinet_fortigate_restapi.pl \
	--plugin=network::fortinet::fortigate::restapi::plugin \
	--mode=system \
	--help
```
