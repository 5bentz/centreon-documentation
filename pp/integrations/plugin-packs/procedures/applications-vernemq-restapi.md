---
id: applications-vernemq-restapi
title: VerneMQ Restapi
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

VerneMQ is a scalable and open source MQTT broker that connects IoT, M2M, mobile and web applications.
The VerneMQ Monitoring Connector monitors Clusters, Listeners, Plugins and sessions using the RestAPI.

## Pack assets

### Templates

The Monitoring Connector **Verne MQ RestAPI** brings a host template:

* **App-Vernemq-Restapi-custom**

The connector brings the following service templates (sorted by the host template they are attached to):

<Tabs groupId="sync">
<TabItem value="App-Vernemq-Restapi-custom" label="App-Vernemq-Restapi-custom">

| Service Alias | Service Template                     | Service Description |
|:--------------|:-------------------------------------|:--------------------|
| Clusters      | App-Vernemq-Clusters-Restapi-custom  | Check clusters      |
| Listeners     | App-Vernemq-Listeners-Restapi-custom | Check listeners     |
| Plugins       | App-Vernemq-Plugins-Restapi-custom   | Check plugins       |
| Sessions      | App-Vernemq-Sessions-Restapi-custom  | Check sessions      |

> The services listed above are created automatically when the **App-Vernemq-Restapi-custom** host template is used.

</TabItem>
</Tabs>

### Collected metrics & status

Here is the list of services for this connector, detailing all metrics linked to each service.

<Tabs groupId="sync">
<TabItem value="Clusters" label="Clusters">

| Metric name               | Unit  |
|:--------------------------|:------|
| clusters.running.count    | count |
| clusters.notrunning.count | count |
| *clusters*#status         | N/A   |

</TabItem>
<TabItem value="Listeners" label="Listeners">

| Metric name                | Unit  |
|:---------------------------|:------|
| listeners.running.count    | count |
| listeners.notrunning.count | count |
| *listeners*#status         | N/A   |

</TabItem>
<TabItem value="Plugins" label="Plugins">

| Metric name         | Unit  |
|:--------------------|:------|
| plugins.total.count | count |

</TabItem>
<TabItem value="Sessions" label="Sessions">

| Metric name           | Unit  |
|:----------------------|:------|
| sessions.online.count | count |
| sessions.total.count  | count |

</TabItem>
</Tabs>

## Prerequisites

A number of distributions provide VerneMQ, including pre-built binary packages.
Support for these builds, if any, is being provided by the associated distribution vendor.
Their release cycle may lag behind VerneMQ source releases.

More information is available in the official documentation for VerneMQ : https://docs.vernemq.com/getting-started

The VerneMQ HTTP API is enabled by default and installs an HTTP handler on `http://myvernemq.com:8888/api/v1`.
The **centreon-engine** user performs a RestAPI request to this system. 
You must have generated one token on the VerneMQ server with the following command :

```bash
$ vmq-admin api-key create
```

More information on the VerneMQ HTTP API on : https://docs.vernemq.com/administration/http-administration#managing-api-keys

## Installing the monitoring connector

### Pack

1. If the platform uses an *online* license, you can skip the package installation
instruction below as it is not required to have the connector displayed within the
**Configuration > Monitoring Connector Manager** menu.
If the platform uses an *offline* license, install the package on the **central server**
with the command corresponding to the operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-pack-applications-vernemq-restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-applications-vernemq-restapi
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-pack-applications-vernemq-restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-applications-vernemq-restapi
```

</TabItem>
</Tabs>

2. Whatever the license type (*online* or *offline*), install the **Verne MQ RestAPI** connector through
the **Configuration > Monitoring Connector Manager** menu.

### Plugin

Since Centreon 22.04, you can benefit from the 'Automatic plugin installation' feature.
When this feature is enabled, you can skip the installation part below.

You still have to manually install the plugin on the poller(s) when:
- Automatic plugin installation is turned off
- You want to run a discovery job from a poller that doesn't monitor any resource of this kind yet

> More information in the [Installing the plugin](/docs/monitoring/pluginpacks/#installing-the-plugin) section.

Use the commands below according to your operating system's package manager:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```bash
dnf install centreon-plugin-Applications-Vernemq-Restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Applications-Vernemq-Restapi
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```bash
apt install centreon-plugin-applications-vernemq-restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Applications-Vernemq-Restapi
```

</TabItem>
</Tabs>

## Using the monitoring connector

### Using a host template provided by the connector

1. Log into Centreon and add a new host through **Configuration > Hosts**.
2. Fill in the **Name**, **Alias** & **IP Address/DNS** fields according to your resource's settings.
3. Apply the **App-Vernemq-Restapi-custom** template to the host. A list of macros appears. Macros allow you to define how the connector will connect to the resource, and to customize the connector's behavior.
4. Fill in the macros you want. Some macros are mandatory.

