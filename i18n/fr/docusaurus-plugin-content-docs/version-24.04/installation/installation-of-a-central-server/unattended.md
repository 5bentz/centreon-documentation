---
id: unattended-install-central
title: Installation silencieuse d'un serveur central
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Pour installer un serveur central plus rapidement, vous pouvez utiliser un script. Le script exécutera la procédure d'installation complète, installation web incluse.

## Procédure d'installation

1. Mettez votre système à jour :

<Tabs groupId="sync">
<TabItem value="RHEL 8" label="RHEL 8">

```shell
dnf update
subscription-manager register --username my_username --password my_password --auto-attach --force
subscription-manager repos --enable codeready-builder-for-rhel-8-x86_64-rpms
```

> Remplacez **my_username** et **my_password** par les identifiants de votre compte RedHat.

</TabItem>

<TabItem value="Alma / Oracle Linux 8" label="Alma / Oracle Linux 8">

```shell
dnf update
```

</TabItem>
<TabItem value="RHEL 9" label="RHEL 9">

```shell
dnf update
subscription-manager register --username my_username --password my_password --auto-attach --force
subscription-manager repos --enable codeready-builder-for-rhel-9-x86_64-rpms
```

</TabItem>
<TabItem value="Alma / Oracle Linux 9" label="Alma / Oracle Linux 9">

```shell
dnf update
```

</TabItem>
<TabItem value="Debian 11 & 12" label="Debian 11 & 12">

```shell
apt update && apt upgrade
```

</TabItem>
</Tabs>

2. Téléchargez le script à l'aide de la commande suivante :

```shell
curl -L https://download.centreon.com/24.04/unattended.sh --output /tmp/unattended.sh
```

3. Exécutez la commande suivante en **root** :

* Pour spécifier le mot de passe du compte **admin** par défaut :

```shell
bash /tmp/unattended.sh install -t central -v 24.04 -r stable -s -p <admin_password> -l DEBUG  2>&1 |tee -a /tmp/unattended-$(date +"%m-%d-%Y-%H%M%S").log
```

* Pour obtenir un mot de passe autogénéré pour le compte **admin** par défaut (le script vous indiquera où le mot de passe est stocké) :

```shell
bash /tmp/unattended.sh install -t central -v 24.04 -r stable -s -l DEBUG  2>&1 |tee -a /tmp/unattended-$(date +"%m-%d-%Y-%H%M%S").log
```

Dans les deux cas, vous obtiendrez un fichier de log complet avec toutes les erreurs dans votre répertoire **tmp**, fichier nommé **unattended(date).log**.

> Pour obtenir de l'aide sur le script, utilisez la commande suivante :`bash unattended.sh -h`

4. Configurez Centreon

Connectez-vous à l'interface web de Centreon avec l'URL `http://[SERVER_IP]/centreon` en remplaçant [SERVER_IP] par l'adresse IP de votre serveur.
Une fois connecté, suivez les instructions décrites [ici](../../web-and-post-installation/#initialization-of-the-monitoring).

5. Commencez à utiliser Centreon
Suivez notre [guide de démarrage](../../getting-started/welcome.md) pour commencer à superviser.
