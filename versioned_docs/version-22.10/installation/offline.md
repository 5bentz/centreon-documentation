---
id: offline
title: Offline installation
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

To be able to install Centreon on servers with no internet access, create a local copy of the Centreon repository on a server that has an internet access, then make your offline Centreon servers point to it.

## Creating a local copy of the Centreon repository

1. Install Centreon repository on your mirror server.

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```shell
dnf install -y dnf-plugins-core
dnf config-manager --add-repo https://packages.centreon.com/rpm-standard/22.10/el8/centreon-22.10.repo
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```shell
yum install -y yum-utils
yum-config-manager --add-repo https://packages.centreon.com/rpm-standard/22.10/el7/centreon-22.10.repo
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
echo "deb https://packages.centreon.com/apt-standard-22.10-stable $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/centreon.list
echo "deb https://packages.centreon.com/apt-plugins-stable/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/centreon-plugins.list
```

</TabItem>
</Tabs>

2. Retrieve the gpg key for the packages:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```shell
rpm --import https://yum-gpg.centreon.com/RPM-GPG-KEY-CES
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```shell
rpm --import https://yum-gpg.centreon.com/RPM-GPG-KEY-CES
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
wget -O- https://apt-key.centreon.com | gpg --dearmor | tee /etc/apt/trusted.gpg.d/centreon.gpg > /dev/null 2>&1
```

</TabItem>
</Tabs>

3. Create a directory for the local repository:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

   ```shell
   mkdir -p /var/www/html/repos/centreon
   ```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

   ```shell
   mkdir -p /var/www/html/repos/centreon
   ```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
mkdir /var/www/html/centreon
```

</TabItem>
</Tabs>

4. Install the required packages:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```shell
yum install yum-utils createrepo httpd
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```shell
yum install yum-utils createrepo httpd
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
apt install apache2 debmirror
```

</TabItem>
</Tabs>

5. Synchronize the repositories:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

```shell
reposync -p /var/www/html/repos/centreon/ --repo centreon-stable-noarch
reposync -p /var/www/html/repos/centreon/ --repo centreon-stable
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```shell
reposync -p /var/www/html/repos/centreon/ --repo centreon-stable-noarch
reposync -p /var/www/html/repos/centreon/ --repo centreon-stable
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
debmirror \
-a amd64 \
--no-source \
-s main \
-h apt.centreon.com \
-d bullseye \
-r /repository/22.10 \
--keyring=/etc/apt/trusted.gpg.d/centreon.gpg \
--method=https \
/var/centreon-mirror/22.10
```

</TabItem>
</Tabs>

6. Run the following commands:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

Create the repository:

```shell
createrepo /var/www/html/repos/centreon/
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

Create the repository:

```shell
createrepo /var/www/html/repos/centreon/
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

Make the local synchronized repository availble via Apache:

```shell
ln -s /var/centreon-mirror/22.10 /var/www/html/centreon/22.10
```

</TabItem>
</Tabs>

7. Start the web server:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8"> 

```shell
service httpd start
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```shell
service httpd24-httpd start
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
systemctl start apache2
```

</TabItem>
</Tabs>

8. On your Centreon server, edit the following file:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8"> 

```shell
vi /etc/yum.repos.d/centreon.repo
```

Add the following lines:

```shell
[centreon]
name=centreon
baseurl=http://<mirror_ip_address>/repos/centreon
gpgcheck=1
enabled=1
```

> Replace `<mirror_ip_address>` by the actual address of your local repository.

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

```shell
vi /etc/yum.repos.d/centreon.repo
```

Add the following lines:

```shell
[centreon]
name=centreon
baseurl=http://<mirror_ip_address>/repos/centreon
gpgcheck=1
enabled=1
```

> Replace `<mirror_ip_address>` by the actual address of your local repository.

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

```shell
vi /etc/apt/sources.list.d/centreon.list
```

Add the address of the mirror repository and comment the address of the official Centreon repository:

```shell
deb http://`<mirror_ip_address>`/centreon/22.10 bullseye main
#deb https://apt.centreon.com/repository/22.10/ bullseye main
```

> Replace `<mirror_ip_address>` by the actual address of your local repository.

</TabItem>
</Tabs>

## Keeping your local repository up-to-date

To synchronize your mirror with the Centreon repository regularly, create a cron file:

```shell
cd  /var/spool/cron
crontab -e
```

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

The following commands will schedule a synchronization every day at 2 for the **centreon-stable-noarch** repository, and every day at 3 for the **centreon-stable** repository :

```shell
* 2 * * * reposync -p /var/www/html/repos/centreon/ -r centreon-stable-noarch
* 3 * * * reposync -p /var/www/html/repos/centreon/ -r centreon-stable
```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

The following commands will schedule a synchronization every day at 2 for the **centreon-stable-noarch** repository, and every day at 3 for the **centreon-stable** repository :

```shell
* 2 * * * reposync -p /var/www/html/repos/centreon/ -r centreon-stable-noarch
* 3 * * * reposync -p /var/www/html/repos/centreon/ -r centreon-stable
```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

The following command will schedule a synchronization every day at 1:

```shell
* 01 * * * debmirror -a amd64 --no-source -s main -h apt.centreon.com -d bullseye -r /repository/22.10 --keyring=/etc/apt/trusted.gpg.d/centreon.gpg --method=https /var/centreon-mirror/22.10 >> /var/log/debmirror.log
```

</TabItem>
</Tabs>
