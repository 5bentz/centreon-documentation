---
id: applications-monitoring-node-exporter-linux
title: Node Exporter Linux Metrics
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Pack assets

### Templates

The Monitoring Connector **Node Exporter Linux Metrics** brings a host template:

* **App-Monitoring-Node-Exporter-Linux-custom**

The connector brings the following service templates (sorted by the host template they are attached to):

<Tabs groupId="sync">
<TabItem value="App-Monitoring-Node-Exporter-Linux-custom" label="App-Monitoring-Node-Exporter-Linux-custom">

| Service Alias | Service Template                                  | Service Description      | Discovery  |
|:--------------|:--------------------------------------------------|:-------------------------|:----------:|
| Node-Cpu      | App-Monitoring-Node-Exporter-Linux-Cpu-custom     | Check node CPU usage     |            |
| Node-Load     | App-Monitoring-Node-Exporter-Linux-Load-custom    | Check node load          |            |
| Node-Memory   | App-Monitoring-Node-Exporter-Linux-Memory-custom  | Check node memory usage  |            |
| Node-Storage  | App-Monitoring-Node-Exporter-Linux-Storage-custom | Check node storage usage | X          |
| Node-Traffic  | App-Monitoring-Node-Exporter-Linux-Traffic-custom | Check node CPU usage     | X          |

> The services listed above are created automatically when the **App-Monitoring-Node-Exporter-Linux-custom** host template is used.

> If **Discovery** is checked, it means a service discovery rule exists for this service template.

</TabItem>
</Tabs>

### Discovery rules

#### Service discovery

| Rule name                                         | Description                                                   |
|:--------------------------------------------------|:--------------------------------------------------------------|
| App-Monitoring-Node-Exporter-Linux-Interface-Name | Discover network interfaces and monitor bandwidth utilization |
| App-Monitoring-Node-Exporter-Linux-Storage-Name   | Discover the disk partitions and monitor space occupation     |

