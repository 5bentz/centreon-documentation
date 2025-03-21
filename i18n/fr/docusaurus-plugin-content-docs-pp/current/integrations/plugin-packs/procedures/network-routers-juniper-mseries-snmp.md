---
id: network-routers-juniper-mseries-snmp
title: Juniper M-Series
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Contenu du pack

### Modèles

Le connecteur de supervision **Juniper M-Series** apporte un modèle d'hôte :

* **Net-Juniper-Mseries-SNMP-custom**

Le connecteur apporte les modèles de service suivants
(classés selon le modèle d'hôte auquel ils sont rattachés) :

<Tabs groupId="sync">
<TabItem value="Net-Juniper-Mseries-SNMP-custom" label="Net-Juniper-Mseries-SNMP-custom">

| Alias          | Modèle de service                         | Description                                        |
|:---------------|:------------------------------------------|:---------------------------------------------------|
| Cpu-Routing    | Net-Juniper-Mseries-Cpu-Routing-custom    | Contrôle l'utilisation CPU du 'routing engine'     |
| Hardware       | Net-Juniper-Mseries-Hardware-custom       | Contrôle l'état du matériel                        |
| Memory-Routing | Net-Juniper-Mseries-Memory-Routing-custom | Contrôle l'utilisation mémoire du 'Routing Engine' |

> Les services listés ci-dessus sont créés automatiquement lorsque le modèle d'hôte **Net-Juniper-Mseries-SNMP-custom** est utilisé.

</TabItem>
<TabItem value="Non rattachés à un modèle d'hôte" label="Non rattachés à un modèle d'hôte">

| Alias                      | Modèle de service                                          | Description                                                                                                      | Découverte |
|:---------------------------|:-----------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------|:----------:|
| Bgp-Peer-Prefix-Statistics | Net-Juniper-Mseries-SNMP-Bgp-Peer-Prefix-Statistics-custom | Contrôle les statistiques des préfixes des pairs BGP                                                               |            |
| Bgp-Peer-State             | Net-Juniper-Mseries-SNMP-Bgp-Peer-State-custom             | Contrôle le statut des pairs BGP                                                                                 |            |
| Disk-Generic-Id            | Net-Juniper-Mseries-Disk-Generic-Id-custom                 | Contrôle du taux d'espace libre disponible du disque                                                             |            |
| Disk-Generic-Name          | Net-Juniper-Mseries-Disk-Generic-Name-custom               | Contrôle du taux d'espace libre disponible du disque                                                             |            |
| Disk-Global                | Net-Juniper-Mseries-Disk-Global-custom                     | Contrôle du taux d'espace libre disponible du disque                                                             | X          |
| Ldp-Session-Status         | Net-Juniper-Mseries-SNMP-Ldp-Session-Status-custom         | Contrôle le statut des sessions LDP                                                                              |            |
| Lsp-Status                 | Net-Juniper-Mseries-SNMP-Lsp-Status-custom                 | Contrôle le statut des LSP                                                                                       |            |
| Rsvp-Session-Status        | Net-Juniper-Mseries-SNMP-Rsvp-Session-Status-custom        | Contrôle le statut des sessions RSVP                                                                             |            |
| Traffic-Generic-Id         | Net-Juniper-Mseries-Traffic-Generic-Id-custom              | Contrôle de la bande passante de l'interface. Pour chaque contrôle apparaîtra le nom de l'interface              |            |
| Traffic-Generic-Name       | Net-Juniper-Mseries-Traffic-Generic-Name-custom            | Contrôle de la bande passante de l'interface. Pour chaque contrôle apparaîtra le nom de l'interface              |            |
| Traffic-Global             | Net-Juniper-Mseries-Traffic-Global-custom                  | Contrôle de la bande passante d'un ensemble d'interfaces. Pour chaque contrôle apparaîtra le nom de l'interface  | X          |

> Les services listés ci-dessus ne sont pas créés automatiquement lorsqu'un modèle d'hôte est appliqué. Pour les utiliser, [créez un service manuellement](/docs/monitoring/basic-objects/services) et appliquez le modèle de service souhaité.

> Si la case **Découverte** est cochée, cela signifie qu'une règle de découverte de service existe pour ce service.

</TabItem>
</Tabs>

### Règles de découverte

#### Découverte d'hôtes

| Nom de la règle | Description                                                                                                                                                                                                                                             |
|:----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SNMP Agents     | Discover your resources through an SNMP subnet scan. You need to install the [Generic SNMP](./applications-protocol-snmp.md) connector to get the discovery rule and create a template mapper for the **Net-Juniper-Mseries-SNMP-custom** host template |

Rendez-vous sur la [documentation dédiée](/docs/monitoring/discovery/hosts-discovery) pour en savoir plus sur la découverte automatique d'hôtes.

#### Découverte de services

| Nom de la règle                  | Description                                                             |
|:---------------------------------|:------------------------------------------------------------------------|
| Net-Juniper-Mseries-Storage-Name | Découvre les partitions des disques et supervise leur taux d'occupation        |
| Net-Juniper-Mseries-Traffic-Name | Découvre les interfaces réseau et supervise le statut et l'utilisation |

Rendez-vous sur la [documentation dédiée](/docs/monitoring/discovery/services-discovery)
pour en savoir plus sur la découverte automatique de services et sa [planification](/docs/monitoring/discovery/services-discovery/#règles-de-découverte).

### Métriques & statuts collectés

Voici le tableau des services pour ce connecteur, détaillant les métriques rattachées à chaque service.

<Tabs groupId="sync">
<TabItem value="Bgp-Peer-Prefix-Statistics" label="Bgp-Peer-Prefix-Statistics">

| Métrique                                                  | Unité |
|:----------------------------------------------------------|:------|
| *peers*~*afisafi*#peer.afisafi.prefixes.in.count          | count |
| *peers*~*afisafi*#peer.afisafi.prefixes.in.accepted.count | count |
| *peers*~*afisafi*#peer.afisafi.prefixes.in.rejected.count | count |
| *peers*~*afisafi*#peer.afisafi.prefixes.in.active.count   | count |
| *peers*~*afisafi*#peer.afisafi.prefixes.out.count         | count |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Bgp-Peer-State" label="Bgp-Peer-State">

| Métrique       | Unité |
|:---------------|:------|
| *peers*#status | N/A   |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Cpu-Routing" label="Cpu-Routing">

| Métrique                         | Unité |
|:---------------------------------|:------|
| *cpu*#cpu.utilization.percentage | %     |
| *cpu*#cpu.load.1m.percentage     | %     |
| *cpu*#cpu.load.5m.percentage     | %     |
| *cpu*#cpu.load.15m.percentage    | %     |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Disk-*" label="Disk-*">

| Métrique                              | Unité |
|:--------------------------------------|:------|
| storage.partitions.count              | count |
| *disk_name*#storage.space.usage.bytes | B     |
| *disk_name*#storage.access.count      | count |

> Concerne les modèles de service suivants : Disk-Generic-Id, Disk-Generic-Name, Disk-Global

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Hardware" label="Hardware">

Coming soon

</TabItem>
<TabItem value="Ldp-Session-Status" label="Ldp-Session-Status">

| Métrique               | Unité |
|:-----------------------|:------|
| *sessions*#status      | N/A   |
| *sessions*#last-change | s     |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Lsp-Status" label="Lsp-Status">

| Métrique                | Unité |
|:------------------------|:------|
| *lsps*#status           | N/A   |
| *lsps*#transition-count | N/A   |
| *lsps*#last-transition  | s     |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Memory-Routing" label="Memory-Routing">

| Métrique                         | Unité |
|:---------------------------------|:------|
| *memory*#memory.usage.bytes      | B     |
| *memory*#memory.free.bytes       | B     |
| *memory*#memory.usage.percentage | %     |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Rsvp-Session-Status" label="Rsvp-Session-Status">

| Métrique          | Unité |
|:------------------|:------|
| *sessions*#status | N/A   |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Traffic-*" label="Traffic-*">

| Métrique                                             | Unité |
|:-----------------------------------------------------|:------|
| *interface_name*#status                              | N/A   |
| *interface_name*#interface.traffic.in.bitspersecond  | b/s   |
| *interface_name*#interface.traffic.out.bitspersecond | b/s   |

> Concerne les modèles de service suivants : Traffic-Generic-Id, Traffic-Generic-Name, Traffic-Global

</TabItem>
</Tabs>

## Prérequis

### Configuration SNMP

Le service SNMP doit être activé et configuré sur l'équipement. Veuillez vous référer à la documentation officielle du constructeur/éditeur.

### Flux réseau

La communication doit être possible sur le port UDP 161 depuis le collecteur
Centreon vers la ressource supervisée.

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
dnf install centreon-pack-network-routers-juniper-mseries-snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-network-routers-juniper-mseries-snmp
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-pack-network-routers-juniper-mseries-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-network-routers-juniper-mseries-snmp
```

</TabItem>
</Tabs>

2. Quel que soit le type de la licence (*online* ou *offline*), installez le connecteur **Juniper M-Series**
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
dnf install centreon-plugin-Network-Routers-Juniper-Mseries-Snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Network-Routers-Juniper-Mseries-Snmp
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-plugin-network-routers-juniper-mseries-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Network-Routers-Juniper-Mseries-Snmp
```

</TabItem>
</Tabs>

## Utiliser le connecteur de supervision

### Utiliser un modèle d'hôte issu du connecteur

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Complétez les champs **Nom**, **Alias** & **IP Address/DNS** correspondant à votre ressource.
3. Appliquez le modèle d'hôte **Net-Juniper-Mseries-SNMP-custom**.

> Si vous utilisez SNMP en version 3, vous devez configurer les paramètres spécifiques associés via la macro **SNMPEXTRAOPTIONS**.
> Plus d'informations dans la section [Troubleshooting SNMP](../getting-started/how-to-guides/troubleshooting-plugins.md#snmpv3-options-mapping).

| Macro            | Description                                                                                          | Valeur par défaut | Obligatoire |
|:-----------------|:-----------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| SNMPEXTRAOPTIONS | Any extra option you may want to add to every command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

4. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). L'hôte apparaît dans la liste des hôtes supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails de l'hôte : celle-ci montre les valeurs des macros.

### Utiliser un modèle de service issu du connecteur

1. Si vous avez utilisé un modèle d'hôte et coché la case **Créer aussi les services liés aux modèles**, les services associés au modèle ont été créés automatiquement, avec les modèles de services correspondants. Sinon, [créez les services désirés manuellement](/docs/monitoring/basic-objects/services) et appliquez-leur un modèle de service.
2. Renseignez les macros désirées (par exemple, ajustez les seuils d'alerte). Les macros indiquées ci-dessous comme requises (**Obligatoire**) doivent être renseignées.

<Tabs groupId="sync">
<TabItem value="Bgp-Peer-Prefix-Statistics" label="Bgp-Peer-Prefix-Statistics">

| Macro                      | Description                                                                                        | Valeur par défaut | Obligatoire |
|:---------------------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTER                     | Filter by peer identifier (can be regexp)                                                          |                   |             |
| WARNINGPREFIXESIN          | Specify warning threshold                                                                          |                   |             |
| CRITICALPREFIXESIN         | Specify critical threshold                                                                         |                   |             |
| WARNINGPREFIXESINACCEPTED  | Specify warning threshold                                                                          |                   |             |
| CRITICALPREFIXESINACCEPTED | Specify critical threshold                                                                         |                   |             |
| WARNINGPREFIXESINACTIVE    | Specify warning threshold                                                                          |                   |             |
| CRITICALPREFIXESINACTIVE   | Specify critical threshold                                                                         |                   |             |
| WARNINGPREFIXESINREJECTED  | Specify warning threshold                                                                          |                   |             |
| CRITICALPREFIXESINREJECTED | Specify critical threshold                                                                         |                   |             |
| WARNINGPREFIXESOUT         | Specify warning threshold                                                                          |                   |             |
| CRITICALPREFIXESOUT        | Specify critical threshold                                                                         |                   |             |
| EXTRAOPTIONS               | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). |                   |             |

</TabItem>
<TabItem value="Bgp-Peer-State" label="Bgp-Peer-State">

| Macro          | Description                                                                                                                                                                                                                                                                                                              | Valeur par défaut                                               | Obligatoire |
|:---------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------|:-----------:|
| FILTER         | Filter by peer identifier (can be regexp)                                                                                                                                                                                                                                                                                |                                                                 |             |
| FILTERREMOTEIP | Filter by remote ip address (can be regexp)                                                                                                                                                                                                                                                                              |                                                                 |             |
| FILTERLOCALAS  | Filter by local AS (can be regexp)                                                                                                                                                                                                                                                                                       |                                                                 |             |
| CRITICALSTATUS | Specify critical threshold (default: '%\{peer_status\} =~ /running/ && %\{peer_state\} !~ /established/'). Can use special variables like %\{peer_identifier\}, %\{peer_state\}, %\{peer_status\}, %\{local_type\}, %\{local_ip\}, %\{local_port\}, %\{local_as\}, %\{remote_type\}, %\{remote_ip\}, %\{remote_port\}, %\{remote_as\} | %\{peer_status\} =~ /running/ && %\{peer_state\} !~ /established/ |             |
| WARNINGSTATUS  | Specify warning threshold. Can use special variables like %\{peer_identifier\}, %\{peer_state\}, %\{peer_status\}, %\{local_type\}, %\{local_ip\}, %\{local_port\}, %\{local_as\}, %\{remote_type\}, %\{remote_ip\}, %\{remote_port\}, %\{remote_as\}                                                                               |                                                                 |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                                                                                                                                                                                       |                                                                 |             |

</TabItem>
<TabItem value="Cpu-Routing" label="Cpu-Routing">

| Macro           | Description                                                                                        | Valeur par défaut | Obligatoire |
|:----------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTER          | Filter operating (default: 'routing\|fpc')                                                         | routing           |             |
| WARNING         | Thresholds                                                                                         | 80                |             |
| CRITICAL        | Thresholds                                                                                         | 90                |             |
| WARNINGLOAD15M  | Thresholds                                                                                         |                   |             |
| CRITICALLOAD15M | Thresholds                                                                                         |                   |             |
| WARNINGLOAD1M   | Thresholds                                                                                         |                   |             |
| CRITICALLOAD1M  | Thresholds                                                                                         |                   |             |
| WARNINGLOAD5M   | Thresholds                                                                                         |                   |             |
| CRITICALLOAD5M  | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS    | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). | --verbose         |             |

