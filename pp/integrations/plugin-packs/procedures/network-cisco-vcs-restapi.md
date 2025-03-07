---
id: network-cisco-vcs-restapi
title: Cisco VCS
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Pack assets

### Templates

The Monitoring Connector **Cisco VCS Rest API** brings a host template:

* **Net-Cisco-Vcs-Restapi-custom**

The connector brings the following service templates (sorted by the host template they are attached to):

<Tabs groupId="sync">
<TabItem value="Net-Cisco-Vcs-Restapi-custom" label="Net-Cisco-Vcs-Restapi-custom">

| Service Alias    | Service Template                              | Service Description                                         |
|:-----------------|:----------------------------------------------|:------------------------------------------------------------|
| Alerts           | Net-Cisco-Vcs-Alerts-Restapi-custom           | Check alerts                                                |
| Calls            | Net-Cisco-Vcs-Calls-Restapi-custom            | Check calls                                                 |
| Http-Proxy-Stats | Net-Cisco-Vcs-Http-Proxy-Stats-Restapi-custom | Check HTTP proxy status and statistics                      |
| Zones            | Net-Cisco-Vcs-Zones-Restapi-custom            | Check zone status, call count by zones and search count |

> The services listed above are created automatically when the **Net-Cisco-Vcs-Restapi-custom** host template is used.

</TabItem>
</Tabs>

### Collected metrics & status

Here is the list of services for this connector, detailing all metrics linked to each service.

<Tabs groupId="sync">
<TabItem value="Alerts" label="Alerts">

| Metric name                         | Unit  |
|:------------------------------------|:------|
| alerts.total.count                  | count |
| alerts.acknowledged.current.count   | count |
| alerts.unacknowledged.current.count | count |

</TabItem>
<TabItem value="Calls" label="Calls">

| Metric name | Unit  |
|:------------|:------|
| dummy       | N/A   |

</TabItem>
<TabItem value="Http-Proxy-Stats" label="Http-Proxy-Stats">

| Metric name                           | Unit  |
|:--------------------------------------|:------|
| status                                | N/A   |
| httproxy.connections.client.persecond | N/A   |
| httproxy.connections.server.persecond | N/A   |
| httproxy.requests.completed.persecond | N/A   |
| httproxy.requests.get.persecond       | N/A   |
| httproxy.requests.post.persecond      | N/A   |
| httproxy.responses.1xx.persecond      | N/A   |
| httproxy.responses.2xx.persecond      | N/A   |
| httproxy.responses.3xx.persecond      | N/A   |
| httproxy.responses.4xx.persecond      | N/A   |
| httproxy.responses.5xx.persecond      | N/A   |

</TabItem>
<TabItem value="Zones" label="Zones">

| Metric name                              | Unit  |
|:-----------------------------------------|:------|
| zones.total.count                        | count |
| zones.searches.total.persecond           | N/A   |
| zones.searches.dropped.persecond         | N/A   |
| zones.searches.maxsub.exceeded.count     | count |
| zones.searches.maxtargets.exceeded.count | count |
| *zones*#status                           | N/A   |
| *zones*#zone.calls.current.count         | count |

</TabItem>
</Tabs>

## Prerequisites