More information about discovering services automatically is available on the [dedicated page](/docs/monitoring/discovery/services-discovery)
and in the [following chapter](/docs/monitoring/discovery/services-discovery/#discovery-rules).

### Collected metrics & status

Here is the list of services for this connector, detailing all metrics linked to each service.

<Tabs groupId="sync">
<TabItem value="Node-Cpu" label="Node-Cpu">

| Metric name                                        | Unit  |
|:---------------------------------------------------|:------|
| cpu.utilization.percentage                         | %     |
| *node_cpu*#node.cpu.idle.utilization.percentage    | %     |
| *node_cpu*#node.cpu.iowait.utilization.percentage  | %     |
| *node_cpu*#node.cpu.irq.utilization.percentage     | %     |
| *node_cpu*#node.cpu.nice.utilization.percentage    | %     |
| *node_cpu*#node.cpu.softirq.utilization.percentage | %     |
| *node_cpu*#node.cpu.steal.utilization.percentage   | %     |
| *node_cpu*#node.cpu.system.utilization.percentage  | %     |
| *node_cpu*#node.cpu.user.utilization.percentage    | %     |

</TabItem>
<TabItem value="Node-Load" label="Node-Load">

| Metric name          | Unit  |
|:---------------------|:------|
| load.1minute.count   | count |
| load.5minutes.count  | count |
| load.15minutes.count | count |

</TabItem>
<TabItem value="Node-Memory" label="Node-Memory">

| Metric name              | Unit  |
|:-------------------------|:------|
| node.memory.usage.bytes  | B     |
| node.memory.buffer.bytes | B     |
| node.memory.cached.bytes | B     |

</TabItem>
<TabItem value="Node-Storage" label="Node-Storage">

| Metric name                               | Unit  |
|:------------------------------------------|:------|
| *disk_name*#node.storage.space.free.bytes | B     |

</TabItem>
<TabItem value="Node-Traffic" label="Node-Traffic">

| Metric name                                | Unit  |
|:-------------------------------------------|:------|
| *interface*~status                         | N/A   |
| *interface*~node.packets.in.count          | count |
| *interface*~node.packets.out.count         | count |
| *interface*~node.traffic.in.bitspersecond  | b/s   |
| *interface*~node.traffic.out.bitspersecond | b/s   |

</TabItem>
</Tabs>

## Prerequisites

To install Node exporter on your Linux server please refer to this documentation: https://prometheus.io/docs/guides/node-exporter/#installing-and-running-the-node-exporter. 

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
dnf install centreon-pack-applications-monitoring-node-exporter-linux
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-applications-monitoring-node-exporter-linux
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-pack-applications-monitoring-node-exporter-linux
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-applications-monitoring-node-exporter-linux
```

</TabItem>
</Tabs>

2. Whatever the license type (*online* or *offline*), install the **Node Exporter Linux Metrics** connector through
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
dnf install centreon-plugin-Applications-Monitoring-Nodeexporter-Linux
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Applications-Monitoring-Nodeexporter-Linux
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-plugin-applications-monitoring-nodeexporter-linux
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Applications-Monitoring-Nodeexporter-Linux
```

</TabItem>
</Tabs>

## Using the monitoring connector

### Using a host template provided by the connector

1. Log into Centreon and add a new host through **Configuration > Hosts**.
2. Fill in the **Name**, **Alias** & **IP Address/DNS** fields according to your resource's settings.
3. Apply the **App-Monitoring-Node-Exporter-Linux-custom** template to the host. A list of macros appears. Macros allow you to define how the connector will connect to the resource, and to customize the connector's behavior.
4. Fill in the macros you want. Some macros are mandatory.

| Macro             | Description                                                                                          | Default value     | Mandatory   |
|:------------------|:-----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| NODEEXPORTERPROTO | Specify https if needed (default: 'http')                                                            | http              |             |
| NODEEXPORTERURL   | URL to scrape metrics from (default: '/metrics')                                                     | /metrics          |             |
| NODEEXPORTERPORT  | Port used                                                                             | 9100              |             |
| EXTRAOPTIONS      | Any extra option you may want to add to every command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

5. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The host appears in the list of hosts, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the host: it shows the values of the macros.

### Using a service template provided by the connector

1. If you have used a host template and checked **Create Services linked to the Template too**, the services linked to the template have been created automatically, using the corresponding service templates. Otherwise, [create manually the services you want](/docs/monitoring/basic-objects/services) and apply a service template to them.
2. Fill in the macros you want (e.g. to change the thresholds for the alerts). Some macros are mandatory (see the table below).

<Tabs groupId="sync">
<TabItem value="Node-Cpu" label="Node-Cpu">

| Macro           | Description                                                                                        | Default value     | Mandatory   |
|:----------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNINGAVERAGE  | Warning threshold                                                                                  |                   |             |
| CRITICALAVERAGE | Critical threshold                                                                                 |                   |             |
| WARNINGIDLE     | Warning threshold                                                                                  |                   |             |
| CRITICALIDLE    | Critical threshold                                                                                 |                   |             |
| WARNINGIOWAIT   | Warning threshold                                                                                  |                   |             |
| CRITICALIOWAIT  | Critical threshold                                                                                 |                   |             |
| WARNINGIRQ      | Warning threshold                                                                                  |                   |             |
| CRITICALIRQ     | Critical threshold                                                                                 |                   |             |
| WARNINGNICE     | Warning threshold                                                                                  |                   |             |
| CRITICALNICE    | Critical threshold                                                                                 |                   |             |
| WARNINGSOFTIRQ  | Warning threshold                                                                                  |                   |             |
| CRITICALSOFTIRQ | Critical threshold                                                                                 |                   |             |
| WARNINGSTEAL    | Warning threshold                                                                                  |                   |             |
| CRITICALSTEAL   | Critical threshold                                                                                 |                   |             |
| WARNINGSYSTEM   | Warning threshold                                                                                  |                   |             |
| CRITICALSYSTEM  | Critical threshold                                                                                 |                   |             |
| WARNINGUSER     | Warning threshold                                                                                  |                   |             |
| CRITICALUSER    | Critical threshold                                                                                 |                   |             |
| EXTRAOPTIONS    | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

</TabItem>
<TabItem value="Node-Load" label="Node-Load">

| Macro         | Description                                                                                        | Default value     | Mandatory   |
|:--------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNINGLOAD1  | Warning threshold                                                                                  |                   |             |
| WARNINGLOAD15 | Warning threshold                                                                                  |                   |             |
| WARNINGLOAD5  | Warning threshold                                                                                  |                   |             |
| EXTRAOPTIONS  | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

</TabItem>
<TabItem value="Node-Memory" label="Node-Memory">

| Macro          | Description                                                                                        | Default value     | Mandatory   |
|:---------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| UNITS          | Units of thresholds. Can be : '%', 'B' Default: '%'                                                | %                 |             |
| WARNINGBUFFER  | Warning threshold                                                                                  |                   |             |
| CRITICALBUFFER | Critical threshold                                                                                 |                   |             |
| WARNINGCACHED  | Warning threshold                                                                                  |                   |             |
| CRITICALCACHED | Critical threshold                                                                                 |                   |             |
| WARNINGUSAGE   | Warning threshold                                                                                  |                   |             |
| CRITICALUSAGE  | Critical threshold                                                                                 |                   |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

</TabItem>
<TabItem value="Node-Storage" label="Node-Storage">

| Macro         | Description                                                                                        | Default value     | Mandatory   |
|:--------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FSTYPE        | Inclusion filter on fstype.  Can be used to exclude fstypes. Example : --fstype='^(?!(tmpfs))'     | ^(?!(tmpfs))      |             |
| PARTITIONNAME | Specify which disk to monitor. Can be a regex.  Default: all disks are monitored                   | .*                |             |
| UNITS         | Units of thresholds. Can be : '%', 'B' Default: '%'                                                | %                 |             |
| WARNINGUSAGE  | Warning threshold                                                                                  |                   |             |
| CRITICALUSAGE | Critical threshold                                                                                 |                   |             |
| EXTRAOPTIONS  | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

</TabItem>
<TabItem value="Node-Traffic" label="Node-Traffic">

| Macro              | Description                                                                                                              | Default value     | Mandatory   |
|:-------------------|:-------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| INTERFACENAME      | Specify which interface to monitor. Can be a regex.          Default: all interfaces are monitored except 'lo' interface | ^(?!(lo$))        |             |
| WARNINGPACKETSIN   | Warning thresholds                                                                                                       |                   |             |
| CRITICALPACKETSIN  | Critical thresholds                                                                                                      |                   |             |
| WARNINGPACKETSOUT  | Warning thresholds                                                                                                       |                   |             |
| CRITICALPACKETSOUT | Critical thresholds                                                                                                      |                   |             |
| WARNINGTRAFFICIN   | Warning thresholds                                                                                                       |                   |             |
| CRITICALTRAFFICIN  | Critical thresholds                                                                                                      |                   |             |
| WARNINGTRAFFICOUT  | Warning thresholds                                                                                                       |                   |             |
| CRITICALTRAFFICOUT | Critical thresholds                                                                                                      |                   |             |
| EXTRAOPTIONS       | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options).                       |                   |             |