</TabItem>
<TabItem value="Disk-Generic-Id" label="Disk-Generic-Id">

| Macro        | Description                                                                                                                                                                                    | Valeur par défaut   | Obligatoire |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------|:-----------:|
| DISKID       | Set the storage (number expected) example: 1, 2,... (empty means 'check all storage')                                                                                                          |                     |             |
| TRANSFORMDST | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | $1                  |             |
| TRANSFORMSRC | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | ^.*mounted on: (.*) |             |
| CRITICAL     | Critical threshold                                                                                                                                                                             | 90                  |             |
| WARNING      | Warning threshold                                                                                                                                                                              | 80                  |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                                                             |                     |             |

</TabItem>
<TabItem value="Disk-Generic-Name" label="Disk-Generic-Name">

| Macro        | Description                                                                                                                                                                                    | Valeur par défaut   | Obligatoire |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------|:-----------:|
| DISKNAME     | Set the storage (number expected) example: 1, 2,... (empty means 'check all storage')                                                                                                          |                     |             |
| TRANSFORMDST | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | $1                  |             |
| TRANSFORMSRC | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | ^.*mounted on: (.*) |             |
| CRITICAL     | Critical threshold                                                                                                                                                                             | 90                  |             |
| WARNING      | Warning threshold                                                                                                                                                                              | 80                  |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                                                             |                     |             |