To monitor your Cisco VCS, the Rest API must be configured (you must have a username/password pair to authenticate to it).
For more information see the [Rest API documentation](https://www.cisco.com/c/en/us/support/unified-communications/telepresence-video-communication-server-vcs/products-installation-and-configuration-guides-list.html)

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
dnf install centreon-pack-network-cisco-vcs-restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-network-cisco-vcs-restapi
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-pack-network-cisco-vcs-restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-network-cisco-vcs-restapi
```

</TabItem>
</Tabs>

2. Whatever the license type (*online* or *offline*), install the **Cisco VCS Rest API** connector through
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
dnf install centreon-plugin-Network-Cisco-Vcs-Restapi
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Network-Cisco-Vcs-Restapi
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-plugin-network-cisco-vcs-restapi
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Network-Cisco-Vcs-Restapi
```

</TabItem>
</Tabs>

## Using the monitoring connector

### Using a host template provided by the connector

1. Log into Centreon and add a new host through **Configuration > Hosts**.
2. Fill in the **Name**, **Alias** & **IP Address/DNS** fields according to your resource's settings.
3. Apply the **Net-Cisco-Vcs-Restapi-custom** template to the host. A list of macros appears. Macros allow you to define how the connector will connect to the resource, and to customize the connector's behavior.
4. Fill in the macros you want. Some macros are mandatory.

| Macro              | Description                                                                                                                              | Default value     | Mandatory   |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| VCSAPIUSERNAME     | Set API username                                                                                                                         |                   | X           |
| VCSAPIPASSWORD     | Set API password                                                                                                                         |                   | X           |
| VCSAPIPROTO        | Specify https if needed (default: 'https')                                                                                               | https             |             |
| VCSAPIPORT         | API port (default: 443)                                                                                                                  | 443               |             |
| VCSAPIEXTRAOPTIONS | Any extra option you may want to add to every command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

5. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The host appears in the list of hosts, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the host: it shows the values of the macros.

### Using a service template provided by the connector

1. If you have used a host template and checked **Create Services linked to the Template too**, the services linked to the template have been created automatically, using the corresponding service templates. Otherwise, [create manually the services you want](/docs/monitoring/basic-objects/services) and apply a service template to them.
2. Fill in the macros you want (e.g. to change the thresholds for the alerts). Some macros are mandatory (see the table below).

<Tabs groupId="sync">
<TabItem value="Alerts" label="Alerts">

| Macro                  | Description                                                                                                                            | Default value              | Mandatory   |
|:-----------------------|:---------------------------------------------------------------------------------------------------------------------------------------|:---------------------------|:-----------:|
| FILTERCOUNTERS         | Only display some counters (regexp can be used). (example: --filter-counters='responses')                                              |                            |             |
| FILTERREASON           | Filter alerts by reason (can use regexp)                                                                                               |                            |             |
| WARNINGACKNOWLEDGED    | Thresholds                                                                                                                             |                            |             |
| CRITICALACKNOWLEDGED   | Thresholds                                                                                                                             |                            |             |
| WARNINGTOTAL           | Thresholds                                                                                                                             |                            |             |
| CRITICALTOTAL          | Thresholds                                                                                                                             |                            |             |
| WARNINGUNACKNOWLEDGED  | Thresholds                                                                                                                             |                            |             |
| CRITICALUNACKNOWLEDGED | Thresholds                                                                                                                             |                            |             |
| EXTRAOPTIONS           | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). | --verbose --display-alerts |             |

</TabItem>
<TabItem value="Calls" label="Calls">

| Macro                            | Description                                                                                                                            | Default value     | Mandatory   |
|:---------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERCOUNTERS                   | Only display some counters (regexp can be used). (example: --filter-counters='responses')                                              |                   |             |
| WARNINGCLOUDCURRENT              | Thresholds                                                                                                                             |                   |             |
| CRITICALCLOUDCURRENT             | Thresholds                                                                                                                             |                   |             |
| WARNINGCLOUDTOTAL                | Thresholds                                                                                                                             |                   |             |
| CRITICALCLOUDTOTAL               | Thresholds                                                                                                                             |                   |             |
| WARNINGCOLLABORATIONEDGECURRENT  | Thresholds                                                                                                                             |                   |             |
| CRITICALCOLLABORATIONEDGECURRENT | Thresholds                                                                                                                             |                   |             |
| WARNINGCOLLABORATIONEDGETOTAL    | Thresholds                                                                                                                             |                   |             |
| CRITICALCOLLABORATIONEDGETOTAL   | Thresholds                                                                                                                             |                   |             |
| WARNINGCONNECTIONFAILEDTOTAL     | Thresholds                                                                                                                             |                   |             |
| CRITICALCONNECTIONFAILEDTOTAL    | Thresholds                                                                                                                             |                   |             |
| WARNINGDISCONNECTEDTOTAL         | Thresholds                                                                                                                             |                   |             |
| CRITICALDISCONNECTEDTOTAL        | Thresholds                                                                                                                             |                   |             |
| WARNINGMICROSOFTCONTENTCURRENT   | Thresholds                                                                                                                             |                   |             |
| CRITICALMICROSOFTCONTENTCURRENT  | Thresholds                                                                                                                             |                   |             |
| WARNINGMICROSOFTCONTENTTOTAL     | Thresholds                                                                                                                             |                   |             |
| CRITICALMICROSOFTCONTENTTOTAL    | Thresholds                                                                                                                             |                   |             |
| WARNINGMICROSOFTIMPCURRENT       | Thresholds                                                                                                                             |                   |             |
| CRITICALMICROSOFTIMPCURRENT      | Thresholds                                                                                                                             |                   |             |
| WARNINGMICROSOFTIMPTOTAL         | Thresholds                                                                                                                             |                   |             |
| CRITICALMICROSOFTIMPTOTAL        | Thresholds                                                                                                                             |                   |             |
| WARNINGNONTRAVERSALCURRENT       | Thresholds                                                                                                                             |                   |             |
| CRITICALNONTRAVERSALCURRENT      | Thresholds                                                                                                                             |                   |             |
| WARNINGNONTRAVERSALTOTAL         | Thresholds                                                                                                                             |                   |             |
| CRITICALNONTRAVERSALTOTAL        | Thresholds                                                                                                                             |                   |             |
| WARNINGTRAVERSALCURRENT          | Thresholds                                                                                                                             |                   |             |
| CRITICALTRAVERSALCURRENT         | Thresholds                                                                                                                             |                   |             |
| WARNINGTRAVERSALTOTAL            | Thresholds                                                                                                                             |                   |             |
| CRITICALTRAVERSALTOTAL           | Thresholds                                                                                                                             |                   |             |
| EXTRAOPTIONS                     | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). |                   |             |