</TabItem>
</Tabs>

3. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The service appears in the list of services, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the service: it shows the values of the macros.

## How to check in the CLI that the configuration is OK and what are the main options for?

Once the plugin is installed, log into your Centreon poller's CLI using the
**centreon-engine** user account (`su - centreon-engine`). Test that the connector 
is able to monitor a resource using a command like this one (replace the sample values by yours):

```bash
/usr/lib/centreon/plugins/centreon_monitoring_nodeexporter_linux.pl \
	--plugin=apps::monitoring::nodeexporter::linux::plugin \
	--mode=traffic \
	--hostname=10.0.0.1 \
	--urlpath='/metrics' \
	--port='9100' \
	--proto='http'  \
	--interface='^(?!(lo$))' \
	--warning-traffic-in='' \
	--critical-traffic-in='' \
	--warning-traffic-out='' \
	--critical-traffic-out='' \
	--warning-packets-in='' \
	--critical-packets-in='' \
	--warning-packets-out='' \
	--critical-packets-out='' 
```

The expected command output is shown below:

```bash
OK: packets in: 45 packets out: 92 traffic in: 9 9/s traffic in: 1 1/s | '*interface*~node.packets.in.count'=45;;;0;'*interface*~node.packets.out.count'=92;;;0;'*interface*~node.traffic.in.bitspersecond'=9b/s;;;0;'*interface*~node.traffic.out.bitspersecond'=1b/s;;;0;
```

### Troubleshooting