</TabItem>
<TabItem value="Disk-Global" label="Disk-Global">

| Macro        | Description                                                                                                                                                                                    | Valeur par défaut      | Obligatoire |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------|:-----------:|
| FILTER       | Set the storage (number expected) example: 1, 2,... (empty means 'check all storage')                                                                                                          | ^(?!(devfs\|/dev/md0)) |             |
| TRANSFORMDST | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | $1                     |             |
| TRANSFORMSRC | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | ^.*mounted on: (.*)    |             |
| CRITICAL     | Critical threshold                                                                                                                                                                             | 95                     |             |
| WARNING      | Warning threshold                                                                                                                                                                              | 90                     |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                                                             | --verbose              |             |

</TabItem>
<TabItem value="Hardware" label="Hardware">

| Macro        | Description                                                                                        | Valeur par défaut | Obligatoire |
|:-------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| COMPONENT    | Which component to check (default: '.*'). Can be: 'fru', 'operating', 'alarm'                      | .*                |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). | --verbose         |             |

</TabItem>
<TabItem value="Ldp-Session-Status" label="Ldp-Session-Status">

| Macro              | Description                                                                                                                                         | Valeur par défaut          | Obligatoire |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------|:-----------:|
| FILTERENTITY       | Filter entities and/or peer                                                                                                                         |                            |             |
| FILTERPEER         | Filter entities and/or peer                                                                                                                         |                            |             |
| WARNINGLASTCHANGE  | Warning threshold in seconds                                                                                                                        |                            |             |
| CRITICALLASTCHANGE | Critical threshold in seconds                                                                                                                       |                            |             |
| CRITICALSTATUS     | Define the conditions to match for the status to be CRITICAL (default: '%\{state\} !~ /operational/i'). You can use the following variables: %\{state\} | %\{state\} !~ /operational/i |             |
| WARNINGSTATUS      | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{state\}                            |                            |             |
| EXTRAOPTIONS       | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                  |                            |             |