</TabItem>
<TabItem value="Http-Proxy-Stats" label="Http-Proxy-Stats">

| Macro                     | Description                                                                                                                            | Default value         | Mandatory   |
|:--------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|:----------------------|:-----------:|
| FILTERCOUNTERS            | Only display some counters (regexp can be used). (example: --filter-counters='responses')                                              |                       |             |
| WARNINGCONNECTIONSCLIENT  | Threshold                                                                                                                              |                       |             |
| CRITICALCONNECTIONSCLIENT | Threshold                                                                                                                              |                       |             |
| WARNINGCONNECTIONSSERVER  | Threshold                                                                                                                              |                       |             |
| CRITICALCONNECTIONSSERVER | Threshold                                                                                                                              |                       |             |
| WARNINGREQUESTSCOMPLETED  | Threshold                                                                                                                              |                       |             |
| CRITICALREQUESTSCOMPLETED | Threshold                                                                                                                              |                       |             |
| WARNINGREQUESTSGET        | Threshold                                                                                                                              |                       |             |
| CRITICALREQUESTSGET       | Threshold                                                                                                                              |                       |             |
| WARNINGREQUESTSPOST       | Threshold                                                                                                                              |                       |             |
| CRITICALREQUESTSPOST      | Threshold                                                                                                                              |                       |             |
| WARNINGRESPONSES1XX       | Threshold                                                                                                                              |                       |             |
| CRITICALRESPONSES1XX      | Threshold                                                                                                                              |                       |             |
| WARNINGRESPONSES2XX       | Threshold                                                                                                                              |                       |             |
| CRITICALRESPONSES2XX      | Threshold                                                                                                                              |                       |             |
| WARNINGRESPONSES3XX       | Threshold                                                                                                                              |                       |             |
| CRITICALRESPONSES3XX      | Threshold                                                                                                                              |                       |             |
| WARNINGRESPONSES4XX       | Threshold                                                                                                                              |                       |             |
| CRITICALRESPONSES4XX      | Threshold                                                                                                                              |                       |             |
| WARNINGRESPONSES5XX       | Threshold                                                                                                                              |                       |             |
| CRITICALRESPONSES5XX      | Threshold                                                                                                                              |                       |             |
| CRITICALSTATUS            | Define the conditions to match for the status to be CRITICAL. Can use special variables like: %\{status\}                                | %\{status\} ne "Active" |             |
| WARNINGSTATUS             | Define the conditions to match for the status to be WARNING. Can use special variables like: %\{status\}                                 |                       |             |
| EXTRAOPTIONS              | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). |                       |             |

</TabItem>
<TabItem value="Zones" label="Zones">

