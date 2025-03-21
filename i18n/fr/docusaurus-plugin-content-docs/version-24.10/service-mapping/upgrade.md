---
id: upgrade
title: Monter de version l'extension
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Prérequis

### Licence

Si vous mettez à jour d'une version inférieure à 18.10 vers une version
supérieure à 18.10, une nouvelle licence doit être récupérée auprès du
support Centreon.

### Mettre à jour Centreon web sur votre serveur central

Voir le [chapitre correspondant](../upgrade/introduction.md).

### Installer le dépôt Business

Lorsque vous mettez à jour vers une nouvelle version majeure ou
mineure (c'est à dire version A.B.x avec A ou B qui évolue), contactez
le support pour récupérer l'adresse du nouveau dépôt.

### Mettre à jour la clé de signature RPM

Pour des raisons de sécurité, les clés utilisées pour signer les RPMs Centreon sont changées régulièrement. Le dernier changement a eu lieu le 14 octobre 2021. Lorsque vous mettez Centreon à jour depuis une version plus ancienne, vous devez suivre la [procédure de changement de clé](../security/key-rotation.md#installation-existante), afin de supprimer l'ancienne clé et d'installer la nouvelle.

## Mise à jour du paquet

Afin de mettre à jour le module **Centreon BAM**, lancer la commande
ci-dessous :

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```shell
dnf update centreon-bam-server
```

</TabItem>
<TabItem value="Alma / RHEL / Oracle Linux 9" label="Alma / RHEL / Oracle Linux 9">

```shell
dnf update centreon-bam-server
```

</TabItem>
<TabItem value="Debian 12" label="Debian 12">

```shell
apt install --only-upgrade centreon-bam-server
```

</TabItem>
</Tabs>

## Mise à jour de l'interface

Se connecter à l'interface web de Centreon et se rendre dans le menu
`Administration > Extensions > Gestionnaire`.

Un bouton orange de mise à jour est visible et signale qu'une mise à
jour est disponible, cliquez dessus pour mettre à jour le module, faire
de même pour le widget.
