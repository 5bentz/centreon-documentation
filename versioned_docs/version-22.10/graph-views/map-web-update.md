---
id: map-web-update
title: Updating MAP
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

Use the following procedure to update your MAP version:

1. Stop the **centreon-map-engine** service by running this command on the machine hosting the Centreon MAP service:
 
  ```shell
  sudo systemctl stop centreon-map-engine
  ```

2. Update the packages by running this command on the machine(s) hosting the central service and the Centreon MAP service:

<Tabs groupId="sync">
<TabItem value="Alma / RHEL / Oracle Linux 8" label="Alma / RHEL / Oracle Linux 8">

 - On the central server:
 
 ``` shell
 sudo dnf update centreon-map-web-client
 ```
 
 - On the MAP server:
 
 ``` shell
 sudo dnf update centreon-map-engine
 ```

</TabItem>
<TabItem value="CentOS 7" label="CentOS 7">

 - On the central server:
 
 ``` shell
 sudo yum update centreon-map-web-client
 ```
 
 - On the MAP server:
 
 ``` shell
 sudo yum update centreon-map-engine
 ```

</TabItem>
<TabItem value="Debian 11" label="Debian 11">

 - If MAP only is installed:
 
 On the central server:

 ``` shell
 sudo apt install centreon-map-web-client
 ```

 On the MAP server:

 ``` shell
 sudo apt install centreon-map-engine
 ```

 - If MAP and MAP Legacy are installed on the same server:
   
   - Make a backup of the **map.cnf** file:
    
    ```shell
    cp /etc/my.cnf.d/map.cnf /etc/my.cnf.d/map.cnf.bk
    ```

   - Update the centreon-map-engine package
    
    On the central server:
    
    ``` shell
    sudo apt install -o Dpkg::Options::="--force-overwrite" centreon-map-web-client
    ```
    
    On the MAP server:
    
    ``` shell
    sudo apt install -o Dpkg::Options::="--force-overwrite" centreon-map-engine
    ```
    
   - Retrieve the configuration file backup:
   
    ```shell
    cp /etc/my.cnf.d/map.cnf.bk /etc/my.cnf.d/map.cnf
    ```

   - Answer **Y** when prompted. Then restart MySQL:
   
    ```shell
    systemctl restart mariadb
    ```

</TabItem>
</Tabs>

3. Clear your browser cache.

4. Finalize the update of the module and the widget in the Centreon interface **Administration > Extensions > Manager**.

5. Restart the **centreon-map-engine** service using the following command:
 
  ```shell
  sudo systemctl start centreon-map-engine
  ```
