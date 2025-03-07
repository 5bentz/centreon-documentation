---
id: sc-service-now-incident-events
title: ServiceNow Incident 
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Before starting

- You can send events from a central server, a remote server or a poller.
- By default, this stream connector sends **host_status** and **service_status** events. The event format is shown **[there](#event-format)**.
- Aformentioned events are fired each time a host or a service is checked. Various parameters let you filter out events.

## Installation

Login as `root` on the Centreon central server using your favorite SSH client.

Run the command according on your system:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```shell
dnf install centreon-stream-connector-servicenow
```

</TabItem>

<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```shell
dnf install centreon-stream-connector-servicenow
```

</TabItem>

<TabItem value="Debian 12" label="Debian 12">

```shell
apt install centreon-stream-connector-servicenow
```

</TabItem>
</Tabs>

## Configuration

To configure your stream connector, you must **head over** the **configuration --> Poller --> Broker configuration** menu. **Select** the **central-broker-master** configuration (or the appropriate broker configuration if it is a poller or a remote server that will send events) and **click** the **Output tab** when the broker form is displayed.

**Add** a new **generic - stream connector** output and **set** the following fields as follow:

| Field           | Value                                                               |
| --------------- | ------------------------------------------------------------------- |
| Name            | Servicenow events                                                   |
| Path            | /usr/share/centreon-broker/lua/servicenow-incident-events-apiv2.lua |
| Filter category | Neb                                                                 |

### Add Service Now mandatory parameters

Each stream connector has a set of mandatory parameters. To add them you must **click** on the **+Add a new entry** button located **below** the **filter category** input.

| Type   | Name          | Value explanation                    | Value exemple |
| ------ | ------------- | ------------------------------------ | ------------- |
| string | instance      | the name of the service now instance | MyCompany     |
| string | client_id     | The Oauth client_id                  |               |
| string | client_secret | The Oauth client_secret              |               |
| string | username      | The Oauth user                       |               |
| string | password      | The Oauth pasword                    |               |

### Add Service Now optional parameters

Some stream connectors have a set of optional parameters dedicated to the Software that they are associated with. To add them you must **click** on the **+Add a new entry** button located **below** the **filter category** input.

| Type   | Name            | Value explanation                          | default value                                                     |
| ------ | --------------- | ------------------------------------------ | ----------------------------------------------------------------- |
| string | http_server_url | service-now.com                            | the address of the service-now server                             |
| string | incident_table  | incident                                   | the name of the incident table                                    |
| string | source          | centreon                                   | the source name of the incident                                   |
| string | logfile         | the file in which logs are written         | /var/log/centreon-broker/servicenow-incident-stream-connector.log |
| number | log_level       | logging level from 1 (errors) to 3 (debug) | 1                                                                 |

### Standard parameters

All stream connectors can use a set of optional parameters that are made available through Centreon stream connectors lua modules.

All those parameters are documented **[here](https://github.com/centreon/centreon-stream-connector-scripts/blob/master/modules/docs/sc_param.md#default-parameters)**.

Some of them are overridden by this stream connector.

| Type   | Name                | Default value for the stream connector |
| ------ | ------------------- | -------------------------------------- |
| string | accepted_categories | neb                                    |
| string | accepted_elements   | host_status,service_status             |
| string | host_status         | 1,2                                    |
| string | service_status      | 1,2,3                                  |

## Event bulking

This stream connector is compatible with event bulking. Meaning that it is able to send more that one event in each call to the Service Now REST API.

To use this feature you must add the following parameter in your stream connector configuration.

| Type   | Name            | Value           |
| ------ | --------------- | --------------- |
| number | max_buffer_size | `more than one` |

## Event format

This stream connector is not compatible with event bulking. Meaning that the option `max_buffer_size` can't be higher than 1

### service_status event

```json
{
  "source": "centreon",
  "short_description": "CRITICAL  my_host my_service is not doing well",
  "cmdb_ci": "my_host",
  "comments": "HOST: my_host\n SERVICE: my_service\n OUTPUT: is not doing well"
}
```

### host_status event

```json
{
  "source": "centreon",
  "short_description": "CRITICAL  my_host is not doing well",
  "cmdb_ci": "my_host",
  "comments": "HOST: my_host\n OUTPUT: is not doing well"
}
```

### Custom event format

This stream connector allows you to change the format of the event to suit your needs. Only the **records** part of the json is customisable. It also allows you to handle events type that are not handled by default such as **ba_status events**.

In order to use this feature you need to configure a json event format file and add a new stream connector parameter.

| Type   | Name        | Value                                              |
| ------ | ----------- | -------------------------------------------------- |
| string | format_file | /etc/centreon-broker/servicenow-incident-events-format.json |

> The event format configuration file must be readable by the centreon-broker user

To learn more about custom event format and templating file, head over the following **[documentation](https://github.com/centreon/centreon-stream-connector-scripts/blob/master/modules/docs/templating.md#templating-documentation)**.

## Curl commands

Here is the list of all the curl commands that are used by the stream connector.

You must replace all the *`<xxxx>`* inside the below commands with their appropriate value. *`<instance>`* may become *MyCompany*.

### Get OAuth tokens

```shell
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" 'https://<instance_name>.service-now.com/oauth_token.do' -d 'grant_type=password&client_id=<client_id>&client_secret=<client_secret>&username=<username>&password=<password>'
```

### Refresh OAuth tokens

```shell
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" 'https://<instance_name>.service-now.com/oauth_token.do' -d 'grant_type=refresh_token&client_id=<client_id>&client_secret=<client_secret>&username=<username>&password=<password>&refresh_token=<refresh_token>'
```

The *`<refresh_token>`* is obtained thanks to **[this curl](#get-oauth-tokens)**.

### Send events

```shell
curl -X POST -H 'content-type: application/json' -H 'Accept: application/json' -H 'Authorization: Bearer <access_token>' 'https://<instance_name>.service-now.com/api/now/table/incident' -d '{"source":"centreon","short_description":"CRITICAL  my_host my_service is not doing well","cmdb_ci":"my_host","comments":"HOST: my_host\n SERVICE: my_service\n OUTPUT: is not doing well"}'
```

The *`<access_token>`* is obtained thanks to **[this curl](#get-oauth-tokens)**.
