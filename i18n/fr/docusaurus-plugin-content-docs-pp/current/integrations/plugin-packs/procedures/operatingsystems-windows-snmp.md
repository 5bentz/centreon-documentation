---
id: operatingsystems-windows-snmp
title: Windows SNMP
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Contenu du pack

Windows est un système d’exploitation, autrement dit, un ensemble de programmes
et logiciels permettant de gérer les ressources d’un ordinateur.

### Modèles

Le connecteur de supervision **Windows SNMP** apporte un modèle d'hôte :

* **OS-Windows-SNMP-custom**

Le connecteur apporte les modèles de service suivants
(classés selon le modèle d'hôte auquel ils sont rattachés) :

<Tabs groupId="sync">
<TabItem value="OS-Windows-SNMP-custom" label="OS-Windows-SNMP-custom">

| Alias  | Modèle de service             | Description                                                                                                                                                                  |
|:-------|:------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cpu    | OS-Windows-Cpu-SNMP-custom    | Contrôle du taux d'utilisation du CPU de la machine. Ce contrôle pourra remonter la moyenne du taux d'utilisation des CPU ainsi que le taux par CPU pour les CPU multi-cœur |
| Memory | OS-Windows-Memory-SNMP-custom | Contrôle du taux d'utilisation de la mémoire vive                                                                                                                            |
| Swap   | OS-Windows-Swap-SNMP-custom   | Contrôle du taux d'utilisation de la mémoire virtuelle                                                                                                                       |

> Les services listés ci-dessus sont créés automatiquement lorsque le modèle d'hôte **OS-Windows-SNMP-custom** est utilisé.

</TabItem>
<TabItem value="Non rattachés à un modèle d'hôte" label="Non rattachés à un modèle d'hôte">

| Alias                | Modèle de service                           | Description                                                                                                                                                 | Découverte |
|:---------------------|:--------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------:|
| Disk-Generic-Id      | OS-Windows-Disk-Generic-Id-SNMP-custom      | Contrôle du taux d'espace libre disponible d'un disque (filtre par ID). Pour chaque contrôle apparaîtra le nom du disque                                    |            |
| Disk-Generic-Name    | OS-Windows-Disk-Generic-Name-SNMP-custom    | Contrôle du taux d'espace libre disponible d'un disque (filtre par nom). Pour chaque contrôle apparaîtra le nom du disque                                   |            |
| Disk-Global          | OS-Windows-Disk-Global-SNMP-custom          | Contrôle du taux d'espace libre disponible des disques. Pour chaque contrôle apparaîtra le nom du disque                                                    | X          |
| Ntp                  | OS-Windows-Ntp-SNMP-custom                  | Contrôle la synchronisation avec un serveur NTP                                                                                                             |            |
| Process-Generic      | OS-Windows-Process-Generic-SNMP-custom      | Contrôle permettant de vérifier que les processus Windows sont démarrés                                                                                     | X          |
| Service-Generic      | OS-Windows-Service-Generic-SNMP-custom      | Contrôle permettant de vérifier si les services Windows sont démarrés                                                                                       | X          |
| Traffic-Generic-Id   | OS-Windows-Traffic-Generic-Id-SNMP-custom   | Contrôle de la bande passante d'une interface (filtre par ID). Pour chaque contrôle apparaîtra le nom de l'interface                                        |            |
| Traffic-Generic-Name | OS-Windows-Traffic-Generic-Name-SNMP-custom | Contrôle de la bande passante d'une interface (filtre par nom). Pour chaque contrôle apparaîtra le nom de l'interface                                       |            |
| Traffic-Global       | OS-Windows-Traffic-Global-SNMP-custom       | Contrôle de la bande passante des interfaces. Pour chaque contrôle apparaîtra le nom de l'interface                                                         | X          |
| Uptime               | OS-Windows-Uptime-SNMP-custom               | Contrôle permettant de vérifier la disponibilité du serveur Windows depuis le dernier redémarrage. Il s'agit d'une indication, il n'y a pas de seuil défini |            |

> Les services listés ci-dessus ne sont pas créés automatiquement lorsqu'un modèle d'hôte est appliqué. Pour les utiliser, [créez un service manuellement](/docs/monitoring/basic-objects/services) et appliquez le modèle de service souhaité.

> Si la case **Découverte** est cochée, cela signifie qu'une règle de découverte de service existe pour ce service.

</TabItem>
</Tabs>

### Règles de découverte

#### Découverte d'hôtes

| Nom de la règle | Description                                                                                                                                                  |
|:----------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SNMP Agents     | Découvre les ressources via un scan réseau SNMP. Installez le connecteur [Generic SNMP](./applications-protocol-snmp.md) pour obtenir la règle de découverte |

Rendez-vous sur la [documentation dédiée](/docs/monitoring/discovery/hosts-discovery) pour en savoir plus sur la découverte automatique d'hôtes.

#### Découverte de service

| Nom de la règle                | Description                                                            |
|:-------------------------------|:-----------------------------------------------------------------------|
| OS-Windows-SNMP-Disk-Name      | Découvre les disques et supervise le statut et l'utilisation           |
| OS-Windows-SNMP-Processes-Name | Découvre les processus et supervise le statut et l'utilisation         |
| OS-Windows-SNMP-Services-Name  | Découvre les services et supervise le statut                           |
| OS-Windows-SNMP-Traffic-Name   | Découvre les interfaces réseau et supervise le statut et l'utilisation |

Rendez-vous sur la [documentation dédiée](/docs/monitoring/discovery/services-discovery)
pour en savoir plus sur la découverte automatique de services et sa [planification](/docs/monitoring/discovery/services-discovery/#règles-de-découverte).

### Métriques & statuts collectés

Voici le tableau des services pour ce connecteur, détaillant les métriques rattachées à chaque service.

<Tabs groupId="sync">
<TabItem value="Cpu" label="Cpu">

| Métrique                                   | Unité |
|:-------------------------------------------|:------|
| cpu.utilization.percentage                 | %     |
| *cpu_core*#core.cpu.utilization.percentage | %     |

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
<TabItem value="Memory" label="Memory">

| Métrique           | Unité |
|:-------------------|:------|
| memory.usage.bytes | B     |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Ntp" label="Ntp">

| Métrique            | Unité |
|:--------------------|:------|
| time.offset.seconds | s     |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
<TabItem value="Process-Generic" label="Process-Generic">

| Métrique    | Unité |
|:------------|:------|
| nbproc      | N/A   |
| mem_total   | B     |
| mem_avg     | B     |
| cpu_total   | %     |

</TabItem>
<TabItem value="Service-Generic" label="Service-Generic">

| Métrique                        | Unité |
|:--------------------------------|:------|
| services.total.count            | count |
| services.active.count           | count |
| services.continue.pending.count | count |
| services.pause.pending.count    | count |
| services.paused.count           | count |
| *services*#status               | N/A   |

</TabItem>
<TabItem value="Swap" label="Swap">

| Métrique         | Unité |
|:-----------------|:------|
| swap.usage.bytes | B     |

</TabItem>
<TabItem value="Traffic-*" label="Traffic-*">

| Métrique                                                  | Unité |
|:----------------------------------------------------------|:------|
| interface status                                          |       |
| *interface_name*#interface.traffic.in.bitspersecond       | b/s   |
| *interface_name*#interface.traffic.out.bitspersecond      | b/s   |
| *interface_name*#interface.packets.in.error.percentage    | %     |
| *interface_name*#interface.packets.in.discard.percentage  | %     |
| *interface_name*#interface.packets.out.error.percentage   | %     |
| *interface_name*#interface.packets.out.discard.percentage | %     |

> Concerne les modèles de service suivants : Traffic-Generic-Id, Traffic-Generic-Name, Traffic-Global

</TabItem>
<TabItem value="Uptime" label="Uptime">

| Métrique              | Unité |
|:----------------------|:------|
| system.uptime.seconds | s     |

> Pour obtenir ce nouveau format de métrique, incluez la valeur **--use-new-perfdata** dans la macro de service **EXTRAOPTIONS**.

</TabItem>
</Tabs>

## Prérequis

Configurez le service SNMP en V2 pour superviser le système Windows.

> Les instructions ci-après peuvent changer en fonction de votre version de
> Windows. Référez-vous à la documentation officielle de Microsoft le cas
> échéant.

  - Installez la fonctionnalité SNMP dans le gestionnaire de serveur de Windows : **Gestionnaire de serveur > Ajouter des rôles et des fonctionnalités > Installation basée sur un rôle ou une fonctionnalité > Service SNMP**.

  - Paramétrez le service **SNMP agent** avec votre communauté et les IP des collecteurs qui feront les requêtes.

  - Redémarrez le service SNMP après avoir configuré celui-ci.

## Flux réseaux

La communication doit être possible sur le port UDP 161 depuis le collecteur Centreon vers le serveur Windows supervisé.

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
dnf install centreon-pack-operatingsystems-windows-snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-pack-operatingsystems-windows-snmp
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-pack-operatingsystems-windows-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-pack-operatingsystems-windows-snmp
```

</TabItem>
</Tabs>

2. Quel que soit le type de la licence (*online* ou *offline*), installez le connecteur **Windows SNMP**
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
dnf install centreon-plugin-Operatingsystems-Windows-Snmp
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```bash
dnf install centreon-plugin-Operatingsystems-Windows-Snmp
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```bash
apt install centreon-plugin-operatingsystems-windows-snmp
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```bash
yum install centreon-plugin-Operatingsystems-Windows-Snmp
```

</TabItem>
</Tabs>

## Utiliser le connecteur de supervision

### Utiliser un modèle d'hôte issu du connecteur

1. Ajoutez un hôte à Centreon depuis la page **Configuration > Hôtes**.
2. Complétez les champs **Nom**, **Alias** & **IP Address/DNS** correspondant à votre ressource.
3. Appliquez le modèle d'hôte **OS-Windows-SNMP-custom**.

> Si vous utilisez SNMP en version 3, vous devez configurer les paramètres spécifiques associés via la macro **SNMPEXTRAOPTIONS**.
> Plus d'informations dans la section [Troubleshooting SNMP](../getting-started/how-to-guides/troubleshooting-plugins.md#snmpv3-options-mapping).

| Macro            | Description                                                                                   | Valeur par défaut | Obligatoire |
|:-----------------|:----------------------------------------------------------------------------------------------|:------------------|:-----------:|
| SNMPEXTRAOPTIONS | Any extra option you may want to add to every command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

4. [Déployez la configuration](/docs/monitoring/monitoring-servers/deploying-a-configuration). L'hôte apparaît dans la liste des hôtes supervisés, et dans la page **Statut des ressources**. La commande envoyée par le connecteur est indiquée dans le panneau de détails de l'hôte : celle-ci montre les valeurs des macros.

### Utiliser un modèle de service issu du connecteur

1. Si vous avez utilisé un modèle d'hôte et coché la case **Créer aussi les services liés aux modèles**, les services associés au modèle ont été créés automatiquement, avec les modèles de services correspondants. Sinon, [créez les services désirés manuellement](/docs/monitoring/basic-objects/services) et appliquez-leur un modèle de service.
2. Renseignez les macros désirées (par exemple, ajustez les seuils d'alerte). Les macros indiquées ci-dessous comme requises (**Obligatoire**) doivent être renseignées.

<Tabs groupId="sync">
<TabItem value="Cpu" label="Cpu">

| Macro        | Description                                                                                 | Valeur par défaut | Obligatoire |
|:-------------|:--------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNING      | Warning threshold average CPU utilization                                                   | 80                |             |
| CRITICAL     | Critical threshold average CPU utilization                                                  | 90                |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Disk-Generic-Id" label="Disk-Generic-Id">

| Macro        | Description                                                                                                                                                                                    | Valeur par défaut                             | Obligatoire |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------|:-----------:|
| TRANSFORMSRC | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | ^(..).*                                       |             |
| TRANSFORMDST | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | $1                                            |             |
| DISKID       | Set the storage (number expected) example: 1, 2,... (empty means 'check all storage')                                                                                                          |                                               |             |
| WARNING      | Warning threshold                                                                                                                                                                              | 80                                            |             |
| CRITICAL     | Critical threshold                                                                                                                                                                             | 90                                            |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                                                                                    | --filter-perfdata='storage.space\|used\|free' |             |

</TabItem>
<TabItem value="Disk-Generic-Name" label="Disk-Generic-Name">

| Macro        | Description                                                                                                                                                                                    | Valeur par défaut                             | Obligatoire |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------|:-----------:|
| TRANSFORMSRC | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | ^(..).*                                       |             |
| TRANSFORMDST | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | $1                                            |             |
| DISKNAME     | Set the storage (number expected) example: 1, 2,... (empty means 'check all storage')                                                                                                          |                                               |             |
| WARNING      | Warning threshold                                                                                                                                                                              | 80                                            |             |
| CRITICAL     | Critical threshold                                                                                                                                                                             | 90                                            |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                                                                                    | --filter-perfdata='storage.space\|used\|free' |             |

</TabItem>
<TabItem value="Disk-Global" label="Disk-Global">

| Macro        | Description                                                                                                                                                                                    | Valeur par défaut                                       | Obligatoire |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------|:-----------:|
| FILTER       | Set the storage (number expected) example: 1, 2,... (empty means 'check all storage')                                                                                                          | .*                                                      |             |
| TRANSFORMSRC | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | ^(..).*                                                 |             |
| TRANSFORMDST | Modify the storage name displayed by using a regular expression.  Example: adding --display-transform-src='dev' --display-transform-dst='run' will replace all occurrences of 'dev' with 'run' | $1                                                      |             |
| WARNING      | Warning threshold                                                                                                                                                                              | 80                                                      |             |
| CRITICAL     | Critical threshold                                                                                                                                                                             | 90                                                      |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                                                                                    | --verbose --filter-perfdata='storage.space\|used\|free' |             |

</TabItem>
<TabItem value="Memory" label="Memory">

| Macro        | Description                                                                                 | Valeur par défaut | Obligatoire |
|:-------------|:--------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNING      | Warning threshold                                                                           | 80                |             |
| CRITICAL     | Critical threshold                                                                          | 90                |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Ntp" label="Ntp">

| Macro        | Description                                                                                                     | Valeur par défaut | Obligatoire |
|:-------------|:----------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| NTPADDR      | Set the ntp hostname (if not set, localtime is used)                                                            |                   |             |
| NTPPORT      | Set the ntp port (default: 123)                                                                                 |                   |             |
| TIMEZONE     | Set the timezone of distant server. For Windows, you need to set it. Can use format: 'Europe/London' or '+0100' |                   |             |
| WARNING      | Time offset warning threshold (in seconds)                                                                      | -1:1              |             |
| CRITICAL     | Time offset critical Threshold (in seconds)                                                                     | -2:2              |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                     |                   |             |

</TabItem>
<TabItem value="Process-Generic" label="Process-Generic">

| Macro        | Description                                                                                 | Valeur par défaut | Obligatoire |
|:-------------|:--------------------------------------------------------------------------------------------|:------------------|:-----------:|
| PROCESSNAME  | Filter process name                                                                         |                   |             |
| PROCESSPATH  | Filter process path                                                                         |                   |             |
| PROCESSARGS  | Filter process arguments                                                                    |                   |             |
| WARNING      | Warning threshold of matching processes count                                               |                   |             |
| CRITICAL     | Critical threshold of matching processes count                                              |                   |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Service-Generic" label="Service-Generic">

| Macro                   | Description                                                                                                                 | Valeur par défaut | Obligatoire |
|:------------------------|:----------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| SERVICENAME             | DEPRECATED. Use --filter-name instead                                                                                       |                   |             |
| STATE                   | DEPRECATED. Use --critical/warning-status instead                                                                           |                   |             |
| FILTERNAME              | Filter by service name (can be a regexp)                                                                                    |                   |             |
| WARNING                 | DEPRECATED. Use --warning-active instead                                                                                    |                   |             |
| CRITICAL                | DEPRECATED. Use --critical-active instead                                                                                   |                   |             |
| CRITICALACTIVE          | Thresholds on services count                                                                                                | 1:                |             |
| WARNINGACTIVE           | Thresholds on services count                                                                                                |                   |             |
| WARNINGCONTINUEPENDING  | Thresholds on services count                                                                                                |                   |             |
| CRITICALCONTINUEPENDING | Thresholds on services count                                                                                                |                   |             |
| WARNINGPAUSED           | Thresholds on services count                                                                                                |                   |             |
| CRITICALPAUSED          | Thresholds on services count                                                                                                |                   |             |
| WARNINGPAUSEPENDING     | Thresholds on services count                                                                                                |                   |             |
| CRITICALPAUSEPENDING    | Thresholds on services count                                                                                                |                   |             |
| WARNINGSTATUS           | Set WARNING or CRITICAL threshold for status. You can use the following variables: %\{operating_state\}, %\{installed_state\} |                   |             |
| CRITICALSTATUS          | Set WARNING or CRITICAL threshold for status. You can use the following variables: %\{operating_state\}, %\{installed_state\} |                   |             |
| EXTRAOPTIONS            | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                 | --verbose         |             |

</TabItem>
<TabItem value="Swap" label="Swap">

| Macro        | Description                                                                                 | Valeur par défaut | Obligatoire |
|:-------------|:--------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNING      | Warning threshold in percent                                                                | 80                |             |
| CRITICAL     | Critical threshold in percent                                                               | 90                |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Traffic-Generic-Id" label="Traffic-Generic-Id">

| Macro        | Description                                                                                 | Valeur par défaut | Obligatoire |
|:-------------|:--------------------------------------------------------------------------------------------|:------------------|:-----------:|
| INTERFACEID  | Set the interface (number expected) example: 1,2,... (empty means 'check all interfaces')   |                   |             |
| WARNINGIN    | Thresholds                                                                                  | 80                |             |
| CRITICALIN   | Thresholds                                                                                  | 90                |             |
| WARNINGOUT   | Thresholds                                                                                  | 80                |             |
| CRITICALOUT  | Thresholds                                                                                  | 90                |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Traffic-Generic-Name" label="Traffic-Generic-Name">

| Macro         | Description                                                                                 | Valeur par défaut | Obligatoire |
|:--------------|:--------------------------------------------------------------------------------------------|:------------------|:-----------:|
| INTERFACENAME | Set the interface (number expected) example: 1,2,... (empty means 'check all interfaces')   |                   |             |
| WARNINGIN     | Thresholds                                                                                  | 80                |             |
| CRITICALIN    | Thresholds                                                                                  | 90                |             |
| WARNINGOUT    | Thresholds                                                                                  | 80                |             |
| CRITICALOUT   | Thresholds                                                                                  | 90                |             |
| EXTRAOPTIONS  | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) |                   |             |

</TabItem>
<TabItem value="Traffic-Global" label="Traffic-Global">

| Macro          | Description                                                                                                                                                                                                         | Valeur par défaut | Obligatoire |
|:---------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------|:-----------:|
| FILTER         | Set the interface (number expected) example: 1,2,... (empty means 'check all interfaces')                                                                                                                           | .*                |             |
| WARNINGIN      | Thresholds                                                                                                                                                                                                          | 80                |             |
| CRITICALIN     | Thresholds                                                                                                                                                                                                          | 90                |             |
| WARNINGOUT     | Thresholds                                                                                                                                                                                                          | 80                |             |
| CRITICALOUT    | Thresholds                                                                                                                                                                                                          | 90                |             |
| CRITICALSTATUS | Define the conditions to match for the status to be CRITICAL (default: '%\{admstatus\} eq "up" and %\{opstatus\} ne "up"'). You can use the following variables: %\{admstatus\}, %\{opstatus\}, %\{duplexstatus\}, %\{display\} |                   |             |
| EXTRAOPTIONS   | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles)                                                                                                                         | --verbose         |             |

</TabItem>
<TabItem value="Uptime" label="Uptime">

| Macro        | Description                                                                                 | Valeur par défaut | Obligatoire |
|:-------------|:--------------------------------------------------------------------------------------------|:------------------|:-----------:|
| WARNING      | Warning threshold                                                                           |                   |             |
| CRITICAL     | Critical threshold                                                                          |                   |             |
| EXTRAOPTIONS | Any extra option you may want to add to the command (example: a --verbose flag). Toutes les options sont listées [ici](#options-disponibles) | --check-overload  |             |

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
/usr/lib/centreon/plugins/centreon_windows_snmp.pl \
	--plugin=os::windows::snmp::plugin \
	--mode=service \
    --hostname=10.30.2.114 \
    --snmp-version='2c' \
    --snmp-community='windows_ro' \
    --filter-name='Server' \
    --critical-active=1
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK: Service 'Server' state is 'active' [installed state: 'installed'] | 'services.active.count'=1;;1:;0; 'services.continue.pending.count'=0;;;0; 'services.pause.pending.count'=0;;;0; 'services.paused.count'=0;;;0;
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
/usr/lib/centreon/plugins/centreon_windows_snmp.pl \
	--plugin=os::windows::snmp::plugin \
	--list-mode
```

Le plugin apporte les modes suivants :

| Mode                                                                                                                         | Modèle de service associé                                                                                                             |
|:-----------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------|
| cpu [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/cpu.pm)]                        | OS-Windows-Cpu-SNMP-custom                                                                                                            |
| interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/interfaces.pm)]          | OS-Windows-Traffic-Generic-Id-SNMP-custom<br />OS-Windows-Traffic-Generic-Name-SNMP-custom<br />OS-Windows-Traffic-Global-SNMP-custom |
| list-interfaces [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/listinterfaces.pm)] | Used for service discovery                                                                                                            |
| list-processes [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/listprocesses.pm)]   | Used for service discovery                                                                                                            |
| list-services [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/os/windows/snmp/mode/listservices.pm)]   | Used for service discovery                                                                                                            |
| list-storages [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/liststorages.pm)]     | Used for service discovery                                                                                                            |
| memory [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/os/windows/snmp/mode/memory.pm)]                | OS-Windows-Memory-SNMP-custom                                                                                                         |
| processcount [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/processcount.pm)]      | OS-Windows-Process-Generic-SNMP-custom                                                                                                |
| service [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/os/windows/snmp/mode/service.pm)]              | OS-Windows-Service-Generic-SNMP-custom                                                                                                |
| storage [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/storage.pm)]                | OS-Windows-Disk-Generic-Id-SNMP-custom<br />OS-Windows-Disk-Generic-Name-SNMP-custom<br />OS-Windows-Disk-Global-SNMP-custom          |
| swap [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/os/windows/snmp/mode/swap.pm)]                    | OS-Windows-Swap-SNMP-custom                                                                                                           |
| time [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/ntp.pm)]                       | OS-Windows-Ntp-SNMP-custom                                                                                                            |
| uptime [[code](https://github.com/centreon/centreon-plugins/blob/develop/src/snmp_standard/mode/uptime.pm)]                  | OS-Windows-Uptime-SNMP-custom                                                                                                         |

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
| --change-perfdata --extend-perfdata        | Change or extend perfdata. Syntax: --extend-perfdata=searchlabel,newlabel,target\[,\[newuom\],\[min\],\[m ax\]\]  Common examples:      Convert storage free perfdata into used:     --change-perfdata=free,used,invert()      Convert storage free perfdata into used:     --change-perfdata=used,free,invert()      Scale traffic values automatically:     --change-perfdata=traffic,,scale(auto)      Scale traffic values in Mbps:     --change-perfdata=traffic\_in,,scale(Mbps),mbps      Change traffic values in percent:     --change-perfdata=traffic\_in,,percent()                                                                                                                                                                                                                                                                                                                                                                          |
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
| --output-file                              | Write output in file (can be combined with json, xml and openmetrics options). example:: --output-file=/tmp/output.txt will write the output in /tmp/output.txt.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
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
<TabItem value="Cpu" label="Cpu">

| Option             | Description                                   |
|:-------------------|:----------------------------------------------|
| --use-ucd          | Use UCD mib for cpu average.                  |
| --warning-average  | Warning threshold average CPU utilization.    |
| --critical-average | Critical threshold average CPU utilization.   |
| --warning-core     | Warning thresholds for each CPU core          |
| --critical-core    | Critical thresholds for each CPU core         |

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
| --show-cache                                    | Display cache storage datas.                                                                                                                                                                                                                  |
| --space-reservation                             | Some filesystem has space reserved (like ext4 for root). The value is in percent of total (default: none) (results like 'df' command).                                                                                                        |
| --filter-duplicate                              | Filter duplicate storages (in used size and total size).                                                                                                                                                                                      |
| --filter-storage-type                           | Filter storage types with a regexp (default: '^(hrStorageFixedDisk\|hrStorageNetworkDisk\|hrFSBerkeleyFFS)$').                                                                                                                                |

</TabItem>
<TabItem value="Memory" label="Memory">

| Option       | Description                                            |
|:-------------|:-------------------------------------------------------|
| --units      | Units of thresholds (default: '%') ('%', 'absolute').  |
| --free       | Thresholds are on free space left.                     |
| --warning-*  | Warning threshold. Can be: 'memory'.                   |
| --critical-* | Critical threshold. Can be: 'memory'.                  |

</TabItem>
<TabItem value="Ntp" label="Ntp">

| Option            | Description                                                                                                         |
|:------------------|:--------------------------------------------------------------------------------------------------------------------|
| --oid             | Override default OID.                                                                                               |
| --warning-offset  | Time offset warning threshold (in seconds).                                                                         |
| --critical-offset | Time offset critical Threshold (in seconds).                                                                        |
| --ntp-hostname    | Set the ntp hostname (if not set, localtime is used).                                                               |
| --ntp-port        | Set the ntp port (default: 123).                                                                                    |
| --timezone        | Set the timezone of distant server. For Windows, you need to set it. Can use format: 'Europe/London' or '+0100'.    |

</TabItem>
<TabItem value="Process-Generic" label="Process-Generic">

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
| --process-status       | Filter process status. Can be a regexp. (default: 'running\|runnable').                                                                                                                                                                       |
| --process-name         | Filter process name.                                                                                                                                                                                                                          |
| --regexp-name          | Allows to use regexp to filter process name (with option --process-name).                                                                                                                                                                     |
| --process-path         | Filter process path.                                                                                                                                                                                                                          |
| --regexp-path          | Allows to use regexp to filter process path (with option --process-path).                                                                                                                                                                     |
| --process-args         | Filter process arguments.                                                                                                                                                                                                                     |
| --regexp-args          | Allows to use regexp to filter process arguments (with option --process-args).                                                                                                                                                                |
| --warning              | Warning threshold of matching processes count.                                                                                                                                                                                                |
| --critical             | Critical threshold of matching processes count.                                                                                                                                                                                               |
| --memory               | Check memory usage.                                                                                                                                                                                                                           |
| --warning-mem-each     | Warning threshold of memory used by each matching processes (in Bytes).                                                                                                                                                                       |
| --critical-mem-each    | Critical threshold of memory used by each matching processes (in Bytes).                                                                                                                                                                      |
| --warning-mem-total    | Warning threshold of total memory used by matching processes (in Bytes).                                                                                                                                                                      |
| --critical-mem-total   | Critical threshold of total memory used by matching processes (in Bytes).                                                                                                                                                                     |
| --warning-mem-avg      | Warning threshold of average memory used by matching processes (in Bytes).                                                                                                                                                                    |
| --critical-mem-avg     | Critical threshold of average memory used by matching processes (in Bytes).                                                                                                                                                                   |
| --cpu                  | Check cpu usage. Should be used with fix processes. If processespid changes too much, the plugin can't compute values.                                                                                                                        |
| --warning-cpu-total    | Warning threshold of cpu usage for all processes (in percent). CPU usage is in % of one cpu, so maximum can be 100% * number of CPU and a process can have a value greater than 100%.                                                         |
| --critical-cpu-total   | Critical threshold of cpu usage for all processes (in percent). CPU usage is in % of one cpu, so maximum can be 100% * number of CPU and a process can have a value greater than 100%.                                                        |
| --top                  | Enable top memory usage display.                                                                                                                                                                                                              |
| --top-num              | Number of processes in top memory display (default: 5).                                                                                                                                                                                       |
| --top-size             | Minimum memory usage to be in top memory display (default: 52428800 -\> 50 MB).                                                                                                                                                               |

</TabItem>
<TabItem value="Service-Generic" label="Service-Generic">

| Option                             | Description                                                                                                                    |
|:-----------------------------------|:-------------------------------------------------------------------------------------------------------------------------------|
| --filter-name                      | Filter by service name (can be a regexp).                                                                                      |
| --warning-status --critical-status | Set WARNING or CRITICAL threshold for status. You can use the following variables: %\{operating_state\}, %\{installed_state\}.   |
| --warning-* --critical-*           | Thresholds on services count. Can be: 'total', 'active', 'continue-pending', 'pause-pending', 'paused'.                        |
| --warning                          | DEPRECATED. Use --warning-active instead.                                                                                      |
| --critical                         | DEPRECATED. Use --critical-active instead.                                                                                     |
| --service                          | DEPRECATED. Use --filter-name instead.                                                                                         |
| --regexp                           | DEPRECATED. Use --filter-name instead.                                                                                         |
| --state                            | DEPRECATED. Use --critical/warning-status instead.                                                                             |

</TabItem>
<TabItem value="Swap" label="Swap">

| Option      | Description                                                                                                                                   |
|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------|
| --warning   | Warning threshold in percent.                                                                                                                 |
| --critical  | Critical threshold in percent.                                                                                                                |
| --real-swap | Use this option to remove physical memory from Windows SNMP swap values. Using that option can give wrong values (incoherent or negative).    |

</TabItem>
<TabItem value="Traffic-*" label="Traffic-*">

| Option                                          | Description                                                                                                                                                                                                                                                                                |
|:------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --memcached                                     | Memcached server to use (only one server).                                                                                                                                                                                                                                                 |
| --redis-server                                  | Redis server to use (only one server). Syntax: address\[:port\]                                                                                                                                                                                                                            |
| --redis-attribute                               | Set Redis Options (--redis-attribute="cnx\_timeout=5").                                                                                                                                                                                                                                    |
| --redis-db                                      | Set Redis database index.                                                                                                                                                                                                                                                                  |
| --failback-file                                 | Failback on a local file if Redis connection fails.                                                                                                                                                                                                                                        |
| --memexpiration                                 | Time to keep data in seconds (default: 86400).                                                                                                                                                                                                                                             |
| --statefile-dir                                 | Define the cache directory (default: '/var/lib/centreon/centplugins').                                                                                                                                                                                                                     |
| --statefile-suffix                              | Define a suffix to customize the statefile name (default: '').                                                                                                                                                                                                                             |
| --statefile-concat-cwd                          | If used with the '--statefile-dir' option, the latter's value will be used as a sub-directory of the current working directory. Useful on Windows when the plugin is compiled, as the file system and permissions are different from Linux.                                                |
| --statefile-format                              | Define the format used to store the cache. Available formats: 'dumper', 'storable', 'json' (default).                                                                                                                                                                                      |
| --statefile-key                                 | Define the key to encrypt/decrypt the cache.                                                                                                                                                                                                                                               |
| --statefile-cipher                              | Define the cipher algorithm to encrypt the cache (default: 'AES').                                                                                                                                                                                                                         |
| --add-global                                    | Check global port statistics (by default if no --add-* option is set).                                                                                                                                                                                                                     |
| --add-status                                    | Check interface status.                                                                                                                                                                                                                                                                    |
| --add-duplex-status                             | Check duplex status (with --warning-status and --critical-status).                                                                                                                                                                                                                         |
| --add-traffic                                   | Check interface traffic.                                                                                                                                                                                                                                                                   |
| --add-errors                                    | Check interface errors.                                                                                                                                                                                                                                                                    |
| --add-cast                                      | Check interface cast.                                                                                                                                                                                                                                                                      |
| --add-speed                                     | Check interface speed.                                                                                                                                                                                                                                                                     |
| --add-volume                                    | Check interface data volume between two checks (not supposed to be graphed, useful for BI reporting).                                                                                                                                                                                      |
| --check-metrics                                 | If the expression is true, metrics are checked (default: '%\{opstatus\} eq "up"').                                                                                                                                                                                                           |
| --warning-status                                | Define the conditions to match for the status to be WARNING. You can use the following variables: %\{admstatus\}, %\{opstatus\}, %\{duplexstatus\}, %\{display\}                                                                                                                                   |
| --critical-status                               | Define the conditions to match for the status to be CRITICAL (default: '%\{admstatus\} eq "up" and %\{opstatus\} ne "up"'). You can use the following variables: %\{admstatus\}, %\{opstatus\}, %\{duplexstatus\}, %\{display\}                                                                        |
| --warning-* --critical-*                        | Thresholds. Can be: 'total-port', 'total-admin-up', 'total-admin-down', 'total-oper-up', 'total-oper-down', 'in-traffic', 'out-traffic', 'in-error', 'in-discard', 'out-error', 'out-discard', 'in-ucast', 'in-bcast', 'in-mcast', 'out-ucast', 'out-bcast', 'out-mcast', 'speed' (b/s).   |
| --units-traffic                                 | Units of thresholds for the traffic (default: 'percent\_delta') ('percent\_delta', 'bps', 'counter').                                                                                                                                                                                      |
| --units-errors                                  | Units of thresholds for errors/discards (default: 'percent\_delta') ('percent\_delta', 'percent', 'delta', 'deltaps', 'counter').                                                                                                                                                          |
| --units-cast                                    | Units of thresholds for communication types (default: 'percent\_delta') ('percent\_delta', 'percent', 'delta', 'deltaps', 'counter').                                                                                                                                                      |
| --nagvis-perfdata                               | Display traffic perfdata to be compatible with nagvis widget.                                                                                                                                                                                                                              |
| --interface                                     | Set the interface (number expected) example: 1,2,... (empty means 'check all interfaces').                                                                                                                                                                                                 |
| --name                                          | Allows you to define the interface (in option --interface) byname instead of OID index. The name matching mode supports regular expressions.                                                                                                                                               |
| --speed                                         | Set interface speed for incoming/outgoing traffic (in Mb).                                                                                                                                                                                                                                 |
| --speed-in                                      | Set interface speed for incoming traffic (in Mb).                                                                                                                                                                                                                                          |
| --speed-out                                     | Set interface speed for outgoing traffic (in Mb).                                                                                                                                                                                                                                          |
| --map-speed-dsl                                 | Get interface speed configuration for interface type 'adsl' and 'vdsl2'.  Syntax: --map-speed-dsl=interface-src-name,interface-dsl-name  E.g: --map-speed-dsl=Et0.835,Et0-vdsl2                                                                                                            |
| --force-counters64                              | Force to use 64 bits counters only. Can be used to improve performance.                                                                                                                                                                                                                    |
| --force-counters32                              | Force to use 32 bits counters (even in snmp v2c and v3). Should be used when 64 bits counters are buggy.                                                                                                                                                                                   |
| --reload-cache-time                             | Time in minutes before reloading cache file (default: 180).                                                                                                                                                                                                                                |
| --oid-filter                                    | Define the OID to be used to filter interfaces (default: ifName) (values: ifDesc, ifAlias, ifName, IpAddr).                                                                                                                                                                                |
| --oid-display                                   | Define the OID that will be used to name the interfaces (default: ifName) (values: ifDesc, ifAlias, ifName, IpAddr).                                                                                                                                                                       |
| --oid-extra-display                             | Add an OID to display.                                                                                                                                                                                                                                                                     |
| --display-transform-src --display-transform-dst | Modify the interface name displayed by using a regular expression.  Example: adding --display-transform-src='eth' --display-transform-dst='ens' will replace all occurrences of 'eth' with 'ens'                                                                                           |
| --show-cache                                    | Display cache interface datas.                                                                                                                                                                                                                                                             |

</TabItem>
<TabItem value="Uptime" label="Uptime">

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
| --warning-uptime       | Warning threshold.                                                                                                                                                                                                                            |
| --critical-uptime      | Critical threshold.                                                                                                                                                                                                                           |
| --add-sysdesc          | Display system description.                                                                                                                                                                                                                   |
| --force-oid            | Can choose your oid (numeric format only).                                                                                                                                                                                                    |
| --check-overload       | Uptime counter limit is 4294967296 and overflow. With that option, we manage the counter going back. But there is a few chance we can miss a reboot.                                                                                          |
| --reboot-window        | To be used with check-overload option. Time in milliseconds (default: 5000) You increase the chance of not missing a reboot if you decrease that value.                                                                                       |
| --unit                 | Select the time unit for thresholds. May be 's' for seconds,'m'for minutes, 'h' for hours, 'd' for days, 'w' for weeks. Default is seconds.                                                                                                   |

</TabItem>
</Tabs>

Pour un mode, la liste de toutes les options disponibles et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande :

```bash
/usr/lib/centreon/plugins/centreon_windows_snmp.pl \
	--plugin=os::windows::snmp::plugin \
	--mode=interfaces \
	--help
```
