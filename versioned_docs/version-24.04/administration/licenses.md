---
id: licenses
title: Licenses
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


## How can I obtain a license?

* You can request your token for the [free IT-100 edition](../getting-started/it100.md) on our website.
* If you have purchased a license, request your license files from our [support](https://support.centreon.com) team.

## Types of license

According to your [Centreon edition](https://www.centreon.com/en/editions/), your license can be:
- online: uses a token. Your Centreon platform must be connected to the internet.
- offline: uses one or several license files

## Which modules require a license?

The following modules need to be installed separately and require a valid license.

- [Monitoring Connectors](../monitoring/pluginpacks.md#installation)
- [Auto Discovery](../monitoring/discovery/installation.md)
- [Anomaly Detection](../monitoring/anomaly-detection.md)
- [Service mapping (BAM)](../service-mapping/install.md)
- [Graphical views (MAP)](../graph-views/introduction-map.md)
- [Reporting (MBI)](../reporting/installation.md)

## Viewing license-based modules

Go to **Administration > Extensions > Manager**. All modules currently installed on your platform have a green button with a white check mark in it. Modules that require a license have a colored banner at the bottom (red if you have no valid license, green if you have one).

![image](../assets/administration/licenses.png)

## Adding a license to your Centreon platform

<Tabs groupId="sync">
<TabItem value="Online licenses" label="Online licenses">

> Refer to the [tables of network flows](../installation/technical.md#tables-of-network-flows) to integrate your monitoring platform.

To use an online license, your Centreon platform must be connected to the internet.

#### Check the internet connection

Make sure your Centreon platform is allowed to reach the internet:

- Check that the machine can access this URL: https://api.imp.centreon.com

- If needed, set a proxy server:
  - Go to the **Administration > Parameters > Centreon UI** page, then the **Proxy options** section.
  - Click **Test Internet Connection**. The "Connection Successful" message should appear.

#### Add your license

1. Make sure you have your license token (provided by our support team).

2. Go to **Administration > Extensions > Manager**.

3. Click **Add Token**. A popup window appears.

4. Paste your token in the popup window, and then click **Add**.

    - If your token contains one license, a confirmation message appears.

    - If your token contains several licenses, choose the license you want and then click **Choose**. 

    Press **Esc** to close the popup window. The license is applied and the corresponding modules display their validity date:
    
    ![image](../assets/administration/license_valid.png)

    The **Add token** button changes to become a **View license** button.

</TabItem>
<TabItem value="Offline licenses" label="Offline licenses">

1. To request your license:

    1. Go to **Administration > Extensions > Manager**.

    2. Click **Get fingerprint**.

    3. Paste the fingerprint in an email to our [support](mailto:support@centreon.com) team requesting the license.

2. Once you have received your license, in the **Administration > Extensions > Manager** page, click **Upload license**.

5. Browse to the file and then click **OK**. The license is applied and the corresponding modules display their validity date:
    
    ![image](../assets/administration/license_valid.png)

6. If you have several licenses (e.g. for BAM, MBI, etc.), repeat the steps above until you have uploaded all license files.

</TabItem>
</Tabs>

## Free IT-100 license

See chapter [Set up your free IT-100 solution](../getting-started/it100.md).

## Troubleshooting licenses

### "No valid file uploaded"

![image](../assets/administration/license_not_valid.png)

Check the contents of the following directory:

```shell
ls -lah /etc/centreon/license.d/
```

If the directory already contains licenses with rights that are not **apache/apache**, delete them or change their rights so that they can be overwritten by the new licenses:

```shell
chown apache:apache /etc/centreon/license.d/*
chmod 640 /etc/centreon/license.d/*
```

### "Your EPP license is not valid"

* Check that the fingerprint of the central server (on the **Administration > Extensions > Manager** page) matches the fingerprint in the license.

    ```shell
    less /etc/centreon/license.d/epp.license
    ```

* Check that you do not have more hosts than your license allows. Use the following command:

    ```sql
    SELECT COUNT(*) FROM centreon.host WHERE host_register='1';
    ```