</TabItem>
<TabItem value="Lsp-Status" label="Lsp-Status">

| Macro                   | Description                                                                                                                                | Valeur par défaut | Obligatoire |
|:------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERNAME              | Filter LSPs                                                                                                                                |                   |             |
| FILTERFROM              | Filter LSPs                                                                                                                                |                   |             |
| FILTERTO                | Filter LSPs                                                                                                                                |                   |             |
| WARNINGLASTTRANSITION   | Warning threshold                                                                                                                          |                   |             |
| CRITICALLASTTRANSITION  | Critical threshold                                                                                                                         |                   |             |
| CRITICALSTATUS          | Define the conditions to match for the status to be CRITICAL (default: '%\{state\} !~ /up/i'). You can use the following variables: %\{state\} | %\{state\} !~ /up/i |             |
| WARNINGSTATUS           | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{state\}                   |                   |             |
| WARNINGTRANSITIONCOUNT  | Warning threshold                                                                                                                          |                   |             |
| CRITICALTRANSITIONCOUNT | Critical threshold                                                                                                                         |                   |             |
| EXTRAOPTIONS            | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                         |                   |             |

</TabItem>
<TabItem value="Memory-Routing" label="Memory-Routing">

| Macro             | Description                                                                                        | Valeur par défaut | Obligatoire |
|:------------------|:---------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTER            | Filter operating (default: 'routing\|fpc')                                                         | routing           |             |
| WARNING           | Thresholds                                                                                         | 80                |             |
| CRITICAL          | Thresholds                                                                                         | 90                |             |
| WARNINGUSAGE      | Thresholds                                                                                         |                   |             |
| CRITICALUSAGE     | Thresholds                                                                                         |                   |             |
| WARNINGUSAGEFREE  | Thresholds                                                                                         |                   |             |
| CRITICALUSAGEFREE | Thresholds                                                                                         |                   |             |
| EXTRAOPTIONS      | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles). | --verbose         |             |

</TabItem>
<TabItem value="Rsvp-Session-Status" label="Rsvp-Session-Status">

| Macro          | Description                                                                                                                                | Valeur par défaut | Obligatoire |
|:---------------|:-------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTERNAME     | Filter sessions                                                                                                                            |                   |             |
| FILTERFROM     | Filter sessions                                                                                                                            |                   |             |
| FILTERTO       | Filter sessions                                                                                                                            |                   |             |
| CRITICALSTATUS | Define the conditions to match for the status to be CRITICAL (default: '%\{state\} !~ /up/i'). You can use the following variables: %\{state\} | %\{state\} !~ /up/i |             |
| WARNINGSTATUS  | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{state\}                   |                   |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                         |                   |             |

</TabItem>
<TabItem value="Traffic-Generic-Id" label="Traffic-Generic-Id">

| Macro        | Description                                                                                                                                                             | Valeur par défaut | Obligatoire |
|:-------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| INTERFACEID  | Set the interface (number expected) example: 1,2,... (empty means 'check all interfaces')                                                                               |                   |             |
| CRITICALIN   | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C) | 90                |             |
| WARNINGIN    | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C) | 80                |             |
| CRITICALOUT  | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C) | 90                |             |
| WARNINGOUT   | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C) | 80                |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                                      |                   |             |

</TabItem>
<TabItem value="Traffic-Generic-Name" label="Traffic-Generic-Name">

| Macro         | Description                                                                                                                                                             | Valeur par défaut | Obligatoire |
|:--------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| INTERFACENAME | Set the interface (number expected) example: 1,2,... (empty means 'check all interfaces')                                                                               |                   |             |
| CRITICALIN    | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C) | 90                |             |
| WARNINGIN     | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C) | 80                |             |
| CRITICALOUT   | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C) | 90                |             |
| WARNINGOUT    | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C) | 80                |             |
| EXTRAOPTIONS  | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                                      |                   |             |

</TabItem>
<TabItem value="Traffic-Global" label="Traffic-Global">