| Macro           | Description                                                                                          | Default value     | Mandatory   |
|:----------------|:-----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| APIPROTO        | Specify https if needed (default: 'http')                                                            | http              |             |
| APIPORT         | Port used (default: 8888)                                                                            | 8888              |             |
| APIKEY          | VerneMQ API Token                                                                                    |                   | X           |
| APIEXTRAOPTIONS | Any extra option you may want to add to every command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

5. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The host appears in the list of hosts, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the host: it shows the values of the macros.

### Using a service template provided by the connector

1. If you have used a host template and checked **Create Services linked to the Template too**, the services linked to the template have been created automatically, using the corresponding service templates. Otherwise, [create manually the services you want](/docs/monitoring/basic-objects/services) and apply a service template to them.
2. Fill in the macros you want (e.g. to change the thresholds for the alerts). Some macros are mandatory (see the table below).

<Tabs groupId="sync">
<TabItem value="Clusters" label="Clusters">

| Macro              | Description                                                                                                                                                     | Default value             | Mandatory   |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------|:-----------:|
| FILTERNAME         | Filter cluster name (can be a regexp)                                                                                                                           |                           |             |
| UNKNOWNSTATUS      | Define the conditions to match for the status to be UNKNOWN. You can use the following variables: %\{status\}, %\{display\}                                         |                           |             |
| WARNINGNOTRUNNING  | Thresholds                                                                                                                                                      |                           |             |
| CRITICALNOTRUNNING | Thresholds                                                                                                                                                      |                           |             |
| WARNINGRUNNING     | Thresholds                                                                                                                                                      |                           |             |
| CRITICALRUNNING    | Thresholds                                                                                                                                                      |                           |             |
| CRITICALSTATUS     | Define the conditions to match for the status to be CRITICAL (default: '%\{status\} eq "notRunning"'). You can use the following variables: %\{status\}, %\{display\} | %\{status\} eq "notRunning" |             |
| WARNINGSTATUS      | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{status\}, %\{display\}                                         |                           |             |
| EXTRAOPTIONS       | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options).                                                              | --verbose                 |             |

</TabItem>
<TabItem value="Listeners" label="Listeners">

| Macro              | Description                                                                                                                                                  | Default value          | Mandatory   |
|:-------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------|:-----------:|
| FILTERTYPE         | Filter listener type (can be a regexp)                                                                                                                       |                        |             |
| UNKNOWNSTATUS      | Define the conditions to match for the status to be UNKNOWN. You can use the following variables: %\{status\}, %\{display\}                                      |                        |             |
| WARNINGNOTRUNNING  | Thresholds                                                                                                                                                   |                        |             |
| CRITICALNOTRUNNING | Thresholds                                                                                                                                                   |                        |             |
| WARNINGRUNNING     | Thresholds                                                                                                                                                   |                        |             |
| CRITICALRUNNING    | Thresholds                                                                                                                                                   |                        |             |
| CRITICALSTATUS     | Define the conditions to match for the status to be CRITICAL (default: '%\{status\} ne "running"'). You can use the following variables: %\{status\}, %\{display\} | %\{status\} ne "running" |             |
| WARNINGSTATUS      | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{status\}, %\{display\}                                      |                        |             |
| EXTRAOPTIONS       | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options).                                                           | --verbose              |             |

</TabItem>
<TabItem value="Plugins" label="Plugins">

| Macro         | Description                                                                                        | Default value     | Mandatory   |
|:--------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERNAME    | Filter plugin name (can be a regexp)                                                               |                   |             |
| WARNINGTOTAL  | Thresholds                                                                                         |                   |             |
| CRITICALTOTAL | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS  | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). | --verbose         |             |

</TabItem>
<TabItem value="Sessions" label="Sessions">

| Macro          | Description                                                                                        | Default value     | Mandatory   |
|:---------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| CRTICALTOTAL   | Thresholds                                                                                         |                   |             |
| WARNINGONLINE  | Thresholds                                                                                         |                   |             |
| CRITICALONLINE | Thresholds                                                                                         |                   |             |
| WARNINGTOTAL   | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). | --verbose         |             |

</TabItem>
</Tabs>

3. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The service appears in the list of services, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the service: it shows the values of the macros.

## How to check in the CLI that the configuration is OK and what are the main options for?

Once the plugin is installed, log into your Centreon poller's CLI using the
**centreon-engine** user account (`su - centreon-engine`). Test that the connector 
is able to monitor a resource using a command like this one (replace the sample values by yours):

```bash
/usr/lib/centreon/plugins/centreon_vernemq_restapi.pl \
	--plugin=apps::mq::vernemq::restapi::plugin \
	--mode='sessions' \
	--hostname='10.0.0.1' \
	--port='8888' \
	--proto='http' \
	--api-key=''  \
	--warning-total='' \
	--critical-total='' \
	--warning-online='' \
	--critical-online='' \
	--verbose
```

The expected command output is shown below:

```bash
OK: current online: 47 current total: 47 | 'sessions.online.count'=47;;;0;'sessions.total.count'=47;;;0;
```

### Troubleshooting