| Macro                              | Description                                                                                                                            | Default value         | Mandatory   |
|:-----------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|:----------------------|:-----------:|
| FILTERCOUNTERS                     |                                                                                                                                        |                       |             |
| FILTERZONENAME                     | Filter zones by name (can be a regexp)                                                                                                 |                       |             |
| WARNINGSEARCHESDROPPED             | Thresholds                                                                                                                             |                       |             |
| CRITICALSEARCHESDROPPED            | Thresholds                                                                                                                             |                       |             |
| WARNINGSEARCHESMAXSUBEXCEEDED      | Thresholds                                                                                                                             |                       |             |
| CRITICALSEARCHESMAXSUBEXCEEDED     | Thresholds                                                                                                                             |                       |             |
| WARNINGSEARCHESMAXTARGETSEXCEEDED  | Thresholds                                                                                                                             |                       |             |
| CRITICALSEARCHESMAXTARGETSEXCEEDED | Thresholds                                                                                                                             |                       |             |
| WARNINGSEARCHESTOTAL               | Thresholds                                                                                                                             |                       |             |
| CRITICALSEARCHESTOTAL              | Thresholds                                                                                                                             |                       |             |
| CRITICALSTATUS                     | Define the conditions to match for the status to be CRITICAL. Can use special variables like: %\{status\}, %\{type\}, %\{name\}              | %\{status\} ne "Active" |             |
| WARNINGSTATUS                      | Define the conditions to match for the status to be WARNING. Can use special variables like: %\{status\}, %\{type\}, %\{name\}               |                       |             |
| WARNINGZONECALLSCURRENT            | Thresholds                                                                                                                             |                       |             |
| CRITICALZONECALLSCURRENT           | Thresholds                                                                                                                             |                       |             |
| WARNINGZONESCOUNT                  | Thresholds                                                                                                                             |                       |             |
| CRITICALZONESCOUNT                 | Thresholds                                                                                                                             |                       |             |
| EXTRAOPTIONS                       | Any extra option you may want to add to the command (a --verbose flag for example). All options are listed [here](#available-options). |                       |             |

</TabItem>
</Tabs>

3. [Deploy the configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). The service appears in the list of services, and on the **Resources Status** page. The command that is sent by the connector is displayed in the details panel of the service: it shows the values of the macros.

## How to check in the CLI that the configuration is OK and what are the main options for?

Once the plugin is installed, log into your Centreon poller's CLI using the
**centreon-engine** user account (`su - centreon-engine`). Test that the connector 
is able to monitor a resource using a command like this one (replace the sample values by yours):

```bash
/usr/lib/centreon/plugins/centreon_cisco_vcs_restapi.pl \
	--plugin=network::cisco::vcs::restapi::plugin \
	--mode=zones \
	--hostname='10.0.0.1' \
	--api-username='' \
	--api-password='' \
	--port='443' \
	--proto='https'  \
	--filter-counters='' \
	--filter-zone-name='' \
	--warning-status='' \
	--critical-status='%\{status\} ne "Active"' \
	--warning-zone-calls-current='' \
	--critical-zone-calls-current='' \
	--warning-searches-total='' \
	--critical-searches-total='' \
	--warning-searches-dropped='' \
	--critical-searches-dropped='' \
	--warning-searches-maxsub-exceeded='' \
	--critical-searches-maxsub-exceeded='' \
	--warning-searches-maxtargets-exceeded='' \
	--critical-searches-maxtargets-exceeded='' \
	--warning-zones-count='' \
	--critical-zones-count='' 
```

The expected command output is shown below:

```bash
OK: Number of zones: 33 max sub exceeded: 84 max targets exceeded: 17 All zones are ok | 'zones.total.count'=33;;;0;'zones.searches.total.persecond'=97;;;0;'zones.searches.dropped.persecond'=49;;;0;'zones.searches.maxsub.exceeded.count'=84;;;0;'zones.searches.maxtargets.exceeded.count'=17;;;0;'*zones*#zone.calls.current.count'=;;;0;
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
/usr/lib/centreon/plugins/centreon_cisco_vcs_restapi.pl \
	--plugin=network::cisco::vcs::restapi::plugin \
	--list-mode
```

The plugin brings the following modes:

| Mode                                                                                                                                      | Linked service template                       |
|:------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------|
| alerts [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/cisco/vcs/restapi/mode/alerts.pm)]                   | Net-Cisco-Vcs-Alerts-Restapi-custom           |
| calls [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/cisco/vcs/restapi/mode/calls.pm)]                     | Net-Cisco-Vcs-Calls-Restapi-custom            |
| endpoints [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/cisco/vcs/restapi/mode/endpoints.pm)]             | Not used in this Monitoring Connector         |
| http-proxy-stats [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/cisco/vcs/restapi/mode/httpproxystats.pm)] | Net-Cisco-Vcs-Http-Proxy-Stats-Restapi-custom |
| zones [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/cisco/vcs/restapi/mode/zones.pm)]                     | Net-Cisco-Vcs-Zones-Restapi-custom            |

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
| --hostname                                 | API hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --port                                     | API port (default: 443)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --proto                                    | Specify https if needed (default: 'https')                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --api-username                             | Set API username                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --api-password                             | Set API password                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --timeout                                  | Set HTTP timeout                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
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
<TabItem value="Alerts" label="Alerts">