Please find the [troubleshooting documentation](../getting-started/how-to-guides/troubleshooting-plugins.md)
for Centreon Plugins typical issues.

### Available modes

In most cases, a mode corresponds to a service template. The mode appears in the execution command for the connector.
In the Centreon interface, you don't need to specify a mode explicitly: its use is implied when you apply a service template.
However, you will need to specify the correct mode for the template if you want to test the execution command for the 
connector in your terminal.

All available modes can be displayed by adding the `--list-mode` parameter to
the command:

```bash
/usr/lib/centreon/plugins/centreon_monitoring_nodeexporter_linux.pl \
	--plugin=apps::monitoring::nodeexporter::linux::plugin \
	--list-mode
```

The plugin brings the following modes:

| Mode                                                                                                                                              | Linked service template                           |
|:--------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------|
| cpu [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/linux/mode/cpu.pm)]                        | App-Monitoring-Node-Exporter-Linux-Cpu-custom     |
| list-interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/linux/mode/listinterfaces.pm)] | Used for service discovery                        |
| list-storages [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/linux/mode/liststorages.pm)]     | Used for service discovery                        |
| load [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/linux/mode/load.pm)]                      | App-Monitoring-Node-Exporter-Linux-Load-custom    |
| memory [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/linux/mode/memory.pm)]                  | App-Monitoring-Node-Exporter-Linux-Memory-custom  |
| storage [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/linux/mode/storage.pm)]                | App-Monitoring-Node-Exporter-Linux-Storage-custom |
| traffic [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/apps/monitoring/nodeexporter/linux/mode/traffic.pm)]                | App-Monitoring-Node-Exporter-Linux-Traffic-custom |

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

#### Modes options

All available options for each service template are listed below:

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
| --warning-*            | Warning threshold.  Can be: 'average', 'idle', 'iowait', 'nice', 'irq' 'softirq', 'steal', 'system', 'user'                                                                                                                                   |
| --critical-*           | Critical threshold.  Can be: 'average', 'idle', 'iowait', 'nice', 'irq' 'softirq', 'steal', 'system', 'user'                                                                                                                                  |

</TabItem>
<TabItem value="Node-Load" label="Node-Load">

| Option       | Description                                                |
|:-------------|:-----------------------------------------------------------|
| --warning-*  | Warning threshold.  Can be: 'load1', 'load5', 'load15'.    |
| --critical-* | Warning threshold.  Can be: 'load1', 'load5', 'load15'.    |

</TabItem>
<TabItem value="Node-Memory" label="Node-Memory">

| Option       | Description                                                  |
|:-------------|:-------------------------------------------------------------|
| --units      | Units of thresholds. Can be : '%', 'B' Default: '%'          |
| --warning-*  | Warning threshold.  Can be: 'usage', 'buffer', 'cached'.     |
| --critical-* | Critical threshold.  Can be: 'usage', 'buffer', 'cached'.    |

</TabItem>
<TabItem value="Node-Storage" label="Node-Storage">

| Option           | Description                                                                                      |
|:-----------------|:-------------------------------------------------------------------------------------------------|
| --fstype         | Inclusion filter on fstype.  Can be used to exclude fstypes. Example : --fstype='^(?!(tmpfs))'   |
| --storage        | Specify which disk to monitor. Can be a regex.  Default: all disks are monitored.                |
| --units          | Units of thresholds. Can be : '%', 'B' Default: '%'                                              |
| --warning-usage  | Warning threshold.                                                                               |
| --critical-usage | Critical threshold.                                                                              |

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
| --interface            |         Specify which interface to monitor. Can be a regex.          Default: all interfaces are monitored except 'lo' interface.                                                                                                             |
| --warning-*            |         Warning thresholds.          Can be: 'traffic-in', 'traffic-out', 'packets-in', 'packets-out'.                                                                                                                                        |
| --critical-*           |         Critical thresholds.          Can be: 'traffic-in', 'traffic-out', 'packets-in', 'packets-out'.                                                                                                                                       |

</TabItem>
</Tabs>

All available options for a given mode can be displayed by adding the
`--help` parameter to the command:

```bash
/usr/lib/centreon/plugins/centreon_monitoring_nodeexporter_linux.pl \
	--plugin=apps::monitoring::nodeexporter::linux::plugin \
	--mode=traffic \
	--help
```