Please find the troubleshooting documentation for the API-based plugins in
this [chapter](../getting-started/how-to-guides/troubleshooting-plugins.md#http-and-api-checks).

### Available modes

In most cases, a mode corresponds to a service template. The mode appears in the execution command for the connector.
In the Centreon interface, you don't need to specify a mode explicitly: its use is implied when you apply a service template.
However, you will need to specify the correct mode for the template if you want to test the execution command for the 
connector in your terminal.

All available modes can be displayed by adding the `--list-mode` parameter to
the command:

```bash
/usr/lib/centreon/plugins/centreon_vernemq_restapi.pl \
	--plugin=apps::mq::vernemq::restapi::plugin \
	--list-mode
```

The plugin brings the following modes:

| Mode                                                                                                                        | Linked service template              |
|:----------------------------------------------------------------------------------------------------------------------------|:-------------------------------------|
| clusters [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/mq/vernemq/restapi/mode/clusters.pm)]   | App-Vernemq-Clusters-Restapi-custom  |
| listeners [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/mq/vernemq/restapi/mode/listeners.pm)] | App-Vernemq-Listeners-Restapi-custom |
| plugins [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/mq/vernemq/restapi/mode/plugins.pm)]     | App-Vernemq-Plugins-Restapi-custom   |
| sessions [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/mq/vernemq/restapi/mode/sessions.pm)]   | App-Vernemq-Sessions-Restapi-custom  |

### Available options

#### Generic options

All generic options are listed here:

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
| --source-encoding                          | Define the character encoding of the response sent by the monitored resource Default: 'UTF-8'.      VerneMQ Rest API                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --hostname                                 | Set hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --port                                     | Port used (default: 8888)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --proto                                    | Specify https if needed (default: 'http')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --api-key                                  | VerneMQ API Token.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --timeout                                  | Set timeout in seconds (default: 10).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --http-peer-addr                           | Set the address you want to connect to. Useful if hostname is only a vhost, to avoid IP resolution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --proxyurl                                 | Proxy URL. Example: http://my.proxy:3128                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --proxypac                                 | Proxy pac file (can be a URL or a local file).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --insecure                                 | Accept insecure SSL connections.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --http-backend                             | Perl library to use for HTTP transactions. Possible values are: lwp (default) and curl.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --ssl-opt                                  | Set SSL Options (--ssl-opt="SSL\_version =\> TLSv1" --ssl-opt="SSL\_verify\_mode =\> SSL\_VERIFY\_NONE").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --curl-opt                                 | Set CURL Options (--curl-opt="CURLOPT\_SSL\_VERIFYPEER =\> 0" --curl-opt="CURLOPT\_SSLVERSION =\> CURL\_SSLVERSION\_TLSv1\_1" ).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

#### Modes options

All available options for each service template are listed below:

<Tabs groupId="sync">
<TabItem value="Clusters" label="Clusters">

| Option                   | Description                                                                                                                                                       |
|:-------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-name            | Filter cluster name (can be a regexp).                                                                                                                            |
| --unknown-status         | Define the conditions to match for the status to be UNKNOWN. You can use the following variables: %\{status\}, %\{display\}                                           |
| --warning-status         | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{status\}, %\{display\}                                           |
| --critical-status        | Define the conditions to match for the status to be CRITICAL (default: '%\{status\} eq "notRunning"'). You can use the following variables: %\{status\}, %\{display\}   |
| --warning-* --critical-* | Thresholds. Can be: 'running', 'notrunning'.                                                                                                                      |

</TabItem>
<TabItem value="Listeners" label="Listeners">

| Option                   | Description                                                                                                                                                    |
|:-------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-type            | Filter listener type (can be a regexp).                                                                                                                        |
| --unknown-status         | Define the conditions to match for the status to be UNKNOWN. You can use the following variables: %\{status\}, %\{display\}                                        |
| --warning-status         | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{status\}, %\{display\}                                        |
| --critical-status        | Define the conditions to match for the status to be CRITICAL (default: '%\{status\} ne "running"'). You can use the following variables: %\{status\}, %\{display\}   |
| --warning-* --critical-* | Thresholds. Can be: 'running', 'notrunning'.                                                                                                                   |

</TabItem>
<TabItem value="Plugins" label="Plugins">

| Option                   | Description                             |
|:-------------------------|:----------------------------------------|
| --filter-name            | Filter plugin name (can be a regexp).   |
| --warning-* --critical-* | Thresholds. Can be: 'total'.            |

</TabItem>
<TabItem value="Sessions" label="Sessions">

| Option                   | Description                               |
|:-------------------------|:------------------------------------------|
| --warning-* --critical-* | Thresholds. Can be: 'total', 'online'.    |

</TabItem>
</Tabs>

All available options for a given mode can be displayed by adding the
`--help` parameter to the command:

```bash
/usr/lib/centreon/plugins/centreon_vernemq_restapi.pl \
	--plugin=apps::mq::vernemq::restapi::plugin \
	--mode='sessions' \
	--help
```