| Option                   | Description                                                       |
|:-------------------------|:------------------------------------------------------------------|
| --filter-reason          | Filter alerts by reason (can use regexp).                         |
| --display-alerts         | Display alerts in verbose output.                                 |
| --warning-* --critical-* | Thresholds. Can be: 'total', 'acknowledged', 'unacknowledged'.    |

</TabItem>
<TabItem value="Calls" label="Calls">

| Option                   | Description                                                                                                                                                                                                                                                                                                                                                |
|:-------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached              | Memcached server to use (only one server).                                                                                                                                                                                                                                                                                                                 |
| --redis-server           | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                                                                                                                                            |
| --redis-attribute        | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                                                                                                                                    |
| --redis-db               | Set Redis database index.                                                                                                                                                                                                                                                                                                                                  |
| --failback-file          | Failback on a local file if Redis connection fails.                                                                                                                                                                                                                                                                                                        |
| --memexpiration          | Time to keep data in seconds (default: 86400).                                                                                                                                                                                                                                                                                                             |
| --statefile-dir          | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                                                                                                                                     |
| --statefile-suffix       | Define a suffix to customize the statefile name (default: '').                                                                                                                                                                                                                                                                                             |
| --statefile-concat-cwd   | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.                                                                                                                |
| --statefile-format       | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                                                                                                                                      |
| --statefile-key          | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                                                                                                                               |
| --statefile-cipher       | Define the cipher algorithm to encrypt the cache (default: 'AES').                                                                                                                                                                                                                                                                                         |
| --warning-* --critical-* | Thresholds. Can be: 'traversal-current', 'traversal-total', 'nontraversal-current', 'nontraversal-total', 'cloud-current', 'cloud-total', ' 'collaborationedge-current', 'collaborationedge-total', 'microsoftcontent-current', 'microsoftcontent-total', 'microsoftimp-current', 'microsoftimp-total', 'connectionfailed-total', 'disconnected-total'.    |

</TabItem>
<TabItem value="Http-Proxy-Stats" label="Http-Proxy-Stats">

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
| --filter-counters        | Only display some counters (regexp can be used). (example: --filter-counters='responses')                                                                                                                                                     |
| --warning-* --critical-* | Threshold. Can be: 'connections-client', 'connections-server', 'requests-completed', 'requests-get', 'requests-post', 'responses-1xx', 'responses-2xx', 'responses-3xx', 'responses-4xx', 'responses-5xx'.                                    |
| --warning-status         | Define the conditions to match for the status to be WARNING. Can use special variables like: %\{status\}.                                                                                                                                       |
| --critical-status        | Define the conditions to match for the status to be CRITICAL (default: '%\{status\} ne "Active"'). Can use special variables like: %\{status\}.                                                                                                   |

</TabItem>
<TabItem value="Zones" label="Zones">

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
| --filter-zone-name       | Filter zones by name (can be a regexp).                                                                                                                                                                                                       |
| --warning-* --critical-* | Thresholds. Can be: 'zones-count', 'zone-calls-current', 'searches-total', 'searches-dropped', 'searches-maxsub-exceeded', 'searches-maxtargets-exceeded'.                                                                                    |
| --warning-status         | Define the conditions to match for the status to be WARNING. (default: ''). Can use special variables like: %\{status\}, %\{type\}, %\{name\}.                                                                                                      |
| --critical-status        | Define the conditions to match for the status to be CRITICAL. (default: '%\{status\} ne "Active"'). Can use special variables like: %\{status\}, %\{type\}, %\{name\}.                                                                                |

</TabItem>
</Tabs>

All available options for a given mode can be displayed by adding the
`--help` parameter to the command:

```bash
/usr/lib/centreon/plugins/centreon_cisco_vcs_restapi.pl \
	--plugin=network::cisco::vcs::restapi::plugin \
	--mode=zones \
	--help
```
