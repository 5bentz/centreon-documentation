---
id: applications-awa-jmx
title: AWA (Automic Workload Automation) JMX
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## Contenu du Pack

### Modèles

Le connecteur de supervision Centreon Awa JMX apporte 1 modèle d'hôte :
* App-Awa-JMX-custom

Il apporte les Modèles de Service suivants :

| Service Alias | Service Template   | Default |
|:--------------|:-------------------|:--------|
| Awa-Agent     | App-Awa-Agent-JMX  | X       |
| Awa-Queue     | App-Awa-Queue-JMX  | X       |
| Awa-Server    | App-Awa-Server-JMX | X       |

### Métriques & statuts collectés

<Tabs groupId="sync">
<TabItem value="Awa-Agent" label="Awa-Agent">

| Metric Name | Unit   |
|:------------|:-------|
| status      | string |

</TabItem>
<TabItem value="Awa-Queue" label="Awa-Queue">

| Metric Name | Unit   |
|:------------|:-------|
| status      | string |

</TabItem>
<TabItem value="Awa-Server" label="Awa-Server">

| Metric Name | Unit   |
|:------------|:-------|
| status      | string |

</TabItem>
</Tabs>

## Prerequisites

Veuillez installer l'agent Jolokia sur votre serveur AWA ([Jolokia download page](https://jolokia.org/download.html)).
Demandez à votre administrateur de le déployer et de vous en fournir l'URL.

## Installation

<Tabs groupId="sync">
<TabItem value="Online License" label="Online License">

1. Installer le Plugin Centreon sur tous les collecteurs Centreon devant superviser des resources **AWA JMX**:

```bash
yum install centreon-plugin-Applications-Awa-Jmx
```

2. Sur l'interface Web de Centreon, installer le connecteur de supervision **Awa JMX** depuis la page **Configuration > Packs de plugins**.

</TabItem>
<TabItem value="Offline License" label="Offline License">

1. Installer le Plugin Centreon sur tous les collecteurs Centreon devant superviser des resources **AWA JMX**:

```bash
yum install centreon-plugin-Applications-Awa-Jmx
```

2. Sur le serveur Central Centreon, installer le RPM du Pack **Awa JMX**:

```bash
yum install centreon-pack-applications-awa-jmx
```

3. Sur l'interface Web de Centreon, installer le connecteur de supervision **Awa JMX** depuis la page **Configuration > Packs de plugins**.

</TabItem>
</Tabs>

## Configuration

### Hôte

* Ajoutez un Hôte à Centreon depuis la page **Configuration > Hôtes**
* Complétez les champs **Nom**, **Alias** & **IP Address / DNS** correspondant à votre serveur **AWA JMX**.
* Appliquez le Modèle d'Hôte **applications-awa-jmx-custom**

* Une fois le modèle appliqué, renseignez les macros correspondantes. Attention, certaines macros sont obligatoires ("mandatory"). 

| Mandatory | Name         | Description                                                                                     |
|:----------|:-------------|:------------------------------------------------------------------------------------------------|
|           | EXTRAOPTIONS | Any extra option you may want to add to every command\_line (eg. a --verbose flag) |

## Comment puis-je tester le Plugin et que signifient les options des commandes ? 

Une fois le Plugin installé, vous pouvez tester celui-ci directement en ligne 
de commande depuis votre collecteur Centreon en vous connectant avec 
l'utilisateur **centreon-engine**:

```bash
/usr/lib/centreon/plugins//centreon_awa_jmx.pl \
    --plugin=apps::java::awa::jmx::plugin \
    --mode=queue \
    --custommode=jolokia \
    --url='' \
    --username='' \
    --password='' \
    --filter-name='' \
    --warning-status='' \
    --critical-status='%\{status\} !~ /GREEN/i' \
    --use-new-perfdata 
```

La commande devrait retourner un message de sortie similaire à :

```bash
OK: All queues are ok 
```

Dans cet exemple, une alarme de type CRITICAL sera déclenchée si le statut de la 
queue renseignée via la macro de service FILTERNAME n'est pas égal à "GREEN".
(`--critical-status='%{status} !~ /GREEN/i'`).

La liste de toutes les options complémentaires et leur signification peut être
affichée en ajoutant le paramètre `--help` à la commande:

```bash
/usr/lib/centreon/plugins//centreon_awa_jmx.pl \
    --plugin=apps::java::awa::jmx::plugin \
    --mode=queue \
    --help
```

Tous les modes disponibles peuvent être affichés en ajoutant le paramètre 
`--list-mode` à la commande:

```bash
/usr/lib/centreon/plugins//centreon_awa_jmx.pl \
    --plugin=apps::java::awa::jmx::plugin \
    --list-mode
```

### Diagnostic des erreurs communes

Rendez-vous sur la [documentation dédiée](../getting-started/how-to-guides/troubleshooting-plugins.md)
pour le diagnostic des erreurs communes des Plugins Centreon.