| Macro          | Description                                                                                                                                                                                                         | Valeur par défaut | Obligatoire |
|:---------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTER         | Set the interface (number expected) example: 1,2,... (empty means 'check all interfaces')                                                                                                                           | .*                |             |
| WARNINGIN      | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C)                                             | 80                |             |
| CRITICALIN     | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C)                                             | 90                |             |
| WARNINGOUT     | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C)                                             | 80                |             |
| CRITICALOUT    | Thresholds (will superseed --\[warning-critical\]-errors). : 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C)                                             | 90                |             |
| CRITICALSTATUS | Define the conditions to match for the status to be CRITICAL (default: '%\{admstatus\} eq "up" and %\{opstatus\} ne "up"'). You can use the following variables: %\{admstatus\}, %\{opstatus\}, %\{duplexstatus\}, %\{display\} |                   |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (a --verbose flag for example). Toutes les options sont listées [ici](#options-disponibles).                                                                                                                  |                   |             |

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
/usr/lib/centreon/plugins/centreon_juniper_mseries.pl \
	--plugin=network::juniper::mseries::plugin \
	--mode=interfaces \
	--hostname=10.0.0.1 \
	--snmp-version='2c' \
	--snmp-community='my-snmp-community'  \
	--interface='.*' \
	--name \
	--add-status \
	--add-traffic \
	--critical-status='' \
	--warning-in-traffic='80' \
	--critical-in-traffic='90' \
	--warning-out-traffic='80' \
	--critical-out-traffic='90' 
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK: All interfaces are ok | '*interface_name*#status'='up';;;;'*interface_name*#interface.traffic.in.bitspersecond'=20b/s;80;90;;'*interface_name*#interface.traffic.out.bitspersecond'=20b/s;80;90;;
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
/usr/lib/centreon/plugins/centreon_juniper_mseries.pl \
	--plugin=network::juniper::mseries::plugin \
	--list-mode
```

Le plugin apporte les modes suivants :

| Mode                                                                                                                                                            | Modèle de service associé                                                                                                                         |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------|
| bgp-peer-prefix-statistics [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/bgppeerprefixstatistics.pm)] | Net-Juniper-Mseries-SNMP-Bgp-Peer-Prefix-Statistics-custom                                                                                        |
| bgp-peer-state [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/bgppeerstate.pm)]                        | Net-Juniper-Mseries-SNMP-Bgp-Peer-State-custom                                                                                                    |
| cos [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/cos.pm)]                                            | Not used in this Monitoring Connector                                                                                                             |
| cpu [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/cpu.pm)]                                            | Net-Juniper-Mseries-Cpu-Routing-custom                                                                                                            |
| hardware [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/hardware.pm)]                                  | Net-Juniper-Mseries-Hardware-custom                                                                                                               |
| interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/interfaces.pm)]                              | Net-Juniper-Mseries-Traffic-Generic-Id-custom<br />Net-Juniper-Mseries-Traffic-Generic-Name-custom<br />Net-Juniper-Mseries-Traffic-Global-custom |
| ldp-session-status [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/ldpsessionstatus.pm)]                | Net-Juniper-Mseries-SNMP-Ldp-Session-Status-custom                                                                                                |
| list-bgp-peers [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/listbgppeers.pm)]                        | Not used in this Monitoring Connector                                                                                                             |
| list-interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/listinterfaces.pm)]                                    | Used for service discovery                                                                                                                        |
| list-storages [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/liststorages.pm)]                                        | Used for service discovery                                                                                                                        |
| lsp-status [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/lspstatus.pm)]                               | Net-Juniper-Mseries-SNMP-Lsp-Status-custom                                                                                                        |
| memory [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/memory.pm)]                                      | Net-Juniper-Mseries-Memory-Routing-custom                                                                                                         |
| rsvp-session-status [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/network/juniper/common/junos/mode/rsvpsessionstatus.pm)]              | Net-Juniper-Mseries-SNMP-Rsvp-Session-Status-custom                                                                                               |
| storage [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/storage.pm)]                                                   | Net-Juniper-Mseries-Disk-Generic-Id-custom<br />Net-Juniper-Mseries-Disk-Generic-Name-custom<br />Net-Juniper-Mseries-Disk-Global-custom          |

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
| --hostname                                 | Name or address of the host to monitor (mandatory).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| --snmp-community                           | SNMP community (default value: public). It is recommended to use a read-only community.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-version                             | Version of the SNMP protocol. 1 for SNMP v1 (default), 2 for SNMP v2c, 3 for SNMP v3.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --snmp-port                                | UDP port to send the SNMP request to (default: 161).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --snmp-timeout                             | Time to wait before sending the request again if no reply has been received, in seconds (default: 1). See also --snmp-retries.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --snmp-retries                             | Maximum number of retries (default: 5).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --maxrepetitions                           | Max repetitions value (default: 50) (only for SNMP v2 and v3).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --subsetleef                               | How many OID values per SNMP request (default: 50) (for get\_leef method. Be cautious when you set it. Prefer to let the default value).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --snmp-autoreduce                          | Progressively reduce the number of requested OIDs in bulk mode. Use it in case of SNMP errors (by default, the number is divided by 2).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-force-getnext                       | Use SNMP getnext function in SNMP v2c and v3. This will request one OID at a time.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --snmp-cache-file                          | Use SNMP cache file.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --snmp-username                            | SNMP v3 only: User name (securityName).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --authpassphrase                           | SNMP v3 only: Pass phrase hashed using the authentication protocol defined in the --authprotocol option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --authprotocol                             | SNMP v3 only: Authentication protocol: MD5\|SHA. Since net-snmp 5.9.1: SHA224\|SHA256\|SHA384\|SHA512.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --privpassphrase                           | SNMP v3 only: Privacy pass phrase (privPassword) to encrypt messages using the protocol defined in the --privprotocol option.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --privprotocol                             | SNMP v3 only: Privacy protocol (privProtocol) used to encrypt messages. Supported protocols are: DES\|AES and since net-snmp 5.9.1: AES192\|AES192C\|AES256\|AES256C.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --contextname                              | SNMP v3 only: Context name (contextName), if relevant for the monitored host.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --contextengineid                          | SNMP v3 only: Context engine ID (contextEngineID), if relevant for the monitored host, given as a hexadecimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --securityengineid                         | SNMP v3 only: Security engine ID, given as a hexadecimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --snmp-errors-exit                         | Expected status in case of SNMP error or timeout. Possible values are warning, critical and unknown (default).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --snmp-tls-transport                       | Transport protocol for TLS communication (can be: 'dtlsudp', 'tlstcp').                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-tls-our-identity                    | X.509 certificate to identify ourselves. Can be the path to the certificate file or its contents.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --snmp-tls-their-identity                  | X.509 certificate to identify the remote host. Can be the path to the certificate file or its contents. This option is unnecessary if the certificate is already trusted by your system.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --snmp-tls-their-hostname                  | Common Name (CN) expected in the certificate sent by the host if it differs from the value of the --hostname parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --snmp-tls-trust-cert                      | A trusted CA certificate used to verify a remote host's certificate. If you use this option, you must also define --snmp-tls-their-hostname.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

#### Options des modes

Les options disponibles pour chaque modèle de services sont listées ci-dessous :

<Tabs groupId="sync">
<TabItem value="Bgp-Peer-Prefix-Statistics" label="Bgp-Peer-Prefix-Statistics">

| Option        | Description                                                                                                                                |
|:--------------|:-------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-peer | Filter by peer identifier (can be regexp)                                                                                                  |
| --warning-*   | Specify warning threshold. Can be: 'prefixes-in', 'prefixes-in-accepted', 'prefixes-in-rejected', 'prefixes-in-active', 'prefixes-out'     |
| --critical-*  | Specify critical threshold. Can be: 'prefixes-in', 'prefixes-in-accepted', 'prefixes-in-rejected', 'prefixes-in-active', 'prefixes-out'    |

</TabItem>
<TabItem value="Bgp-Peer-State" label="Bgp-Peer-State">

| Option             | Description                                                                                                                                                                                                                                                                                                                 |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-peer      | Filter by peer identifier (can be regexp)                                                                                                                                                                                                                                                                                   |
| --filter-remote-ip | Filter by remote ip address (can be regexp)                                                                                                                                                                                                                                                                                 |
| --filter-local-as  | Filter by local AS (can be regexp)                                                                                                                                                                                                                                                                                          |
| --warning-status   | Specify warning threshold. Can use special variables like %\{peer_identifier\}, %\{peer_state\}, %\{peer_status\}, %\{local_type\}, %\{local_ip\}, %\{local_port\}, %\{local_as\}, %\{remote_type\}, %\{remote_ip\}, %\{remote_port\}, %\{remote_as\}                                                                                  |
| --critical-status  | Specify critical threshold (default: '%\{peer_status\} =~ /running/ && %\{peer_state\} !~ /established/'). Can use special variables like %\{peer_identifier\}, %\{peer_state\}, %\{peer_status\}, %\{local_type\}, %\{local_ip\}, %\{local_port\}, %\{local_as\}, %\{remote_type\}, %\{remote_ip\}, %\{remote_port\}, %\{remote_as\}    |

</TabItem>
<TabItem value="Cpu-Routing" label="Cpu-Routing">

| Option                   | Description                                                             |
|:-------------------------|:------------------------------------------------------------------------|
| --filter                 | Filter operating (default: 'routing\|fpc').                             |
| --warning-* --critical-* | Thresholds. Can be: 'utilization', 'load-1m', 'load-5m', 'load-15m'.    |

</TabItem>
<TabItem value="Disk-*" label="Disk-*">

| Option                                          | Description                                                                                                                                                                                                                                   |
|:------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached                                     | Memcached server to use (only one server).                                                                                                                                                                                                    |
| --redis-server                                  | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                               |
| --redis-attribute                               | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                       |
| --redis-db                                      | Set Redis database index.                                                                                                                                                                                                                     |
| --failback-file                                 | Failback on a local file if Redis connection fails.                                                                                                                                                                                           |
| --memexpiration                                 | Time to keep data in seconds (default: 86400).                                                                                                                                                                                                |
| --statefile-dir                                 | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                        |
| --statefile-suffix                              | Define a suffix to customize the statefile name (default: '').                                                                                                                                                                                |
| --statefile-concat-cwd                          | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.   |
| --statefile-format                              | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                         |
| --statefile-key                                 | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                  |
| --statefile-cipher                              | Define the cipher algorithm to encrypt the cache (default: 'AES').                                                                                                                                                                            |
| --warning-usage                                 | Warning threshold.                                                                                                                                                                                                                            |
| --critical-usage                                | Critical threshold.                                                                                                                                                                                                                           |
| --warning-access                                | Warning threshold.                                                                                                                                                                                                                            |
| --critical-access                               | Critical threshold. Check if storage is readOnly: --critical-access=readOnly                                                                                                                                                                  |
| --add-access                                    | Check storage access (readOnly, readWrite).                                                                                                                                                                                                   |
| --units                                         | Units of thresholds (default: '%') ('%', 'B').                                                                                                                                                                                                |
| --free                                          | Thresholds are on free space left.                                                                                                                                                                                                            |
| --storage                                       | Set the storage (number expected) example: 1, 2,... (empty means 'check all storage').                                                                                                                                                        |
| --name                                          | Allows to use storage name with option --storage instead ofstorage oid index.                                                                                                                                                                 |
| --regexp                                        | Allows to use regexp to filter storage (with option --name).                                                                                                                                                                                  |
| --regexp-insensitive                            | Allows to use regexp non case-sensitive (with --regexp).                                                                                                                                                                                      |
| --path-best-match                               | Allows to select best path mount point (with --name).                                                                                                                                                                                         |
| --reload-cache-time                             | Time in minutes before reloading cache file (default: 180).                                                                                                                                                                                   |
| --oid-filter                                    | Choose OID used to filter storage (default: hrStorageDescr) (values: hrStorageDescr, hrFSMountPoint).                                                                                                                                         |
| --oid-display                                   | Choose OID used to display storage (default: hrStorageDescr) (values: hrStorageDescr, hrFSMountPoint).                                                                                                                                        |
| --display-transform-src --display-transform-dst | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run'                                                |
| --show-cache                                    | Display cache storage data.                                                                                                                                                                                                                   |
| --space-reservation                             | Some filesystem has space reserved (like ext4 for root). The value is in percent of total (default: none) (results like 'df' command).                                                                                                        |
| --filter-duplicate                              | Filter duplicate storages (in used size and total size).                                                                                                                                                                                      |
| --filter-storage-type                           | Filter storage types with a regexp (default: '^(hrStorageFixedDisk\|hrStorageNetworkDisk\|hrFSBerkeleyFFS)$').                                                                                                                                |

</TabItem>
<TabItem value="Hardware" label="Hardware">

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
| --component            | Which component to check (default: '.*'). Can be: 'fru', 'operating', 'alarm'.                                                                                                                                                                |
| --add-name-instance    | Add literal description for instance value (used in filter, absent-problem and threshold options).                                                                                                                                            |
| --filter               | Exclude the items given as a comma-separated list (example: --filter=fru). You can also exclude items from specific instances: --filter=fru,7.3.0.0                                                                                           |
| --absent-problem       | Return an error if an entity is not 'present' (default is skipping) (comma separated list) Can be specific or global: --absent-problem=fru,7.1.0.0                                                                                            |
| --no-component         | Define the expected status if no components are found (default: critical).                                                                                                                                                                    |
| --threshold-overload   | Use this option to override the status returned by the plugin when the status label matches a regular expression (syntax: section,\[instance,\]status,regexp). Example: --threshold-overload='operating,CRITICAL,^(?!(running)$)'             |
| --warning              | Set warning threshold (syntax: type,regexp,threshold) Example: --warning='operating-temperature,.*,30'                                                                                                                                        |
| --critical             | Set critical threshold (syntax: type,regexp,threshold) Example: --critical='operating-temperature,.*,40'                                                                                                                                      |
| --reload-cache-time    | Time in minutes before reloading cache file (default: 180). Use '-1' to disable cache reload.                                                                                                                                                 |

</TabItem>
<TabItem value="Ldp-Session-Status" label="Ldp-Session-Status">

| Option                 | Description                                                                                                                                           |
|:-----------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-*             | Filter entities and/or peer. Can be: 'entity', 'peer' (can be a regexp).                                                                              |
| --warning-status       | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{state\}                              |
| --critical-status      | Define the conditions to match for the status to be CRITICAL (default: '%\{state\} !~ /operational/i'). You can use the following variables: %\{state\}   |
| --warning-last-change  | Warning threshold in seconds.                                                                                                                         |
| --critical-last-change | Critical threshold in seconds.                                                                                                                        |

</TabItem>
<TabItem value="Lsp-Status" label="Lsp-Status">

| Option            | Description                                                                                                                                  |
|:------------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-*        | Filter LSPs. Can be: 'name', 'from', 'to' (can be a regexp).                                                                                 |
| --warning-status  | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{state\}                     |
| --critical-status | Define the conditions to match for the status to be CRITICAL (default: '%\{state\} !~ /up/i'). You can use the following variables: %\{state\}   |
| --warning-*       | Warning threshold. Can be: 'transition-count', 'last-transition' (seconds).                                                                  |
| --critical-*      | Critical threshold. Can be: 'transition-count', 'last-transition' (seconds).                                                                 |

</TabItem>
<TabItem value="Memory-Routing" label="Memory-Routing">

| Option                   | Description                                                             |
|:-------------------------|:------------------------------------------------------------------------|
| --filter                 | Filter operating (default: 'routing\|fpc').                             |
| --warning-* --critical-* | Thresholds. Can be: 'usage' (B), 'usage-free' (B), 'usage-prct' (%).    |

</TabItem>
<TabItem value="Rsvp-Session-Status" label="Rsvp-Session-Status">

| Option            | Description                                                                                                                                   |
|:------------------|:----------------------------------------------------------------------------------------------------------------------------------------------|
| --filter-*        | Filter sessions. Can be: 'name', 'from', 'to' (can be a regexp).                                                                              |
| --warning-status  | Define the conditions to match for the status to be WARNING (default: ''). You can use the following variables: %\{state\}                      |
| --critical-status | Define the conditions to match for the status to be CRITICAL (default: '%\{state\} !~ /up/i'). You can use the following variables: %\{state\}    |

</TabItem>
<TabItem value="Traffic-*" label="Traffic-*">

| Option                                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|:------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached                                     | Memcached server to use (only one server).                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --redis-server                                  | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                                                                                                                                                                                                                                                  |
| --redis-attribute                               | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                                                                                                                                                                                                                                          |
| --redis-db                                      | Set Redis database index.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| --failback-file                                 | Failback on a local file if Redis connection fails.                                                                                                                                                                                                                                                                                                                                                                                                              |
| --memexpiration                                 | Time to keep data in seconds (default: 86400).                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --statefile-dir                                 | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                                                                                                                                                                                                                                           |
| --statefile-suffix                              | Define a suffix to customize the statefile name (default: '').                                                                                                                                                                                                                                                                                                                                                                                                   |
| --statefile-concat-cwd                          | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.                                                                                                                                                                                                                      |
| --statefile-format                              | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                                                                                                                                                                                                                                            |
| --statefile-key                                 | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --statefile-cipher                              | Define the cipher algorithm to encrypt the cache (default: 'AES').                                                                                                                                                                                                                                                                                                                                                                                               |
| --add-global                                    | Check global port statistics (by default if no --add-* option is set).                                                                                                                                                                                                                                                                                                                                                                                           |
| --add-status                                    | Check interface status.                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --add-duplex-status                             | Check duplex status (with --warning-status and --critical-status).                                                                                                                                                                                                                                                                                                                                                                                               |
| --add-traffic                                   | Check interface traffic.                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --add-errors                                    | Check interface errors.                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --add-cast                                      | Check interface cast.                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --add-speed                                     | Check interface speed.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --add-volume                                    | Check interface data volume between two checks (not supposed to be graphed, useful for BI reporting).                                                                                                                                                                                                                                                                                                                                                            |
| --add-optical                                   | Check interface optical metrics.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --check-metrics                                 | If the expression is true, metrics are checked (default: '%\{opstatus\} eq "up"').                                                                                                                                                                                                                                                                                                                                                                                 |
| --warning-status                                | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{admstatus\}, %\{opstatus\}, %\{duplexstatus\}, %\{display\}                                                                                                                                                                                                                                                                                                         |
| --critical-status                               | Define the conditions to match for the status to be CRITICAL (default: '%\{admstatus\} eq "up" and %\{opstatus\} ne "up"'). You can use the following variables: %\{admstatus\}, %\{opstatus\}, %\{duplexstatus\}, %\{display\}                                                                                                                                                                                                                                              |
| --warning-errors                                | Set warning threshold for all error counters.                                                                                                                                                                                                                                                                                                                                                                                                                    |
| --critical-errors                               | Set critical threshold for all error counters.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --warning-* --critical-*                        | Thresholds (will superseed --\[warning-critical\]-errors). Can be: 'total-port', 'total-admin-up', 'total-admin-down', 'total-oper-up', 'total-oper-down', 'in-traffic', 'out-traffic', 'in-error', 'in-discard', 'out-error', 'out-discard', 'in-ucast', 'in-bcast', 'in-mcast', 'out-ucast', 'out-bcast', 'out-mcast', 'speed' (b/s).  And also: 'fcs-errors (%)', 'input-power' (dBm), 'bias-current' (mA), 'output-power' (dBm), 'module-temperature' (C).   |
| --units-traffic                                 | Units of thresholds for the traffic (default: 'percent\_delta') ('percent\_delta', 'bps', 'counter').                                                                                                                                                                                                                                                                                                                                                            |
| --units-errors                                  | Units of thresholds for errors/discards (default: 'percent\_delta') ('percent\_delta', 'percent', 'delta', 'deltaps', 'counter').                                                                                                                                                                                                                                                                                                                                |
| --units-cast                                    | Units of thresholds for communication types (default: 'percent\_delta') ('percent\_delta', 'percent', 'delta', 'deltaps', 'counter').                                                                                                                                                                                                                                                                                                                            |
| --nagvis-perfdata                               | Display traffic perfdata to be compatible with nagvis widget.                                                                                                                                                                                                                                                                                                                                                                                                    |
| --interface                                     | Set the interface (number expected) example: 1,2,... (empty means 'check all interfaces').                                                                                                                                                                                                                                                                                                                                                                       |
| --name                                          | Allows you to define the interface (in option --interface) byname instead of OID index. The name matching mode supports regular expressions.                                                                                                                                                                                                                                                                                                                     |
| --speed                                         | Set interface speed for incoming/outgoing traffic (in Mb).                                                                                                                                                                                                                                                                                                                                                                                                       |
| --speed-in                                      | Set interface speed for incoming traffic (in Mb).                                                                                                                                                                                                                                                                                                                                                                                                                |
| --speed-out                                     | Set interface speed for outgoing traffic (in Mb).                                                                                                                                                                                                                                                                                                                                                                                                                |
| --force-counters32                              | Force to use 32 bits counters (even in snmp v2c and v3). Should be used when 64 bits counters are buggy.                                                                                                                                                                                                                                                                                                                                                         |
| --reload-cache-time                             | Time in minutes before reloading cache file (default: 180).                                                                                                                                                                                                                                                                                                                                                                                                      |
| --oid-filter                                    | Define the OID to be used to filter interfaces (default: ifName) (values: ifDesc, ifAlias, ifName, IpAddr).                                                                                                                                                                                                                                                                                                                                                      |
| --oid-display                                   | Define the OID that will be used to name the interfaces (default: ifName) (values: ifDesc, ifAlias, ifName, IpAddr).                                                                                                                                                                                                                                                                                                                                             |
| --oid-extra-display                             | Add an OID to display.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --display-transform-src --display-transform-dst | Modify the interface name displayed by using a regular expression.  Example: adding --display-transform-src='eth' --display-transform-dst='ens' will replace all occurrences of 'eth' with 'ens'                                                                                                                                                                                                                                                                 |
| --show-cache                                    | Display cache interface data.                                                                                                                                                                                                                                                                                                                                                                                                                                    |

</TabItem>
</Tabs>

Pour un mode, la liste de toutes les options disponibles et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_juniper_mseries.pl \
	--plugin=network::juniper::mseries::plugin \
	--mode=interfaces \
	--help
```
